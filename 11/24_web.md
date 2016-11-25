上下のマージンを入れたい...

phpのログインをする

# hisotry
postでうまく値を渡せていなかった説

気がついて直した
postのnameと一致してなかった

php リダイレクト
http://qiita.com/nenneko/items/ed0c0dadf943651e4f3e

ログイン失敗をlogincheck から getで受け取る

http://webkaru.net/php/php-in-html/
html内でphpスクリプト実行

授業用のサーバーで, \_GET の値がないからエラーが出てた
https://php1st.com/574/
isset関数尊い

**とりあえず、レイアウトだけ作ってしまうか。**

```
<script src="http://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
<script src="../../js/bootstrap.min.js"></script>
```
がなかったから、アニメーションがなかった

# php

## 文字列
連結
```
$string = "11";
$string2 = "22";
$string3 = $string.$string2;

echo "{$string3}";
```

http://www.futomi.com/lecture/macosx/php_dbconnect.html
これを実行した

```
localhost:~ futomi$ sudo cp /etc/php.ini.default /etc/php.ini
localhost:~ futomi$ sudo chmod 644 /etc/php.ini
localhost:~ futomi$ sudo vi /etc/php.ini
```

postgresql+phpの環境構築 (Mac OSX, Marvericks)
http://qiita.com/hanashima/items/e22a0247712e47fe41d0
ここにあるやつ

<img src="https://gyazo.com/72cb6cf7c8ef5a2b2d31a6c6ee6425d7.png">
書き足した

<img src="https://gyazo.com/996a46de4ca0f5e54148caaafae7adaf.png">
sudoしなきゃ

apatcheを再起動

https://yyengine.jp/blog/mac/mac-apache/

```
sudo apachectl restart
```

## まとめ
php で pg_connect() 関数が呼べるように作業をした.

php.ini に `extension=pgsql.so` を書き足した後で,

apachectl をルート権限で再起動した.

以上で, httpからphpのファイルを実行した時, pg_connect()のエラーが出なくなった.

> lolipopではpsql使えなさそうだからmysqlの設定もしなきゃ...

# postgre sql
環境設定
http://qiita.com/_daisuke/items/13996621cf51f835494b
これがいいかも

http://qiita.com/tstomoki/items/0f1a930bd42a8e1fdaac

http://qiita.com/tamano/items/be43de7bb733ad38362c

psqlの環境設定をするか...

# check role
http://www.dbonline.jp/postgresql/role/index1.html

# create user

```
$ createuser -P root
```

```
(dbname)=> \t
Tuples only is on.
(dbname)=> \du
 rild      | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 root      |                                                            | {}
```


```
$ initdb /usr/local/var/postgres -E utf
The files belonging to this database system will be owned by user "rild".
This user must also own the server process.

The database cluster will be initialized with locales
  COLLATE:  C
  CTYPE:    UTF-8
  MESSAGES: C
  MONETARY: C
  NUMERIC:  C
  TIME:     C
initdb: "utf" is not a valid server encoding name
```

# sql
## create table
入ってテーブル作るよ

`mysql testdb -u test -p`

# connect to mysql/postgresql with php
## man
php > mysql_connect
http://php.net/manual/ja/function.mysql-connect.php

# other
`$ apachectl -k graceful`を実行してみた

```
$ apachectl -k graceful
httpd not running, trying to start
(13)Permission denied: AH00072: make_sock: could not bind to address [::]:80
(13)Permission denied: AH00072: make_sock: could not bind to address 0.0.0.0:80
no listening sockets available, shutting down
AH00015: Unable to open logs
```

一瞬 mysql にログインできなくなったけど, パスワードを打ち間違えたかな..?


https://httpd.apache.org/docs/current/ja/stopping.html

publicなディレクトリに `phpinfo.php` を設置する

```
$ cat phpinfo.php
<?php phpinfo(); ?>
```

hostにlocalhostを指定していたら以下のメッセージが出て困った
```
Error:SQLSTATE[HY000] [2002] No such file or directory
```

指定するhostを127.0.0.1にしたら変わった
```
Error:SQLSTATE[42S02]: Base table or view not found: 1146 Table 'testdb.user' doesn't exist
```

いろいろなサイトにlocalhostじゃダメだよと書いてある
http://qiita.com/konatanokonataI/items/337529d6fa3cda287b57

リモートにデータベースのクエリ文公開したらまずいかな...よね

# issue
ブラウザを広げた時にレイアウトが崩れる
