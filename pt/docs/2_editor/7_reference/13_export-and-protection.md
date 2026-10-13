---
title: Exportação e proteção
date: 2026-10-11
tags: [level_author]
---

# Exportação e proteção

Exportar salva o nível fora do jogo como pasta ou arquivo compactado, com todos os arquivos que ele usa. Uma senha criptografa o conteúdo do nível no disco, e uma senha esquecida não tem recuperação

## Exportar o nível

Fica na aba `{{ui:settings_level-settings_publication}}` das configurações do nível: o destino `{{ui:editor_share_archive}}`, o modo em `{{ui:editor_share_format}}` e `{{ui:editor_share_passphrase}}` para um modo protegido. Mais - [[17_publishing]]

Um arquivo compactado leva o nível, os metadados dele e todos os arquivos que ele usa. Uma música que fica fora da pasta do nível também é copiada para dentro. A referência a ela passa a apontar para a cópia no arquivo compactado

A pasta `ai` do nível, onde um assistente de IA guarda as anotações dele sobre o nível, também é empacotada, a menos que `{{ui:settings_level-settings_metadata-level-ai-share}}` esteja desmarcado nos metadados do nível. Um modo com senha nunca a empacota: anotações de design legíveis ao lado de um nível criptografado anulariam a senha. O relatório avisa quando a pasta ficou de fora. Mais - [[7_ai-assistant#A pasta ai]]

| `{{ui:editor_share_format}}` | O que você recebe | Com o que abrir |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_folder}}` | a mesma pasta que o nível tem no disco. Compacte e envie | não precisa de nada |
| `{{ui:settings_level-settings_export-mode_folder-protected}}` | a mesma pasta, com o documento do nível criptografado. Os metadados, a capa e as mídias continuam legíveis, por isso um navegador de níveis ainda mostra o cartão dele | gpg para o documento do nível |
| `{{ui:settings_level-settings_export-mode_zip}}` | um único arquivo | um clique duplo no Explorador de Arquivos do Windows, sem instalar nada |
| `{{ui:settings_level-settings_export-mode_targz}}` | um único arquivo | qualquer compactador |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | um zip com criptografia AES-256 própria. O sentido comum de uma senha em um arquivo compactado | 7-Zip ou qualquer outro compactador, que pede a senha |
| `{{ui:settings_level-settings_export-mode_zip-protected}}`, `{{ui:settings_level-settings_export-mode_targz-protected}}` | o mesmo arquivo compactado envolto em `.gpg` | gpg |

O Explorador de Arquivos do Windows não abre nenhuma das opções com senha. Esse é o preço de uma senha

Uma coleção ou um único recurso da Biblioteca aceita os mesmos cinco modos de arquivo compactado, inclusive os com senha. Os dois modos de pasta são só para um nível. Mais - [[17_publishing#Arquivo compactado]]

> [!tip] Dica
> Tudo o que não pôde ir junto (um recurso atrás de uma URL, um arquivo que nada referencia) aparece no relatório depois da exportação

> [!warning] Aviso
> Uma senha protege o conteúdo durante o envio e contra cópias casuais. Não é DRM: qualquer pessoa com o arquivo e a senha sempre consegue abri-lo

## Proteger o nível

Criptografa o documento do nível no disco. Abrir o nível pede a senha

O que fica protegido é o **conteúdo**: objetos, quadros-chave, temas. Os metadados, a capa e as mídias continuam legíveis. Por isso o navegador de níveis ainda mostra o cartão do nível sem a senha

A senha é pedida uma vez por sessão e fica só na memória. Ela nunca é gravada em lugar nenhum, por isso o salvamento automático continua funcionando

Para remover a proteção, deixe o campo vazio e clique em `{{ui:settings_level-settings_protect-apply}}`

> [!caution] Cuidado
> Uma senha esquecida não pode ser recuperada. Nenhuma chave é guardada em lugar nenhum, e não há como entrar no arquivo sem ela
