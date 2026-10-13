---
title: 속도와 단축키
date: 2026-10-02
tags: [level_author]
---

# 속도와 단축키

명령 팔레트(Ctrl+Shift+P), 콘텐츠 검색(Ctrl+F), 위치 표시 버튼, 타임라인의 화살표 키가 시간을 가장 많이 아껴 줍니다. 모든 키는 설정에서 다시 할당할 수 있습니다

## 시간을 가장 많이 아끼는 네 가지

- **`{{ui:editor_search-title_command}}`** (`Ctrl+Shift+P`) - 에디터가 할 수 있는 모든 것을 이름으로 검색합니다. 어떤 버튼이 어느 패널에 있는지 기억하는 것보다 빠릅니다
- **`Search Content`** (`Ctrl+F`) - 이름으로 오브젝트나 오디오 트랙에 바로 이동합니다. 재생 헤드도 함께 이동합니다
- **`{{ui:cmd_editor_ping}}`** - 뷰포트가 선택 항목을 화면에 맞추고, 타임라인과 계층 구조가 그 위치로 스크롤됩니다. 모두 한 번에 일어납니다. 다중 선택에서 다시 누르면 다음 오브젝트로 넘어갑니다
- **타임라인의 화살표 키** - 목록 속 순서가 아니라 방향으로 이동합니다. 마우스 없이 이웃한 키프레임 사이를 오갈 수 있습니다

## 기본값

아래의 그룹과 이름은 `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`에 표시되는 것과 같습니다

### 재생

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | 재생 및 일시 정지 |

### 편집

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | 실행 취소 |
| `Ctrl+Y` 또는 `Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | 다시 실행 |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | 저장 |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | 복사 |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | 붙여넣기 |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | 복제 |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | 선택 항목으로 프리팹 만들기 |

### 선택

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | 선택 항목 삭제 |
| `Ctrl` 누른 채로 | `{{ui:settings_keybindings_editor_multi_select}}` | 다중 선택 |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | 모든 선택을 한 번에 해제: 오브젝트, 키프레임, 오디오, 비트 |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | 프리팹 모드에서 나와 레벨로 돌아가기 |

### 보기

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `Ctrl+F` | `Search Content` | 콘텐츠 검색 |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | 명령 실행 |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | 왼쪽 패널 표시 또는 숨기기 |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | 오른쪽 패널 표시 또는 숨기기 |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | 아래쪽 패널 표시 또는 숨기기 |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | 뷰포트 위의 도구 그룹 표시 또는 숨기기 |
| `` ` `` 누른 채로 | `{{ui:settings_keybindings_editor_preview}}` | 미리 보기: 키를 누르고 있는 동안 에디터 인터페이스가 숨겨집니다 |

### 타임라인

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | 접기 순환: 모든 하위 트리, 선택한 종류만, 없음 |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | 스냅 켜기 또는 끄기 |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | 선택 도구 |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | 사각형 선택 도구 |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | 가위 도구 |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | 가장자리 도구 |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | 타임라인에서 선택한 오브젝트 접기 |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | 레벨 타임라인 열기 |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | 로컬 타임라인 열기 |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | 오디오 타임라인 열기 |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | 이벤트 타임라인 열기 |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | 프리팹 타임라인 열기 |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | 템포를 탭으로 입력하는 비트 그리드 창. `{{ui:settings_keybindings_editor_beat_tap}}` 자체에는 기본 키가 없으므로, 필요하면 키를 할당하십시오 |
| `Ctrl` 누른 채 휠 | `{{ui:settings_keybindings_timeline_pan_modifier}}` | 팬 |
| `Shift` 누른 채 휠 | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | 줌 |

`Z X C V B N` 키는 타임라인 툴바를 왼쪽에서 오른쪽으로 따라가고, `Q W E R T` 키는 탭 줄을 따라갑니다. 도구가 더 적은 타임라인은 오른쪽부터 뺍니다: 로컬 타임라인에는 `Z X C V` 키만 있습니다. 열린 타임라인에 해당 도구가 없는 글자 키는 아무 동작도 하지 않습니다

### 기즈모

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | 선택 |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | 위치 |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | 회전 |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | 스케일 |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | 크기 |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | 앵커 |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | 피벗 |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | 숨김: 선택은 유지되지만 핸들도 테두리도 그려지지 않습니다 |

### 창

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | 전체 화면 켜기 또는 끄기. 어느 화면에서나 작동하며, 데스크톱 전용입니다 |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | 설정이 열려 있는 동안 설정을 지금 바로 디스크에 기록합니다. 에디터에서는 `Ctrl+S` 키가 대신 레벨을 저장합니다 |

