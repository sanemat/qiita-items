csvで変更のあったカラムだけ見分けたいとき。`word-diff-regex`オプションに`"[^,]+"`渡して使う。

```
$ git diff --word-diff-regex="[^,]+" 3f8e0eb...6df01c5 -- x-ken-all.csv
```

<img width="1146" alt="Screen Shot 2016-10-28 at 17.58.18.png" src="https://qiita-image-store.s3.amazonaws.com/0/5653/8689844f-1ef3-a5b8-bf3e-f0fff1ecdbfd.png">

使わないとこう。

<img width="1051" alt="Screen Shot 2016-10-28 at 17.57.56.png" src="https://qiita-image-store.s3.amazonaws.com/0/5653/ef079c4a-5f24-302d-5136-231a740a6b62.png">

見やすーい。
