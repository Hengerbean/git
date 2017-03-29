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

分支管理：
	创建与合并分支：

		查看分支： $ git branch 
		创建分支： $ git branch <name>
		切换分支： $ git checkout <name>
		创建+切换分支： $ git checkout -b <name>
		合并某分支到当前分支：$ git merge <name>
		删除分支： $ git branch -d <name>

		首先在工作分支上开发新需求，忽然要修补bug。
			切换到你的线上分支，为这个紧急任务新建一个修补分支，并在其中修复它。
			在测试通过之后，切换回线上分支，然后合并这个修补分支，最后将改动推送到远程。
			切换回你的最初工作的分支上，继续工作。
	
	解决冲突：
		当git无法自。动合并时，就必须首先解决冲突，在提交，合并完成。用 $ git log --graph  命令可以看到分支合并图。

 
	分支管理策略：
		
		能查看分支合并历史：

			$ git merge --no-ff -m "comment" <name>
	Bug分支管理：
		当手头的工作没有完成时，先把工作现场 $ git stash 一下，然后去修复Bug，修复后，再 $ git stash pop ,回到工作现场。
		$ git stash		储存当前现场
		$ git tash list	查看储存目录 
		$ git tash apply stash@{0}	回复储存现场
		$ git tash drop 	删除储存现场
		$ git tash pop		回复并删除储存现场

	Feature分支：
		开发一个新Feature，最好新创建一个分支;
		如果要丢弃一个没被合并的分支，通过 $ git branch -D <name>
强行删除。
	
	多人协作：
		
		查看远程库的信息：$ git remote -v
		本地新建的分支如果不推送，对其他人就不可见。
		从本地推送分支，使用 $ git push origin branch-name ,如果推送失败，先用 git pull 抓取远程的新提交。
		在本地创建和远程分支对应的分支，使用 $ git checkout -b branch-name origin/branch-name ,本地和远程分支的名称最好一致。
		建立本地分支和远程分支的关联，使用 $ git branch --set -upstream orgin/branch-name
		从远程库抓取使用 $ git pull,如果有冲突，先解决冲突。

标签管理：
	
	创建标签：
		$ git tag -a <tagname> -m "comment"	创建标签
		$ git tag 	显示所有标签
		$ git show <tagname> 显示标签信息

	操作标签： 
		$ git push origin <tagname>	推送一个本地标签
		$ git push origin --tag	可以推送全部本地未推送的标签
		$ git tag -d <tagname>	删除一个本地标签
		$ git push origin :refs/tags/<tagname>	可以删除一个远程标签。

Gitub:

	在 github上，可以任意Fork开源仓库.
	自己拥有Fork后的仓库读写权限。
	可以推送pull request 给官方仓库来贡献代码.
忽略特殊文件：
	忽略默写文件时，需要编写 .gitignore;
	.gitignore 文件本身要放到版本库中，并且可以对.gitignore作版本控制。


处理冲突：
	git status
	
	git add
	
	git commit


			REDIS

	运行redis命令
	redis-server /opt/local/etc/redis.conf

	进入redis命令行
	redis-cli -h ip -p port
	
	关闭redis命令
	redis-cli -h 127.0.0.1 -p 6379 shutdown


		MONGODB

	开启mongodb命令
	mongostart

	关闭mongodb命令
	mongostop
	
	

	

