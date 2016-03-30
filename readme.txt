Git is a version control system.
Git is free software.
git
git config --global user.name "henger"
git config --global user.email "470386285@qq.com"

创建版本库：
	1.创建一个空目录：
		$ mkdir learngit
		$ cd learngit
		$ pwd
	
	2.声明一个Git仓库：
		$ git init

	3.把文件添加到暂存区：
		$ git add readme.txt

	4.把文件提交到仓库：
		$ git commit -m "wrote a readme file"

时光机穿梭：
	1.获取仓库当前的状态：
		$ git status

	2.查看修改内容：
		$ git diff readme.txt 

	3.查看提交日志：
		$ git log
		$ git log --pretty=oneline

	4.查看命令历史：
		$ git reflog
	
	5.版本回退：

		$ git reset --hard HEAD^
		$ git reset --hard HEAD^^
		$ git reset --head commitID
	
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- fileName。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD fileName，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退，不过前提是没有推送到远程库。

删除文件：
	工作区 
		$ rm fileName
	版本库 
		$ git rm fileName

	用版本库里的版本替换工作区的版本 
		$ git checkout -- fileName

