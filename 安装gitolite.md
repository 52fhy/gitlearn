# 安装gitolite管理git服务器

---

## 为什么安装gitolite
git默认使用SSH协议，在服务器上基本上不用怎么配置就能直接使用。但是如果面向团队服务，需要控制权限的话，还是用gitolite方便些。

## gitosis OR gitolite？
为什么不用gitosis呢？原因很简单，它已经好几年没有更新了。
gitolite原本是作为gitosis的lite版本出现的，可是现在的功能甚至已经超过gitosis了。

## 安装gitolite

建立git用户：
```
groupadd git
adduser git -g git
```

登录到git用户。如果没有给git用户设置密码，可以从root用户通过su切换过去。
```
su git
```

将公钥文件(.pub)放在git用户当前目录。假如客户端用户名是52fhy,公钥文件是id_rsa.pub：

```
scp id_rsa.pub xxx@host:/tmp
mv /tmp/id_rsa.pub ~/52fhy.pub
```
改名是为了好识别用户。host是你的主机地址或域名。

现在来安装gitolite。还是在git用户家目录：
```
# 获取版本库
git clone git://github.com/sitaramc/gitolite

# 创建bin目录，用于存放安装后的文件
mkdir -p ~/bin

# 将gitolite安装到bin目录
gitolite/install -to ~/bin

# 使用YourName.pub公钥初始化版本库
./bin/gitolite setup -pk 52fhy.pub
```

默认这个52fhy是管理员。如果没有提示错误，就安装好了。
该过程会自动新建`~/.ssh/authorized_keys`（如果不存在）。


## 管理用户和版本库

不应该手动在服务器端加入新的用户或者版本库。

gitolite使用一个特殊的版本库 `gitolite-admin`来管理员用户和版本库，只要在这个版本库中修改并 push，服务器就会自动根据配置作出修改。

首先在客户端迁出版本库：
```
git clone git@host:gitolite-admin
```
注意，这里`gitolite-admin`不用带路径，全称就是这个。以后通过gitolite新建的版本库也不用带绝对路径。

clone到本地后，可以看到gitolite-admin文件夹。

如果需要使用不同的密钥连接多个ssh服务器，可以编辑 ~/.ssh/config 进行配置。这里不做介绍。

进入 `gitolite-admin` 目录，其中的 `keydir` 目录是用来放置用户公钥的，而 `conf/gitolite.conf` 则是用来配置用户和版本库。

编辑 `conf/gitolite.conf`如下：
```
repo foo
    RW+         =   52fhy
    RW          =   bob
    R           =   carol
	
repo testing
    RW+     =   @all
```

上面的配置的含义是：

有一个名为 foo 的版本库；
用户 52fhy 对它有读、写、删除权限；
用户 bob 对它有读写权限；
用户 carol 对它仅有只读权限。

testing版本库任何人都有读写、删除权限。

如果需要新增一个版本库，只需要在`conf/gitolite.conf`文件新增。示例：
```
repo test2
	RW  	=   user2
```

push上去后，自动新增test2版本库。注意需要将用户uer2的公钥文件复制到keydir 目录中。gitolite会自动将公钥加入到 `~/.ssh/authorized_keys` 中。

此时test2版本库的访问地址为 git@host:test2。

如果希望把 test2 版本库放在 bar 目录下，可以这样编辑配置文件：

repo bar/test2
    RW+         =   alice
    RW          =   bob
    R           =   carol
此时foo 版本库的访问地址为 git@host:bar/test2。

>参考：
安装gitolite | zrong's blog
http://zengrong.net/post/1720.htm