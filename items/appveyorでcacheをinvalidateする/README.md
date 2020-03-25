Q.appveyorでキャッシュが壊れてエラーから抜けたい！cacheのinvalidateどうするか。
A.ブラウザでコンソール開いて自分でdelete投げる。

> Simplest usage is to use javascript console on appveyor:
>
>```
$.ajax({
    url: 'https://ci.appveyor.com/api/projects/<username>/<project>/buildcache',
    type: 'DELETE'})
```
https://github.com/appveyor/ci/issues/985#issuecomment-279199811

なんでやねん

Updates(2017-11-04 9:50)
google chrome developer toolsのsnippetsでこんなの保存しておくと良い。

```javascript
var targetUrl = new URL(location.href).pathname.split('/');
var purgeApi = 'https://ci.appveyor.com/api/projects/' + targetUrl[2] + '/' + targetUrl[3] + '/buildcache';
$.ajax({
  url: purgeApi,
  type: 'DELETE'});
```
