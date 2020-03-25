「`docker rm`で起動中のコンテナは削除されない」そうだけど、なんかそれはうってなるので、status exited のコンテナだけ明示して削除したい。

```bash
docker rm $(docker ps -a --filter 'status=exited' -q)
```

[Filter](https://docs.docker.com/reference/commandline/cli/#filtering_2)
引用

```
-f, --filter=[]       Provide filter values. Valid filters:
                      exited=<int> - containers with exit code of <int>
                      status=(restarting|running|paused|exited)
```

```--filter 'exited=1'```と終了コードでフィルターも出来る。
