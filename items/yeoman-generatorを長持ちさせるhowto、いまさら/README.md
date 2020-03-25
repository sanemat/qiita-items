# TL;DR

yeoman-generatorはつらい。よいalternative generatorあったら教えてください!! [giter8](https://github.com/foundweekends/giter8)かな。golangだとなおいい。

そんなyeoman-generatorを長持ちさせるhowto。

# yeomanオワコン説

だいたい yeoman-generator はオワコンだし近づきたくないものとして扱われる(要出典)。alternativeとして[slash](https://github.com/slushjs/slush)や[plop](https://github.com/amwmedia/plop)というのが一瞬人気が出たが、オワコンのyeomanより先にしんでいった…

## メンテナンス性

yeoman自体は生きているが、だいたいのyeoman-generatorはしんでいる。
[Discovering Generators](http://yeoman.io/generators/)

あたりまえだが大体のgeneratorは作って動いたところで飽きる。そしてそんなに頻繁には使わない。

使いたい人が自分好みにしたいな、と思った時に、オプションをつける。が、自分好みにしたい人は、自分好みにしたところで飽きるので、継続してメンテするわけではない。

まだ単純な例だけど、[generator-webapp](https://github.com/yeoman/generator-webapp/blob/1cacc60006c247735742eb9ae066304009fbc64b/app/templates/_package.json)こんな感じになる。

```json
{
  "eslintConfig": {
    "env": {<% if (includeBabel) { %>
      "es6": true,<% } %>
      "node": true,
      "browser": true<% if (includeJQuery) { %>,
      "jquery": true<% } %>
    }
  }
}
```

結果if-elseまみれのよくわからないフォーマットのよくわからないファイルができる。つらい。

## 暗黙のルールが負担

templateに`package.json`がそのままの名前で置けない。`_package.json`でおいているgeneratorが多いかな。あと、ドットで始まるファイルをコピーしない、など。`_gitignore` のようにunderscore prefixにして、運ぶときにリネームしているgeneratorが多い。

## 作っている時に動かしたあとの挙動がわかりにくい

linkとかunlinkとかよくわからない。

## 一年ぶりに直そうと思った時にイミフでもう直せない

こんなだった。

```js
var yeoman = require('yeoman-generator');
module.exports = yeoman.Base.extend({
  init: function () {
```

???

```js
const Generator = require('yeoman-generator');
module.exports = class extends Generator {}
```

# 長持ちさせるhowto

上記の逆をやる。

## if-elseで分岐しない

あきらめる。opinionatedでいこう。

## 用途ごとに分ける

よくあるcommand lineありなしみたいなもの。2個も3個もif elseが出てきたら、それはもう別物なので、仕組みを分ける。Sindreさんがそうしているからもう正しい。[node-module-boilerplate](https://github.com/sindresorhus/node-module-boilerplate)内のboilerplateとcli-boilerplate。

(だけど[generator-nm](https://github.com/sindresorhus/generator-nm)側では1個にしてるんだよね、こっちはよくわからない)

## 小さく作る

小さく作って選択肢を減らそう。

## よく使う

よく使え。

## 暗黙のルールはスクリプトにする

最終構成の形で、ファイルを配置する。ルールはファイルを置くときには考えなくていい。コピーするスクリプトでテンプレートにする。

```js
const rimraf = require('rimraf');
const pify = require('pify');
const path = require('path');
const copy = require('copy-concurrently');
const uniqueString = require('unique-string');
const tempDir = require('temp-dir');
const move = require('move-concurrently');
const globby = require('globby');

const getPath = () => path.join(tempDir, uniqueString());
const buildTemplate = (tempDest, copyDest, sourceDir) => {
  return Promise.resolve().then(() => {
    return copy(sourceDir, tempDest);
  }).then(() => {
    console.log(`copied to ${tempDest}`);
    return pify(rimraf)(copyDest);
  }).then(() => {
    console.log(`removed ${copyDest}`);
    return move(path.join(tempDest, 'package.json'), path.join(tempDest, '_package.json'));
  }).then(() => {
    return globby(['.*'], { cwd: tempDest });
  }).then((value) => {
    console.log(value);
    return Promise.all(value.map((dotFile) => {
      return move(path.join(tempDest, dotFile), path.join(tempDest, dotFile.replace(/^./, '__')));
    }));
  }).then(() => {
    return copy(tempDest, copyDest);
  }).then(() => {
    console.log('completed');
  });
};

Promise.resolve().then(() => {
  const tempDest = getPath();
  console.log(tempDest);
  const copyDest = path.join('generator-rustm', 'generators', 'app', 'templates');
  return buildTemplate(tempDest, copyDest, 'boilerplate');
}).then(() => {
  const tempDest = getPath();
  console.log(tempDest);
  const copyDest = path.join('generator-rustmc', 'generators', 'app', 'templates');
  return buildTemplate(tempDest, copyDest, 'cli-boilerplate');
}).catch(err => {
  console.error(err);
});
```
[update.js](https://github.com/pandawing/rust-module-boilerplate/blob/98c531f1390f66d37ab362406d881c04ea39c5b1/update.js)

## run-yo で簡単に実行する

example ディレクトリに出力するようにしておけば便利。

```
$ run-yo --help

  Usage
    run-yo [input (default: example)]

  Examples
    run-yo
    (run the yeoman generator from ./ to ./example/ )
```

## 継続アップデート

[tachikoma](http://tachikoma.io)や[greenkeeper](https://greenkeeper.io/)をどうぞ。

# 完成したもの

https://github.com/pandawing/rust-module-boilerplate/

こちらです。


参照: [scaffold tools | 實松アウトプット](https://sanematsu.wordpress.com/2017/10/21/scaffold-tools/)
