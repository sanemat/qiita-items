うっかり`rake relase`出来ないようにする [Ruby - Rake のタスクを消す (プライベートな gem のうっかり rake release を防ぐ) - Qiita](http://qiita.com/kyanny/items/2de40ca0b5127a0f5c2a) という対処の他に。

`RubyGems 2.2.0 and newer` で`allowed_push_host`が使える。exampleはコピペ。

```rb
Gem::Specification.new 'my_gem', '1.0' do |s|
  # ...
  s.metadata['allowed_push_host'] = 'https://gems.my-company.example'
end
```

http://guides.rubygems.org/publishing/#serving-your-own-gems

----

追記(2015-02-12 2:40)
bundler v1.8.0から、`bundle gem foo`で生成する`.gemspec`に`allowed_push_host`の記述入るようになった。こんな。

```rb
if spec.respond_to?(:metadata)
  spec.metadata['allowed_push_host'] = "TODO: Set to 'http://mygemserver.com' to prevent pushes to rubygems.org, or delete to allow pushes to any server."
end
```
