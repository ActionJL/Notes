#### 连接两个互不相关的两个仓库

git init

git add *

git commit -m 'local repository'

git remote add origin <remote repository name>

git pull origin master --allow-unrelated-histories

git push origin master:master