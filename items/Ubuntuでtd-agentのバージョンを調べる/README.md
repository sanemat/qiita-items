td-agentのバージョン調べようとしてfluentdのバージョン出てコレじゃねーってなることよくあると思う。

```
$ sudo td-agent --version
td-agent 0.12.26
```

これfluentdのバージョンね。なので、apt-cache policy 使うと、インストール済み、新しいのがあれば新しい候補、などが表示される。これもちろんtd-agentの場合に限らないんだけど、いちばんよく遭遇するのがtd-agentなので。

```
$ sudo apt-cache policy td-agent
td-agent:
  Installed: 2.3.2-0
  Candidate: 2.3.2-0
  Version table:
 *** 2.3.2-0 0
        100 /var/lib/dpkg/status

```
