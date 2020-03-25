テスト無いペライチのrubyスクリプトも、Travis-CIでrubocopぐらい掛けたい。

```yaml
language: ruby
rvm:
- 2.1
before_install:
- gem install rubocop
script: rubocop --fail-level=W
```

rubocopでwarning出ると終了コードを1にする。

[実例](https://github.com/tachikomaio/twist-hubot/blob/1135455dcaddc212dbea7218798ed72f4806f202/.travis.yml#L1-L6)
