## 搭建git服务器

>远程仓库实际上和本地仓库没啥不同，纯粹为了7x24小时开机并交换大家的修改。GitHub就是一个免费托管开源代码的远程仓库。但是对于某些视源代码如生命的商业公司来说，既不想公开源代码，又舍不得给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用。

git不区分服务端和客户端，所以，当你安装好了git，下面就可以开始搭建属于自己的git服务器。

开始~

先创建一个git用户，用来运行git服务：
```
$ sudo adduser git
```

然后切换到该用户：
```
su - git
```

需要使用非root权限创建`~/.ssh/`和`~/.ssh/authorized_keys`：

```
mkdir .ssh
chmod 700 .ssh
touch ~/.ssh/authorized_keys 
chmod 644 ~/.ssh/authorized_keys
```

```
vim ~/.ssh/authorized_keys
```
复制每个人的公钥到`~/.ssh/authorized_keys`即可。

提示：
>使用`ssh-keygen -t rsa -C "youremail@example.com"`生成公钥。

然后就可以免密码git clone啦：

```
$ git clone git@xxxx:/home/git/test.git
Cloning into 'test'...
Enter passphrase for key '/c/Users/YJC/.ssh/id_rsa':
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

测试发现，不用配置`etc/ssh/sshd_config`。

重要的步骤：使用非root用户，例如刚创建的git用户创建`~/.ssh/`和`~/.ssh/authorized_keys`！还要正确设置权限，如700,644.

