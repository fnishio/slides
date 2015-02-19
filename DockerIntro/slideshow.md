author: @f_nishio
title: Docker やってみた

## Docker 1.0

6月9日、Docker 1.0がリリースされました！ \\(^o^)/

![docker logo](./images/docker.png)

## ということで

Dockerを紹介してみよう。ただし...

- **偏った視点**からdockerをオススメします。
- すでに docker をお使いの方に有益な情報は**０**です。
- dockerのホントの**すごさ**はこんなもんじゃありません。たぶん

## こんなとき、どうしてます...?
- **ちょっと** _XXX_ 試してみたいな... (XXX = node.js, nginx, mongodb, postgresql, ...)
- でも、面倒なのは**ちょっと**...

## 苦難の日々
1. MacBook上にインストール
  - 環境を汚したくない ヽ(｀Д´#)ﾉ ﾑｷｰ!!
  - いろいろ試してるうちに、設定変更やライブラリの依存、ぐしゃぐしゃ ヽ(｀Д´#)ﾉ ﾑｷｰ!!
2. VirtualBoxにLinuxインストールしてサーバ立てる
  - VM上なら何でもやり放題! (ﾟдﾟ)ｳﾏｰ
  - VMイメージ、意外にデカイんです ヽ(｀Д´#)ﾉ ﾑｷｰ!!
  - VM起動、時間かかりすぎ ヽ(｀Д´#)ﾉ ﾑｷｰ!!
  - いろいろな環境を仮想環境で用意するのは面倒 ヽ(｀Д´#)ﾉ ﾑｷｰ!!
3. AWS上に環境を作る
  - micro Instance いっぱい作る！ (ﾟдﾟ)ｳﾏｰ
  - AWSにつながらないよ,ここのスタバ... (´･ω･`)ｼｮﾎﾞｰﾝ

## Dockerなら ｳﾏｳﾏ(ﾟ∀ﾟ)
- ホスト環境を汚さない、仮想コンテナ！
- Virtual Machineより軽量, 速い！
- docker hubのofficial imageを使って一瞬で環境構築！
- 一度環境設定してしまえば、元に戻すのは一瞬。いつでもクリーンな環境に戻れる！
- Linuxでつくった環境を簡単にMacに持ち出せる, どこでも動く, Portable !

「**うまい　うますぎる**」

![うま-](./images/umai.jpg)

## About Docker
- コンテナ型仮想化環境　＝　軽量な仮想化環境

![image](./images/Screenshot_from_docker.io_about.png)

## About Docker
- Build, Ship and Run Any App, Anywhere

![docker_cycle](./images/build_ship_run.gif)

## About Docker
- Docker Hub

![](./images/Docker_Hub_Registry_-_Repositories_of_Docker_Images.png)

## About Docker
- Dockerfileで環境設定を自動化、同一構成のコンテナを簡単に作成できる
  - 複数の開発者でサーバ環境を共有
  - 均一のテスト環境, CI
- **Immutable Infrastructure**
  - デプロイメントのたびに新しいインフラを構築し、既存のインフラは不要になった後に廃棄

![](./images/Docker_introduction.png)

## How to Play
- MongoDBを使ってみた
- 環境をcommitしてみた
- Dockerfileで環境構築を自動化してみた

## MongoDBを使ってみた
    $ docker pull mongo
    $ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
    mongo               2.6                 c1639b86dba1        2 weeks ago         1.038 GB
    mongo               2.6.1               c1639b86dba1        2 weeks ago         1.038 GB
    mongo               latest              c1639b86dba1        2 weeks ago         1.038 GB

    $ docker run --name test-mongo -d mongo

    $ docker run -it --link test-mongo:mongo --rm mongo sh -c 'exec mongo "$MONGO_PORT_27017_TCP_ADDR:$MONGO_PORT_27017_TCP_PORT/test"'
    > use testdb;
    switched to db testdb
    > obj1 = { name : "mongo", category : "database" };
    { "name" : "mongo", "category" : "database" }
    > db.Orders.save(obj1);
    WriteResult({ "nInserted" : 1 })
    > obj2 = { name : "mysql", category : "database" };
    { "name" : "mysql", "category" : "database" }
    > db.Orders.save(obj2);
    WriteResult({ "nInserted" : 1 })
    > db.Orders.find();
    { "_id" : ObjectId("53a24ce6919a6e0781c967e7"), "name" : "mongo", "category" : "database" }
    { "_id" : ObjectId("53a24d0c919a6e0781c967e8"), "name" : "mysql", "category" : "database" }

## 環境をcommitしてみた
    $ docker run -i -t ubuntu /bin/bash
    root@3f79adef422d:/# apt-get install iputils-ping
    ...
    root@3f79adef422d:/# exit

    $ docker ps -a
    CONTAINER ID        IMAGE                COMMAND                CREATED             STATUS                     PORTS               NAMES
    3f79adef422d        ubuntu:latest        /bin/bash              6 days ago          Exited (0) 3 seconds ago                       sick_ardinghelli
    $ docker commit 3f79adef422d ping-ubuntu

    $ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
    ping-ubuntu         latest              62c89558e47b        6 days ago          276.5 MB
    ubuntu              latest              ad892dd21d60        2 weeks ago         275.5 MB

    $ docker run -i -t ping-ubuntu /bin/bash
    root@90230eadc1d8:/# ping localhost

## Dockerfileで環境構築を自動化してみた
    $ cat Dockerfile
    FROM node
    ADD . /usr/src/app
    WORKDIR /usr/src/app
    RUN npm install
    EXPOSE 3000
    CMD [ "./bin/www" ]

    $ docker build -t="nishio/node:latest" .
    $ docker images
    nishio/node         latest              2c6feb1e2ab7        3 days ago          1.115 GB
    node                0.10                6a8a9894567d        2 weeks ago         1.112 GB
    node                0.10.28             6a8a9894567d        2 weeks ago         1.112 GB
    node                latest              6a8a9894567d        2 weeks ago         1.112 GB

    $ docker run --name test-node -p 3000:3000 -d nishio/node

## できたらAWSに置くだけ

![](./images/aws_docker.png)

## References

- [Docker](http://www.docker.com/ "Docker")
- [Introduction to Docker](http://www.slideshare.net/dotCloud/docker-intro-november)
- [Be a Happier Developer with Docker](http://www.slideshare.net/dotCloud/be-a-happier-developer-with-docker-tricks-of-the-trade-35851445?ref=http://blog.docker.com/)
