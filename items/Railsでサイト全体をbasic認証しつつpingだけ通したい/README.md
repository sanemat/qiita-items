http_basic_authenticate_with してしまうとskip_before_actionの書き方がわからなかったので。

## 解決例

```rb
http_basic_authenticate_with realm: 'Staging', name: 'user', password: 'password'
```

app/controllers/application_controller.rb

```rb
class ApplicationController < ActionController::Base
  before_action :site_http_basic_authenticate_with if Rails.env.production?

  def site_http_basic_authenticate_with
    authenticate_or_request_with_http_basic("Application") do |name, password|
      name == ENV['MY_SITE_USERNAME'] && password == ENV['MY_SITE_SECRET']
    end
  end
end
```

app/controllers/home_controller.rb

```rb
class HomeController < ApplicationController
  skip_before_action :site_http_basic_authenticate_with, only: [:ping]

  def ping
   render text: 'pong'
  end
end

```

## 失敗例

### skip_before_action http_basic_authenticate_with
`http_basic_authenticate_with` 使いつつ, 外したい側で `skip_before_action :http_basic_authenticate_with`
=> そんな名前のactionはない

### skip_before_action authenticate_or_request_with_http_basic
`http_basic_authenticate_with` 使いつつ, その中身はbefore_actionで`authenticate_or_request_with_http_basic` なので、外したい側で `skip_before_action :authenticate_or_request_with_http_basic`
=> これだとskip対象にならなかった。

### skip_before_action { site_http_basic_authenticate_with }

これだともとのrails側実装にも近いし、仮に(?)basic認証複数になっても平気だし、ヨサげ。

```rb
class ApplicationController < ActionController::Base
  before_action { site_http_basic_authenticate_with(name: ENV['MY_SITE_USERNAME'], password: ENV['MY_SITE_SECRET']) if Rails.env.production?

  def site_http_basic_authenticate_with(options = {})
    authenticate_or_request_with_http_basic(options['realm']||"Application") do |name, password|
      name == options['name'] && password == options['password']
    end
  end
end
```

=> うまくskip指定が書けない。

----
see:
[rails/rails#4-1-stable actionpack/lib/action_controller/metal/http_authentication.rb](https://github.com/rails/rails/blob/3ea18d68f7aed88dba31b5a130ccff25a62a794e/actionpack/lib/action_controller/metal/http_authentication.rb#L69-L90)
