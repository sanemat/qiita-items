anyenv経由のrbenvだとうまくいかない。あとたぶん、普通のrbenvでもうまくいかない。

# rubyのpath
デフォルトのrbenvのpath `~/.rbenv`
anyenv経由のrbenvのpath `~/.anyenv/envs/rbenv`

## 間違い
RubyMineのrbenvサポートが`~/.rbenv`決め打ちなので、`~/.rbenv` にシンボリックリンク張る
rubyのsdkとしては認識されるけど、たとえばrakeしようとした時に`/usr/bin/ruby`が使われてしまう。使うインタプリタがsystem rubyになる…
[Rbenv Support](http://www.jetbrains.com/ruby/webhelp/rbenv-support.html)

## 正解
(rbenvその他もろもろ設定した上で)mineコマンド作ってシェルから`mine .`などで起動。
[WebStorm - Tools > Run Command… で困らないために - Qiita [キータ]](http://qiita.com/tanakahisateru/items/187b45aad936a78faf1b)

Tools -> Show Gem Environment で意図通りの情報が出てればオッケー!
![Screen Shot 2013-12-04 at 15.04.59.png](https://qiita-image-store.s3.amazonaws.com/0/5653/8823abe9-3951-2126-4aab-0edad2b16916.png)
