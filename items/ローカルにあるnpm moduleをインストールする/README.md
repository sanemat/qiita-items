例えばhubot-scriptsを書くときに、開発中はローカルファイルを読み込みたい。そういうとき下記フォーマットで指定できる。

```bash
npm install <folder>
```

具体的には、`package.json`の`dependencies`に`"hubot-tantanmen": "*"`と書いておいて、

```bash
npm install ../hubot-tantanmen
```

でオッケー。

[npm-install](https://www.npmjs.org/doc/cli/npm-install.html)
