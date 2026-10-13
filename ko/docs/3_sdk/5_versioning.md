---
title: 버전 관리와 마이그레이션
date: 2026-10-02
tags: [developer, level_author]
---

# 버전 관리와 마이그레이션

버전은 세 가지입니다: 게임의 gv, SDK의 sv, 모델 형식 세대의 mg. SDK에서는 mg 값을 기준으로 오래된 파일을 마이그레이션하고, 빌드보다 새로운 세대의 파일은 읽기를 거부합니다

## 세 가지 버전

| 라벨 | 뜻 | 버전의 대상 | 위치 |
|---|---|---|---|
| `gv` | `game version` | 게임 클라이언트 | Unity 프로젝트의 `bundleVersion` |
| `sv` | `sdk version` | 라이브러리로서의 SDK, 공개 API 기준 semver | `SdkVersion.Value` |
| `mg` | `model generation` | 모델 형식, 도메인마다 세대 하나 | 모든 루트의 `[ModelGeneration]`, `ModelGenerations.Current` |

현재 버전은 `gv {{v:version.gv}}`, `sv {{v:version.sv}}`, `mg {{v:version.mg}}`입니다

`gv`, `sv` 두 번호는 서로 따라갈 필요가 없지만, 대부분의 경우 일치합니다.
버전은 함께 올리며, 공통 업데이트에는 같은 버전이 붙습니다

각 부분의 의미:
- `gv`: major - 전체 업데이트(스토리, 멀티플레이어), minor - 일반적인 새 기능, patch - 핫픽스
- `sv`, SDK에서 API 안정성을 약속하기 시작한 뒤: major - 호환되지 않는 API 변경(타입 제거, 멤버의 시그니처나 의미 변경), minor - 아무도 대응할 필요가 없는 추가, patch - 시그니처를 바꾸지 않는 수정

**`mg` 값이 다른 무엇보다 중요합니다.** SDK에서는 이 값으로 파일을 마이그레이션할지 읽기를 거부할지 결정합니다

설정 화면에는 세 버전이 이 순서로 라벨과 함께 표시됩니다: `gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`. 라벨이 없으면 버그 보고서에 적힌 같은 숫자 두 개를 구별할 수 없습니다

끝에 `b` 문자와 숫자가 붙은 버전, 예를 들어 `gv 1.1.0b1` 버전은 베타입니다: 테스트용 다음 버전 빌드이며, 보통 Steam 베타 브랜치에서 배포됩니다. 그다음 릴리스는 문자 없이 나옵니다(`gv 1.1.0`). 베타에서 저장한 파일은 이전 릴리스에서 열리지 않을 수 있습니다

> [!warning] 경고
> SDK에서 달리 밝히기 전까지 `sv` 버전은 게임을 따라가며, `sv 1.0.0` 버전은 API 안정성을 약속하지 않습니다. DLL 기반으로 빌드한 코드에는 `sv` major 번호가 아직 호환성에 관해 아무것도 알려 주지 않습니다

## 버전이 아닌 숫자

"버전"처럼 보이지만 버전이 아닌 숫자가 두 개 더 있습니다:
- `LevelMeta.LevelVersion` (키 `vrs`) - 제작자가 정한 레벨 버전, `"1.0"` 같은 문자열
- `BlobFormat.Generation` - `.blob` 형식의 바이트 배치. 자세히 - [[3_blob-format]]

## 세대: 도메인마다 정수 하나

도메인은 하나의 전체로 마이그레이션되는 루트입니다. 도메인은 21개입니다: `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` 등.
`Level` 안의 부분도 여기에 포함됩니다: `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`. 각 도메인은 자기 엔벨로프의 `g` 키에 세대를 기록합니다

| 상수 | 값 | 의미 |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | 세대가 전혀 없음 |
| `ModelGenerations.Test` | 0 | 마이그레이션 경로를 검증하는 `Versions/V0` 뼈대 |
| `ModelGenerations.V1_AlphaRelease` | 1 | `gv 1.0.0` 버전과 함께 출시된 세대, 대부분의 도메인이 아직 이 세대에 있음 |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`, `LevelMeta`, `LevelStatistics`, `GameStatistics`, 그리고 새로운 `Collection` |
| `ModelGenerations.Current` | 최신 | 인터페이스와 보고서에 표시되는 값 |

**세대는 `major.minor` 형태가 아니라 하나의 수입니다.** 파일 형태의 변경에는 마이그레이션이 필요하거나 필요하지 않거나 둘 중 하나입니다. 그 중간 단계는 없습니다

**번호는 하나의 전역 카운터에서 나옵니다.** 변경된 도메인은 자기 다음 빈 번호가 아니라 `ModelGenerations.Current + 1` 값을 받습니다. 바로 이 방식 덕분에 버전 문자열에 있는 하나의 `mg` 값이 의미를 유지합니다

## 새로운 것은 거부됩니다

모델 변경은 모두 새로운 세대입니다. 형태 변경, 필드 추가, 새 enum 값은 똑같이 취급됩니다.
따라서 빌드가 아는 것보다 높은 세대는 그 빌드가 한 번도 본 적 없는 형태임이 확실합니다

예외는 하나입니다: 기존 모델 어디에서도 언급하지 않는 완전히 새로운 모델, 예를 들어 별도 파일에 담긴 아바타 스킨. 이것은 마이그레이션할 원본이 없는 새 도메인이므로 세대가 올라가지 않습니다. 올라가는 것은 그 모델을 참조하기 시작하는 기존 모델의 세대입니다

그런 파일은 아예 읽히지 않습니다: 기본값으로 채우지도, 일부를 건너뛰지도 않습니다. `NewerGenerationException` 예외에는 `Domain`, `FileGeneration`, `BuildGeneration` 값이 담기며, 호스트는 플레이어에게 업데이트를 요청합니다

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## 오래된 것은 마이그레이션됩니다

형태가 바뀌는 도메인은 다음을 받습니다:
1. 전역 카운터에서 나온 새 세대
2. `Versions/V<old>/` 폴더에 있는 이전 형태의 고정 스냅샷: `[GenerateModel]` 특성과 `[ModelGeneration(domain, <old>)]` 특성이 붙은 클래스
3. `Versions/V<old>/Migrations/` 폴더의 `ModelMigration<TFrom, TTo>` 클래스

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` 클래스는 리플렉션으로 스냅샷과 마이그레이터를 찾고, 현재 형태에 이를 때까지 체인을 따라갑니다. 읽는 동안 일어난 손실 있는 대체는 모두 조용히 넘어가지 않고 `SerializationReport`에 기록됩니다

## 읽기 전 거부

`LevelMeta.MinGeneration` (키 `min_generation`) - 레벨의 도메인 중 가장 높은 세대입니다. 저장할 때 `LevelGenerations.Required()` 메서드로 계산되며 직접 입력하지 않습니다

클라이언트는 `level.json` 파일을 열기 전에 이 값을 비교합니다. 그래서 미래의 레벨은 수 메가바이트의 내용을 읽지 않고도 거부됩니다. 아무것도 선언하지 않은 파일에는 `-1` 값이 저장됩니다

결정의 전체 기록 - SDK 저장소의 [VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md)
