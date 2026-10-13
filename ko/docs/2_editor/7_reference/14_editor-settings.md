---
title: 에디터 설정
date: 2026-10-11
tags: [level_author]
---

# 에디터 설정

자동 저장, 그리드, 선택, 기즈모, 새 레벨 프리셋을 여기서 설정합니다. 자동 저장은 기본으로 켜져 있으며 편집 후 {{v:editor.autosave-delay}}초가 지나면 실행됩니다

## 레벨 에디터

자동 저장, 카메라, 선택, 파일 형식을 여기서 설정합니다

| 설정 | 하는 일 | 기본값 |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | 자동 저장을 켭니다 | 켜짐 |
| `{{ui:settings_game-editor_autosave-rate}}` | 저장되지 않은 편집이 생긴 뒤 자동 저장까지 몇 초가 지나는지 | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | 사본을 몇 개 보관하는지. 한도에 이르면 가장 오래된 사본이 삭제됩니다 | {{v:editor.autosave-copies}} |

타이머는 저장되지 않은 편집이 있는 동안에만 돌아갑니다

자동 저장 한 번은 두 가지 일을 합니다:
1. 레벨의 사본을 `<game folder>/backups/<level id>/`에 씁니다
2. `Ctrl+S` 단축키와 마찬가지로 레벨 자체를 저장합니다

