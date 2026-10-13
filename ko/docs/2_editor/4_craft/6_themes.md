---
title: 테마
date: 2026-10-02
tags: [level_author]
---

# 테마

테마는 오브젝트가 슬롯 번호로 참조하는 64색 팔레트입니다. 테마를 바꾸면 그 테마를 참조하는 모든 것이 함께 바뀝니다

`Theme` 타입의 색상은 자기 색상을 저장하지 않고 슬롯 번호만 저장합니다. 현재 프레임에서 활성인 테마의 그 슬롯에 있는 색상을 가져옵니다

이것이 직접 입력한 색상보다 나은 이유와 어떤 테마에서도 레벨을 읽기 쉽게 유지하는 방법 - [[5_color-and-postprocessing]]

## 테마에 담기는 것

- **이름** - 목록과 선택 창에 표시됩니다
- **ID**, `ThemeId`. 테마 키프레임은 이름이 아니라 이것으로 테마를 참조합니다
- 8x8 그리드의 **64가지 색상**, 각각 투명도 포함
- 슬롯마다 **슬롯 이름**, 선택 사항. 슬롯 하나라도 이름을 붙이기 전까지 파일은 이름 목록 대신 `null`을(를) 저장합니다

테마는 레벨 폴더의 별도 파일이 아니라 `level.json` 안의 데이터입니다([[1_level-needs]] 참고). 레벨에는 테마를 몇 개든 넣을 수 있습니다

게임은 슬롯에 아무 역할도 정해 두지 않습니다: 게임에 들어 있는 `Balanced` 테마는 그저 64가지 색상을 색조별로 묶어 둘 뿐입니다

## 색상이 값을 찾는 방법

두 단계입니다:
1. 이벤트 타임라인의 `Theme` 트랙이 이 프레임에서 어느 테마가 활성인지 알려 줍니다
2. `Theme` 타입의 색상이 활성 테마의 0부터 63까지의 슬롯 중 하나를 지정합니다

테마를 참조할 수 있는 것에는 예를 들어 도형의 색상(모서리마다 따로), 텍스트의 색상, 레벨 배경이 있습니다

**슬롯의 위치가 곧 그 슬롯의 정체입니다.** 색상을 다른 슬롯으로 옮기면 이전 슬롯을 참조하던 모든 것의 색이 바뀝니다

## 시간에 따라 테마 바꾸기

두 테마 키프레임 사이에서 게임은 팔레트 전체를 한 테마에서 다른 테마로 부드럽게 섞습니다. 이징은 뒤쪽 키프레임에서 가져옵니다([[5_keyframes-and-easing]] 참고)

테마 키프레임이 하나도 없으면 모든 슬롯이 흰색입니다

> [!warning] 경고
> 새 키프레임은 `Linear`을(를) 받으므로, 팔레트가 이전 테마 키프레임부터 이 키프레임까지 내내 서서히 바뀝니다. 드롭에서 정확히 테마가 바뀌게 하려면 드롭 지점의 키프레임에 `Constant`을(를) 지정하십시오

> [!caution] 주의
> 테마 키프레임은 테마 자체보다 오래 남을 수 있습니다. 키프레임이 아직 참조하는 테마를 삭제하면 해당 프레임이 모두 흰색이 됩니다. 키프레임 자체는 남습니다. 에디터는 그런 테마를 삭제하기 전에 한 번 더 묻습니다

## 테마를 만들고 편집하는 방법

레벨 리소스 중 `Themes` 탭에 레벨의 테마가 표시됩니다. 이 탭에는 `{{ui:settings_level-settings_resources-themes-add}}`, `{{ui:settings_level-settings_resources-themes-import}}`이(가) 있습니다. 행을 클릭하면 `{{ui:settings_level-settings_theme-editor}}`이(가) 열립니다:
- 테마의 `{{ui:field_common_name}}`
- `Theme Id`, `{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- 8x8 그리드. 칸을 클릭하면 그 칸이 선택되고, 번호와 함께 `Color:`이(가) 표시되며, 그리드 아래의 색상환에 색상이 불러와집니다
- 선택한 칸의 `{{ui:editor_theme-editor_color-name}}`

에디터는 복사본에서 작업합니다. 저장하기 전까지는 아무것도 레벨에 들어가지 않습니다. 저장 자체는 실행 취소 한 단계입니다

## 슬롯을 고르는 방법

색상을 `Theme`(으)로 바꾸고 `{{ui:editor_select-theme_color}}`을(를) 엽니다

그리드는 재생 헤드가 아니라 편집 중인 키프레임의 프레임에서 섞인 그대로의 팔레트를 보여 줍니다. 옆에는 그 프레임 앞뒤의 테마 키프레임 두 개와, 각 키프레임에서 선택한 슬롯에 들어 있는 색상이 표시됩니다. 이름 없는 슬롯에는 `{{ui:editor_search_unnamed}}` 라벨이 붙습니다

## 공유하고 가져오는 방법

- **이 기기의 공유 라이브러리.** 테마 행의 `{{ui:editor_level-theme-item_export}}`은(는) 테마를 `resources/themes`에 저장합니다 - 기기 전체의 공유 라이브러리이며, `resources`은(는) `levels` 옆에 있습니다([[4_level-folder-and-backups]] 참고). `{{ui:settings_level-settings_theme-library}}`은(는) 라이브러리를 보여 주고 이미 `{{ui:editor_theme-library-item_in-level}}`인 것을 표시합니다. `{{ui:editor_library_delete}}`은(는) 라이브러리에서 테마를 지웁니다. 가져오기는 테마를 레벨에 복사하므로, 레벨은 라이브러리에 의존하지 않습니다. `{{ui:settings_level-settings_theme-library}}`에는 컬렉션의 테마도 출처 칩과 함께 표시됩니다 - [[16_library-and-collections]]
- **게임의 테마.** `{{ui:editor_search-title_theme}}`은(는) 레벨의 테마 옆에 게임과 함께 제공되는 테마도 보여 줍니다

다음: [[5_color-and-postprocessing|색상, 테마, 포스트 프로세싱]], [[1_readability-and-fairness|가독성과 공정성]]
