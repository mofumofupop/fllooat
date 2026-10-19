# jphacks/sp_2603 から mofumofupop/fllooat への移行

JPHACKS で開発した [jphacks/sp_2603](https://github.com/jphacks/sp_2603) を、mofumofupop のリポジトリとして続けて開発するための調査結果と方針をまとめる。リポジトリは移管 (transfer) せず、履歴ごと複製する。2026年10月19日時点の内容で、未決の項目が残っている。

## 決まっていること

- **移管ではなく複製する。** jphacks/sp_2603 の持ち主は jphacks org で、こちらの権限は WRITE だけなので、そもそも移管はできない。元のリポジトリは JPHACKS の提出物としてそのまま残す。
- **履歴ごと複製する。** コミットの作者情報を変えなければ、mofumofupop/fllooat の Contributors にも同じメンバーが表示される。
- **`wakana2050` の Initial commit (JPHACKS のテンプレート) は外す。** mofumofupop/universe で cathiecode の Initial commit を外したときと同じ手順を使う。
- **最初は private で作り、あとで public にする。**
- **ライセンスは MIT のまま、著作権表示を `もふもふぽっぷ, JPHACKS` にする方針。** 詳しくは次の節。
- **デプロイ元は、今後 mofumofupop/fllooat に移す。** 時期は未定で、それまでは jphacks/sp_2603 からデプロイする。

## ライセンスは MIT のまま、著作権表示を足す

元のリポジトリの `LICENSE` は次のとおりで、JPHACKS のテンプレートで置かれたもの。

```
The MIT License (MIT)

Copyright (c) 2026 JPHACKS
```

MIT ライセンスは、著作権表示とライセンス文を残せば、誰でも複製・改変・再配布できる。そのため複製そのものに許可は要らない。ただし、表示を残すことが条件なので、**元のコードについての JPHACKS の著作権表示は消さずに残し、もふもふぽっぷの名前を足す**形にする。

```
The MIT License (MIT)

Copyright (c) 2026 もふもふぽっぷ, JPHACKS
```

名前の順番に決まりはなく、JPHACKS の名前が残っていればよい。日本語の名前を書いても問題ない。どちらの名前がどのコードの権利者かを分けて示したい場合は、次のように行を分けてもよいが、実務上の違いはほとんどない。

```
Copyright (c) 2026 もふもふぽっぷ
Copyright (c) 2026 JPHACKS
```

表記をもふもふぽっぷだけにしたい場合は、JPHACKS の表示を消してよいかを運営事務局に確認する必要がある。[JPHACKS2021 の参加者向けガイドライン](https://jphacks.github.io/2021-guideline/rule/) では、成果物の知的財産権は創作・開発した参加者に帰属するとされていて、`JPHACKS` の表記はテンプレート由来の可能性が高い。とはいえ表記を消す根拠としては弱いので、確認が取れるまでは両方を残す。

なお、jphacks/sp_2603 にあるコードは今後も MIT で公開され続ける。複製先でライセンスを変えても、元のリポジトリの分は取り消せない。

## チームメンバーの同意は未取得

元のリポジトリのコントリビューターは次の5人。

| GitHub | コミット数 | 備考 |
| --- | --- | --- |
| otnc | 109 | |
| usamimi39 | 39 | |
| DAVM26 | 5 | |
| oliveoiler | 3 | |
| wakana2050 | 1 | JPHACKS のテンプレートの Initial commit。複製では外す |

MIT を続けるだけなら、ほかのメンバーの同意がなくても複製と公開はできる。それでも、mofumofupop で続けることと、著作権表示にもふもふぽっぷを足すことは、usamimi39・DAVM26・oliveoiler に伝えて、記録が残る場所 (Issue や Discord) で同意を取っておく。MIT 以外のライセンスに変えることになった場合は、既存のコードを書いた全員の同意が必要になる。

## JPHACKS の規約で確認が必要なこと

確認できたのは2021年版のガイドラインだけで、同じ URL の2026年版と2025年版は見つからなかった (404)。2021年版には次の定めがある。

- 成果物の知的財産権は、創作・開発した参加者に帰属する
- 運営事務局とスポンサー企業は、イベントの報告や公表に必要な範囲で成果物を使える
- 運営事務局が用意した素材は、イベントでの開発目的に限って使える
- GitHub で公開するときは、原則として MIT ライセンスを置く
- 商品化・サービス化したい場合は、運営事務局またはスポンサー企業と優先的に交渉する

最後の項目が今年も同じなら、有料化や事業化をするときに影響する。public にする前に、今年の応募要項か参加者向けガイドラインで確認する。運営事務局の素材にあたるもの (テンプレートの README など) が残っていないかも、あわせて確認する。

## 第三者の素材のライセンスはそのまま引き継ぐ

フォント (Gen Interface JP、OFL-1.1) などの第三者の素材は、元のリポジトリの `THIRD_PARTY_LICENSES.md` と `licenses/` で管理している。これは複製先でもそのまま残し、自分たちのライセンスの変更とは関係なく、それぞれのライセンスに従う。

## デプロイ元を移すときの注意

jphacks/sp_2603 は GitHub Actions から mofumofupop の Cloudflare アカウントにデプロイしている。Cloudflare 側には `GitHub Actions deploy (jphacks/sp_2603)` という API トークンがあり、jphacks/sp_2603 の Secrets に `CLOUDFLARE_API_TOKEN` が登録されている。

複製先からも同じ Worker にデプロイすると、2つのリポジトリが同じ本番環境を上書きし合う。デプロイ元を移すときは、次の順で切り替える。

1. mofumofupop/fllooat 用の API トークンを作り、Secrets に登録する
2. mofumofupop/fllooat からデプロイできることを確かめる
3. jphacks/sp_2603 のデプロイ用ワークフローを止め、`CLOUDFLARE_API_TOKEN` を Secrets から消す
4. Cloudflare の `GitHub Actions deploy (jphacks/sp_2603)` トークンを削除する

JPHACKS の審査や表彰が残っているあいだは、jphacks/sp_2603 のデプロイを止めない。

## 複製の手順 (予定)

mofumofupop/universe のモノレポ化と同じく、`git filter-repo` を使う。

1. jphacks/sp_2603 の `main` を clone する
2. `wakana2050` の Initial commit を根元から外す。最初に残るコミットが `.gitignore` などを追加した形になる
3. コミットメッセージ中の `#123` を `jphacks/sp_2603#123` に書き換える。元のリポジトリには Issue と PR が54番まであり、そのままだと複製先の別の Issue にリンクされてしまう
4. このリポジトリの `main` に取り込み、`LICENSE` の著作権表示を `もふもふぽっぷ, JPHACKS` にする
5. 履歴の中身が元の `main` と一致することを確かめてから push する

Issue、PR、Projects、Secrets は複製されない。必要なものは手で移すか、元のリポジトリへのリンクで済ませる。

## 未決の項目

- JPHACKS の著作権表示を将来も残すか (運営事務局への確認しだい)
- usamimi39・DAVM26・oliveoiler への説明と同意
- 今年の JPHACKS の規約の確認
- public にする時期
- デプロイ元を移す時期
