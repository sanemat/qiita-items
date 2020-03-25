# Valentina Studio
PG Commanderがヨサソウ。だけどちょっとお高い。(5800円, 2014-07-21 16:16 5800円のところをセールで3900円、あれ、安い?!)

quoraで評価の高い Valentina StudioでGUIからつないだ。
[PostgreSQL: What is the best free GUI PostgreSQL client for Mac OS X? - Quora](http://www.quora.com/PostgreSQL/What-is-the-best-free-GUI-PostgreSQL-client-for-Mac-OS-X)

## 使い方

```
$ heroku config|grep DATABASE
DATABASE_URL: postgres://username:password@ec2-your-host.compute-1.amazonaws.com:5432/yourdatabase
```

![Screen Shot 2014-07-21 at 16.24.55.png](https://qiita-image-store.s3.amazonaws.com/0/5653/8392b42b-9579-2a7d-cea6-9b36ea22ff47.png)

`Servers` の `Connect to...` からPostgreSQL, Generalを選ぶ。
![Screen Shot 2014-07-21 at 16.27.46.png](https://qiita-image-store.s3.amazonaws.com/0/5653/2bff00fd-cd56-cf3d-2352-c55bdb2b158c.png)

host, username, password, database-name をコピペ。接続するとdatabaseがズラッと並ぶので、自分のデータベースを探す。苦行。

まああとは普通に使える。
![Screen Shot 2014-07-21 at 16.30.17.png](https://qiita-image-store.s3.amazonaws.com/0/5653/6d8ee8f4-1533-a2fd-129d-5e29955a0262.png)

## 感想

Sequel Proがはやくpostgresqlに対応してほしい(来なそう)
[Can't wait till Sequel Pro supports Postgres. Was really excited to see them pu... | Hacker News](https://news.ycombinator.com/item?id=5214420)

## 参照

- [PG Commander, a PostgreSQL client for Mac](https://eggerapps.at/pgcommander/)
- [Valentina Studio - Manager for Valentina, SQLite, mySQL, PostgreSQL](http://www.valentina-db.com/en/valentina-studio-overview)
- [PG Commander](http://qiita.com/fukayatsu/items/0a0befefcf026de80773)
- [【PG Commander】PostgreSQLのGUIツールがシンプルでいい感じでした。 ｜ Developers.IO](http://dev.classmethod.jp/tool/pg-commander/)
- [各種DBのMac用GUIクライアント - komagata](http://docs.komagata.org/5164)
