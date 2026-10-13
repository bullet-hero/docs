---
title: SDK 기여
date: 2026-10-02
tags: [developer]
---

# SDK 기여

SDK 문제는 bullet-hero/sdk 저장소의 이슈로 보고하고, 코드 변경은 같은 저장소에 풀 리퀘스트로 보냅니다. 기여자 규칙도 같은 저장소의 코드 옆에 있습니다

저장소는 [bullet-hero/sdk](https://github.com/bullet-hero/sdk), 기본 브랜치는 `master`입니다

## 보고할 곳

| 대상 | 보고할 곳 |
|---|---|
| SDK 및 그 코드 | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| 게임: 플레이어의 버그와 요청 | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| 문서 텍스트 | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## 규칙이 있는 곳

기여자 규칙은 SDK 저장소 자체에, 그 규칙이 설명하는 코드 옆에 있습니다:

| 파일 | 내용 |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | 의존성, 레벨 패키지, DLL 및 패키지 빌드, 확인용 샘플 |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | 개념 모델, 폴더 색인, 라이브러리 전체의 규약 |
| 각 폴더의 `CLAUDE.md` | 그 폴더의 지역 규칙, 예: [Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | 버전 축, 세대, 마이그레이션과 거부 |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | 모델이 엔티티를 지정하는 방식: Guid, int, 프레임, 필드 경로 |
| [[ugc-licensing-policy]] (이 사이트) | 사용자 콘텐츠의 라이선스 정책, `TrustedSourceCatalog` 클래스와 함께 수정됨 |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | 스냅샷과 마이그레이터 작성 방법 |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | 생성기 계약 |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | 분석기와 모델 생성기, 다시 빌드하는 방법 |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | 이중 컴파일 계약 |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | `sv` 버전별 변경 사항, 최신 항목이 맨 위 |

## 빌드와 테스트

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- 여기서는 Unity에서 컴파일하는 것과 같은 소스를 Unity 없이 빌드합니다. 엔진 독립 계약을 어기는 파일은 이 빌드를 깨뜨립니다
- 출력은 `bin~`, `obj~` 폴더에 들어갑니다
- pack 명령은 `.nupkg` 파일만 만듭니다. nuget.org 게시는 `sv` 태그가 푸시될 때 저장소의 `release` 워크플로가 수행합니다

> [!caution] 주의
> 분석기와 모델 생성기는 SDK 루트의 미리 빌드된 `BH.SDK.Roslyn.dll` 파일로 배포됩니다. `Roslyn/` 폴더에서 무엇이든 수정했다면 다시 빌드하고 덮어써야 합니다. 그렇지 않으면 소스가 바뀌었는데도 이전 생성기가 계속 실행됩니다

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Unity 에디터 안에서는 메뉴 항목 **Tools > BH.SDK.Roslyn > Build Analyzer**에서 같은 작업을 합니다

## 미리 알아 둘 불변 조건

- 핵심은 `UnityEngine` 타입을 하나도 참조하지 않습니다. 엔진이 필요한 코드는 `UnityExtensions/` 폴더에, 또는 엔진 없는 분기를 갖춘 `#if BHSDK_UNITY` 조건 아래 `UnityIntegration/` 폴더에 들어갑니다
- 코드는 파일과 메모리 내 데이터에서 똑같이 작동하며, BCL의 비동기 기능만 사용합니다
- `netstandard2.1`, C# 9 - Unity 프로젝트가 컴파일할 때 쓰는 값입니다. 이 값은 올리지 않습니다
- 모델은 `[GenerateModel] public sealed partial class` 형태입니다. 직렬화되는 모든 필드는 `Names.cs`에서 키를 가져옵니다
- 모델 변경은 모두 스냅샷과 마이그레이터를 갖춘 새 세대입니다. 자세히 - [[5_versioning]]
- SDK 버전은 세 곳에 있습니다: `SdkVersion.cs`, `package.json`, `BH.SDK.csproj` 파일의 `<Version>`. 이 중 하나만 바뀌면 `SdkVersionAgreementTests` 테스트가 실패합니다
