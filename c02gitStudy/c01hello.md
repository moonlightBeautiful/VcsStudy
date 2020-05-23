#git学习
1.简介
    Git是目前世界上 最先进 分布式版本 控制系统（没有之一）。
2.运行原理
    Git没有客户端服务器端的概念，但是要把找个机器当做“中央服务器”仓库，方便“交换”修改。
3.中央服务器搭建远程仓库
    找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上
    ，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。
    1.window版本
        1.git的安装很复杂，在linux下很简单。 
        2.Git的云托管平台 GitHub
            只支持git作为唯一的 仓库格式 进行托管 的 托管平台。
        3.Git 搭建自己的托管平台 gogs 
            1.下载、安装git（bash）：服务端和客户端均需版本 >= 1.8.3
            2.下载NSSM用于注册Windows服务：https://nssm.cc/download
                解压并添加到系统变量中
                "控制面板" --> "高级系统设置"--> "环境变量"--> "系统变量"-->"Path"
                在"变量值"项目添加NSSM文件路径"D:\nssm-2.24\win64"(记得在路径前添加半角";")
            3.下载gogs 解压、配置：
                1.执行scripts下的mysq.sql
                2.新建代码仓库目录：D:\gogs\scripts\repository\avfms
                3.修改系统安装文件D:\gogs\scripts\windows\install-as-service.bat
                    SET gogspath=D:\gogs (按实际安装目录修改)
                4.以管理权限运行安装脚本：install-as-service.bat
                    会发现多了服务gogs
            4.浏览器输入http://127.0.0.1:3000/
                设置一下：数据库、仓库根目录、URL地址、端口号、管理员账号
                数据库选择SQLite3
            5.设置完之后，登陆地址为http://localhost:3000/       
    2.linux版本
        1.git作为中央服务器
            其实就是在linux上安装git，然后设置公钥让别的机器可以访问仓库
            1.中央服务器上安装Git，初始化Git仓库
            2.本地电脑把公钥给中央服务器上
            3.客户端克隆中央服务器仓库
                $ git clone git@中央服务器ip:/home/.../中央服务器仓库.git
   
4.git本地仓库
    1.window版本
        1.下载 一路默认安装
        2.界面使用，右键 git bash
            1.本机所有Git仓库配置用户名和邮箱
                $ git config --global user.name "Your Name"
                $ git config --global user.email "email@example.com"
5.git命令学习
    0.简介
        git的仓库包含 工作区+版本库（.git目录=暂存区+分支） 
        Git中，用HEAD表示当前版本
    1.创建本地仓库
        进入文件夹后，输入：
        git init
        会出现.git目录，这个目录就是版本库
    3.添加文件到分支
        先添加到暂存区： git add readme.txt
        再提交到分支：git commit -m "add readme file"  只会把暂存区的内容保存到分支上
    4.查看仓库状态：会显示工作区、暂存区的修改的文件
        git status  
    5.查看HEAD到最开始的交日志
        git log --pretty=oneline
    6.查看分支上的HEAD移动的历史命令：
        git reflog
    7.版本回退：工作区回退到分支上的某一次提交点，并清空暂存区。
        git reset --hard commit版本号
    8.撤销修改：
        撤销工作区的修改：工作区某个文件恢复到版本库（暂存区或分支）的最新状态，不会清空暂存区。
            git checkout -- readme.txt
            我尝试了，必须指定某个文件撤销，-- readme.txt
        撤销暂存区的修改：清空暂存区
            git reset HEAD readme.txt   
            或者
            git reset HEAD
    9.删除文件到分支
        1.git rm test.txt
        2.git commit
        如果误删，再版本库中从新检出一份git checkout -- test.txt
6.远程仓库
    本地库与远程库关联：远程仓库的默认名称是origin
        1.先有本地库，后有远程库，本地库关联远程库。
            git remote add origin(远程仓库名) 地址/仓库名.git
        2.直接从远程库克隆一个本地库，自动关联本地的master分支和远程的master，默认只克隆master分支到本地
            git clone 地址/仓库名.git
    本地库分支所有提交推送到远程库分支：要指定远程分支
        git push -u origin master
        第一次推送要使用 -u，本地库master与远程库master关联，以后可以不使用 -u了。
    把远程库分支最新的提交同步下来
        git pull
    查看远程库的信息
        git remote
    
7.分支
    1.创建一个分支：其实新建了一个指针叫dev，指向master相同的提交。
        git checkout -b dev = git branch dev  + git checkout dev
            -b 是切换到创建的dev分支，不+ -b，则不会切换。
    2.查看所有分支
        git branch
    3.分支合并：
        git merge 需要合并的分支dev  ：如果没有冲突，则把当前分支的指针 指向 需要合并的分支的指针上
        git merge --no-ff 需要合并的分支dev  ：为当前分支创建一个新的提交点，其实就是把 当前分支的指针 指向 需要合并的分支的指针上则
    4.删除指定分支
        git branch -d 指定分支dev  
        貌似必须在其他分支上操作删除指定分支
    5.切换分支 -c 创建分支
        git checkout = git switch 用来切换分支
        git switch -c 切换到的目标分支并新建分支
    6.解决冲突
        当两个分支合并的时候 或者 本地库推送内容到远程库时， 同一个文件可能存在冲突
        修改有冲突的文件后才能 合并或者推送
    7.分支策略
        1.master分支应该是非常稳定的，也就是仅用来发布新版本
        2.dev分支上用来干活，开发。到了某个版本发布时，在合并到master上。
            只接从远程库克隆一个本地库，自动关联本地的master分支和远程的master，默认只克隆master分支到本地。
            需要手动创建开发分支并与远程分支的开发分支关联
            git checkout -b dev origin/dev
        3.bug分支，一般是新版本出现bug，需要修复
            正在dev分支上v2版本，突然v1版本有个bug需要修复。
            1.先在dev分支上保存所有未提交的修改（工作区和暂存区）到堆栈中
                git stash save '备注''
            2.在需要修复的版本创建bug分支
                git checkout -b bug-001
            3.修复bug后，切换到master上，合并bug分支，删除bug分支
                git switch master
                git merge --no-ff -m "修复bug..." bug-001
                git branch -d bug-001
            4.切换到dev分支，把堆栈中保存的所有未提交的修改（工作区和暂存区）恢复，干活
                git switch dev
                git stash pop
        4.rebase操作可以把本地未push的分叉提交历史整理成直线
    8.标签管理  
        其实就是给commit取个名字
        创建标签，在本地创建，需要推送到远程
            git tag v1.0    默认打在最近的提交上
            git tag v0.9 提交id   指定提交打标签
            可以指定为标签指定说明
                git tag -a 标签名 -m "说明" 
        查看所有标签，标签不是按时间顺序列出，而是按字母排序的
            git tag
        查看指定标签带说明
            git show 标签名
        删除标签
            git tag -d 标签名    仅仅删除的本地标签
            删除远程标签 git push origin :refs/tags/标签名
        推送标签到远程分支
            标签都只存储在本地，不会自动推送到远程
            git push origin 标签名             送指定标签
            git push origin --tags            推送全部标签
            
            
        2
        
         
        
        
    
            
    
                
                
                    

                
                
            
            
                