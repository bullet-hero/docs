---
title: 게시
date: 2026-10-11
tags: [level_author]
---

# 게시

레벨은 레벨 설정의 "게시" 탭에서만 보냅니다: 아카이브로 보내거나 Steam 창작마당에 올립니다. 보고서가 레벨을 스스로 검사하며, 보고서에 오류가 있으면 보낼 수 없습니다

## "게시" 탭

`게시`는 레벨 설정의 탭입니다. 레벨을 어디로든 보내는 곳은 여기뿐입니다

위쪽의 `{{ui:editor_share_destination}}`에 선택한 전송 방식이 표시됩니다. 누르면 `{{ui:editor_share_pick-title}}`이(가) 열립니다: 이 빌드가 이 기기에서 제공하는 방식들이 한 줄 설명과 함께 나옵니다.
기본으로 `{{ui:editor_share_archive}}`이(가) 선택되어 있습니다. 마지막 선택은 게임을 닫을 때까지 기억됩니다

그 아래에는:
- 방식 자체의 설정
- 방식의 보고서
- 실행 버튼: `{{ui:editor_share_export}}` 또는 `게시`

이 빌드가 이 기기에서 제공하는 방식이 없으면 탭에 `{{ui:editor_share_none}}`이(가) 표시됩니다

## 보고서

보고서는 스스로 검사합니다: 방식을 열 때와 그 방식의 설정이 하나라도 바뀔 때. 검사 버튼은 없습니다.
보고서는 `오류: N, 경고: N, 조언: N` 줄로 시작하고, 그 뒤에 문제마다 한 줄씩 이어집니다

오류가 있으면 실행할 수 없습니다. 경고와 조언은 판단에 맡깁니다

레벨을 어떤 규칙으로 판정할지는 방식이 정합니다. `{{ui:editor_share_archive}}`은(는) `{{ui:editor_publish_profile-local}}` 세트로, `{{ui:editor_share_steam}}`은(는) 창작마당 규칙으로 검사합니다. 각 세트가 요구하는 것과 각 판정의 뜻 - [[5_publish-readiness]]

## 전송 방식

| 방식 | 사용할 수 있는 곳 | 보내는 것 |
|---|---|---|
| `{{ui:editor_share_archive}}` | 저장 대화 상자가 있는 모든 기기. iOS 제외 | 레벨, 컬렉션 또는 리소스 하나를 파일로 |
| `{{ui:editor_share_steam}}` | Steam 빌드 전용 | 레벨 또는 직접 만든 컬렉션 |

이 빌드나 이 기기에 없는 방식은 목록에 아예 나오지 않습니다

## 아카이브

레벨의 경우:

| 요소 | 하는 일 |
|---|---|
| `{{ui:editor_share_format}}` | 일곱 가지 내보내기 모드 중 하나. 일반 폴더부터 비밀번호로 보호된 아카이브까지 |
| `{{ui:editor_share_passphrase}}` | 보호 모드에서만 보입니다. 비밀번호가 비어 있으면 보호 모드는 실행되지 않습니다 |
| `{{ui:editor_share_export}}` | 지정한 곳에 레벨을 씁니다 |

