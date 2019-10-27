# Ruby on Rails and Google Cloud Platform on Docker Development Environment

Ruby on Rails を Docker で開発し、 Google Cloud Platform で稼働させたいときにつかうテンプレートです。主に自分用です。Docker はホストPC にインストールされている前提です。

Win10, Docker Desktop 2.1.0.4 stable で動作確認済み。

## 仕様

| 言語, エンジン | version |
| -------------- | ------- |
| Ruby           | 2.5     |
| Rails          | 6.0.0   |
| MySQL          | 5.7     |

## ディレクトリ構成

| ディレクトリ | 説明                                                  |
| ------------ | ----------------------------------------------------- |
| /            | リポジトリのルートディレクトリ。                      |
| /containers  | コンテナの Dockerfile などを収めています。            |
| /src         | Rails のソースコード一式が入ります。                  |
| /tmp         | MySQLのデータがなど、永続化に必要なデータが入ります。 |

## DB について

開発環境では MySQLコンテナを使用し、Google Cloud Platform にデプロイ後は CloudSQL を使用する想定です。

## 使い方

pull した後、下記コマンドを実行して使います。

```shell
docker-compose build
docker-compose up -d
docker-compose exec ruby25 bash
```

ruby25 コンテナにログインするので下記コマンドを実行すると Rails のプロジェクトが src ディレクトリ配下に作成されます。

```shell
rails new my_project
```

その後、プロジェクトディレクトリに移動してサーバを起動します。

```shell
cd my_project
rails s -b 0.0.0.0
```

ホストPC のブラウザで http://localhost:3000/ にアクセスして "Yay! You’re on Rails!" が表示されればOK。ここから開発を始めます。Google Cloud Platform の CLI を実行したい場合は下記コマンドを実行してください。

```shell
docker-compose exec gcloud bash
```

Rails のソースコードは /src にマウントされています。

```shell
cd /src/my_project
```



以上

