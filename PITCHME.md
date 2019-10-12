# Node.js 超入門
### ECL 輪読発表
##### 岸本悠希
---
# OUTLINE
### ・クッキーの利用
### ・超簡単掲示板を作ろう
### ・expressを利用しよう
---
* クッキーはwebブラウザに用意されてるもので、サーバーから送られた値を保管しておくための仕組み
* どうやってサーバー間とやりとりしてるの？？ |
  * 実は、「ヘッダー情報」として値をやりとりしている
---
* しかし問題点が、、、
 * クッキーは保管できる値の種類が限られている() |
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
// データ受信終了のイベント処理 
    request.on('end', () => { 
        data = qs.parse(body); 
        setCookie('msg', data.msg, response);//★クッキーの保存
        write_index (request, response); }
     ); 
    } else { 
        write_index (request, response);
    }
```
@[4](クッキーの保存を行っている)
---





