# 授業課題兼サークルのWeb制作
## ことはじめ
フロントとバックどっちも一人で作ります。(初心者)
普段はAndroidのアプリを少しだけかじっている程度。
さて(遠い目)

## Bootstrapテンプレート？
Honoka を使うことに決定。

理由？
日本語 Bootstrap 検索！
一応開発も止まってないみたいだし....

https://github.com/windyakin/Honoka/wiki/Getting%20Started

## sqlとの連携
データベース名とか、パスワード、ユーザIDとかは分けたい。
.envとかに書くことはインターン先のレポジトリを見せていただいた時に知っていた。

調べてもライブラリ？を使うことばかり進めてくる。
[ReaDouble](https://readouble.com/)？使えるものなら使いたいけれど、授業課題なので、制約が。
サーバーに入ってる、入れられるデータ的な都合で。
公開するサーバーにはパッケージを入れるとかできないしね。仕方ないね。

というわけで普通はしないだろうけれど、jsonに書き出すことにします。


http://qiita.com/fantm21/items/603cbabf2e78cb08133e

ファイルを開いてやるとか...?
http://qiita.com/tadsan/items/bbc23ee596d55159f044

## jsonを読み込む
とりあえず、jsonをPHP読み込んでみる。

```
{"env":
    {"database":[
        {
            "name":"simpledb",
            "user":"simpleuser01",
            "pass":"simpleuserpass01"
        }
    ]}
}

```


```
<?php
$url = "env.json";
// $url = "jsondata.json";
$json = file_get_contents($url);
$json = mb_convert_encoding($json, 'UTF8', 'ASCII,JIS,UTF-8,EUC-JP,SJIS-WIN');
$arr = json_decode($json,true);

if ($arr === NULL) {
  print"null";
        return;
}else{
        $json_count = count($arr["env"]["database"]);
        $bc_name = array();
        $bc_user = array();
        $bc_pass = array();
        for($i=$json_count-1;$i>=0;$i--){
            $bc_name[] = $arr["env"]["database"][$i]["name"];
            $bc_user[] = $arr["env"]["database"][$i]["user"];
            $bc_pass[] = $arr["env"]["database"][$i]["pass"];
        }

        print"練習";
        $a = 0;
        while ($a != 3) {
print"
dbname: $bc_name[$a] <br>
dbuser: $bc_user[$a] <br>
dbpass: $bc_pass[$a] <br>
";
            $a++;
        }

}
 ?>

```

できた！


## localのMySQLサーバに接続してみる
MySQLのrunの方法さえ忘れた辛い。

```
$ mysql.server start
Starting MySQL
 SUCCESS!
```
たったこれだけのことを...
https://open-groove.net/mysql/mysql-start-stop/

>>>
runするためには $ mysql.sever start とやるように言われているので、仰せのままにする
止める時は $ mysql.sever stop

昔やってたよねはい。

さて、次はユーザIDとパスワード...


### テスト用MySQLユーザ作成
http://dev.mysql.com/doc/refman/5.6/ja/adding-users.html
http://wiki.minaco.net/index.php?MySQL%2F%E3%83%A6%E3%83%BC%E3%82%B6%E3%81%A8DB%E4%BD%9C%E6%88%90
http://www.dbonline.jp/mysql/user/index1.html


```
CREATE USER user;
CREATE USER user IDENTIFIED BY [PASSWORD] 'password';
```

```
CREATE USER 'ユーザ名'@'localhost' IDENTIFIED BY '一番いいパスワードを頼む';
```

`ERROR 1819 (HY000): Your password does not satisfy the current policy requirements`

追記。

このままではこのユーザ何もできなくないかい。
というわけで、

#### ユーザの権限変更
http://www.dbonline.jp/mysql/user/index5.html

```
mysql> SELECT Host, Database FROM mysql.user;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version
for the right syntax to use near 'FROM mysql.user' at line 1
```
あ、スペースダメなのですか。

```
mysql> SHOW GRANTS FOR 'test'@'localhost';
```

これで確認できました。
```
+------------------------------------------+
| Grants for test@localhost                |

+------------------------------------------+
| GRANT USAGE ON *.* TO 'test'@'localhost' |
+------------------------------------------+
```
`権限なし` とは,,,

権限を変更しましょう。

せっかくなので、スクリプトの練習をしてみます。
addpermission.sql
```
grant select on test.* to 'test'@'localhost';
```

実効は、
`source ./addpermission.sql`

`testdb`のつもりが`test`の権限も与えてしまっていたので、
権限の削除も行います。

http://qiita.com/ritukiii/items/afdc91e68d0cf3e0f383#%E6%A8%A9%E9%99%90%E3%82%92%E5%89%8A%E9%99%A4%E3%81%99%E3%82%8B

```
revoke select on test.* from 'test'@'localhost';
```

### テスト用DB作成
```
mysql> CREATE DATABASE testdb CHARACTER SET utf8;
ERROR 1044 (42000): Access denied for user 'test'@'localhost' to database 'testdb'
```
無碍なり。

rootでログインして再度作成。おk。

### testユーザでログイン
http://mysql.javarou.com/dat/000393.html

テーブルの作成までやりました。
http://www.dbonline.jp/mysql/table/index1.html

create権限を与えていなかったので、rootで再度ログインする必要があった。


## PHPでローカルログインサーバ作るよ
つまりはこの前授業でやってことをローカルでやってみる。
PHPのデータベース関連の情報は env.json に分けておきます。


続く。
