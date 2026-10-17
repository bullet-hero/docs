---
title: Política de privacidade do jogo
date: 2026-10-17
tags: [legal]
---

# Política de privacidade do jogo

O desenvolvedor do Bullet Hero não coleta, não recebe, não vende e não compartilha nenhum dado pessoal. O jogo não tem contas próprias, nem publicidade, nem análise de dados, nem relatórios de falhas, nem rastreamento, nem identificador de publicidade. Tudo o que o jogo lembra sobre você fica no seu próprio dispositivo, exceto o que você permite que uma loja guarde para você na sua própria conta dessa loja

Estas coisas podem sair do seu dispositivo, e nenhuma delas vai para o desenvolvedor:

- um nível que você abre pode fazer referência a um arquivo hospedado em um site de terceiros, e carregá-lo faz contato com esse site ([[game-privacy-policy#Acesso à rede]])
- um nível ou um arquivo de perfil que você compartilha de propósito com outra pessoa vai para onde você o enviar ([[game-privacy-policy#Níveis que você compartilha]])
- nas builds da Steam, o jogo se comunica com a Oficina Steam por meio do cliente da Steam ([[game-privacy-policy#Oficina Steam]])
- nas builds da Steam, o jogo guarda uma cópia dos seus salvamentos no Steam Cloud e informa as suas conquistas à Steam ([[game-privacy-policy#Steam Cloud e conquistas]])
- nas builds da Steam, o jogo mostra a sua atividade atual no Discord por meio do cliente do Discord ([[game-privacy-policy#Discord Rich Presence]])
- na build do Google Play, o jogo informa as suas conquistas ao Google Play Games e pergunta ao Google Play sobre atualizações e avaliações ([[game-privacy-policy#Google Play]])
- na build da RuStore, o jogo pergunta ao aplicativo da RuStore sobre atualizações e avaliações ([[game-privacy-policy#RuStore]])
- em um computador, um programa de IA que você conecta ao editor de níveis vê o nível que você tem aberto ([[game-privacy-policy#Assistente de IA no editor]])

| | |
|---|---|
| Data de vigência | 17 de outubro de 2026 |
| Versão da política | 1.4 |
| Aplicativo | Bullet Hero: `com.vertoker.BulletHero` no Android, `com.vertoker.Bullet-Hero` no iOS, e as builds para computador de Windows, Linux e macOS |
| Desenvolvedor | vertoker, desenvolvedor individual |
| Contato | [kostyachurakov@gmail.com](mailto:kostyachurakov@gmail.com) |

Esta política abrange apenas o jogo. O site tem a própria política - [[privacy-policy]]. O servidor também terá a própria política, escrita quando o servidor existir

## A quem esta política se aplica

Esta política abrange todas as builds do Bullet Hero, em todas as plataformas e em todas as lojas pelas quais ele é distribuído, e todas as versões do jogo às quais nenhuma política mais recente esteja vinculada

Quando uma loja (Google Play, App Store, Steam, RuStore, VK Play ou qualquer outra) coleta dados próprios sobre a sua compra, instalação ou uso do aplicativo, essa coleta é regida pela política de privacidade da própria loja, e não por esta. O desenvolvedor recebe dessas lojas apenas o que elas escolhem mostrar a todo desenvolvedor: estatísticas agregadas e anônimas sobre instalações, falhas e conquistas que não podem ser associadas a um jogador individual

## O que é armazenado no seu dispositivo

O jogo grava o seguinte no próprio armazenamento do aplicativo e lê isso de volta na próxima inicialização:

- **Configurações**: gráficos, áudio, controles, atribuição de teclas, interface e preferências de idioma
- **Progresso e estatísticas**: tentativas, melhores resultados, mortes, tempo de jogo e registros semelhantes, tanto do dispositivo como um todo quanto de cada nível
- **Conquistas**: quais conquistas você desbloqueou e quando
- **Níveis**: os níveis que você cria, importa ou baixa, incluindo o áudio, as imagens e outras mídias deles, além dos backups automáticos deles e, se você usa o assistente de IA, as anotações dele na pasta `ai` do nível
- **Skins do avatar**: as skins que você cria ou importa, e qual delas você está usando
- **Perfil de desempenho do dispositivo**: se você roda o teste de estresse, as medições dele junto com o modelo do dispositivo, o nome do chip gráfico e o tamanho da tela. Ele é usado apenas para avaliar o quanto um nível pesa neste dispositivo e nunca sai do dispositivo: nem a transferência de perfil nem o Steam Cloud o levam
- **Estado local**: as configurações do assistente de IA do editor, o estado da última sincronização com o Steam Cloud e, no Android, a última vez em que o jogo pediu uma avaliação
- **Logs de diagnóstico**: o próprio arquivo de log do motor, gravado localmente para que um problema possa ser investigado no dispositivo onde aconteceu

Nada disso é enviado ao desenvolvedor, e nada disso é copiado para nenhum serviço operado pelo desenvolvedor. Só o Steam Cloud, nas builds da Steam, guarda uma cópia na sua conta Steam ([[game-privacy-policy#Steam Cloud e conquistas]]). Onde isso fica depende da plataforma:

- **Android e iOS**: o armazenamento privado do jogo. Outros aplicativos não podem lê-lo, e ele é excluído junto com o jogo quando você o desinstala
- **Windows, Linux e macOS**: a pasta de dados de aplicativos no seu perfil de usuário, o local padrão do motor. Outros programas executados na sua conta podem lê-la, como podem ler qualquer um dos seus arquivos, e ela continua lá depois que o jogo é desinstalado, até que você exclua essa pasta. O desinstalador que vem com as builds gratuitas (`unins000`) exclui apenas os arquivos do próprio jogo e não mexe nessa pasta

O jogo também oferece, em `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}`, controles explícitos para excluir as estatísticas e os backups armazenados sem desinstalar o jogo

O jogo não pede acesso aos seus contatos, fotos, câmera, microfone, localização, agenda, registro de chamadas, lista de aplicativos instalados nem a nenhum outro recurso sensível, e não pede nenhuma permissão em tempo de execução

## Acesso à rede

Bullet Hero não tem servidor. O desenvolvedor não opera nenhum serviço ao qual o jogo se conecte e, portanto, não recebe nenhum dado dele

Um nível é uma pasta de arquivos, e o autor dele pode apontar um desses arquivos para um endereço da internet em vez de colocá-lo dentro da pasta. Quando você abre um nível assim, o jogo baixa esse arquivo do site que o autor escolheu. Esse site então vê o que qualquer site vê quando um arquivo é pedido a ele, principalmente o seu endereço IP e os detalhes técnicos da requisição. O desenvolvedor não controla nem observa essas requisições, e nenhum registro delas é mantido

Fora isso, o jogo faz requisições de rede apenas por meio da loja ou do aplicativo com que ele veio, e apenas na build dessa loja:

- as builds da Steam: a Oficina Steam, o Steam Cloud e as conquistas da Steam por meio do cliente da Steam, e o Discord Rich Presence por meio do cliente do Discord
- a build do Google Play: as conquistas do Google Play Games, a verificação de atualizações e o pedido de avaliação por meio do Google Play no celular
- a build da RuStore: a verificação de atualizações e o pedido de avaliação por meio do aplicativo da RuStore no celular

Nenhuma outra build faz essas requisições: o código de cada loja é compilado apenas na build dessa loja. O assistente de IA no editor escuta apenas o endereço de loopback do próprio computador e não pode ser alcançado pela rede ([[game-privacy-policy#Assistente de IA no editor]])

## Oficina Steam

As builds da Steam usam a Oficina Steam por meio do cliente da Steam executado no seu computador. As builds para todas as outras lojas nunca iniciam a Steam: o código que se comunica com ela é compilado apenas nas builds da Steam

O jogo pergunta à Steam em quais itens da Oficina a sua conta está inscrita, para poder listá-los como níveis e coleções. O cliente da Steam os baixa. Quando você escolhe publicar um nível ou uma coleção, o jogo o entrega ao cliente da Steam junto com o título, a descrição, a imagem de pré-visualização, os descritores de conteúdo e a visibilidade que você definiu, e a Steam o armazena nos servidores dela, vinculado à sua conta Steam. Um item público pode ser visto por qualquer pessoa na Steam até que você o remova de lá

Tudo isso passa entre o cliente da Steam e os servidores da Valve e é regido pela própria política de privacidade da Steam e pelo Acordo de Assinatura do Steam. O desenvolvedor não recebe nada disso além do que a Steam mostra a todo desenvolvedor sobre um item da Oficina

## Steam Cloud e conquistas

Nas builds da Steam, o jogo guarda uma cópia das suas configurações, estatísticas, conquistas, níveis, biblioteca e skins do avatar no Steam Cloud, vinculada à sua conta Steam. Ele lê essa cópia ao iniciar e grava as mudanças enquanto você joga e quando você sai, por meio do cliente da Steam. As configurações de gráficos e de controles, os backups, os relatórios de erros, as gravações, o perfil de desempenho do dispositivo e o estado local do editor nunca vão para lá. O Steam Cloud pode ser desligado para o jogo nas propriedades dele na Steam, e então o jogo guarda tudo apenas neste computador

Cada conquista que você desbloqueia também é informada à Steam, que a mostra no seu perfil da Steam de acordo com as suas configurações de privacidade da Steam

Os dois ficam nos servidores da Valve e são regidos pela própria política de privacidade da Steam e pelo Acordo de Assinatura do Steam. O desenvolvedor não recebe nada disso além do que a Steam mostra a todo desenvolvedor, como a porcentagem de jogadores que desbloquearam cada conquista

## Discord Rich Presence

As builds da Steam podem mostrar no seu perfil do Discord o que você está fazendo no jogo: o menu, o editor de níveis, o sandbox ou o nível que você está jogando, e por quanto tempo. Um nível é mostrado pelo nome, junto com os autores dele, apenas quando já é público - um item da Oficina Steam ou um nível que vem com o jogo. Qualquer outro nível é mostrado apenas como nível personalizado, e o nível que você está editando nunca é nomeado. Isso só funciona enquanto o aplicativo do Discord está sendo executado no mesmo computador. As builds para todas as outras lojas não têm integração com o Discord: o código que se comunica com o Discord é compilado apenas nas builds da Steam

O jogo entrega essa atividade ao cliente do Discord no seu dispositivo, nunca a um servidor próprio. Em seguida, o cliente do Discord a publica na sua conta do Discord, e os seus amigos e servidores do Discord podem vê-la. O jogo não faz login no Discord, não lê as suas mensagens, servidores ou lista de amigos e não envia nada em seu nome

O que acontece com essa atividade do lado do Discord é regido pela [Política de Privacidade do Discord](https://discord.com/privacy). O desenvolvedor não recebe nada disso. Você pode ocultar a sua atividade a qualquer momento no Discord: `User Settings` -> `Activity Privacy`

## Google Play

A build do Google Play usa três serviços do Google Play no seu celular:

- **Google Play Games**: se você entrou na sua conta do Google Play Games, cada conquista que você desbloqueia também é informada lá, na sua conta Google, e aparece no seu perfil do Play Games. O jogo apenas pergunta ao Play Games se você entrou na conta e quais conquistas já estão desbloqueadas. Ele não lê o seu nome, os seus amigos nem nada mais da sua conta. A entrada na conta é feita pelo próprio Google Play Games, e sem ela as conquistas ficam só no jogo
- **Atualizações**: quando o menu principal abre, o jogo pergunta ao Google Play se há uma versão mais nova, e o Google Play a baixa em segundo plano
- **Avaliação**: depois de um nível concluído, a partir do terceiro e no máximo uma vez a cada 60 dias, o jogo pede ao Google Play que mostre a janela de avaliação dele. Se a janela aparece, e o que você escreve nela, depende do Google Play: o jogo nunca vê a sua nota nem o seu comentário

O que o Google faz com esses dados é regido pela [Política de Privacidade do Google](https://policies.google.com/privacy). O desenvolvedor não recebe nada disso além do que o Google Play mostra a todo desenvolvedor, como os comentários publicados e a porcentagem de jogadores que desbloquearam cada conquista

## RuStore

A build da RuStore usa o aplicativo da RuStore no seu celular para duas coisas, e apenas enquanto esse aplicativo está instalado:

- **Atualizações**: quando o menu principal abre, o jogo pergunta à RuStore se há uma versão mais nova, e a RuStore a baixa em segundo plano
- **Avaliação**: depois de um nível concluído, a partir do terceiro e no máximo uma vez a cada 60 dias, o jogo pede à RuStore que mostre a janela de avaliação dela. Se a janela aparece, e o que você escreve nela, depende da RuStore: o jogo nunca vê a sua nota nem o seu comentário

O que a RuStore faz com esses dados é regido pelos próprios documentos da RuStore. O desenvolvedor não recebe nada disso além do que a RuStore mostra a todo desenvolvedor

## Assistente de IA no editor

No Windows, Linux e macOS, o editor de níveis pode deixar um programa de assistente de IA editar o nível aberto. Isso fica desligado até você ligar `{{ui:settings_game-editor_mcp-enabled}}` em `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor_mcp_title}}`. Enquanto está ligado, o jogo escuta apenas o endereço de loopback do próprio computador, aceita um programa por vez e só o deixa entrar com um token aleatório gravado em um arquivo no armazenamento do jogo. Nada fora deste computador consegue se conectar

O programa que você conecta é escolha sua e não faz parte do jogo. Ele pode ler o nível aberto, os recursos e a música dele, e imagens da área de jogo, e pode enviá-los a quem executa o modelo de IA dele. O que acontece com eles lá é regido pelos termos e pela política de privacidade do próprio programa. O desenvolvedor não recebe nada disso

## Níveis que você compartilha

Os níveis são portáteis por design: um nível pode ser exportado como um arquivo compactado comum e enviado a outra pessoa pelo meio que você escolher. Esse arquivo vai diretamente de você para o destinatário, ou pelo serviço que você usar para enviá-lo. Ele não passa pelo desenvolvedor, e o desenvolvedor não guarda nenhuma cópia dele

O mesmo vale para os outros arquivos que o jogo pode gravar para você levar: um arquivo de perfil feito com `{{ui:settings_profile-transfer_title}}`, que contém os seus níveis, estatísticas, configurações, biblioteca e skins do avatar, e uma skin do avatar exportada sozinha

Um nível que você cria pode conter a sua própria música, imagens e texto e, se você os colocar lá, o seu nome ou apelido. Tudo o que você coloca dentro de um nível fica visível para todos a quem você dá esse nível. Decidir o que incluir cabe apenas a você. Se você usa o assistente de IA, as anotações que ele guarda na pasta `ai` do nível vão junto com as exportações do nível e os envios para a Oficina, a menos que `{{ui:settings_level-settings_metadata-level-ai-share}}` seja desmarcado, e uma exportação protegida por senha nunca as leva

Um nível pode, opcionalmente, ser protegido por uma frase-senha. Essa frase-senha é usada para criptografar o conteúdo do nível no seu dispositivo e nunca é gravada em disco, nunca é registrada em log e nunca é transmitida. Se você a perder, nem o desenvolvedor nem ninguém mais pode recuperar o conteúdo do nível

## Crianças

O jogo não coleta dados pessoais de ninguém, e isso inclui crianças. Ele não contém publicidade, nem compras no aplicativo, nem chat, nem nenhum outro recurso de comunicação, nem nenhum mecanismo pelo qual uma criança possa revelar informações pessoais ao desenvolvedor ou a outro jogador por meio do próprio jogo

Como os níveis podem ser compartilhados como arquivos e podem conter texto, imagens e áudio arbitrários escolhidos pelo autor, os pais e responsáveis continuam responsáveis pelos níveis que uma criança obtém de outras pessoas

## Componentes de terceiros

O jogo é feito com o motor Unity. **Os serviços de coleta de dados da própria Unity (Unity Analytics, Unity Ads, Unity In-App Purchasing, Unity Cloud Diagnostics, o diagnóstico do motor, as estatísticas de hardware, os relatórios de falhas e os relatórios de desempenho) estão todos desativados neste projeto**, e os pacotes que os fornecem não são incluídos na build. Não há nenhum SDK de publicidade, análise de dados, atribuição ou relatório de falhas de qualquer tipo

A build de uma loja traz a biblioteca própria dessa loja, e nenhuma outra build a traz: Steamworks (por meio do Facepunch.Steamworks) e o Discord Social SDK nas builds da Steam, o Google Play Games Services e as bibliotecas de avaliação e de atualização no aplicativo do Google Play na build do Google Play, o SDK de avaliação e de atualização da RuStore na build da RuStore. Cada uma delas se comunica apenas com o próprio serviço, como descrito acima

## Seus direitos

Normas como o GDPR, o UK GDPR, a CCPA/CPRA e a Lei Federal russa nº 152-FZ concedem a você direitos de acesso, correção, exclusão e oposição ao tratamento dos seus dados pessoais

Como o desenvolvedor não tem absolutamente nenhum dado pessoal sobre você, não há nada a acessar, corrigir, exportar ou excluir do lado do desenvolvedor, e nenhum pedido é necessário para exercer esses direitos. Os dados descritos em [[game-privacy-policy#O que é armazenado no seu dispositivo]] estão sob o seu próprio controle: eles podem ser examinados na pasta de armazenamento do jogo no seu dispositivo, apagados de dentro do jogo ou removidos por completo ao desinstalar o aplicativo. Uma cópia que uma loja guarda na sua conta (o Steam Cloud, as conquistas na Steam ou no Google Play Games) fica com essa loja, e esses direitos sobre ela são exercidos junto a essa loja, segundo a política dela. Você ainda pode escrever para o endereço de contato acima com qualquer pergunta sobre esta política

## Retenção de dados

O desenvolvedor não retém dados pessoais e, portanto, não tem nenhum prazo de retenção a declarar. Os dados armazenados no seu dispositivo são mantidos pelo tempo que você os mantiver lá. Uma cópia que uma loja guarda na sua conta é mantida por essa loja segundo a política dela

## Alterações nesta política

Esta política vai mudar se o jogo mudar, muito provavelmente quando forem adicionados o servidor próprio do jogo, as contas de jogador ou o multiplayer, e nada disso existe hoje. Quando ela mudar, a data de vigência e a versão da política no topo desta página são atualizadas, e o texto anterior continua disponível no histórico público de versões desta página. Continuar usando o jogo depois de uma alteração significa que a política atualizada se aplica a esse uso

## Contato

Perguntas sobre esta política, ou sobre privacidade no Bullet Hero em geral, vão para o endereço de contato no topo desta página
