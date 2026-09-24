---
title: Как написать генератор
date: 2026-09-24
tags: [developer]
---

# Как написать генератор

Как генератор собирается из базовых классов SDK и что он обязан соблюдать, чтобы работать в редакторе

Генератор создаёт содержимое уровня по нескольким параметрам вместо того, чтобы автор расставлял каждый объект руками. Добавить генератор - значит добавить один класс: хост строит форму, оценку и отмену по контракту, никто не пишет для него интерфейс и никакой список не правится. Что делают встроенные генераторы, описано на [[8_generators]]

## Три вида

| Вид | Создаёт | Базовый класс | Точка входа |
|---|---|---|---|
| `Level` | новые `Level` и `LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | новые объекты и ресурсы в активной области | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | правки уже существующих объектов | `BaseModifier<TParams>` | `Run(context, parameters)` |

У Content и Modifier одна точка входа, они различаются намерением и `GeneratorRequirements`. Модификатору по умолчанию нужно выделение. Для генераторов, которые создают объекты, есть `BaseSpawnGenerator<TParams>`: он создаёт, привязывает к родителю и размещает во времени каждый объект, так что конкретному классу остаётся только математика расстановки

## Без реестра

`GeneratorRegistry` находит все генераторы через рефлексию при первом обращении, и два генератора с одинаковым `NameKey` падают прямо там. На момент написания сканируется только собственная сборка SDK, поэтому новый генератор живёт в репозитории SDK и приходит пулл-реквестом (см. [[10_contributing-sdk]])

## Пример

Ряд объектов, построенный на тех же классах, что встроенный `RadialGenerator`:

```csharp
using BH.SDK.Generators;
using BH.SDK.Generators.Spawn;
using BH.SDK.Rules;

public class RowGenerator : BaseSpawnGenerator<RowGenerator.Parameters>
{
    public override string NameKey => "gen_geometry_row";

    public override GeneratorHints Hints { get; } = new GeneratorHints.Builder()
        .Section(GeneratorSections.Main, SpawnParameters.MainFields)
        .Section(GeneratorSections.Main, nameof(Parameters.Count), nameof(Parameters.Spacing))
        .Section(GeneratorSections.Additional, SpawnParameters.AdditionalFields)
        .Section(GeneratorSections.Additional, nameof(Parameters.StartX), nameof(Parameters.Y))
        .Range(nameof(Parameters.Count), 1, 256)
        .Range(nameof(Parameters.Spacing), 0f, ValueRules.MaxPos)
        .Range(nameof(Parameters.StartX), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(Parameters.Y), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(SpawnParameters.Size), ValueRules.MinSca, ValueRules.MaxSca)
        .Build();

    protected override void Generate(GeneratorContext context, Parameters parameters)
    {
        for (var i = 0; i < parameters.Count; i++)
        {
            var obj = Spawn(context, parameters, $"row_{i}", context.Span);
            AddPosition(obj, parameters.StartX + i * parameters.Spacing, parameters.Y, obj.Span.StartFrame);
        }
    }

    // Spawn добавляет ключ размера и ключ цвета, AddPosition - третий
    protected override GeneratorCost EstimateTyped(GeneratorContext context, Parameters parameters)
        => new GeneratorCost(parameters.Count, parameters.Count * 3);

    public class Parameters : SpawnParameters
    {
        public int Count = 8;
        public float Spacing = 2f;
        public float StartX;
        public float Y;
    }
}
```

`NameKey` имеет форму ключа локализации, хост показывает название через свою таблицу строк

## Обязательные правила

- **Меняйте уровень только через `GeneratorContext`** (`Create`, `Edit`, `Delete`, `SetValue` и другие). Он записывает каждое изменение в `GeneratorChangeLog`, и на этом держится вся отмена. Прямое изменение модели компилируется и молча ломает отмену
- **Каждое поле указано в секции, у каждого числа есть `Range`.** Порядок полей из рефлексии не гарантирован, а хосту не к чему прижать неограниченное число. Диапазоны проверяет тест
- **Параметры - публичные изменяемые поля и конструктор без параметров.** К ним привязывается форма, их сериализует пресет. Не перекрывайте унаследованное поле, всё адресуется по имени поля
- **Оценка совпадает с запуском.** Хост показывает её до запуска и отказывает в запуске, если он выйдет за `LevelRules.MaxObjects`
- **Случайность берётся из `context.CreateRandom()`,** а не из `System.Random`: одно и то же зерно даёт один и тот же уровень на любой платформе
- **Привязывайте созданное к `context.Parent`,** именно это позволяет хосту собрать весь запуск в один объект
- **Объявите `GeneratorRequirements.LevelScope`,** если трогаете `context.Game` или `context.Audio`: оба равны `null`, пока активная область - префаб
- **Переопределите `IsDangerousTyped`,** если сочетание параметров удаляет или переписывает содержимое за пределами окна, на которое смотрит автор. Тогда хост попросит подтверждение

> [!info] Интересно
> В SDK нет декодера аудио, FFT и загрузчика картинок. Генератор, которому нужны такие данные, объявляет `GeneratorRequirements.ExternalAnalysis` и реализует интерфейс из `External/` (`IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` и другие), а хост заполняет данные до запуска. Если ему ничего не передали, генератор обязан ничего не создать

Полный контракт - [Generators/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Generators/README.md)
