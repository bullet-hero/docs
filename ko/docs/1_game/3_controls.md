---
title: 조작
date: 2026-10-02
tags: [player]
---

# 조작

마우스, 터치스크린, 게임패드 또는 모션 센서로 플레이할 수 있습니다. 마우스로는 왼쪽 버튼을 누르고 있으면 아바타를 조종하고, Space, Shift 또는 오른쪽 버튼으로 대시합니다

입력은 조작 설정에서 다시 할당할 수 있지만, 게임패드 버튼은 다시 할당할 수 없습니다

레벨을 시작하지 않고 조작을 단계별로 배우거나 모든 모드를 시험하려면 - [[13_sandbox]]

## 장치

모든 조작은 `{{ui:settings_common_title}}` → `{{ui:settings_controls_title}}`에서 설정하며, 장치마다 그룹이 하나씩 있습니다

| 장치 | 기본 모드 | 이동 | 대시 |
|---|---|---|---|
| `{{ui:enum_control-device_keyboard-mouse}}` | `{{ui:enum_control-mode_absolute}}` | 왼쪽 버튼을 누르고 있으면 아바타가 마우스를 따라갑니다 | `Space`, `Shift`, 마우스 오른쪽 버튼 또는 더블 클릭(0.3초) |
| `{{ui:enum_control-device_touchscreen}}` | `{{ui:enum_control-mode_relative}}` | 화면 어디서든 손가락으로 드래그 | 두 번째 손가락 |
| `{{ui:enum_control-device_gamepad}}` | `{{ui:field_common_direction}}` | 아무 스틱 | `Start`, `Select` 외의 아무 버튼 |
| `{{ui:enum_control-device_device-gyro}}` | `{{ui:field_common_direction}}` | 기기를 수평에서 기울이기, 20°에서 최고 속도 | 화면 아무 곳이나 탭 |

마우스만으로 충분합니다: 왼쪽 버튼으로 아바타를 조종하고, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}`(으)로 대시합니다. 키보드는 선택 사항입니다

게임패드에서는 `Start` 버튼으로 일시 정지하고 재개합니다. 게임패드 버튼은 다시 할당할 수 없습니다: 플레이 중에는 오른쪽 페이스 버튼을 포함해 `Start`, `Select` 외의 모든 버튼이 대시입니다. 일시 정지 메뉴에서는 다른 메뉴와 마찬가지로 오른쪽 페이스 버튼이 "뒤로" 역할을 합니다

## 조작 모드

| 모드 | 입력의 의미 |
|---|---|
| `{{ui:enum_control-mode_absolute}}` | 위치. 커서가 그 위치로 이동하고, 아바타가 커서를 따라잡습니다 |
| `{{ui:enum_control-mode_relative}}` | 움직임. 커서가 움직임을 누적하고, 아바타가 커서를 따라잡습니다 |
| `{{ui:field_common_direction}}` | 방향. 커서가 아예 없습니다 |

모든 모드에서 이동은 즉각적입니다: 가속도 미끄러짐도 없습니다

커서 모드에서 아바타는 자기 걷기 속도로 커서를 따라잡습니다. 그래서 빠른 마우스보다 뒤처집니다. 대시는 커서 쪽으로 향합니다. 커서가 가까우면 대시가 짧아지고 정확히 커서 위에서 끝납니다

조종 버튼을 놓거나 손가락을 뗐을 때 일어나는 일은 체크박스 하나가 정합니다 - 마우스는 `{{ui:settings_controls-keyboard-mouse_km-cursor-return}}`, 터치스크린은 `{{ui:settings_controls-touchscreen_touch-cursor-return}}`:

- 켜짐 - 아바타가 그 자리에 멈추고, 커서가 아바타에게 돌아옵니다. 마우스의 기본값입니다
- 꺼짐 - 커서가 놓은 자리에 남고, 아바타가 그곳까지 걸어갑니다. 커서를 움직일 수 있는 것은 대미지뿐입니다. 터치스크린의 기본값입니다

`{{ui:field_common_direction}}` 모드에서는 스틱을 절반만 밀면 속도도 절반입니다. 대시는 항상 전체 길이로 나갑니다

터치스크린의 `{{ui:enum_control-mode_absolute}}` 모드에서는 커서가 손가락 위쪽에 놓입니다(`{{ui:settings_controls-touchscreen_touch-finger-offset-y}}`). 그래서 손가락이 아바타를 가리지 않습니다

손가락 하나로 아바타를 조종하는 동안 두 번째 손가락은 닿는 곳 어디서나 대시합니다 - 패널이나 버튼 위에서도 마찬가지입니다. 인터페이스는 그 터치를 받지 않으므로, 대시가 실수로 무언가를 누르는 일은 없습니다

정확한 수치 - [[6_avatar]]

## 모션 센서

모션 센서에는 보정이 없습니다. 휴대폰을 화면이 위를 향하게 평평하게 놓으면 아바타가 멈춰 있습니다

- 오른쪽 가장자리를 아래로 기울이면 아바타가 오른쪽으로 갑니다
- 위쪽 가장자리를 아래로 기울이면 위로 갑니다
- `{{ui:settings_controls-device_sensitivity}}` 값 1에서는 20°에서 최고 속도가 됩니다. 값 2에서는 절반의 기울기로 충분합니다

센서는 화면을 따릅니다: 휴대폰을 가로로 돌렸다가 다시 돌려도 오른쪽은 오른쪽입니다. 센서에는 두 가지 모드가 있습니다: `{{ui:enum_control-mode_absolute}}`, `{{ui:field_common_direction}}`

## 다시 할당

- **게임플레이 입력**은 `{{ui:settings_controls_title}}` 탭에 있습니다: 모드, `{{ui:settings_controls-keyboard-mouse_dash-keys}}`, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}`, 감도, 데드존, 스무딩, 반전, 화면 조이스틱과 대시 버튼. `{{ui:settings_controls_reset}}` 버튼은 모든 장치를 이 플랫폼의 기본값으로 되돌립니다
- **단축키**는 `{{ui:settings_keybindings_label}}` 탭에 있습니다. 거의 모두 에디터용입니다. 에디터 밖에는 `{{ui:settings_keybindings_window_toggle_fullscreen}}`(기본값 `F11`), `{{ui:settings_keybindings_window_settings_save}}`(설정이 열려 있을 때 `Ctrl+S`), 탐색 키가 있습니다. `{{ui:settings_keybindings_reset}}` 버튼은 모든 재할당을 되돌립니다

