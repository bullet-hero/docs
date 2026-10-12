---
title: 合法なリソースへの2つの道
date: 2026-09-25
tags: [level_author]
---

# 合法なリソースへの2つの道

リソースが条件を満たすのは、適切なライセンスがあるか、権利者の許可がある場合です。3つ目の道はありません

外部リソースとは、レベルが持ち込むすべてのものです：音楽、画像、フォント、テキスト、あらゆるファイル。すべてのリソースが**2つのうちどちらか**に当てはまる必要があります

## 選択肢A：オープンライセンス

リソースがすでに`CC BY-NC`より厳しくない条件で配布されている場合です。リソースは独自の条件を保ちます。`CC BY-NC`に変わるわけではありません

標準プロファイルが受け付けるもの：
- [CC0](https://creativecommons.org/publicdomain/zero/1.0/)：パブリックドメイン
- [CC BY](https://creativecommons.org/licenses/by/4.0/)：バージョン4.0と3.0
- [CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/)：バージョン4.0と3.0
- [MIT](https://choosealicense.com/licenses/mit/)と[Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)：テキストとコード向け
- [SIL OFL 1.1](https://openfontlicense.org/open-font-license-official-text/)：フォント向け。メタデータに記載する必要があります
- [Unlicense](https://choosealicense.com/licenses/unlicense/)

> [!tip] 推奨
> 自分で選べるなら`CC0`にしてください。レベルに何も求めない唯一のライセンスです

## 標準プロファイルが拒否するもの

- **プロプライエタリ**、いわゆる「全著作権所有」
- [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/)：レベルをCC BY-NC-SAで公開しなければならなくなりますが、レベルはこのライセンスでは配布されません
- [CC BY-ND](https://creativecommons.org/licenses/by-nd/4.0/)：改変を禁止しており、ゲームはこれに対応していません
- [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/)と[CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/)：同じ2つの理由から

GPLファミリーは、CC BY-NCより自由であるにもかかわらずリストにありません。GPLのコードは、Appleの規約と衝突せずにApp Storeで配布することができません。そのため、iOS版に入るものはすべてMITやApacheの形にとどめる必要があります

## プロファイルはサービスで決まる

どのライセンスを受け付けるかを決めるのはライセンスではなくサービスです。上のリストは標準プロファイルです。ストア版が受け付けるものはより少なく、コミュニティサーバーは別のものを受け付けることがあります

## 選択肢B：権利者の許可

個人的な「いいよ、使って」では足りません。`CC BY-NC`のレベルは公に配布されるので、許可は個人的な使用ではなく、まさにその配布を対象にしている必要があります

有効な許可は、次の3点をすべて認めるものです：
1. Bullet Heroのレベル内でリソースを使用する権利
2. リソースを含むレベルが、ゲームのサービスを通じて、クレジット表記付きで第三者により自由かつ非営利に配布される権利
3. 明示的に非営利目的の使用に限ること

尋ね方：[[6_asking-permission]]

> [!caution] 注意
> 許可があっても、拒否が通過に変わるわけではありません。リソースのライセンスが拒否されるものの1つであれば、許可によってそのリソースは人による審査に回されますが、「許可済み」にはなりません

## 許可の範囲と期限

範囲や証拠のない許可は不完全とみなされます。期限切れの許可はまったく数に入りません

**範囲は記録されます**。そしてそれは重要です：
- 特定の1つのレベル向けの許可は、そのリソースを別のレベルにコピーすると効力を失います
- どのレベルでもよいという許可は、どんな再利用にも有効です

次へ：[[6_asking-permission]]、[[4_resource-record]]
