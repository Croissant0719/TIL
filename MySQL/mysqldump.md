# mysqldump

## basic options

|オプション|意味|説明|
|:-:|:-:|:--|
|-u|ユーザー名(user)|サーバに接続するユーザー名|
|-p|パスワード(password)|パスワードを指定してログイン|
|-h|ホスト名(host)|接続するサーバのホスト名(ex. localhost, 127.0.0.1)指定しないとlocalhostになる|
|-B|データベース(dababase)|複数のデータベースを名前を指定してダンプ|
|-A|すべてのデータベース(all)|複数のデータベースをまとめてダンプ|
|-d|定義のみ(no-data)|定義のみダンプを取りたいときに指定|
|-n|データベースは無視(no-create-db)|データベースを作成せずにダンプ|
|-t|テーブルは無視(no-create-info)|テーブルの作成を行わずにダンプ|

### データベース

$ mysqldump -u USER_NAME -p -h HOST_NAME DB_NAME > OUTPUT_FILE_NAME

### テーブル

$ mysqldump -u USER_NAME -p -h HOST_NAME DB_NAME TABLE_NAME > OUTPUT_FILE_NAME

### テーブルの定義とデータのダンプ

$ mysqldump -u USER_NAME -p -h HOST_NAME -A -n > OUTPUT_FILE_NAME
