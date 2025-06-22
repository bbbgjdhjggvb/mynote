.delete(1,4)：删除1到3（包含3）
.replace(1,3,string)：将1到2替换未string 
.insert(1,string)：在索引为1的字符前面插入string，索引位置可以没有字符
```
String s=null;
StringBuffer sb=new StringBuffer();
sb.append(s);
## sb是"null"
StringBuffer sb1=new StringBuffer(s);
## 底层源码有supper(s.length()+16)，s为空，会抛出空指针异常
```