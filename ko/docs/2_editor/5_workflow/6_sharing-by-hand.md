---
title: 레벨을 직접 공유하는 방법
date: 2026-10-01
tags: [level_author]
---

# 레벨을 직접 공유하는 방법

레벨 폴더를 zip 또는 tar.gz 형식으로 묶고, 비밀번호가 필요하면 gpg 도구로 암호화합니다. 다른 컴퓨터에서는 압축을 푼 레벨을 바로 플레이할 수 있고, 게임은 이런 아카이브를 직접 읽습니다

레벨은 파일이 든 폴더입니다. 아카이브는 보내기 위해 묶은 같은 폴더입니다.
레벨이 쓰는 모든 것이 함께 갑니다: 노래, 이미지, 커버

받는 사람이 레벨을 어디에 두는지 - [[2_metadata-and-sharing#지금 레벨을 공유하는 방법]]

## 아카이브에 들어가지 않는 것

- 레벨이 링크로 가져오는 리소스. 링크는 그대로 남습니다
- 레벨의 어떤 것도 참조하지 않는 파일

게임의 내보내기 보고서에 둘 다 나열됩니다. 자세히 - [[13_export-and-protection#레벨 내보내기]]

## 다섯 종류

각각 상대방이 이미 가진 도구로 열립니다:

| 파일 | 내용 | 여는 도구 |
|---|---|---|
| `level.json.gpg` | 레벨 문서만, 비밀번호로 보호되어 레벨 폴더 안에 있음 | gpg |
| `LEVEL_FOLDER.tar.gz` | 폴더 전체를 하나의 아카이브로 | 7-Zip, Keka, Ark, 탐색기 |
| `LEVEL_FOLDER.tar.gz.gpg` | 같은 아카이브를 비밀번호로 보호 | gpg |
| `LEVEL_FOLDER.zip` | 같은 폴더를 zip 형식으로 | Windows에서 더블 클릭, 설치할 것 없음 |
| `LEVEL_FOLDER.zip.gpg` | 같은 zip 파일을 비밀번호로 보호 | gpg |

기본적으로 게임은 zip 자체 기능(AES-256)을 써서 아카이브에 비밀번호를 겁니다. 탐색기를 제외한 모든 압축 프로그램이 이런 아카이브를 열 수 있으며, 비밀번호를 묻습니다.
`.gpg` 종류는 요청하면 게임이 씁니다

## 명령 줄을 실행하기 전에

명령 줄에서 두 곳을 바꾸십시오:
- `LEVEL_FOLDER` - 레벨 폴더 이름, 즉 레벨 ID. 숫자와 글자로 된 긴 문자열이며, `levels` 안에 있는 폴더의 이름입니다
- `YOUR_PASSWORD` - 비밀번호 자체

명령 줄에 입력한 비밀번호는 셸 기록에 남습니다.
줄에서 `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` 부분을 지우면 gpg에서 화면으로 비밀번호를 묻습니다

## 레벨 문서와 gpg

암호화하면 원본 옆에 `level.json.gpg` 파일이 생깁니다. 원본 파일은 그대로 남습니다: 결과를 확인한 뒤 직접 삭제하십시오.
복호화하면 문서가 원래 이름으로 다시 쓰입니다. 암호화된 파일은 그대로 남습니다:

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## tar.gz 아카이브

폴더는 안쪽에서 묶입니다: 아카이브에는 감싸는 폴더 없이 레벨 파일 자체가 들어갑니다.
압축을 풀려면 대상 폴더가 이미 있어야 하며, tar 명령은 폴더를 만들지 않습니다. `mkdir` 명령은 cmd, PowerShell, Mac 또는 Linux의 터미널에서 똑같이 동작합니다:

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

묶기와 암호화를 한 번에 합니다. 보호되지 않은 아카이브는 디스크에 아예 닿지 않습니다.
두 번째 줄은 아카이브를 복호화하고 같은 폴더에 다시 풉니다:

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## zip 아카이브

Windows에서 - 모든 컴퓨터에 있는 PowerShell에서 실행합니다. 별표는 폴더 자체가 아니라 폴더의 내용을 묶습니다.
`Expand-Archive` 명령은 폴더를 직접 만들므로, 미리 `mkdir` 명령을 실행할 필요가 없습니다:

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

Mac 또는 Linux에서 - zip 및 unzip:

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

7-Zip에서 비밀번호를 묻는 zip 파일은 7-Zip 자체로 만듭니다. 7-Zip 프로그램이 설치되어 있어야 합니다:

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## 게임이 다시 읽습니다

모든 종류는 양방향으로 동작합니다. 게임이 쓴 것은 gpg, tar, zip 도구로 열 수 있습니다. gpg, tar, zip 도구로 만든 것은 게임이 읽습니다.
그래서 자체 형식이 아니라 표준 도구를 택했습니다

> [!tip] 팁
> 게임은 파일 이름이 아니라 파일이 실제로 무엇인지를 봅니다. 그래서 이름을 바꾼 아카이브도 열립니다. 게임은 `7z` 형식을 알아보지만 받아들이지 않습니다: 파일이 깨졌다고 하는 대신 형식 이름을 알려 줍니다. 이런 아카이브는 zip 형식으로 다시 묶으십시오

> [!caution] 주의
> **잊어버린 비밀번호는 복구할 수 없습니다**. 키는 어디에도 저장되지 않습니다: 게임에도, 파일에도, 누구에게도. 초기화도, 복구도, 우회 방법도 없습니다. 비밀번호를 잃은 레벨은 비밀번호와 함께 사라집니다. 에디터를 닫기 전에 비밀번호를 적어 두십시오

다음: [[4_level-folder-and-backups|레벨 폴더와 백업]], [[4_not-losing-work|작업을 잃지 않기]]
