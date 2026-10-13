---
title: Como contribuir com o SDK
date: 2026-10-02
tags: [developer]
---

# Como contribuir com o SDK

Relate problemas do SDK nas issues do repositório bullet-hero/sdk e envie mudanças de código para lá como pull requests. As regras para contribuidores ficam no mesmo repositório, ao lado do código

O repositório é [bullet-hero/sdk](https://github.com/bullet-hero/sdk), o branch padrão é `master`

## Onde relatar

| Sobre o quê | Onde |
|---|---|
| o SDK e o código dele | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| o jogo: bugs e pedidos dos jogadores | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| o texto da documentação | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## Onde estão as regras

As regras para contribuidores ficam no próprio repositório do SDK, ao lado do código que descrevem:

| Arquivo | O que há nele |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | dependências, pacotes de níveis, compilação da DLL e do pacote, o exemplo de verificação |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | o modelo mental, um índice de pastas e as convenções da biblioteca inteira |
| `CLAUDE.md` em cada pasta | as regras locais daquela pasta, por exemplo [Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | eixos de versão, gerações, migração e recusa |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | como o modelo endereça as entidades: Guid, int, quadro, caminho de campo |
| [[ugc-licensing-policy]] (neste site) | a política de licenciamento do conteúdo de usuários, editada junto com `TrustedSourceCatalog` |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | como escrever um snapshot e um migrador |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | o contrato dos geradores |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | os analisadores e o gerador de modelos, como recompilá-los |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | o contrato de compilação dupla |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | mudanças por versão `sv`, as mais novas no topo |

## Compilação e testes

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- aqui as mesmas fontes que a Unity compila são compiladas sem a Unity. Um arquivo que quebra o contrato de independência do motor quebra esta compilação
- a saída vai para `bin~` e `obj~`
- o comando pack só cria um `.nupkg`. A publicação no nuget.org é feita pelo workflow `release` do repositório quando uma tag `sv` é enviada

> [!caution] Cuidado
> Os analisadores e o gerador de modelos são distribuídos como um `BH.SDK.Roslyn.dll` pré-compilado na raiz do SDK. Depois de editar qualquer coisa em `Roslyn/`, recompile-o e copie-o por cima. Senão o gerador antigo continua rodando, mesmo que as fontes digam outra coisa

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Dentro do editor da Unity, o item de menu **Tools > BH.SDK.Roslyn > Build Analyzer** faz o mesmo

## Invariantes que vale a pena conhecer de antemão

- o núcleo não referencia nenhum tipo de `UnityEngine`. Código que precisa do motor vai para `UnityExtensions/` ou para `UnityIntegration/` atrás de `#if BHSDK_UNITY`, com um ramo sem motor
- o código funciona igual com arquivos e com dados em memória e usa só a assincronia da BCL
- `netstandard2.1` e C# 9 são o que o projeto da Unity usa para compilar. Eles não são aumentados
- um modelo é uma `[GenerateModel] public sealed partial class`. Cada campo serializado pega a chave de `Names.cs`
- qualquer mudança de modelo é uma nova geração com um snapshot e um migrador. Mais - [[5_versioning]]
- a versão do SDK fica em três lugares: `SdkVersion.cs`, `package.json` e `<Version>` em `BH.SDK.csproj`. `SdkVersionAgreementTests` falha se um deles mudou sozinho
