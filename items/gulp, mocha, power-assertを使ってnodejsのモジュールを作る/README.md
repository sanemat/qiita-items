# どんな感じ
![gulp-mocha-power-assert](https://gist.githubusercontent.com/sanemat/d5300f37edb2093ccec1/raw/f0542e5b10ab53f05e59e4669fae856489fe903c/gulp-mocha-power-assert1.gif)

# yo
```
npm install -g generator-node-gulp
yo node-gulp
david update # ひとまず最新に
```

# mocha, assert
組み合わさってるのが`mocha`と`should`なので、`should`を消して`assert`に変える。

```
npm uninstall should --save-dev
```

`gulp-mocha`にはrequireオプション無いが、対策は後述。

# power-assert

```
npm install power-assert intelli-espower-loader --save-dev
```

`assert`を`power-assert`に変える。

`gulp-mocha`はrequireオプションのpull requestが来るたびに、「それはmochaの領分だろ」って[撃ち落としてる](https://github.com/sindresorhus/gulp-mocha/pull/34)。opinionatedだ。Constさんの別の[pull request](https://github.com/sindresorhus/gulp-mocha/pull/12)を見て`gulpfile.js`に`require('intelli-espower-loader');`って書けばよさそうとわかった。

package.jsonに `"directories": { "test": "test/" },`付け足して終わり。

# 参照
## 具体例
[prefecture-jp](https://github.com/sanemat/node-prefecture-jp)
## その他
[generator-node-gulp](https://github.com/stefanbuck/generator-node-gulp)
[gulp-mocha](https://github.com/sindresorhus/gulp-mocha)
[david](https://github.com/alanshaw/david)
[power-assert](https://github.com/twada/power-assert)
[intelli-espower-loader](https://github.com/azu/intelli-espower-loader)
