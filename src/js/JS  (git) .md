# git账号:2974464448@qq.com
     密码：zf18756371756
     http://fast.hsw.cn/

# VPN 
     账号：zhangfeiyizhou
     密码：zf18756371756

# 一.命令行操作：
1.cmd里面的叫做DOS命令（磁盘操作系统）

     cmd终端唤醒：win键+R，输入cmd回车

     目录的创建和删除：
                  mkdir ：创建目录
                  rmdir：删除目录
                  copy con A.tet:创建A.txt文本文件   ctrl+z回车：结束

     输入d：进入d盘

     dir:列出当前目录的列表（那些文件）

     cls：清空终端命令

     del 文件名: 删除某个文件

     cd+目录名:进入目录

     cd..:返回上一级目录

     tab：补全（联想单词）



2. 安装git软件，git用的是linux命令（一路next,直到结束）
window系统，任意目录，右键选择git，bash进入linux命令操作

cd 目录名：进入目录

mkdir 创建目录

rmdir 删除目录

ls 查看当前目录列表，或dir

clear 清空当前控制台

rm -rf 文件名：删除一个文件或目录

cat 文件名：打开文件

touch 2.txt,如果2.txt不存在，则创建空文件2.txt

cd ../返回上一级，注意后面的空格

不管DOS命令还是linux命令，通过方向键将输入的命令显示出来

输入ipconfig，DOS还是linux,都可以查看ip地址



# 二.版本管理工具
1. 版本管理工具：团队协助开发，每一次提交记录为一个版本

2. git:分布式的，每一个用户都有服务器（本地），git是一个分布式的版本控制系统，在git中即使用户离线，也能进行项目的提交和更新操作（本地服务器），等到下一次连线中央服务器时进行整体的同步操作



# 三.git相关操作
1. master(主分支)->设置子分支（自己开发的分支）->子分支开发完成->合并到主分支
      --master：代码库应该又有一个，且只有一个主分支，所有使用的正式版本，都在这个主分支上发布，Git主分支的名字，默认叫做main，它是自动建立的，版本库初始化之后，默认就是在主分支上进行开发的
      --Develop:滴定仪的开发分支，主分支只用来分布重大版本，日常开发应该在另一条分支上完成，我们把开发用的分支，叫做Develop，这个分支可以用来生成的最新隔夜版本，如果想正式发布，就在main分支上，对Develop分支进行合并（merge）

2. 无需创建中央服务器(gielab)，使用第三方的网站实现，利用github创建中央服务器（仓库）
      --第一步：进入github注册
              1.输入邮箱
              2.等待邮箱给的验证密码
              3.设置密码

      --第二步：创建仓库（服务器）


# 四.git创建远程仓库https
1. 右上角 +
2. 点击 New repository :新建一个仓库
3. Repository name ：仓库名称（唯一性）
4. Description (optional) ：仓库的描述：可以打中文
5. Public ：公用仓库
6. Add a README file （打钩）： 自动生成一个可读文件，里面是仓库的名称和描述
7. Add .gitignore （打钩，输入node）：  提交时，忽略的本地代码
8. Choose a license (MLT )：设置证书
9. Code.https仓库的地址
10. 打开Visual相应的文件
11. 在命令行中输入git clone https地址（克隆）
12. 在命令行中输入git pull(防止新的修改进来)
13. 在命令行中输入git add .（工作区->暂存区）
14. 在命令行中输入git commit -m '注释'（暂存区->本地服务器）
15. 在命令行中输入git push（本地服务器->远程仓库）


# 四.git分支以及常用的命令
第一步：点击 New repository :新建一个仓库

第二步：点击Code,选择https或ssh：：：连接仓库的地址（克隆仓库的地址）：https和ssh

第三步：https:将本地的代码同步到远程仓库中（github）
    --输入：git clone 空格Code.https仓库的地址，回车键，就会把刚才创建的远程仓库的代码克隆到相应的本地文件中，同时本地和远程仓库进行了连接

第四步：将本地工作区的内容提交到远程仓库（工作区->暂存区->本地服务器->远程仓库）
#    1.--输入：git status:查看状态--对比工作区和本地服务器的区别
    案例：
PS D:\rrrrr.js> git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
   (use "git add <file>..." to include in what will be committed)
         index.html.txt -----------------（新加的文件--红色）

nothing added to commit but untracked files present (use "git add" to track)
   PS D:\rrrrr.js>

#   2.--输入git add（空格）.（点）:将新增的或修改的文件提交到暂存区（暂时存放，方便撤回），命令后面的点，表示所有文件
   案例：
       PS D:\rrrrr.js> git add .

#      再次查看（对比工作区和本地服务器的区别）git status
PS D:\rrrrr.js> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
(use "git restore --staged <file>..." to unstage)
     new file:   index.html.txt-----------------（新加的文件--绿色）

PS D:\rrrrr.js>

#    3.--输入git commit(空格)-m(空格)"提交的注释"：将暂存区的文件提交到本地服务器
   案例：
PS D:\rrrrr.js> git commit -m "新增了一个轮播图"
Author identity unknown

*** Please tell me who you are.

Run

git config --global user.email "you@example.com"
git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got '俊杰@DESKTOP-9OSN0MR.(none)')
PS D:\rrrrr.js>

