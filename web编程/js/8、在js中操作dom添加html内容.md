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

### 获取标签的子标签
```
liElem = ul.querySelector("li");
```

### 带属性的子标签
```js
const maleRadio = document.querySelector('input[type="radio"][value="male"]');
```

### 获取标签的所有子标签
```
liElems = ul.querySelectorAll("li");
```

### 获取标签中的属性的值
如果标签中存在`data-xxx`属性可以通过`li.dataset.xxx`来获得里面的内容
`getAttribute("data-xxx")`来获取这个属性对象。



### 创建组件并添加到树中
1. `createElement`
2. `appendChild`
```js
var li = document.createElement("li");
unlist.appendChild(li);
```

### 通过js让单选框选上
```js
maleRadio.checked = true;
```