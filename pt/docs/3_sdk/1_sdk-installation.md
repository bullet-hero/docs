---
title: Instalação
date: 2026-10-02
tags: [developer, level_author]
---

# Instalação

O SDK é o pacote BulletHero.SDK no nuget.org ou uma compilação a partir do código-fonte. A Unity o recebe como git submodule, e o exemplo ConsoleSmoke verifica se os seus níveis são lidos

O código do SDK está em [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk). A licença é MIT

## .NET

O pacote `BulletHero.SDK` está publicado no nuget.org: `dotnet add package BulletHero.SDK`. As três dependências chegam junto com ele. Para compilá-lo a partir do código-fonte:

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

Depois conecte uma das duas opções:
- o `.nupkg` a partir de uma pasta local: `dotnet add package BulletHero.SDK --source <folder>`. As três dependências chegam junto com ele
- `BH.SDK.dll` diretamente. Nesse caso, adicione você mesmo os três pacotes abaixo: uma referência a uma DLL não traz as dependências dela

Dependências, todas do NuGet:

| Pacote | Versão | Para quê |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP para níveis protegidos por senha |
| `SharpZipLib` | 1.4.2 | tar e zip (o gzip vem da BCL) |

### Detalhes da compilação

- o assembly é `BH.SDK.dll`, e a documentação XML dele fica ao lado
- o alvo é `netstandard2.1`, a linguagem é C# 9. São os mesmos números do projeto da Unity, por isso as mesmas fontes compilam tanto dentro da Unity quanto sem ela
- as pastas de saída são `bin~` e `obj~`. O til é necessário porque a Unity não importa pastas cujo nome termina com ele

## Unity

O jogo conecta o SDK como git submodule:

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

Para remover: `git rm -r -f Assets/Plugins/BH.SDK`

O que o projeto da Unity precisa fornecer por conta própria:
- `Newtonsoft.Json` pelo pacote `com.unity.nuget.newtonsoft-json`
- `BouncyCastle.Cryptography` e `SharpZipLib` do NuGet (o jogo os instala com o NuGetForUnity)
- o scripting define `BHSDK_UNITY` em Player Settings. Sem ele, `UnityIntegration` segue o ramo sem motor
- `BH.SDK.Roslyn.dll` na raiz do SDK. A Unity aplica um analisador só ao assembly da pasta dele e aos assemblies que o referenciam. Movido para outro lugar, ele não analisa nada

A raiz do repositório contém um `package.json` com o nome `com.vertoker.bullet-hero-sdk` e a versão mínima da Unity `6000.0`. Por isso o Package Manager também consegue adicionar o SDK por URL do git. Esse caminho não é usado e não é descrito aqui

## Verificação: o exemplo ConsoleSmoke

`Samples~/ConsoleSmoke` é um aplicativo de console `net8.0`. Ele referencia o `BH.SDK.dll` compilado, exatamente como uma ferramenta de terceiros faria. O aplicativo lê uma pasta de nível e imprime o nome, a quantidade de objetos e a geração. Depois faz a ida e volta do nível por JSON e por `.blob`

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| Código de saída | Significado |
|---|---|
| 0 | tudo coincidiu |
| 1 | argumentos errados |
| 2 | `level.*` ou `metadata.*` não encontrado |
| 3 | uma ida e volta não coincidiu |
| 4 | o arquivo é mais novo do que este SDK |

A saída com o nível integrado do jogo `new-zero-demo` (gravada com `sv 1.0.0`):

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

Próximo - [[2_level-format]]

## Do que o SDK é feito

| Parte | O que é | Precisa da Unity |
|---|---|---|
| `BH.SDK` | o núcleo: modelos, serialização, versões, regras, validação, arquivos compactados, publicação, geradores | não |
| `UnityIntegration` | uma camada fina em que cada arquivo compila tanto com a Unity quanto sem ela (`#if BHSDK_UNITY`), por exemplo o logger `Cat` | não: fora da Unity ele é compilado direto no núcleo |
| `UnityExtensions` | conversões para tipos da Unity, transformações 2D, movimento do avatar | sim, sempre |
| `BH.SDK.Roslyn` | analisadores e um gerador de código-fonte. Para cada modelo com `[GenerateModel]` ele escreve `Equals`, a cópia, os codecs de JSON e de `.blob` e o percurso de validação | roda na compilação |

Um arquivo de modelo contém só os campos e os construtores dele. Tudo o que é repetitivo é escrito pelo gerador. Assim, não dá para esquecer um campo em um dos sete corpos gerados

## Por que uma biblioteca separada

- **Os níveis sobrevivem ao jogo.** Um nível é uma pasta de arquivos em formatos abertos (JSON, tar.gz, zip, OpenPGP). O código que os lê também é aberto. Um nível continua legível mesmo quando o jogo que o gravou já não existe
- **Interoperabilidade com outros jogos de ritmo.** O formato é descrito abertamente, então um conversor para outro jogo ou de outro jogo pode ser escrito com base nele
- **Correções rápidas.** Um defeito no formato é visível de fora. Qualquer pessoa que leia o código pode relatá-lo ou enviar uma correção
- **Ferramentas de terceiros.** Um conversor, um validador, um gerador de níveis ou um mod trabalha com os mesmos modelos que o jogo. Não é preciso reconstruí-los a partir dos arquivos
- **Servidores.** O núcleo compila sem a Unity como `netstandard2.1`. Assim, um servidor executa as mesmas verificações sobre os mesmos modelos que o cliente
