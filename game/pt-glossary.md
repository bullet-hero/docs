# Brazilian Portuguese term base

The terms `pt.yaml` is translated with. `pt` is Brazilian Portuguese: the code carries no region, the text is written
for Brazil. Every value in `pt.yaml` follows this table: a thing is named the same way on every screen, in every hint,
in every tooltip.

- **`strict`** rows are checked by the game's tests: whenever the English value of a key contains the `en` term (a
  whole word, any case, tags ignored, a plural `s`/`es` included), its Portuguese value must contain the `pt` term.
- The check is a plain substring match, accents included, so a `strict` cell is the part every form of the term
  shares: `objeto` covers `objetos`. Where the plural moves a word or an accent (`níveis`, `quadros-chave`, `linhas
  do tempo`), the cell is the shared part and the note gives the full term; where no such part is a word anyone would
  recognise (`coleção`, `coleções`), the row is `loose`.
- **`loose`** rows are guidance: a common word whose best translation depends on the sentence around it. Follow them
  unless the sentence reads wrong, and never use a `loose` row's `pt` for a different concept.
- A row whose `pt` is the same Latin text as `en` means "keep it in Latin" - product names, formats, keys.
- Loanwords follow the Brazilian Unity documentation and the Brazilian rhythm-game communities (osu!, Geometry
  Dash): a Portuguese word where they use one (`camada`, `quadro-chave`, `linha do tempo`), the English word where
  they keep it (`prefab`, `gizmo`, `checkpoint`, `hitbox`).
- Brazil, never Portugal: `você`, a button is an infinitive, sentence case, and Brazilian vocabulary (`arquivo`, never
  `ficheiro`; `tela`, never `ecrã`; `salvar`, never `guardar`; `mouse`, never `rato`).

The canonical meanings are the [glossary](../en/docs/2_editor/7_reference/1_glossary.md). To propose a change, open an
issue or a pull request that edits this table and every `pt.yaml` value that uses the term, in one change.

Punctuation, labels and the rest of the house style for Portuguese: `Assets/Addressables/TEXT-STYLE.md`, section 12,
in the game's repository.

