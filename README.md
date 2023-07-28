# scratch3の拡張機能

## Dockerを使ってscratch-guiを利用しよう
1. Dockerfileとdocker-compose.ymlを作成しよう
   - 作業フォルダの中にDockerfileとdocker-compose.ymlを入れよう
     
   - Dockerfile
      ``` Dockerfile
      FROM node:16.18.1-alpine3.16
      
      WORKDIR /usr/src/app
      
      ENV NODE_ENV=development
      
      RUN apk update && apk upgrade
      
      RUN apk add --no-cache bash git openssh curl
      
      RUN apk add --no-cache python3
      
      RUN npm i -g webpack webpack-cli webpack-dev-server
      ```
   - docker-compose.yml
      ``` docker-compose.yml
      version: '3'
      
      services:
        app:
          image: scratch3:16.18.1-alpine3.16
          build: .
          user: "node:node"
          environment:
            NODE_ENV: development
          ports:
            - 8073:8073
            - 8601:8601
          volumes:
            - ./:/usr/src/app
          tty: true
      ```
2. Dockerイメージのビルド
   ``` bash
   $ docker-compose build
   $ docker images
   ```
3. コンテナを起動
   ``` bash
   $ docker-compose up -d
   $ docker-compose exec app bash
   bash-5.0$ whoami
   bash-5.0$ node --version
   bash-5.0$ npm --version
   bash-5.0$ exit
   ```
4. Scratch-guiのインストール
   ``` bash
   $ docker-compose exec app bash
   bash-5.0$ git clone --depth 1 https://github.com/llk/scratch-gui.git
   bash-5.0$ cd scratch-gui
   bash-5.0$ yarn install
   bash-5.0$ yarn start
   ```
   そのあとhttps://localhost:8601に接続するとScratchを起動することができる
   

## 参考資料
- https://deep.tacoskingdom.com/blog/29
- https://twitter.com/ichiroc/status/1630904665637543936
