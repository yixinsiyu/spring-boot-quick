##Gitee(码云)、Github同时配置ssh key

一、创建gitee和github的ssh key
cd ~/.ssh
ssh-keygen -t rsa -C "xxxxx@xxxxx.com"

替换正确的邮箱，按enter

Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/FlyingHorse/.ssh/id_rsa): id_rsa.gitee
创建gitee的ssh key时输入id_rsa.gitee，创建github的ssh key时输入id_rsa.github

Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in id_rsa.gitee.
Your public key has been saved in id_rsa.gitee.pub.
The key fingerprint is:
SHA256:lmjU8A4k+r6liYJmENBPM/7Frx3XDg98VeWvIQ9dLyw xxxxx@xxxxx.com
The key's randomart image is:
+---[RSA 2048]----+
| .  . o         o|
|. ..+o +       ..|
|. .+ oo.o       +|
|.  .o. +o.   o .+|
| .  ..o.S. .E.=.o|
|.  . ...  o ==o+ |
|o   . .  o o *o  |
|oo . =  . .   o  |
|o.. +            |
+----[SHA256]-----+
一路按enter，知道输出如图

二、把public key复制到gitee或github
cat id_rsa.gitee.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZbvgUEj3XAXH4HkW27ibdXgV6VHdrA9/WdSDHtiiC55mjPvxj3OtPxIbpeJmhWyHiJWR6
uUuK+gkb//O51uWCPhHqxKR7+45tZ9jHqXW+hEKPp+odQgc+3hiHAjTkn3JGeIJlQp2UdJCDHBrp+kcgVeg91+y7cU3ufaUQ/hpD
rCgn6uvwjwJgnDhV9DYi+gFUFe7LUwa1o4nfwg43ycuOOuT7c6VO2dj/0pLRUVTPQYu/C3kaaPVedir7mKIu/dM6Ec44bhYTp1Dq
qp8BO42Cfo+n+dempqYTe2wcPvuDjSj884IATc/KvBfc86Yd2Uj7NI7li90Y3i6adoxUIWQh xxxxx@xxxxx.com
查看公钥，gitee输入id_rsa.gitee.pub，github输入id_rsa.github.pub

将第二行到结尾的内容复制到gitee或github的ssh中保存

三、创建配置解决ssh冲突
在.ssh文件夹中创建config文件，添加以下内容以区分两个ssh key

# gitee
Host gitee.com
HostName gitee.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa.gitee

# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa.github
四、测试连接
输入

ssh -T git@gitee.com
若返回如下图，则gitee则连接正常

Welcome to Gitee.com, yourname!
输入

ssh -T git@github.com
若返回如下图，则github则连接正常

Hi yourname! You've successfully authenticated, but GitHub does not provide shell access.