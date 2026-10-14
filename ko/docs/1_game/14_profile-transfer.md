---
title: 프로필 이전
date: 2026-10-14
tags: [player]
---

# 프로필 이전

프로필 전체가 zip 파일 하나에 담깁니다: 레벨, 통계, 설정, 라이브러리. 다시 설치하거나 다른 기기로 옮기기 전에 프로필을 내보내고, 새 기기에서 가져오십시오

버튼은 `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`에 있습니다. Windows, Mac, Linux, Android에서 작동합니다. iOS에서는 사용할 수 없습니다

## 파일에 들어가는 내용

| 부분 | 데이터 폴더 안의 위치 | 기본 체크 |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | 예 |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | 예 |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | 예 |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | 예 |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | 아니요 |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | 아니요 |
| `{{ui:settings_profile-transfer_category-recordings}}` | `recordings` | 아니요 |

파일은 일반 zip 파일이므로 어떤 압축 프로그램으로도 열립니다. 안에는 데이터 폴더와 같은 폴더들([[1_installation]])과 함께, 파일을 설명하는 `profile.json` 파일이 들어 있습니다

## 내보내기

1. `{{ui:settings_profile-transfer_export}}` 버튼을 누릅니다
2. 필요한 부분을 체크합니다
3. 파일을 저장할 위치를 고릅니다

내보내기는 설정이 열리는 곳이라면 어디서든 작동합니다: 메인 메뉴, 일시 정지한 플레이, 에디터. 먼저 통계가 디스크에 저장되므로 파일은 최신 상태입니다

## 가져오기

1. 메인 메뉴에서 설정을 열고 `{{ui:settings_profile-transfer_import}}` 버튼을 누릅니다
2. zip 파일을 고릅니다
3. 부분을 체크하고 모드를 고릅니다
4. 확인합니다

가져오기는 메인 메뉴에서만 작동합니다. 실행 중인 레벨이나 열려 있는 에디터는 자신의 파일을 붙잡고 있어서, 그 아래에서 파일을 교체할 수 없습니다

| 모드 | 결과 |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | 체크한 각 부분을 비우고 파일의 내용으로 채웁니다 |
| `{{ui:settings_profile-transfer_mode-merge}}` | 레벨은 추가됩니다. 양쪽에 모두 있는 레벨은 더 새로운 사본으로 통째로 교체됩니다. 통계는 각 카운터의 더 큰 값과 더 나은 기록을 남깁니다. 라이브러리 파일, 자동 저장, 보고서는 추가만 되고 기존 것은 그대로 남습니다 |

가져오기는 무엇이든 쓰기 전에 한 번 더 묻습니다. 교체는 비울 부분을 알려 주고, 병합은 레벨을 몇 개 추가하고, 교체하고, 유지하는지 알려 줍니다

**다른 종류의 기기에서 온 설정.** 휴대폰의 프로필을 컴퓨터에서 가져오면(또는 그 반대) 기존의 조작 설정과 그래픽 설정은 유지됩니다. 나머지는 모두 파일에서 가져옵니다

게임은 더 새로운 버전의 게임에서 만든 파일을 거부합니다 - 먼저 게임을 업데이트하십시오. zip 형식이 아닌 파일, 프로필이 아닌 zip 파일, 비밀번호로 보호된 zip 파일, 손상된 파일도 거부합니다. 이런 경우에는 아무것도 바뀌지 않습니다

## 백업

게임은 가져오기 전에 교체하려는 부분을 백업 하나에 저장합니다. 백업은 데이터 폴더 안의 `profile-backups` 폴더에 있습니다. 백업은 하나뿐입니다: 다음 가져오기가 덮어씁니다

