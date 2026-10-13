---
title: 샌드박스와 튜토리얼
date: 2026-10-02
tags: [player]
---

# 샌드박스와 튜토리얼

샌드박스는 메인 메뉴에 있는 아레나로, 아바타를 움직이고, 여섯 가지 공격 중 무엇이든 자신에게 발사해 보고, 여섯 단계로 된 튜토리얼을 진행할 수 있습니다. 레벨은 필요하지 않습니다

처음 실행하면 게임이 튜토리얼을 한 번 제안합니다: `{{ui:menu_tutorial-offer_confirm}}` 버튼은 튜토리얼 화면으로 샌드박스를 열고, `{{ui:menu_tutorial-offer_cancel}}` 버튼은 제안을 영구히 닫습니다. 어느 쪽이든 샌드박스 자체는 메뉴에 남습니다

## 패널

샌드박스에는 왼쪽에 패널이 하나 있습니다. 손잡이를 클릭하면 패널이 접히고, 손잡이를 드래그하면 패널을 넓히거나 좁힐 수 있습니다. 패널에는 탭이 다섯 개 있습니다:

| 탭 | 하는 일 |
|---|---|
| `{{ui:sandbox_tab_home}}` | 샌드박스가 무엇인지, 각 탭이 무엇을 하는지 |
| `{{ui:sandbox_tab_tutorial}}` | 튜토리얼 단계와 지금 해야 할 일 |
| `{{ui:sandbox_tab_controls}}` | 지금 조작 중인 기기의 모드, 모션 센서 스위치, 모든 조작 설정으로 가는 경로 |
| `{{ui:sandbox_tab_attacks}}` | 여섯 가지 공격 중 무엇이든 직접 발사하거나 웨이브가 저절로 오게 함 |
| `{{ui:sandbox_tab_game}}` | 목숨, 공격 속도, 봇, 자유 카메라 |

`{{ui:settings_common_title}}` 버튼은 샌드박스 위에 게임 설정을 엽니다. `{{ui:sandbox_panel_exit}}` 버튼은 메인 메뉴로 돌아갑니다

## 일시 정지

일시 정지 버튼은 화면 오른쪽 위 모서리에 있습니다. `Esc` 키도 샌드박스를 나가는 대신 일시 정지를 엽니다. 일시 정지는 레벨에서처럼 모든 것을 멈춥니다: 아바타, 공격, 튜토리얼. 일시 정지 창에는 `{{ui:root_error_continue}}`, `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-menu}}` 버튼이 있습니다

## 튜토리얼

여섯 단계를 순서대로 진행합니다:

1. `{{ui:sandbox_tutorial_move_title}}` - 화면 너비만큼 이동합니다
2. `{{ui:sandbox_tutorial_dash_title}}` - 대시를 세 번 합니다
3. `{{ui:sandbox_tutorial_dodge_title}}` - 느려진 탄막 속에서 피격 없이 10초를 버팁니다. 피격되면 카운트가 처음부터 다시 시작됩니다
4. `{{ui:sandbox_tutorial_dash-through_title}}` - 고리가 화면 가장자리 밖까지 커지므로, 빠져나가는 유일한 방법은 고리의 테두리를 대시로 통과하는 것입니다. 고리 두 개를 통과해야 합니다 - 실패한 고리가 이미 통과한 고리를 취소하지는 않습니다. 대시 중에는 아무것에도 맞지 않습니다
5. `{{ui:sandbox_tutorial_choose-mode_title}}` - `{{ui:sandbox_tab_controls}}` 탭에서 모드를 시험해 보고 `{{ui:sandbox_tutorial_confirm-mode}}` 버튼을 누릅니다
6. `{{ui:sandbox_tutorial_done_title}}` - `{{ui:sandbox_tutorial_play-level}}` 버튼이 튜토리얼 레벨을 시작합니다

아레나에서 단계를 진행하는 동안 패널은 접히고, 단계는 화면 위쪽의 작은 카드로 표시됩니다. 터치는 카드를 통과합니다. 손잡이로는 여전히 패널을 열 수 있습니다. `{{ui:sandbox_tutorial_choose-mode_title}}` 단계와 `{{ui:sandbox_tutorial_done_title}}` 단계에서는 패널이 `{{ui:sandbox_tab_tutorial}}` 탭으로 저절로 열립니다

피격이나 사망은 튜토리얼 전체가 아니라 그 일이 일어난 단계만 다시 시작하게 하며, 그 단계는 통과할 때까지 빨간색으로 표시됩니다. 통과한 단계는 초록색입니다

목록에서 단계를 클릭하면 이미 통과한 단계라도 그 단계가 시작됩니다. 단계를 통과하면 튜토리얼은 아직 통과하지 않은 다음 단계로 넘어갑니다. 튜토리얼은 모든 단계를 통과해야만 완료로 인정됩니다 - 통계에 기록되는 것도 그때입니다. 같은 탭의 `{{ui:sandbox_tutorial_restart}}` 버튼으로 언제든 튜토리얼을 다시 시작할 수 있습니다

> [!warning] 경고
> `{{ui:sandbox_tab_game}}` 탭에서 `{{ui:sandbox_game_immortal}}` 옵션을 켜면 피격이 전혀 집계되지 않으므로, `{{ui:sandbox_tutorial_dodge_title}}` 단계와 `{{ui:sandbox_tutorial_dash-through_title}}` 단계도 피격을 감지하지 못합니다. 튜토리얼을 진행하는 동안에는 목숨을 몇 개 남겨 두십시오

## 조작

모드는 지금 조작 중인 기기에 대해 바뀌며 즉시 저장됩니다. 모션 센서에는 `{{ui:enum_control-mode_relative}}` 모드가 없습니다. 각 모드의 의미 - [[3_controls#조작 모드]]

## 공격과 게임

- `{{ui:sandbox_attacks_auto}}` 옵션은 메인 메뉴 배경처럼 `{{ui:sandbox_attacks_gap}}` 간격으로 무작위 웨이브를 발사합니다
- `{{ui:sandbox_attacks_clear}}` 버튼은 화면의 모든 공격을 지웁니다
- `{{ui:sandbox_game_speed}}` 값은 공격만 느리게 하거나 빠르게 합니다. 아바타는 항상 자신의 속도로 움직입니다
- 목숨: `{{ui:sandbox_game_immortal}}`, 1, 3, 5 중 하나. 목숨이 다 떨어지면 다시 채워지고, 샌드박스는 끝나지 않습니다
- `{{ui:sandbox_game_bot}}` 옵션은 메인 메뉴 배경에서 플레이하는 것과 같은 봇에게 아바타를 넘깁니다
- `{{ui:sandbox_game_free-camera}}` 옵션을 켜면 화면 가장자리 너머를 볼 수 있습니다: 마우스 가운데 버튼이나 두 손가락으로 시점을 옮기고, 휠이나 핀치로 확대/축소합니다. 파란 테두리는 레벨 카메라가 보는 영역을 보여 주며, `{{ui:sandbox_camera_back}}` 버튼은 시점을 그곳으로 되돌립니다. 조작, 대시, 공격은 이 옵션이 없을 때와 똑같이 작동합니다
- 사망은 레벨에서와 같이 진행됩니다: 공격이 느려지다 사라지고, 아바타가 목숨을 가득 채운 채 중앙에 나타납니다
