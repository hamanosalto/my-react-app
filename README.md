# はじめに
DockerでReactの環境を構築する手順を以下に示します。この例では、Dockerを使用してReactアプリケーションをセットアップし、
開発環境を整え簡単なTodoアプリケーションの作成をしていきます。

# 必要なソフトウェア

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [React(Windowsの方)](https://qiita.com/techpit-jp/items/984b80a795b7a6f6dd60)
- [React(Macの方)](https://qiita.com/kyosuke5_20/items/c5f68fc9d89b84c0df09)

# プロジェクトのディレクトリ構成
まず、プロジェクトのディレクトリを以下のように構成します。

      my-react-app/

      ├── Dockerfile

      ├── docker-compose.yml

         └── src/

            └── index.js

            └── App.js

    
# Dockerfile の作成

my-react-appディレクトリにDockerfileを作成します。

・ベースイメージとしてnodeを使用

FROM node:14

・作業ディレクトリを設定

WORKDIR /usr/src/app

・package.jsonとpackage-lock.jsonをコピー

COPY package*.json ./

・依存関係をインストール

RUN npm install

・アプリケーションをビルド

RUN npm run build

・アプリケーションを起動

CMD ["npm", "start"]

・ホストとコンテナ間でマウントするポートを指定

EXPOSE 3000

# docker-compose.yml の作成

my-react-appディレクトリにdocker-compose.ymlを作成します。


      version: '3'
   
      services:
   
           web:
     
             build: .
       
             ports:
       
               - "3000:3000"
       
             volumes:
       
               - .:/usr/src/app
         
               - /usr/src/app/node_modules
       
             stdin_open: true
       
             tty: true
       
# package.json の作成

my-react-appディレクトリにpackage.jsonを作成します。Reactプロジェクトを生成するには、以下のコマンドを使用します。

      npx create-react-app my-react-app

このコマンドを実行すると、my-react-appディレクトリに必要なファイルが生成されます。既にcreate-react-appを実行している場合は、package.jsonの内容を確認して、そのまま利用できます。

# React アプリケーションの実行

プロジェクトのディレクトリで以下のコマンドを実行します。

      docker-compose up

このコマンドを実行すると、DockerがReactアプリケーションをビルドし、http://localhost:3000 でアクセスできるようになります。

# セットアップ手順

1. リポジトリをクローンします。

    ```bash
    git clone https://github.com/your-username/my-react-app.git
    cd my-react-app
    ```

2. Docker Composeを使用して、環境を立ち上げます。

    ```bash
    docker-compose up
    ```

3. ブラウザで [http://localhost:3000](http://localhost:3000) にアクセスして、Reactアプリケーションを確認します。

# 使用方法

アプリケーションのコードを編集すると、変更は自動的に反映されます。コンテナはホットリロードをサポートしています。

# ビルドと実行

アプリケーションをビルドして実行するには、以下のコマンドを使用します。

docker-compose up --build

# 停止
アプリケーションを停止するには、以下のコマンドを使用します。

# さいごに
これで開発環境が整いましたので後はソースをダウンロードしていただき動作を確認してみてください。

      docker-compose down
