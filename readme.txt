https://www.liaoxuefeng.com/

2020-1-1
这个是我用git创建的版本库。和GitHub Desktop应该是同一个东西，不过是不同的入口。我现在还不知道怎么用，先创建了再说。

增加一些git的基本操作。
1、创建一个文件夹作为本地仓库；
2、初始化一个Git仓库，使用git init命令。
3、添加文件到Git仓库，分两步：
	使用命令git add <file>，注意，可反复多次使用，添加多个文件；
	使用命令git commit -m <message>，完成。

4、要随时掌握工作区的状态，使用git status命令。
5、如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

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
1、在没有add前，调用git restore <file>可以撤销修改；
2、在add后，调用git restore --staged <file>。这个操作据说可以撤销修改，可是我没有实现。






