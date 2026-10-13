---
title: 통계
date: 2026-10-02
tags: [advanced_player]
---

# 통계

게임은 레벨마다, 그리고 기기 전체에 대해 시도, 사망, 피격, 시간을 집계합니다. 모든 데이터는 stats 폴더에 로컬로 저장됩니다. 기록은 플레이 조건 조합마다 따로 보관됩니다

## 두 파일

| 파일 | 담는 내용 |
|---|---|
| `stats/statistics.json` | 플레이어에 관한 모든 것: 모든 레벨과 화면에 걸쳐 |
| `stats/<LevelId>.json` | 레벨 하나에서 한 모든 것 |

파일 형식은 JSON, 시간은 UTC 기준입니다. 아무것도 외부로 전송되지 않습니다

`stats` 폴더는 게임 폴더 안에서 `levels` 폴더 옆에 있습니다, [[1_installation]]. 레벨 안에 들어가는 일은 없습니다.
그래서 친구에게 보낸 레벨이 이미 클리어된 상태로 도착하지 않습니다. 또 레벨을 삭제하고 다시 가져와도 진행 상황이 남습니다

## "프로필" 탭

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}` 탭에는 기기 공용 파일의 내용이 표시됩니다:

| 섹션 | 항목 |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`, `{{ui:settings_profile_last-played}}`, `{{ui:settings_profile_launches}}`, `{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`, `{{ui:settings_profile_game-time}}`, `{{ui:settings_profile_editor-time}}`, `{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`, `{{ui:settings_profile_clears}}`, `{{ui:settings_profile_deaths}}`, `{{ui:settings_profile_hits}}`, `{{ui:settings_profile_levels-played}}`, `{{ui:settings_profile_levels-cleared}}`, `{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`, `{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`, `{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`, `{{ui:settings_profile_tutorial-first}}`, `{{ui:settings_profile_tutorial-last}}` - [[13_sandbox|샌드박스 튜토리얼]]의 모든 단계를 마쳐야만 완료로 집계됩니다 |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`, `{{ui:settings_profile_levels-deleted}}`, `{{ui:settings_profile_objects}}`, `{{ui:settings_profile_operations}}`, `{{ui:settings_profile_generators}}`, `{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`, `{{ui:settings_profile_device-touch}}`, `{{ui:settings_profile_device-gamepad}}`, `{{ui:settings_profile_device-gyro}}` |

시간은 레벨 시간이 아니라 실제 초 단위로 집계됩니다. 체크포인트에서의 슬로 모션과 절반 속도로 한 플레이는 실제로 걸린 만큼 집계됩니다

기기 항목은 플레이 중에 어떤 기기로 아바타를 조작했는지 보여 줍니다. 연결만 되어 있는 기기는 집계되지 않습니다

## 레벨별 통계

레벨 파일에는 다음이 담깁니다:

- 처음과 마지막으로 플레이한 시점
- 레벨에서 보낸 실제 시간과 세션 수
- 시도(다시 시작할 때마다 새 시도), 클리어, 사망, 피격, 대시
- 체크포인트로 돌아간 횟수와 중단한 플레이
- 가장 멀리 도달한 지점과 첫 클리어
- 레벨의 어디에서 죽는지: 길이 대비 비율별, 체크포인트별

## 기록

기록은 플레이 조건별로 보관됩니다: 목숨, 속도, 체크포인트 켬/끔, 충돌 켬/끔, 봇.
속도는 화면에 보이는 그대로 소수점 둘째 자리까지 구분합니다

젠(목숨 0개)에서도 피격은 집계됩니다: 모든 충돌이 수치에 들어가고, 면제되는 것은 목숨과 플레이 종료뿐입니다

플레이는 같은 조건의 기록과 다음 순서대로 비교해 앞서면 기록을 경신합니다:

1. 더 멀리 도달한 경우
2. 피격이 더 적은 경우
3. 남은 목숨이 더 많은 경우
4. 대시를 더 적게 쓴 경우

기록에는 플레이의 시드와 당시의 레벨 버전도 저장됩니다.
버전은 조건에 포함되지 않습니다. 그래서 레벨이 수정되기 전에 세운 기록도 계속 보이며, 옆에 버전이 표시됩니다

**에디터에서 한 플레이는 집계되지만 기록은 세우지 않습니다.** 시도, 사망, 피격에는 더해집니다. 레벨이 메모리에만 존재했기 때문에 기록, 최고 진행도, 첫 클리어는 남기지 않습니다

## 저장, 삭제, 동결

게임은 30초마다 통계를 저장합니다. 그리고 플레이가 끝날 때, 화면이 바뀔 때, 종료할 때 즉시 저장합니다.
게임이 비정상 종료되어도 잃는 데이터는 최대 30초 분량입니다

- **삭제:** `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`. 그곳에 `{{ui:settings_other_cache-orphan-statistics}}` 버튼과 `{{ui:settings_other_cache-all-statistics}}` 버튼이 있습니다
- **레벨과 함께 삭제:** 레벨을 삭제할 때 `{{ui:root_level-delete_statistics}}` 옵션이 제시됩니다
- **동결:** 익명 모드는 게임을 닫을 때까지 모든 저장을 멈춥니다, [[4_settings]]
- **다른 기기로 옮기기:** 프로필을 내보내고 그 기기에서 가져옵니다. 병합하면 각 카운터의 더 큰 값이 남습니다, [[14_profile-transfer]]

> [!warning] 경고
> 손으로 복사한 레벨 폴더는 레벨 ID 값을 그대로 유지합니다. 원본과 사본이 하나의 통계 파일을 공유합니다
