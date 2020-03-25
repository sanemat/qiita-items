# 結論
DockerfileのADDとchownの組み合わせは壊れているので、最後にRUN mvすると直る。
ADDしたいディレクトリやファイルのパーミッションが0700や0600だとなるっぽい。

## ADD nested directory なぜか動かない

rootユーザーだとアクセスできてしまうので、気付きにくい。

```text
# ディレクトリ構成
.
├── Dockerfile
├── parent-dir
│   ├── child-dir
│   │   └── child.txt
│   └── parent.txt
└── reproduce.txt
```

```
# 準備
$ chmod -R go-rwx .
```

```
# Dockerfile
FROM ubuntu:14.04
RUN mkdir -p /code
COPY ./parent-dir /code/parent

# Create user
RUN adduser someuser

RUN chown -R someuser:someuser /code
USER someuser
```

こうすると someuserで/code/parent には触れるが、/code/parent/child-dirには触れない

```
$ cd /code/parent/child-dir
bash: cd: /code/parent/child-dir: Permission denied
```

## 最後に mvするとなぜか動く

```
# Dockerfile
FROM ubuntu:14.04
RUN mkdir -p /temp_dir
COPY ./parent-dir /temp_dir/parent

# Create user
RUN adduser someuser

RUN chown -R someuser:someuser /temp_dir
RUN mv /temp_dir /code

USER someuser
```

```
$ cd /code/parent/child-dir
(works fine)
```

なぜ!

## 環境
```text
host, guestともにUbuntu 14.04

$ docker version
Client version: 1.1.2
Client API version: 1.13
Go version (client): go1.2.1
Git commit (client): d84a070
Server version: 1.1.2
Server API version: 1.13
Go version (server): go1.2.1
Git commit (server): d84a070

$ docker -D info
Containers: 44
Images: 157
Storage Driver: aufs
 Root Dir: /var/lib/docker/aufs
 Dirs: 247
Execution Driver: native-0.2
Kernel Version: 3.13.0-24-generic
Debug mode (server): false
Debug mode (client): true
Fds: 29
Goroutines: 67
EventsListeners: 2
Init Path: /usr/bin/docker
Sockets: [unix:///var/run/docker.sock]
WARNING: No swap limit support

$  uname -a
Linux mouse.tachikoma.io 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
```

----
issue立てたけどうまく伝わる気がしない…
[ADD and COPY does not work correctly with nested directory · Issue #7511 · docker/docker](https://github.com/docker/docker/issues/7511)

[DockerfileでADDとchown/chmodの順序には気をつけよう - Qiita](http://qiita.com/mokemokechicken/items/0ee43407a57e2033da15)
