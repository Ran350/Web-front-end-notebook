# 正規表現編

## 正規表現とは

> 文字の組み合わせを照合するためのパターン

JavaScipt では `RegExp オブジェクト`として扱う

---

## いつ使う

- 入力値が正しいフォーマットかをチェックするとき
- 統一のフォーマットに変換するとき
- URL に応じて表示する情報を切り替えるとき
- など

---

## 使い方

1. コンストラクタ記法
   - const regex = new RegExp('[^0-9]', 'g')
   - 第一引数がパターン，第二引数がオプション
2. リテラル記法
   - const regex = /[^0-9]/g
   - `/パターン/オプション`の記法

---

## 正規表現パターン | 特殊文字パターン

特殊文字に何がマッチするか

| 文字   | 意味                           |
| ------ | ------------------------------ |
| ^      | 入力の先頭                     |
| $      | 入力の末尾                     |
| \*     | 直前の０回以上の繰り返し       |
| +      | 直前の１回以上の繰り返し       |
| ?      | 直前の０回か１回               |
| .      | 改行文字以外の１文字           |
| (x)    | ()内に指定した文字             |
| x ｜ y | 指定した文字のどちらか         |
| {n}    | 直前のｎ回の繰り返し           |
| {n,}   | 直前の少なくともｎ回の繰り返し |

```
const regex = pattern => {
    const str = "0123456789";
    const result = str.match(pattern);
    console.log(result[0]);
}

regex(/^[0-9]/) // 0

regex(/[0-9]$/) // 9

regex(/[0-9]*/) // 0123456789
regex(/[0-9]*5/) // 012345

regex(/[0-9]+/) // 0123456789

regex(/[0-9]?/) // 0
regex(/012[0-9]/) // 0123

regex(/[0-9]./) // 01
regex(/012[0-9]./) // 01234

regex(/(012)/) // 012
regex(/(017)/) // error

regex(/(01|56)/) // 01
regex(/(02|56)/) // 56
regex(/(02|57)/) // error

regex(/[0-9]{5}/) // 01234
regex(/[0-9]{5,}/) // 0123456789
regex(/[0-9]{11}/) // error
```

---

## 正規表現パターン | 文字集合パターン

| 文字          | 意味                            |
| ------------- | ------------------------------- |
| /[0-9]/       | 数値（0〜9 のいずれか）         |
| /[a-z]/       | 英小文字（a から z のいずれか） |
| /[A-Z]/       | 英大文字（A から Z のいずれか） |
| /[a-z0-9A-Z]/ | 英数大小文字                    |
| /[^0-9]/      | 数値以外（0〜9 でない）         |

---

## 特殊文字のエスケープ

パターン内でバックスラッシュ`\`を使う
例

```
const pattern = /\/posts\/*/

const pattern = /^[a-zA-Z0-9]*@gmail\.com/
```

---

## JavaScript のマッチングメソッド

### replace() | マッチする文字列を置換

```
const telWithHyphen = '080-1234-5678';
const tel = telWithHyphen.replace(/[^0-9]/g, '');

console.log(tel);
// 08012345678
```

### match() | マッチする文字列を抽出

```
const pattern = /[0-9]{5}/;
const str = "0123456789";
const result = str.match(pattern);

consle.log(result[0]); // 返り値は配列
// 01234
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

## 参考教材

[【とらゼミ】正規表現マスター講義 - YouTube](https://www.youtube.com/watch?v=vncq2vWaGDI&list=PLX8Rsrpnn3IVvcPCZTixO7Pf5lAGoyNOA&index=10)

[JavaScript 正規表現まとめ - Qiita](https://qiita.com/iLLviA/items/b6bf680cd2408edd050f)

[正規表現 - JavaScript - MDN ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_Expressions)
