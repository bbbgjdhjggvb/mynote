1. 添加分支`git branch newbranch`
2. 查看分支`git branch`
3. 转换分支`git checkout newbranch`
	1. `git chechout`
	2. 创建并转换分支`git checkout -b newbranch`
4. 删除分支`git branch -d oldbranch`
5. 另一种切换分支的方式`git switch newbranch`
	1. `git switch -c newbranch`：创建并切换到新的分支
6. 切换到某一个commit`git switch <commit hash>`
	1. 在切换到以前的commit后`git log`只能查看该commit前的commit。查看所有commit用`git relog`

### 分支合并下的Fast forward模式
1. 触发情况[[Fast forward模式]]
2. 触发后会失去new branch分支
3. 如果不想触发Fast forward模式保留分支使用`git merge --no-ff - m""`
	1. 会保留new branch分支，保留commit，在master创建一个新的stage并自动commit
4. [[--no-ff]]

#### 分支策略
1. master分支是稳定版本，不在上面干活
2. dev是不稳定版本，merge到dev

#### bug分支
当出现bug时，创建类似issue-101的分支来解决bug，但是在的工作还没有commit，因为还没有完成。利用`stach`功能来将当前工作现场存储起来。后面进行恢复
```
git stash
```
然后切换到master分支，新将一个issue-101分支，解决issue，然后合并。
然后切换到dev分支，使用`git stash list`查看工作现场，然后使用`git stash apply`：恢复线程，但是不删除stash中保留的部分，再用`git stash drop`进行删除。两个语句合在一起就是`git stash pop`