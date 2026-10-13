---
title: 실행 인수
date: 2026-10-12
tags: [advanced_player, developer]
---

# 실행 인수

실행 인수는 화면, 레벨, 플레이를 바로 열고, 스위치는 게임 실행 한 번의 동작을 바꿉니다. 인수는 실행 파일 뒤에 씁니다: 바로 가기, 터미널, Steam의 실행 옵션에서

인수 없이 실행하면 게임은 메인 메뉴를 엽니다

MCP 연결을 사용하는 AI 어시스턴트는 이미 실행 중인 게임에 같은 인수를 보낼 수 있습니다 - [[7_ai-assistant]]

## 구문

- 모든 인수는 하이픈 두 개로 시작합니다: `--editor`
- 값은 공백이나 `=` 기호 뒤에 옵니다: `--speed 1.5` 형식과 `--speed=1.5` 형식은 같습니다
- 키의 대소문자는 구분하지 않습니다: `--Editor`도 작동합니다
- 숫자는 시스템 언어와 관계없이 소수점으로 점을 씁니다: `1.5`, 절대 `1,5` 형식은 쓰지 않습니다
- 공백이 있는 값은 큰따옴표로 감쌉니다: `--level "D:\My Levels\Volcano"`

**게임이 사용할 수 없는 인수 때문에 실행이 멈추는 일은 없습니다.** 그런 인수는 버려지고, 그에 관한 줄이 로그에 남으며, 게임은 평소의 화면을 엽니다. 로그 위치 - [[11_help#로그]]

**알 수 없는 인수는 무시됩니다.** 게임은 자신의 인수, 즉 하이픈 두 개로 시작하는 인수만 읽습니다. 하이픈 하나로 시작하는 Unity 자체 인수(예: `-screen-width`)는 그대로 통과합니다. 해상도와 전체 화면은 이 인수로 설정합니다

## 화면

| 인수 | 열리는 것 |
|---|---|
| `--menu` | 메인 메뉴, 인수가 없을 때와 같음 |
| `--editor` | 레벨 에디터 |
| `--game` | `--level`에 지정한 레벨, 그리고 플레이가 바로 시작됨 |
| `--settings` | 설정 화면이 위에 열린 메인 메뉴 |

화면 인수는 하나까지만 전달합니다. 서로 다른 두 개는 서로를 무효로 만들고, 로그에 경고가 남은 채 메뉴가 열립니다

`--settings` 뒤에 탭 이름을 붙일 수 있습니다: `general`, `audio`, `controls`, `keybindings`, `graphics`, `interface`, `game-editor`, `profile`, `other`. 이름이 없으면 설정은 마지막으로 열었던 탭에서 열립니다. 알 수 없는 이름은 버려지고, 설정은 그래도 열립니다

설정은 실행 한 번에 한 번만 열립니다. 나중에 메뉴로 돌아와도 다시 열리지 않습니다. 각 탭에 무엇이 있는지 - [[4_settings]]

## 레벨 선택

`--level` 인수는 레벨을 식별자(`LevelId`) 또는 레벨 폴더의 경로로 지정합니다. 제목은 절대 통하지 않습니다: 제목은 중복되고, 번역되고, 수정되기 때문입니다. 식별자로 읽히는 값은 항상 식별자로 취급됩니다

레벨은 게임이 이미 목록에 보여 주는 레벨 중에서 찾습니다. 목록에 없는 폴더는 게임이 찾지 못합니다

| 함께 쓴 인수 | 결과 |
|---|---|
| 없음 | 메뉴가 레벨 화면에서 열리고 `{{ui:menu_levelview_play-btn}}` 버튼을 기다림 |
| `--editor` | 이 레벨을 연 상태로 에디터가 열림 |
| `--game` | 플레이가 바로 시작됨 |

비밀번호는 절대 인수로 전달하지 않습니다. 보호된 레벨은 화면에서 비밀번호를 묻고, 답을 입력하면 열립니다

## 플레이 조건

이 조건들은 레벨 화면의 컨트롤 값을 채우고, `{{ui:menu_levelview_play-btn}}` 버튼을 누른 것처럼 플레이가 시작됩니다. `--game` 인수와 함께 쓸 때만 작동합니다. 그렇지 않으면 로그에 경고를 남기고 무시됩니다

| 인수 | 값 | 레벨 화면의 컨트롤 |
|---|---|---|
| `--speed` | `0`보다 크고 `2` 이하, `0.1` 단위로 반올림 | `{{ui:field_common_speed}}` |
| `--lives` | `0`부터 `16`까지, `0`은(는) `{{ui:menu_levelview_options-lifes_option-zen}}` 모드 | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0` 또는 양의 정수, `0`은(는) 플레이마다 새 시드 | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`, `reflex`, `warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`, `--no-checkpoints` | - | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | - | `{{ui:menu_levelview_options-no-collision_title}}` |

생략한 조건은 기본값을 따릅니다: 목숨 3개, 속도 `1.0`, 체크포인트 켬, 봇 없음, 시드 `0`, 충돌 켬

이렇게 시작한 플레이도 일반 플레이입니다. 다른 플레이와 마찬가지로 통계에 들어갑니다, [[10_statistics]]

## 실행 전체에 적용되는 스위치

이 세 가지는 어떤 화면과도 함께 작동하며, 저장된 설정을 바꾸지 않습니다:

| 인수 | 하는 일 |
|---|---|
| `--autosave on`, `--autosave off` | 이번 실행 동안 에디터의 자동 저장을 켜거나 끕니다. `{{ui:settings_game-editor_title}}` 설정 탭은 강제된 값을 표시하고 바꿀 수 없게 합니다 |
| `--suppress-game-saves` | 실행 전체에 익명 모드를 적용합니다. 게임 안에서는 끌 수 없습니다, [[4_settings#익명 모드]] |
| `--frame-stats` | 프레임 시간 요약을 GPU 시간, CPU 시간과 함께 로그에 기록합니다. 성능 측정에 사용합니다 |

`--frame-stats` 인수는 화면마다 30초에 한 번, 그리고 화면 위의 창이 바뀔 때마다 한 줄을 기록합니다. 화면의 처음 3초는 집계하지 않습니다

## 조합

| 명령 | 결과 |
|---|---|
| 없음 또는 `--menu` | 메뉴 |
| `--editor` | 레벨이 열리지 않은 에디터 |
| `--settings` | 메뉴, 설정은 마지막으로 열었던 탭에서 열림 |
| `--settings graphics` | 같음, `{{ui:settings_graphics_title}}` 탭에서 |
| `--level X` | 레벨 X 화면의 메뉴, `{{ui:menu_levelview_play-btn}}` 버튼을 기다림 |
| `--level X --game` | 레벨 X, 플레이 진행 중 |
| `--level X --editor` | 에디터, 레벨 X 열림 |
| `--level` 없이 `--game` | 메뉴와 경고 |
| `--menu --editor` | 메뉴와 경고 |
| `--game` 없이 `--speed 2` | 조건이 경고와 함께 무시됨 |
| `--editor --autosave off` | 에디터, 이번 실행에서만 자동 저장 꺼짐 |
| `--autosave maybe` | 경고와 함께 무시됨, 플레이어의 설정이 적용됨 |
| `--suppress-game-saves` | 메뉴. 이번 실행에서 게임 자체의 저장은 하나도 디스크에 기록되지 않음 |
| `--level X --game --suppress-game-saves` | 레벨 X, 플레이 진행 중, 끝난 뒤에 통계가 남지 않음 |
| `--editor --suppress-game-saves` | 에디터. 레벨 저장, 자동 저장, 백업은 기록되고 설정과 통계는 기록되지 않음 |

## 예시

Windows에서, 터미널이나 바로 가기로:

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

Steam에서는 게임의 실행 옵션에 실행 파일 없이 인수만 적습니다: `--editor --autosave off`

## Android

Android에는 명령줄이 없습니다. 인수는 게임을 실행하는 인텐트의 `bh` 문자열 엑스트라에 담겨 전달되며, 직접 입력한 줄과 똑같이 나뉩니다. 컴퓨터에서는 `adb` 명령으로 전달합니다:

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **따옴표가 중요합니다.** `am start` 전체는 큰따옴표로, `bh` 값은 작은따옴표로 감쌉니다. 그렇지 않으면 기기의 셸이 줄을 나눕니다: `bh`에는 첫 번째 인수만 들어가고, 나머지는 `am` 명령의 자체 파라미터로 넘어갑니다
- **`-S` 옵션은 실행 중인 게임을 먼저 종료합니다.** 인수는 실행할 때 한 번만 읽힙니다. 이미 실행 중인 게임에 보내도 아무것도 바뀌지 않습니다

iOS에는 실행 인수가 전혀 없습니다
