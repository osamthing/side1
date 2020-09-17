# Docker + PostgreSQL + PHP7 + Apache2

DockerでPostgreSQLとPHPを動かす環境を構築します。





```
$ cd /YOUR_DOCKER_DIR/
$ tree
.
├── README.md
├── db
├── docker-compose.yml
├── index.php
└── web
    ├── Dockerfile
    └── php.ini
    
$ docker-compose up -d
Creating network "side1_default" with the default driver
Creating side1_db_1 ... done
Creating side1_web_1 ... done

$ docker ps | grep -e side1_db_1 -e side1_web_1
b23e0c069f88        side1_web                                                                                        "docker-php-entrypoi…"   2 minutes ago       Up 2 minutes        0.0.0.0:8899->80/tcp                       side1_web_1
c6f3cebeb70b        postgres:11-alpine                                                                               "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        0.0.0.0:5433->5432/tcp                     side1_db_1
```



## WEB

http://localhost:8899/

webサーバーのDocumentRootにアクセスする

```
$ docker exec -it side1_web_1 bash
```

中身はDebian10.5になってます。



## Database

設定情報

```
ホスト localhost
ポート 5433
データベース postgres
ユーザ postgres
パスワード password
```

Login

```
$ docker exec -it side1_db_1 psql -U postgres 
```

Dump

```
$ docker exec side1_db_1 pg_dumpall -U postgres > dump.sql
```

Restore

```
$ cat dump.sql | docker exec -i side1_db_1 psql -U postgres
```



## Docker

Dockerの起動

```
hoge
```

Dockerの停止

```
$ docker-compose down
Stopping YOUR_DOCKER_DIR_web_1 ... done
Stopping YOUR_DOCKER_DIR_db_1  ... done
Removing YOUR_DOCKER_DIR_web_1 ... done
Removing YOUR_DOCKER_DIR_db_1  ... done
Removing network YOUR_DOCKER_DIR_default
```



## Docker image

https://hub.docker.com/_/postgres



-------------

https://qiita.com/namizatork/items/dc1e8115fa293ec416b0

https://qiita.com/kurkuru/items/b44653a5fcd1072852c0

https://qiita.com/dyoshikawa/items/c3c4269e02433551278b