각 모드가 무엇을 쓰고 무엇으로 여는지 - [[13_export-and-protection#레벨 내보내기]]

컬렉션이나 리소스 하나의 경우 `{{ui:editor_share_format}}`은(는) 그중 다섯 모드를 제공하며, 모두 아카이브입니다. 폴더 모드는 없습니다:

| `{{ui:editor_share_format}}` | 결과물 | 여는 방법 |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | 파일 하나 | Windows 탐색기에서 더블 클릭, 따로 설치할 것이 없습니다 |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | AES-256 암호화가 내장된 zip | 7-Zip 등의 압축 프로그램, 비밀번호를 묻습니다 |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | zip 전체를 OpenPGP(으)로 감싼 것 | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | 파일 하나 | 아무 압축 프로그램 |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | tar.gz 파일을 OpenPGP(으)로 감싼 것 | gpg |

`{{ui:editor_share_passphrase}}`은(는) 비밀번호 모드 세 가지에서 나타납니다. 비밀번호가 비어 있으면 아무것도 내보내지 않습니다.
아래의 컬렉션 검사가 같은 `{{ui:editor_publish_profile-local}}` 규칙으로 적용됩니다

## Steam 창작마당

Steam 빌드 전용입니다. 요소:

| 요소 | 하는 일 |
|---|---|
| `{{ui:editor_publish_visibility}}` | 아이템을 볼 수 있는 사람: `{{ui:editor_publish_visibility-public}}`, `{{ui:editor_publish_visibility-friends-only}}`, `{{ui:editor_publish_visibility-private}}`. 기본값은 `{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | 이번 업로드의 변경 사항 메모. 여러 줄 필드이며 라벨은 별도 줄에 있습니다 |
| `제목과 설명을 올릴 언어` | 아이템의 텍스트를 어떤 언어로 가져올지(아래 참조) |
| `{{ui:editor_share_steam-descriptors}}` | 체크 상자 다섯 개, Steam 자체의 콘텐츠 설명자(아래 참조) |
| `게시` | 레벨을 업로드합니다 |

레벨은 항상 창작마당 규칙으로 검사합니다. 여기서는 규칙을 고를 수 없습니다

창작마당 아이템은 레벨에서 채워집니다:
- 제목과 설명은 레벨의 이름과 설명이며, 한 언어로 올라갑니다
- 미리 보기는 레벨 커버이며, png 또는 jpg, 1 MB 이하입니다. 그 밖의 커버는 건너뛰며, 아이템은 그림 없이 업로드됩니다
- 태그는 게임이 직접 정합니다. 아래 "창작마당 태그"를 참조하십시오

`게시`를 처음 누르면 아이템이 생성됩니다. 그다음부터는 같은 아이템이 업데이트됩니다.
게임은 직접 게시한 아이템 중에서 레벨 자체의 ID 값으로 그 아이템을 찾으므로 레벨에는 아무것도 저장되지 않습니다

보호된 레벨은 게시할 수 없습니다. 자세히 - [[13_export-and-protection]]

레벨 메타데이터에서 `{{ui:settings_level-settings_metadata-level-ai-share}}`을(를) 해제하지 않는 한, 업로드에는 AI 어시스턴트가 레벨에 대한 메모를 보관하는 레벨의 `ai` 폴더가 포함됩니다. 구독하는 사람은 모두 레벨과 함께 그 폴더를 받습니다. 자세히 - [[7_ai-assistant#ai 폴더]]

> [!warning] 경고
> Steam 창작마당 법적 계약에 동의하지 않았다면 아이템은 업로드되지만 숨겨진 상태로 남습니다. 아이템 페이지에서 계약에 동의하십시오. 게임이 그 페이지를 Steam 오버레이로 엽니다

### 제목 언어

Steam에서는 아이템마다 제목 하나와 설명 하나가 표시됩니다. 게임은 다음 순서로 처음 찾은 언어를 사용합니다:
1. `{{ui:settings_game-editor_title}}` 설정의 `{{ui:settings_game-editor_publish-language}}`: `{{ui:enum_publish-language_english}}`(기본값) 또는 기기의 언어인 `{{ui:enum_publish-language_system}}`. 자세히 - [[14_editor-settings]]
2. 사용자 자신의 언어, 즉 게임 인터페이스의 언어
3. 영어
4. 텍스트를 처음 작성한 언어

설명은 제목과 언어가 맞도록 제목의 언어에서 먼저 찾습니다.
현지화되지 않은 이름(일반 텍스트)은 쓴 그대로 올라가며, 그 줄에 `{{ui:editor_share_steam-language-as-written}}`이(가) 표시됩니다

### 콘텐츠 설명자

`{{ui:editor_share_steam-descriptors}}`에는 Steam 자체의 콘텐츠 설명자인 체크 상자 다섯 개가 있습니다:
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

설명자는 게시할 때마다 전송되며 레벨에는 저장되지 않습니다. 게시할 때마다 전체 세트가 전송되므로, 체크를 해제한 상자는 이미 게시된 아이템에서도 해당 설명자를 제거합니다.
설명자는 업로드 직후 두 번째 업데이트로 올라갑니다. 이 부분이 실패해도 아이템은 게시된 상태이며, 결과에 설명자가 설정되지 않았다고 표시됩니다

### 게시 후

성공하면 양식에 어떤 아이템이 생성되거나 업데이트되었는지와 `{{ui:editor_publish_open-item}}` 버튼이 표시됩니다. 이 버튼은 Steam에서 아이템 페이지를 엽니다

실패하면 양식에 다음이 표시됩니다:
- 쉬운 말로 된 이유, `게시하지 못했습니다: ...`
- `전송한 내용과 Steam의 응답: ...` - 영어로 된 기술적인 줄입니다. 문제를 보고할 때 개발자에게 이 줄을 그대로 전달하는 것이 좋습니다
- Steam에서 이 방식이 거부되는 이유를 펼쳐 보여 주는 `?`, 그리고 세 링크: `{{ui:editor_publish_help-docs}}`(이 페이지), `{{ui:editor_publish_help-steam-support}}`, `{{ui:editor_publish_help-agreement}}`

게시에 관한 게임 자체의 로그 줄은 인터페이스 언어와 관계없이 항상 영어입니다

| 이유 | 해결 방법 |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | Steam 클라이언트를 실행하고 Steam에서 게임을 다시 시작합니다 |
| `{{ui:enum_workshop-failure_not-owner}}` | 그 계정으로 게시하거나, 레벨의 사본을 만들면 새 아이템으로 올라갑니다 |
| `{{ui:enum_workshop-failure_access-denied}}` | 계정이 게임을 소유하지 않았거나, 계정이 제한되어 있거나(아직 Steam에서 구매한 적이 없음), 창작마당이 그 계정에 닫혀 있습니다 |
| `{{ui:enum_workshop-failure_invalid-param}}` | 게임의 창작마당이 업로드용으로 설정되어 있지 않거나, Steam 클라이언트가 다른 게임의 ID 값으로 실행 중입니다. Steam 클라이언트와 게임을 다시 시작합니다 |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | 창작마당 파일에서 오래된 아이템을 삭제합니다 |
| `{{ui:enum_workshop-failure_connection}}` | 연결 상태와 Steam 상태를 확인합니다 |
| `{{ui:enum_workshop-failure_invalid-request}}` | 제목은 128자 이하, 설명은 8000자 이하, 미리 보기는 1 MB 이하의 png 또는 jpg |
| `{{ui:enum_workshop-failure_staging}}` | 디스크 여유 공간을 확인하고, 레벨 파일이 다른 프로그램에서 열려 있지 않은지 확인합니다 |

새 아이템이 생성되었지만 업로드가 거부되면 게임은 그 빈 아이템을 삭제합니다. 그래서 창작마당에 방치된 아이템이 남지 않습니다

## Steam 미포함 빌드

Steam 미포함 빌드에서는 목록에 `{{ui:editor_share_steam}}`이(가) 표시되지 않습니다. `{{ui:editor_share_archive}}`은(는) 남아 있습니다

## 컬렉션 공유 방법

컬렉션은 "라이브러리" 탭의 컬렉션 페이지에서 공유합니다. `{{ui:editor_share_share}}`은(는) 같은 패널을 창으로 엽니다: `{{ui:editor_share_archive}}`, 그리고 Steam 빌드에서는 직접 만든 컬렉션에 한해 `{{ui:editor_share_steam}}`도 있습니다

컬렉션 검사:
- 이름이 있습니다
- 라이선스가 명시되어 있습니다
- 비어 있지 않습니다
- 컬렉션이 이름으로 가리키는 모든 파일이 컬렉션 안에 있습니다
- 항목이 참조하는 모든 리소스가 컬렉션에 포함되어 있습니다

라이선스가 없을 때의 처리는 방식에 따라 다릅니다. `{{ui:editor_share_archive}}`에서는 경고이며 내보내기가 실행됩니다. `{{ui:editor_share_steam}}`에서는 오류입니다.
오류가 있으면 실행할 수 없습니다. 컬렉션에 대해 자세히 - [[16_library-and-collections]]

## 리소스 하나 공유 방법

라이브러리의 모든 테마, 도형, 이펙트, 프리팹 행에도 `{{ui:editor_share_share}}` 버튼이 있습니다.
이 버튼은 리소스와 그 리소스에 필요한 모든 것(예: 프리팹의 도형, 텍스처, 중첩 프리팹)을 항목 하나짜리 컬렉션으로 묶습니다

`{{ui:editor_share_archive}}`만 사용할 수 있으며, 컬렉션과 같은 다섯 형식을 비밀번호 형식까지 포함해 제공합니다. 받는 사람은 다른 컬렉션과 마찬가지로 `{{ui:editor_library_import-archive}}`(으)로 그 파일을 가져옵니다

## 창작마당 태그

태그는 게임이 직접 정합니다:

| 아이템 | 태그 |
|---|---|
| 레벨 | `level` |
| 컬렉션 | `collection`, 그리고 안에 든 종류마다 하나씩: `prefabs`, `themes`, `shapes`, `effects` |

텍스처, 폰트, 오디오는 태그를 받지 않으며 단독으로는 창작마당에 올라가지 않습니다. 이들은 컬렉션의 프리팹, 테마, 도형, 이펙트가 사용하는 것으로서 컬렉션 안에 들어갑니다. 미디어만 있는 컬렉션은 이유를 알려 주는 줄과 함께 거부되며, 그런 컬렉션은 아카이브로 공유하는 것이 좋습니다

> [!info] 참고
> Steam 자체의 "컬렉션"은 창작마당 아이템을 엮은 목록으로, Valve의 기능입니다. Bullet Hero의 컬렉션과는 아무 관계가 없습니다

## 구독

Steam 빌드는 구독한 항목을 읽습니다:
- 레벨은 레벨 목록의 `{{ui:editor_library-source_workshop}}` 아래에 나타납니다, [[2_playing-levels]]
- 컬렉션은 에디터 라이브러리의 `{{ui:editor_library-source_workshop}}` 칩 아래에 읽기 전용으로 나타납니다

다음: [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
