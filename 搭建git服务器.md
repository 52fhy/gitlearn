## �git������

>Զ�ֿ̲�ʵ���Ϻͱ��زֿ�ûɶ��ͬ������Ϊ��7x24Сʱ������������ҵ��޸ġ�GitHub����һ������йܿ�Դ�����Զ�ֿ̲⡣���Ƕ���ĳЩ��Դ��������������ҵ��˾��˵���Ȳ��빫��Դ���룬���᲻�ø�GitHub�������ѣ��Ǿ�ֻ���Լ��һ̨Git��������Ϊ˽�вֿ�ʹ�á�

git�����ַ���˺Ϳͻ��ˣ����ԣ����㰲װ����git������Ϳ��Կ�ʼ������Լ���git��������

��ʼ~

�ȴ���һ��git�û�����������git����
```
$ sudo adduser git
```

Ȼ���л������û���
```
su - git
```

��Ҫʹ�÷�rootȨ�޴���`~/.ssh/`��`~/.ssh/authorized_keys`��

```
mkdir .ssh
chmod 700 .ssh
touch ~/.ssh/authorized_keys 
chmod 644 ~/.ssh/authorized_keys
```

```
vim ~/.ssh/authorized_keys
```
����ÿ���˵Ĺ�Կ��`~/.ssh/authorized_keys`���ɡ�

��ʾ��
>ʹ��`ssh-keygen -t rsa -C "youremail@example.com"`���ɹ�Կ��

Ȼ��Ϳ���������git clone����

```
$ git clone git@xxxx:/home/git/test.git
Cloning into 'test'...
Enter passphrase for key '/c/Users/YJC/.ssh/id_rsa':
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

���Է��֣���������`etc/ssh/sshd_config`��

��Ҫ�Ĳ��裺ʹ�÷�root�û�������մ�����git�û�����`~/.ssh/`��`~/.ssh/authorized_keys`����Ҫ��ȷ����Ȩ�ޣ���700,644.

