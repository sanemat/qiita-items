切り出したいなってなってから、ハマったので。

- `gradle init` からkotlin library作る
- [Maven Publish Plugin](https://docs.gradle.org/current/userguide/publishing_maven.html) を使い, `./gradlew publishToMavenLocal` で `$HOME/.m2/repository/` 以下にpom, jarをつくる
- `https://bintray.com/USER_NAME/maven/PACKAGE_NAME` にupload
- `maven { url 'https://dl.bintray.com/USER_NAME/maven' }` で取得できる

GitHub repositoryにbuild artifact をcommitしない、の場合、ひとまずこれでよさそう。

<blockquote class="twitter-tweet" data-lang="en"><p lang="ja" dir="ltr">くっそーおれはmethod 1個をlibraryに切り出したいだけなのに なんでみんな親切じゃないんだ ばかにしやがって(被害妄想)</p>&mdash; murahashi kenichi (@sanemat) <a href="https://twitter.com/sanemat/status/1071686452403068928?ref_src=twsrc%5Etfw">December 9, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

いろいろ参考qiita見てたけど結局自分が何を設定しているかわからなくなったので、最小構成、default構成でいく。

gradleがglobalに入っていなければ入れる。[Gradle | Installation](https://gradle.org/install/) でSDKMAN が一番上だったのでSDKMANでgradle 5.0入れた。なんもわからん。(なんだよ`sdk`commandって)

## `gradle init` からkotlin library作る

`gradle init` で kotlin libraryを作っていく。file structureと、gradle wrapper commandなど作ってくれる。

あらかじめ温めておいたmethodを、Libraryの場所に置く。

## [Maven Publish Plugin](https://docs.gradle.org/current/userguide/publishing_maven.html) を使い, `./gradlew publishToMavenLocal` で `$HOME/.m2/repository/` 以下にpom, jarをつくる

```kotlin
// a part of build.gradle.kts
publishing {
    publications {
        create<MavenPublication>("maven") {
            groupId = "jp.sane.numbertovietnamese"
            artifactId = "numbertovietnamese"
            version = "0.2.0"

            from(components["java"])
        }
    }
}
```

`~/.m2/repository` 以下にpomとjarができる。android application側から、ここで

```kotlin
repositories {
    mavenLocal()
}
```

参照できるようになる。android application側が動くぞってなったら次のstep。

## `https://bintray.com/USER_NAME/maven/PACKAGE_NAME` にupload

`~/.m2/repository`に出来たkotlin libraryのjar, pomを`https://bintray.com/USER_NAME/maven/PACKAGE_NAME` にupload

jcenterへはまたあとで。

## `maven { url 'https://dl.bintray.com/USER_NAME/maven' }` で取得できる

```
maven {
    url 'https://dl.bintray.com/USER_NAME/maven'
}
```

ここで、mavenLocalからではなく、publicなところからlibraryを取得できるようになった。

## 依存よくわからない

これでいいんだろうか。`kotlin-stdlib-jdk8` に依存するの??

```
\--- jp.sane.numbertovietnamese:numbertovietnamese:0.2.0
     \--- org.jetbrains.kotlin:kotlin-stdlib-jdk8:1.3.10
          +--- org.jetbrains.kotlin:kotlin-stdlib:1.3.10 (*)
          \--- org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.3.10 (*)
```

## 参照

- [作ったAndroidライブラリを公開する方法 - Qiita](https://qiita.com/gupuru/items/aa81f007d306fc6c4a2c)
- [Androidでaptのライブラリを作るときの高速道路 - Qiita](https://qiita.com/rejasupotaro/items/b9b89f88348222b46708)
- [JavaやGroovy製のライブラリをMavenリポジトリで公開する - Qiita](https://qiita.com/ligun/items/34a570e48d97b68b1608)
- [jCenterでライブラリを公開する方法 - Qiita](https://qiita.com/ryo_mm2d/items/da49cc4677847c20c3fb)
- [カジュアルにライブラリを作っていく話 Android のサンプルと共に - Qiita](https://qiita.com/numa08/items/7df55c55c17d1d246d7f)
