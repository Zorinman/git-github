
# HTTPS  
配置当前用户的全局 Git 配置，即写入到 ~/.gitconfig 文件中，所有git都走代理
git config --global http.proxy http://127.0.0.1:7890  
git config --global https.proxy http://127.0.0.1:7890  



# SSH
由于防火墙原因导致速度过慢  
我们可以使用工具利用Clash来配置代理使速度提高
![img_7.png](图片/img_7.png)

由于这里使用的是SSH连接 所以我们需要在git中对其SSH的config文件进行配置  
config文件默认路径为C:\Users\Dandelin\.ssh（gitbash中：～/.ssh)  
config文件默认不存在 我们需要在默认路径下创建 并且将代理地址设置为**127.0.0.1:7890**(7890为主机中监听clash的端口,如上图)  
```
$touch config  #创建config文件
$vim config    #编辑config文件
#添加以下内容:
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    ProxyCommand ncat -x 127.0.0.1:7890 %h %p
```

由于SSH代理需要使用 ncat 所以需要在git 中安装ncat，在以下连接下载ncat的静态编译版本
https://nmap.org/ncat/
![img_8.png](图片/img_8.png)

下载完成后需要编辑环境变量添加`ncat.exe`的所在路径，也就是`/E/netcat/`  

查看是否成功添加路径  
```
$ which nc
/E/netcat/nc

```
成功配置.

⭐注意 使用SSH连接如果你为了解决拉取速度慢在 `~/.ssh`的config文件中配置了代理加速， 那么你需要 `ncat`走代理带能拉取推送远程仓库，我们还需要下载`ncat`并且编辑环境变量中添加`ncat.exe`的所在路径（下载请看git clone pull push速度慢解决.md)
⭐使用HttpS时如何连接的是私人仓库必须要带token，此时更推荐ssh