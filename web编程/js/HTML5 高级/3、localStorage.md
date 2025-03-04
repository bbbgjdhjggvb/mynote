### 存储数据
1. 数据必须是字符串类型
```
localStorage.setItem("key", "value");
```

### 读取数据
1. 如果没有读取到数据，返回null
```
const value = localStorage.getItem("key");
```

### 删除数据
```
localStorage.removeItem("key");
```

### 清空所有数据
```
localStorage.
```

### 获取所有key
```
const len = localstorage.length;

for(var i = 0; i < len; i++){
	var key = localStorage.key(i);
}
```