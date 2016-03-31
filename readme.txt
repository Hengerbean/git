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

远程仓库：
	创建SSH Key：
		在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。

	$ ssh-keygen -t rsa -C "470386285@qq.com"

	id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
	登陆GitHub：

	打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，点“Add Key”。

添加远程库:
	在右上角找到“Create a new repo”按钮，创建一个新的仓库。在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库。
	
	在本地的git仓库下运行命令：

	$ git remote add origin git@github.com:Hengerbean/git.git
	$ git remote add origin git@server-name:path/repo-name.git
	下一步，就可以把本地库的所有内容推送到远程库上：

		$ git push -u origin master
	从现在起，只要本地作了提交，就可以通过命令：

	$ git push origin master

从远程库克隆:
	先创建github远程版本库：

	$ git clone git@github.com:server_name/repo_name.git
	要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。

	Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

	


	
