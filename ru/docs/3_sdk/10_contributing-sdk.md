---
title: Вклад в SDK
date: 2026-09-24
tags: [developer]
---

# Вклад в SDK

Где записаны правила SDK для контрибьюторов и как его собрать, протестировать и упаковать

SDK - отдельный репозиторий, [vertoker/bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk), ветка по умолчанию `master`. Изменения приходят пулл-реквестами. Правила для контрибьюторов лежат в самом репозитории, рядом с кодом, который они описывают, а эта страница только указывает на них

## Где правила

| Файл | Что в нём |
|---|---|
| [README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/README.md) | зависимости, пакеты уровней, сборка DLL и пакета, пример-проверка |
| [CLAUDE.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/CLAUDE.md) | модель мышления, указатель папок и соглашения всей библиотеки |
| `CLAUDE.md` в каждой папке | локальные правила этой папки, например [Serialization](https://github.com/vertoker/bullet-hero-sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/vertoker/bullet-hero-sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/vertoker/bullet-hero-sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/VERSIONING.md) | оси версий, поколения, миграция и отказ |
| [Docs/IDENTIFIERS.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/IDENTIFIERS.md) | как модель адресует сущности: Guid, int, кадр, путь к полю |
| [Docs/UGC-LICENSING-POLICY.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/UGC-LICENSING-POLICY.md) | политика лицензирования пользовательского контента, правится вместе с `TrustedSourceCatalog` |
| [Versions/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Versions/README.md) | как написать снимок и мигратор |
| [Generators/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Generators/README.md) | контракт генератора |
| [Roslyn/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Roslyn/README.md) | анализаторы и генератор моделей, как их пересобрать |
| [UnityIntegration/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/UnityIntegration/README.md) | контракт двойной компиляции |
| [CHANGELOG.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/CHANGELOG.md) | изменения по версиям `sv`, сверху раздел `[Unreleased]` |

## Инварианты, которые стоит знать заранее

- ядро не ссылается ни на один тип `UnityEngine`. Код, которому нужен движок, идёт в `UnityExtensions/` или в `UnityIntegration/` за `#if BHSDK_UNITY` с веткой без движка
- код одинаково работает с файлами и с данными в памяти и использует только асинхронность из BCL
- `netstandard2.1` и C# 9 - то, с чем компилируется Unity-проект, их не поднимают
- модель - это `[GenerateModel] public sealed partial class`, и каждое сериализуемое поле берёт ключ из `Names.cs`
- любое изменение модели - новое поколение со снимком и мигратором, см. [[5_versioning]]
- версия SDK живёт в трёх местах: `SdkVersion.cs`, `package.json` и `<Version>` в `BH.SDK.csproj`. `SdkVersionAgreementTests` падает, если одна из них сдвинулась одна

## Сборка и тесты

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

Здесь без Unity собираются те же исходники, что компилирует Unity, поэтому файл, нарушивший контракт независимости от движка, ломает эту сборку. Вывод идёт в `bin~` и `obj~`. Команда упаковки только создаёт `.nupkg`, из репозитория ничего не отправляется на nuget.org

> [!caution] Внимание
> Анализаторы и генератор моделей поставляются готовой `BH.SDK.Roslyn.dll` в корне SDK. После правки чего-либо в `Roslyn/` пересоберите и скопируйте её, иначе продолжит работать старый генератор, хотя исходники говорят другое

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Внутри редактора Unity то же самое делает пункт меню **Tools > BH.SDK.Roslyn > Build Analyzer**
