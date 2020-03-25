これ cleanしたら、gradle.properties 消える? じゃあだめだこれ

----

`gradle.properties` をgitignoreしたうえで、参照する。

```gradle
// build.gradle
android {
    defaultConfig {
        resValue "string", "google_maps_key", (project.findProperty("GOOGLE_MAPS_API_KEY") ?: "")
    }
```
```gradle
// gradle.properties
GOOGLE_MAPS_API_KEY=AIzaYOURAPIKEY
```

あとは普通にこういうやつで参照できる。

```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="@string/google_maps_key" />
```

## references

Hiding API keys from your Android repository – Code Better – Medium https://medium.com/code-better/hiding-api-keys-from-your-android-repository-b23f5598b906
https://stackoverflow.com/a/51582501/104080
