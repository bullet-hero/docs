---
title: 내보내기와 보호
date: 2026-10-11
tags: [level_author]
---

# 내보내기와 보호

내보내기는 레벨을 레벨이 쓰는 모든 파일과 함께 게임 밖에 폴더나 아카이브로 저장합니다. 비밀번호는 디스크에 있는 레벨 콘텐츠를 암호화하며, 잊어버린 비밀번호는 복구할 수 없습니다

## 레벨 내보내기

레벨 설정의 `{{ui:settings_level-settings_publication}}` 탭에 있습니다: 대상은 `{{ui:editor_share_archive}}`, 모드는 `{{ui:editor_share_format}}` 항목에서 고르고, 보호 모드에는 `{{ui:editor_share_passphrase}}` 필드를 씁니다. 자세히 - [[17_publishing]]

아카이브에는 레벨, 메타데이터, 레벨이 쓰는 모든 파일이 들어갑니다. 레벨 폴더 밖에 있는 곡도 복사해 넣습니다. 그 참조는 아카이브 안의 복사본을 가리키도록 바뀝니다

AI 어시스턴트가 레벨에 관한 메모를 보관하는 레벨의 `ai` 폴더도 함께 압축됩니다. 단, 레벨 메타데이터에서 `{{ui:settings_level-settings_metadata-level-ai-share}}` 옵션을 해제하면 제외됩니다. 비밀번호가 있는 모드는 이 폴더를 절대 압축하지 않습니다: 암호화된 레벨 옆에 읽을 수 있는 설계 메모가 있으면 비밀번호가 무의미해지기 때문입니다. 폴더가 제외되면 보고서가 알려 줍니다. 자세히 - [[7_ai-assistant#ai 폴더]]

| `{{ui:editor_share_format}}` | 결과 | 여는 방법 |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_folder}}` | 디스크에 있는 레벨 폴더 그대로입니다. 압축해서 보내면 됩니다 | 필요 없음 |
| `{{ui:settings_level-settings_export-mode_folder-protected}}` | 같은 폴더지만 레벨 문서가 암호화됩니다. 메타데이터, 커버, 미디어는 읽을 수 있는 상태로 남으므로 레벨 브라우저에 카드가 계속 표시됩니다 | 레벨 문서는 gpg |
| `{{ui:settings_level-settings_export-mode_zip}}` | 파일 하나 | Windows 탐색기에서 더블 클릭, 설치할 것 없음 |
| `{{ui:settings_level-settings_export-mode_targz}}` | 파일 하나 | 아무 압축 프로그램 |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | 자체 AES-256 암호화가 적용된 zip. 아카이브 비밀번호의 일반적인 의미입니다 | 비밀번호를 묻는 7-Zip 또는 다른 압축 프로그램 |
| `{{ui:settings_level-settings_export-mode_zip-protected}}`, `{{ui:settings_level-settings_export-mode_targz-protected}}` | 같은 아카이브를 `.gpg` 파일로 감싼 것 | gpg |

Windows 탐색기는 비밀번호가 있는 옵션을 하나도 열지 못합니다. 그것이 비밀번호의 대가입니다

라이브러리의 컬렉션이나 리소스 하나도 비밀번호 모드를 포함해 같은 다섯 가지 아카이브 모드로 내보낼 수 있습니다. 폴더 모드 두 가지는 레벨 전용입니다. 자세히 - [[17_publishing#아카이브]]

> [!tip] 팁
> 함께 옮길 수 없었던 것(URL 뒤의 리소스, 아무것도 참조하지 않는 파일)은 내보낸 뒤 보고서에 나열됩니다

> [!warning] 경고
> 비밀번호는 전송 중에, 그리고 가벼운 복사로부터 콘텐츠를 보호합니다. DRM이 아닙니다: 파일과 비밀번호가 있는 사람은 언제든 열 수 있습니다

## 레벨 보호

디스크에 있는 레벨 문서를 암호화합니다. 레벨을 열 때 비밀번호를 묻습니다

보호되는 것은 **콘텐츠**입니다: 오브젝트, 키프레임, 테마. 메타데이터, 커버, 미디어는 읽을 수 있는 상태로 남습니다. 그래서 레벨 브라우저는 비밀번호 없이도 레벨 카드를 보여 줍니다

비밀번호는 세션당 한 번 묻고 메모리에만 보관합니다. 어디에도 기록되지 않으므로 자동 저장이 계속 작동합니다

보호를 해제하려면 필드를 비워 두고 `{{ui:settings_level-settings_protect-apply}}` 버튼을 누르십시오

> [!caution] 주의
> 잊어버린 비밀번호는 복구할 수 없습니다. 키는 어디에도 보관되지 않으며, 비밀번호 없이는 파일을 열 방법이 없습니다
