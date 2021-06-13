## デプロイ用のコンテナのテンプレート

Django + PostgreSQL + Redis + Gunicorn + nginxの構成です.
RedisはDjango Channels用に入れてあります.

基本はdev環境に手を加えていく方針ですが,直接Dockefileやdocker-composeを書けば動きます.

dev環境がある時,

1. requilments.txtにgunicornを追記する.
2. DockerfileをコピーしてDockerfile.prodを作成する.デバッグ関連の環境変数(PYTHONDONTWRITEBYTECODEなど)を設定する.
3. docker-compose.ymlをコピーしてdocker-compose.prod.ymlを作成する.
4. DjangoのサービスでビルドするDockerfileをDockerfile.prodに差し替える.サーバ起動コマンドをguniconのコマンドに変更する.また,環境変数のソースを.envや.env_dbに変更する.
5. nginxフォルダを作成する.nginx用のDockerfileと,nginx.confを作成する.
6. docker-compose.prod.ymlにnginxを追記する.
7. 静的要素をnginx経由で配信するため,settings.pyのSTATIC_URLとSTATIC_ROOTを設定する.
8. entrypoint.shを作成する.(manege.pyのmigrate,collectstaticを行う)
   
以上で起動できる(はず).

1~6でGunicornとnginxを追加し,7,8で静的要素を配信するための設定を行なっています.

docker-compose.prod.ymlを利用してコンテナを立ち上げるときは,

```Bash
$ docker-compose -f docker-compose.prod.yml [command]
```

で起動できます.