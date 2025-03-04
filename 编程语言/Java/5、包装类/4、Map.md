#### Map遍历方法
1. 使用KeySet()方法
	1. 该方法获取所有key,然后通过key取出value
```
Set keyset=map.KeySet()
for(object key:keyset){
	Ssytem.out.println(map.get(key))
}
//使用迭代器
Iterator iterator=keyset.iterator();
while(iterator.hasNext()){
	object key=iterator.next();
	System.out.println(map.get(key));
}
```
2. 使用values()方法
	1. 取出的是value
```
Collection values=map.values();
for(object value:values){
	System.out.println(value);
}
//迭代器
Iterator it=valuse.iterator();
```
3. 使用entrySet()方法
	1. 取出来的对象是entry
	2. 返回的类型是`EntrySet<Map<k,v>>`
```
Set entryset=map.entrySet();
for(object entry:entrySet){
	Map.Entry m=(Map.Entry)entry;
	m.getKey();
	m.getValue();
}
```