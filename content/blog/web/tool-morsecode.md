---
title: "モールス信号の相互変換をJavaScriptで作ってみた"
date: 2020-09-20T03:00:22+09:00
img: tool-morsecode
categories: ["Web"]
tags: ["Tool","WebTopic"]
js: "tool-morsecode"
css: "tool-optimization-en&jp-txt"
---

なぜかずっと作ってみたかったモールス信号と英文の相互変換をJavaScriptで作ってみました。使い場面は全くなさそうなのと、もっと簡単にできるかもだけど一応、コピペ用のコードも載せときます。

{{<ad>}}

## モールス信号と英文の相互変換

<div class=flex>
  <div>
    <h3>英語</h3>
		<textarea id=english onchange="encode(this.value);" onkeydown="encode(this.value);" placeholder="Hello. " autofocus></textarea>
  </div>
  <div>
    <h3>モールス信号</h3>
		<textarea id=morse onchange="decode(this.value);" onkeydown="decode(this.value);" placeholder=".... . .-.. .-.. --- .-.-.- "></textarea>
  </div>
</div>


## 主な仕様

### 1. 英語とモールス信号 どちらを入力しても相互変換されます

`英語→モールス信号` と `モールス信号→英語` の相互変換に対応しています。

### 2. 改行,大文字は無効化

モールス信号の特性上、大文字と改行は反映されません。

### 3. "error：正しい信号を入力してください" と表示される場合

モールス信号が間違っている可能性があります。対応している文字は以下です。

```html
対応文字
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u, v, w, x, y, z, .(ピリオド), ,(カンマ), ?, !, -, /, @, (, )
```

{{<ad>}}

## コード

### エンコード：英語→モールス信号

大文字や改行を全て無効化して、一文字づつモールス信号に置き換えてます。コピペで使えるはず。

```js
let json = {"0": "----- ","1": ".---- ","2": "..--- ","3": "...-- ","4": "....- ","5": "..... ","6": "-.... ","7": "--... ","8": "---.. ","9": "----. ","a": ".- ","b": "-... ","c": "-.-. ","d": "-.. ","e": ". ","f": "..-. ","g": "--. ","h": ".... ","i": ".. ","j": ".--- ","k": "-.- ","l": ".-.. ","m": "-- ","n": "-. ","o": "--- ","p": ".--. ","q": "--.- ","r": ".-. ","s": "... ","t": "- ","u": "..- ","v": "...- ","w": ".-- ","x": "-..- ","y": "-.-- ","z": "--.. ",".": ".-.-.- ",",": "--..-- ","?": "..--.. ","!": "-.-.-- ","-": "-....- ","/": "-..-. ","@": ".--.-. ","(": "-.--. ",")": "-.--.- ","": " ",},out;

function encode(e) {
  out = ""; //変数outリセット

  //大文字,改行を消して一文字ずつ区切って配列化
  e = e.toLowerCase().replace(/[\n\r]/g,"").split("");
  //>"Hello." → ["h","e","l","l","o","."]
  
  //一文字ずつモールス信号へ置き換えて、変数outに加える
  //json[e[i]]は文字が"h"の場合はjson.hのように動作する
  for (let i = 0; i < e.length; i++) {
    out = out + json[e[i]];
  }
  //>["h","e","l","l","o","."] → ".... . .-.. .-.. --- .-.-.- "

  console.out(out);
}

//サンプル
encode("Hello.");
//>".... . .-.. .-.. --- .-.-.- "
```

### デコード：モールス信号→英語

半角スペースでモールス信号を区切って、1つずつ英語に置き換えてます。これもコピペで使えるはず。

```js
let json = {"0": "----- ","1": ".---- ","2": "..--- ","3": "...-- ","4": "....- ","5": "..... ","6": "-.... ","7": "--... ","8": "---.. ","9": "----. ","a": ".- ","b": "-... ","c": "-.-. ","d": "-.. ","e": ". ","f": "..-. ","g": "--. ","h": ".... ","i": ".. ","j": ".--- ","k": "-.- ","l": ".-.. ","m": "-- ","n": "-. ","o": "--- ","p": ".--. ","q": "--.- ","r": ".-. ","s": "... ","t": "- ","u": "..- ","v": "...- ","w": ".-- ","x": "-..- ","y": "-.-- ","z": "--.. ",".": ".-.-.- ",",": "--..-- ","?": "..--.. ","!": "-.-.-- ","-": "-....- ","/": "-..-. ","@": ".--.-. ","(": "-.--. ",")": "-.--.- ","": " ",},out;

// モールス信号 → 英語
function decode(e) {
  out = ""; //変数outリセット
  
  //半角スペースで区切って配列化
  //カッコの中は最後に半角スペースが入ってない時のために最後に半角スペースを追加
  e = (e + " ").split(" ");
  
  //1つずつ英文に置き換えて変数outに加える
  for (let i = 0; i < e.length; i++) {
    let result = Object.keys(json).filter(
      function (k) {
        return json[k] == e[i] + " "
      }
    )[0];
    out = out + result;
  }
  
  //エラー処理
  if (out.includes("undefined")){
    out = "error：正しい信号を入力してください";
  }
  
  console.out(out);
}

//サンプル
decode(".... . .-.. .-.. --- .-.-.-");
//>"hello."
```

***

jsonのvalueからkeyを取得（モールス信号→英語のところ）したことがなくててこずりました。後で忘れないためにブログメモしとこかな。

あと、誕生日を祝っていただき本当にありがとうございます。来年は20歳か...。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">お祝いしてくれた方、<br>ありがとうございます🧚🏻‍♂️ <a href="https://t.co/ugYucojffB">pic.twitter.com/ugYucojffB</a></p>&mdash; 2001Y (@Y20010920T) <a href="https://twitter.com/Y20010920T/status/1307477437266063361?ref_src=twsrc%5Etfw">September 20, 2020</a></blockquote>