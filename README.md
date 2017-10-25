## 如何使用git ##

### 1 初始化一个git仓库 ###

通过 `git init` 命令把这个目录变成Git可以管理的仓库

	$ git init
	Initialized empty Git repository in /Users/michael/learngit/.git/

### 2 添加文件到git仓库 ###

第一步：`git add <file>`
用命令git add告诉Git，把文件添加到仓库

	$ git add readme.txt

第二步：`git commit`
用命令git commit告诉Git，把文件提交到仓库。-m后面输入的是本次提交的说明

	$ git commit -m "wrote a readme file"
	[master (root-commit) cb926e7] wrote a readme file
 	1 file changed, 2 insertions(+)
 	create mode 100644 readme.txt

### 3 运行git status命令看看结果

`git status`命令可以让我们时刻掌握仓库当前的状态

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#    modified:   readme.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

### 4 git diff查看difference

`git diff` 查看具体修改了什么内容

	$ git diff readme.txt 
	diff --git a/readme.txt b/readme.txt
	index 46d49bf..9247db6 100644
	--- a/readme.txt
	+++ b/readme.txt
	@@ -1,2 +1,2 @@
	-Git is a version control system.
	+Git is a distributed version control system.
	 Git is free software.

### 5 git log 查看commit 快照

`git log` 命令显示从最近到最远的提交日志。你看到的一大串类似3628164...882e1e0的是commit id（版本号）

	$ git log
	commit 3628164fb26d48395383f8f31179f24e0882e1e0
	Author: Michael Liao <askxuefeng@gmail.com>
	Date:   Tue Aug 20 15:11:49 2013 +0800
	
	    append GPL
	
	commit ea34578d5496d7dd233c827ed32a8cd576c5ee85
	Author: Michael Liao <askxuefeng@gmail.com>
	Date:   Tue Aug 20 14:53:12 2013 +0800
	
	    add distributed
	
	commit cb926e7ea50ad11b8f9e909c05226233bf755030
	Author: Michael Liao <askxuefeng@gmail.com>
	Date:   Mon Aug 19 17:51:55 2013 +0800
	
	    wrote a readme file

### 6 回退到上一个版本

`git reset`用`HEAD`表示当前版本，上一个版本就是`HEAD^`,上上一个版本就是`HEAD^^`,往上100个版本`HEAD~100`

	$ git reset --hard HEAD^
	HEAD is now at ea34578 add distributed

回退到指定版本。`git reset --hard [commit id]`

### 7 记录你的每一次命令

`git reflog`

	$ git reflog
	ea34578 HEAD@{0}: reset: moving to HEAD^
	3628164 HEAD@{1}: commit: append GPL
	ea34578 HEAD@{2}: commit: add distributed
	cb926e7 HEAD@{3}: commit (initial): wrote a readme file

### 8 工作区&暂存区

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

![](images/0.jpg)

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

### 9 `git checkout -- file` 丢弃工作区的修改

	$ git checkout -- readme.txt

* 命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

* 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

* 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

* 总之，就是让这个文件回到最近一次git commit或git add时的状态。

### 10 删除文件

当你直接在文件管理器删除文件后，现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit：

	$ git rm test.txt
	rm 'test.txt'
	$ git commit -m "remove test.txt"
	[master d17efd8] remove test.txt
	 1 file changed, 1 deletion(-)
	 delete mode 100644 test.txt
