---
title: Assistente de IA
date: 2026-10-13
tags: [level_author]
---

# Assistente de IA

Um cliente de IA compatível com MCP pode editar o nível aberto no editor enquanto você assiste. Cada lote da IA é um passo de desfazer, e a IA não pode publicar, excluir arquivos nem gravar sobre outro nível

O jogo no Windows, no Linux e no Mac traz um servidor MCP para isso. A IA edita pelas mesmas operações que você, então cada mudança aparece no viewport na hora e entra no histórico como se fosse sua

Qualquer cliente compatível com MCP funciona, como um aplicativo de chat ou um assistente de programação. Nada no jogo está preso a uma IA específica

## Conectando um cliente

1. Abra `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`
2. Marque `{{ui:settings_game-editor_mcp-enabled}}`. A linha de status abaixo das configurações mostra a porta em que o editor escuta
3. Pressione `{{ui:settings_game-editor_mcp-copy-config}}`. A área de transferência agora tem a configuração do cliente com os dois caminhos preenchidos
4. Cole-a nas configurações de servidores MCP do seu cliente
5. Abra um nível no editor, ou peça à IA que abra o editor ou um nível ela mesma

A configuração copiada tem esta cara:

```json
{ "mcpServers": { "bullet-hero": { "command": "<path to BH.MCP>", "args": ["--endpoint", "<path to endpoint.json>"] } } }
```

O arquivo do servidor `BH.MCP` fica ao lado do jogo:

| Sistema | Arquivo do servidor |
|---|---|
| Windows | `<pasta do jogo>/BH.MCP.exe` |
| Linux | `<pasta do jogo>/BH.MCP` |
| Mac | `<game>.app/Contents/Resources/mcp/osx-arm64/BH.MCP`, no Intel `osx-x64` em vez de `osx-arm64` |

Só este computador pode se conectar, e só um cliente por vez.
Celulares e tablets não têm a seção MCP: o assistente é só para computador

Várias cópias do jogo podem rodar ao mesmo tempo. A IA trabalha na última que foi iniciada até você pedir para trocar, e consegue listar todas. Cada cópia continua aceitando um único cliente. Para várias cópias, mantenha `{{ui:settings_game-editor_mcp-port}}` em `0`, já que duas cópias não podem escutar na mesma porta

## O que a IA pode e não pode fazer

A IA pode fazer quase tudo o que você pode:
- ler o nível: a hierarquia, os objetos, os quadros-chave, os eventos e os recursos
- criar, mudar e excluir objetos, quadros-chave, marcadores, checkpoints, faixas de áudio e a grade de batidas
- rodar geradores, empacotar e posicionar prefabs, trabalhar dentro do modo prefab
- importar para o nível um arquivo de textura, fonte ou áudio
- preencher o registro de atribuição de um arquivo de textura, fonte ou áudio depois de importá-lo: título, descrição, link, fontes de origem e autores - [[4_resource-record]]
- usar os temas, as fontes e os sons de interface predefinidos do próprio jogo. `resources_list` os marca como do jogo, e eles não precisam ser importados. O jogo não traz efeitos predefinidos: um efeito que a IA coloca é um que o nível já tem ou um novo que ela cria
- desenhar qualquer contorno como forma do nível a partir dos cantos dele, colorir uma forma com um gradiente, definir a fonte e o alinhamento de um texto, criar e editar os temas do nível
- desfazer e refazer, salvar o nível aberto, abrir outro nível, criar um novo
- iniciar e pausar a reprodução, como o seu botão de reproduzir
- levar o jogo para outra tela, como o editor, um nível ou as configurações, com os mesmos argumentos que uma inicialização aceita - [[12_launch-arguments]]
- iniciar o jogo quando ele não está rodando, se o servidor fica ao lado do jogo instalado e o MCP já está ligado

Uma partida iniciada assim conta nas suas estatísticas como qualquer outra, então a IA só inicia uma quando você pede

