---
title: Contribuir al SDK
date: 2026-10-02
tags: [developer]
---

# Contribuir al SDK

Informa de los problemas del SDK en los issues del repositorio bullet-hero/sdk, y envía allí mismo los cambios de código como pull requests. Las reglas para contribuir están en el mismo repositorio, junto al código

El repositorio es [bullet-hero/sdk](https://github.com/bullet-hero/sdk), la rama predeterminada es `master`

## Dónde informar

| Sobre qué | Dónde |
|---|---|
| el SDK y su código | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| el juego: errores y peticiones de los jugadores | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| el texto de la documentación | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## Dónde están las reglas

Las reglas para contribuir están en el propio repositorio del SDK, junto al código que describen:

| Archivo | Qué contiene |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | dependencias, paquetes de niveles, compilación de la DLL y del paquete, el ejemplo de comprobación |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | el modelo mental, un índice de carpetas y las convenciones de toda la biblioteca |
| `CLAUDE.md` en cada carpeta | las reglas locales de esa carpeta, por ejemplo [Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | ejes de versión, generaciones, migración y rechazo |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | cómo direcciona el modelo las entidades: Guid, int, fotograma, ruta de campo |
| [[ugc-licensing-policy]] (en este sitio) | la política de licencias del contenido de los usuarios, que se edita junto con `TrustedSourceCatalog` |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | cómo escribir una instantánea y un migrador |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | el contrato de los generadores |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | los analizadores y el generador de modelos, cómo recompilarlos |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | el contrato de doble compilación |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | los cambios por versión `sv`, los más recientes arriba |

## Compilación y pruebas

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- aquí se compilan sin Unity las mismas fuentes que compila Unity. Un archivo que rompe el contrato de independencia del motor rompe esta compilación
- la salida va a `bin~` y `obj~`
- el comando pack solo crea un `.nupkg`. La publicación en nuget.org la hace el workflow `release` del repositorio cuando se sube una etiqueta `sv`

> [!caution] Precaución
> Los analizadores y el generador de modelos se distribuyen como una `BH.SDK.Roslyn.dll` precompilada en la raíz del SDK. Después de editar cualquier cosa en `Roslyn/`, recompílala y cópiala encima. Si no, sigue funcionando el generador antiguo, aunque las fuentes digan otra cosa

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Dentro del editor de Unity, el elemento de menú **Tools > BH.SDK.Roslyn > Build Analyzer** hace lo mismo

## Invariantes que conviene conocer de antemano

- el núcleo no hace referencia a ningún tipo de `UnityEngine`. El código que necesita el motor va a `UnityExtensions/` o a `UnityIntegration/`, detrás de `#if BHSDK_UNITY` y con una rama sin motor
- el código funciona igual con archivos y con datos en memoria y solo usa la asincronía de la BCL
- `netstandard2.1` y C# 9 son con lo que compila el proyecto de Unity. No se suben
- un modelo es una `[GenerateModel] public sealed partial class`. Cada campo serializado toma su clave de `Names.cs`
- cualquier cambio del modelo es una nueva generación con una instantánea y un migrador. Más - [[5_versioning]]
- la versión del SDK vive en tres lugares: `SdkVersion.cs`, `package.json` y `<Version>` en `BH.SDK.csproj`. `SdkVersionAgreementTests` falla si uno de ellos se ha movido por separado
