### html
```html
<script type = "text/javascript" [src = "hello.js"]>
	js语句;
</script>
```
1. 如果src不为空，那么js语句将会会生效

### js放置的位置
#### 放在head
1. 必须以函数的形式，在body中以标记的形式调用或者用触发器
```html
<head>
	<script type = "text/javascript" [src = "hello.js"]>
		function func(){
			xxxx;
		}
	</script>
</head>
...
<form>
	<input name="xxx" type="button" onclick="func();" value="调用函数">
</form>
```
####  放在body
```html
<body>
	<script type="text/javascript">
		document.write("xxxxx");
	</script>
</body>
```

#### 外部js文件中
```html
<head>
	<script type="text/javascript" src="js/demo.js">
	</script>
</head>
```

#### 事件代码中
```html
<body>
	<form>
		<input type="button" onclick="代码内容" value="xxx">
	</form>
</body>
```