# Fluentd Aggregator Image
Fluentd の Docker イメージです。GKEのポッド上で多くの入力元からのログを一元化することを想定しています。
そのため、Google Cloud Storage の出力プラグインがインストールされています。

## リファレンスデザイン
[Fluentd GCP Image](https://github.com/GoogleCloudPlatform/k8s-stackdriver/tree/master/fluentd-gcp-image)

## debian-base-amd64:v1.0.0
非常に軽量の debian イメージです。
sh などの最低限のツールは搭載されていますが、例えば、/bin/bash などを実行することはできません。
`apt-get` は使用できますが、より便利な `clean-install` というコマンドが提供されています。

v1.0.0 は、version 9.8 の debian ディストリビューションを使用しています。

## fluentd の設定方法
`/etc/fluent/config.d` 以下の全ての `.conf` ファイルを読みます。
GKE 上でデプロイする際に、configmap から設定をしてください。

## ビルド方法：fluentd のプラグインのカスタマイズ (Gemfile の更新）
Gemfile を更新して、`make build` を行なってください。
依存関係が解決できなかった場合、ビルドが失敗します。

イメージの作成に成功したら、`update-dependencies` で Gemfile.lock を更新できます。

## fluentd の引数
`FLUENTD_ARG` 環境変数が fluentd コマンドに渡されます。

