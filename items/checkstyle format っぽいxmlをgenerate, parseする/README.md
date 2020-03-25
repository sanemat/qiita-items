# checkstyle formatっぽいxml

checkstyle formatっぽいxmlをgenerate, parseする時。

```xml
<?xml version='1.0'?>
<checkstyle>
  <file name='/home/ubuntu/example-circle_ci-pull_request_review/lib/example/circle_ci/pull_request_review.rb'>
    <error line='7' column='120' severity='info' message='Line is too long. [156/120]' source='com.puppycrawl.tools.checkstyle.Metrics/LineLength'/>
  </file>
</checkstyle>
```

だいたいこんなやつ。特にかっちり決まったフォーマットがあるわけではないっぽい(自分調べ)。

[手探りで実装していく様子/ Checkstyle format vigetlabs/grunt-complexity](https://github.com/vigetlabs/grunt-complexity/issues/11)
[実際のcheckstyle format例](https://github.com/pritykovskaya/UniRank/blob/a8074e8fdc3ff9ed0f2e6fc5795b3b4a5c03b0ca/checkstyle_report.xml)
[checkstyleのloggerのtest](https://github.com/checkstyle/checkstyle/blob/master/src/test/java/com/puppycrawl/tools/checkstyle/XMLLoggerTest.java)

## parse

```
XML Declaration
 └── checkstyle element
      └── file element
           └── error element
```

file elementがname attributeを持つ。name attributeがfile path。ここは、フルパス(absolute path)か相対パス(relative path)かは、出力する側依存ぽいので、決め打てない。checkstyle本体はabsolute pathだけど、checkstyleっぽいformatの場合、出力する側依存。

file elementがerror elementを持つ。

error elementはline, column, severity, message, source のattributeを持つ。必ず全attribute持つかというとそうでもないっぽい。source attributeはない互換formatも多い。

lineは1オリジン。
columnは1オリジン。
severityは [ignore, info, warning, error]
http://checkstyle.sourceforge.net/property_types.html#severity


error無しだとこんな出力するものが多い。fileは見たけど、errorは無いよ的に。

```xml
<?xml version='1.0'?>
<checkstyle>
  <file name='/Users/sane/work/tachiko/pigeon.tachikoma.io/Rakefile'/>
</checkstyle>
```

## generate

parseの逆。あとはxmlっぽければよさそう。jenkinsのcheckstyleプラグインに通れば正、通らなければダメ、が一番か。

## 参考実装・調査

jscs, eslintはcheckstyle formatterあり。
rubocopはrubocop-checkstyle_formatter を使う。
いろいろ調べたメモ: [lintとか #tng15](https://gist.github.com/sanemat/5416e4f701922a47773a)