게임이 키 입력을 기다리는 동안 `"..."에 사용할 키를 누르세요` 문구가 표시됩니다. 그때의 규칙은 `{{ui:settings_escape-cancels_backspace}}`입니다

키의 경우 게임은 다시 할당한 것만 저장합니다. 나중에 기본 할당이 더 좋아지면, 그 할당을 직접 바꾸지 않은 한 변경 사항이 그대로 적용됩니다. `{{ui:settings_controls_title}}` 탭은 전체가 저장되므로, 이 탭의 새 기본값은 적용되지 않습니다

에디터의 단축키 - [[3_speed-and-shortcuts]]

## 여러 장치를 동시에

아바타를 조종하는 장치는 하나입니다 - 마지막으로 사용한 장치입니다. 전환은 메뉴 없이 같은 프레임에 저절로 일어납니다

게임은 매 프레임 모든 활성 장치를 확인합니다. 건드리지 않은 게임패드는 0을 보내며, 이는 사용으로 간주되지 않습니다

첫 프레임에는 아직 아무것도 사용되지 않았으므로 플랫폼이 정합니다: 컴퓨터에서는 마우스, 휴대폰에서는 터치스크린입니다

대시와 일시 정지는 어느 장치가 조종하든 모든 활성 장치에서 작동합니다. 마우스로 조종하는 동안 게임패드 버튼으로 대시할 수 있습니다. 대시만으로는 조종이 넘어가지 않습니다

장치가 아바타를 조종하려면 다음 조건을 모두 충족해야 합니다:

- 활성으로 표시되어 있음
- 플랫폼이 지원함
- 지금 연결되어 있음

위쪽의 `{{ui:settings_controls-active_now}}` 항목은 지금 어느 장치가 조종하고 있는지 보여 줍니다

> [!tip] 팁
> 조작 방식이 아무 반응도 없는 것 같습니까? 보통은 그 뒤에 다른 장치를 건드린 것입니다. 먼저 `{{ui:settings_controls-active_now}}` 항목을 보세요