사본에는 레벨 파일만 들어 있습니다. 복원하는 방법은 두 가지입니다:
- 레벨 설정에서: `{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- 직접: 사본을 레벨 폴더에 `level.json`(또는 `level.blob`) 이름으로 복사합니다

자세히 - [[4_not-losing-work#자동 저장]]

`{{ui:settings_game-editor_camera-min-size}}`와(과) `{{ui:settings_game-editor_camera-max-size}}`은(는) 에디터 뷰포트를 얼마나 확대하고 축소할 수 있는지 제한합니다

`{{ui:settings_game-editor-multi-select-requires_hold}}`와(과) `{{ui:settings_game-editor-pick-invisible_aabb}}`은(는) 뷰포트에서 클릭이 무엇을 뜻하는지 바꿉니다.
선택이 갑자기 익숙한 방식과 다르게 동작한다면 이 두 설정을 확인하십시오

`{{ui:settings_game-editor-level-serialize_mode}}`와(과) `{{ui:settings_game-editor-resources-serialize_mode}}`은(는) 디스크에 쓸 때의 기본 형식을 정합니다

`{{ui:settings_game-editor_publish-language}}`은(는) 창작마당 아이템의 제목과 설명을 어떤 언어로 먼저 게시할지 고릅니다: `{{ui:enum_publish-language_english}}`(기본값) 또는 기기의 언어인 `{{ui:enum_publish-language_system}}`

자세히 - [[3_speed-and-shortcuts]]

## 그리드

뷰포트 그리드는 레벨 뒤에 그려지며 오브젝트 배치를 돕습니다

| 설정 | 하는 일 | 기본값 |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | 에디터를 열 때 그리드가 켜져 있는지. 시작 상태일 뿐입니다 | 꺼짐 |
| `{{ui:settings_game-editor-grid_size}}` | 칸 하나의 한 변, 월드 단위 | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | 선이 얼마나 잘 보이는지, 0에서 1까지 | 0.25 |

툴바의 그리드 버튼으로 그리드를 켜고 끕니다. 이 상태는 세션 사이에 저장되지 않습니다

그리드의 모양:
- 가장자리가 없습니다. 줌에 따라 칸이 10배 단위로 바뀌고, 더 촘촘한 그리드는 서서히 나타납니다
- 어떤 단계의 그리드에 선이 너무 많이 필요하면 그 단계는 성기게 그려지지 않고 꺼집니다
- 선 색상은 항상 현재 프레임의 카메라 배경을 반전한 색이므로 배경이 바뀌어도 그리드가 보입니다. 직접 정하는 것은 불투명도뿐입니다

스냅이 켜져 있으면 위치를 드래그할 때 칸의 절반 단위, 즉 교차점과 칸의 중심에 달라붙습니다. 화면에 보이는 그리드를 기준으로 합니다. 그리드가 꺼져 있으면 위치는 고정된 간격에 달라붙습니다

## 선택

| 설정 | 하는 일 | 기본값 |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | 켜짐: 다중 선택 모드에서 `Ctrl` 키를 누르고 있는 동안에만 클릭이 선택에 추가하고, 일반 클릭은 선택을 교체합니다. 꺼짐: 모드가 켜져 있는 동안 모든 클릭이 선택에 추가합니다 | 켜짐 |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | 선택한 모든 오브젝트의 히트박스를 반투명하게 채워 그립니다 | 꺼짐 |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | 클릭이 오브젝트가 그리는 내용이 아니라 오브젝트의 사각형 전체로 오브젝트를 고릅니다 | 꺼짐 |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | 메뉴가 열리기까지 길게 누르는 시간, 초 단위 | 0.5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | 길게 누르는 동안 커서가 드래그로 바뀌지 않고 움직일 수 있는 거리 | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | 선택한 오브젝트의 히트박스를 얼마나 진하게 그리는지 | 0.5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | 모든 히트박스 보기에서의 같은 값. 그곳에서는 수백 개가 겹치므로 더 옅습니다 | 0.25 |

다중 선택 모드에서 `Ctrl` 키를 떼도 아무것도 해제되지 않고 모드도 끝나지 않습니다. 선택을 교체하는 것은 다음 일반 클릭뿐입니다. 모드에 대해 자세히 - [[4_hierarchy-and-clipboard]]

툴바의 콜라이더 버튼은 프레임 안에 있는 모든 것의 히트박스를 보여 줍니다. 플레이어의 원도 포함됩니다. 이 상태는 세션 사이에 저장되지 않습니다. 화면에 히트박스가 너무 많으면 일부만 그리지 않고 메시지와 함께 보기가 스스로 꺼집니다

콜라이더가 없는 오브젝트는 어느 보기에서도 히트박스를 그리지 않으며, 비활성 오브젝트도 마찬가지입니다

두 보기의 채우기 색상은 `설정 > 그래픽 > 콜라이더만 표시 모드 > 채우기 색상`이며, 게임의 "콜라이더만 표시" 모드([[4_settings]])와 공유합니다. 위의 두 불투명도는 계속 에디터 자체의 설정입니다

## 기즈모

| 설정 | 하는 일 | 기본값 |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | 뷰포트의 드래그 핸들 크기, 0.1에서 10까지. 마우스에 맞춘 핸들은 손가락으로 누르기 어렵습니다 | 1 |

핸들은 줌과 관계없이 화면에서 같은 크기를 유지합니다

## AI 에이전트

`{{ui:settings_game-editor_mcp_title}}`을(를) 켜면 MCP 지원 AI 클라이언트가 열려 있는 레벨을 편집할 수 있습니다. Windows, Linux, Mac에서만 지원합니다: 휴대폰과 태블릿에는 이 섹션이 표시되지 않습니다

| 설정 | 하는 일 | 기본값 |
|---|---|---|
| `{{ui:settings_game-editor_mcp-enabled}}` | 클라이언트의 연결을 허용합니다. 이 컴퓨터에서만, 한 번에 한 클라이언트만 연결할 수 있습니다 | 꺼짐 |
| `{{ui:settings_game-editor_mcp-port}}` | 에디터가 수신하는 포트. 값이 `0`일 때는 시작할 때마다 빈 포트를 고르고, 그 밖에는 {{v:mcp.port-min}}부터 {{v:mcp.port-max}}까지입니다. 다른 숫자는 되돌려집니다 | 0 |
| `{{ui:settings_game-editor_mcp-follow-ai}}` | AI 에이전트가 어떤 프레임을 본 뒤 재생 헤드가 가는 곳. 꺼짐: 두고 간 자리로 돌아갑니다. 켜짐: 그 프레임에 일시 정지 상태로 남습니다 | 켜짐 |
| `{{ui:settings_game-editor_mcp-reveal-edits}}` | AI 에이전트가 편집할 때마다 생성하거나 변경한 것을 선택하고 위치를 표시합니다. 드래그, 입력, 플레이 중에는 하지 않습니다 | 켜짐 |
| `{{ui:settings_game-editor_mcp-operation-delay}}` | 에디터가 AI의 두 작업 사이에 기다리는 시간(초), 0부터 {{v:mcp.operation-delay-max}}까지. 값이 `0`일 때는 각 작업을 즉시 적용합니다. 재생, 일시 정지, 재생 헤드 이동은 절대 지연되지 않으며, AI 에이전트가 읽기만 하는 작업도 마찬가지입니다 | {{v:mcp.operation-delay}} |

`{{ui:settings_game-editor_mcp-copy-config}}`은(는) MCP 클라이언트가 받는 구성을 복사합니다. 서버 경로와 게임의 연결 파일 경로가 채워진 상태입니다

설정 아래의 줄은 에디터가 무엇을 하고 있는지 알려 줍니다: 꺼짐, 포트에서 수신 중, 연결됨, 또는 에디터의 AI 배지에서 중지됨

이 설정은 이 기기에만 보관됩니다

자세히 - [[7_ai-assistant]]

## 레벨 생성

`{{ui:settings_editor-settings_level-presets}}`은(는) 새 레벨이 무엇으로 시작하는지 정합니다: 비어 있거나 작은 기본 골격이 있는 상태입니다.
프리셋이 없으면 그 골격을 매번 직접 만들어야 합니다

> [!caution] 주의
> `{{ui:settings_editor-settings_parameters}}`에서는 나중에 바꾸기 번거로운 것을 정합니다: 프레임 단위의 길이와 프레임 레이트

> [!tip] 팁
> `{{ui:settings_editor-settings_quot-level-quot-file-format}}` 목록과 `{{ui:settings_editor-settings_quot-metadata-quot-file-format}}` 목록은 레벨과 메타데이터를 디스크에 어떤 형식으로 쓸지 고릅니다. 둘 다 나중에 레벨의 `{{ui:settings_level-settings_dangerous-zone}}`에서 바꿀 수 있습니다

자세히 - [[2_first-level]]

## 라이브러리

`{{ui:settings_editor-settings_library}}`은(는) `{{ui:settings_editor-settings_community}}` 다음에 오는 마지막 탭입니다. 여러 레벨에서 재사용하는 리소스가 들어 있습니다: 이 기기의 공유 라이브러리, 직접 만든 컬렉션, 그리고 Steam 빌드에서는 Steam 창작마당에서 구독한 컬렉션

왼쪽 열에서 종류를 고릅니다: `{{ui:settings_level-settings_collections}}`, 이어서 프리팹, 테마, 도형, 이펙트, 그다음 텍스처, 폰트, 오디오.
여기서 컬렉션을 생성하고 편집하며, 컬렉션 사이에 항목을 복사하고, 가져오고 내보내며, Steam 빌드에서는 직접 만든 컬렉션을 게시합니다

자세히 - [[16_library-and-collections]]

## 다른 사람의 작업물 사용

레벨에 들어가는 모든 외부 리소스(음악, 이미지, 폰트, 텍스트)는 다음 두 가지 중 하나에 해당해야 합니다:
- `CC BY-NC` 이상으로 자유로운 라이선스
- 공개 비상업적 배포에 대한 권리자 본인의 허락

> [!caution] 주의
> 개인적으로 받은 "네, 괜찮아요"만으로는 부족합니다. `CC BY-NC` 레벨은 공개적으로 배포됩니다. 허락은 개인적인 사용만이 아니라 바로 그 배포를 포함해야 합니다

기기에만 남아 있는 레벨은 검사하지 않습니다.
규칙은 한 시점에 적용됩니다: 레벨을 서비스에 넘길 때

전체 규칙, 허용되는 라이선스 목록, 요청 템플릿, 리소스를 찾을 곳:
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
