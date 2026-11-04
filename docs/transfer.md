# jphacks/sp_2603 から mofumofupop/fllooat への移行

JPHACKS で開発した [jphacks/sp_2603](https://github.com/jphacks/sp_2603) を、mofumofupop のリポジトリとして続けて開発するための方針と、移行でやったことをまとめる。リポジトリは移管 (transfer) せず、履歴ごと複製した。2026年11月4日に、複製、public 化、デプロイ元の切り替えを終えた。チームメンバーの同意と JPHACKS の規約の確認が残っている。

## 決まっていること

- **移管ではなく複製する。** jphacks/sp_2603 の持ち主は jphacks org で、こちらの権限は WRITE だけなので、そもそも移管はできない。元のリポジトリは JPHACKS の提出物としてそのまま残す。
- **コミット履歴は残し、作者は otnc・usamimi39・DAVM26・oliveoiler の4人だけにする。** コミットの作者情報は変えないので、mofumofupop/fllooat の Contributors にも4人が表示される。そのために次の2つを外した。
  - `wakana2050` の Initial commit (JPHACKS のテンプレート)
  - 24個のコミットのメッセージにある `Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com>` の行。残すと、そのコミットの共同作者として Claude が表示される
- **最初は private で作り、あとで public にする。** 2026年11月4日に public にした。
- **ライセンスは MIT のまま、著作権表示はもふもふぽっぷを先頭に書き、JPHACKS の表示も残す。** 詳しくは次の節。
- **デプロイ元を mofumofupop/fllooat に移す。** 2026年11月4日に切り替えた。

## ライセンスは MIT のまま、もふもふぽっぷを先頭に書く

元のリポジトリの `LICENSE` は次のとおりで、JPHACKS のテンプレートで置かれたもの。

```
The MIT License (MIT)

Copyright (c) 2026 JPHACKS
```

MIT ライセンスは、著作権表示とライセンス文を残せば、誰でも複製・改変・再配布できる。そのため複製そのものに許可は要らない。ただし、表示を残すことが条件なので、**元のコードについての JPHACKS の著作権表示は消さずに残し、その前にもふもふぽっぷの名前を書く**。

```
The MIT License (MIT)

Copyright (c) 2026 もふもふぽっぷ, JPHACKS
```

**順番は、もふもふぽっぷを先頭にする。** MIT は名前の順番を定めていないので、JPHACKS の名前が残っていれば、どちらを先に書いても条件は満たす。日本語の名前を書いても問題ない。

**JPHACKS の表示は、今後もこのまま残す。** [JPHACKS2021 の参加者向けガイドライン](https://jphacks.github.io/2021-guideline/rule/) では、成果物の知的財産権は創作・開発した参加者に帰属するとされていて、`JPHACKS` の表記はテンプレート由来の可能性が高い。それでも表記を消す根拠としては弱いので、消さないことにした。

なお、jphacks/sp_2603 にあるコードは今後も MIT で公開され続ける。複製先でライセンスを変えても、元のリポジトリの分は取り消せない。

## チームメンバーの同意は未取得

元のリポジトリ (`main` の157コミット) の作者は次のとおり。複製後に残したのは上の4人。

| GitHub | コミット数 | 複製後 |
| --- | --- | --- |
| otnc | 109 | 残す |
| usamimi39 | 39 | 残す |
| DAVM26 | 5 | 残す |
| oliveoiler | 3 | 残す |
| wakana2050 | 1 | 外す。JPHACKS のテンプレートの Initial commit |
| Claude (共同作者) | 24 | 外す。コミットメッセージの `Co-Authored-By` 行だけを消し、コミット自体は残す |

MIT を続けるだけなら、ほかのメンバーの同意がなくても複製と公開はできる。それでも、mofumofupop で続けることと、著作権表示にもふもふぽっぷを足すことは、usamimi39・DAVM26・oliveoiler に伝えて、記録が残る場所 (Issue や Discord) で同意を取っておく。MIT 以外のライセンスに変えることになった場合は、既存のコードを書いた全員の同意が必要になる。

## JPHACKS の規約で確認が必要なこと

確認できたのは2021年版のガイドラインだけで、同じ URL の2026年版と2025年版は見つからなかった (404)。2021年版には次の定めがある。

- 成果物の知的財産権は、創作・開発した参加者に帰属する
- 運営事務局とスポンサー企業は、イベントの報告や公表に必要な範囲で成果物を使える
- 運営事務局が用意した素材は、イベントでの開発目的に限って使える
- GitHub で公開するときは、原則として MIT ライセンスを置く
- 商品化・サービス化したい場合は、運営事務局またはスポンサー企業と優先的に交渉する

最後の項目が今年も同じなら、有料化や事業化をするときに影響する。その前に、今年の応募要項か参加者向けガイドラインで確認する。運営事務局の素材にあたるもの (テンプレートの README など) が残っていないかも、あわせて確認する。

## 第三者の素材のライセンスはそのまま引き継ぐ

フォント (Gen Interface JP、OFL-1.1) などの第三者の素材は、元のリポジトリの `THIRD_PARTY_LICENSES.md` と `licenses/` で管理している。これは複製先でもそのまま残し、自分たちのライセンスの変更とは関係なく、それぞれのライセンスに従う。

## デプロイ元の切り替え

jphacks/sp_2603 は GitHub Actions から mofumofupop の Cloudflare アカウントにデプロイしていた。複製先からも同じ Worker にデプロイすると、2つのリポジトリが同じ本番環境を上書きし合うので、2026年11月4日に次の順で切り替えた。

1. Cloudflare で `GitHub Actions deploy (mofumofupop/fllooat)` という API トークンを作り、mofumofupop/fllooat の Secrets に `CLOUDFLARE_API_TOKEN` として登録した。権限は jphacks/sp_2603 のトークンと同じにした
2. mofumofupop/fllooat の `Deploy` ワークフローを手で実行し、`fllooat.mfmf.moe` にデプロイできることを確かめた
3. jphacks/sp_2603 の `Deploy` ワークフローを無効にし、Secrets から `CLOUDFLARE_API_TOKEN` を消した
4. Cloudflare の `GitHub Actions deploy (jphacks/sp_2603)` トークンを削除した

今は mofumofupop/fllooat の `main` で CI が通ると、本番にデプロイされる。jphacks/sp_2603 に push しても、本番は変わらない。

## 複製の手順

mofumofupop/universe のモノレポ化と同じく、`git filter-repo` を使った。

1. jphacks/sp_2603 の `main` を clone する
2. `wakana2050` の Initial commit を根元から外す。`git replace --graft` で2番目のコミットの親をなくしてから `git filter-repo` を実行し、Initial commit で追加された `LICENSE` と `README.md` は、新しい最初のコミットに入るようにする
   - PR #1 のマージコミットも1番目の親が Initial commit なので、親を PR のブランチ側だけにする。マージの前後で中身は変わらないので、このコミットは差分のない普通のコミットとして残る
3. コミットメッセージを2か所書き換える
   - `Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com>` の行を消す
   - `#123` を `jphacks/sp_2603#123` に書き換える。元のリポジトリには Issue と PR が54番まであり、そのままだと複製先の別の Issue にリンクされてしまう
4. 作者が otnc・usamimi39・DAVM26・oliveoiler の4人だけになったことと、ファイルの中身が元の `main` と一致することを確かめる
5. このリポジトリの `main` に取り込み、`LICENSE` の著作権表示を `もふもふぽっぷ, JPHACKS` にしてから push する。このファイルを書いたコミットは、取り込んだ履歴の上に積み直した

複製した履歴は156コミットで、書き換えたコミットからは GitHub の署名が外れた。Issue、PR、Projects、Secrets は複製されないので、必要なものは手で移すか、元のリポジトリへのリンクで済ませる。

## 未決の項目

- usamimi39・DAVM26・oliveoiler への説明と同意
- 今年の JPHACKS の規約の確認
