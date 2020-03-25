# TL;DR

gitやGitHub関連のツールを作っていると、git configの結果をparseしたくなることはよくありますね。

```bash
$ git config --list --null | gitconfig2json | jq
{
  "branch": {
    "chore/foo=bar.baz": {
      "merge": "refs/heads/master",
      "remote": "upstream"
    },
    "master": {
      "merge": "refs/heads/master",
      "remote": "upstream"
    }
  },
  "color": {
    "ui": "auto"
  },
  "core": {
    "bare": "false",
    "editor": "vim",
    "excludesfile": "~/data/src/github.com/sanemat/dotfiles2016/gitignore-system",
    "filemode": "false",
    "logallrefupdates": "true",
    "repositoryformatversion": "0"
  },
  "remote": {
    "upstream": {
      "fetch": "+refs/heads/*:refs/remotes/upstream/*",
      "url": "git@github.com:packsaddle/rust-gitconfig2json_cli.git"
    }
  },
  "url": {
    "git@gist.github.com:": {
      "pushinsteadof": "https://gist.github.com//"
    },
    "git@github.com:": {
      "pushinsteadof": "https://github.com/"
    }
  }
}
```

きれいにparseできました！便利！

- [gitconfig2json_cli](https://crates.io/crates/gitconfig2json_cli)
- [gitconfig2json](https://crates.io/crates/gitconfig2json_cli)
- [gitconfig](https://crates.io/crates/gitconfig2json)

そのあとは[jq コマンドを使う日常のご紹介 - Qiita](https://qiita.com/takeshinoda@github/items/2dec7a72930ec1f658af)などでどうぞ。

# `git config --list --null`

`$ git config --list --null`の結果はこんなです。`\0`が潰れちゃってますが実際の区切りは`\0`です。

```text
core.excludesfile
~/data/src/github.com/sanemat/dotfiles2016/gitignore-system include.path
~/data/src/github.com/sanemat/dotfiles2016/gitconfig ghq.root
~/data/src core.editor
vim color.ui
auto alias.delete-merged-branches
!git branch --merged | grep -v \* | xargs -I % git branch -d % url.git@gist.github.com:.pushinsteadof
https://gist.github.com// url.git@github.com:.pushinsteadof
git://github.com/ url.git@github.com:.pushinsteadof
https://github.com/ alias.permission-reset
!git diff -p | grep -E "^(diff|old mode|new mode)" | sed -e "s/^old/NEW/;s/^new/old/;s/^NEW/new/" | git apply core.repositoryformatversion
0 core.filemode
false core.bare
false core.logallrefupdates
true remote.upstream.url
git@github.com:packsaddle/rust-gitconfig2json_cli.git remote.upstream.fetch
+refs/heads/*:refs/remotes/upstream/* branch.master.remote
upstream branch.master.merge
refs/heads/master branch.chore/foo=bar.baz.remote
upstream branch.chore/foo=bar.baz.merge
refs/heads/master 
```

### `\0`区切りにしないと

`color.ui=auto`こういうのはいいけど、
`branch.chore/foo=bar.baz.merge=refs/heads/master`これがparse不能になる。

## key-valueペア

改行と`\0`区切りでkey-valueペアになる。こんなかんじ。

```
key1\n
value1\0key2\n
value2-1\n
value2-2\0
```
## keyの階層

keyは`key1.key2`や`key1.key2.key3`。

あれ、`url.git@github.com:.pushinsteadof`とか `branch.chore/foo=bar.baz.remote`とかどうすんのまじで。

```bash
$ git config --list --null | gitconfig2json | jq
{
  "branch": {
    "chore/foo=bar.baz": {
      "merge": "refs/heads/master",
      "remote": "upstream"
    },
    "master": {
      "merge": "refs/heads/master",
      "remote": "upstream"
    }
  },
  "color": {
    "ui": "auto"
  },
  "core": {
    "bare": "false",
    "editor": "vim",
    "excludesfile": "~/data/src/github.com/sanemat/dotfiles2016/gitignore-system",
    "filemode": "false",
    "logallrefupdates": "true",
    "repositoryformatversion": "0"
  },
  "remote": {
    "upstream": {
      "fetch": "+refs/heads/*:refs/remotes/upstream/*",
      "url": "git@github.com:packsaddle/rust-gitconfig2json_cli.git"
    }
  },
  "url": {
    "git@gist.github.com:": {
      "pushinsteadof": "https://gist.github.com//"
    },
    "git@github.com:": {
      "pushinsteadof": "https://github.com/"
    }
  }
}
```

うまくparseしてますね。どうして。

どうやら、key1.foo.bar.baz.key3 とあったらfoo.bar.bazがkey2らしいです。ホントかよ。

[Parse git config --list - Stack Overflow](https://stackoverflow.com/questions/47121285/parse-git-config-list)

# おしまい

そんなわけできれいにparseできましたが、ふつーにparseしやすいフォーマットで出力できればいいのにね。どこで言うのがいいんだろう。

- [gitconfig2json_cli](https://crates.io/crates/gitconfig2json_cli)
- [gitconfig2json](https://crates.io/crates/gitconfig2json_cli)
- [gitconfig](https://crates.io/crates/gitconfig2json)
