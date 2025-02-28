参考视频  
https://www.bilibili.com/video/BV1s3411g7PS/?spm_id_from=333.788.top_right_bar_window_history.content.click&vd_source=b9c639db66d1d92699bdd73eff797082  
https://www.bilibili.com/video/BV1HM411377j?spm_id_from=333.788.videopod.sections&vd_source=b9c639db66d1d92699bdd73eff797082  


### 1.首先下载git (for windows)

https://git-scm.com/downloads/win  
这里会自动安装其命令行工具git bash, 接下来的命令操作均在**git bash**进行
### 2.创建本地仓库  
在本地创建一个文件夹用于本地仓库  
这里我创建的仓库目录为 /E/gitrepo  
在该文件夹下右键选择用git bash打开可以直接操作当前目录
![img.png](img.png)

为当前git配置 name 和email（随意即可）
`git config --global user.name"Zorin"`  
`git config --global user.email "XXXXXXX@qq.com"`  
在当前仓库下初始化  
`git init`

### 3.将git和github进行连接(通过SSH)
为git生成一对密钥用于SSH连接认证
将密钥文件生成于默认路径C:\Users\Dandelin\.ssh(gitbash中：~/.ssh)
```
$ssh-keygen 
# 提示输入保存路径时直接回车保存在默认路径（不保存在默认路径会导致git不能识别）
#Enter file in which to save the key (/c/Users/YourUsername/.ssh/id_ed25519): 
# 提示输入密码时回车表示无密码（可选）
#Enter passphrase (empty for no passphrase): 
#Enter same passphrase again:
# 生成完成
```
最终会生成两个文件.pub后缀的为公钥，打开复制里面的公钥内容  
![img_1.png](img_1.png)  

打开github 点击右上角头像处 选择Setting  
![img_2.png](img_2.png)  
打开SSH and GPG keys  
![img_3.png](img_3.png)  
创建SSH key ，并将git生成的公钥内容粘贴即可  
![img_4.png](img_4.png)  

### 4.关联远程仓库
选择github上需要关联的仓库，查看并复制github的SSH连接  
![img_5.png](img_5.png)  
在git bash 中将git于github上的仓库关联  
`git remote add origin git@github.com:Zorinman/K8S.git  ` origin为github上需要关联仓库的名字 可自行修改（如我的为K8S）  

**建议一个本地仓库对应一个远程仓库**（也可以在一个本地仓库路径下使用git remote add 添加多个远程仓库 ）
### 5.推送，拉取仓库内容

git有三个分区 分别成为工作区 暂缓区 本地仓库  ，当在本地commit之后才可以将内容推送至远程仓库  
首先将工作区的内容添加至暂缓区，完成修改后最后提交至本地仓库。
![img_6.png](img_6.png)

 将本地仓库内容推送至github的某个仓库 `git push 远程仓库名称 远程分支名：本地分支命`     
 将github某个仓库拉取至本地 `git pull 远程仓库名称 远程分支名：本地分支命`  
以上的仓库名称和分支命均可以省略，省略则默认为origin main:main
**速度慢解决方案参考 git clone pull push速度慢解决**