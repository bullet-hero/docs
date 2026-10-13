---
title: 키프레임과 이징
date: 2026-10-12
tags: [level_author]
---

# 키프레임과 이징

키프레임은 한 트랙의 한 프레임에서의 값과, 그 값에 도달하는 이징입니다. 레벨에서 움직이거나 색이 바뀌거나 켜지고 꺼지는 모든 것은 키프레임 목록입니다

기본 개념 - [[3_how-the-editor-thinks]]. 키프레임 인스펙터의 모든 필드 - [[5_object-properties]]

## 애니메이션할 수 있는 것

트랙마다 다른 트랙과 독립된 자기 키프레임이 있습니다:

| 소유자 | 트랙 |
|---|---|
| 모든 오브젝트 | 위치, 회전, 스케일, 크기, 앵커, 피벗 |
| 도형 | 색상, UV |
| 텍스트 | 색상, 폰트 크기, `{{ui:editor_dummy_text-11}}` (텍스트가 얼마나 쓰였는지), `{{ui:editor_dummy_text-12}}` (그중 얼마가 마스크 뒤에 숨었는지) |
| 카메라 | 위치, 회전, 줌, 피벗, 흔들림 |
| 레벨 | 배경, 테마, 화면 제한, 포스트 프로세싱 효과 12가지 각각 |
| 플레이어 | 크기, 속도, 표시 여부, 조작, 충돌 |

도형의 색상 키프레임은 오브젝트의 직사각형 영역 위에 펼친 그레이디언트일 수도 있습니다. `{{ui:editor_keyframe-color_layout}}` 필드가 레이아웃을 정합니다: `{{ui:enum_color4-x4-key-type_value}}` (단색), `{{ui:enum_color4-x4-key-type_vertical}}` (아래에서 위로), `{{ui:enum_color4-x4-key-type_horizontal}}` (왼쪽에서 오른쪽으로), `{{ui:enum_color4-x4-key-type_bari-centrical}}` (모서리마다 색 하나)

폰트 크기 키프레임은 월드 단위의 고정 크기인 숫자 하나이거나, `{{ui:field_common_auto-size}}` 옵션을 켠 범위입니다. 텍스트는 범위의 `{{ui:field_common_max}}` 크기로 그려지고, 직사각형 영역에 맞을 때까지 `{{ui:field_common_min}}` 쪽으로 줄어듭니다

오브젝트의 키프레임은 구간의 시작부터 셉니다. 그래서 오브젝트를 시간상으로 옮기면 애니메이션 전체가 함께 옮겨집니다

위치는 부모 기준으로 정합니다. 키프레임은 이전 키프레임에 대한 증가분이 아니라 값 자체를 저장합니다

플레이어의 표시 여부, 조작, 충돌은 켜짐 아니면 꺼짐입니다. 이 키프레임에는 이징이 없습니다: 섞을 것이 없기 때문입니다

빈 플레이어 트랙의 첫 키프레임은 화면에서 아무것도 바꾸지 않습니다: 표시 여부, 조작, 충돌은 켜진 상태로, 크기와 속도는 플레이어의 평소 값으로 시작합니다. 조작이 꺼져 있거나 플레이어가 숨겨져 있으면 플레이어를 조종할 수 없습니다: 커서가 사라지고 누르는 입력이 인식되지 않습니다. 숨겨진 플레이어도 피격됩니다: 그것을 정하는 것은 충돌뿐입니다

## 텍스트: 채우기와 등장

두 텍스트 트랙은 서로 다른 방식으로 글자를 숨깁니다. 둘 다 0부터 1까지의 비율을 받고 텍스트의 글자 수를 셉니다

**`{{ui:editor_dummy_text-11}}` 트랙**은 텍스트 중 쓰인 부분의 비율입니다: 0 - 아무것도 없음, 1 - 전부. 쓰이지 않은 글자는 아예 그려지지 않으므로 줄이 짧아집니다. 빈 트랙은 텍스트 전체를 씁니다. 키프레임마다 방향을 정합니다:
- `{{ui:enum_text-fill-direction_forward}}` (기본값) - 첫 글자부터, 타자기처럼
- `{{ui:enum_text-fill-direction_backward}}` - 마지막 글자부터
- `{{ui:enum_text-fill-direction_from-center}}` - 가운데에서 바깥으로 자라남
- `{{ui:enum_text-fill-direction_to-center}}` - 양 끝에서 자라나 가운데에서 만남

**`{{ui:editor_dummy_text-12}}` 트랙**은 마스크 뒤에 숨겨진 글자의 비율입니다: 0 - 모두 보임, 1 - 모두 마스크됨. 숨겨진 글자는 자리를 유지하고 마스크 문자로 그려지며, 기본값은 {{v:text.appearing-mask-default}}입니다. 마스크는 텍스트 오브젝트의 `{{ui:editor_inspector-appearing_mask}}` 필드이며, 여기에 문자가 여러 개 있으면 숨겨진 글자마다 그중 하나를 씁니다. 빈 트랙은 아무것도 숨기지 않습니다. 키프레임마다 모드를 정합니다:
- `{{ui:enum_text-appearing-mode_random}}` (기본값) - 흩어져 있지만 실행할 때마다 똑같이 흩어집니다. 0.3에서 숨겨진 글자는 0.6에서도 숨겨져 있으므로, 텍스트가 깜빡이지 않고 점점 드러납니다
- `{{ui:enum_text-appearing-mode_forward}}` - 숨겨진 글자가 끝에 있어, 텍스트가 앞에서부터 나타납니다
- `{{ui:enum_text-appearing-mode_backward}}` - 숨겨진 글자가 앞에 있습니다

