# tl;dr

Macだんだんいまいちだなーってぐらいの人は諦めて限界までMac使いましょう。

デスクトップLinux環境が好きなひとはがんばってください、頼りにしてます。
限界まで来た、別にデスクトップLinux環境好きではないひとが、Ubuntuをどうにか使うためのtipsです。
なおギョームはmacでやってます。管理の問題もあるし、xcode使うし。

# tips

## システムの文字を大きくする

いまどきのHiDPIなノートパソコンでは文字を大きくしないとつらい。

```
System Settings -> Universal Access -> Seeing -> Large Text -> ON
```

あとはchromeとかatomとかで調整してくれ。

chromeのFont Size をLargeにすると、サイトによってはこんな表示になっちゃうけど、諦めるかuser script詰めるとか頑張って。

![Screenshot from 2016-12-07 19-30-32.png](https://qiita-image-store.s3.amazonaws.com/0/5653/01ff8cd8-5672-90ea-9a4d-03357c9128ef.png)

## ハイバネーション

7年前にデスクトップ環境でFedora 11を使っていたとき、ハイバネーションってほぼ成功しなくてげんなり来てた。
Ubuntu16.04もリリース直後に使い始めて3回に1回ぐらいの体感成功率だったので、こんなもんか−と思っていたが、いまはだいたい4回に3回ぐらい成功している気がする。
閉じたら戻るなんて期待しない。当たり前は通じない。失敗してもめげない。

## google日本語入力

fictx + mozc。学習は違うんだっけ?

## 1password

1passwordからexport, Mac上でKeePassXにimport。Dropboxに突っ込む。
KeePassXのフォーマットにしてからは、あとはUbuntuでも同じ。
UbuntuでDropboxはパッケージがあるので便利。syncして読み込む。
また、AndroidでもKeepass2AndroidとDropsyncを使って共有してる。iosは頑張れ。

## itunes

アキラメロン

## Licecap

アニメーションgifは重要なコミュニュケーション手段なので、Peekというのを使ってる。

![game-with-transactions.gif](https://qiita-image-store.s3.amazonaws.com/0/5653/d584c5e4-5140-b5fe-c742-3d4050e9bf29.gif)

このanimation gifはPeekで作った。ファイルサイズ大きくなったので、http://ezgif.com/optimize これ使ってファイル容量半分にした。このサイトの評価は知らない。

## セキュアブート

Ubuntu使うだけならonで良さそうに思えたけど、virtual boxなど使っていくとoffにせざるをえなくてoff。

## bluetooth


なんかよくわからないけどすぐ切れる。つらい。困ったらリスタート。

```
sudo service bluetooth restart
```

## skype

~~https://web.skype.com/~~

~~ubuntuのパッケージはクソみたいにi386ぶっこんでくるんで、げんなり。
Skype for Web最高!~~

あきらめる。使い物にならない。androidのタブレットをマシンの横に置いて、それで通話してます。

## openvpnを、もらったovpnファイルと使う

```
sudo apt-get install network-manager-openvpn
cd ~/.vpn && sudo openvpn --config your.ovpn
```

`network-manager-openvpn-gnome`パッケージはあるんだけど、よくわからないが2016年11月時点では動かない。ひどい罠。
なのでgnomeはあきらめて、openvpnコマンドで起動する。

会社の情報は家に持ち帰らない(持ち帰れない)ように大体は設計されてるんだけど、外部会場でやるハッカソンにAPI提供するにあたり、デモサーバーにsshするのに必要になって設定した。

「winですか macですか」「ubuntuです」「あー」みたいな

## blu-ray

アキラメロン

## Gimp, Audacity, MySQL Workbench, Idea Ultimate

あたりのどの環境でもあるものでがんばる。

# まとめ

トータルでは苦行なので主義主張のあるやっかいな方、お金や時間に余裕のある方はやるといいと思います!
いやー、Macって使いやすいですね。
