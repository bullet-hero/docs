---
title: 도움말과 버그 신고
date: 2026-10-02
tags: [player, level_author]
---

# 도움말과 버그 신고

게임 버그는 releases 이슈에, 질문은 Discord에 올립니다. 설정에 있는 버전 문자열과 버그가 나타나기까지의 단계를 첨부하십시오

먼저 [[5_troubleshooting]] 페이지를 확인하십시오. 사라진 레벨, "게임 업데이트 필요", 거부된 아카이브는 그곳에서 다룹니다

## 어디에 올릴까

| 내용 | 위치 |
|---|---|
| 게임이나 에디터의 버그, 게임에 대한 요청 | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| SDK 또는 SDK 코드의 버그 | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| 문서의 오류나 오래된 정보 | [bullet-hero/docs](https://github.com/bullet-hero/docs), [[community]] |
| 질문, 레벨 제작 도움, 토론 | [Discord](https://discord.gg/gkHQrp9NgS) |

GitHub의 메시지는 공개됩니다. 누구나 읽고 덧붙일 수 있습니다.
문서에는 이슈나 풀 리퀘스트를 보낼 수 있습니다

버그인지 확실하지 않습니까? 먼저 Discord에서 물어보십시오

프로젝트의 모든 링크 - [[links]]

## 버그 신고에 넣을 내용

재현할 수 있는 버그는 고쳐집니다. "튕겼어요"는 보통 고칠 수 없습니다: 무엇을 반복해야 할지 아무도 모르기 때문입니다

1. **버전 문자열.** 설정 화면의 버전 문자열을 클릭하면 자동으로 복사됩니다. 형식은 다음과 같습니다: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`, [[4_settings]]
2. **플랫폼과 기기:** 운영 체제, 그리고 휴대폰이라면 모델명
3. **단계:** 무엇을 했는지, 무엇을 기대했는지, 실제로 무슨 일이 일어났는지
4. **레벨,** 버그가 레벨과 관련 있다면: 아카이브로 묶은 레벨 폴더 또는 열었던 아카이브. 레벨이 보호되어 있다면 그렇다고 적어 주십시오
5. **오류 보고서,** 오류 창이 떴다면. `{{ui:root_error_save}}` 버튼은 보고서를 `reports` 폴더에 저장하고, `{{ui:root_error_open-reports-folder}}` 버튼은 그 폴더를 엽니다, [[1_installation]]

> [!tip] 팁
> 파일은 메시지 본문에 붙여 넣지 말고 첨부하십시오. 로그는 길어서 본문 안에서는 읽기 어렵습니다

## 로그

게임은 실행되는 동안 로그를 남깁니다. 오류 창이 전혀 뜨지 않았을 때 도움이 됩니다

- **Windows:** 게임 데이터 폴더의 `Player.log`, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (Unity의 표준 위치)
- **Android:** 로그는 logcat에 기록됩니다. 기기를 컴퓨터에 연결한 상태에서 `adb logcat -s Unity` 명령으로 출력할 수 있습니다
- **기타 시스템:** 아직 설명되지 않았습니다
