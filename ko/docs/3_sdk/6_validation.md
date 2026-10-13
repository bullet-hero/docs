---
title: 검증
date: 2026-10-01
tags: [developer, level_author]
---

# 검증

검증은 ValidationFacade 클래스로 직접 호출하며, 저장과 불러오기에 내장되어 있지 않습니다. 문제는 Error, Warning, Advice 세 그룹으로 나뉘고, ValidateAndFix 메서드는 고칠 수 있는 것을 고칩니다

어디에서 실행할지는 게임이 정합니다. 에디터에서 레벨을 열면 문제를 보고하지만, 플레이할 때는 검사를 건너뜁니다. 그래서 검증을 기다리는 것은 제작자이고, 플레이어는 기다리지 않습니다

레벨 제작자는 서비스에 레벨을 제출할 때 검증을 만납니다. 자세히 - [[7_publish-profiles]]

## 호출 방법

`ValidationFacade` 클래스가 유일한 진입점입니다. 호출하는 쪽은 패스가 몇 개인지 알 필요가 없습니다:

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| 메서드 | 하는 일 |
|---|---|
| `Validate(root, settings)` | 모든 루트를 검사합니다: `Level`, `LevelMeta`, `UserSettings`, 독립된 `Prefab` 또는 `EffectData`. 그래프 패스는 `Level` 루트에서만 실행됩니다 |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | 고칠 수 있는 것을 고치고 남은 것을 보고합니다 |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | 세 패스를 한 번에 실행하며, 아무것도 고치지 않습니다. 메타데이터만 평가하려면 `level` 인수에 `null` 값을 넘길 수 있습니다 |

`ValidationReport` 객체에는 `RuleIssues`, `GraphIssues` 목록이 있습니다:
- `IsValid` - 문제가 하나도 없음
- `HasErrors` - `Error` 그룹의 문제가 하나 이상 있음

## 심각도

모든 규칙은 `RuleGroup` 중 하나에 속합니다:
- `Error` - 파일을 기록된 그대로 플레이할 수 없음
- `Warning` - 플레이는 되지만 의도대로가 아님(한 번도 나타나지 않는 내용, 대체값이 있는 깨진 참조). 또는 유일한 수정 방법이 파괴적임
- `Advice` - 플레이 결과는 바뀌지 않음

## 세 가지 패스

| 패스 | 확인하는 것 | 대상 |
|---|---|---|
| `RuleAnalyzer` | 모든 값이 범위 안에 있는지, `null` 값이 아닌지, 알려진 enum 멤버인지 | 모든 루트 |
| `LevelGraphAnalyzer` | 오브젝트끼리 서로 맞는지 | `Level` 루트만 |
| `PublishReadinessAnalyzer` | 주어진 프로필에 따라 레벨을 모르는 사람에게 넘겨도 되는지 | `LevelMeta`, 선택적으로 `Level` |

## 규칙

타입은 `[RuleContainer]` 표식으로 검사에 포함됩니다. 그 속성에는 규칙 특성이 붙습니다:
- `[RuleNotNull]`, `[RuleInRange]`, `[RuleMinValue]`, `[RuleEnumValid]`, `[RuleCollectionMaxCount]` 등
- `[RuleEnumFlagsValid]` - 플래그 enum용
- `[RuleOptional]` - 없어도 되는 필드용

한도 자체는 `Rules/` 테이블의 상수입니다: `FrameRules`, `ValueRules`, `LevelRules` 등. 예를 들어 `LevelRules.MaxObjects` 값은 262,144입니다

모든 규칙 컨테이너를 도는 순회 코드는 리플렉션 없이 `BH.SDK.Roslyn` 생성기가 만듭니다. 큰 레벨에서는 이 덕분에 순회 시간이 대략 절반으로 줄어듭니다

## 수정

모든 규칙 특성은 자기 값을 수정할 수 있습니다(`Fix`).
`RuleFixer` 클래스는 추적 순서의 역순으로 수정을 적용합니다: 수정 하나가 더 깊은 곳의 문제를 옮겨 놓을 수 있기 때문입니다. `ValidateAndFix` 메서드는 결과가 더 이상 바뀌지 않을 때까지 패스를 반복합니다

그래프 패스는 수정 뒤에 실행됩니다. 수정 자체가 그래프에 문제를 만들 수 있습니다. 예를 들어 새 ID가 기존 ID와 겹치는 경우입니다

**그래프 문제는 절대 수정되지 않습니다:** `DuplicateObjectId`, `MissingParent`, `ParentCycle`, `PrefabRemapBroken`, `IdCounterNearExhaustion` 등. 이런 수정은 모두 내용에 관한 결정입니다(두 오브젝트 중 어느 쪽이 ID를 유지할지). 추측으로 고치면 레벨이 다시 쓰입니다

> [!caution] 주의
> `ValidateAndFix` 메서드는 넘겨준 객체를 변경합니다. 원본이 필요하다면 사본에서 실행하십시오. 예를 들어 제작자에게 정확히 무엇이 바뀌었는지 보여 줘야 하는 경우입니다
