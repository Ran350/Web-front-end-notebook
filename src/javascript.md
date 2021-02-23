# JavaScript 編

## 変数

### const

再宣言，再代入は禁止．
スコープはブロック`{}`内．

変数はできれば const で宣言するべき．

### let

再宣言禁止，再代入可能．
スコープはブロック`{}`内．

変数を const で宣言できない要件の場合，仕方ないので let で宣言する．

### var

再宣言，再代入が可能．
スコープは関数内．
使ったら負け．

---

## スコープ

- グローバルスコープ
  - プログラム全体のどこからでもアクセス可能
  - 宣言文（const,let,var）を**付けず**に変数宣言するとグローバルスコープに
  - バグの元になりやすい
- ブロックスコープ
  - ブロック`{}`の内側からのみアクセス可能
  - const や let で定義すると実現できる
- 関数スコープ
  - 関数の内側からのみ利用可能
  - var で宣言した変数も関数外からはアクセスできない
  - **即時関数**を利用すると，実現できる！

---

## mutable と immutable

### mutable

宣言後に変更可能な変数の型．
ただし，配列やオブジェクトは const で宣言しても mutable となる．

### immutable

宣言後に変更**不**可能な変数の型．
const で宣言された変数．

バグを防ぐために変数は immutable であるべきと言われている．

---

## アロー関数

従来の関数

```
function funcName( argments ){
    // 処理
}
```

アロー関数

```
const funcName = ( argments ) => {
    // 処理
}

const funcName = ( argments ) => // 1行で書ける処理;
```

---

## 配列メソッド

### map() | 新しい配列をつくる

配列をイテレート（反復） -> 要素 1 つずつに処理 -> 新しい配列をつくる

```
const x = [1,2,3,4];
const result = x.map( x => x*2 );

console.log(result);
// [2,4,6,8]
```

### filter() | 条件に合う要素を抽出

配列をイテレート -> 条件が true の要素のみ返す

```
const obj = [{id:1, text="fuga"},
             {id:2, text="hoge"},
             {id:3, text="piyo"}];

const result = obj.filter( x => {
    return x.text === "hoge"
} );

console.log(result);
// [ {id:2, text:"hoge"} ]
```

### findIndex() | 要素の何番目かを知る

配列をイテレート -> 条件が true の要素が何番目かを返す

```
const obj = [{id:1, text="fuga"},
             {id:2, text="hoge"},
             {id:3, text="piyo"}];

const index = obj.findIndex( x => {
    return x.text === "hoge"
} );

console.log(index, obj[index]);
// 1, {id:2, text:"hoge"}
```

### test() | マッチする文字列か判定

正規表現を使う -> マッチするなら true，しないなら false を返す

```
const regex = RexExp("hoge*");
const x = "hogehoge";
const y = "fugafuga";

console.log( regex.test(x) );   // true
console.log( regex.test(y) );   // false
console.log( /hoge*/.test(x) ); // true
```

---

## DOM

> Document Object Model は、マークアップがなされたリソースをリソース要素の木構造で表現し操作可能にする仕組み、またそのモデルである。
> (Wikipedia より)

JavaScript から HTML へアクセスする窓口．HTML 要素の値の取得や変更ができる-> DOM 操作

---

## DOM 要素の取得

### id で指定

```
document.getElementByID("id名");
```

### class で指定

```
document.getElementsByClassName("class名");
```

### form 要素を取得

```
// HTMLでの記述
// <form name="hoge">
//     <div>
//         <label for="title-id">ラベル</lable>
//         <input id="title-id" name="title" type="text />
//     </div>
// </form>

const x = document.forms.hoge;

// 取得したいinput要素のnameを指定
const y = x.title.value;
```

---

## DOM 要素の書き換え

### innerText

DOM 要素内の**テキスト**を取得，設定できる

```
const = element = document.getElementByID("ID名");
element.innerText = "書き換えました";
```

### innerHTML

DOM 要素内の**HTML**を取得，設定できる

```
// HTMLでの記述
// <div id ="parent">
//     <div>Hello!</div>
// </div>

const element = document.getElementByID("parent");
console.log(element.innerHTML);
// <div>Hello!</div>

const user = "Taro";
element.innerHTML = `<p>Hello ${user}</p>`
console.log(element.innerHTML);
```

