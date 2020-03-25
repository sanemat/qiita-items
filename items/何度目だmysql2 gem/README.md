homebrewだけど、/usr/localにいれてないので。

```
bundle config --local build.mysql2 "--with-ldflags=-L$(brew --prefix openssl)/lib"
```
