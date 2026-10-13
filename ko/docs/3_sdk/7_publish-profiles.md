---
title: 게시 프로필
date: 2026-10-01
tags: [developer, level_author]
---

# 게시 프로필

서비스는 어떤 레벨을 받는지 PublishProfile 파일로 기술합니다: 라이선스, 리소스 출처, 필수 필드, 크기 한도. 서비스를 추가하려면 분석기를 고치는 대신 파일을 하나 작성하면 됩니다

## 프로필은 데이터입니다

게시 프로필(`PublishProfile`)은 다른 루트와 똑같이 직렬화되는 모델이며, 자기 세대를 가집니다

레벨은 Steam 창작마당, 공식 서버, 커뮤니티 서버, 스토어 빌드의 카탈로그로 갈 수 있습니다. 각 장소는 같은 질문에 저마다 다르게 답합니다. 답은 해가 지나며 바뀌지만, 코드는 바뀌지 않습니다

프로필이 정하는 것:

| 필드 | 의미 |
|---|---|
| `ProfileKey` | 어떤 서비스인지, 모든 보고서에 반복해서 표시됩니다 |
| `AllowedLicenses` | 서비스가 받는 `TypicalLicenseType` 값 |
| `AllowedUriTypes` | 리소스를 가져올 수 있는 방식. 빈 목록이면 어떤 방식이든 허용 |
| `AllowUnknownLicense`, `AllowPermissionInstead` | 알 수 없는 라이선스나 서면 허가로 충분한지 |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution`, `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | 반드시 채워야 하는 것 |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | 크기 한도, 0 값은 한도 없음 |
| `Sources`, `UnknownSourceTrust` | 사이트 목록과, 목록에 없는 사이트의 등급 |

어떤 라이선스를 받을지는 프로필만 정합니다. 라이선스의 속성처럼 보이지만 실제로는 받는 서비스의 속성입니다

## 내장 프로필 네 가지

| 팩토리 | `ProfileKey` | 용도 |
|---|---|---|
| `CreateOpen()` | `local` | 기기에 있는 레벨. 필수 항목 없음 |
| `CreateStandard()` | `standard` | 공개 서버 |
| `CreateWorkshop()` | `workshop` | Steam 창작마당. CC BY 계열은 모두 통과하고, 빠진 문서는 경고만 합니다 |
| `CreateStrict()` | `strict` | 스토어 빌드, `standard` 프로필보다 엄격함 |

| 항목 | `standard` | `strict` |
|---|---|---|
| 라이선스 | CC0 1.0, CC BY 4.0 및 3.0, CC BY-NC 4.0 및 3.0, SIL OFL 1.1, MIT, Apache 2.0, the Unlicense | `standard` 프로필과 같음 |
| 리소스 출처 | 레벨 폴더, 게임, 또는 직접 링크 | 링크 불가 |
| 저작자 표시와 해시 | - | 필수 |
| 리소스당 한도 | 64 MiB | 32 MiB |
| 데이터 파일당 한도 | 32 MiB | 16 MiB |
| 레벨당 한도 | 256 MiB | 128 MiB |

> [!tip] 권장
> 서비스용 팩토리를 새로 추가하지 마십시오. 네 프로필 중 하나를 가져와 필요한 필드를 바꾸고 JSON 파일로 배포하는 것이 좋습니다

### 이 라이선스와 크기를 고른 이유

- GPL 계열 라이선스는 `standard` 프로필에서 제외됩니다. App Store에서 배포되는 GPL 저작물은 Apple 약관과 충돌합니다
- CC BY-SA 라이선스는 제외됩니다: ShareAlike 조건 때문에 레벨 자체의 라이선스를 바꿔야 하게 됩니다
- CC BY-ND 라이선스는 제외됩니다: NoDerivatives 조건은 게임의 기반인 편집을 금지합니다
- strict 크기는 휴대폰이 모바일 네트워크로 다운로드할 수 있는 크기입니다

## 리소스의 출처

라이선스 필드는 제작자가 무엇을 주장하는지 말해 줍니다. `SourceTrust` 값은 리소스를 가져온 사이트를 고려할 때 그 주장이 얼마나 믿을 만한지 말해 줍니다:

| 등급 | 결과 | 예 |
|---|---|---|
| `Approved` | 게시 | Kenney, ccMixter, Incompetech |
| `PartiallyApproved` | 게시, 기록은 살펴볼 가치가 있음 | Pixabay, SoundImage |
| `RequiresLicenseCheck` | 실제 페이지에서 라이선스를 확인 | OpenGameArt, Free Music Archive, Wikimedia Commons |
| `RequiresResourceCheck` | 먼저 저작물 자체를 확인 | Rawpixel, itch.io |
| `NotAllowed` | 거부 | YouTube, SoundCloud, Spotify |
| `Unknown` | 기록 없음, `UnknownSourceTrust` 값으로 결정 | - |

`TrustedSourceCatalog.CreateDefault()` 메서드는 사이트 25개를 반환합니다. 이것은 출발점이 되는 목록입니다. 운영자마다 이 목록을 바꿀 것으로 예상합니다. 그러므로 어떤 기록이 반드시 있을 것이라고 기대해서는 안 됩니다

`Sources` 목록이 비어 있으면 출처 등급 평가가 꺼집니다

스트리밍 플랫폼은 목록에서 빠지는 대신 `NotAllowed` 등급으로 올라 있습니다. 목록에 없는 사이트는 `UnknownSourceTrust` 값으로 평가되며, `standard`, `strict` 프로필에서 이 등급은 거부 대신 확인을 요구합니다

카탈로그와 [[ugc-licensing-policy]] 문서는 같은 내용을 다루며 함께 수정됩니다

## 결과로 무엇을 할까

호출할 메서드는 `ValidationFacade.ValidateForPublish`입니다. 자세히 - [[6_validation]]

`PublishReadinessReport` 객체에는 다음이 있습니다:
- `HasErrors` - `Error` 그룹의 문제
- `NeedsManualReview` - `Warning` 그룹의 문제
- `IsReady`

그다음 무슨 일이 일어날지는 프로필이 정하지 않습니다. 클라이언트는 오류가 있으면 업로드를 막습니다. 서버는 레벨을 게시하는 대신 검토 대기열에 넣습니다

제작자 쪽에서 본 같은 검사 - [[5_publish-readiness]]
