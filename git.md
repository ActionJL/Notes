### 连接两个互不相关的两个仓库
##### 初始化git版本管理
git init  
***
##### 添加当前项目到暂存区
git add *
***
##### 提交到本地仓库
git commit -m 'local repository'
***
##### 建立本地仓库与远程仓库的连接
git remote add origin <remote repository name>
***
##### 将远程仓库的内容合并到本地
git pull origin master --allow-unrelated-histories
***
##### 将本地内容一并提交到远程仓库
git push origin master:master
***

##### 强制将本地仓库推送到远程仓库
git push -f origin master
***
