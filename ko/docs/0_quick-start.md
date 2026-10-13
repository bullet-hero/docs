---
title: 빠른 시작
date: 2026-10-02
tags: [player, level_author]
---

# 빠른 시작

게임을 다운로드하고 레벨 목록을 열어 아무 레벨이나 플레이합니다. 직접 만들려면 에디터에서 레벨을 생성하고 그 폴더에 1-2분 길이의 트랙을 넣습니다

각 단계는 가장 짧은 경로입니다. 자세한 내용은 링크에 있습니다.
자주 묻는 질문에 대한 짧은 답변 - [[6_faq]]

## 1. 게임 받기

모든 빌드와 스토어 - [[download]]

## 2. 실행하기

메인 메뉴에서 필요한 버튼은 세 개입니다: `{{ui:menu_main_levels-btn}}`, `{{ui:menu_main_editor-btn}}`, `{{ui:settings_common_title}}`.
`{{ui:menu_main_story-btn}}`, `{{ui:menu_main_multiplayer-btn}}` 버튼은 아직 작동하지 않습니다

## 3. 첫 레벨 플레이하기

`{{ui:menu_main_levels-btn}}` 버튼을 누르고 레벨을 고른 다음 `플레이`를 누릅니다.
조작하는 것은 작은 사각형입니다. 목표는 트랙이 끝날 때까지 살아남는 것입니다

> [!tip] 팁
> 처음 플레이할 때는 `{{ui:menu_levelview_options-lifes_title}}` 옵션을 `{{ui:menu_levelview_options-lifes_option-zen}}`(으)로 설정하세요. 그러면 플레이가 끝나지 않으니 차분하게 조작에 익숙해질 수 있습니다. `{{ui:menu_levelview_options-no-collision_title}}` 옵션은 한 단계 더 나아갑니다: 켜면 아무것도 플레이어에게 닿지 않습니다

누군가에게 받은 레벨이 있습니까? 레벨은 폴더입니다. 그 폴더를 `levels` 폴더에 복사하고 `{{ui:root_level-browser_refresh}}` 버튼을 누릅니다.
자세히 - [[2_playing-levels]]

## 4. 조작

| 장치 | 이동 | 대시 |
|---|---|---|
| 마우스 | 왼쪽 버튼을 누르고 있기 | `Space`, `Shift` 또는 오른쪽 버튼 |
| 터치스크린 | 손가락으로 드래그 | 두 번째 손가락 |
| 게임패드 | 아무 스틱 | `Start`, `Select` 외의 아무 버튼 |

게임패드 버튼을 제외한 모든 조작은 `{{ui:settings_common_title}}` → `{{ui:settings_controls_title}}`에서 다시 할당할 수 있습니다.
자세히 - [[3_controls]]

## 5. 무언가 작동하지 않는다면

자주 발생하는 문제와 해결 방법 - [[5_troubleshooting]]

문제를 알릴 곳 - [[11_help]]

## 6. 첫 레벨 만들기

`{{ui:menu_main_editor-btn}}` 버튼을 누르고 레벨을 생성한 다음 그 폴더에 트랙(`ogg`, `mp3` 또는 `wav`)을 넣습니다.
처음에는 1-2분 길이의 트랙이면 충분합니다

에디터는 편집하고 1분이 지나면 레벨을 자동으로 저장합니다. `Ctrl+S` 키를 누르면 바로 저장됩니다

전체 과정을 단계별로 - [[2_first-level]]
