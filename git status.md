### git status

- 要随时掌握工作区的状态，使用`git status`命令。

- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

  

  -----

  ### 版本回退

  

  * HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。

  * 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。

  * 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。
  * cat file_name 查看文件内容。

  -----

  

### \*git使用[^分支]



+ **查看** 分支：`git branch` 

+ **创建**分支：`git branch <name>`

+ **切换**分支：`git checkout <name>`或者`git switch <name>`

+ **创建+切换**分支：`git checkout -b <name>`或者`git switch -c <name>`

+ **合并**某分支到当前分支：`git merge <name>`

+ **删除**分支：`git branch -d <name>`



[^分支]: 每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支

******************

### 解决冲突



* 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。  

* 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
  * 用`git log --graph`命令可以看到分支合并图。($ git log --graph --pretty=oneline --abbrev-commit)



****

### 分支管理策略

* Git分支十分强大，在团队开发中应该充分应用。

* 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并

  

---------- - -

### bug分支

* 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

* 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

* 在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

----

### feature（新功能）分支

* 开发一个新feature，最好新建一个分支；

* 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

-----

### 多人协作

#### 工作模式

> 1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
> 2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
> 3. 如果合并有冲突，则解决冲突，并在本地提交；
> 4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！
>
> 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。
>
> 这就是多人协作的工作模式，一旦熟悉了，就非常简单。  

####  小结

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

---



### git rebase

- rebase操作可以把本地未push的分叉提交历史整理成直线；

- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。    

  

  【详细解决一些问题】https://blog.csdn.net/Fairy_Jun/article/details/109441581

----

### 标签

#### 新建标签

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。

#### 删除与推送标签

- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

----

### 连接gihub与gitee

详见：https://www.liaoxuefeng.com/wiki/896043488029600/1163625339727712

-----

### 配置别名

```
$ git config --global alias.别名 原名
```

> co : checkout
>
> st : status
>
> ci : commit
>
> br : branch
>
> unstage : 'reset HEAD'                                       //撤销更改
>
> last : 'log -1'                                                           //显示最后一次提交信息
>
> lg : "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"                   //显示分支、ci、创建时                                          间、创建人



---

### 搭建Git服务器

教学链接：https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664