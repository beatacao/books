一、 mac 终端 git clone 报错  

    ssh: connect to host github.com port 22: Operation timed out
    fatal: Could not read from remote repository.

    Please make sure you have the correct access rights
    and the repository exists.  

1、 分析：  
输出信息prot 22: Operation timed out，初步分析端口问题我们修改端口试试，这里将端口改为443。   

2、 解决方法：  
在存放私钥公钥（id_rsa和id_rsa.pub）文件里，新建config文本。命令vim ~/.ssh/config,输入一下内容：  

    Host github.com  
    User YourEmail@163.com  
    Hostname ssh.github.com    
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id_rsa  
    Port 443  

保存退出。  
目前，还不能使用，需要最后设置config：  

    git config --global user.name "XXX"
    git config --global user.email XXX@xx.com

这个操作就是为了刷新config，使修改生效。