| en | pt | kind | note |
|---|---|---|---|
| Level | nív | strict | Termo completo "nível", plural "níveis": a célula é "nív" porque o plural muda o final e as duas formas só compartilham isso. Tudo o que forma uma partida: objetos, áudio, eventos e recursos próprios. O "level" do som é outra coisa: "volume" ou "nível de sinal" |
| Object | objeto | strict | O que o autor cria na linha do tempo, com intervalo, transformação e pai próprios |
| Rect | objeto vazio | loose | Objeto que não desenha nada: só transformação, intervalo e filhos. Como em ru, duas palavras: o tipo é "objeto vazio", a forma geométrica é "retângulo" |
| Shape | forma | loose | Geometria real que um objeto desenha, não uma imagem. O jogo gera cerca de 500 sozinho |
| Collider | colisor | strict | Aquilo com que um objeto colide. Pode não coincidir com o que ele desenha. Plural "colisores" |
| Prefab | prefab | strict | Modelo reutilizável de objetos que se coloca em um nível quantas vezes for preciso. Em inglês, como na Unity. Plural "prefabs" |
| Prefab Mode | modo prefab | strict | Editar o conteúdo próprio de um modelo em vez do nível ao redor. Nunca "modo de prefab" |
| Effect | efeito | loose | Objeto que a cada quadro cria os próprios objetos a partir de poucos parâmetros. Bloom, Vignette etc. são "efeitos de pós-processamento", nunca "efeito" sozinho |
| Inframe Object | objeto de quadro | loose | Objeto criado por um efeito. O motor cuida dele: não pode ser selecionado nem editado |
| Theme | tema | strict | Paleta a que o nível se refere por índice: recolorir é uma mudança, não cem. Uma música nunca é "tema" aqui, é "música" |
| Frame | quadro | strict | Unidade de tempo do nível. O quadro é uma célula e o tempo é o limite entre duas células. Como em "taxa de quadros" e "quadro-chave". Nunca "fotograma" nem "frame" |
| Keyframe | chave | strict | Termo completo "quadro-chave", plural "quadros-chave": a célula é "chave" porque as duas formas a compartilham e porque distingue Keyframe de Frame. Valor fixado pelo autor em um quadro, entre dois o valor é interpolado |
| Key | quadro-chave | loose | Abreviação de keyframe: "quadro-chave". A tecla do teclado é "tecla", a chave de localização é "chave" |
| Track | faixa | strict | Linha de quadros-chave de uma propriedade animável: posição, rotação, volume. Audio Track é "faixa de áudio". Plural "faixas" |
| Timeline | do tempo | strict | Termo completo "linha do tempo", plural "linhas do tempo": a célula é "do tempo" porque as duas formas a compartilham. Eixo de quadros sobre o qual o nível é editado, uma aba por tipo de conteúdo |
| Span | intervalo | loose | Quando um objeto existe: quadro inicial e duração, não quadro final. O verbo span ("abranger") não se traduz como "intervalo" |
| Playhead | indicador | strict | O quadro mostrado agora. Forma longa "indicador de reprodução" onde couber. Plural "indicadores". Não é Cursor ("cursor"), e outro "indicator" do inglês vira "sinal" |
| Ease | suaviza | strict | Termo completo "suavização", verbo "suavizar": a célula é a raiz "suaviza", que os dois compartilham. Como o valor passa do quadro-chave anterior para este. Não é Curve ("curva") nem o antialiasing |
| Marker | marcador | strict | Ponto com nome na régua do nível, para voltar ao lugar exato. Plural "marcadores" |
| Checkpoint | checkpoint | strict | Para onde uma morte leva o jogador de volta. Em inglês, como na comunidade de Geometry Dash e como em ru, que também usa o empréstimo. Plural "checkpoints" |
| Anchor | âncora | strict | Borda que segue a borda do pai: se o pai encolhe, o filho se move junto. Plural "âncoras". "ancorar" e "ancorado" não contêm "âncora", por isso onde o inglês tem anchor vai o substantivo |
| Layer | camada | strict | Ordem de desenho relativa ao pai: a camada do filho se soma à do pai |
| Pivot | pivô | loose | Ponto em torno do qual o objeto gira e escala, dentro do próprio retângulo |
| Gizmo | gizmo | strict | Alças de arrasto desenhadas sobre o objeto selecionado no viewport. Em inglês, como na Unity |
| Snapping | encaixe | strict | Atrair um arrasto para algo: para o conteúdo com o ímã, para a música com o botão de batida. Por isso Fit é "ajustar", nunca "encaixar", e Settings é "configurações" |
| Snap | encaix | strict | Igual a Snapping. A célula é a raiz "encaix", que "encaixe" e "encaixar" compartilham. Fit é "ajustar", nunca "encaixar" |
| Beat | batida | strict | A grade própria da música: o autor a define e nada a lê durante o jogo. Plural "batidas", como em "batidas por minuto". Não "tempo", que colide com a linha do tempo e com o tempo do nível. Hits nunca são "batidas" |
| Beat Segment | segmento | strict | Termo completo "segmento de batida". Trecho de andamento constante com andamento, fase e comprimento de compasso próprios. Não "intervalo", que é Span |
| BPM | BPM | strict | Batidas por minuto. Em latim, como nas comunidades de jogos de ritmo |
| Tap | toque | loose | Um toque ao marcar o andamento. Na tela sensível ao toque também "toque" |
| Generator | gerador | strict | Automação da criação: produz conteúdo do nível a partir de poucos parâmetros. Plural "geradores" |
| Modifier | modificador | strict | Gerador que edita ou remove o que já existe em vez de adicionar. A tecla do teclado é Modifier Key |
| Seed | semente | strict | O número do qual sai cada valor aleatório do nível: a mesma semente reproduz exatamente o mesmo |
| Raw Data | dados brutos | strict | Todo o modelo salvo como uma árvore editável. Aqui nada é validado, de propósito |
| Recommendation | Recomendação | strict | Um dos cinco rótulos: `<b>Recomendação:</b>`, e a frase que segue começa com minúscula |
| Tip | Dica | strict | Um dos cinco rótulos: `<b>Dica:</b>`, e a frase que segue começa com minúscula |
| Worth knowing | Vale saber | strict | Um dos cinco rótulos: `<b>Vale saber:</b>`, e a frase que segue começa com minúscula |
| Warning | Aviso | strict | Um dos cinco rótulos: `<b>Aviso:</b>`, e a frase que segue começa com minúscula. Os avisos da validação também são "avisos" |
| Caution | Cuidado | strict | Um dos cinco rótulos: `<b>Cuidado:</b>`, e a frase que segue começa com minúscula |
| More | Mais | loose | A última linha de links de uma ajuda, `More:`, é `Mais:` |
| Bullet Hero | Bullet Hero | strict | Nome do produto. Não se traduz |
| Steam | Steam | loose |  |
| JSON | JSON | strict | Nome de formato. Não se traduz |
| MSAA | MSAA | strict | Sigla técnica. Não se traduz |
| FXAA | FXAA | strict | Sigla técnica. Não se traduz |
| HDR | HDR | loose |  |
| VFX | VFX | loose |  |
| URL | URL | loose |  |
| Ctrl | Ctrl | loose | As teclas ficam em latim |
| Shift | Shift | loose | Em latim |
| Enter | Enter | loose | Em latim, não "Entrar" |
| Hierarchy | hierarquia | strict | Painel do editor que lista os objetos pela relação pai-filho. A janela Hierarchy da Unity é "Hierarquia" |
| Inspector | inspetor | strict | Painel do editor com as propriedades do que está selecionado. Grafia brasileira, sem "c". Plural "inspetores" |
| Viewport | viewport | strict | Área do editor que mostra a tela do nível. Em inglês, no masculino ("o viewport"), como dizem os usuários brasileiros da Unity e do Blender. A categoria de comandos View é "Exibir", e Preview é "pré-visualização" |
| Command Palette | paleta de comandos | strict | Janela que procura e executa um comando pelo nome. Como no VS Code em português |
| Command | comando | loose |  |
| Selection | seleção | loose |  |
| Select | selecionar | loose |  |
| Marquee | seleção retangular | strict | Selecionar arrastando um retângulo |
| Apply | aplicar | loose |  |
| Reset | redefinir | loose |  |
| Cancel | cancelar | loose |  |
| Confirm | confirmar | loose |  |
| OK | OK | loose | O botão OK de uma interface brasileira continua "OK" |
| Save | salvar | loose | "salvar", nunca "guardar" |
| Load | carregar | loose |  |
| Open | abrir | loose |  |
| Close | fechar | loose |  |
| Exit | sair | loose |  |
| Create | criar | loose |  |
| Add | adicionar | loose | "adicionar", não "acrescentar": um só verbo no arquivo inteiro |
| Remove | remover | loose | Diferente de Delete ("excluir"): Remove tira algo de uma lista, Delete o apaga |
| Delete | excluir | loose | "excluir", nunca "eliminar" |
| Duplicate | duplicar | loose |  |
| Copy | copiar | loose |  |
| Paste | colar | loose |  |
| Cut | recortar | loose |  |
| Undo | desfazer | loose |  |
| Redo | refazer | loose |  |
| History | histórico | loose | Diferente de Story ("história") |
| Edit | editar | loose | Como categoria de menu também "Editar" |
| Rename | renomear | loose |  |
| Move | mover | loose |  |
| Import | importar | loose |  |
| Export | exportar | loose |  |
| Archive | arquivo compactado | loose | Contêiner portátil de um nível ou de uma coleção. Nunca "arquivo" sozinho, que é File |
| Folder | pasta | loose |  |
| File | arquivo | loose | "arquivo", nunca "ficheiro" |
| Search | pesquisar | loose | Como substantivo, "pesquisa" |
| Filter | filtrar | loose | Como substantivo, "filtro" |
| Refresh | atualizar | loose |  |
| Toggle | alternar | loose | Um interruptor de mostrar e ocultar pode dizer "Mostrar/ocultar" |
| Show | mostrar | loose |  |
| Hide | ocultar | loose |  |
| Hidden | oculto | loose |  |
| Visible | visível | loose |  |
| Enabled | ativado | loose |  |
| Disabled | desativado | loose |  |
| On | ativado | loose | Estado de um interruptor |
| Off | desativado | loose |  |
| None | nenhum | loose | Concorda com o substantivo a que se refere ("nenhuma" para uma forma) |
| Auto | automático | loose |  |
| Custom | personalizado | loose |  |
| Default | padrão | loose |  |
| All | tudo | loose |  |
| Nothing | nada | loose |  |
| Current | atual | loose |  |
| Active | ativo | loose |  |
| Global | global | loose |  |
| Local | local | loose |  |
| Parent | pai | loose |  |
| Child | filho | loose |  |
| Root | raiz | loose |  |
| Fold | recolher | loose |  |
| Unfold | expandir | loose |  |
| Flatten | achatar | loose |  |
| Transform | transformação | loose |  |
| Position | posição | loose |  |
| Rotation | rotação | loose |  |
| Scale | escala | loose |  |
| Size | tamanho | loose |  |
| Offset | deslocamento | loose |  |
| Angle | ângulo | loose |  |
| Radius | raio | loose |  |
| Width | largura | loose |  |
| Height | altura | loose |  |
| Min | mín. | loose |  |
| Max | máx. | loose |  |
| Step | passo | loose |  |
| Random | aleatório | loose |  |
| Rnd | aleat. | loose | Abreviação de "aleatório" em rótulos curtos |
| From | de | loose |  |
| To | até | loose |  |
| Value | valor | loose |  |
| Type | tipo | loose |  |
| Name | nome | loose |  |
| Mode | modo | loose |  |
| Count | quantidade | loose |  |
| Speed | velocidade | loose |  |
| Velocity | velocidade | loose |  |
| Gravity | gravidade | loose |  |
| Particle | partícula | loose |  |
| Orbital | orbital | loose |  |
| Lifetime | tempo de vida | loose |  |
| Color | cor | loose |  |
| Alpha | alfa | loose |  |
| Opacity | opacidade | loose |  |
| Opaque | opaco | loose |  |
| Transparent | transparente | loose |  |
| Gradient | gradiente | loose |  |
| Texture | textura | loose |  |
| Font | fonte | loose |  |
| Text | texto | loose |  |
| Localized Text | texto localizado | loose |  |
| Language | idioma | loose |  |
| Audio | áudio | loose |  |
| Audio Track | faixa de áudio | loose |  |
| Volume | volume | loose |  |
| Music | música | loose |  |
| Sound | som | loose |  |
| Resource | recurso | loose |  |
| Resources | recursos | loose |  |
| Metadata | metadados | loose |  |
| Meta | meta | loose |  |
| License | licença | loose |  |
| Author | autor | loose |  |
| Artist | artista | loose |  |
| Settings | configurações | loose | Nunca "ajustes": "ajustar" é Fit |
| Editor | editor | loose |  |
| Game | jogo | loose |  |
| Player | jogador | loose |  |
| Avatar | avatar | loose |  |
| Dash | dash | loose | Em inglês, como na comunidade de Geometry Dash |
| Hitbox | hitbox | loose |  |
| Damage | dano | loose |  |
| Health | vida | loose | Como nos jogos em português |
| Death | morte | loose |  |
| Camera | câmera | loose |  |
| Zoom | zoom | loose |  |
| Pan | panorâmica | loose | Mover a vista. No áudio, Stereo Pan é "pan estéreo" |
| Shake | tremor | loose |  |
| Grid | grade | loose |  |
| Ruler | régua | loose |  |
| Loop | loop | loose | Em inglês, como nos editores de áudio e vídeo |
| Play | reproduzir | loose | Reproduzir no editor é "reproduzir", jogar o nível é "jogar" |
| Pause | pausar | loose | Como substantivo, "pausa" |
| Stop | parar | loose |  |
| Preview | pré-visualização | loose |  |
| Render | renderização | loose |  |
| Post-processing | pós-processamento | loose |  |
| Post | pós-processamento | loose | Abreviação de post-processing |
| Bloom | bloom | loose |  |
| Vignette | vinheta | loose |  |
| Chromatic Aberration | aberração cromática | loose |  |
| Lens Distortion | distorção de lente | loose |  |
| Film Grain | granulação de filme | loose |  |
| Grain | granulação | loose |  |
| Motion Blur | desfoque de movimento | loose |  |
| Blur | desfoque | loose |  |
| Color Curves | curvas de cor | loose |  |
| Curve | curva | loose | Não é Ease ("suavização") |
| Lift Gamma Gain | Lift/Gamma/Gain | loose | Controles da correção de cor, em inglês |
| Shadows Midtones Highlights | sombras/meios-tons/realces | loose |  |
| White Balance | balanço de branco | loose |  |
| Analog Glitch | glitch analógico | loose |  |
| Digital Glitch | glitch digital | loose |  |
| Glitch | glitch | loose |  |
| Gamma | gama | loose |  |
| Background | fundo | loose |  |
| Framerate | taxa de quadros | loose |  |
| Fixed Framerate | taxa fixa de simulação | loose | Como em ru, dois sentidos: nas configurações é a taxa de atualização da simulação, em outros lugares é "taxa de quadros fixa" |
| Collision | colisão | loose |  |
| Screen Limit | limite da tela | loose |  |
| Cursor | cursor | loose |  |
| Control | controle | loose |  |
| Controls | controles | loose |  |
| Keybinding | atribuição de teclas | loose |  |
| Shortcut | atalho | loose |  |
| Button | botão | loose |  |
| Interface | interface | loose |  |
| Screen | tela | loose | "tela", nunca "ecrã" |
| Window | janela | loose |  |
| Panel | painel | loose |  |
| Tab | aba | loose |  |
| Menu | menu | loose |  |
| Tool | ferramenta | loose |  |
| Library | biblioteca | loose |  |
| Bot | bot | loose |  |
| Tutorial | tutorial | loose |  |
| Sandbox | sandbox | loose |  |
| Hint | ajuda | loose | O texto de ajuda de um campo ou de uma janela. Nunca "dica" (Tip) nem "faixa" (Track) |
| Glossary | glossário | loose |  |
| Validation | validação | loose |  |
| Rules | regras | loose |  |
| Format | formato | loose |  |
| Version | versão | loose |  |
| Desktop | computador | loose |  |
| Mobile | celular | loose | "celular", nunca "telemóvel" |
| Alignment | alinhamento | loose | Diferente de Placement ("posicionamento") |
| Align | alinhar | loose |  |
| Center | centro | loose |  |
| Left | esquerda | loose |  |
| Right | direita | loose |  |
| Top | superior | loose | Concorda com o substantivo: "borda superior" |
| Bottom | inferior | loose | Concorda com o substantivo: "borda inferior" |
| Horizontal | horizontal | loose |  |
| Vertical | vertical | loose |  |
| Linear | linear | loose |  |
| Appearing | aparecimento | loose |  |
| Scissors | tesoura | loose |  |
| Edges | bordas | loose | Como em ru, dois sentidos: a ferramenta que move as bordas de um intervalo é "bordas", as arestas de uma forma são "arestas" |
| Point | ponto | loose |  |
| Continue | continuar | loose |  |
| Next | próximo | loose |  |
| Back | voltar | loose |  |
| Loading | carregando | loose |  |
| Progress | progresso | loose |  |
| Statistics | estatísticas | loose |  |
| Preset | predefinição | loose | Default é "padrão", não "predefinido" |
| Clipboard | área de transferência | loose |  |
| Console | console | loose |  |
| Ping | localizar | loose | Mostrar algo no viewport, na linha do tempo e na hierarquia |
| Override | substituição | loose |  |
| Placement | posicionamento | loose |  |
| Template | modelo | loose |  |
| Clip | clipe | loose |  |
| Slip | deslizar conteúdo | loose | Como em ru: mover o conteúdo dentro do intervalo sem mover o intervalo |
| Slot | slot | loose |  |
| Beat Grid | grade de batidas | loose |  |
| Bar | compasso | loose | Na música. A barra de progresso é "barra" |
| Tempo | andamento | loose | Não "tempo", que em português também é o tempo do nível e da linha do tempo |
| Tap Tempo | andamento por toques | loose |  |
| Stereo Pan | pan estéreo | loose |  |
| Font Size | tamanho da fonte | loose |  |
| Word Wrap | quebra automática de linha | loose |  |
| Backup | backup | loose |  |
| Branch | ramo | loose |  |
| Fit | ajustar | loose | Nunca "encaixar", que é Snap |
| Finding | ocorrência | loose | O que a validação encontra em um nível |
| Fix | corrigir | loose |  |
| Group | grupo | loose |  |
| Id | ID | loose |  |
| Mipmap | mipmap | loose |  |
| Sampling | amostragem | loose |  |
| Tiling | mosaico | loose |  |
| Wrapping | fora das bordas | loose | O que uma textura mostra além das próprias bordas, como em ru |
| Pixel art | pixel art | loose |  |
| Drawing | desenho | loose |  |
| Emission Shape | forma de emissão | loose |  |
| Over Lifetime | ao longo da vida | loose |  |
| Forces | forças | loose |  |
| Scatter | dispersão | loose |  |
| Spread | abertura | loose |  |
| Tangent | tangente | loose |  |
| Clamp | limitar | loose |  |
| Ping Pong | ida e volta | loose |  |
| Temperature | temperatura | loose |  |
| Tint | tonalidade | loose |  |
| Modifier Key | tecla modificadora | loose |  |
| Dead Zone | zona morta | loose |  |
| Sensitivity | sensibilidade | loose |  |
| Stick | analógico | loose |  |
| Shoulder | botão de ombro | loose |  |
| Gamepad | gamepad | loose | Não "controle", que já é Control |
| Touchscreen | tela sensível ao toque | loose |  |
| Motion Sensor | sensor de movimento | loose |  |
| Handedness | mão dominante | loose |  |
| Double Tap | toque duplo | loose |  |
| Workshop | Oficina | loose | Como na Steam em português do Brasil |
| Story | história | loose |  |
| Wave | onda | loose |  |
| Immortal | imortal | loose |  |
| Dodge | esquiva | loose |  |
| Zen | zen | loose |  |
| Clears | conclusões | loose | Quantas vezes um nível foi concluído |
| Hits | impactos | loose |  |
| Profile | perfil | loose |  |
| Frame Hierarchy | hierarquia do quadro | loose | Segue Hierarchy ("hierarquia") e Frame ("quadro"), os dois strict |
| Stop Frame | quadro de parada | loose |  |
| Runtime Seed | semente de execução | loose |  |
| Level Logo | capa do nível | loose | A imagem mostrada na lista de níveis |
| Post-processing effect | efeito de pós-processamento | loose |  |
| Audio effect | efeito de áudio | loose | "efeito" sozinho é só o objeto Effect |
| Chorus | chorus | loose |  |
| Compressor | compressor | loose |  |
| Distortion | distorção | loose |  |
| Echo | eco | loose |  |
| Flange | flanger | loose |  |
| Highpass | passa-altas | loose |  |
| Lowpass | passa-baixas | loose |  |
| Normalize | normalizar | loose |  |
| Param EQ | EQ paramétrico | loose |  |
| Pitch Shifter | alteração de tom | loose |  |
| Reverb | reverberação | loose |  |
| Emitter | emissor | loose |  |
| Variant | variante | loose |  |
| Fader | fader | loose |  |
| Signal level | nível de sinal | loose | O "level" das ajudas de efeitos de áudio. LocalizationGlossaryTests o exclui |
| Swatch | amostra | loose |  |
| Device library | biblioteca compartilhada do dispositivo | loose |  |
| Collection | coleção | loose | Pasta de recursos reutilizáveis: prefabs, temas, formas, efeitos, texturas, fontes, áudio. Nada a ver com as coleções da Steam. É loose porque "coleções" troca o "ão" por "õ" e não contém "coleção". A collection das regras de validação (uma estrutura de dados) não precisa ser "coleção", e LocalizationGlossaryTests exclui essas chaves |
| Anti-aliasing | antialiasing | loose | Em inglês. Nunca "suavização", que é Ease |
| Overlay | sobreposição | loose |  |
| Scrub | arrasto | loose |  |
| Gradient stop | parada de cor | loose |  |
| Link to a docs page | título da página | loose | Um link para a documentação leva o título em português da página vinculada |
| Difficulty | Dificuldade | loose | Níveis de dificuldade: as balas como clima, de algumas gotas ao colapso. Vale a imagem, não a palavra literal |
| Auto (difficulty) | Auto | loose |  |
| Drizzle (difficulty) | Garoa | loose |  |
| Rain (difficulty) | Chuva | loose |  |
| Downpour (difficulty) | Aguaceiro | loose |  |
| Hail (difficulty) | Granizo | loose |  |
| Barrage (difficulty) | Rajada | loose |  |
| Onslaught (difficulty) | Investida | loose |  |
| Deluge (difficulty) | Dilúvio | loose |  |
| Inferno (difficulty) | Inferno | loose |  |
| Singularity (difficulty) | Singularidade | loose |  |
