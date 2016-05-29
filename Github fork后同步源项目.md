
# Github fork后同步源项目

---

介绍：
有时候我们在github上看到一些比较好的项目，我们都会fork一下它，然后在本地进行操作，但是fork之后，项目是不会跟源项目保持同步的，需要我们自己进行一些操作让其同步。

解决方法：

假设源项目是：git@github.com:52fhy/gitlearn.git
<br/>
自己的项目是：git@github.com:xxx/gitlearn.git

1、先fork源代码；

2、将fork后的代码clone到本地
```
git clone git@github.com:xxx/gitlearn.git
```

3、添加源项目到远程主机列表并改名叫52fhy（自定义的。因为默认是origin，与自己的重复了）：
```
git remote add 52fhy git@github.com:52fhy/gitlearn.git
```
这样做的目的是下次pull或者fetch的时候可以选择从哪个远程库更新。

4、查看远程主机列表，发现多了52fhy:
```
git remote -v

52fhy     git@github.com:52fhy/gitlearn.git (fetch)
52fhy     git@github.com:52fhy/gitlearn.git (push)
origin  git@github.com:xxx/52fhy/gitlearn.git (fetch)
origin  git@github.com:xxx/52fhy/gitlearn.git (push)
```

5、假如源项目更新了，可以通过下面代码更新：
```
git fetch 52fhy
git merge 52fhy/master
```
选择从源项目52fhy更新并合并到本地库。

6、更新到自己fork来的远程代码库
```
git push
```
因为默认关联自己的远程库，不用指定远程主机名。


