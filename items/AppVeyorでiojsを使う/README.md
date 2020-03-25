[Testing with Node.js and io.js - Appveyor](http://www.appveyor.com/docs/lang/nodejs-iojs#selecting-node-js-or-io-js-version)

appveyor.yml

```diff
 # install
 install:                                                                                                               
+- ps: Install-Product node 3                                                                                                               
 - node --version
 - npm --version
 - npm install 
```

nodejsが`0.x`, `1`以降はiojs。次は4から始まるらしいし困らなそう。

[実際の例](https://ci.appveyor.com/project/sanemat/electron-triage-for-github/build/1.0.144)

matrixでやるならこっち
[Testing under multiple versions of Node.js or io.js](http://www.appveyor.com/docs/lang/nodejs-iojs#testing-under-multiple-versions-of-node-js-or-io-js)

`nodejs/nan` のappveyor.ymlを参考にすると良さそう。 
[nodejs/nan appveyor.yml](https://github.com/nodejs/nan/blob/1c725597a3a101da7fc88f27b3cdecf8528df9ab/appveyor.yml)
