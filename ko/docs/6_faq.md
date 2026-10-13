---
title: 자주 묻는 질문
date: 2026-10-02
tags: [player, level_author]
---

# 자주 묻는 질문

Bullet Hero - 리듬 게임과 탄막 슈팅을 결합한 무료 하이브리드 게임입니다. 계정이 필요 없고, 서버는 아직 없습니다. 레벨은 플레이어가 내장 에디터에서 만들고 폴더나 압축 파일로 서로 주고받습니다

## 게임

### Bullet Hero 게임이란 무엇입니까?

리듬 게임과 탄막 슈팅의 하이브리드입니다. 레벨은 음악과 그에 맞춰 움직이는 도형으로 이루어집니다. 플레이어가 조작하는 작은 사각형이 트랙이 끝날 때까지 살아남아야 합니다

Bullet Hero 프로젝트는 장르를 위한 엔진으로 만들어지고 있습니다. 그래서 대부분의 레벨은 플레이어가 내장 에디터에서 만듭니다.
자세히 - [[1_game/index]]

### 게임은 무료입니까?

예. 게임에는 결제, 광고, 유료 콘텐츠가 없습니다.
자세히 - [[1_licensing-basics]]

### 어디에서 받을 수 있습니까?

모든 빌드와 스토어 - [[download]]

게임은 정식 출시되었으며, 버전은 `gv {{v:version.gv}}`입니다. 빌드에는 서명이 없습니다

### 계정이나 인터넷이 필요합니까?

아니요. 계정도 서버도 없으며, 게임은 아무것도 어디로도 보내지 않습니다

인터넷이 필요한 것은 한 종류의 레벨뿐입니다: 제작자의 웹 주소에서 파일을 불러오는 레벨입니다.
자세히 - [[1_installation]]

### 레벨은 어디에 저장됩니까?

게임 데이터 폴더 안의 `levels` 폴더에 저장됩니다. 여는 방법: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`.
자세히 - [[1_installation]]

## 레벨 플레이

### 누군가에게 받은 레벨은 어떻게 플레이합니까?

폴더를 `levels`에 넣고 레벨 목록에서 `{{ui:root_level-browser_refresh}}` 버튼을 누릅니다.
압축 파일(`.zip`, `.tar.gz`)은 에디터에서 `{{ui:gen_level_archive}}` 생성기로 엽니다.
자세히 - [[2_playing-levels]]

### 레벨이 더 새로운 버전에서 만들어졌다는 메시지가 나옵니다. 어떻게 해야 합니까?

게임을 업데이트하세요. 이전 버전은 파일을 잘못 읽지 않도록 더 새로운 버전의 파일을 열지 않습니다.
자세히 - [[5_troubleshooting]]

### 잊어버린 레벨 비밀번호를 복구할 수 있습니까?

아니요. 키는 어디에도 저장되지 않습니다: 게임에도, 파일에도, 누구에게도 없습니다.
자세히 - [[5_troubleshooting]]

### 게임이 레벨을 스스로 플레이할 수 있습니까?

예. 레벨 화면의 `{{ui:menu_levelview_options-bot}}` 조건에서 `{{ui:enum_bot-kind_reflex}}` 또는 `{{ui:enum_bot-kind_warm}}` 중 하나를 고릅니다. 봇은 플레이어와 같은 조작을 사용하며, 봇도 질 수 있습니다.
자세히 - [[9_bots]]

## 레벨 제작

### 첫 레벨은 어떻게 만듭니까?

메인 메뉴의 `{{ui:menu_main_editor-btn}}`, 그다음 `{{ui:settings_editor-settings_editor-settings}}`, 그다음 `{{ui:settings_editor-settings_create-level}}` 순서로 누릅니다.
레벨 폴더에 트랙을 복사하고, 템포(bpm)를 설정하고, 키프레임이 두 개인 오브젝트를 배치한 다음 플레이 테스트를 실행합니다.
자세히 - [[2_first-level]]

### 어떤 음악 파일을 쓸 수 있습니까?

`ogg`, `mp3`, `wav`뿐이며 그 밖에는 없습니다. `flac`, `aiff`, 트래커 모듈은 불러와지지 않습니다

가장 좋은 선택은 `ogg` 형식입니다. `wav`보다 8-10배 작고, `mp3` 형식과 달리 시작 부분에 무음을 덧붙이지 않습니다.
자세히 - [[2_preparing-the-track]]

### 아무 노래나 써도 됩니까?

자신의 디스크에 있는 것은 아무것도 검사하지 않습니다. 음악의 라이선스는 레벨을 서비스에 제출할 때 중요해지며, 그런 서비스는 아직 없습니다.
자세히 - [[1_licensing-basics]]

### 레벨은 어떻게 공유합니까?

폴더나 압축 파일로 직접 전달합니다. Steam 빌드에서는 레벨을 Steam 창작마당에 게시할 수도 있습니다. 공식 서버는 아직 없습니다.
자세히 - [[6_sharing-by-hand]], [[17_publishing]]

## 프로젝트

### 온라인 순위표나 레벨 카탈로그가 있습니까?

아직 없습니다. 공식 서버와 커뮤니티 서버는 개발 중입니다.
자세히 - [[4_server/index]]

### 게임 코드는 왜 비공개입니까?

제게는 개인적인 이유가 있습니다.
개발이 완전히 끝나면 모든 저장소가 공개되고, [bullet-hero](https://github.com/bullet-hero) 조직은 다른 사람에게 넘겨질 수도 있습니다

SDK, 문서, 앞으로 나올 서버는 이미 공개되어 있습니다. 자세히 - [[index]]

### 버그를 발견했습니까?

게임 버그는 [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)에 알려 주세요. 질문은 [Discord](https://discord.gg/gkHQrp9NgS)에서 해 주세요.
어디에 쓰고 무엇을 첨부할지 - [[11_help]]

프로젝트의 모든 링크 - [[links]]
