# railsでER図

## 現状(2014-08-08)の結論
`railroady` v1.1.2　使うのが良さそう。

## ~~現状(2014-08-07)の結論~~
~~github: 'preston/railroady'のmaster指定して使うのが良さそう。~~

## 経緯
`rails-erd`が1.1.0 January 17, 2013 からアップデート無い。githubのmasterもそこで止まってる。
動きそうなforkはGraphsのNetwork見るところ`github: 'devbbq/rails-erd'`これかな(未確認)。
`rails-erd`は`RailRoad`がrails 2.3で動かなくなったあとに主流になったっぽい(未確認)
`RailRoad`のforkの`railroady`がrails 3/4 対応してる。1.1.2 August 8, 2014 リリースしてくれた! ~~ただrailroadyのgemのリリースは1.1.1 July 31, 2013 で止まってる。masterはその後も更新してる。masterだとrails4.1.4, ruby2.1.2, 簡単なmodel/controllerでエラー無く動いた。のでまあこれでいいかか。~~

こんなsvgが`doc/`以下に出る。

![Screen Shot 2014-08-07 at 0.55.29.png](https://qiita-image-store.s3.amazonaws.com/0/5653/0d79318e-8570-d042-8cb9-4b028e26ff3e.png)

![Screen Shot 2014-08-07 at 0.55.44.png](https://qiita-image-store.s3.amazonaws.com/0/5653/dab5c700-11e0-9ed6-51c1-eb731b81c0b1.png)

```text
$ tree doc/
doc/
├── controllers_brief.svg
├── controllers_complete.svg
├── models_brief.svg
└── models_complete.svg
```

もっといいのがありそう。
