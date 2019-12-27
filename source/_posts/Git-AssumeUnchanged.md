---
title:  Git忽略不想提交的文件
date: 2019-12-26 21:48:35
author:     孙宏伟
summary:    git ignore files
categories:  Git
tags:
 - Git
---

## Git忽略不想提交的文件

&ensp;&ensp;&ensp;&ensp;在使用Git进行代码管理的时候,由于编译或功能验证需求会产生很多临时文件,这些是不希望上传到远程代码仓库的,但通过*git status*查看时经常会出现一片红的未追踪文件或修改的文件,对提交工作带来困难,这种情况可以通过配置**".gitignore"**文件对未提交的文件进行忽略,假设不小心进行了提交,也可以通过**"assume-unchanged"**命令对修改的文件进行忽略,当内容发生变化时不再进行提示.

### ".gitignore"配置文件
&ensp;&ensp;&ensp;&ensp;在本地新创建几个文件,然后通过*git status*命令查看,会发现未追踪的文件部分里会列出新增的几个文件:
```
sun@sun:~/SUN/GitTest$ touch test001.txt test002.txt test003.txt
sun@sun:~/SUN/GitTest$ git status 
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	test001.txt
	test002.txt
	test003.txt

nothing added to commit but untracked files present (use "git add" to track)
```

&ensp;&ensp;&ensp;&ensp;如果想对"test001.txt"文件进行忽略,则在相同文件夹内新建一个".gitignore"文件,在里面添加"test001.txt",在此执行"git status"会发现未追踪的文件列表内"test001.txt"已经不再显示了:
```
sun@sun:~/SUN/GitTest$ echo test001.txt > .gitignore
sun@sun:~/SUN/GitTest$ git status 
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
	test002.txt
	test003.txt

nothing added to commit but untracked files present (use "git add" to track)
```
&ensp;&ensp;&ensp;&ensp;同理也可以将文件夹路径填入到该文件,则Git会自动对整个文件夹的内容进行忽略.

### "assume-unchanged"指令
&ensp;&ensp;&ensp;&ensp;但是有时由于操作不当,不小心将某个临时文件push到了远程仓库,那上述方法就不再好用了,每次编译后修改过的文件列表总会出现该文件,为了避免每次仍然要提交这些不必要文件,"assume-unchanged"这个指令就排上用场了.
&ensp;&ensp;&ensp;&ensp;假设"test002.txt"是不小心提交到远程仓库的文件,每次编译都会导致该文件内容改变,出现在修改的文件列表里:
```
sun@sun:~/SUN/GitTest$ echo aaaa>test002.txt 
sun@sun:~/SUN/GitTest$ echo aaaa>test003.txt 
sun@sun:~/SUN/GitTest$ git status 
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   test002.txt
	modified:   test003.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
&ensp;&ensp;&ensp;&ensp;执行如下命令,默认忽略该文件的修改:
```
sun@sun:~/SUN/GitTest$ git update-index --assume-unchanged test002.txt
```
&ensp;&ensp;&ensp;&ensp;再此执行"git status"发现修改过的文件列表中已经没有了"test002.txt"这个文件:
```
sun@sun:~/SUN/GitTest$ git status 
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   test003.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

&ensp;&ensp;&ensp;&ensp;对于本地进行"git add"或者"git commit"命令的文件,可以使用"checkout"或"reset"命令进行护肤,具体方法不在此展开.


