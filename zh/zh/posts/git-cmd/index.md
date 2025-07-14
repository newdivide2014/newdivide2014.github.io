# Git常用命令

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1811921555&auto=1&height=66"></iframe>

记录一些常用的git命令，忘记的时候来翻翻看。

### git常用命令

1. 查看当前git用户的配置
    
        git config --list

2. 配置用户信息
   
        git config --global user.name "xxx"
        git config --global user.email "xxx@xxx"

3. 开始新的项目，初始化新的仓库
   
        git init 

4. 把文件/目录加入暂存区（stage）例子是把当前目录下的所有文件加入到暂存区。
   
        git add .

5. 把文件或目录从暂存区（stage）移除
    git rm --cached ./demo.txt
此刻./demo.txt文件已经从暂存区域删除，但是仍在当前目录下，如果想把该文件也从工作目录中删除，执行

        git rm ./demo.txt

6. git提交忽略某些文件
有些不需要git管理的文件比如.o文件等，可以在跟目录下创建一个名为**.gitignore**，然后在此文件里添加：

        *.o
所有空行或`#`开头的行都会被忽略，以上的设置在每次提交是就会忽略所有的.o文件。

7. 修改最后一次提交
有时执行了`git commit -m "XXX"`后，发现还有一些文件没有添加到暂存区，想撤回刚刚的提交操作，可以使用以下命令修改最后一次的提交信息
        
        git commit -amend 

8. 查看历史
   
        git log
        # 查看text.c文件的所有改动历史，
        # 每条记录显示在一行
        git log --pretty=oneline test.c

9. 恢复单个文件历史版本

        # 得到text.c的历史版本号
        git log text.c 
        # 恢复到版本为2e17053b时候的text.c文件
        git reset 2e17053b

10. 查看你曾使用过的git命令
    git reflog用来记录你的每一次命令
### git分支相关

1. 推送远程分支

        git push <远程主机名> <本地分支名>:<远程分支名>
        git push origin local:remote
        # 示例
        git push origin master
        # 表示将本地的master分支推送到远程的origin主线的master分支
        # 如果master不存在，则会被新建

2. 创建新的分支并切换

        git checkout -b <本地分支名> <远程分支名>
        # 示例：
        git checkout -b dev origin/master
        # 从远程拉取dev分支到本地,命名为develop，并切换到develop分支
        git checkout -b develop origin/dev

3. 删除分支

        # 删除远程分支
        git push origin :<远程分支名>
        git push origin :dev
        # 等同于
        git push origin --delete <远程分支名>

        # 删除本地分支
        git branch -D <本地分支>

4. 查看各个分支最后一个提交对象的信息

        git branch -v

5. 查看与当前分支 合并/未合并 的分支

        # 与当前分支已经合并的分支
        git branch --merged
        # 与当前分支未合并的分支
        git branch --no-merged

6. 同步远程服务器数据到本地

        git fetch origin

7. 对于`git pull`的理解
   
`git pull`的过程可以理解为：

        git fetch origin master 
        git merge FETCH_HEAD
        # 完整的格式为：
        git pull <远程主机名> <远程分支名>:<本地分支名>
        # 如果远程分支是与当前分支合并，则冒号后面的部分可以省略，例如：
        git pull origin dev

8. 分支的合并
   
把一个分支整合到另一个分支有两种方法：`merge`和`rebase`（衍合）
`merge`是把两个分支最新的快照和二者最新的共同祖先进行三方合并，产生一个新的提交对象。
`rebase`单独写




###  git stash缓存本地仓库工作目录

1. 执行存储时，添加备注，方便查找，只有`git stash`也可以的，但查找时不方便。

        git stash save "save message"

2. 查看stash了哪些存储

        git stash list 

3. 显示做了哪些改动，默认show第一个存储,如果要显示其他存贮，后面加`stash@{$num}`。

        git stash show
        # 显示第二个存储改动
        git stash show stash@{1}

4.  显示存储的改动，默认显示第一个。

        git stash show -p
        git stash show  stash@{$num}  -p
        # 显示第二个存储的改动
        git stash show  stash@{1}  -p


5. 应用某个存储,但不会把存储从存储列表中删除，默认使用第一个存储。

        git stash apply
        git stash apply stash@{$num}
        # 应用第二个
        git stash apply stash@{1}

6. 命令恢复之前缓存的工作目录，将缓存堆栈中的对应stash删除，并将对应修改应用到当前的工作目录下，默认为第一个stash。

        git stash pop
        git stash pop stash@{$num}
        # 应用并删除第二个
        git stash pop stash@{1}

7. 丢弃stash@{$num}存储，从列表中删除这个存储

        git stash drop stash@{$num}

8. 删除所有缓存的stash

         git stash clear



### git submodule相关

1. 添加第三方git仓库
```sh
# path是该子模块存储的目录路径
git submodule add <url> <path>
# 例子
git submodule add https://XXXXXXX.git /home/user
```
添加完成后会在.gitmodules中看到每个submodule的信息。

2. 将第三方git仓库同步到主线

克隆仓库后，默认子模块的目录下是空的，需要在本地仓库根目录把子模块拉到本地，用到命令如下：
```sh
git submodule init
git submodule update
或者：
git submodule update 
# 例子
git clone https://XXXXXXX.git
git submodule init && git submodule update

#下面这句的效果和上面的命令效果一样
git clone https://XXXXXXX.git --recursive
```


3. 删除submodule
```sh
git submodule deinit <submodule-name>
```

---

### FAQs

1. 执行 git remote add [shortname] [url] 如果提示：remote origin already exists.

则先删除：git remote rm origin
然后再添加：git remote add origin https://XXXX.git

2. git add 操作时，有时会误添加一些不想提交的文件，如何解决？
误add单个文件
```
git reset HEAD 将file退回到unstage区
```
误add多个文件，只撤销部分文件
```
git reset HEAD 将file退回到unstage区
```
3. windows git bash 在使用`git log`时中文乱码

执行命令`export LANG=”zh_CN.UTF-8`就好了


---

> : 嘟囔  
> URL: http://localhost:1313/zh/zh/posts/git-cmd/  

