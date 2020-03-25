`~/.stack`の場所を移動したい場合、`stack`コマンド実行する前に環境変数`STACK_ROOT`にpathをいれておけばよい。

E.g.

```bash
# .bashrc
export STACK_ROOT="$HOME/data/stack"
```

こんなかんじになる

```bash
$ stack path
Run from outside a project, using implicit global project config
Using resolver: lts-7.0 from implicit global project's config file: /home/sanemat/data/stack/global-project/stack.yaml
stack-root: /home/sanemat/data/stack
project-root: /home/sanemat/data/stack/global-project
(snip)
```


[move .stack - Google Groups](https://groups.google.com/forum/#!topic/haskell-stack/jnZjoSdId5U)
