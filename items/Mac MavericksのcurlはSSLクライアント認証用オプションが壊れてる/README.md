壊れているので気をつける。

## SSLクライアント認証の地雷1

Mavericksのcurl v7.30.0 は `-E/--cert` オプションが壊れている。 
[Curl: Important note for curl users on OS X Mavericks 10.9](http://curl.haxx.se/mail/archive-2013-10/0036.html)
[error: SSL certificate problem: Invalid certificate chain while accessing発生時の対応 | iii ThreeTreesLight](http://threetreeslight.com/post/78186114011/error-ssl-certificate-problem-invalid-certificate)

ふええ

```
$ curl -vvv -s -k --key client.key --cert client.crt https://localhost:4242

client sent no required SSL certificate while reading client request headers
```
