---
title: mac高效工具配置
tags: []
date: 2016-04-12 08:00:00
---

### vim语法高亮

在vim中输入命令:syntax on激活语法高亮，若需要Vim启动时自动激活，在~/.vimrc中添加一行syntax on即可。

### iterm2 + zsh

step1.安装iterm2
    
[https://www.iterm2.com/](https://www.iterm2.com/)

step2.安装zsh, oh-my-zsh

[http://macshuo.com/?p=676](http://macshuo.com/?p=676)

step3.设置默认shell为zsh

    chsh -s /bin/zsh

### chrome lastpass插件

    记住网站密码，不用重复输入密码
    
### ssh免密码登录 [参考](http://dhq.me/use-ssh-config-manage-ssh-session)


step1.生成密钥 

    ssh-keygen -t rsa -C "caijinlin2012@gmail.com"
    这里使用 rsa 的加密方式（另外一种加密方式是 dsa），中间会询问密钥生成的位置，这里只输入 cjb，在当前位置生成名为 cjb 的密钥，接着会询问是否要设置一个密码(passphrase)，这里留空，直接按回车就行（本来就不想登陆输入密码了...），最后，会在当前目录路径下生成一个名为 cjb 的私钥，一个名为cjb.pub 的公钥。

step2.上传公钥到服务器 (如果方法一不行采用第二种)
    
    方法1.使用ssh-copy-id 
        安装ssh-copy-id: curl -L https://raw.githubusercontent.com/beautifulcode/ssh-copy-id-for-OSX/master/install.sh | sh 
        ssh-copy-id i ~/.ssh/cjl.pub root@182.92.5.70

    方法2.
        把公钥 cjb.pub 上传到远程 cjb 服务器的 ~/.ssh/ 目录下：
        scp cjl.pub root@182.92.5.70:~/.ssh/
        上传完后，登录到服务器，把公钥 cjb.pub 的内容复制到 authorized_keys 文件里（不存在则新创建一个）：
        cat cjb.pub >> authorized_keys

step3. 加入配置文件

    ~/.ssh下新建配置文件config
        Host        cjb
            HostName        216.194.70.6
            Port            22
            User            user
            IdentityFile    ~/.ssh/cjb  
        Host        cjh
            HostName    182.92.5.70
            Port        22
            User        user

step4. ssh cjh 

        登录成功说明免密码登录成功了


###  sublime过滤文件夹搜索

    sublime text => Preferences => Setting - User 加入配置，过滤文件夹和文件类型

    "folder_exclude_patterns": ["Runtime", "._d", ".metadata", ".settings"],
    "file_exclude_patterns": ["*.pyc", "*.pyo", ".project"]

