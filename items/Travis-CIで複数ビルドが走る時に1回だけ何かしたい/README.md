Travis-CIで複数ビルドが走る時に1回だけ何かしたい場合。具体的には、Pull Request契機にbashから何か起動したいがRubyのバージョン複数、データベースも複数、だったりの場合。あまり実行環境に依存しないように書くと変更に強い。

```bash
#!/bin/bash
set -euv
if  [[ "${TRAVIS_JOB_NUMBER: -2}" == ".1" ]]; then
  # you want to do
fi
```

たとえばこれが [Build #19](https://travis-ci.org/packsaddle/ruby-restore_bundled_with/builds/67380365) でJOB NUMBERは`19.1, 19.2, 19.3, 19.4` なので、最後の文字列2文字が`.1`の時だけ実行するようにすれば良い。

正規表現でこんなのにしても良さそうだが試してないのであしからず。

```bash
#!/bin/bash
set -euv
if [[ "${TRAVIS_JOB_NUMBER}" =~ \.1$ ]]; then
  # you want to do
fi
```

----
* [Actual example](https://github.com/packsaddle/ruby-restore_bundled_with/blob/640d66342ab124fdeca96f327af94f82be3f99eb/bin/run-rubocop.sh#L3)
* [bashでの文字列操作 | cobonzuの日記 | スラド](http://srad.jp/~cobonzu/journal/547921/)
