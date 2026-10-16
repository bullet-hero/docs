---
title: 성능 평가
date: 2026-10-17
tags: [player, level_author]
---

# 성능 평가

플레이하기 전에 게임이 레벨이 내 기기에서 얼마나 무거운지 다섯 칸짜리 게이지로 보여줍니다: 켜진 칸이 많을수록 레벨이 가볍습니다. 초록색 칸은 원활하게 실행, 노란색은 빠듯함, 빨간색은 프레임 레이트가 떨어진다는 뜻입니다

점수는 숫자이며, `{{v:performance.score-limit}}`는 목표 프레임 레이트에서 한 프레임에 쓸 수 있는 시간과 정확히 같습니다. 구간은 점수로 정해집니다:

| 칸 | 구간 | 점수 |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | `{{v:performance.score-warning}}` 미만 |
| 4 | `{{ui:level_performance_tight}}` | `{{v:performance.score-warning}}`부터 `{{v:performance.score-limit}}`까지 |
| 3 | `{{ui:level_performance_drops}}` | `{{v:performance.score-limit}}` 초과, `{{v:performance.score-heavy}}`까지 |
| 2 | `{{ui:level_performance_severe-drops}}` | `{{v:performance.score-heavy}}` 초과, `{{v:performance.score-severe}}`까지 |
| 1 | `{{ui:level_performance_does-not-hold}}` | `{{v:performance.score-severe}}` 초과 |
| 없음 | `{{ui:level_performance_unknown}}` | 레벨이나 기기를 아직 측정하지 않음 |

점수는 레벨의 평균이 아니라 가장 무거운 순간에 대한 예측입니다. 3분 동안 가볍다가 1초 동안 멈추는 레벨은 그 1초의 점수를 받습니다

## 어디에서 볼 수 있나요

- 레벨 브라우저: 각 레벨 카드의 게이지와 필터의 `{{ui:root_level-filters_performance}}` 그룹
- 메뉴의 레벨 페이지: 게이지, 구간, 점수
- 레벨 에디터의 레벨 메타데이터: 내 기기와 기준 기기에서의 점수, 그리고 레벨에서 가장 무거운 순간의 타임스탬프

## 점수의 두 절반

**레벨의 절반**은 저장할 때마다 그 뒤 몇 초 동안, 작업을 계속하는 사이에 에디터에서 측정되어 메타데이터에 저장됩니다. 끝나기 전에 에디터를 떠나면 파일에는 이전 측정이 남습니다. 레벨이 무엇을 요구하는지 나타냅니다: 살아 있는 오브젝트 수, 그것들이 화면을 얼마나 덮는지, 이펙트와 포스트 프로세싱 패스가 몇 개 실행되는지. 이 기능 이전에 저장된 레벨에는 이 기록이 없고, 다시 저장될 때까지 `{{ui:level_performance_unknown}}`으로 표시됩니다. 에디터는 레벨을 열 때 이를 측정하고 에디터를 떠날 때까지 결과를 유지하지만, 파일에 쓰지는 않습니다

**기기의 절반**은 내 기기가 각 작업을 얼마나 빨리 처리하는지 나타냅니다. 기기를 측정하기 전까지 게임은 플랫폼의 기준 기기를 사용합니다. 설정도 반영됩니다: 렌더 스케일, 안티앨리어싱, 이펙트, 포스트 프로세싱은 다시 측정하지 않아도 점수를 바꿉니다

## 기기 측정하기

1. 메인 메뉴에서 `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`을 엽니다
2. `{{ui:settings_graphics-performance_measure}}`를 누릅니다. 측정에 도움이 되는 것을 창이 알려줍니다: 다른 앱과 게임 닫기, 휴대폰이나 노트북을 충전기에 연결하기, 기기를 만지지 않기
3. `{{ui:settings_graphics-performance_start}}`을 누르고 최대 {{v:performance.benchmark-max-seconds}}초 기다립니다. 설정 화면이 숨겨지고 게임이 테스트 레벨을 재생하며, 측정하는 내용을 위쪽 양 모서리에 표시합니다. 다른 앱으로 전환하지 마세요

`{{ui:settings_graphics-performance_stop}}`로 측정을 일찍 끝낼 수 있습니다. 중지되거나 시간이 초과된 측정은 아무것도 저장하지 않으며 이전 결과가 유지됩니다

끝나면 창에 결과가 표시됩니다: 내 기기에서의 데모 레벨 게이지, 기기를 제한하는 요소(프로세서 또는 그래픽 칩), 추천하는 `{{ui:settings_quick-setup_performance}}` 프리셋, 그리고 내 레벨이 구간마다 몇 개씩 들어가는지. `{{ui:settings_graphics-performance_again}}`으로 한 번 더 측정합니다

측정이 고르지 않았더라도(기기가 너무 뜨거웠거나 다른 앱이 바빴다면) 어떤 기준 기기보다 내 기기에 가깝기 때문에 게임은 그 결과를 그대로 쓰고, 창이 이를 알려줍니다. 더 정확한 점수를 얻으려면 다른 앱을 닫고 다시 측정하세요

## 다른 기기로 옮기기

측정 결과는 측정한 기기의 것입니다. 프로필 이전([[14_profile-transfer]])과 클라우드 저장은 이를 옮기지 않으므로, 새 기기는 다시 측정할 때까지 기준 기기에서 시작합니다
