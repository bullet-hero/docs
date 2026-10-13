---
title: 문제 해결
date: 2026-10-03
tags: [player]
---

# 문제 해결

직접 복사한 레벨은 다시 스캔하면 목록에 나타납니다. 더 새로운 버전의 레벨은 게임 업데이트가 필요하고, .7z 아카이브는 zip으로 다시 압축해야 합니다. 잊어버린 비밀번호는 복구할 수 없습니다. Discord에 활동이 표시되는 것은 Steam 빌드에서 Discord 앱이 실행 중일 때뿐입니다

문제를 찾지 못했습니까? 신고할 곳 - [[11_help]]

## 레벨이 목록에 없음

- **직접 복사함.** 레벨 폴더는 `levels` 바로 안에 있어야 합니다, [[1_installation]]. 복사한 다음 `{{ui:root_level-browser_refresh}}` 버튼을 누르십시오
- **창작마당 아이템.** Steam 빌드는 구독한 아이템만 보여 줍니다. `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` 옵션은 디스크에서 찾은 폴더를 추가합니다. 그 폴더에는 `{{ui:root_level-entry_not-listed}}` 표시가 붙습니다
- **아무것도 보이지 않음.** 레벨 폴더에 접근할 수 없는 상태일 수 있습니다. 이 상태에서는 `{{ui:settings_other_title}}` 탭의 저장 공간 정리가 실행되지 않고, 다음 문구가 표시됩니다: `레벨 검사에서 아무것도 찾지 못해 정리를 거부했습니다`

## 레벨이 불러와지지 않음

불러오기 화면에 단계가 표시됩니다: `{{ui:root_loading_reading}}`, `{{ui:root_loading_validating}}`, `{{ui:root_loading_resources}}`, `{{ui:root_loading_building}}`

- **웹 주소에 있는 파일.** 레벨은 파일을 자기 폴더에 두는 대신 링크에서 가져올 수 있습니다. `{{ui:settings_general_title}}` → `{{ui:settings_general_resource-web-timeout}}` 값은 게임이 그런 파일을 몇 초 동안 기다릴지 정합니다
- **손상된 레벨.** `Json` 형식의 레벨은 텍스트이므로 눈으로 읽을 수 있습니다. 손상된 `Blob` 레벨은 통째로 거부됩니다. 자세히 - [[4_level-folder-and-backups]]
- **오류 창.** 창에는 `{{ui:root_error_copy}}`, `{{ui:root_error_save}}`, `{{ui:root_error_open-reports-folder}}` 버튼이 있습니다. 보고서는 `reports` 폴더에 저장됩니다. [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)에 올리는 버그 신고에 첨부하십시오, [[11_help]]
- **`레벨에 필요한 프레임당 오브젝트 수가 이 기기의 허용치보다 많습니다`.** 이것은 불러오기 오류가 아닙니다. 레벨은 플레이되지만 일부가 그려지지 않습니다. 자세히 - [[1_level-budget]]

## "업데이트 필요"

이전 버전의 게임은 더 새로운 버전의 파일을 열지 않습니다. 게임을 업데이트하십시오

| 메시지 | 할 일 |
|---|---|
| `이 레벨은 더 새로운 버전의 게임에서 만들어져...` | 게임 업데이트 |
| `이 아카이브에는 더 새로운 버전의 게임에서 만든 레벨이 들어 있습니다...` | 게임 업데이트 |
| `클립보드에 더 새로운 버전의 게임에서 복사한 에디터 내용이 있습니다...` | 게임 업데이트 |
| `설정 또는 통계가 더 새로운 버전의 게임에서 저장되었습니다...` | `{{ui:root_update-required_download}}`, `{{ui:root_update-required_keep}}` 또는 `{{ui:root_update-required_overwrite}}` |

`{{ui:root_level-entry_newer-version}}` 또는 `{{ui:root_level-entry_newer-file}}` 표시가 붙은 카드도 같은 거부입니다. 레벨을 열기 전부터 표시됩니다

### 더 새로운 버전의 설정이나 통계

이 경우 게임은 기본값으로 실행됩니다. 게임을 닫을 때까지 자체 데이터를 아무것도 저장하지 않으며, 더 새로운 파일은 그대로 남습니다. 이것이 익명 모드입니다, [[4_settings]].
`--suppress-game-saves` 사용 시에는 `{{ui:root_update-required_overwrite}}` 버튼이 없습니다

더 새로운 버전의 레벨 통계는 표시되지 않습니다. 저장이 꺼져 있지 않다면 그 레벨을 플레이할 때 통계가 덮어쓰입니다

### 게임이 거부하는 이유

파일 형식이 바뀔 때마다 새로운 세대 번호가 붙습니다. 빌드는 잘못 읽지 않도록 더 새로운 세대의 파일을 읽지 않습니다

## 보호된 레벨

열기 전에 게임이 `{{ui:level_passphrase_password}}` 입력을 요청합니다.
비밀번호는 세션마다 한 번 묻고, 메모리에만 보관합니다

암호화되는 것은 내용뿐입니다: 오브젝트, 키프레임, 테마. 제목, 커버, 미디어는 읽을 수 있는 상태로 남으므로 비밀번호 없이도 카드가 표시됩니다

보호된 레벨을 삭제할 때는 비밀번호가 필요 없습니다

> [!caution] 주의
> 잊어버린 비밀번호는 복구할 수 없습니다. 키는 어디에도 저장되지 않습니다 - 게임에도, 파일에도, 누구에게도

## 아카이브가 거부됨

| 메시지 | 원인 |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | `.7z` 형식입니다. `.zip` 형식으로 다시 압축하십시오 |
| `{{ui:editor_create-level_archive-wrong-password}}` | 비밀번호가 일치하지 않습니다 |
| `{{ui:editor_create-level_archive-damaged}}` | 아카이브가 손상되었습니다. 다시 보내 달라고 요청하십시오 |
| `{{ui:editor_create-level_archive-not-archive}}` | 파일이 아예 레벨 아카이브가 아닙니다 |

이름을 바꾼 아카이브는 문제가 되지 않습니다: 게임은 파일의 바이트로 형식을 인식합니다.
받아들이는 아카이브 - [[2_playing-levels]]

## Discord에 플레이 중인 내용이 표시되지 않음

- **Steam 빌드가 아님.** Discord에 활동을 표시하는 것은 Steam 빌드뿐입니다
- **Discord 앱이 닫혀 있음.** 같은 컴퓨터에서 Discord 데스크톱 앱이 실행 중이어야 합니다. 게임보다 나중에 실행했습니까? 다음에 화면이 바뀔 때 상태가 나타납니다
- **활동이 숨겨져 있음.** Discord에서: `User Settings` -> `Activity Privacy` -> 감지된 활동 공유를 켜십시오
- **직접 만든 레벨의 이름이 표시되지 않음.** 의도된 동작입니다: 이름이 표시되는 것은 창작마당 레벨이나 게임과 함께 제공되는 레벨뿐이며, 에디터는 편집 중인 레벨의 이름을 절대 표시하지 않습니다. 이유 - [[game-privacy-policy#Discord Rich Presence]]
