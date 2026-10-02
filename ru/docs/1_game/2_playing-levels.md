---
title: Как играть в уровни
date: 2026-10-02
tags: [player]
---

# Как играть в уровни

Выберите уровень в списке уровней, задайте условия забега и запустите его. Чужой уровень - это обычная папка: скопируйте её в папку levels и обновите список

## Главное меню

| Кнопка | Что делает |
|---|---|
| `{{ui:menu_main_levels-btn}}` | список уровней, описан ниже |
| `{{ui:menu_main_editor-btn}}` | редактор уровней, [[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | арена без уровня и обучение, [[13_sandbox]] |
| `{{ui:settings_common_title}}` | все настройки, [[4_settings]] |
| `{{ui:menu_main_story-btn}}` | пока не работает |
| `{{ui:menu_main_multiplayer-btn}}` | пока не работает |

## Список уровней

`{{ui:menu_main_levels-btn}}` в главном меню открывают список уровней. Уровни берутся из трёх мест:

- `{{ui:root_level-source_local}}` - папка `levels`, [[1_installation]]
- `{{ui:root_level-source_builtin}}` - уровни, которые идут с игрой
- `Мастерская` - только в сборке для Steam. Здесь видны уровни, на которые вы подписаны. Коллекции ресурсов, на которые вы подписаны, - не уровни: они появляются в библиотеке редактора, [[16_library-and-collections]]

Сверху есть поиск, `{{ui:root_level-browser_sort}}` и `{{ui:root_level-browser_layout}}` (сетка или список). Список открывается сеткой.
Сортировать можно `{{ui:root_level-browser_sort-relevance}}`, `{{ui:root_level-browser_sort-title}}`, `{{ui:root_level-browser_sort-duration}}`, `По прогрессу` и `{{ui:root_level-browser_sort-recent}}`

Скопировали уровень в папку? Нажмите `{{ui:root_level-browser_refresh}}`, и список обновится

Замок на карточке значит, что уровень защищён паролем

Удержание или правый клик по карточке открывает меню: `{{ui:level_passphrase_open}}` и `{{ui:root_level-browser_delete}}`.
`{{ui:root_level-browser_delete}}` у уровня из `Мастерской` отменяет подписку на предмет и удаляет его файлы. Для этого нужен запущенный Steam: иначе Steam скачает уровень заново. Встроенные уровни удалить нельзя

## Как добавить чужой уровень

Уровень - это обычная папка с файлами. Её можно заархивировать и отправить другу

**Папка.** Скопируйте папку уровня в `levels` и нажмите `{{ui:root_level-browser_refresh}}`.
Копировать нужно саму папку уровня: ту, где лежат `level.json` (или `level.blob`) и `metadata.json`

**Архив.** Откройте редактор и создайте новый уровень генератором `{{ui:gen_level_archive}}`.
Затем выберите файл кнопкой `{{ui:editor_create-level_archive-choose}}`

| Файл | Результат |
|---|---|
| `.zip`, `.tar.gz` | открывается |
| `.zip` с собственным паролем, `.zip.gpg`, `.tar.gz.gpg` | открывается после `{{ui:editor_create-level_archive-protected}}` |
| `.7z` | пока отклоняется. Перепакуйте его в zip |
| что-то другое | отклоняется, [[5_troubleshooting]] |

Переименованный архив тоже откроется: игра узнаёт формат по байтам файла.
Архив из старой версии игры обновится при импорте

Импортированный уровень по умолчанию получает свой id. Поэтому он не перезапишет уровень, который уже есть на устройстве

Подробнее - [[6_sharing-by-hand]]

## Экран уровня

На экране уровня видны обложка, авторы, описание и автор музыки. Там же кнопки `{{ui:level_level-view_authors}}` и `{{ui:level_level-view_licenses}}`

Имя автора и строка о музыке открывают свою ссылку, если она записана в метаданных уровня

Возрастной рейтинг указывает автор уровня. Игра его не проверяет

"Есть контент, созданный ИИ" появляется, если автор заявил, что уровень, его обложка или один из ресурсов сгенерированы ИИ. Это тоже заявление самого автора. Отсутствие строки не значит "без ИИ": автор мог просто ничего не указать

Перед забегом можно выбрать условия:

| Условие | Варианты |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}` (забег не заканчивается), `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}`, `{{ui:menu_levelview_options-lifes_option-custom}}` (ползунок до 16) |
| `{{ui:field_common_speed}}` | `0.5`, `1.0`, `2.0`, `{{ui:menu_levelview_options-lifes_option-custom}}` (ползунок до 2). Уровень и музыка меняются вместе |
| `Контрольные точки` | вкл. или выкл., [[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | вкл. или выкл. Аватар проходит сквозь всё, [[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`, [[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | число, `{{ui:level_level-view_seed-randomize}}`, `{{ui:level_level-view_seed-clear}}`. `0` - новый сид на каждый забег, [[8_determinism]] |

`Начать` запускает забег

В паузе есть `{{ui:game_pause-window_continue-btn}}`, `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}` (когда точка уже достигнута), `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}` и `{{ui:game_game-result_back-to-menu}}`. `{{ui:game_game-result_back-to-options}}` возвращает на экран уровня с теми условиями, с которыми начат забег, или на вкладку `Играть` редактора, если забег начат оттуда

## Окно результата

Окно показывает `Пройдено` или `{{ui:game_game-result_lose}}` и три секции: `Прогресс`, `{{ui:game_game-result_section-damage}}` и `{{ui:game_game-result_section-conditions}}`

- строки: `Пройдено`, `{{ui:game_game-result_checkpoint}}`, `{{ui:field_common_time}}`, `{{ui:game_game-result_length}}`, `{{ui:game_game-result_hits}}`, `{{ui:game_game-result_lives-left}}`, `{{ui:game_game-result_streak}}`
- условия забега: `{{ui:field_common_speed}}`, `{{ui:menu_levelview_options-lifes_title}}`, `{{ui:menu_levelview_options-bot}}`, `{{ui:game_game-result_seed}}`, `Чекпоинты`. У забега `{{ui:menu_levelview_options-no-collision_title}}` к `{{ui:menu_levelview_options-lifes_title}}` добавляется `· Без столкновений`
- кнопки: `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}`, `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}`, `{{ui:game_game-result_back-to-menu}}`

При поражении окно по умолчанию не открывается. Вместо этого забег отматывается к последней контрольной точке.
Изменить это - `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`

## Рекорды

На экране уровня есть блок рекорда: `{{ui:menu_levelview_record-best}}`, `{{ui:menu_levelview_record-attempts}}` и `{{ui:menu_levelview_record-clears}}` (или `{{ui:menu_levelview_record-none}}`)

Рекорд свой для каждого набора условий: жизни, скорость, контрольные точки, столкновения и бот. Блок показывает рекорд для условий, выбранных сейчас.
Попытки и прохождения считаются для любого забега

Как выбирается рекорд - [[10_statistics]]

## Пометки на карточках

| Пометка | Что значит |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | папка мастерской есть на диске, но вы на неё не подписаны. Видна, только если включено `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` |
| `{{ui:root_level-entry_unverified}}` | источник уровней не ответил |
| `{{ui:root_level-entry_newer-version}}`, `{{ui:root_level-entry_newer-file}}` | эта версия игры уровень не откроет, [[5_troubleshooting]] |

## Удаление уровня

Удержание или правый клик по карточке → `{{ui:root_level-browser_delete}}`. Игра сначала спросит подтверждение

Вместе с уровнем можно удалить его статистику (`{{ui:root_level-delete_statistics}}`) и бэкапы (`{{ui:root_level-delete_backups}}`)

Для удаления защищённого уровня пароль не нужен
