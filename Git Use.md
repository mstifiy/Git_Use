## 版本库基础操作

```bash
# 新建文件夹
mkdir repository_name & cd repository_name
# 初始化库
git init
# 添加文件到仓库
git add <file>
# 提交文件到仓库
git commit -m <message>
# 查看仓库状态
git status
# 查看文件修改信息
git diff <file>
# 版本回退，HEAD指向当前版本，HEAD^上一个版本，上n个版本HEAD~n
git reset --hard HEAD^
# 查看历史命令
git reflog
# 查看提交历史
git log
```

![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)

> stage（或者叫index）为**暂存区**

```bash
# 丢弃工作区的修改，git checkout用版本库里的版本替换工作区的版本
git checkout -- <file>
# 撤销暂存区的修改，并重新放回工作区
git reset HEAD <file>
# 删除暂存区中的文件
git rm <file>
```

## 远程仓库操作

```bash
# 关联远程仓库，origin为给远程库指定的名字，可随意命名
git remote add origin git@github.com:<user_name>/<repository_name>.git
# 推送master分支到远程仓库
git push -u origin master #第一次
git push origin master	#非第一次
# 删除与远程库的绑定
git remote -v #查看远程库绑定信息
git remote rm <name>
```

## 多人协作

```bash
# 克隆远程仓库
git clone ssh_link(recommend)/https_link
# 分支管理
git branch	# 查看分支
git branch <name>  # 创建分支
git checkout <name>或git switch <name> 	# 切换分支
git checkout -b <name>或者git switch -c <name>	# 创建+切换分支
git merge <name>	# 合并分支[用于合并指定分支到当前分支]
git branch -d <name>	# 删除分支
git branch -D <name>	# 强行删除分支
# 查看分支合并图
git log --graph
# 普通合并模式（非快进）
git merge --no-ff -m "merge with no-ff" dev # 合并后的历史有分支，能看出来曾经做过合并
```

![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

- `master`分支保持稳定，仅用来发布新版本，平时不能在上面干活。
- 开发者都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

### 多人协作流程

```bash
# 克隆工作分支，一般是dev分支
git clone -b <指定分支名> <远程仓库地址>
# 默认克隆
git clone <远程仓库地址>
git checkout -b <branch-name> origin/<branch-name>	# 创建本地分支，名称最好和远程一致
git branch --set-upstream <branch-name> origin/<branch-name> # 建立本地分支和远程分支的关联
# 提交分支
git push origin <branch-name>
git pull	# 抓取远程提交并合并
```

