---
title: 설치
date: 2026-10-02
tags: [developer, level_author]
---

# 설치

SDK 배포 형태는 nuget.org의 BulletHero.SDK 패키지, 또는 소스에서 빌드한 결과물입니다. Unity에서는 git 서브모듈로 연결하며, ConsoleSmoke 샘플로 레벨이 읽히는지 확인합니다

SDK 코드는 [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk)에 있습니다. 라이선스는 MIT입니다

## .NET

`BulletHero.SDK` 패키지는 nuget.org에 게시되어 있습니다: `dotnet add package BulletHero.SDK`. 의존성 세 개도 함께 설치됩니다. 소스에서 직접 빌드하려면:

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

그다음 둘 중 하나를 연결합니다:
- 로컬 폴더의 `.nupkg`: `dotnet add package BulletHero.SDK --source <folder>`. 의존성 세 개도 함께 설치됩니다
- `BH.SDK.dll` 파일을 직접 연결. 이 경우 아래 세 패키지를 직접 추가합니다: DLL 참조로는 의존성이 따라오지 않습니다

의존성은 모두 NuGet 패키지입니다:

| 패키지 | 버전 | 용도 |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | 비밀번호로 보호된 레벨용 OpenPGP |
| `SharpZipLib` | 1.4.2 | tar, zip (gzip 처리는 BCL에서) |

### 빌드 세부 사항

- 어셈블리 이름은 `BH.SDK.dll`, XML 문서는 같은 위치에 있습니다
- 대상은 `netstandard2.1`, 언어는 C# 9입니다. Unity 프로젝트와 같은 값이므로, 같은 소스가 Unity 안에서도 밖에서도 빌드됩니다
- 출력 폴더는 `bin~`, `obj~`입니다. 물결표가 붙는 이유는 Unity에서 이름이 물결표로 끝나는 폴더를 가져오지 않기 때문입니다

## Unity

게임에서는 git 서브모듈로 SDK 저장소를 연결합니다:

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

제거 명령은 `git rm -r -f Assets/Plugins/BH.SDK`입니다

Unity 프로젝트에서 직접 갖춰야 하는 것:
- `com.unity.nuget.newtonsoft-json` 패키지를 통한 `Newtonsoft.Json`
- NuGet의 `BouncyCastle.Cryptography`, `SharpZipLib` (게임에서는 NuGetForUnity로 설치합니다)
- Player Settings의 스크립팅 정의 심볼 `BHSDK_UNITY`. 이 심볼이 없으면 `UnityIntegration`에서 엔진 없는 분기가 선택됩니다
- SDK 루트의 `BH.SDK.Roslyn.dll`. Unity에서 분석기는 그 폴더의 어셈블리와 그 어셈블리를 참조하는 어셈블리에만 적용됩니다. 다른 곳으로 옮기면 아무것도 분석하지 않습니다

저장소 루트에 `package.json` 파일이 있습니다: 이름은 `com.vertoker.bullet-hero-sdk`, 최소 Unity 버전은 `6000.0`. 따라서 Package Manager에서도 git URL 방식으로 SDK 추가가 가능합니다. 이 방법은 사용하지 않으며 여기서 설명하지 않습니다

## 확인: ConsoleSmoke 샘플

`Samples~/ConsoleSmoke` - `net8.0` 콘솔 애플리케이션입니다. 서드파티 도구와 똑같이 빌드된 `BH.SDK.dll` 파일을 참조합니다.
애플리케이션은 레벨 폴더를 읽고 이름, 오브젝트 수, 세대를 출력합니다. 그다음 레벨을 JSON 형식과 `.blob` 형식으로 각각 왕복 변환합니다

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| 종료 코드 | 의미 |
|---|---|
| 0 | 모두 일치 |
| 1 | 잘못된 인수 |
| 2 | `level.*` 또는 `metadata.*` 파일이 없음 |
| 3 | 왕복 변환 결과가 일치하지 않음 |
| 4 | 파일이 이 SDK보다 새로움 |

게임 내장 레벨 `new-zero-demo`에서의 출력 (`sv 1.0.0` 기준으로 기록):

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

다음 - [[2_level-format]]

## SDK의 구성

| 부분 | 설명 | Unity 필요 여부 |
|---|---|---|
| `BH.SDK` | 핵심: 모델, 직렬화, 버전, 규칙, 검증, 아카이브, 게시, 생성기 | 아니요 |
| `UnityIntegration` | 모든 파일이 Unity 유무와 관계없이 컴파일되는 얇은 계층(`#if BHSDK_UNITY`), 예를 들어 `Cat` 로거 | 아니요: Unity 밖에서는 핵심에 바로 포함되어 컴파일됩니다 |
| `UnityExtensions` | Unity 타입으로의 변환, 2D 트랜스폼, 아바타 이동 | 예, 항상 |
| `BH.SDK.Roslyn` | 분석기와 소스 생성기. `[GenerateModel]` 특성이 붙은 모든 모델에 대해 `Equals`, 복사, JSON 및 `.blob` 코덱, 검증 순회를 작성합니다 | 컴파일 시점에 실행 |

모델 파일에는 필드와 생성자만 있습니다. 반복되는 코드는 모두 생성기가 작성합니다. 그래서 생성되는 일곱 개의 본문 중 어느 하나에서 필드를 빠뜨리는 일이 생기지 않습니다

## 별도 라이브러리인 이유

- **레벨은 게임보다 오래 남습니다.** 레벨은 개방형 형식(JSON, tar.gz, zip, OpenPGP)의 파일로 이루어진 폴더입니다. 그 파일을 읽는 코드도 공개되어 있습니다. 레벨을 만든 게임이 사라져도 레벨은 계속 읽을 수 있습니다
- **다른 리듬 게임과의 연동.** 형식이 공개적으로 설명되어 있으므로, 다른 게임과 상호 변환하는 변환기를 이 설명에 맞춰 만들 수 있습니다
- **빠른 수정.** 형식의 결함은 외부에서도 보입니다. 코드를 읽는 사람이라면 누구나 결함을 보고하거나 수정을 보낼 수 있습니다
- **서드파티 도구.** 변환기, 검증기, 레벨 생성기, 모드가 게임과 같은 모델로 작업합니다. 파일에서 모델을 재구성할 필요가 없습니다
- **서버.** 핵심은 Unity 없이 `netstandard2.1` 대상으로 빌드됩니다. 그래서 서버에서도 클라이언트와 같은 모델에 같은 검사를 실행합니다
