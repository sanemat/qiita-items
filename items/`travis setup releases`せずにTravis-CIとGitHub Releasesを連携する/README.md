`travis setup releases`はidとpasswordをいったん入力して、(その後2factor authして)、コマンド内からGitHubのTokenを取りに行く。そんな挙動は気持ち悪いので、自分でブラウザからtoken取得してyamlを書きたい。

ただ、公式ドキュメントが、こうなっているので、secureにする方法がよくわからなかった。

```yaml
deploy:
  api_key: "GITHUB_TOKEN"
```

結論はこうすればいい。secureの部分は`$ travis encrypt -r your_account/your_repos "<github_token>"` こんな感じで。

```yaml
deploy:
  api_key:
    secure: "YOUR_ENCRYPTED_VALUE"
```

環境変数を暗号化して渡すのにしかencrypt使ったことなかったので、FOO=valueにして渡す発想しか無くて、FOO部分を探しまわってしまった。今回は不要だった。

## 手順

[New personal access token](https://github.com/settings/tokens/new) から必要最小限な権限のscopeを選んでTOKENを発行。public repoなら `public_repo`, private repoなら`repo`。

そのtokenをencrypt。

```bash
$ travis encrypt -r your_account/your_repos "<github_token>"
```

あとはyamlに書く。

```yaml
deploy:
  provider: releases
  api_key:
    secure: "YOUR_ENCRYPTED_VALUE"
  file:
  - "package/do-not-merge-wip-for-github.zip"
  on:
    repo: sanemat/do-not-merge-wip-for-github
    tags: true
  skip_cleanup: true
```

おわり。

----
* [GitHub Releases Uploading - Travis CI](http://docs.travis-ci.com/user/deployment/releases/)
* [node-webkitアプリをTravis CI経由でGitHub Releaseにバイナリ登録する | Web Scratch](http://efcl.info/2014/09/05/node-webkit-binary-release/)
* [Travis-CI で Go の Windows 用バイナリを Github release に登録する - Qiita](http://qiita.com/methane/items/f8c5a5f2209739daf44e)
