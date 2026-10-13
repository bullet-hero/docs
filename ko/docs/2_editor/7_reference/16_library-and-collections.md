---
title: 라이브러리와 컬렉션
date: 2026-10-02
tags: [level_author]
---

# 라이브러리와 컬렉션

컬렉션에는 여러 레벨에서 재사용하는 리소스가 들어 있습니다. 레벨은 컬렉션을 참조하지 않습니다: 가져오기를 하면 리소스가 레벨 안으로 복사되므로 레벨은 어디서나 플레이됩니다

## 컬렉션이란

**컬렉션**은 재사용할 수 있는 리소스의 폴더입니다. 일곱 종류의 리소스를 담을 수 있습니다:

| 종류 | 저장 방식 |
|---|---|
| 프리팹, 테마, 도형, 이펙트 | 데이터, 항목마다 파일 하나 |
| 텍스처, 폰트, 오디오 | 미디어 파일 |

컬렉션은 레벨에 묶여 있지 않습니다. 기기에 있으며 어떤 레벨을 열어도 사용할 수 있습니다

## 출처

라이브러리는 세 출처의 리소스를 보여 줍니다. 각 출처는 목록 위의 필터 칩입니다:

| 칩 | 내용 | 변경 가능 |
|---|---|---|
| `{{ui:editor_library-source_library}}` | 이 기기의 공유 라이브러리: `resources/prefabs`, `themes`, `shapes`, `effects` | 예 |
| `{{ui:editor_library-source_local}}` | 직접 만든 컬렉션, `resources/collections` | 예 |
| `{{ui:editor_library-source_workshop}}` | Steam 창작마당에서 구독한 컬렉션. 제자리에서 읽습니다. Steam 빌드 전용 | 아니요 |

읽기 전용 컬렉션은 이렇게 바꿉니다: 그 항목을 직접 만든 컬렉션으로 복사합니다

## "라이브러리" 탭

`{{ui:settings_editor-settings_library}}`은(는) 에디터 홈 화면의 마지막 탭으로, `{{ui:settings_editor-settings_community}}` 다음에 있습니다

