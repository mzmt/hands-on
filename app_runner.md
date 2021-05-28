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

### Railsのサンプルプロジェクトをcloneする

`git clone git@github.com:mzmt/rails6_docker_template.git`

https://github.com/mzmt/rails6_docker_template

### `docker-compose up`して動くことを確認する
動くことが確認できたらctrl + Cで終了

### AWS consoleを開く
https://console.aws.amazon.com/console/home

### ECRレポジトリを作成する

![Screen Shot 2021-05-28 at 11 12 05](https://user-images.githubusercontent.com/13535662/119919566-abeee000-bfa5-11eb-9e73-724f0fc40479.png)

可視性設定をプライベートにして、リポジトリ名に適当な名前を入力し、「レポジトリを作成」ボタンを押す

![Screen Shot 2021-05-28 at 11 13 58](https://user-images.githubusercontent.com/13535662/119919762-0ee07700-bfa6-11eb-824c-6f81978e2ec0.png)


### ECRにpushする
レポジトリを開き、「プッシュコマンドを表示」ボタンを押すと、画面上にコマンドが表示されるのでコピーして実行する
![Screen Shot 2021-05-28 at 11 18 48](https://user-images.githubusercontent.com/13535662/119920099-b2ca2280-bfa6-11eb-9fae-4145b91608ae.png)

これでECRのレポジトリにビルド済みのRailsイメージが配置されたので、そのイメージを使ってApp Runnerにデプロイしていく

### App Runnerでデプロイ
App Runnerを開き、「サービスの作成」をクリック
![Screen Shot 2021-05-28 at 11 25 25](https://user-images.githubusercontent.com/13535662/119920552-7ba84100-bfa7-11eb-82bb-29e1dc127daf.png)


rails envを設定しないとdevelopmentで立ち上がってしまうので注意
RAILS_ENV: production
その他はデフォルトの設定でok

### AWS CLIやDockerをインストールしていない場合
ECRのパブリックレポジトリの検索で、「mzmt/rails6_docker_template」と入力するとビルド済みのイメージが使用できます
App Runnerのプロバイダーに「Amazon ECR パブリック」を選択し、以下のURIを入力すると利用可能です
`public.ecr.aws/d5c5w7d9/mzmt/rails6_docker_template:latest`

![Screen Shot 2021-05-28 at 11 22 57](https://user-images.githubusercontent.com/13535662/119920298-12c0c900-bfa7-11eb-93f6-03e583bc624c.png)



## もしデプロイが失敗した場合

デプロイ ログチェック
アプリケーションログチェック
