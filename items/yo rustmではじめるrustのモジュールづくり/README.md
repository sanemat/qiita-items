# TL;DR

`yo rustm`で、シュッとrustのモジュールを作り始められる。

```
$ yo rustm
? What do you want to name your module? gitconfig
? What is your module description? My splendid module
? What is your GitHub username? packsaddle
? What is the URL of your website? http://sane.jp
Initialized empty Git repository in /mnt/623D90F735FA5D47/sanemat/data/src/githu
b.com/packsaddle/rust-gitconfig/.git/
   create package.json
   create Cargo.toml
   create changelog.md
   create ci/install.sh
   create ci/script.sh
   create license-apache
   create license-mit
   create readme.md
   create src/lib.rs
   create .appveyor.yml
   create .conventional-changelog.context.js
   create .gitignore
   create .travis.yml
```

[generator-rustm](https://www.npmjs.com/package/generator-rustm)

# cargo newだといろいろ足りない

もちろん謹製のコマンドでcargo newがあり、CLIなら --bin をつけることで、まずほんとの最小限のファイルは作成できる。

```bash
$ cargo new hello_world --bin
# あるいは
$ cargo new hello_world

$ tree hello_world/
hello_world/
├── Cargo.toml
└── src
    └── lib.rs
```

これだけでは [crates](https://crates.io/)にpackageを登録するには、ちょっといろいろ足りないので、yo rustmではじめると便利。

# yo rustmがやること

- ci
- tag打ったらzipでgithub releaseへ
    - windows, linux, mac で使えるバイナリをzip
    - zipには必要十分なファイルだけ入れる
- readme
- travis, appveyor, cratesのbadgeをreadmeに
- changelog
- ライセンス
- cratesへのリリースに コレぐらいはあって欲しい Cargo.toml埋め

ci, zip releaseは[trust](https://github.com/japaric/trust)。changelogは[conventional-changelog](https://github.com/conventional-changelog/conventional-changelog)。

便利ですね。

## 姉妹品 yo rustmc

CLIツール用には、 姉妹品の[generator-rustmc](https://www.npmjs.com/package/generator-rustmc)が便利です。`yo rustmc`。

# インストール

```bash
npm i -g yo generator-rustm
# あるいは
npm i -g yo generator-rustmc
```

nodejsはあるよね。

# tips
## 好きなディレクトリ名をつける

`cargo new`はその名前でディレクトリを作っちゃいます。ディレクトリ名は`rust-your_crate`にしたい若干面倒なひとも`yo rustm`なら安心。

```bash
$ cargo new hello_world
     Created library `hello_world` project
$ tree hello_world/
hello_world/
├── Cargo.toml
└── src
    └── lib.rs

$ mkdir -p rust-your_crate
$ cd rust-your_crate/
$ yo rustm
? What do you want to name your module? your_crate
(snip)
```