Ela não pode:
- publicar na Oficina Steam
- excluir um nível ou qualquer arquivo
- gravar sobre outro nível ou outro arquivo. Uma importação cujo nome de arquivo já está em uso é recusada
- abrir um nível somente leitura, nem um nível protegido cuja senha você não digitou nesta sessão
- abrir outro nível enquanto o aberto tem mudanças não salvas

**Um lote da IA é um passo no histórico.** Ele aparece na aba `{{ui:settings_level-settings_history}}` como `{{ui:op_group_ai-batch}}`, com a legenda que a própria IA deu. Um `Ctrl+Z` remove o lote inteiro. Mais sobre o histórico - [[10_level-settings#Histórico]]

**A IA nunca põe dois objetos na mesma camada enquanto os dois estão em reprodução.** Se um lote fizesse isso, ela sobe o objeto posterior para a próxima camada livre no mesmo passo e avisa. O conteúdo de prefab é a exceção: ele pode dividir camadas com o resto do nível

O primeiro lote da IA que muda um nível define o `{{ui:settings_level-settings_metadata-level-ai-generated}}` dele como `{{ui:enum_ai-generation_yes}}`, dentro do mesmo passo. Desfazer o lote reverte isso. Mais - [[2_metadata-and-sharing#Geração por IA]]

## Você tem prioridade

A IA nunca disputa o editor com você:
- enquanto você arrasta uma alça do gizmo ou arrasta pela linha do tempo, as edições da IA são recusadas, e ela espera e tenta de novo
- a IA só pega o indicador de reprodução enquanto você não está fazendo nada: sem reproduzir, sem arrastar, sem digitar, sem salvar
- o editor começa a reproduzir um nível assim que ele abre, então a IA pode pausá-lo para olhar quadros. Um nível que a IA abre ou cria ela mesma fica pausado. Se você está assistindo à reprodução de propósito, a IA pergunta antes de pausar
- se você mexe no editor enquanto a IA está olhando um quadro, a IA para na hora. O indicador de reprodução fica onde você o colocou
- enquanto um percurso pelo histórico está rodando, a IA também não pode editar

Enquanto um cliente está conectado, o viewport mostra `AI` no canto superior direito, abaixo dos botões de pesquisa. A cor dele é o estado: verde - conectado, âmbar - a IA está trabalhando, vermelho - a última chamada da IA terminou em erro.
Depois que o cliente se desconecta, o selo continua por {{v:mcp.badge-hold-seconds}} segundos, para que uma IA que se reconecta a cada passo não fique piscando. Ele se oculta junto com as ferramentas do viewport.
Passe o mouse sobre ele para ler o estado em palavras: `{{ui:editor_agent-badge_connected}}` e, enquanto a IA trabalha, a legenda do que ela está fazendo.
O X ao lado desconecta o cliente e o recusa, e o selo some

Uma parada não é salva. Desligar e ligar de novo `{{ui:settings_game-editor_mcp-enabled}}` ou reiniciar o jogo a desfaz

## O que a IA vê

A IA olha o nível de duas formas:
- **um esquema.** Uma imagem de qualquer quadro, calculada fora da tela. Não move o indicador de reprodução. Mostra formas e hitboxes, mas nem textos nem efeitos
- **uma captura.** Pixels reais, exatamente como o nível é desenhado, tirados pelo seu indicador de reprodução. Por um momento, o indicador salta para aquele quadro e as sobreposições do editor se ocultam. Depois o indicador volta para onde você o deixou, a menos que `{{ui:settings_game-editor_mcp-follow-ai}}` esteja ligado. A imagem é enquadrada pela câmera do nível, não pela câmera do editor. Para ver um detalhe de perto, a IA pode enquadrar um retângulo do mundo no lugar. O nível não muda

Uma imagem parada de um efeito depois de um salto é próxima do que a reprodução contínua mostra, mas nem sempre é idêntica

A IA não consegue ouvir a música. Ela transforma a música em números: andamento, batidas, compassos, seções, o volume de cada banda.
Isso é uma estimativa com um grau de confiança, e pode errar, por exemplo pela metade ou pelo dobro do andamento. A grade de batidas que você definiu no nível vale mais do que a estimativa da IA.
Uma grade de batidas que a IA propõe a partir da análise arredonda para o número inteiro um andamento que esteja a menos de 0,01 % dele, e o deslocamento dela é sempre menor que um compasso. Uma proposta sobre parte da música usa o andamento próprio dessa parte, então uma música cujo andamento muda recebe um segmento por andamento

Por isso, quando o tempo certo importa, a IA pode pedir que você escute. Ela toca um trecho de até {{v:mcp.max-play-seconds}} segundos no editor, e isso também move o indicador de reprodução. Mexa no editor, e a reprodução para onde estiver

Enquanto o som do editor está mudo, a IA não toca nada e pede que você ligue o som

As ações da própria IA não fazem sons de interface: um desfazer, um salvamento ou uma recusa causados por ela são silenciosos. Só se ouve o que ela toca de propósito

## A pasta ai

A IA mantém a memória dela sobre o nível na pasta `ai`, dentro da pasta do nível. A próxima sessão, com qualquer cliente, lê essa pasta primeiro e continua de onde a última parou

O que fica lá:
- `CONTEXT.md` - o briefing, a música, o plano de seções, as decisões, as suas observações e as perguntas em aberto
- outros arquivos que a IA decidir manter, só `.md` ou `.json`
- `manifest.json` - se a pasta vai junto com o nível. A IA não pode mudá-lo

A pasta só aparece quando a IA tem algo para gravar pela primeira vez. Um arquivo comporta até {{v:mcp.ai-file-max-kb}} KB, a pasta inteira até {{v:mcp.ai-folder-max-mb}} MB. São arquivos de texto comuns: você pode ler, editar ou excluir esses arquivos

> [!warning] Aviso
> A pasta `ai` não faz parte do histórico do nível. `Ctrl+Z` não desfaz o que a IA escreveu lá

**A pasta vai junto com o nível por padrão**: em um arquivo compactado exportado e em um envio para a Oficina Steam. Para mantê-la só com você, desmarque `{{ui:settings_level-settings_metadata-level-ai-share}}` na aba `{{ui:settings_level-settings_metadata}}` das configurações do nível. A caixa de seleção aparece quando a pasta já existe. Ela é salva em um arquivo na hora, então `Ctrl+Z` também não a reverte

Um modo de exportação com senha nunca leva a pasta, independentemente da caixa de seleção. Mais - [[13_export-and-protection#Exportar o nível]]

Uma cópia do nível neste dispositivo leva a pasta junto, já que uma cópia não é um compartilhamento

## Configurações

Todas ficam em `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}` e valem só neste dispositivo:
- `{{ui:settings_game-editor_mcp-enabled}}` - se um cliente pode se conectar. Desligado por padrão
- `{{ui:settings_game-editor_mcp-port}}` - a porta em que o editor escuta. `0` escolhe uma livre a cada inicialização
- `{{ui:settings_game-editor_mcp-follow-ai}}` - ligado: depois de uma captura, o indicador de reprodução fica no quadro que a IA olhou, pausado
- `{{ui:settings_game-editor_mcp-reveal-edits}}` - depois de cada edição da IA, seleciona e localiza o que ela criou ou mudou
- `{{ui:settings_game-editor_mcp-operation-delay}}` - quanto tempo o editor espera entre duas operações da IA, para você conseguir acompanhar. `0` aplica cada uma na hora

Cada configuração e o padrão dela - [[14_editor-settings#Agente de IA]]

A seguir: [[4_not-losing-work]], [[13_export-and-protection]]
