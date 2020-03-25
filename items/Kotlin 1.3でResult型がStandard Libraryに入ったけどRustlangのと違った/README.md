Rustlangにかぶれているので、Result型返すぞーとおもったけど、まだその用途ではなかった。

Kotlin 1.3で、Standard LibraryにResult型が入ったみたい。

[Encapsulate successful or failed function execution](https://github.com/Kotlin/KEEP/blob/d464fefd2a13123e91126d0ba87a48b9bab0a44b/proposals/stdlib/result.md#encapsulate-successful-or-failed-function-execution)
[Result type for Kotlin (aka Try monad)](https://youtrack.jetbrains.com/issue/KT-18608)
[Encapsulate successful or failed function execution #127](https://github.com/Kotlin/KEEP/issues/127)

やろうと思ったのはこういうの。

```kotlin
fun numberToVietnamese(num: Int) : Result<String, Box<Error>> {
}
```

return valueでpattern matchingしたいじゃん。

でもone type argumentしか取れないって言うし、one typeにしても、ダメって言われる。

[Limitations](https://github.com/Kotlin/KEEP/blob/d464fefd2a13123e91126d0ba87a48b9bab0a44b/proposals/stdlib/result.md#limitations)

> This Result class cannot be used directly as a return type of Kotlin functions.

この目的のResultではまだないみたい。
