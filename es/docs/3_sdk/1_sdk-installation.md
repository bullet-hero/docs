---
title: Instalación
date: 2026-10-02
tags: [developer, level_author]
---

# Instalación

El SDK es el paquete BulletHero.SDK de nuget.org o una compilación desde el código fuente. En Unity se conecta como git submodule, y el ejemplo ConsoleSmoke comprueba que tus niveles se leen

El código del SDK está en [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk). La licencia es MIT

## .NET

El paquete `BulletHero.SDK` está publicado en nuget.org: `dotnet add package BulletHero.SDK`. Las tres dependencias llegan con él. Para compilarlo desde el código fuente:

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

Después conecta una de las dos opciones:
- el `.nupkg` desde una carpeta local: `dotnet add package BulletHero.SDK --source <folder>`. Las tres dependencias llegan con él
- `BH.SDK.dll` directamente. En ese caso añade por tu cuenta los tres paquetes de abajo: una referencia a una DLL no trae consigo sus dependencias

Dependencias, todas de NuGet:

| Paquete | Versión | Para qué |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP para los niveles protegidos con contraseña |
| `SharpZipLib` | 1.4.2 | tar y zip (gzip viene de la BCL) |

### Detalles de la compilación

- el ensamblado es `BH.SDK.dll`, y su documentación XML está a su lado
- el destino es `netstandard2.1`, el lenguaje es C# 9. Son los mismos números que los del proyecto de Unity, así que las mismas fuentes compilan tanto dentro de Unity como sin él
- las carpetas de salida son `bin~` y `obj~`. La tilde final hace falta porque Unity no importa las carpetas cuyo nombre termina en tilde

## Unity

El juego conecta el SDK como git submodule:

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

Para quitarlo: `git rm -r -f Assets/Plugins/BH.SDK`

Lo que el proyecto de Unity tiene que aportar por sí mismo:
- `Newtonsoft.Json` a través del paquete `com.unity.nuget.newtonsoft-json`
- `BouncyCastle.Cryptography` y `SharpZipLib` de NuGet (el juego los instala con NuGetForUnity)
- el scripting define `BHSDK_UNITY` en Player Settings. Sin él, `UnityIntegration` toma la rama sin motor
- `BH.SDK.Roslyn.dll` en la raíz del SDK. Unity aplica un analizador solo al ensamblado de su carpeta y a los ensamblados que lo referencian. Si se mueve a otro sitio, no analiza nada

La raíz del repositorio contiene un `package.json` con el nombre `com.vertoker.bullet-hero-sdk` y una versión mínima de Unity `6000.0`. Por eso el Package Manager también puede añadir el SDK por URL de git. Esa vía no se usa y no se describe aquí

## Comprobación: el ejemplo ConsoleSmoke

`Samples~/ConsoleSmoke` es una aplicación de consola `net8.0`. Hace referencia a la `BH.SDK.dll` compilada, igual que lo haría una herramienta de terceros. La aplicación lee una carpeta de nivel e imprime el nombre, la cantidad de objetos y la generación. Después escribe el nivel en JSON y en `.blob`, lo vuelve a leer y compara el resultado

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| Código de salida | Significado |
|---|---|
| 0 | todo coincidió |
| 1 | argumentos incorrectos |
| 2 | no se encontró `level.*` o `metadata.*` |
| 3 | el nivel releído no coincidió |
| 4 | el archivo es más reciente que este SDK |

La salida con el nivel integrado del juego `new-zero-demo` (grabada con `sv 1.0.0`):

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

Siguiente - [[2_level-format]]

## De qué está hecho el SDK

| Parte | Qué es | Necesita Unity |
|---|---|---|
| `BH.SDK` | el núcleo: modelos, serialización, versiones, reglas, validación, archivos comprimidos, publicación, generadores | no |
| `UnityIntegration` | una capa fina en la que cada archivo compila tanto con Unity como sin él (`#if BHSDK_UNITY`), por ejemplo el logger `Cat` | no: fuera de Unity se compila directamente en el núcleo |
| `UnityExtensions` | conversiones a tipos de Unity, transformaciones 2D, movimiento del avatar | sí, siempre |
| `BH.SDK.Roslyn` | analizadores y un generador de código fuente. Para cada modelo con `[GenerateModel]` escribe `Equals`, la copia, los códecs de JSON y `.blob` y el recorrido de validación | se ejecuta al compilar |

Un archivo de modelo contiene solo sus campos y constructores. Todo lo repetitivo lo escribe el generador. Así no se puede olvidar un campo en uno de los siete cuerpos generados

## Por qué una biblioteca aparte

- **Los niveles sobreviven al juego.** Un nivel es una carpeta de archivos en formatos abiertos (JSON, tar.gz, zip, OpenPGP). El código que los lee también es abierto. Un nivel sigue siendo legible aunque el juego que lo escribió ya no exista
- **Interoperabilidad con otros juegos de ritmo.** El formato está descrito abiertamente, así que a partir de él se puede escribir un conversor hacia otro juego o desde otro juego
- **Correcciones rápidas.** Un defecto del formato se ve desde fuera. Cualquiera que lea el código puede informar de él o enviar una corrección
- **Herramientas de terceros.** Un conversor, un validador, un generador de niveles o un mod trabajan con los mismos modelos que el juego. No hace falta reconstruirlos a partir de los archivos
- **Servidores.** El núcleo compila sin Unity como `netstandard2.1`. Así un servidor ejecuta las mismas comprobaciones sobre los mismos modelos que el cliente
