# HTML 編

## 文書情報

VSCode を使用している場合は，`!`を入力すると補完できる．
[Emmet](https://qiita.com/tedkuma/items/67876e6be3369b0e730c)
という開発者ツールキットの機能．

| タグ  | 意味                                        | よく使われる属性       |
| ----- | ------------------------------------------- | ---------------------- |
| head  | ブラウザや bot に必要な情報を渡すためのタグ |                        |
| meta  | Web サイトの情報を書き込むタグ              | name, content          |
| title | ページタイトル                              |                        |
| link  | 外部のファイルを読み込む                    | href, rel, title, type |

---

## 文書

| タグ    | 意味                                     |
| ------- | ---------------------------------------- |
| body    | ユーザーが見れる文書の情報を書き込む     |
| section | 「章分けされている」とロボット側に伝える |
| div     | 特に意味を持たない                       |
| header  | ページの冒頭にあたる部分で使われる       |
| footer  | 問い合わせ情報などを記載する             |
| h1~h6   | 文章の見出しを表現する                   |
| p       | 文章の段落をひとまとめにする             |

---

## コンテンツ

| タグ | 意味         | よく使われる属性 |
| ---- | ------------ | ---------------- |
| a    | リンクを表す | href             |
| img  | 画像を表す   | src, alt         |

---

## 箇条書き

| タグ | 意味               |
| ---- | ------------------ |
| ul   | 黒ポチの箇条書き   |
| ol   | 番号付きの箇条書き |
| li   | 項目               |

---

## 表

| タグ  | 意味                         |
| ----- | ---------------------------- |
| table | 表を宣言する                 |
| th    | 見出し(一番上の行)を作るタグ |
| tr    | 縦の列を作る                 |
| td    | 横の行を作る                 |

例

```
<table>
            <tr>
                <th>thは表の見出し</th>
                <th>thは表の見出し</th>
            </tr>
            <tr>
                <td>ヨコの行</td>
                <td>ヨコの行</td>
            </tr>
</table>
```

<table>
            <tr>
                <th>thは表の見出し</th>
                <th>thは表の見出し</th>
            </tr>
            <tr>
                <td>ヨコの行</td>
                <td>ヨコの行</td>
            </tr>
</table>

---

## 入力

| タグ   | 意味                                      | よく使われる属性                            |
| ------ | ----------------------------------------- | ------------------------------------------- |
| form   | 入力・送信フォームを作成する              | name, method                                |
| input  | テキストを入力する                        | value, type={text, checkbox, radio, submit} |
| label  | input,textarea,select 要素にラベリング    | for                                         |
| button |                                           | type={reset/submit/button}                  |
| select | メニューの選択肢を作成する                | name                                        |
| option | select タグ内でメニューの選択肢を作成する | value, label                                |

### 参考

- [初心者向け入門】HTML フォーム - Qiita](https://qiita.com/ab-boy_ringo/items/ce0e8b73339d1748e07b)
- [フォームの HTML - Qiita](https://qiita.com/takeshisakuma/items/8198e78e28d346350868)

---

## 空要素

| タグ | 意味             |
| ---- | ---------------- |
| hr   | 水平の横線を引く |
| br   | 改行する         |

---

## 属性

| 属性名 | 意味                                 |
| ------ | ------------------------------------ |
| class  | 要素にスタイルを適用する             |
| style  | スタイル情報を記述する               |
| id     | 固有の識別子を設定する               |
| src    | 埋め込みコンテンツの URL             |
| alt    | 画像が表示できない場合の代替テキスト |

[HTML 属性リファレンス - HTML: HyperText Markup Language | MDN ](https://developer.mozilla.org/ja/docs/Web/HTML/Attributes)
