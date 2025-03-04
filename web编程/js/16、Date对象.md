### 创建日期对象
1. `var today = new Date()`：如果直接使用Date创建，返回当前日期
2. 使用特殊格式字符串
```
var d = new Date("12/03/2016 12:00:00");
```

### 常用方法
1. `getDate()`：返回日期中的几号
2. `getDay()`：返回周几，0表示周日，1表示周1，...
3. `getMonth`：11代表12，0代表1
4. `getFullYear()`：返回年份
5. `getHours()`
6. `getMinutes()`
7. `getSecond()`
8. `getTime()`：获取时间戳，指的是从格威治标准时间1970/1/1 0：0：0到目标时间花费的毫秒数
9. `timee = Date.now()`：获取当前时间戳

### 将日期转换为字符串
1. `today.toString()`
2. `date.toLocaleString()`
3. `date.toDateString()`：将日期部分
4. `date.toTimeString()`：将时间部分

### 调整日期和时间
1. `date.setDate(today.getDate() + 5)`
2. `date.setDate(today.FullYear() + 1)`