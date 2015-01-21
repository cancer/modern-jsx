## ExtendScriptをモダンな感じで開発してみた

---

## 自己紹介
![](https://avatars2.githubusercontent.com/u/730940?s=200)  

宇野 陽太([@cancer6](https://twitter.com/cancer6))  

株式会社ピクセルグリッド(2015/1〜)  

AngularJS / Backbone / React.js あたりを触ったり  
CSSの設計したりなど

---

## ExtendScript

---

### What is ExtendScript

http://en.wikipedia.org/wiki/ExtendScript

- レイヤー編集やファイル作成などの操作ができるPhotoshop用のスクリプト(JS)
- Photoshop CSの頃からある
- Photoshopの内部にあるJSエンジンで実行
 - ES3相当 / JSONとかsetTimeoutとか使えない
- `Photoshop Script`とか`Adobe JSX`とかとも呼ばれてる
- ExtendScript ToolkitというIDEがある

---

## Architecture

---

### Architecture

3,4年ぐらい前に作ったものをリファクタリングする

- CoffeeScript
- gulp
 - gulp-coffee
 - gulp-concat(include用)
 - gulp-rename(拡張子`.js`を`.jsx`に直す)
 - (and more)
- Underscore

---

### \#include

- ExtendScriptでは外部ファイルを`\#include`で読み込むことができる

```
#include "lib/underscore.js";
#include "actions/action.js";
#include "module/a.js";
#include "module/b.js";
```

開発中はinclude.jsxとapp.jsxだけconcatし、  
ビルド時に全部結合していました  
(理由は覚えてない...)

---

## Test

---

### テストフレームワーク

- 実行環境がPhotoshop or ExtendScript Toolkit
- レイヤーオブジェクトや独自のファイルオブジェクトなどがある
 - ブラウザやターミナル上で実行するのが難しい

---

### テストダブル

- PhotoshopのエンジンがいつものJSと違う
 - sinon.js使おうとするもsetTimeoutが無くてエラーが出る

---

### なので自分で作る

- ocha.js
 - mocha / jasmine ライクに書けるフレームワーク
- sinobi.js
 - sinon.js ライクに書けるテストダブル

それぞれ最低限のテストが書ける程度に作って  
ExtendScript Toolkitから実行する

---

### 今回はやらなかったけど...

https://github.com/adobe-photoshop/generator-core

- Generatorプラグインにするとよりモダンに
 - Photoshop CCから利用可能
 - Photoshopの中にNode.jsサーバーが組み込まれてる
 - terminalなどからGeneratorCoreを起動することで接続できる

---

### ご清聴ありがとうございました

