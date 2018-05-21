# simple using of git
## 1. 获取仓库
* 在现有目录中创建仓库：  
> git init  
> git add *  
> git add LICENSE  
> git commit -m 'initial project version'  
* 克隆一个仓库：  
> git clone https://github.com/libgit2/libgit2  
> git clone https://github.com/libgit2/libgit2 mylibgit `自定义仓库名字`  

## 2. git常用命令  
* 查看当前文件状态
> git status
* 工作目录下文件的状态  
![status](https://github.com/henerywang/usefultools/blob/master/realtek/git_status.png?raw=true) 
* 跟踪新文件  
> git add newfile `新文件会变成staged状态`
* 暂存已修改的文件  
> git add modified_file `同样是add，但是针对的是有跟踪的文件并且做了修改。运行了 git add 之后又作了修订的文件，需要重新运行 git add 把最新版本重新暂存起来`
* 状态简览  
> git status -s  `?:未跟踪，A:新添加到staged,MM:有修改，并且暂存区也有, M:修改并放入暂存器,M :修改但没有放入暂存区`
* 工作区中忽略某些文件  
> vim .gitignore  `利用通配符可以过滤掉一些不关心的文件`
* 查看已暂存和未暂存的修改  
> git diff `查看已修改文件和暂存的差异`  
> git diff --staged `查看已暂存的将要添加到下次提交里的内容`  
* 提交更新  
> git commit 
> git commit -v `提交时，把修改记录放到log中`  
> git commit -m `log放在m后面，不会启动编辑器`  
> git commit -a `跳过使用暂存区，modified文件会直接跳过git add，直接提交  
* 移除文件  
> git rm  
> git rm -f `如果文件在暂存区，需要带上-f`  
* 移动文件  
> git mv old new
* 查看git提交历史
> git log  
> git log -p `查看提交的改动内容`  
> git log -p 2 `查看最近两次提交的改动内容`  
> git log --pretty=oneline `这个有点复杂，可以另外写一篇来单独描述`  
* 撤消操作
> git commit -m 'initial commit'  
> git add forgotten_file  
> git commit --amend `最终你只会有一个提交 - 第二次提交将代替第一次提交的结果`  
* 取消暂存的文件
> git reset staged_file  
* 取消修改的文件
> git checkout -- modified_file  

## 3. 远程仓库使用
* 如果clone了一个远程仓库，可以用如下命令查看仓库服务器的默认名字和对应的url  
> git remote -v    
* 从远程仓库中抓取与拉取  
> git fetch remote-name  
* 推送到远程仓库  
> git push origin master  
* 远程仓库的移除与重命名  
> git remote rename old new  
> git remote rm name

## 4.总结
### git工作流程
1. 在工作目录中修改文件。  
2. 暂存文件，将文件的快照放入暂存区域。  
3. 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。

### 由git状态引出的工作区概念，如下图：
![workstation](https://github.com/henerywang/usefultools/blob/master/realtek/work_station.png?raw=true) 