# どんな感じ

![grunt-mocha-power-assert](https://gist.githubusercontent.com/sanemat/d5300f37edb2093ccec1/raw/99152d5044df5aa3f16169557bedfd0c2d0faa33/grunt-mocha-power-assert2.gif)

# yo
```
npm install -g generator-node
yo node
david update # ひとまず最新に
```

# mocha, assert

組み合わさってるのが`nodeunit`なので、まず`mocha`と`assert`に変える。

`grunt`と`mocha`の組み合わせ
- grunt-simple-mocha
- grunt-mocha-test

`simple-mocha`がよさそうだけど、`mocha`のrequireオプションを`power-assert`関連で使いたいので、requireオプション使える`grunt-mocha-test`を使う。

```
npm install grunt-mocha-test --save-dev
```

# power-assert
```
npm install power-assert intelli-espower-loader --save-dev
```

`assert`を`power-assert`に変える。
`grunt-mocha-test` のrequire オプションに`intelli-espower-loader`渡す。

package.jsonに `"directories": { "test": "test/" },`付け足して終わり。

# 参照
## 具体例
[tokyo-amesh-scraper](https://github.com/sanemat/tokyo-amesh-scraper)
## その他
[generator-node](https://github.com/yeoman/generator-node)
[grunt-mocha-test](https://github.com/pghalliday/grunt-mocha-test)
[david](https://github.com/alanshaw/david)
[power-assert](https://github.com/twada/power-assert)
[intelli-espower-loader](https://github.com/azu/intelli-espower-loader)
