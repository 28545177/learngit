﻿https://www.liaoxuefeng.com/

2020-1-1
这个是我用git创建的版本库。和GitHub Desktop应该是同一个东西，不过是不同的入口。我现在还不知道怎么用，先创建了再说。

增加一些git的基本操作。
1、创建一个文件夹作为工作区；
2、初始化一个Git仓库，使用git init命令。
3、添加文件到Git仓库，分两步：
	使用命令git add <file>，注意，可反复多次使用，添加多个文件；
	使用命令git commit -m <message>，完成。

4、要随时掌握工作区的状态，使用git status命令。
5、如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
git diff查看的是工作区和缓冲区中的数据差别。所以在数据add后，这个命令就不会有结果了；

6、版本回退
（1）查看版本的历史记录
git log
参数--pretty=oneline，显示简略信息。
git log --pretty=oneline
记录的前面显示一长串字符，这个是commit id；
（2）回退
Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100；
回退命令git reset
git reset --hard HEAD^		回退到上一个版本
（3）返回最新版本
首先要得到最新版本的commit id。使用
git reflog，查看命令历史，得到所有版本信息。找到最新版本的commit id；
然后调用：git reset --hard commit id，回退到相应的版本；


2020-1-2
使用桌面版增加了一个版本库。今天的一个目标就是让命令行版和桌面版之间统一；

撤销修改
这个功能和廖雪峰网站上的命令不同。使用的
git restore来撤销修改。其中，
（1）在没有add前，调用git restore <file>可以撤销修改；
说明：工作区和缓冲区的数据都是A，修改后工作区是A+，此时没有add，调用上述命令，将工作区的A+返回到A；

（2）在add后，调用git restore --staged <file>。这条语句修改的是缓冲区中的信息。
说明：工作区和缓冲区的数据都是A，修改后工作区的数据是A+，add后缓冲区的数据也是A+。此时调用上述数据，缓冲区中的数据变成了A。如果想要将工作区的数据也修改的话，重复（1）的操作，调用git restore <file>，改变工作区的数据；

删除文件
文件删除后，工作区和缓冲区的内容不同，可以：
（1）删除缓冲区的内容：git rm <file>
（2）将缓冲区的数据恢复到工作区：git restore <file>

创建远程库
（1）首先创建ssh-key
ssh-keygen -t rsa -C "youremail@example.com"
在用户主目录下，生成.ssh目录，里面有id_rsa和id_rsa.pub这两个文件。这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

（2）在Github上载入ssh-key
登陆GitHub，打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容；

（3）创建库，创建后，Github的提示信息
	…or create a new repository on the command line
	 echo "# learngit" >> README.md
	git init
	git add README.md
	git commit -m "first commit"
	git remote add origin https://github.com/28545177/learngit.git
	git push -u origin master

	…or push an existing repository from the command line
	 git remote add origin https://github.com/28545177/learngit.git
	git push -u origin master

	…or import code from another repository
	You can initialize this repository with code from a Subversion, Mercurial, or TFS project.

（4）根据提示，输入：
git remote add origin https://github.com/28545177/learngit.git，在本地关联远程库；
输入：git push -u origin master 第一次，使用参数-u，上传所有的分支。
正常使用时，输入git push origin master，
将本地数据推送到远程库中；

（5）从远程库下载数据，输入：
git clone git@github.com:28545177/gitskills.git

回家后，创建新的文件夹，或者直接就用昨天文件夹作为本地仓库，调用git clone将今天修改的数据下载到本地工作区；

使用分支功能
Git鼓励大量使用分支：
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>或者git switch <name>
创建+切换分支：git checkout -b <name>或者git switch -c <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

分支冲突解决
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。

标签管理
发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。
标签跟分支很像，但是分支可以移动，标签不能移动；
本来是想不到要用这个功能，甚至本来是想不到用Github的，不过在学习微信小程序开发的时候，讲课老师用的就是这个标签功能，这才开始学习的。

新建标签
git tag <name>		#在最新提交的commit上打标签
如果要给历史提交的commit打标签，那么先要找到历史提交的commit id，然后打标签
git log --pretty=oneline --abbrev-commit		#简略方式查看历史信息，得到历史commit id
git tag v0.9 f52c633	#给f52c633打标签v0.9

查看所有标签
git tag

删除标签  -d
git tag -d <tagname>

标签上传远端
标签存在本地，不会上传到远程。如果要上传到远程的话，使用命令：
git push origin <tagname>
如果要上传所有的本地标签，使用：
git push origin --tags

删除远端标签
1、删除本地标签
git tag -d <tagname>
2、从远端删除，使用的还是push，格式为：
git push origin :refs/tags/<tagname>







