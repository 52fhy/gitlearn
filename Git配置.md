
# Git����

---

## �����û���
���ñ���git�û��������䡣�����������룺
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## ���ñ���

��û�о����ô��������git status��status����������Ĳ��üǡ�git�ṩ�˱������ã�
```
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
```
������������co��ʾcheckout��ci��ʾcommit��br��ʾbranch��

���������ɥ�Ĳ���ı�������`lg`:
```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

�鿴��־������ʹ�ã�
```
git lg
```

## �����ļ�
����Git��ʱ�򣬼���`--global`����Ե�ǰ�û������õģ�������ӣ���ֻ��Ե�ǰ�Ĳֿ������á�

����ʹ��`git config -l`�鿴���á�

�����ļ������ˣ�ÿ���ֿ��Git�����ļ�������.git/config�ļ��У�
```
$ cat .git/config 
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
```

����ǰ�û���Git�����ļ������û���Ŀ¼�µ�һ�������ļ�.gitconfig�У�
```
$ cat .gitconfig
[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com
```

## �����ļ�

��Щʱ��������ĳЩ�ļ��ŵ�Git����Ŀ¼�У����ֲ����ύ���ǣ����籣�������ݿ�����������ļ������ȵȡ������½�.gitignore�ļ���

```
touch .gitignore
vi .gitignore
```

����ʾ����
```
Conf/*
Data/*
Logs/*
Runtime/*
.idea/*
.buildpath
.project/
.settings/
```

�����ļ���ԭ���ǣ�

- ���Բ���ϵͳ�Զ����ɵ��ļ�����������ͼ�ȣ�
- ���Ա������ɵ��м��ļ�����ִ���ļ��ȣ�Ҳ�������һ���ļ���ͨ����һ���ļ��Զ����ɵģ����Զ����ɵ��ļ���û��Ҫ�Ž��汾�⣬����Java���������.class�ļ���
- �������Լ��Ĵ���������Ϣ�������ļ��������ſ���������ļ���

��`git check-ignore`�������Ƿ񱻼�����Թ������ˣ�
```
$ git check-ignore -v a.class
```
