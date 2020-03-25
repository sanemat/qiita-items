`RUN _command_` だと環境変数足りないのか、 `.bash_profile` が読まれないのか、こんな感じでしのいでるのですが、もっといい方法ないのかなあ

```
RUN git clone https://github.com/riywo/anyenv $HOME/.anyenv
ENV PATH $HOME/.anyenv/bin:$PATH
RUN echo 'eval "$(anyenv init -)"' >> ~/.bash_profile

RUN /bin/bash -l -c 'anyenv install rbenv'

RUN /bin/bash -l -c 'rbenv install 2.1.2'
RUN /bin/bash -l -c 'rbenv global 2.1.2'
RUN /bin/bash -l -c 'gem install bundler'
RUN /bin/bash -l -c 'rbenv rehash'

RUN /bin/bash -l -c 'bundle'
```

[anyenv が入っている Dockerfile 書いた - Qiita](http://qiita.com/python_spameggs/items/e6aec07592a79193fbdd)
[Man page of BASH](http://linuxjm.sourceforge.jp/html/GNU_bash/man1/bash.1.html)
