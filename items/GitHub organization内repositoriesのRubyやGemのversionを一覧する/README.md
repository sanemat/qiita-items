# TL;DR

全部`git clone`してきてlocalで`git grep`, `grep`する。

## Shallow clone

shallow clone into ~/tmp/packsaddle20191210

```zsh
mkdir -p ~/tmp/packsaddle20191210
cd ~/tmp/packsaddle20191210
github-repos -org packsaddle -z | xargs -0 -P4 -I {} git clone {} --depth 1
```

[Git clone repositories in a GitHub organization](https://dev.to/sanemat/git-clone-repositories-in-a-github-organization-gh8)
[sanemat/go-githubrepos](https://github.com/sanemat/go-githubrepos)

## Check ruby version

```zsh
for dir in */; do (cd $dir; git grep -n -E "^[ ]{3}ruby 2" -- Gemfile.lock| tr -s '\n' '\0' | xargs -0 -I {} printf "$(basename $(pwd))/{}\n") done
// or
for dir in */; do (cd $dir; grep -nH -E "^[ ]{3}ruby 2.*$" -- Gemfile.lock| tr -s '\n' '\0' | xargs -0 -I {} printf "$(basename $(pwd))/{}\n") done
c
```

### Check gem version

E.g. rails

```zsh
for dir in */; do (cd $dir; git grep -n -E "^[ ]{4}rails " -- Gemfile.lock| tr -s '\n' '\0' | xargs -0 -I {} printf "$(basename $(pwd))/{}\n") done
// or
for dir in */; do (cd $dir; grep -nH -E "^[ ]{4}rails .*$" -- Gemfile.lock| tr -s '\n' '\0' | xargs -0 -I {} printf "$(basename $(pwd))/{}\n") done
```

### For example

the name of repository/the name of file:line number: version

```
ruby-cron_for_github-app/Gemfile.lock:14:    rake (0.9.2.2)
ruby-saddler/Gemfile.lock:24:    rake (13.0.1)
```

いいかんじ。
[Show Ruby/Gem version in repository on GitHub organization](https://dev.to/sanemat/show-ruby-gem-version-in-repository-on-github-organization-1h7d)
