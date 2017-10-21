
在使用git push的时候发现个问题：本地有多个分支，我在dev分支开发，commit后使用git push命令箱推送到远程，提示：

``` bash
$ git push
To git.youshu.cc:php/readwith.git
 ! [rejected]          master -> master (non-fast-forward)
error: failed to push some refs to 'git@git.xxx.com:php/readwith.git'
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. Check out this branch and integrate the remote changes
hint: (e.g. 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```

到远程发现dev分支倒是推送上去了，但是这里提示出错。仔细看，才知道git尝试把本地的master分支也推送上去。这并不是我本意。

后来查询到git push是有默认行为的，在配置里。我查询了，本地配置是：
``` bash
$ git config --global -l  | grep push
push.default=matching
```

查询了相关资料，得知：

push.default 有以下几个可选值：
``` bash
nothing, current, upstream, simple, matching
```

其用途分别为：
``` bash
nothing - push操作无效，除非显式指定远程分支，例如git push origin develop（我觉得。。。可以给那些不愿学git的同事配上此项）。
current - push当前分支到远程同名分支，如果远程同名分支不存在则自动创建同名分支。
upstream - push当前分支到它的upstream分支上（这一项其实用于经常从本地分支push/pull到同一远程仓库的情景，这种模式叫做central workflow）。
simple - simple和upstream是相似的，只有一点不同，simple必须保证本地分支和它的远程
upstream分支同名，否则会拒绝push操作。
matching - push所有本地和远程两端都存在的同名分支。
```

原来是这么回事！我立马改了本地配置：
``` bash
$ git config --global push.default simple


$ git config --global -l  | grep push
push.default=simple

```

再提交：
``` bash
$ git push
Everything up-to-date
```

没有出错了。

建议阅读更多相关知识：
Git push与pull的默认行为 - 蛤蛤 - SegmentFault  https://segmentfault.com/a/1190000002783245