### 탐색

| 키 | 설정에서의 이름 | 동작 |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | 마지막으로 클릭한 영역에서 위로 이동 |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | 마지막으로 클릭한 영역에서 아래로 이동 |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | 마지막으로 클릭한 영역에서 왼쪽으로 이동 |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | 마지막으로 클릭한 영역에서 오른쪽으로 이동 |

기즈모 숫자 키, 타임라인 글자 키, `Space` 같은 단독 키는 텍스트 필드에 입력하는 동안 아무 동작도 하지 않습니다. 프레임 필드에서 입력한 `2` 때문에 기즈모가 바뀌지는 않습니다

## 타임라인의 화살표 키

화살표 키는 화면에서 그 방향으로 가장 가까운 항목을 고릅니다. 같은 키를 누르면 줌 배율과 상관없이 같은 항목을 찾습니다

- 다중 선택 상태에서는 누른 방향으로 가장 멀리 있는 항목에서 시작합니다. 선택한 블록 안으로 되돌아가지 않습니다
- 화살표 이동은 항상 선택을 교체합니다. 선택에 추가하지는 않습니다
- 타임라인은 새 항목을 보여 주는 데 필요한 만큼만 스크롤됩니다. 재생 헤드 표시를 클릭하면 여전히 화면이 가운데로 맞춰집니다
- 테스트 플레이어가 켜져 있는 동안에는 화살표 키가 타임라인이 아니라 플레이어를 조작합니다. 계층 구조와 `{{ui:settings_level-settings_raw}}` 탭은 클릭해 들어가면 화살표 키를 계속 받습니다

## 레벨 보기

**미리 보기.** `` ` `` 키를 누르고 있으면 에디터 인터페이스가 숨겨지고 레벨만 보입니다. 전환이 아니라 누르고 있는 동안만 작동합니다: 키를 놓으면 모든 것이 돌아옵니다. 레벨, 레터박스 막대, 플레이어, 카메라 경계는 계속 보입니다.
이 기능에는 버튼도 설정도 없습니다. 키는 `{{ui:settings_keybindings_editor_preview}}` 항목에서 다시 할당할 수 있습니다

**뷰포트 그리드**는 툴바 버튼이나 `{{ui:cmd_editor_viewport-grid}}` 명령으로 켜고 끕니다. 처음에는 꺼져 있습니다. 이 동작은 `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`에서 바꾸며, 직접 켰는지 여부는 세션 사이에 기억되지 않습니다

**기즈모 자석**은 기즈모로 드래그하는 것을 그리드에 스냅합니다. 기본으로 켜져 있으며 기즈모 모드와 무관합니다. 툴바 버튼과 `{{ui:cmd_editor_gizmo-magnet}}` 명령으로 켜고 끕니다

**레벨을 살펴볼 때는 일시 정지가 정상 상태입니다.** 재생이 일시 정지된 동안에도 그리드, 콜라이더, 봇 오버레이, 기즈모 핸들, 선택 테두리가 모두 계속 그려집니다. 기즈모 핸들을 잡으면 재생이 일시 정지됩니다

## 키 다시 할당

모든 키는 다시 할당할 수 있습니다: `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

바꾼 키만 저장됩니다. 나머지는 기본값에서 옵니다.
그래서 건드리지 않은 키라면 개선된 기본값이 그대로 적용됩니다.
`{{ui:settings_keybindings_reset}}` 버튼은 변경 사항을 지울 뿐이며, 모든 키가 기본값으로 돌아갑니다

> [!tip] 팁
> 키 표시는 인터페이스에 고정되어 있지 않습니다. 다시 할당하면 명령 팔레트와 모든 컨텍스트 메뉴에 새 키가 즉시 표시됩니다

## 누르는 키와 누르고 있는 키

누르는 키는 보조 키가 정확히 일치할 때만 작동합니다.
`Ctrl+Shift+P` 키를 눌러도 `Ctrl+P` 키는 작동하지 않고, `Ctrl` 키를 누른 채로는 단독 `T` 키가 작동하지 않습니다

누르고 있는 키는 그 보조 키가 눌려 있는 키 중에 있으면 작동합니다. 이미 진행 중인 동작을 세밀하게 조정하는 역할입니다

> [!info] 참고
> 그래서 누르고 있는 키 두 개가 일부러 한 버튼을 공유할 수 있습니다. 다중 선택과 타임라인 팬은 둘 다 `Ctrl` 키에 있지만 서로 방해하지 않습니다

다음: [[1_order-of-work|작업 순서]], [[2_reuse|재사용: 프리팹, 복사, 생성기]]
