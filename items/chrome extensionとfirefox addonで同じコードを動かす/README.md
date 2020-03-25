# TL;DR

- web extensionsで書く
- [Chrome incompatibilities - Mozilla | MDN](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Chrome_incompatibilities) を読む
- [mozilla/webextension-polyfill](https://github.com/mozilla/webextension-polyfill)をつかう
- 細かいところで違うので、mdnとにらめっこする…

## web extensionsとchrome extesionsでちがうところ(記載済み)

### browserとchrome

[mozilla/webextension-polyfill](https://github.com/mozilla/webextension-polyfill) 使ってbrowserにあわせれば良さそう。

### promiseとcallback

[mozilla/webextension-polyfill](https://github.com/mozilla/webextension-polyfill) 使ってpromiseにあわせれば良さそう。

## 違うところ(mdn個別には書いてある)

### page_actionのdefault_iconにchromeはsvg未サポート

https://developer.mozilla.org/en-US/Add-ons/WebExtensions/manifest.json/page_action

### っていうかchrome extensionがsvg iconサポートしてなくね??

> Icons should generally be in PNG format, because PNG has the best support for transparency. They can, however, be in any format supported by WebKit, including BMP, GIF, ICO, and JPEG. 
> https://developer.chrome.com/extensions/manifest/icons

[29683 - Extension icons should support SVG - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=29683) こんなのあるし。ひぇぇ。
