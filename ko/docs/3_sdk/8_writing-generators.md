---
title: 생성기 작성
date: 2026-10-02
tags: [developer]
---

# 생성기 작성

생성기는 SDK 기본 클래스(BaseLevelGenerator, BaseContentGenerator, BaseModifier) 중 하나를 상속한 클래스 하나입니다. 폼, 예상치, 실행 취소는 호스트가 계약을 보고 스스로 만듭니다

생성기는 몇 가지 파라미터로 레벨 내용을 만듭니다. 제작자가 오브젝트를 하나하나 손으로 배치할 필요가 없습니다

생성기용 인터페이스를 따로 작성하는 사람은 없으며, 목록도 수정하지 않습니다

내장 생성기가 하는 일 - [[8_generators]]

## 세 가지 종류

| 종류 | 만드는 것 | 기본 클래스 | 진입점 |
|---|---|---|---|
| `Level` | 새 `Level` 및 `LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | 활성 범위 안의 새 오브젝트와 리소스 | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | 이미 있는 오브젝트의 편집 | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content, Modifier 두 종류는 진입점이 같습니다. 차이는 의도와 `GeneratorRequirements` 값에 있습니다. 모디파이어는 기본적으로 선택 항목이 필요합니다

오브젝트를 만드는 생성기를 위해 `BaseSpawnGenerator<TParams>` 클래스가 있습니다. 이 클래스가 모든 오브젝트를 만들고, 부모를 지정하고, 시간 위에 배치합니다. 구체 클래스에는 배치 계산만 남습니다

## 레지스트리 없음

`GeneratorRegistry` 클래스는 처음 접근할 때 리플렉션으로 모든 생성기를 찾습니다. `NameKey` 값이 같은 생성기가 두 개 있으면 그 자리에서 실패합니다

검색 대상은 SDK 자체 어셈블리뿐입니다. 그래서 새 생성기는 SDK 저장소에 있어야 하며, 풀 리퀘스트로 들어옵니다. 자세히 - [[9_contributing-sdk]]

## 예제

내장 `RadialGenerator` 생성기와 같은 클래스 위에 만든 오브젝트 한 줄:

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

    // Spawn adds a size key and a color key, AddPosition adds the third
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

`NameKey` 값은 현지화 키 형태입니다. 호스트는 자체 문자열 테이블을 통해 이름을 표시합니다

## 필수 규칙

- **레벨은 `GeneratorContext` 객체를 통해서만 변경합니다** (`Create`, `Edit`, `Delete`, `SetValue` 등). 이 객체가 모든 변경을 `GeneratorChangeLog`에 기록하며, 실행 취소 전체가 여기에 기대고 있습니다. 모델을 직접 변경해도 컴파일은 되지만 실행 취소가 조용히 깨집니다
- **모든 필드는 섹션에 나열하고, 모든 숫자에는 `Range` 범위를 지정합니다.** 리플렉션이 주는 필드 순서는 보장되지 않습니다. 범위가 없는 숫자는 호스트가 값을 제한할 기준이 없습니다. 범위는 테스트로 검사됩니다
- **파라미터는 public 가변 필드와 파라미터 없는 생성자입니다.** 폼은 이 필드에 바인딩되고, 프리셋은 이 필드를 직렬화합니다. 상속받은 필드를 숨기지 마십시오: 모든 것이 필드 이름으로 지정됩니다
- **예상치는 실제 실행과 일치해야 합니다.** 호스트는 실행 전에 예상치를 보여 줍니다. 실행 결과가 `LevelRules.MaxObjects` 한도를 넘게 되면 호스트가 거부합니다
- **무작위 값은 `System.Random` 클래스가 아니라 `context.CreateRandom()` 메서드에서 가져옵니다.** 같은 시드는 어떤 플랫폼에서든 같은 레벨을 만듭니다
- **만든 것의 부모는 `context.Parent` 오브젝트로 지정합니다.** 호스트는 이 방법으로 실행 한 번의 결과 전체를 오브젝트 하나로 모읍니다
- **`context.Game` 또는 `context.Audio` 객체를 다룬다면 `GeneratorRequirements.LevelScope` 값을 선언합니다.** 활성 범위가 프리팹인 동안에는 둘 다 `null` 값입니다
- **파라미터 조합에 따라 제작자가 보고 있는 창 밖의 내용을 삭제하거나 다시 쓴다면 `IsDangerousTyped` 메서드를 재정의합니다.** 그러면 호스트가 확인을 요청합니다

## 외부 데이터

SDK에는 오디오 디코더도, FFT도, 이미지 로더도 없습니다. 이런 데이터가 필요한 생성기는:
1. `GeneratorRequirements.ExternalAnalysis` 값을 선언합니다
2. `External/` 폴더의 인터페이스를 구현합니다: `IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` 등

데이터는 호스트가 실행 전에 채웁니다. 아무것도 받지 못했다면 생성기는 아무것도 만들지 않아야 합니다

전체 계약 - [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
