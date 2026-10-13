---
title: 설치
date: 2026-10-02
tags: [player]
---

# 설치

게임은 레벨, 설정, 통계를 하나의 데이터 폴더에 보관합니다. 업데이트는 안전합니다: 새 버전은 이전 데이터를 모두 읽습니다. Android에서는 게임을 제거하면 레벨도 함께 지워집니다

다운로드 - [[download]]

## 파일 위치

| 시스템 | 폴더 |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

가장 빠르게 여는 방법은 게임 안에서 여는 것입니다: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`

들어 있는 내용:

| 폴더 | 내용 |
|---|---|
| `levels` | 레벨, 레벨마다 자체 폴더 |
| `backups` | 에디터의 자동 저장 |
| `stats` | 통계 |
| `settings.json` | 설정 |
| `reports` | 오류 보고서 |

## 제거

Windows, Linux, Mac에서는 무료 버전의 게임 옆에 제거 프로그램이 있습니다: Windows에서는 `unins000.exe`, Linux에서는 `unins000`, Mac에서는 `Bullet Hero.app` 옆의 `unins000`입니다. 실행하면 아무것도 묻지 않고 스스로 게임을 제거합니다. 레벨, 설정, 통계는 데이터 폴더에 남습니다

제거 프로그램은 게임 자체의 파일만 지웁니다. 게임 폴더에 직접 넣은 파일은 남고, 폴더는 비어 있을 때만 사라집니다. 게임이 실행 중이면 제거 프로그램이 먼저 닫기 버튼을 누른 것처럼 게임을 닫고, AI용 MCP 서버도 함께 닫습니다. 저장하지 않은 변경 사항이 있는 레벨은 그 변경 사항을 잃으므로 제거하기 전에 저장하세요

Windows 설치 프로그램으로 설치한 게임은 다른 프로그램과 똑같이 Windows 설정의 앱에서 제거합니다

스토어 버전은 해당 스토어에서 제거합니다

## 업데이트

새 버전의 게임은 어떤 업데이트든, 무엇이 바뀌었든 이전 데이터를 모두 문제없이 읽습니다

이전 버전은 더 새로운 버전의 레벨을 열지 못합니다. 게임이 업데이트를 요구하면 업데이트하세요

Google Play 버전에서는 메인 메뉴가 새 업데이트를 제안하고, 업데이트는 백그라운드에서 내려받아집니다. 준비되면 메인 메뉴에 `{{ui:menu_update-ready_text}}` 문구가 표시됩니다. `{{ui:menu_update-ready_install-btn}}` 버튼을 누르세요. 레벨을 클리어한 뒤 게임 평가를 요청할 수 있습니다

> [!caution] 주의
> Android에서는 게임을 제거하면 모든 레벨도 함께 삭제됩니다. 제거하기 전에 프로필을 내보내세요 - [[14_profile-transfer]]
