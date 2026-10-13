---
title: 레벨 플레이
date: 2026-10-11
tags: [player]
---

# 레벨 플레이

레벨 목록에서 레벨을 고르고 플레이 조건을 정한 다음 시작합니다. 다른 사람의 레벨은 평범한 폴더입니다: 레벨 폴더에 복사하고 목록을 새로 고치면 됩니다

## 메인 메뉴

| 버튼 | 기능 |
|---|---|
| `{{ui:menu_main_levels-btn}}` | 레벨 목록, 아래에서 설명합니다 |
| `{{ui:menu_main_editor-btn}}` | 레벨 에디터, [[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | 레벨이 없는 아레나와 튜토리얼, [[13_sandbox]] |
| `{{ui:settings_common_title}}` | 모든 설정, [[4_settings]] |
| `{{ui:menu_main_story-btn}}` | 아직 작동하지 않습니다 |
| `{{ui:menu_main_multiplayer-btn}}` | 아직 작동하지 않습니다 |

## 레벨 목록

메인 메뉴의 `{{ui:menu_main_levels-btn}}` 버튼을 누르면 레벨 목록이 열립니다. 레벨은 세 곳에서 옵니다:

- `{{ui:root_level-source_local}}` - `levels` 폴더, [[1_installation]]
- `{{ui:root_level-source_builtin}}` - 게임과 함께 제공되는 레벨
- `창작마당` - Steam 빌드 전용입니다. 구독한 레벨을 보여 줍니다. 구독한 리소스 컬렉션은 레벨이 아닙니다: 에디터의 라이브러리에 나타납니다, [[16_library-and-collections]]

위쪽에는 검색 필드, `{{ui:root_level-browser_sort}}`, `{{ui:root_level-browser_layout}}`(그리드 또는 목록), `{{ui:root_level-browser_filters}}` 버튼이 있습니다. 목록은 그리드로 열립니다. 정렬 기준은 `{{ui:root_level-browser_sort-relevance}}`, `{{ui:root_level-browser_sort-title}}`, `{{ui:root_level-browser_sort-duration}}`, `{{ui:root_level-browser_sort-progress}}`, `{{ui:root_level-browser_sort-recent}}` 중에서 고를 수 있습니다. 정렬 버튼 옆의 화살표(`{{ui:root_level-browser_reverse}}`)는 순서를 뒤집습니다. `{{ui:root_level-browser_sort-relevance}}` 정렬에는 방향이 없습니다

검색은 먼저 레벨 이름을, 그다음 제작자를, 그다음 태그를 봅니다

`{{ui:root_level-browser_filters}}` 버튼은 추가 필터 창을 엽니다. 누를 때마다 뒤에 있는 목록이 바로 바뀝니다:

- `{{ui:root_level-filters_ai}}` - `{{ui:root_level-filters_ai-yes}}`, `{{ui:root_level-filters_ai-no}}`, `{{ui:root_level-filters_ai-unspecified}}`
- `{{ui:root_level-filters_length}}` - 가장 짧은 레벨과 가장 긴 레벨, 그리고 길이를 알 수 없는 레벨을 표시할지 여부
- `{{ui:root_level-filters_progress}}` - `{{ui:root_level-filters_progress-unplayed}}`, `{{ui:root_level-filters_progress-started}}`, `{{ui:root_level-filters_progress-cleared}}`, `{{ui:root_level-filters_progress-bot}}`
- `{{ui:root_level-filters_recent}}` - 최근 24시간, 7일 또는 30일
- `{{ui:root_level-filters_age}}` - 표시할 최고 연령 등급
- `{{ui:root_level-filters_other}}` - 비밀번호가 있는 레벨 숨기기, 더 새로운 버전의 게임에서 만든 레벨 숨기기
- `{{ui:root_level-filters_tags}}` - 태그를 한 번 누르면 필수, 두 번 누르면 제외

`{{ui:root_level-filters_progress}}`, `{{ui:root_level-filters_recent}}` 필터는 메인 메뉴의 목록에만 있습니다. 에디터의 목록에는 자체 필터가 있습니다. 버튼에는 켜진 필터의 수가 표시되고, `{{ui:root_level-browser_reset}}` 버튼은 필터를 모두 끕니다. 필터는 게임을 닫을 때까지 유지됩니다

폴더에 레벨을 복사했습니까? `{{ui:root_level-browser_refresh}}` 버튼을 누르면 목록이 갱신됩니다

카드의 자물쇠는 레벨이 비밀번호로 보호되어 있다는 뜻입니다

카드를 길게 누르거나 마우스 오른쪽 버튼으로 클릭하면 메뉴가 열립니다: `{{ui:level_passphrase_open}}`, `{{ui:root_level-browser_delete}}`. `창작마당` 레벨에서 `{{ui:root_level-browser_delete}}` 항목을 고르면 아이템 구독이 취소되고 파일이 삭제됩니다. 이때 Steam 클라이언트가 실행 중이어야 합니다: 그렇지 않으면 Steam 클라이언트가 레벨을 다시 다운로드합니다. 기본 제공 레벨은 삭제할 수 없습니다

## 다른 사람의 레벨 추가하기

레벨은 평범한 파일 폴더입니다. 압축해서 친구에게 보낼 수 있습니다

**폴더.** 레벨 폴더를 `levels` 폴더에 복사하고 `{{ui:root_level-browser_refresh}}` 버튼을 누릅니다. 레벨 폴더 자체를 복사해야 합니다: `level.json` 파일(또는 `level.blob` 파일)과 `metadata.json` 파일이 들어 있는 폴더입니다

**아카이브.** 에디터를 열고 `{{ui:gen_level_archive}}` 생성기로 새 레벨을 생성합니다. 그다음 `{{ui:editor_create-level_archive-choose}}` 버튼으로 파일을 고릅니다

| 파일 | 결과 |
|---|---|
| `.zip`, `.tar.gz` | 열립니다 |
| 자체 비밀번호가 있는 `.zip`, `.zip.gpg`, `.tar.gz.gpg` | `{{ui:editor_create-level_archive-protected}}` 메시지 다음에 열립니다 |
| `.7z` | 지금은 거부됩니다. zip 형식으로 다시 압축하세요 |
| 그 밖의 파일 | 거부됩니다, [[5_troubleshooting]] |

이름을 바꾼 아카이브도 열립니다: 게임은 파일의 바이트로 형식을 인식합니다. 이전 버전의 게임에서 만든 아카이브는 가져올 때 업데이트됩니다

기본적으로 가져온 레벨에는 자체 ID가 부여됩니다. 그래서 기기에 이미 있는 레벨을 덮어쓰지 않습니다

자세히 - [[6_sharing-by-hand]]

## 레벨 화면

레벨 화면에는 커버, 제작자, 설명, 음악 제작자가 표시됩니다. `{{ui:level_level-view_authors}}`, `{{ui:level_level-view_licenses}}` 버튼도 있습니다

제작자 이름과 음악 줄은 레벨 메타데이터에 링크가 있으면 그 링크를 엽니다

연령 등급은 레벨 제작자가 정합니다. 게임은 이를 확인하지 않습니다

"AI 생성 콘텐츠 포함" 문구는 제작자가 레벨, 커버 또는 리소스 중 하나를 AI로 생성했다고 밝혔을 때 표시됩니다. 이것 역시 제작자 자신의 신고입니다. 이 문구가 없다고 "AI 없음"이라는 뜻은 아닙니다: 제작자가 아무것도 밝히지 않았을 수도 있습니다

플레이하기 전에 조건을 고를 수 있습니다:

| 조건 | 선택지 |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}` (플레이가 끝나지 않음), `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}`, `{{ui:menu_levelview_options-lifes_option-custom}}` (최대 16까지의 슬라이더) |
| `{{ui:field_common_speed}}` | `0.5`, `1.0`, `2.0`, `{{ui:menu_levelview_options-lifes_option-custom}}` (최대 2까지의 슬라이더). 레벨과 음악이 함께 바뀝니다 |
| `체크포인트` | 켜기 또는 끄기, [[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | 켜기 또는 끄기. 아바타가 모든 것을 통과합니다, [[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`, [[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | 숫자, `{{ui:level_level-view_seed-randomize}}`, `{{ui:level_level-view_seed-clear}}`. `0` - 플레이할 때마다 새 시드, [[8_determinism]] |

`플레이` 버튼을 누르면 플레이가 시작됩니다

일시 정지 메뉴에는 `{{ui:game_pause-window_continue-btn}}`, `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}` (체크포인트에 도달한 뒤), `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}`, `{{ui:game_game-result_back-to-menu}}` 버튼이 있습니다. `{{ui:game_game-result_back-to-options}}` 버튼은 플레이를 시작한 조건 그대로 레벨 화면으로 돌아가고, 에디터에서 시작한 플레이라면 에디터의 `플레이` 탭으로 돌아갑니다

## 결과 창

창에는 `통과` 또는 `{{ui:game_game-result_lose}}` 문구와 세 섹션이 표시됩니다: `진행 상황`, `{{ui:game_game-result_section-damage}}`, `{{ui:game_game-result_section-conditions}}`

- 행: `완료율`, `{{ui:game_game-result_checkpoint}}`, `{{ui:field_common_time}}`, `{{ui:game_game-result_length}}`, `{{ui:game_game-result_hits}}`, `{{ui:game_game-result_lives-left}}`, `{{ui:game_game-result_streak}}`
- 플레이 조건: `{{ui:field_common_speed}}`, `{{ui:menu_levelview_options-lifes_title}}`, `{{ui:menu_levelview_options-bot}}`, `{{ui:game_game-result_seed}}`, `체크포인트`. `{{ui:menu_levelview_options-no-collision_title}}` 플레이에서는 `{{ui:menu_levelview_options-lifes_title}}` 항목에 `· 충돌 없음` 문구가 덧붙습니다
- 버튼: `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}`, `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}`, `{{ui:game_game-result_back-to-menu}}`

기본적으로 패배해도 창이 열리지 않습니다. 대신 플레이가 마지막 체크포인트로 되감깁니다. 바꾸려면 - `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`

## 기록

레벨 화면에는 기록 블록이 있습니다: `{{ui:menu_levelview_record-best}}`, `{{ui:menu_levelview_record-attempts}}`, `{{ui:menu_levelview_record-clears}}` (또는 `{{ui:menu_levelview_record-none}}`)

조건 조합마다 별도의 기록이 있습니다: 목숨, 속도, 체크포인트, 충돌, 봇. 블록에는 지금 선택한 조건의 기록이 표시됩니다. 시도 횟수와 클리어 횟수는 모든 플레이에서 집계됩니다

기록을 고르는 방식 - [[10_statistics]]

## 카드 표시

| 표시 | 의미 |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | 창작마당 폴더가 디스크에 있지만 구독하지 않은 상태입니다. `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` 옵션이 켜져 있을 때만 보입니다 |
| `{{ui:root_level-entry_unverified}}` | 레벨 소스가 응답하지 않았습니다 |
| `{{ui:root_level-entry_newer-version}}`, `{{ui:root_level-entry_newer-file}}` | 이 버전의 게임은 레벨을 열지 않습니다, [[5_troubleshooting]] |
| `{{ui:root_level-entry_level-missing-badge}}` | 폴더에 `level.json` 파일이 없어서 레벨을 시작할 수 없습니다, [[4_level-folder-and-backups]] |
| `{{ui:root_level-entry_meta-missing-badge}}` | 폴더에 읽을 수 있는 `metadata.json` 파일이 없습니다. 카드에는 폴더 이름이 표시되고, 레벨은 플레이됩니다, [[4_level-folder-and-backups]] |

## 레벨 삭제

카드를 길게 누르거나 마우스 오른쪽 버튼으로 클릭 → `{{ui:root_level-browser_delete}}`. 게임은 먼저 확인을 요청합니다

레벨과 함께 통계(`{{ui:root_level-delete_statistics}}`)와 백업(`{{ui:root_level-delete_backups}}`)도 삭제할 수 있습니다

보호된 레벨을 삭제할 때는 비밀번호가 필요 없습니다
