# scratch3の拡張機能

## Dockerを使ってscratch-guiを利用しよう
1. Dockerを準備しよう
   - Dockerfile
``` Dockerfile
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
   -docker-compose.yml
```docker-compose.yml
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

## 参考資料
- https://deep.tacoskingdom.com/blog/29
- https://twitter.com/ichiroc/status/1630904665637543936
