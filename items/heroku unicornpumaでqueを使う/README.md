# Que

TL;DR: Que is a high-performance alternative to DelayedJob or QueueClassic that improves the reliability of your application by protecting your jobs with the same ACID guarantees as the rest of your data.

[chanks/que](https://github.com/chanks/que)

## Motivation

resque, sidekiq便利だけど(あとredisも便利だけど)、herokuで使うのにミドルウェア増やしたくない。redistogo? かと言ってDelayedJobはチョット…
あと、できればworkerで常時1dyno使いたくない。

## How to use

(snip)

## Heroku integration

localhostのwebrickなどで動かしてたそのままだと、puma/unicornで動かない。documentにある通り、`on_worker_boot`や`after_fork`で起動する。

for Puma:

```
# config/puma.rb
on_worker_boot do
  ActiveRecord::Base.establish_connection

  Que.mode = :async
end
```

And for Unicorn:

```
# config/unicorn.rb
after_fork do |server, worker|
  ActiveRecord::Base.establish_connection

  Que.mode = :async
end
```

[advanced_setup](https://github.com/chanks/que/blob/a7df15952b2c7602b20cbcbc764d09560789360c/docs/advanced_setup.md)

これでok.
