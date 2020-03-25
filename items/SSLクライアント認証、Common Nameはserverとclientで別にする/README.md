オレオレ証明書の場合だけかもしれない。
SSLクライアント認証、試してみるのはオレオレ証明書でいいと思うのだが、それでハマった。

## SSLクライアント認証の地雷2

デフォルト設定ママEnter連打していくと、だいたい設定がおなじになる。Common Nameがserverとclientで同じだと、認証で失敗する。「common nameが同じなので、認証失敗しました」というエラーは特に出ない。

Common Nameは分ける。解決はstackoverflowのコメントで見つけたのだけど、permalinkは失念。

なお作成手順。

```bash
# NOTE: Set a different common name between server and client!

# Create the CA Key and Certificate for signing Client Certs
openssl genrsa -des3 -out ca.key 4096
openssl rsa -in ca.key -out ca.key # remove password!
openssl req -new -x509 -days 3650 -key ca.key -out ca.crt

# Create the Server Key, CSR, and Certificate
openssl genrsa -des3 -out server.key 1024
openssl rsa -in server.key -out server.key # remove password!
openssl req -new -key server.key -out server.csr

# We're self signing our own server cert here.  This is a no-no in production.
openssl x509 -req -days 3650 -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt

# Create the Client Key and CSR
openssl genrsa -des3 -out client.key 1024
openssl rsa -in client.key -out client.key # no password!

openssl req -new -key client.key -out client.csr

# Sign the client certificate with our CA cert.  Unlike signing our own server cert, this is what we want to do.
openssl x509 -req -days 3650 -in client.csr -CA ca.crt -CAkey ca.key -set_serial 02 -out client.crt
```

----
see:
[Securing Docker’s Remote API | James Carr](http://blog.james-carr.org/2013/10/30/securing-dockers-remote-api/)
[クライアント証明書 + SSL通信な HTTP サーバのセットアップ - 電卓片手に](http://k-ui.jp/blog/2013/03/13/setup-client-certificate/)
