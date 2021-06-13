## dev
開発時のコンテナ

Django + PostgreSQL + Redis

## prod
運用時のコンテナ

Django + Gunicorn + nginx + PostgreSQL + Redis

## コマンド

### デフォルトの起動
docker-compose.ymlを指定してコンテナを起動するときは,

```Bash
$ docker-compose up
```

### ファイルを指定した起動
docker-compose.yml以外のファイル(docker-compose.prod.yml)などを指定してコンテナを起動するときは,

```Bash
$ docker-compose -f docker-compose.prod.yml up
```

### docker-compose更新後の起動
dokcer-composeを更新した後の起動は

```Bash
$ docker-compose up --build
```

### コンテナの停止,削除
コンテナを全て停止して削除するときは

```Bash
$ docker-compose down
```

このコマンドだと,コンテナとネットワークを削除する.

### コンテナの停止,削除(名前付きボリューム)
名前付きボリュームで永続化したデータを削除するときは

```Bash
$ docker-compose down -v
```
