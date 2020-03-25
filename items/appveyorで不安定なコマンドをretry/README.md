# TL;DR

`appveyor-retry`をつかう。

```
$ appveyor-retry call your-command
```

[Generic wrapper for retry](https://help.appveyor.com/discussions/suggestions/816-generic-wrapper-for-retry)

# なぜ

`npm install`など、ネットワーク由来でコケやすい。travis-ciだと`travis_retry`コマンドがある。[Common Build Problems - Travis CI](https://docs.travis-ci.com/user/common-build-problems/#travis_retry)

# 具体的には

cmdとpowershellでちょっと違うが、つまりこうする。

```yaml
environment:
  matrix:
  - nodejs_version: 8
  - nodejs_version: 9

# install
install:
- cmd: appveyor-retry powershell Install-Product node $env:nodejs_version
- node --version
- npm --version
- appveyor-retry call npm install
```

こんなかんじ。callなしの`appveyor-retry npm install`でいいのだけど、call付きだとpowershellの場合に混乱しなくていい。

```yaml
- ps: Install-Product node $env:nodejs_version
```

powershellはもともとこうしていたらこうする。

```yaml
- cmd: appveyor-retry powershell Install-Product node $env:nodejs_version
```

少しだけ不安定さが減る。