한 줄을 타이핑하듯 나타내려면 `{{ui:editor_dummy_text-11}}` 트랙을 0에서 1까지 애니메이션하십시오. 노이즈 속에서 해독하듯 드러내려면 `{{ui:editor_dummy_text-12}}` 트랙을 1에서 0까지 애니메이션하십시오

## 조언

- 움직이는 것에만 키프레임을 넣으십시오. 키프레임이 없는 트랙은 기본값을 씁니다
- 정확히 비트에 맞춘 변화에는 `Constant` 이징을 쓰십시오. 예를 들어 드롭에서 테마를 바꿀 때입니다
- 회전은 한 바퀴에서 되돌아가지 않습니다: 0도 키프레임과 720도 키프레임은 오브젝트를 두 바퀴 돌립니다. 파일과 AI 어시스턴트가 쓰는 라디안으로는 각각 0, 12.566입니다

## 두 키프레임 사이

첫 키프레임 이전과 마지막 키프레임 이후에는 값이 그대로 유지됩니다. 두 키프레임 사이에서는 게임이 지나간 시간의 비율을 구하고, 이를 이징에 통과시킨 다음 두 값을 섞습니다

비율은 그려진 프레임이 아니라 시간으로 셉니다. 그래서 커브는 30 fps에서도 144 fps에서도 같습니다

**이징은 쌍 중 뒤쪽 키프레임에 속합니다.** 키프레임의 이징은 이전 키프레임에서 이 키프레임에 도착하는 부분을 정합니다. 그래서 트랙의 첫 키프레임의 이징은 절대 드러나지 않습니다. 새 키프레임에는 `Linear` 이징이 지정됩니다

`{{ui:hint_editor_inspector_ease_header}}` 필드는 `{{ui:editor_search-title_ease}}` 창을 엽니다. 이 창에서는 이징마다 자기 커브가 그려져 있습니다. 여러 키프레임을, 다른 트랙에 있더라도 함께 선택해서 한 번의 실행 취소 단계로 바꿀 수 있습니다

## 이징 29가지

`Linear` 이징은 직선입니다. `Constant` 이징은 이전 값을 유지하다가 키프레임에서 바로 바뀝니다

나머지 27가지는 세 개씩 묶인 아홉 계열입니다: `In`, `Out`, `InOut`. 예: `InSine`, `OutSine`, `InOutSine`

| 계열 | 모양 |
|---|---|
| `Sine` | 가장 부드러운 커브 |
| `Quad`, `Cubic`, `Quart`, `Quint` | 2, 3, 4, 5제곱 |
| `Expo` | 지수 |
| `Circ` | 원의 4분의 1 |
| `Back` | 범위를 넘어갔다가 돌아옴 |
| `Elastic` | 값 주위에서 진동함 |

`In` 계열은 천천히 시작해 빠르게 끝납니다. `Out` 계열은 빠르게 시작해 차분히 멈춥니다. `InOut` 계열은 양 끝에서 느립니다. `Sine`부터 `Expo`까지 각 계열은 앞의 계열보다 더 급격합니다

> [!caution] 주의
> `Back`, `Elastic` 이징은 범위를 벗어납니다: `Out` 쪽은 목표를 지나치고, `In` 쪽은 시작점 너머로 물러납니다. 콜라이더는 오브젝트와 함께 움직입니다. 그래서 안전 지대 가장자리에서 멈추도록 만든 탄환은 몇 프레임 동안 안전 지대에 들어갑니다

## 무작위 값

키프레임의 값이 꼭 숫자 하나일 필요는 없습니다:
- 숫자: `{{ui:field_common_value}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_float-type_random-min-max-step}}`
- 벡터(위치, 스케일 등): `{{ui:field_common_value}}`, `{{ui:enum_vector-type_random-rect}}`, `{{ui:enum_vector-type_random-rect-step}}`, `{{ui:enum_vector-type_random-circle}}`, `{{ui:enum_color-type_random-lerp}}`, `{{ui:enum_vector-type_random-lerp-step}}`
- 색상: `{{ui:field_common_value}}`, `{{ui:editor_events-timeline_track_theme}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}` 형태는 각 축을 따로 고릅니다. `{{ui:enum_color-type_random-lerp}}` 형태는 모든 축에 숫자 하나를 고르므로, 점이 A, B 사이의 직선 위에 놓입니다. 간격이 있는 형태는 결과를 간격의 배수로 내림합니다. 간격이 0이면 그리드가 꺼지고, 간격이 없는 형태처럼 동작합니다. 그다음 키프레임은 다른 키프레임처럼 섞입니다

같은 시드는 같은 레벨을 만듭니다. 무작위 수는 시드, 키프레임의 프레임, 레이어, 오브젝트의 시작 프레임, 트랙, 채널로 계산됩니다. 자세히 - [[8_determinism]]

다음: [[2_rhythm-and-structure|리듬과 구조]], [[6_themes|테마]]
