# TL;DR

crate名はハイフンでつなごう。こんな感じ [hyper-tls](https://crates.io/crates/hyper-tls), [tokio-core](https://crates.io/crates/tokio-core)

依存はこう。ハイフン。

```toml
[dependencies]
hyper-tls = "0.1.2"
tokio-core = "0.1"
```

使うときは、こう。アンダースコア。

```rust
extern crate hyper_tls;
extern crate tokio_core;
```

## rustlangの(かつての)公式ルール

公式ドキュメントでは[RFC 0430](https://github.com/rust-lang/rfcs/blob/8ee535b4fcc8bb22c121ad19a36414f1259397c0/text/0430-finalizing-naming-conventions.md)で

| Item | Convention |
| ---- | ---------- |
| Crates | `snake_case` (but prefer single word) |

こういうルールがあり、`snake_case`で命名するのが正しそうに見える。
ググると出てくるのは、実はRFC 0430を元にした古いドキュメントで、[Naming conventions](https://doc.rust-lang.org/1.0.0/style/style/naming/README.html)、今はない :thinking:

## Steve Klabnik said

> The `-` to `_` thing didn't always exist, so you'll see a lot of earlier projects use `_`. The convention is generally to use `-`.
https://users.rust-lang.org/t/is-it-good-practice-to-call-crates-hello-world-hello-world-or-does-it-not-matter/6114/2

えぇ。。

> That style guide has been entirely removed, check nightly. The reason it was was because its old, not updated, and not accurate.
[Rules and etiquette on Rust crate names (self.rust)](https://www.reddit.com/r/rust/comments/5200kk/rules_and_etiquette_on_rust_crate_names/)

ひえっ

## 一枚岩ではない

rustlang のorganizationメンバーでmozilla所属の人でもアンダースコア区切りで新規crate [state_machine_future](https://crates.io/crates/state_machine_future) 作る人は居るのでもっとわからない。

## crates.io

crates.ioはさらにカオスであり、cargo-editは、なんと間違えると正しい方を追加してくれる。

```
$ cargo add serde-json
WARN: Added `serde_json` instead of `serde-json`

$ cargo add hyper_tls
WARN: Added `hyper-tls` instead of `hyper_tls`

$ cat Cargo.toml
(snip)
[dependencies]
hyper-tls = "0.1.2"
serde_json = "1.0.8"
```

賢いのやら賢くないのやら。

ハイフンとアンダースコアが違うだけのcrateは同名扱い、リネームしようと名前変えpublishしようとしても、それあるから！ってエラーで拒絶される。

## なんだこれ

なんだこれ…と思わなくはない。

形から入るタイプなのでこういうのすごく気になる。[yo rustmではじめるrustのモジュールづくり - Qiita](https://qiita.com/sanemat/items/df73ca01fd56b9efa410)のgenerator-rustmもいろいろ調べた結果、古いドキュメントをあたってしまい初めはcrateをアンダースコアで作ってしまった。今はハイフンになってます。

[私のcrate](https://crates.io/users/sanemat)も、新しく作りかけで名前スクワッティングしているcrate以外アンダースコアなんだなあ。それか無理やり1語にしてる。

:thinking: 
