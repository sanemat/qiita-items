ベトナム語に限らない。Text to Speech `android.speech.tts.TextToSpeech`を使うだけ。音がズレてるけど、実際は再生っぽい記号押したら読み上げてます。

<blockquote class="twitter-tweet" data-lang="en"><p lang="lt" dir="ltr">speech Vietnamese <a href="https://t.co/eMdcmbxXSB">https://t.co/eMdcmbxXSB</a></p>&mdash; murahashi kenichi (@sanemat) <a href="https://twitter.com/sanemat/status/1067809486973284352?ref_src=twsrc%5Etfw">November 28, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

※ Android Studio Emulatorで録画

コードはこんな感じのコピペ。よくわからない。

```kotlin
val vietnamese = "năm"
// android - Unresolved reference inside anonymous Kotlin listener - Stack Overflow
// https://stackoverflow.com/questions/35049850/unresolved-reference-inside-anonymous-kotlin-listener
val textToSpeech = object {
    val value: TextToSpeech get() = inner
    private val inner = TextToSpeech(
        applicationContext,
        {
            value.setLanguage(Locale("vi"))
            value.speak(vietnamese, TextToSpeech.QUEUE_FLUSH,null,null)
        }
    )
}.value
```

ベトナム語の数字を覚えよう。
