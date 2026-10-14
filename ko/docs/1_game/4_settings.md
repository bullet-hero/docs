---
title: 설정
date: 2026-10-14
tags: [player]
---

# 설정

가장 중요한 설정은 첫 실행 때 정해집니다: 게임이 언어, 음량, 성능, 효과를 묻는 빠른 설정을 저절로 엽니다. 초기화는 설정에만 영향을 주며, 레벨은 그대로 남습니다

## 탭

| 탭 | 들어 있는 것 |
|---|---|
| `{{ui:settings_general_title}}` | 언어 - 각 언어는 그 언어 자체로 표시됩니다(`Русский (ru)`). `시스템 (ko)` 항목은 기기를 따르며, 실제로 어떤 언어로 정해졌는지 보여 줍니다. 그 밖에 한 번에 불러오는 레벨 파일 수, 웹 주소에 있는 파일의 시간 제한, `{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | 음량: `{{ui:settings_audio_volume}}`, `{{ui:settings_audio_game}}`, `{{ui:settings_audio_ui}}`, `{{ui:settings_audio_editor-ui}}`, `{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | 장치와 조종 방식, [[3_controls]] |
| `{{ui:settings_keybindings_label}}` | 단축키, 대부분 에디터용, [[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | 화면, 프레임 레이트, 안티앨리어싱, `{{ui:settings_graphics-colliders-mode_title}}`, 텍스처, 이펙트, 포스트 프로세싱 |
| `{{ui:settings_interface_label}}` | 게임 내 인터페이스, `{{ui:settings_interface_open-menu-on-lose}}`, `{{ui:settings_interface_menu-background}}`, `{{ui:settings_interface_levels-layout}}`, 화면 방향, 통계 오버레이 |
| `{{ui:settings_game-editor_title}}` | 에디터 자체 설정. 에디터 전용 `{{ui:settings_interface_levels-layout}}`도 여기에 있습니다 |
| `{{ui:settings_profile_tab}}` | 내 통계, [[10_statistics]] |
| `{{ui:settings_other_title}}` | 저장 공간 정리, 프로필 이전과 Steam Cloud 상태([[14_profile-transfer]]), Android의 폴더 접근, 익명 모드, `{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}` 설정은 메인 메뉴 버튼 뒤에 무엇을 보여 줄지 고릅니다: 봇이 공격을 피하는 실시간 아레나, 회전하는 도형이 가득한 필드, 또는 아무것도 없음

`{{ui:settings_interface_levels-layout}}` 설정은 레벨 선택 화면이 어떤 모습으로 열릴지 고릅니다 - 커버를 늘어놓은 `{{ui:enum_level-browser-layout_grid}}` 또는 설명이 붙은 행을 늘어놓은 `{{ui:enum_level-browser-layout_list}}`. 이 설정은 두 개입니다: `{{ui:settings_interface_label}}` 탭의 것은 메뉴용(기본값 `{{ui:enum_level-browser-layout_grid}}`), `{{ui:settings_game-editor_title}}` 탭의 것은 에디터용(기본값 `{{ui:enum_level-browser-layout_list}}`)입니다. 검색 필드 옆의 버튼으로도 보기를 전환할 수 있으며, 이 전환은 그 화면을 떠날 때까지 유지됩니다

## 빠른 설정

`{{ui:settings_quick-setup_title}}` 버튼은 `{{ui:settings_general_title}}` 탭의 `{{ui:settings_general-open_folder}}` 위에 있으며, 가장 중요한 질문 몇 가지를 한 페이지에 한 범주씩 묻습니다. 맨 처음 실행할 때는 튜토리얼 제안보다 먼저 저절로 열립니다.
각 답에는 그 답이 무엇을 하는지 설명하는 줄이 하나 있습니다. 페이지는 어떤 순서로든 열 수 있으며, `{{ui:settings_quick-setup_next}}` 버튼은 다음 페이지를 제안할 뿐입니다

| 페이지 | 질문 | 답 | 바뀌는 것 |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}` 및 게임의 모든 언어(각 언어 자체로 표시) | `{{ui:settings_general_title}}` 탭과 같음 |
| | `{{ui:settings_audio_volume}}` | 슬라이더 | `{{ui:field_common_audio}}` 탭과 같음 |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`, `{{ui:settings_quick-setup_performance-economy}}`, `{{ui:settings_quick-setup_performance-recommended}}`, `{{ui:settings_quick-setup_performance-max}}` | 렌더 스케일(PC), 안티앨리어싱, 텍스처 크기, 이펙트의 프레임 레이트 - 단, 프레임 레이트 상한은 바꾸지 않습니다: 어느 답이든 화면의 주사율로 실행됩니다. `{{ui:settings_quick-setup_performance-minimum}}` 답은 파티클 효과와 포스트 프로세싱도 끄고 이미지를 512로 제한합니다 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`, `{{ui:settings_quick-setup_comfort-soft}}`, `{{ui:settings_quick-setup_comfort-minimal}}` | 모든 포스트 프로세싱 효과와 아바타의 파편 효과. `{{ui:settings_quick-setup_comfort-soft}}` 답은 글리치, 그레인, 블러, 렌즈 왜곡, 색수차를 끕니다 |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | 여기서는 아무것도 바뀌지 않습니다: 튜토리얼에서 모든 조작 방식을 시험해 보고 맞는 방식을 고를 수 있습니다. 튜토리얼은 메인 메뉴나 샌드박스에서 열립니다 |

`{{ui:settings_quick-setup_default-badge}}` 표시가 붙은 답은 이 기기에서 게임이 처음부터 사용하는 설정입니다. 선택은 즉시 적용되며 전체 설정에서도 보입니다.
설정이 어느 답과도 일치하지 않으면 아무 답도 강조되지 않고, 그렇다는 줄이 표시됩니다 - 직접 정한 설정이며, 답을 누르면 그 설정이 대체됩니다

## 접힌 섹션

긴 탭은 섹션으로 나뉩니다. 자주 바꾸는 것은 펼쳐져 있고, 세부 조정은 접혀 있습니다: 섹션은 제목을 누르면 열립니다.
탭의 초기화 버튼 옆에 있는 버튼은 모든 섹션을 한 번에 접거나 펼칩니다

`{{ui:settings_controls_title}}` 탭에서는 지금 손에 든 장치만 펼쳐져 있습니다

## 초기화

탭마다 자체 초기화가 있습니다.
`{{ui:settings_other_title}}` 탭의 `{{ui:settings_other_reset}}` 버튼은 모든 탭을 한 번에 초기화합니다

초기화는 설정에만 영향을 줍니다. 레벨은 그대로 남습니다

## 버전 문자열

설정 화면에는 버전 문자열이 있습니다. 클릭하면 복사됩니다

형식은 다음과 같습니다: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`.
버그 신고에 인용할 줄이 바로 이것입니다, [[11_help]]

## 그래픽

**안티앨리어싱.** PC의 기본값은 `{{ui:enum_anti-aliasing-type_msaa}}` 방식입니다. 휴대폰은 안티앨리어싱 없이 시작합니다. 게임의 모든 도형은 실제 지오메트리이며, `{{ui:enum_anti-aliasing-type_msaa}}` 방식은 모든 플랫폼에서 그 가장자리를 흐리지 않고 깨끗하게 만듭니다

`{{ui:enum_anti-aliasing-type_fxaa}}` 방식은 저사양 휴대폰용입니다. 화면 전체를 한 번 처리하는 패스이므로 비용이 일정합니다. `{{ui:enum_anti-aliasing-type_msaa}}` 방식의 비용은 투명한 도형이 많이 겹쳐 그려질수록 커집니다

TAA 방식은 일부러 제공하지 않습니다. 빠른 탄 뒤에 잔상을 남기고, 지터가 글리치 효과를 방해하기 때문입니다

**프레임 레이트.** 목표 프레임 레이트는 수직 동기화가 아니라 직접 설정합니다. 그래서 60 Hz 화면에서도 144 Hz 화면에서도 레벨의 타이밍이 같습니다.
`{{ui:settings_graphics_vsync}}` 옵션이 켜져 있는 동안(PC 전용) 프레임 레이트 상한은 아무 효과가 없습니다

> [!tip] 권장
> 저사양 기기에서는 먼저 **렌더 스케일**을 1 미만으로 낮추십시오. 선명도만 떨어지고, 인터페이스는 원래 크기 그대로입니다. PC 전용

자세히 - [[2_mobile-devices]]

## 콜라이더 전용 모드

연습용 모드로, `{{ui:settings_graphics_title}}` 탭의 접힌 섹션에 있습니다. `{{ui:settings_graphics-colliders-mode_active}}` 옵션을 켜면 플레이 중인 레벨이 모든 히트박스를 단색 배경 위에 한 가지 색의 평평한 채움으로 그리고, 그 밖에는 아무것도 그리지 않습니다.
사라지는 것: 도형 자체의 모습, 콜라이더가 없는 도형, 이펙트, 텍스트, 포스트 프로세싱, 테마 배경.
그대로인 것: 음악, 충돌, 카메라와 카메라 흔들림, 체크포인트, 인터페이스와 통계 - 이 모드의 플레이도 다른 플레이와 똑같이 집계됩니다.
아바타는 평소대로 그려집니다

이 모드는 레벨을 플레이할 때만 작동합니다. 에디터, 샌드박스, 메뉴 배경은 평소대로 그려집니다

| 옵션 | 하는 일 |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | 켜짐(기본값) - 채움이 색상의 알파만큼 반투명해지고, 겹친 장애물은 더 진하게 보입니다. 알파는 0.15 아래로 내려가지 않습니다. 꺼짐 - 모든 채움이 불투명해지고, 색상의 알파는 잠깁니다 |
| `{{ui:settings_graphics-colliders-mode_color}}` | 채움 색상, 기본값은 알파 0.6의 빨간색입니다. 에디터의 콜라이더 보기도 같은 색조를 자체 불투명도로 사용합니다 |
| `{{ui:settings_graphics-colliders-mode_background}}` | 채움 뒤에 그려지는 것, 기본값은 어두운 회색입니다 - 검은색이 아니므로 주변의 검은 여백과 대비되어 카메라 프레임의 가장자리가 보입니다 |

두 색상은 각자의 제목 아래 접혀 있습니다: 필요한 쪽을 펼치면 색상환이 나타납니다

## 익명 모드

`{{ui:settings_other_title}}` → `{{ui:settings_other_suppress-game-saves}}`에서 켭니다

모드가 켜져 있는 동안 게임은 자체 데이터를 아무것도 저장하지 않습니다. `settings.json`, 전체 통계, 레벨 통계는 디스크에 손대지 않은 채 남습니다.
바꾼 설정은 게임을 닫을 때까지 그대로 작동합니다

레벨 작업은 평소대로 저장됩니다: 저장, 내보내기, 가져오기, 복사, 삭제.
에디터의 자동 저장과 백업도 작동하며, 이 둘에는 자체 스위치가 따로 있습니다

모드는 게임을 닫을 때까지 유지되며 어디에도 기억되지 않습니다

모드를 끄면 현재 설정이 저장됩니다. 그동안 플레이한 모든 것은 버려집니다

> [!info] 참고
> 이 모드는 저절로 켜지기도 합니다. [[12_launch-arguments|실행 인수]] `--suppress-game-saves` 사용 시 실행 전체에 걸쳐 모드가 켜지며, 게임 안에서는 끌 수 없습니다. 더 새로운 버전의 게임에서 저장된 설정이나 통계도 이 모드를 켭니다. 이때 게임은 실행할 때마다 그 파일을 유지할지, 기본값으로 덮어쓸지 묻습니다
