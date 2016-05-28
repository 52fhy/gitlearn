# Git命令汇总

---

说明：本文是在https://github.com/michaelliao/learngit的基础上进行整理补充的。

### 1. 工作区和版本库
![工作区和版本库](img/01.jpeg)
	
**说明：**

* 工作区（Working Directory）就是创建仓库的文件夹
* 版本库（Repository）就是工作区的隐藏目录`.git`，版本库中有暂存区（stage/index）和分支（master）
* `git add` 实际是把文件添加到暂存区， `git commit` 把暂存区的内容提交到当前分支


### 2.创建版本库

创建git仓库文件夹，名为：`learngit`，并初始化：
```	
$ mkdir learngit
$ cd learngit
$ git init 
```		

### 3. 添加文件
1) 在`leangit`下添加一个`readme.txt`文件，并编辑一些内容
2) 添加到仓库暂存区（）在暂存区 文件会变绿
```	
$ git add readme.txt
```	
3) 提交readme.txt文件到当前分支, `-m`提交说明：
```	
$ git commit -m "add readme.txt"
```
好的习惯是每次都加注释，写明改动的内容。
		
### 4. 修改文件
#### 4.1 当文件在工作区时

1) 查看readme.txt文件内容
```
$ cat readme.txt
```
2) 修改readme.txt文件内容
```
$ vi readme.txt
```
3) 查看仓库状态
```
$ git status
```
4) 添加到仓库暂存区，并提交到当前分支（一般是master）：
```
$ git add readme.txt
$ git commit -m "modify readme.txt"
```

#### 4.2 当文件在暂存区时
修改文件内容，然后提交到分支：
```
$ vi readme.txt
$ git add readme.txt
$ git commit -m "modify readme.txt at the stage"		
```

### 5. 撤销修改文件（未提交到分支）
#### 5.1 当文件在工作区时
执行撤销命令
```
$ git checkout -- readme.txt
```
		
#### 5.2 当文件在暂存区时
1) 令文件回到工作区
```
$ git reset HEAD readme.txt
```
2) 执行撤销命令
```
$ git checkout -- readme.txt
```
		
### 6. 版本回退

说明：在Git中，`HEAD`表示当前版本，`HEAD^`表示上一版本 `HEAD^^`表示上上一个版本

1) 查看提交日志输出(完整版)
```
$ git log
```

2) 查看提交日志输出（精简版）
```
$ git log --pretty=noline
```
	
3) 回到上一版本
```
$ git reset --hard HEAD^
```
		
4) 回到指定版本（hard 后面添加版本号）
```
$ git reset --hard ea34578
```
	
5) 查看命令历史
```
$ git reflog
```		

### 7. 远程仓库（以github为例）
#### 7.1 添加到远程库
1) 在github上创建一个名为`learngit`的空仓库
2) 在本地`learngit`仓库下运行命令添加远程主机
```
$ git remote add origin git@github.com:52fhy/learngit.git
```
其中origin是远程主机名，`git@github.com:52fhy/learngit.git`是主机地址。可以使用`git remote rename <原主机名> <新主机名>`更改主机名。

3) 把本地内容推送到github远程库上(第一次push 参数带 `-u` 关联远程仓库)
```
$ git push -u origin master
```	
关联后下次直接使用`git push`就可以了。当然也可以指定推送到某个远程仓库：
```
git push <远程主机名> <本地分支名>:<远程分支名>
```
如果省略远程分支名，则表示将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。

注意git pull是<远程分支>:<本地分支>。

注意：如果在`git push -u origin` master时出现以下错误，证明电脑没有修改远程仓库的公钥，
```
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

解决方法：
1) 在github上点击`Edit profile` --> `SSH and GPG keys` --> `new SSH key` 添加SHH公钥
2) 打开`id_rsa.pub`文件（/Users/YJC/.ssh/id.rsa.pub）
3) 将`id_rsa.pub`文件内容拷贝到key就可以了，title随便填。

#### 7.2 从远程库克隆
1) 在github上创建一个名为`clonegit`的仓库
2) 使用命令克隆仓库
```
$  git clone git@github.com:52dhy/gitlearn
```
默认主机名是`origin`，可以使用`-o`参数指定主机名：
```
$ git clone -o gitlearn git@github.com:52dhy/gitlearn
```

#### 7.3 从远程仓库更新本地仓库（已关联）
```
$ git pull origin master
```
git pull完整命令格式：
```
 git pull <远程主机名> <远程分支名>:<本地分支名>
