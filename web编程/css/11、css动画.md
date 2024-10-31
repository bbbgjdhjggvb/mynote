#### keyframe 和 animation
```css
.loader{
	animation: myanimation 2s 设置动画效果
}
@keyframes myanimation{
	0%{
		transform:rotate(0deg);
	}
	60%{
		transform:rotate(90%);
	}
	100%{
		transform:rotate(100%);
	}
}
```

#### 设置动画效果
1. infinite：无限循环
2. forwards：保持最终效果
3. ease-in-out：

#### transform属性
1. 旋转
	1. `transform:rotate(xxxdeg)`
2. 平移
	1. `transform:translate(10px, 20px)`右10px,下20px
3. 缩放
	1. `transform:scale(0.98, 0.99)`按x缩放到原来0.98，按y缩放到原来0.99
