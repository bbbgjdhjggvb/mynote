#### 初始化仓库
`git init`：做初始化工作，但是没有对文件进行追踪

#### 版本提交
`git add 文件或者文件夹`：
1. 添加追踪文件或者文件夹
2. 将被追踪文件添加到暂存区
3. 合并时把有冲突文件标记为已经解决冲突
`git commit`：提交snapshot
1. `git commit -a`：自动把已经追踪的文件添加到暂存区，并提交
`git status`：查看状态，追踪和未追踪，修改未修改
1. change not staged for commit：被追踪的文件已经发生修改，但没有加入暂存区，`git add`命令添加到暂存区
2. change to be committed：被放在暂存区的文件
3. 暂存的是版本
4. `git status -s`
	1. ??：新添加的未追踪的文件
	2. A：暂存区
	3. M：修改过
	4. 左栏指明暂存区的状态，右栏指明工作区状态
	5. 空M：修改但不在暂存
	6. M：以修改且以暂存
	7. MM：修改后暂存，再修改未暂存

#### 查看提交历史
`git log`
`git log -p -2`
1. -p表示显示差异
2. -2表示最近提交的两次
3. --stat：每次提交的简略统计信息
4. --graph：
5. --pretty =oneline：简化信息
git log --pretty=format:"%h - %an, %ar : %s"
指定输出格式

#### 忽略文件
创建.gitignore文件

#### 查看已暂存和未暂存的修改
`git diff`：不加任何参数，未暂存
`git diff --staged`：以暂存

#### 移除文件
从追踪文件list中移除，并删除文件
`git rm 文件`:删除文件并移除追踪清单
`git rm -f`:删除修改过的，已经放到暂存区的
`git rm --cached`：从移动清单，暂存区中删除，但保留在本地文件中

#### 移动文件
`git mv hello.txt hi.txt`
等价于
```
mv hello.txt hi.txt
git rm hello.txt
git add hi.txt
```


#### 撤销操作
`git commit --amend`：有想要提交的文件上次未提交或者提交信息写错。这个命令会将暂存区的文件提交，并且重写提交信息
`git reset HEAD <file>`：取消暂存文件
1. --hard：重置到指定提交，清除暂存区和实际文件更改
2. --soft：重置到指定提交，保留暂存区和实际文件更改
3. --mixed（默认）：重置到指定提交，取消暂存区，保留实际文件更改。用来撤销commit 
`git checkout --<file>`：取消工作区修改

