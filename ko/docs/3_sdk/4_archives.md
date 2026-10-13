---
title: 아카이브와 보호
date: 2026-10-01
tags: [developer, level_author]
---

# 아카이브와 보호

레벨은 폴더, tar.gz, zip 중 하나로 내보내며, 원하면 비밀번호를 걸 수 있습니다: AES-256 zip 또는 OpenPGP. SDK에서는 받은 파일의 형식을 이름이 아니라 첫 바이트로 판별합니다

## 내보내기 모드

레벨은 `LevelExportMode`의 형태 중 하나로 기기를 떠납니다:

| 값 | 모드 | 기록되는 것 | 보호 |
|---|---|---|---|
| 0 | `Folder` | 디스크와 같은 구조의 일반 폴더 | 없음 |
| 1 | `FolderProtectedLevel` | `level.json.gpg` 파일만 암호화된 폴더 | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | 없음 |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | 없음 |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | 항목이 AES-256 방식으로 암호화된 `<name>.zip` | zip 자체 암호화 |

번호는 모드의 정체성이며 절대 바뀌지 않습니다. 에디터 드롭다운에서의 순서는 따로 정해집니다(`DisplayOrder`)

**모든 형식은 개방형 표준입니다.** `tar -xzf`, `gpg -d`, 그리고 어떤 압축 프로그램으로든 게임 없이 열 수 있습니다:

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## 두 가지 보호 방식

**`ZipEncrypted` 모드가 비밀번호로 레벨을 잠그는 기본 방법입니다.** 받는 사람에게 압축 프로그램은 있어도 gpg 프로그램은 없을 가능성이 높습니다

**OpenPGP 하나로 문서, 폴더, 아카이브를 모두 잠글 수 있습니다.** 폴더를 보호할 수 있는 것은 이 방식뿐입니다

`FolderProtectedLevel` 모드에서는 메타데이터, 커버, 미디어가 읽을 수 있는 상태로 남습니다. 그래서 레벨 브라우저에 카드가 계속 표시됩니다

안쪽 확장자는 이름에 남습니다: `level.json.gpg`. `gpg -c level.json` 명령이 정확히 이 이름으로 파일을 만들기 때문에, 추측 없이 형식을 알 수 있습니다

## 안에 들어가는 것

`LevelArchiveBuilder` 클래스는 폴더의 파일 목록이 아니라 모델을 보고 내용을 정합니다. 레벨이 참조하지 않는 파일은 밖에 남습니다. 그런 파일이 몇 개 남았는지는 보고서에 나옵니다

레벨의 참조는 다음과 같이 처리됩니다:
- `AbsolutePath` 리소스는 아카이브 안으로 복사됩니다. 그 참조는 `LevelPath` 값으로 바뀌지만, 내보낸 사본에서만 바뀝니다
- `DirectUrl` 리소스는 그대로 두고 보고서에 기록합니다: URL 주소는 파일 안에 담아 옮길 수 없습니다
- 없는 파일은 `archive.resource_missing` 코드로 보고서에 기록됩니다

## 바이트로 판별

파일 이름은 누구나 쓸 수 있습니다. 그래서 `ArchiveFormatSniffer` 클래스는 첫 8바이트로 판단합니다:

| 첫 바이트 | 형식 |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`, `50 4B 05 06`, `50 4B 07 08`, `50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| OpenPGP 패킷 태그, 마지막에 검사 | `OpenPgp`: 복호화한 뒤 다시 판별 |

> [!warning] 경고
> `.7z` 형식은 읽지도 쓰지도 않습니다. 거부 메시지에서 형식 이름을 밝히기 위해서만 판별합니다(`Unsupported`). 그러면 파일이 깨졌다고 판단하는 대신 레벨을 zip 형식으로 다시 압축하게 됩니다

## 읽기

`LevelArchiveReader.ReadAsync` 메서드는 폴더 또는 탐색 가능한 `Stream` 객체를 받습니다. 반환값은 `LevelArchiveContent` 객체이며, 그 안의 `LevelArchiveOpenResult` 값은 다음 중 하나입니다:

| 결과 | 의미 |
|---|---|
| `Ok` | 읽음 |
| `PassphraseRequired` | 비밀번호가 없으므로 물어봐야 함 |
| `WrongPassphrase` | 이미 비밀번호를 입력했지만 틀림 |
| `Damaged` | 파일이 손상됨 |
| `NotAnArchive` | 아카이브가 아님 |
| `Unsupported` | 형식은 인식했지만 지원하지 않음 |

`PeekMetaAsync` 메서드는 카드나 카탈로그를 위해 메타데이터만 읽습니다

서버는 누군가 업로드하기로 한 것이면 무엇이든 읽습니다. 그래서 리더는 `ArchiveLimits` 한도 안에서 작동합니다. 기본값은 다음과 같습니다:
- 항목 4096개
- 항목당 512 MiB
- 전체 1 GiB

주어진 저장 공간 밖으로는 아무것도 압축 해제되지 않습니다

에디터 쪽에서의 내보내기 - [[13_export-and-protection]]
