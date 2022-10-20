# 問題1(emptyDir)

Webサーバーnginxをクラスタ上で起動したいが、コンテンツのディレクトリ(`/usr/share/nginx/html`)に対しemptyDirで用意される空のボリュームを割り当てておきたい。
この仕様に対するデプロイメントを作成せよ、作成ファイル名は `ex1.yml` とする。

* vscodeのスニペットから始めてよい(というか推奨)、deploymentと入れると途中で拾えるはず
* 名前やセレクターで使うappキーの値などはex1にする
* コンテナの利用するイメージはnginxとする
* ports.containerPortは80とする
* ボリューム名はマッピングさえできれば名前は好きにしていいが、名前を見てなんのためのボリュームかわかる名称にしておくこと(マナーです)
    * 今回はemptyDir形式で空のボリュームを用意させる
    * このボリュームをディレクトリ`/usr/share/nginx/html`にマウントさせること

成功していれば、コンテンツディレクトリ(`/usr/share/nginx/html`)以下は空っぽとなる。

自分で評価するという意味では、いちど失敗(ファイルが見える)の状態を確認した上で覆い隠すようにボリュームを設定すると良いかもしれない。
以下がチェックの例となっている。

```pwsh
# 成功例
PS> kubectl exec -it deploy/ex1 -- ls /usr/share/nginx/html
PS> # 空っぽなのでそのまま返って正解
```

```pwsh
# 失敗例
PS> kubectl exec -it deploy/ex1 -- ls /usr/share/nginx/html
50x.html  index.html
# ↑ もともとのコンテンツが見えてる
```
