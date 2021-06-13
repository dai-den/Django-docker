## 開発用のコンテナ

Django + PostgreSQL + Redisの構成です.
RedisはDjango Channels用に入れてあります.

PostgreSQLのデータは名前付きボリュームとして保存してあります.
パスは

```Bash
  /var/lib/docker/volumes
```

のような場所にあります.
Macだと直接は覗けないので,適当なイメージ(debian等)にnsenterを入れたコンテナを経由して見てください.

Djangoだと開発までの環境構築の手順は以下のような感じになると思います.

1. Dockerfileを作成する.
2. Dockerfileで読み込むrequirements.txtを作成する.
3. docker-compose.ymlを作成する.最初はDjango, PostgreSQLくらいでも良い.データベースへのログインに関連する情報をenviromentに設定する.
4. startprojectする.myprojectは自分のプロジェクト名に置き換える.
   
```Bash
  docker-compose run web django-admin.py startproject testproject .
```

5. 生成された以下のファイルで,docker-compose内でDjangoのサービスに設定したデータベース関連の環境変数を設定する.デバッグモードと通信を許可するホストも設定しておく.

```
testproject/settings.py
```

6. コンテナを作成する.

```Bash
$ docker compose up
```

7. Djangoのコンテナの中に入ってstartappする.アプリ名をsettings.py内のINSTALLED_APPSに追加する.
8. マイグレートする前にユーザーモデルを変更しておく.CustomUserModelを作成してsettings.pyのAUTH_USER_MODELに入れる.
9. myapp/adminにCustomUserModelを追加して,管理画面に表示する.
10. makemigrationsとmigrateする.