### setAttribute

DOM 要素の属性を設定できる

```
// HTMLでの記述
// <div id ="parent">
//     <img id="image" src="before.png">
// </div>

const element = document.getElementById("image");
element.setAttribute('src', "after.png");
```

### insertAdjacentHTML

指定した DOM 要素の相対的な位置に HTML を挿入する

指定できる４つのポジション

1. beforebegin : 自身の直前
2. afterbegin : 子要素の先頭
3. beforeend : 子要素の末尾
4. afterend : 自身の直後

```
// HTMLでの記述
// <ul id ="list">
//     <div>このしたにどんどん追加される</div>
// </ul>

let counter = 1;

const element = document.getElementByID("list");
element.insertAdjacentHTML(
    'beforeend',
    `<li>${couner}つ目の子要素だよ</li>`
);
counter += 1;
```

---

## 非同期処理

### 非同期処理とは

> あるタスクが実行をしている際に、他のタスクが別の処理を実行できる方式である。
> ([日本 OSS 推進フォーラム](http://ossforum.jp/node/753)より)

実行完了を待たない．
並行して次の処理を実行する．

### いつ使う？

通信が発生する処理で起きる

- Web API を叩く
- データベースへクエリを投げる

### 特徴

◎ ユーザを待たせない

- 重い処理や時間のかかる通信中にユーザに別の操作を許可する

× 制御が難しい

- 実行完了までデータが存在しない

### Promise で完了を待つ方法

Promise の状態

- pending: 初期状態
- fulfilled: 処理が成功して完了した状態
- rejected: 処理が失敗して完了した状態

```
const promiseFunc = () => {
    return new Promise((resolve, reject) => {
        someAsynchronousFunc(() => {
            // 何かしらの非同期処理

        }).then(() => {
            // 非同期処理が成功した場合
            return resolve('成功！');

        }).catch(() => {
            // 非同期処理が失敗した場合
            return reject('失敗!');
        })
    })
};
```

### async/await で完了を待つ方法

Promise より async/await がオススメ

- 記述が簡潔になる
- 直感的でわかりやすい

使い方

- 非同期処理を伴う関数定義に async をつける
- 非同期処理を伴う関数実行時に await をつける
- await は async 付き関数内でしか使えない

```
const asyncFunc = async() => {
    const hoge = await someAsynchronousFunc(() => {
        // 何かしらの非同期処理

    }).then(() => {
        // 非同期処理が成功した場合
        return '成功！'

    }).catch(() => {
        // 非同期処理が失敗した場合
        return '失敗!'
    })
}
```

---

## 即時関数

### 保守性を高めるには？

- ファイル分割
- カプセル化

### カプセル化する方法

1. 機能ごとにファイルを分割
2. ファイル内のコードを即時関数でラップ
3. 即時関数内で以下を記述
   - 初期化
   - メソッド

### カプセル化するメリット

- スコープを限定できる
- 擬似的なオブジェクト思考開発
  - 再利用できる
  - 必要なときに呼び出せる

### 関数スコープ(再喝)

- 関数の内側からのみ利用可能
- var で宣言した変数も関数外からはアクセスできない
- **即時関数**を利用すると，実現できる！

### 即時関数によるカプセル化

```
const headerModule = (() => {
    // 初期化処理
    let couner = 0;

    // メソッド化
    return {
        countUp: () => {
            couner += 1;
            console.log("現在のカウントは", counter);
        },
        selectMenu: () => {
            console.log("ヘッダーのメニュー");
        }
    }
})();
```

### Tips: 即時関数で async を使う

```
(async() =>{
    const url = "https://api.github.com/users/Ran350"

    const json = await fetch(url)
        .then(res => {
            return res.json()
        }).catch(error => {
            return null
        });

    console.log(json.login);
})();
```

---

## イベントリスナー

### JavaScript イベント

ユーザによって引き起こされると，関数が実行される．

### イベントを設定する方法

1. HTML 要素に対応したイベント属性

   - 基本的にはこちらを使う
   - 例: \<button onclick="setInnerText("hoge")">テキスト\</button>

2. JavaScript イベントリスナーを設定
   - １つの要素に複数のイベントを設定したいときはこちらを使う
   - addEventListener()を使う

### イベントリスナーの使い方

1. addEventListener()の第一引数に，受け付ける[イベントの種類](https://developer.mozilla.org/en-US/docs/Web/Events)を指定
2. addEventListener()の第二引数に，イベントの処理を記述
   - 発生したイベントの情報を参照するには，[event オブジェクト](https://phpjavascriptroom.com/?t=js&p=event_object)を用いる

```
// HTMLでの記述
// <input id="image" type="file" />

const element = document.getElementById("image");
element.addEventListener('change', event => {
    const file = event.target.files[0];
});
```

### 予期せぬ挙動を防ぐ方法

1. preventDefault()

   - 要素のデフォルトのイベントを無効化

2. stopPropagation()
   - 子要素のイベントが親要素にも伝播することを防ぐ

```
element.addEventListener('cahnge', event => {
    event.preventDefault();
    event.stopPropagation();
});
```

### 参考

[JS イベントまとめ -Qiita](https://qiita.com/hththt/items/aefbcc6eb191588dadff)

---

## 文字列操作

### split()

文字列を指定した区切り文字列で分割する

```
// urlからクエリ文字列を取り出す例
const url = "https://api.github.com/?users=Ran350";
const user = url.split("?users=");

console.log(user);
// ["https://api.github.com/", "Ran350"]
```

### slice()

指定した数値に応じて，文字列の一部分を取り出す

```
const str = "123456789";

console.log(str.slice(2,5)); // 先頭の3文字目〜６文字目
// 345
```

### String.length

文字列の長さを表す分かりすぎて怖い JavaScript 入門

```
const str = "1234567";
console.log(str.length);
// 7
```

### toLocaleString()

数値を言語依存の文字列に変換する

```
const price = 19800;
const localePrice = price.toLocaleString();

consle.log(localePrice);
// 19,800
```

### replace()

パターンにマッチした文字列を置換する

```
// 改行コードを<br>タグに
const str = "Hello!\n Welcome come!";
const result = str.replace(/\r?\n/g, "<br>");

console.log(result);
// Hello!<br> Welcome come!
```

---

## コーディング規約

チームの方針に従う．

### なぜコーディング規約が必要か

- チーム全員が読みやすいコードにするため
- コードレビューの指針とするため
- 開発と運用で人員が変わってもコードの一貫性を保つため

### 変数宣言

- まずは const で宣言することを考える
- 再代入の可能性があるなら let で
- var は非推奨

### 命名規則

- 基本はキャメルケース
  - const variableNamesLikeThis = "hoge";
  - const functionNamesLikeThis = () => {};
- クラス名はアッパーキャメルケース
  - const ClassNamesLikeThis {}
- 定数はスネークケース
  - const SOME_API_KEY = "ABCdefGhIjkLmn";

### 行末のセミコロン

チームで統一するのが良い．
あってもなくてもエラーにならない．
（ちなみに Google 先生はバグ防止のため常にセミコロンを入れている．）

### 関数宣言の方法

どれかに統一するのが良い

- アロー関数
  - ES6 が使える環境なら推奨
  - const funcHoge = () => { /_ 処理 _/ }
- 関数式
  - const funcHoge = function(){ /_ 処理 _/ }
- function 宣言
  - グローバルスコープになっちゃうので非推奨
  - function funcHoge(){ /_ 処理 _/ }

### インデント

[Prettier](https://ics.media/entry/17030/)などのフォーマッタをチームで使用するのが良い．

- スペース 4 つが推奨
- スペース 2 つの環境もある
- タブインデントは非推奨

---

## 参考教材

[【とらゼミ】分かりすぎて怖い JavaScript 入門 - YouTube 再生リスト](https://www.youtube.com/watch?v=EXxIVEC72mU&list=PLX8Rsrpnn3IVvcPCZTixO7Pf5lAGoyNOA)

[【しまぶーの IT 大学】JavaScript 講座 - YouTube 再生リスト](https://www.youtube.com/watch?v=pnsieVYy72M&list=PLwM1-TnN_NN7-zdRV8YsGUB82VVhfYiWW)

[【しまぶーの IT 大学】モダン JavaScript 講座 - YouTube 再生リスト](https://www.youtube.com/watch?v=De9PH3EAz7c&list=PLwM1-TnN_NN4SV6DEs4OtfA51Up6XzTfB)
