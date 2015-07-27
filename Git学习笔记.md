# Git学习笔记

标签： git

---

内容概要
>1. 第一次使用github
2. 再次使用git
3. 从远程更新至本地版本库
4. 写在后面

##1. 第一次使用github

1) github注册账号,网址：https://github.com/
使用邮箱注册账号。

注意先不要创建版本库。


2) 安装git

Linux请参考网上教程，这里演示windows操作。

实际命令行操作基本是一样的。


 msysgit 是Windows版的Git，从http://msysgit.github.io/下载，然后按默认选项安装即可。

官方下载比较慢，可以使用第三方下载点：[msysgit_1.9.4.0_XiaZaiBa.zip](http://xiazai.xiazaiba.com/Soft/M/msysgit_1.9.4.0_XiaZaiBa.zip)

安装完成后，在开始菜单里找到"Git"->"Git Bash"，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

说明：git命令操作和Linux命令差不多，很多命令可以直接使用,比如cd,vi
 

3) 安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

4) 创建SSH Key

在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

会让你输入 `.ssh/id_rsa` 文件的路径,默认即可
然后输入新密码，确认即可。

 
5) 登陆GitHub，打开`Account settings`，`SSH Keys`页面：
然后，点"Add SSH Key"，填上任意Title，在Key文本框里粘贴 `id_rsa.pub` 文件的内容：

>为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。
 

6) 创建本地版本库(我选的D盘)
```
$ cd /d/phpsetup/www/git/
$ mkdir fhyblog
$ cd fhyblog
$ pwd

/d/phpsetup/www/git/fhyblog
```

7) 通过 git init 命令把这个目录变成Git可以管理的仓库：
```
$ git init

Initialized empty Git repository in /Users/52fhy/fhyblog/.git/
```
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个 .git 的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

 

8) 在本地版本库fhyblog里放入一些代码或文件

　　我放了src目录和一个readme.txt文件

9) 进入版本库目录：
```
$ cd /d/phpsetup/www/git/fhyblog/
``` 

10) 更新本地版本库(.指当前所有目录及文件)
```
$ git add .
```
当然,如果你仅仅是提交一个文件,可以这样写
```
$ git add readme.txt
```
更新一个目录这样写：
```
$ git add src/
```
此时还没有真正提交到版本库,只是放在暂存区。提交请继续往下看：


11) 执行更新操作：
```
$ git commit -m "相关说明"

[master 91115af] .
1 file changed, 53 insertions(+)
create mode 100644 "\345\215\207\347\272\247\346\227\245\345\277\227.txt"
```

12) 更新至远程(Github):

要关联一个远程库，使用命令 
```
$ git remote add origin git@github.com:yourname/yourgit.git 
```
关联后，使用命令 
```
git push -u origin master
```
进行第一次推送master分支的所有内容；

所以，远程github上确保你的版本库是空的，否则你在这一步可能会不成功。

此后，每次本地提交后，只要有必要，就可以使用命令 `git push origin master` 推送最新修改；

```
$ git push origin master

Warning: Permanently added the RSA host key for IP address '192.30.252.129' to the list of known hosts.
Enter passphrase for key '/c/Users/YJC/.ssh/id_rsa':
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 292 bytes | 0 bytes/s, done.
Total 2 (delta 0), reused 0 (delta 0)
To git@github.com:52fhy/fhyblog.git
efe4969..91115af master -> master
Branch master set up to track remote branch master from origin.

Admin@YJC-PC /d/phpsetup/www/git/fhyblog (master)
```
 

如果完成到这里,恭喜你!你已经有了本地和远程版本库了。



##2. 再次使用git
以后本地版本库里有更新,使用 `git add`  添加,使用命令 `git commit` 提交。
更新至远程使用命令 `git push origin master` 推送



##3. 从远程更新至本地版本库
要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。

```
$ git clone git@github.com:52fhy/fhyBlog.git

Cloning into 'fhyBlog'...
Enter passphrase for key '/c/Users/YJC/.ssh/id_rsa':
remote: Counting objects: 284, done.
remote: Compressing objects: 100% (238/238), done.
remote: Total 284 (delta 28), reused 283 (delta 27)R
Receiving objects: 94% (267/284), 644.00 KiB | 12.00 KiB/
Receiving objects: 100% (284/284), 676.81 KiB | 12.00 KiB/s, done.
Resolving deltas: 100% (28/28), done.
```
 

##4. 写在后面

本文仅是Git的基本使用,可以作为新手入门教程。更多Git相关操作，请参考：
>1. [Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000),极力推荐，尤其是新手；
2. 《Pro Git》一书,百度搜索吧；
3. [Git官方教程](http://git-scm.com/doc)。




本文在博客园（cnblogs）里也有博客，喜欢博客园的朋友请移步[Git使用笔记- 博客园](http://www.cnblogs.com/52fhy/p/3973887.html#3086891)。

---

更新时间: 2015-7-27 12:24:53

版权: 本文采用以下协议进行授权,[自由转载 - 非商用 - 非衍生 - 保持署名 | Creative Commons BY-NC-ND 3.0](http://creativecommons.org/licenses/by-nc-nd/3.0/deed.zh)，转载请注明作者及出处。
