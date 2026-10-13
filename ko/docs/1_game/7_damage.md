---
title: 대미지와 목숨
date: 2026-10-02
tags: [advanced_player]
---

# 대미지와 목숨

피격될 때마다 목숨이 하나 줄고, 아바타가 {{v:avatar.knockback-time}}초 동안 밀려나며, {{v:avatar.damage-timeout}}초 동안 무적이 됩니다. 기본 설정에서는 사망하면 레벨이 마지막 체크포인트로 되감기고 목숨이 회복됩니다

## 피격의 세 단계

1. **밀려남, `{{v:avatar.knockback-time}}`초.** 아바타를 맞힌 대상의 반대쪽으로 초당 `{{v:avatar.knockback-speed}}` 유닛의 속도로 밀려납니다. 약 {{v:avatar.knockback-distance}} 유닛으로, 대시 한 번의 거리 전체이자 기본 화면 높이의 4분의 3입니다. 이 동안에는 입력을 받지 않습니다. 대시로 밀려남에서 벗어날 수 없습니다: 넉백이 모든 것보다 우선합니다
2. 그 {{v:avatar.knockback-time}}초가 지나면 **조작이 돌아옵니다**
3. 피격된 순간부터 꼬박 `{{v:avatar.damage-timeout}}`초 동안 **맞지 않습니다**. 그 1초 안의 모든 피격은 무시됩니다

아바타를 맞힌 대상의 정확히 위에 서 있으면 밀어낼 방향이 없습니다. 이때는 전혀 밀려나지 않습니다

등장하는 동안(`{{v:avatar.spawn-time}}`초)과 대시 보호 시간 `{{v:avatar.dash-invulnerability}}`초 동안에도 맞지 않습니다, [[6_avatar]]

> [!info] 참고
> 위험 지대 안에 머물러도 목숨은 열 개가 아니라 하나만 줄어듭니다. 두 번째 위험 지대로 밀려나도 살아남을 수 있습니다. 촘촘한 탄막은 즉사처럼 보이지만, 보호 1초가 끝나는 바로 그 순간 날아오는 탄 하나보다 대가가 적은 경우가 많습니다

## 목숨

목숨 수는 레벨 화면에서 고릅니다: `{{ui:menu_levelview_options-lifes_option-zen}}`, `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}` 또는 최대 16까지의 `{{ui:menu_levelview_options-lifes_option-custom}}`, [[2_playing-levels]]

피격될 때마다 목숨이 하나 줄어듭니다. 마지막 목숨을 앗아 가는 피격이 곧 사망입니다.
`{{ui:menu_levelview_options-lifes_option-zen}}` 모드도 다른 플레이처럼 피격에 반응합니다 - 밀려남, 실드 링, 파티클 폭발, 1초의 보호가 평소대로 작동하고 피격은 통계에 집계됩니다 - 하지만 목숨이 줄지 않으므로 플레이가 끝나지 않습니다

목숨은 아바타 주위의 점 고리로 표시됩니다: 켜진 점은 남은 목숨, 꺼진 점은 잃은 목숨입니다.
결과 창에는 `{{ui:game_game-result_hits}}` 항목과 `{{ui:game_game-result_lives-left}}` 항목이 표시됩니다

## 사망하면 일어나는 일

기본 설정에서는 사망해도 플레이가 끝나지 않습니다:

1. 레벨 시계가 실제 시간으로 `{{v:checkpoint.rewind-time}}`초에 걸쳐 부드럽게 멈춥니다. 음악도 함께 늘어집니다
2. 레벨이 마지막으로 도달한 체크포인트로 돌아갑니다. 목숨이 회복됩니다
3. 시계가 다시 `{{v:checkpoint.rewind-time}}`초에 걸쳐 플레이 속도까지 부드럽게 빨라집니다. 가속하는 동안에는 맞지 않습니다. 그렇지 않으면 위험한 지점 옆의 체크포인트가 첫 1초 만에 목숨을 모두 앗아 갈 것입니다

일시 정지하면 이 가속도 멈춥니다

레벨 화면에서 `체크포인트` 토글이 꺼져 있으면 레벨 시작 지점으로 되감깁니다

사망 시 결과 창이 열리게 하려면 `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}` 옵션을 켭니다. 이때 재생이 멈춥니다.
그 창의 `{{ui:game_game-result_restart-checkpoint}}` 버튼은 도달한 체크포인트에서 새 시도를 시작합니다

## 체크포인트

체크포인트는 레벨 제작자가 배치합니다. 체크포인트를 적용할지는 `체크포인트` 토글로 직접 정합니다

도달한 체크포인트란 레벨의 현재 위치 또는 그 이전에 있는 마지막 체크포인트입니다. 그래서 그곳으로 돌아가도 아무것도 취소되지 않고 되감기기만 합니다

제작자는 체크포인트가 체력을 회복하도록 설정할 수 있습니다. 그러면 그 체크포인트를 지날 때 플레이 도중에 목숨이 한 번 회복됩니다

화면 아래쪽 진행 막대에는 체크포인트마다 눈금이 있습니다. 진행 막대는 `{{ui:settings_interface_label}}` → `{{ui:settings_interface_show-game-progress}}`에서 켭니다

체크포인트를 켠 기록과 끈 기록은 따로 보관됩니다, [[10_statistics]]

## 충돌 없음

`{{ui:menu_levelview_options-no-collision_title}}` 토글은 `{{ui:menu_levelview_options-lifes_option-zen}}` 모드와 별개이며, 레벨 화면과 에디터 실행 패널에서 `체크포인트` 토글 옆에 있습니다. 켜면 아바타가 모든 것을 통과합니다: 더 이상 아무것도 아바타에 닿을 수 없습니다

`{{ui:menu_levelview_options-no-collision_title}}` 플레이는 `{{ui:menu_levelview_options-lifes_option-zen}}` 모드나 일반 플레이와 별도로 자체 기록을 가지며, 결과 창은 `{{ui:menu_levelview_options-lifes_title}}` 값 뒤에 `· 충돌 없음` 표시를 덧붙여 이를 구분합니다, [[10_statistics]]
