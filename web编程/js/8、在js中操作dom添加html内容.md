### 通过html中的id获得组件
1. `getElementByid`
```js
var p = document.getElementByid("text")
p.textcontent = ""
```
一定不能是
```js
var text = document.getElementByid("text").textcontent;
text = "";
```




### 创建组件并添加到树中
1. `createElement`
2. `appendChild`
```js
var li = document.createElement("li");
unlist.appendChild(li);
```