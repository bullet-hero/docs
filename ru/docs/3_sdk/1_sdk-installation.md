---
title: Установка
date: 2026-09-24
tags: [developer, level_author]
---

# Установка

Как подключить SDK к проекту на .NET или Unity и проверить, что он читает ваши уровни

Код SDK лежит в [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk). Лицензия MIT

## .NET

Пакет `BulletHero.SDK` пока не опубликован на nuget.org. Соберите его из исходников:

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll и BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

Затем подключите одно из двух:
- `.nupkg` из локальной папки: `dotnet add package BulletHero.SDK --source <папка>`. Три зависимости придут вместе с ним
- `BH.SDK.dll` напрямую. Тогда три пакета ниже добавьте сами: ссылка на DLL свои зависимости не приносит

Зависимости, все из NuGet:

| Пакет | Версия | Зачем |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP для уровней под паролем |
| `SharpZipLib` | 1.4.2 | tar и zip (gzip берётся из BCL) |

### Детали сборки

- сборка называется `BH.SDK.dll`, рядом с ней лежит XML-документация
- цель - `netstandard2.1`, язык - C# 9. Это те же числа, что у Unity-проекта, поэтому одни и те же исходники собираются и в Unity, и без него
- папки вывода - `bin~` и `obj~`. Тильда нужна, потому что Unity не импортирует папки с тильдой на конце

## Unity

Игра подключает SDK как git submodule:

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BulletHeroSDK
```

Удаление - `git rm -r -f Assets/Plugins/BulletHeroSDK`

Что Unity-проект должен дать сам:
- `Newtonsoft.Json` через пакет `com.unity.nuget.newtonsoft-json`
- `BouncyCastle.Cryptography` и `SharpZipLib` из NuGet (игра ставит их через NuGetForUnity)
- scripting define `BHSDK_UNITY` в Player Settings. Без него `UnityIntegration` выберет ветку без движка
- `BH.SDK.Roslyn.dll` в корне SDK. Unity применяет анализатор только к сборке из его папки и к сборкам, которые на неё ссылаются. Перенесённый в другое место, он ничего не анализирует

В корне репозитория лежит `package.json` с именем `com.vertoker.bullet-hero-sdk` и минимальной версией Unity `6000.0`. Поэтому Package Manager может добавить SDK и по git URL. Разработчики этот путь не используют и не описывают

## Проверка: пример ConsoleSmoke

`Samples~/ConsoleSmoke` - консольное приложение на `net8.0`. Оно ссылается на собранную `BH.SDK.dll`, ровно как сторонний инструмент.
Приложение читает папку уровня, печатает имя, число объектов и поколение. Затем прогоняет уровень туда и обратно через JSON и `.blob`

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <папка уровня>
```

| Код выхода | Значение |
|---|---|
| 0 | всё совпало |
| 1 | неверные аргументы |
| 2 | не найден `level.*` или `metadata.*` |
| 3 | прогон туда и обратно не совпал |
| 4 | файл новее этого SDK |

Вывод на встроенном уровне игры `new-zero-demo` (записан на SDK 0.15.0):

```
BH.SDK 0.15.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505132 bytes)
round trip Blob: equal (680751 bytes)
exit 0
```

Дальше - [[2_level-format]]

## Из чего состоит SDK

| Часть | Что это | Нужен Unity |
|---|---|---|
| `BH.SDK` | ядро: модели, сериализация, версии, правила, валидация, архивы, публикация, генераторы, связь с Afterbeat | нет |
| `UnityIntegration` | тонкий слой, где каждый файл компилируется и с Unity, и без него (`#if BHSDK_UNITY`), например логгер `Cat` | нет: вне Unity он компилируется прямо в ядро |
| `UnityExtensions` | преобразования в типы Unity, 2D-трансформы, движение аватара | да, всегда |
| `BH.SDK.Roslyn` | анализаторы и генератор исходников. Для каждой модели с `[GenerateModel]` он пишет `Equals`, копирование, кодеки JSON и `.blob` и обход валидации | работает во время компиляции |

Файл модели содержит только её поля и конструкторы. Всё повторяющееся пишет генератор. Поэтому поле нельзя забыть в одном из семи сгенерированных тел

## Зачем отдельная библиотека

- **Уровни переживают игру.** Уровень - это папка файлов в открытых форматах (JSON, tar.gz, zip, OpenPGP). Код, который их читает, тоже открыт. Уровень остаётся читаемым, даже если игры, которая его записала, больше нет
- **Связь с другими ритм-играми.** Конвертация в *Afterbeat* (бывший *Project Arrhythmia*) и обратно уже есть в SDK. Подробнее - [[9_afterbeat-interop]]
- **Быстрые исправления.** Дефект формата виден снаружи. Любой, кто читает код, может сообщить о нём или прислать исправление
- **Сторонние инструменты.** Конвертер, валидатор, генератор уровней или мод работают с теми же моделями, что и игра. Восстанавливать их по файлам не нужно
- **Серверы.** Ядро собирается без Unity как `netstandard2.1`. Поэтому сервер выполняет те же проверки над теми же моделями, что и клиент