```
如果远程分支(例如master)是与当前分支支(例如master)合并，则冒号后面的部分可以省略。

### 8. 分支管理

`master`分支是一条线，git用`master`指向最新的提交，在用`HEAD`指向`master`，以此才确定当前分支，和提交点。

master分支：
![master](img/master.png)

创建分支：
![commitAtNewBranch](img/commitAtNewBranch.png)

新分支的修改和提交：
![newBranch](img/newBranch.png)

分支的合并：
![merge](img/merge.png)

合并完成删除分支：
![masterBranch](img/masterBranch.png)

>分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

>现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

```
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>
强行删除：git branch -D <name>
查看分支合并状况：git log --graph --pretty=oneline --abbrev-commit
```
		
### 9. 藏匿当前未提交的分支

如： 当前在修改自己的分支`dev`,突然项目经理要求修复一个bug-07

解决方法： 

1) 藏匿当前`dev`分支的工作状态
```
$ git stash
```
2) 新建一个`bug-07`分支
```
$ git branch -b bug-07
```
3) 修复bug并提交，合并`bug-07`到`master`分支
```
$ git commit -m "fix the bug-07"
$ git checkout master
$ git merge --no-ff -m "merge  bug-07" bug-07
```
	
4) 删除`bug-07`分支
```
$ git branch -d  bug-07
```
5) 查看当前`stash`
```
$ git stash list
```
6) 恢复`dev`分支的工作状态，并删除stash内容
```
$ git stash pop 
```

### 10. 多人协作

![Git远程操作](img/02.jpg)

#### git clone
克隆一个版本库
```
git clone <版本库的网址>
git clone <版本库的网址> <本地目录名>
```

git clone支持多种协议，除了HTTP(s)以外，还支持SSH、Git、本地文件协议等，下面是一些例子。
```
$ git clone http[s]://example.com/path/to/repo.git/
$ git clone ssh://example.com/path/to/repo.git/
$ git clone git://example.com/path/to/repo.git/
$ git clone /opt/git/project.git 
$ git clone file:///opt/git/project.git
$ git clone ftp[s]://example.com/path/to/repo.git/
$ git clone rsync://example.com/path/to/repo.git/
$ git clone [user]@example.com:path/to/repo.git/
```

#### git remote
管理主机名
```
git remote 列出所有远程主机
git remote -v 参看远程主机的网址
git remote show <主机名> 查看该主机的详细信息
git remote add <主机名> <网址> 添加远程主机
git remote rm <主机名> 删除远程主机
git remote rename <原主机名> <新主机名> 主机改名
```

#### git fetch
取回本地
```
git fetch <远程主机名>
git fetch <远程主机名> <分支名>
```

比如，取回origin主机的master分支。
```
$ git fetch origin master
```


#### git pull
取回远程主机某个分支的更新，再与本地的指定分支合并
```
git pull <远程主机名> <远程分支名>:<本地分支名>
```
如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动"追踪"origin/master分支。
Git也允许手动建立追踪关系。
```
git branch --set-upstream master origin/next
```
上面命令指定master分支追踪origin/next分支。
如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。
```
$ git pull origin
```

如果当前分支只有一个追踪分支，连远程主机名都可以省略。
```
$ git pull
```

#### git push
git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相仿。
```
git push <远程主机名> <本地分支名>:<远程分支名>
```

如果省略远程分支名，则表示将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。
```
$ git push origin master
```

如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。
```
$ git push origin :master

# 等同于
$ git push origin --delete master
```

如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。
```
$ git push origin
```
如果当前分支只有一个追踪分支，那么主机名都可以省略。
```
$ git push
```

如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。
```
$ git push -u origin master
```
上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。

不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。如果要修改这个设置，可以采用git config命令。
```
$ git config --global push.default matching
# 或者
$ git config --global push.default simple
```
还有一种情况，就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用--all选项。
```
$ git push --all origin
```
上面命令表示，将所有本地分支都推送到origin主机。

最后，git push不会推送标签（tag），除非使用--tags选项。
```
$ git push origin --tags
```

### 11. 标签管理
 
* 创建一个标签，默认为`HEAD`当前分支添加标签
``` 
$ git tag v1.0
``` 
* 为版本号为`e8b8ef6`添加`v2.0`标签
``` 
$ git tag v2.0 e8b8ef6
``` 
* 为版本号为`6cb5a9e`添加带有说明的标签，`-a`指定标签名,`-m`指定说明文字
``` 
$ git tag -a v3.0 -m "version 0.2 released" 6cb5a9e
``` 
* 根据标签查看指定分支
``` 
$ git show v0.2
``` 
* 查看所有标签
``` 
$ git tag
``` 
* 删除`v1.0`标签
``` 
$ git tag -d v1.0
``` 
* 把`v0.9`标签推送到远程
``` 
$ git push origin v0.9
``` 
* 推送所有尚未推送到远程的本地标签
``` 
$ git push origin --tags
``` 
* 删除远程标签, 先删除本地标签，再删除远程标签
``` 
$ git tag -d v0.9
$ git push origin :refs/tags/v0.9
``` 

>参考：
Git远程操作详解 - 阮一峰的网络日志
http://www.ruanyifeng.com/blog/2014/06/git_remote.html



