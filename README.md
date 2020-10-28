# JavaScript の import/export の書き方

## ECMAScript モジュールと CommonJS モジュールの違い
ECMAScript はブラウザレベルの JS 仕様であるのに対して、CommonJS はそれ以外のサーバサイドでの CUI や GUI もカバーする仕様。Node.js も CommonJS の仕様にもとづいて実装されている。

## ECMAScript の import/export
名前付きとデフォルトがある。

### 名前付き import/export
変数を1個 export する。
```javascript
const foo = 'foo'
export { foo }
```

関数も同じようにいける。export を宣言の前に付けると、宣言と同時に export まで一括でできる。
```javascript
export function hoge() {
    // body
}
```

エクスポート、インポートを対応付けるとこうなる。
```javascript
export const foo
export function bar() {
    // body
}
```

```javascript
import { foo, bar } from './sample_modules.js'
```

### 1モジュール1ファイル
1つのモジュールは基本的に1つのファイルに対応させる。

どのファイルから読み込むのかの指定は from 句の後に書く。

「名前付き」とはいうが、自分で名前を付けるというのではなく、export したい関数や変数の名前を使うことになる。

ただし、「名前付き」import/export には、エイリアス機能が使えるので、これを使って明示的にモジュール名を変更した場合にはこの限りではない。

つまり自分で名前を付けることもできる。

```javascript
const internalFoo = 'foo'
export { internalFoo as foo }
```

```javascript
import { foo as myFoo } from './named-export-alias.js'
console.log(myFoo)  // -> foo
```

エイリアスは import/export の両面から使うことができる。

## デフォルト import/export
デフォルトエクスポートは、モジュールごとに1つしかエクスポートできない特殊なエクスポート方法である。

```javascript
const foo = 'foo'
export default foo
```

```javascript
export default function() {
    // body
}
```

import するには import する側で名前を付けてやる必要がある。
```javascript
export default {
    baz: 'baz'
}
```
```javascript
import myModule from './my-module.js'
console.log(myModule)  // { baz: 'baz' }
```

export する側は「デフォルト」なので特に名前を付けたりはしない。

import する側はデフォルトエクスポートを読み込んだとしても、それをファイル内で使うことになるので、参照できるように何らかの名前を付ける必要がある。

## CommonJS の import/export
### export
module.exports の後に続けて export したい関数やクラスを定義する。
```javascript
module.exports = hoge() {
    console.log('This is the export style of CommonJS.')
}
```

### import 
require の後に読み込みたいモジュールがあるファイルのパスを指定する。

その戻り値を変数に代入し、import したファイルの中ではその変数名を使って参照する。
```javascript
const hogeModule = require('./hoge.js')
hogeModule()
```
