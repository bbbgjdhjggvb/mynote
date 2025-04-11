### 加载数据库
```c++
QSqlDatabase db = QSqlDatabase::addDatabase("QMYSQL");        
db.setDatabaseName("test");
db.setHostName("localhost");
db.setUserName("root");
db.setPassword("Pxqf8332657@");

if(db.open()){
    qDebug() << "database open success";
}else{
	qDebug() << "database open fail";
}
```

### 执行语句
```c++
QSqlQuery query;
QString sql = QString("insert into user_id values(%1, '%2','%3')").arg("5").arg("zhangsan").arg("4");
if(query.exec(sql)){
    qDebug() << "insert success";
}else{
    qDebug() << "insert fail";
}

sql = QString("select * from user_id");
query.exec(sql);
while(query.next()){
    qDebug() << query.value(0);
    qDebug() << query.value(1);
    qDebug() << query.value(2);
}
```