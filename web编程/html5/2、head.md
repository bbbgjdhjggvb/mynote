#### link
1. 显示tab上标签`<link rel="icon" href="相对路径">`
2. 可选源size="32*32"
#### meta
1. 设置显示窗口随移动设备调整窗口：`<meta name="viewport" content="width=device-width, initial-scale=1.0">`
2. 描述关键词，搜索引擎：
```
<meta name="description" content="这是一个介绍网页的描述。">
<meta name="keywords" content="HTML, CSS, JavaScript, Web Development">
name后面的东西提供给搜索引擎
```
3. 刷新网页或者重定向：`<meta http-equiv="refresh" content="30;url=https://example.com">`，指定30秒后刷新并且指定到另外一个网站
4. 禁止浏览器缓存实时刷新
```
<meta http-equiv="cache-control" content="no-cache">
<meta http-equiv="pragma" content="no-cache">
```