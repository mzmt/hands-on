# AWS App Runner × Railsハンズオン

## App Runnerとは
https://aws.amazon.com/jp/apprunner/

> コンテナ化されたウェブアプリケーションやAPIを開発者が簡単かつ迅速にデプロイできるフルマネージド型サービスです

> 事前のインフラ経験を必要とせずにデプロイすることができます

> ソースコードからでも、コンテナイメージからでも始められます

2021/5現在ソースコードからのデプロイはNode.jsとPythonのみ対応

## 事前準備
- AWSアカウントの作成
- Dockerのインストール
- AWS CLIのインストール

DockerとAWS CLIに関しては、ECRのパブリックレポジトリにビルド済みのRailsイメージを配置しているので、なくても大丈夫です

## 流れ
1. `rails new`でプロジェクトを作成
2. Dockerfileを書きコンテナ化する
3. ECRのレポジトリを作成し、ビルドしたイメージをpushする
4. App Runnerにデプロイ

2021/05現在、RubyはApp Runnerのコードレポジトリからのデプロイに対応していないので、ECRにコンテナイメージを置いておく必要がある


## 手順

- Railsのサンプルプロジェクトをcloneする

`git clone git@github.com:mzmt/rails6_docker_template.git`
https://github.com/mzmt/rails6_docker_template

- `docker-compose up`して動くことを確認する
動くことが確認できたらctrl + Cで終了

- AWS consoleを開く
https://console.aws.amazon.com/console/home

- ECRレポジトリを作成する

- 画面上にコマンドが表示されるので実行してECRにpushする

- App Runnerでデプロイ

## もしデプロイが失敗した場合

デプロイ ログチェック
アプリケーションログチェック