좁은 버튼 열에서 종류를 고릅니다:
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`, `{{ui:editor_library_kind-themes}}`, `{{ui:editor_library_kind-shapes}}`, `{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`, `{{ui:editor_library_kind-fonts}}`, `{{ui:field_common_audio}}`

그 오른쪽에 페이지 제목(왼쪽)과 버튼(오른쪽)이 한 줄로 놓입니다. 목록은 그 아래에 있습니다.
목록이 비어 있으면 가운데에 그렇다고 표시됩니다

`{{ui:editor_library_kind-prefabs}}`부터 `{{ui:field_common_audio}}`까지 일곱 종류의 페이지에서는 `{{ui:editor_library_copy-target}}`이(가) 제목 아래에 전체 너비의 별도 줄을 차지합니다. 출처 칩은 그 아래 줄에 있습니다

라이브러리 창(컬렉션 카드, 텍스처 그림, 공유 창)은 모서리의 X 표시로 닫습니다. `{{ui:editor_library_close}}` 버튼은 없습니다

모든 행은 버튼입니다. 누르면 종류별 주요 동작을 합니다:

| 종류 | 행을 누르면 |
|---|---|
| 컬렉션 | 페이지를 엽니다 |
| 테마, 도형, 이펙트 | 에디터를 엽니다 |
| 텍스처 | 그림과 크기를 보여 줍니다 |
| 프리팹, 폰트, 오디오 | 아무 일도 없습니다. 오디오 행에는 자체 재생 버튼이 있습니다 |

행 오른쪽의 작은 버튼은 나머지 동작이고, 휴지통 아이콘은 삭제하거나 제거합니다

`{{ui:editor_library_open-folder}}`은(는) 현재 페이지의 폴더를 시스템 파일 관리자에서 보여 줍니다. Windows, macOS, Linux에서만 사용할 수 있습니다

### 컬렉션

`{{ui:editor_library_open-folder}}`와(과) `{{ui:editor_library_refresh}}`은(는) 페이지 제목 오른쪽에 있습니다. `새 컬렉션`과 `{{ui:editor_library_import-archive}}`은(는) 그 아래의 별도 줄에 오른쪽 정렬로 있습니다

- `새 컬렉션`은 빈 컬렉션을 생성하고 그 카드를 엽니다
- `{{ui:editor_library_import-archive}}`은(는) `.zip` 또는 `.tar.gz` 파일이나 비밀번호로 보호된 아카이브(자체 비밀번호가 있는 `.zip`, `.zip.gpg`, `.tar.gz.gpg`)에서 컬렉션을 추가합니다. 그 컬렉션이 이미 기기에 있으면 교체할지 묻습니다

비밀번호로 보호된 아카이브는 `{{ui:editor_library_passphrase-title}}` 창을 엽니다: `{{ui:editor_library_passphrase-needed}}`. 비밀번호를 입력하고 `{{ui:editor_library_open}}`을(를) 누릅니다.
비밀번호가 틀리면 `{{ui:editor_library_passphrase-wrong}}`이(가) 표시됩니다
- `{{ui:editor_library_open-folder}}`은(는) `resources/collections` 폴더를 엽니다
- `{{ui:editor_library_refresh}}`은(는) 폴더를 다시 읽습니다

직접 만든 컬렉션에는 `{{ui:editor_library_edit}}`와(과) 휴지통 아이콘이 있습니다. 휴지통은 먼저 확인을 받은 뒤 컬렉션을 모든 파일과 함께 삭제합니다

### 컬렉션 카드

`{{ui:editor_library_edit}}`은(는) 컬렉션 카드 창을 엽니다:
- `{{ui:editor_library_field-name}}`, `{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`, 쉼표로 구분
- `{{ui:editor_library_field-license}}`: `{{ui:editor_library_license-unspecified}}` 또는 일반적인 라이선스 중 하나
- `{{ui:editor_library_set-cover}}`은(는) png 이미지를 고릅니다. 옆의 줄에 커버가 있는지 표시됩니다

`{{ui:editor_save_text}}`은(는) 카드를 씁니다. `{{ui:editor_cancel_text}}`, X 표시 또는 창 바깥 클릭은 변경 사항을 버립니다

### 컬렉션 페이지

| 요소 | 하는 일 |
|---|---|
| `{{ui:settings_common_back}}` | 목록으로 돌아갑니다 |
| `{{ui:editor_library_edit}}` | 카드를 엽니다. 직접 만든 컬렉션에만 있습니다 |
| `{{ui:editor_share_share}}` | 공유 창을 엽니다: 비밀번호 유무와 관계없이 `.zip` 또는 `.tar.gz`(으)로 `{{ui:editor_share_archive}}`, Steam 빌드에서는 직접 만든 컬렉션에 한해 `{{ui:editor_share_steam}}`도 있습니다 |
| `{{ui:editor_library_open-folder}}` | 컬렉션 자체의 폴더를 엽니다 |
| `{{ui:editor_library_delete}}` | 먼저 확인을 받고 컬렉션을 삭제합니다 |

그 아래에 내용이 있습니다. 행은 해당 종류의 페이지에서와 같은 방식으로 항목을 열고, 휴지통 아이콘은 컬렉션에서 항목을 제거합니다

읽기 전용 컬렉션에는 `{{ui:editor_library_read-only}}`이(가) 표시됩니다

`{{ui:editor_share_share}}`에 대해 자세히 - [[17_publishing]]

### 프리팹, 테마, 도형, 이펙트

이 페이지들은 모든 출처의 모든 항목을 보여 줍니다. 칩으로 목록을 좁힙니다

`{{ui:editor_library_copy-target}}`은(는) 직접 만든 컬렉션 중 하나를 고릅니다. 기본값은 `{{ui:editor_library_copy-target-none}}`입니다. 대상을 고르면 다른 곳에서 온 모든 행에 `{{ui:editor_library_copy-to}}`이(가) 생깁니다

테마, 도형, 이펙트는 레벨 설정에서와 같은 에디터에서 열립니다. `{{ui:editor_save_text}}`은(는) 항목이 있는 곳, 즉 `{{ui:editor_library-source_library}}` 또는 직접 만든 컬렉션에 변경 사항을 씁니다.
창작마당에서 온 항목은 읽기 전용으로 열리고 `{{ui:editor_save_text}}`은(는) 꺼져 있습니다. 바꾸려면 직접 만든 컬렉션으로 복사하십시오

`{{ui:editor_library_new-entry}}`은(는) 에디터에서 새 테마, 도형, 이펙트를 만듭니다. 항목은 대상 컬렉션에, 대상을 고르지 않았다면 `{{ui:editor_library-source_library}}`에 저장됩니다. 프리팹은 레벨 안에서 만들며 `{{ui:editor_library_new-entry}}`이(가) 없습니다

변경할 수 있는 항목에는 휴지통 아이콘이 있으며, 먼저 확인을 받습니다

모든 행에 `{{ui:editor_share_share}}`이(가) 있습니다. 이 버튼은 항목과 그 항목에 필요한 모든 것(예: 프리팹의 도형, 텍스처, 중첩 프리팹)을 항목 하나짜리 컬렉션으로서 `.zip` 또는 `.tar.gz`에 묶습니다. 비밀번호는 걸어도 되고 걸지 않아도 됩니다. 받는 사람은 다른 컬렉션과 마찬가지로 `{{ui:editor_library_import-archive}}`(으)로 그 파일을 가져옵니다

`{{ui:editor_library_open-folder}}`은(는) 해당 종류의 공유 라이브러리 폴더를 엽니다. 예: `resources/themes`

### 텍스처, 폰트, 오디오

이 페이지들은 모든 컬렉션의 파일을 보여 줍니다. 파일용 개인 라이브러리는 없으므로 이 종류는 컬렉션에만 있습니다

- 텍스처 행은 그림을 보여 줍니다
- 오디오 행에는 재생 버튼이 있습니다. 한 번에 한 트랙만 재생되며, 페이지를 벗어나면 멈춥니다
- 폰트 행에는 미리 보기가 없습니다

`{{ui:editor_library_add-file}}`은(는) 기기의 파일을 대상 컬렉션에 넣으므로, 대상이 없으면 버튼이 꺼져 있습니다. 텍스처는 png 또는 jpg, 폰트는 ttf 또는 otf, 오디오는 mp3, wav, ogg입니다.
컬렉션에 바이트가 똑같은 파일이 이미 있으면 아무것도 추가되지 않으며 게임이 그렇다고 알려 줍니다

행에는 `{{ui:editor_library_copy-to}}`와(과) 휴지통 아이콘이 있습니다

### 복사할 때 함께 가져가는 것

복사는 항목에 필요한 모든 것을 가져갑니다: 프리팹의 도형, 텍스처, 폰트, 중첩 프리팹, 이펙트의 파티클 도형.
그 리소스들의 저작자 정보도 함께 갑니다

## "컬렉션" 탭

`{{ui:editor_library_kind-collections}}`은(는) 레벨 설정의 탭으로, `{{ui:editor_library_kind-prefabs}}` 바로 다음에 있습니다. 위쪽에 두 모드가 있습니다: `가져오기`와 `{{ui:editor_collections_mode-build}}`

### 가져오기

1. 탭에 컬렉션 목록이 표시됩니다. 필요한 컬렉션을 누릅니다
2. 필요한 항목에 체크합니다. `{{ui:editor_collections_select-all}}`와(과) `{{ui:editor_collections_select-none}}`은(는) 모두 체크하거나 모든 체크를 해제합니다
3. `선택: N, 추가되는 종속 항목: M` 줄이 레벨에 무엇이 들어올지 보여 줍니다. 종속 항목은 저절로 추가됩니다
4. `가져오기`를 누릅니다

가져오기 전체가 실행 취소 한 단계입니다

텍스처, 폰트, 오디오는 레벨에서 새 ID 값을 받고, 파일은 고유한 이름으로 레벨 폴더에 복사됩니다.
레벨에 바이트까지 똑같은 파일이 이미 있으면 다시 복사하지 않습니다: 가져오기는 레벨에 있는 텍스처, 폰트, 트랙을 사용합니다

### 컬렉션 만들기

1. `{{ui:editor_collections_target}}`에서 `새 컬렉션` 또는 직접 만든 컬렉션 중 하나를 고릅니다. 새 컬렉션은 `{{ui:editor_library_field-name}}` 필드에서 이름을 가져옵니다
2. 일곱 종류 중 어떤 것이든 레벨의 리소스에 체크합니다
3. `{{ui:editor_collections_build}}`을(를) 누릅니다

새 컬렉션은 레벨의 제작자를 물려받습니다

보호된 레벨로는 컬렉션을 만들 수 없습니다. 자세히 - [[13_export-and-protection]]

## 리소스 선택과 검색

검색과 리소스 선택 창에는 프리팹, 테마, 도형, 이펙트용 `{{ui:settings_editor-settings_library}}` 단계가 있습니다. 이 단계는 모든 출처를 보여 줍니다.
리소스 선택 창은 도형, 콜라이더, 이펙트, 테마 필드와 `{{ui:cmd_editor_place-prefab}}`입니다

라이브러리에서 항목을 고르면 종속 항목과 함께 레벨로 가져와 할당합니다. 충돌이 있으면 "컬렉션" 탭에서와 같은 질문을 합니다

레벨의 리소스 탭 안에 있는 라이브러리 브라우저도 같은 방식으로 동작하며 출처 칩을 보여 줍니다. 자세히 - [[11_level-resources]]

## 충돌

가져오는 항목이 같은 ID 값으로 이미 레벨에 있을 수 있습니다:
- 내용이 같으면 아무것도 할 필요가 없습니다
- 내용이 다르면 `{{ui:editor_resource-conflict_title}}` 창이 열립니다

창에는 모든 충돌이 나열되며, 각각 `{{ui:editor_resource-conflict_copy}}` 토글이 있습니다:

| 선택 | 결과 |
|---|---|
| 유지(토글 꺼짐) | 레벨의 버전이 남아 사용됩니다 |
| `{{ui:editor_resource-conflict_copy}}` | 컬렉션의 버전이 새 ID 값으로 추가됩니다. 함께 가져온 모든 것은 이 사본을 참조합니다 |

`{{ui:editor_resource-conflict_all-keep}}`와(과) `{{ui:editor_resource-conflict_all-copy}}`은(는) 모든 토글을 한 번에 설정합니다. `가져오기`는 선택을 적용하고, `{{ui:editor_cancel_text}}`은(는) 아무것도 가져오지 않습니다

어떤 버전도 조용히 이기지 않습니다. 내용이 다른 충돌은 모두 이 창에서 결정합니다

## 저작자 정보

레벨 리소스에 대한 기록은 텍스처, 폰트, 오디오뿐 아니라 테마, 이펙트, 도형, 프리팹도 다룹니다.
가져오기는 필요한 기록을 레벨로 복사하므로 저작자 정보가 리소스와 함께 들어옵니다

자세히 - [[4_resource-record]]

## 디스크에서

컬렉션은 게임 데이터 폴더의 `resources/collections/<collection-guid>/`에 있습니다. 이 기기의 공유 라이브러리가 있는 곳, 즉 `levels` 옆의 바로 그 `resources` 폴더입니다. 자세히 - [[4_level-folder-and-backups]]

| 경로 | 내용 |
|---|---|
| `collection.json` 또는 `collection.blob` | 매니페스트: 이름, 설명, 제작자, 라이선스, 텍스처, 폰트, 오디오 항목, 그리고 안에 있는 모든 것의 저작자 정보 |
| `cover.png` | 커버, 선택 사항 |
| `prefabs/`, `themes/`, `shapes/`, `effects/` | 항목마다 `<guid>.json` 또는 `<guid>.blob` 하나. 이 기기의 공유 라이브러리와 같은 파일입니다 |
| `media/` | 텍스처, 폰트, 오디오 파일 |

컬렉션은 아카이브로 전달합니다: 컬렉션 페이지의 `{{ui:editor_share_share}}`, 목록의 `{{ui:editor_library_import-archive}}`.
컬렉션이 아닌 아카이브는 거부됩니다

다음: [[17_publishing]], [[2_reuse]], [[4_resource-record]]
