

# 一.git 本地文件

1. git init  ：初始化 

2. git add . ：上传暂存区

3. git commit -m '' ：上传本地仓库

4. git status ：查看git的状态

5. git diff ：查看版本的差距

6. git reset HEAD^：退回一个版本

7. git reflog ：查看所有的历史记录

8. git push ：上传到远程仓库

9. git pull ：查看git的状态



# 二.git分支

1. git branch  ：查看分支 

2. git branch 分支名称 . ：创建分支

3. git checkout 分支名称 ：切换分支

4. git checkout -b 分支名称 ：创建并切换到这个分支

5. git merge 被合并的分支名称 ：合并分支

             b分支的内容合并给a分支：
                                 1. 先切换到a分支
                                 2. 命令行： git merge b


6. git branch -d 分支名称 ：删除分支

             a分支已经有b分支的内容了，所以要删除b分支：
                                 1. 先切换到a分支
                                 2. 命令行： git branch -d b //删除b分支




# 三.git 创建项目

1. 打开githup 创建一个项目

2. 选择 http 或 秘钥

3. 在命令行中输入git clone https地址（克隆）