#   4.第一次提交，git会提示你，输入邮箱和用户名
    git config --global user.email"2974464448@qq.com"：邮箱
    git config --global user.name "zhangfeiyizhou"   ：用户名

#   5.如果想查看自己的邮箱和用户名
    git config --list

#   6.--输入git origin main:将本地服务器同步到远程仓库
    git push origin main（origin：远程仓库的默认名称，main：主分支）



# 五.git创建远程仓库:ssh(秘钥)
     ----通过秘钥和私有进行匹配，一旦匹配上了，后续一直保持连接状态
         1.生成2个秘钥
         2.将公钥给匹配的giehub网站
         3.私钥放置在本地


         1.在D盘传建一个文件
         2.打开Visual文件，选择D盘中建立的相应文件
         3.按Ctrl+~键(终端命令行中编写文件，将写的文件：HTML/CSS/JS文件放入Visual目录中，)
            输入cd github项目名

         4.git config --global uaer.name '用户名'
         5.git config --global uaer.email '邮箱'
         6.git config --list（查看所有配置） q键退出

         7.输入：ssh-keygen -t rsa -C '邮箱' 一直按回车键，直到结束，生成ssh
         
         8.去c盘->用户->.ssh->id_rsa  复制公钥

         9.进入github网站，点击右上角图片，选择settings,点击左菜单SSH and GPG keys

         10.点击SSH keys 的 Add SSH keys

         11.Title:(标题)--顺便取

         12.在Key中粘贴公钥，点击Add SSH keys

         13.输入github密码

         14.点击右上角的图片，点击Your repositories(我的项目)

         15.点击相应的项目

         16.点击Code的SSH地址，拷贝地址

         17.打开命令行输入git clone 单击右键，输入yes（克隆了）
#           注意：输入cd gitpub的项目名称,然后把写的文件拖入到gitpub的项目名称中

         18. 在命令行中输入git pull(防止新的修改进来)

         19. 在命令行中输入git add .（工作区->暂存区）
          
         20. 在命令行中输入git commit -m'注释'（暂存区->本地服务器）
          
         21. 在命令行中输入git push origin +主分支的名称（默认main）（ 本地服务器->远程仓库）

# 六.如何代码删除了，如何恢复（一旦出现问题，千万不要去删除远程的仓库）
1.git log命令，回车键
2.git reset --hard commit_id 退回，复制commit_id的随机哈希值（前8位即可）按回车键
3.git push origin head --force  强行推倒远程服务器


# 七.git分支
1. git branch 创建分支

2. git checkout 切换分支

3. git branch 查看分支

4. git merge 分支合并
案例：
   第一步：cd +目录（进入目录）
   第二步：git branch +分支名称（创建分支）
   第三步：git branch（查看分支）
   第四步：git checkout +分支名称（切换分支）
   第五步：git add .（工作区->暂存区）
   第六步：git commit -m'注释'（暂存区->本地服务器）
   第七步：git push origin +子分支的名称（ 本地服务器->远程仓库）
   第八步：先切换到主分支，再合并：git checkout main(主分支)
   第九步: git merge +子分支名称

5. 现在建一个一个主分支和一个子分支，而且（主分支和子分支的内容一致）

6. 想要切换主分支：git checkout +主分支名称

7. 想要切换子分支：git checkout +子分支名称

8. 在子分支里，添加书写的文件

9. 再上传到子分子：git add . ,git commit -m""，git push origin 子分支名称

10. 再将子分支传给主分支：git merge +子分支名称

11. 再切换主分支：git checkout +主分支名称

12. 再将主分支上传：git add . ,git commit -m""，git push origin 主分支名称

13. 查看girpub内主分支和子分支内容是否一致

14. 如果想在主分支中输入内容，先切换到主分支：git checkout +主分支（直接在文件中写）

15. 如果想在子分支中输入内容，先切换到子分支：git checkout +子分支（直接在文件中写）


# 八.主分支比子分支的内容多
     ----git pull origin +主分支的名称:   更新主分支代码

1. 如果主分支的内容比子分子的内容多（同事新增的）

2. 先更新，主分支的内容：git pull origin main(主分支)

3. 再，切换子分支：git checkout +子分支名称

4. 用子分支来合并主分支，取主分支多的内容：git merge +主分子

4. 再,git add . ,git commit -m""，git push origin 子分支名称

5. 查看girpub内主分支和子分支内容是否一致


# 九.将本地目录变成远程仓库
    --前面的操作是：先创建远程仓库，然后将远程仓库克隆到本地
    --当前的操作是：将本地的任何目录都，同步到远程仓库

    git init (初始化)
    git add .
    git commit -m ''
    git remote add origin +远程仓库地址（当前目录与远程仓库连接）
    git pull --rebase origin main（更新连上的远程仓库文件）
    git push -u origin main
      --上面的命令仅仅是将本地开发目录变成远程仓库，其他的更新提交操作和前面的命令是一样的

1. 首先在D盘建立一个目录

2. 打开Visual进入相应的目录，Ctrl+~键打开命令行

3. 打开gitpub建立一个项目名称...

4. 复制远程仓库地址

5. git init (初始化)

6. git add .,git commit -m ''

7. git remote add origin +远程仓库地址（当前目录与远程仓库连接）

8. git pull --rebase origin main（更新连上的远程仓库文件）

9. git push -u origin main

