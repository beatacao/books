# git 基础

## 获取Git仓库   
    
    1、在现有项目根目录下初始化：git init; git add; git commit   
    2、克隆已有仓库： git clone  
    
## 查看已暂存和未暂存的修改   

    git status: 简单列出已暂存和未暂存文件名   
    git diff ： 列出修改的具体信息； 不加任何参数，只列出未暂存修改信息；添加参数 --staged 或 --cached 列出已暂存修改信息   

## git commit -a 跳过暂存直接提交  

## git rm: 移除文件； git rm --cached xxx: 不再跟踪

## 重命名：git mv 等同于： mv , git rm, git add三条命令  

## 撤销操作   

    . get reset HEAD <file>: 撤销对某个文件的暂存；注意：不加 --hard 参数只会修改暂存区，添加--hard参数后，该命令非常危险，可能会导致丢失工作目录中所有当前进度    
    . git checkout -- <file>: 会丢失当前修改，因为该命令仅仅是copy另一个版本的文件覆盖当前文件。  
    


