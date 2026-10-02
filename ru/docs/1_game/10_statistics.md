---
title: Статистика
date: 2026-10-02
tags: [advanced_player]
---

# Статистика

Игра считает попытки, смерти, попадания и время по каждому уровню и по всему устройству. Всё хранится локально в папке stats. Рекорд записывается отдельно для каждого набора условий забега

## Два файла

| Файл | Что хранит |
|---|---|
| `stats/statistics.json` | всё о вас: по всем уровням и экранам |
| `stats/<LevelId>.json` | всё, что вы делали с одним уровнем |

Файлы в JSON, время в UTC. Никуда ничего не отправляется

Папка `stats` лежит рядом с `levels` в папке игры, [[1_installation]]. Внутри уровня её нет никогда.
Так уровень, отправленный другу, не приедет уже пройденным. А ваш прогресс переживёт удаление уровня и повторный импорт

## Вкладка "Профиль"

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}` показывает общий файл устройства:

| Секция | Строки |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`, `{{ui:settings_profile_last-played}}`, `{{ui:settings_profile_launches}}`, `{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`, `{{ui:settings_profile_game-time}}`, `{{ui:settings_profile_editor-time}}`, `{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`, `{{ui:settings_profile_clears}}`, `{{ui:settings_profile_deaths}}`, `{{ui:settings_profile_hits}}`, `{{ui:settings_profile_levels-played}}`, `{{ui:settings_profile_levels-cleared}}`, `{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`, `{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`, `{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`, `{{ui:settings_profile_tutorial-first}}`, `{{ui:settings_profile_tutorial-last}}` - прохождение засчитывается, только когда пройдены все шаги [[13_sandbox|обучения в песочнице]] |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`, `{{ui:settings_profile_levels-deleted}}`, `{{ui:settings_profile_objects}}`, `{{ui:settings_profile_operations}}`, `{{ui:settings_profile_generators}}`, `{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`, `{{ui:settings_profile_device-touch}}`, `{{ui:settings_profile_device-gamepad}}`, `{{ui:settings_profile_device-gyro}}` |

Время считается в реальных секундах, а не во времени уровня. Замедление у контрольной точки и забег на половинной скорости учитываются столько, сколько шли на самом деле

Строки устройств показывают, какое устройство вело аватара во время игры. Просто подключённое не считается

## По уровню

Файл уровня хранит:

- когда вы впервые и последний раз в него играли
- реальное время в уровне и число заходов
- попытки (каждый рестарт - новая), прохождения, смерти, попадания, рывки
- возвраты к контрольной точке и брошенные забеги
- самую дальнюю достигнутую точку и первое прохождение
- где в уровне вы погибаете: по доле длины и по контрольным точкам

## Рекорды

Рекорд записывается под условия забега: жизни, скорость, контрольные точки вкл. или выкл., столкновения вкл. или выкл. и бот.
Скорость учитывается до сотых, ровно как на экране

Дзен (0 жизней) по-прежнему считает попадания: в его числа идёт каждое столкновение, от них избавлены только жизни и конец забега

Забег бьёт рекорд с теми же условиями, если, по порядку:

1. он дошёл дальше
2. он получил меньше попаданий
3. он закончился с большим числом жизней
4. он потратил меньше рывков

Рекорд также хранит сид забега и версию уровня на тот момент.
Версия не входит в условия. Поэтому рекорд, поставленный до переделки уровня, остаётся виден, а версия показана рядом

**Забег из редактора считается, но рекордов не ставит.** Он добавляется к попыткам, смертям и попаданиям. Рекорда, лучшего прогресса и первого прохождения он не даёт, потому что уровень существовал только в памяти

## Запись, удаление, заморозка

Игра записывает статистику каждые 30 секунд. И сразу - в конце забега, при смене экрана и при выходе.
Вылет стоит не больше 30 секунд данных

- **Удалить:** `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`. Там есть `{{ui:settings_other_cache-orphan-statistics}}` и `{{ui:settings_other_cache-all-statistics}}`
- **Удалить с уровнем:** удаление уровня предлагает `{{ui:root_level-delete_statistics}}`
- **Заморозить:** анонимный режим останавливает любую запись до закрытия игры, [[4_settings]]

> [!warning] Предупреждение
> Папка уровня, скопированная вручную, сохраняет id уровня. Оригинал и копия делят один файл статистики
