**与`git的使用.md`中的流程类似**
⭐第一次拉取和推送使用-u如`git push -u origin main`和`git pull -u origin main`这表示设置默认上游分支，后续就可以直接`git pull` 和`git push `不用加远程仓库名和分支名

1.安装git

2.初始化本地仓库可以直接在VScode的源代码管理中点击`初始化仓库`

-------
# 个人测试：

3.**将git于github上的仓库关联**
 `git remote add origin git@github.com:Zorinman/K8S.git`   origin为github上需要关联仓库的名字 可自行修改（如我的为K8S）

4.**本地分支与远程分支名字保持一致（个人）**
如需要：`git branch -m master main` 重命名本地主分支master为main

5.**同步本地仓库和远程仓库开始推送**

**本地仓库完全覆盖远程仓库（丢弃远程所有内容，强制同步本地内容）**

`git push -u origin main --force` (origin是远程仓库名，main是远程分支名)

**远程仓库完全覆盖本地仓库（丢弃本地所有内容，强制同步远程内容）**
本地仓库已经初始化并有提交删除等信息：`git pull origin main --force` 强制拉取远程 main 分支，覆盖本地冲突文件

**远程仓库或者本地仓库一方完全为空**  
**情况1.本地仓库完全为空**：`git clone 仓库Https\SSH`  
后续直接`git push -u origin main` 和`git pull  -u origin main`
**情况2 远程仓库完全为空**  
直接 `git push -u origin main`

---------------

# 团队开发：
3.**先克隆团队项目到本地仓库** `git clone 仓库Https\SSH`

4.**关联远程仓库** `git remote add origin 仓库Https\SSH`

5.**在本地创建并切换到新分支（避免直接修改 main分支）**
`git checkout -b <新分支名>`

6.**git commit -m 提交本地修改**

7.**推送到远程仓库**
推送前再进行一次同步 防止远程 main 分支在这期间可能有新更新
``` shell 
git checkout main                  # 切换到主分支
git pull origin main               # 拉取远程最新代码
git checkout feature/your-feature-name  # 切回你的分支
git merge main                     # 将主分支更新合并到你的新分支
```

`git push -u origin <新分支名>`
这时候远程仓库会自动创建这个新分支

8.**发送合并请求**
在github远程仓库页面选择你的新分支，点击进行合并请求， 团队成员审核后，代码会合并到主分支（如 main）
