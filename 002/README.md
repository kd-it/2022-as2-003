# 問題2(hostPath)

イメージ[photon](https://hub.docker.com/_/photon)を用いたデプロイメントを作成せよ。
提出するファイルは本ディレクトリにあるex2.ymlとする。

なおphotonは、alpineと同様の省スペースのLinuxディストリビューションです(alpineよりは大きい)。
RHEL寄りのものとなっており、RHEL/CentOS(後継派生ものも含む)の`dnf`のミニ版`tdnf`によるパッケージ管理なども持っています。

* デプロイメントの名前は`ex2`とする
* `hostPath`を用いてボリュームを生成し、ノード上のディレクトリ `/data` を使用するようにせよ(名前は任意)
* 上記`hostPath`を用いたボリュームを、コンテナのディレクトリ `/data` にマウントさせよ
* photonイメージのsleepコマンドには"infinity"が実装されていないので、代用として"1h"(1時間)を渡せ ※下記コード例参照

```yaml
# コード例
command:
  - sleep
  - 1h
```

今回のボリュームのマウントを行った場合、ここまでの授業で利用したノード上の `/data` ディレクトリ以下が丸々見えるようになっている。自分で行っていればこのディレクトリにいくつかディレクトリができているはずである

```bash
# 確認の例
PS> kubectl exec -it deployments/ex2 -- ls /data
db  jenkins  mariadb  mariadb-data  pv0001
```

