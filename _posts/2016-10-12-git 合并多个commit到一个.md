---
layout: post
title: git 合并多个commit到一个
---

标签（空格分隔）： git rebase

---

## 背景和现象

在向Gerrit提交代码的时候，每次提交只能有一个commit，即使是chang id 一致也不行，Gerrit系统会报如下错误：

```
sdn@SZX1000107431:~/onos$ git review 
You are about to submit multiple commits. This is expected if you are
submitting a commit that is dependent on one or more in-review
commits. Otherwise you should consider squashing your changes into one
commit before submitting.

The outstanding commits are:
`
1a253d5 (HEAD, review/cheng_fan/fixbug_leaflist) fix java doc problems
17a8ee6 add namespace info for yangnode
4fc6ec8 [ONOS-5397]fixbug:NBI Error for complicate list inside container`

Do you really want to submit the above commits?
Type 'yes' to confirm, other to cancel: yes
remote: Processing changes: refs: 1, done    
To ssh://chengfan@gerrit.onosproject.org:29418/onos
 ! [remote rejected] HEAD -> refs/publish/master/fixbug_leaflist (squash commits first)
error: failed to push some refs to 'ssh://chengfan@gerrit.onosproject.org:29418/onos'
sdn@SZX1000107431:~/onos$ git rebase -i 17a8ee6
Successfully rebased and updated refs/heads/review/cheng_fan/fixbug_leaflist.
sdn@SZX1000107431:~/onos$ git rebase -i 1a253d5
Successfully rebased and updated refs/heads/review/cheng_fan/fixbug_leaflist.
```

提示你需要`squash commits first`

## 解决方法

主要参考这篇文章：https://feeding.cloud.geek.nz/posts/combining-multiple-commits-into-one/

解决方法如下：

```
git rebase -i 4fc6ec8

```

rebase的对象是想合并的两个提交之前的一个提交。接着会进入vim进行交互式的rebase，将第二个提交squash 掉然后保存退出即可。



