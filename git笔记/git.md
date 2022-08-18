# Git简易的简易命令行入门 #
## Git全局设置
设置用户名  
``` github
git config --global user.name "xifan"
```
设置用户邮箱
```
git config --global user.email "2329197332@qq.com"
```
## 创建本地git仓库 ##
创建仓库文件夹  
```
mkdir [文件夹名]
```
进入到文件夹目录
```
cd [文件夹名]
```
初始化仓库
```
git init  
## 提交文件 ##
```
添加文件或文件夹到暂存区（文件夹包括里面的所有文件）  
**注意**：使用git上传文件夹一定要注意,文件夹里面至少有一个文件,因为git不能管理空文件夹 所以上传就会不成功
```
git add [文件名]
git add .[文件夹名]
```
将暂存区的文件添加到本地仓库
```
git commit -m "[提交说明]"
```
关联远程仓库的
```
git remote add origin [仓库地址]
```
将本地分支版本与远程仓库合并
```
git push -u origin "master"
```
