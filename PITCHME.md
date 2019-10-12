## Node.js 超入門
#### ECL 輪読発表
##### 岸本悠希
---
## OUTLINE
#### ・クッキーの利用
#### ・超簡単掲示板を作ろう
#### ・expressを利用しよう
---
## クッキーの利用
---
* クッキーはwebブラウザに用意されてるもので、サーバーから送られた値を保管しておくための仕組み
* どうやってサーバー間とやりとりしてるの？？ 
  * 実は、「ヘッダー情報」として値をやりとりしている |
---
* しかし問題点が、、、
 * クッキーは保管できる値の種類が限られている |
---
```js
<body> 
    <head> 
        <h1><%=title %></h1> 
    </head> 
    <div role="main"> 
        <p><%=content %></p> 
        <p><table style="width:400px;"> 
            <tr><th>伝言です! </th></tr> 
            <tr><td><%=data.msg %></td></tr> 
        </table></p> 
        <p>your last message:<%= cookie_data %></p> 
        <form method="post" action="/"> 
        <p>MESSAGE <input type="text" name="msg"> 
        <input type="submit" value="送信 "></p> 
    </div> 
</body>
```
@[11](<%= cookie_data %>というタグを追加して、cookie_dataという値を表示している)
---
```js
// クッキーの値を設定 
function setCookie(key, value, response) { 
    var cookie = escape(value); 
    response.setHeader('Set-Cookie', [key + '=' + cookie]); 
}
```
@[3](エスケープ処理・・・クッキーに保存できる形式に変換する)
@[4](指定のキーに設定して保存する。第二引数は配列['キー=値', 'キー=値'…])
---
```js
function getCookie(key, request) { 
    var cookie_data = request.headers.cookie != undefined ? 
        request.headers.cookie : ''; 
    var data = cookie_data.split(';'); 
    for(var i in data) { 
        if (data[i].trim().startsWith(key + '=')){ 
            var result = data[i].trim().substring(key.length + 1); 
            return unescape(result); 
        } 
    }
    return ''; 
}
```
@[2,3](クッキーの値を取り出す)
@[2,3](三項演算子・・・変数 = 条件 ? trueの値 : falseの値;)
@[4](クッキーを分解する)
@[5,6,7,8,9,10](アンエスケープしてreturn)
---
<img width="700" src="https://user-images.githubusercontent.com/56333428/66698490-81d9a300-ed19-11e9-939a-02120da473c7.png">
---
<img width="400" src="https://user-images.githubusercontent.com/56333428/66698529-c49b7b00-ed19-11e9-9496-b3cfadcf91c9.png">
<img width="400" src="https://user-images.githubusercontent.com/56333428/66698520-b2214180-ed19-11e9-8c11-2946b5a332ab.png">
---
##### まとめ
* クッキーの問題点
 * 保管できる値が限られている |
* クッキーに値を保存する際に、まず行う処理
 * エスケープ処理 |
---
## 超簡単掲示板を作ろう
---
##### 掲示板に必要なもの
* 投稿データをファイルに保存
* 自分のIDをローカルストレージに保管
---
```js
<!DOCTYPE html> 
<html lang="ja"> 
<head> 
    <meta http-equiv="content-type" 
        content="text/html; charset=UTF-8"> 
        <title> ミニ掲示板</title> 
        <link type="text/css" href="./style.css" rel="stylesheet"> 
        <script> 
        function init() { 
            var id = localStorage.getItem('id'); 
            if (id == null){ 
                location.href = './login'; 
            }
        document.querySelector('#id').textContent = 'ID:' + id; 
        document.querySelector('#id_input').value = id; 
    } 
    </script>  
</head> 
```
@[4](クッキーを分解する)
---





