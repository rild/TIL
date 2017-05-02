ディレクトリ構造
http://tech.pjin.jp/blog/2016/01/27/php-framework-laravel-primer-1/

- [PHPおすすめフレームワーク『Laravel5』入門 Viewの基本](http://tech.pjin.jp/blog/2016/01/28/php-framework-laravel-primer-2/)
だん

> workspace/prac/php-framework/test-project

# ブログ作ってみよう
- [Blogを作ってみよう(意訳)]

```
CREATE TABLE laravel_prac_blog (
     id MEDIUMINT NOT NULL AUTO_INCREMENT,
     title VARCHAR NOT NULL,
     body VARCHAR NOT NULL,
     PRIMARY KEY (id)
);
```
これはうまくいかなかった
どうも、varchar + not null というのがダメっぽい
```
CREATE TABLE laravel_prac_blog (
     id MEDIUMINT NOT NULL AUTO_INCREMENT,
     title CHAR(50),
     body TEXT,
     PRIMARY KEY (id)
);
```
> 参考: http://qiita.com/YujiMiyashita/items/9882ab9f44ee306b3e53

## なんかおかしい
```
$ php artisan make:migration create_articles_table –create=articles
```
どうもこれが変。
めちゃめちゃ激しい赤字で
```

  [Symfony\Component\Console\Exception\RuntimeException]

  Too many arguments, expected arguments "command" "name".
```

と言われる。

> 助けて公式

[あった。](https://readouble.com/laravel/5.3/ja/migrations.html)

> php artisan make:migration create_users_table --create=users

php artisan make:migration create_articles_table --create=articles
一つハイフンが足りてないやん。

```
rilds-MacBook-Pro:test-project rild$ php artisan make:migration create_articles_table –-create=articles


  [Symfony\Component\Console\Exception\RuntimeException]
  Too many arguments, expected arguments "command" "name".



rilds-MacBook-Pro:test-project rild$ php artisan make:migration create_articles_table --create=articles
Created Migration: 2016_12_10_071150_create_articles_table
```
> 一体何が違うんじゃ....

select * from information_schema.tables where table_schema = 'testdb' and table_name = migrations

`php artisan migration` とやった時点で、用意されていた文が実行されるみたい