- `{{ui:settings_profile-transfer_backup-restore}}` 버튼은 백업을 되돌려 놓습니다. 이때 교체되는 내용이 새 백업이 되므로 복원도 되돌릴 수 있습니다
- `{{ui:settings_profile-transfer_backup-save-as}}` 버튼은 원하는 위치에 사본을 저장합니다
- `{{ui:settings_profile-transfer_backup-delete}}` 버튼은 백업을 삭제합니다
- `{{ui:settings_profile-transfer_clear-cache}}` 버튼은 `profile-backups` 폴더 전체를 삭제합니다: 백업과 중단된 이전 작업이 남긴 것

`{{ui:settings_profile-transfer_backup-to-folder}}` 옵션은 가져오기 중에 기본으로 체크되어 있습니다: 게임이 바로 게임 밖 어디에 사본을 보관할지 묻습니다

> [!caution] 주의
> Android에서는 백업이 게임 데이터 폴더에 있어 게임과 함께 삭제됩니다. 게임을 제거하기 전에 프로필을 내보내거나 백업을 다른 곳에 저장하십시오

가져오기 도중에 게임이 닫히면 다음 실행 때 프로필이 원래 상태로 돌아갑니다

## Steam Cloud

Steam 버전에서는 프로필이 Steam 계정을 자동으로 따라갑니다. 버튼은 없습니다. 게임은 시작할 때 한 번 동기화하고, 플레이하는 동안 바뀐 내용을 보내고, 종료할 때 마지막으로 동기화합니다

스위치는 Steam에 있습니다: Steam의 게임 속성에 있는 Steam Cloud 체크박스입니다. 켜져 있는지, 마지막 동기화가 언제였는지는 `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_cloud_title}}`에 표시됩니다

| 부분 | 두 기기에서 모두 바꿨을 때 |
|---|---|
| `{{ui:settings_profile-transfer_category-statistics}}` | 각 카운터는 더 큰 값과 더 좋은 기록을 남기며, 아무것도 잃지 않습니다 |
| `{{ui:settings_profile-transfer_category-settings}}` | 더 새로운 사본이 이깁니다. `{{ui:settings_graphics_title}}`, `{{ui:settings_controls_title}}` 설정은 각 기기에서 항상 그 기기의 것으로 유지됩니다 |
| `{{ui:settings_profile-transfer_category-levels}}` | 레벨의 더 새로운 사본이 통째로 이깁니다. 다른 사본은 진 기기의 에디터 백업에 들어갑니다 |
| `{{ui:settings_profile-transfer_category-library}}` | 파일마다 더 새로운 사본이 이깁니다 |

- 한 기기에서 삭제한 레벨은 다른 기기에서도 삭제됩니다. 각 기기는 그 레벨의 마지막 상태를 에디터 백업에 남깁니다
- 한 기기에서 삭제한 통계는 다른 기기에서도 삭제됩니다. 마지막 동기화 이후 다른 기기에서 플레이했다면 그 진행 상황은 유지됩니다
- Steam이 게임에 남겨 둔 공간보다 큰 레벨은 그 기기에만 남습니다
- `{{ui:settings_profile-transfer_category-backups}}`, `{{ui:settings_profile-transfer_category-reports}}`, `{{ui:settings_profile-transfer_category-recordings}}` 항목은 동기화되지 않습니다
- 더 새로운 버전의 게임이 쓴 클라우드 사본은 이 기기의 게임을 업데이트할 때까지 건드리지 않습니다
- 에디터에서 열려 있는 레벨은 교체되지 않습니다. 다음 실행 때 동기화됩니다
- `{{ui:settings_other_suppress-game-saves}}` 옵션이 켜져 있으면 아무것도 동기화되지 않습니다

## Android에서 빌드 간 이동

파일로 설치한 게임(itch.io 등)은 Google Play에서 업데이트할 수 없고, 그 반대도 마찬가지입니다. 빌드의 서명이 달라서 Android 시스템이 업데이트를 거부합니다. 전환하려면:

1. 프로필을 내보내고 파일을 게임 밖에 저장합니다
2. 게임을 제거합니다
3. 다른 빌드를 설치합니다
4. 프로필을 가져옵니다
