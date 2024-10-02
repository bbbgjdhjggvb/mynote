#### 创建标签
标签是一个指向commit的指针
```
在想要创建标签的分支
git tag v1.0 #默认在最新的commit创建标签
git tag v2.0 afdd #在指定commit创建标签
git tag v1.0 -m "" #说明信息
```

#### 查看标签
```
git tag #按字母顺序查看标签
git show <tagname> #查看指定标签的信息
```

#### 删除标签
标签创建实在本地不会推送到远程
```
git tag -d <tagname> #
```

#### 推送标签
```
git push mynote v1.0
git push mynote --tags #推送所有标签
```

#### 删除远程标签
1. 删除本地标签`git tag -d xxxx`
2. 删除远程标签`git push mynote :refs/tags/xxxx`