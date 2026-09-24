---
title: Установка
date: 2026-09-24
tags: [developer, level_author]
---

# Установка

Как подключить SDK к проекту на .NET или на Unity и проверить, что он читает ваши уровни

## .NET: пакет BulletHero.SDK

Пакет называется `BulletHero.SDK`, собирается под `netstandard2.1` на C# 9. Оба числа взяты у Unity-проекта, поэтому одни и те же исходники собираются и в Unity, и без него. Сборка называется `BH.SDK.dll`, рядом с ней лежит XML-документация

Зависимости, все из NuGet:

| Пакет | Версия | Зачем |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP для уровней под паролем |
| `SharpZipLib` | 1.4.2 | tar и zip (gzip берётся из BCL) |

> [!warning] Предупреждение
> На момент написания (2026-09-24) пакет не опубликован на nuget.org. Соберите его из исходников командами ниже

```bash
git clone https://github.com/vertoker/bullet-hero-sdk.git
cd bullet-hero-sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll и BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

Папки вывода называются `bin~` и `obj~`, с тильдой, потому что Unity не импортирует папки с тильдой на конце. Дальше два варианта:
- подключить `.nupkg` из локальной папки: `dotnet add package BulletHero.SDK --source <папка>`, три зависимости придут вместе с ним
- сослаться на `BH.SDK.dll` напрямую и добавить три пакета выше самостоятельно, ссылка на DLL свои зависимости не приносит

## Unity

В корне репозитория лежит `package.json` с именем `com.vertoker.bullet-hero-sdk` и минимальной версией Unity `6000.0`. Игра подключает SDK как git submodule:

```bash
git submodule init
git submodule add -f https://github.com/vertoker/bullet-hero-sdk.git Assets/Plugins/BulletHeroSDK
```

Удаление - `git rm -r -f Assets/Plugins/BulletHeroSDK`. Раз `package.json` лежит в корне, Package Manager может добавить репозиторий и по git URL, но разработчики этот путь не используют и не описывают

Что Unity-проект должен дать сам:
- `Newtonsoft.Json` через пакет `com.unity.nuget.newtonsoft-json`
- `BouncyCastle.Cryptography` и `SharpZipLib` из NuGet (игра ставит их через NuGetForUnity)
- scripting define `BHSDK_UNITY` в Player Settings, иначе `UnityIntegration` выберет ветку без движка
- `BH.SDK.Roslyn.dll` в корне SDK. Unity применяет анализатор только к сборке, в папке которой он лежит, и к сборкам, которые на неё ссылаются, поэтому перенесённый в другое место он ничего не анализирует

## Проверка: пример ConsoleSmoke

`Samples~/ConsoleSmoke` - консольное приложение на `net8.0`, которое ссылается на собранную `BH.SDK.dll`, ровно как сторонний инструмент. Оно читает папку уровня, печатает имя, число объектов и поколение и прогоняет уровень туда и обратно через JSON и `.blob`

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

Дальше: [[2_level-format]]
