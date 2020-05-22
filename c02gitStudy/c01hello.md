#git学习
1.简介
    Git是目前世界上 最先进 分布式版本 控制系统（没有之一）。
2.运行原理
    Git没有客户端服务器端的概念，但是要把找个机器当做“中央服务器”仓库，方便“交换”修改。
3.中央服务器搭建
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
   
4.git客户端安装和使用
    1.window版本
        1.下载 一路默认安装
        2.界面使用   git bash
            1.右键git bash，输入如下，本机所有Git仓库都会使用这个配置
                $ git config --global user.name "Your Name"
                $ git config --global user.email "email@example.com"
            2.创建本地仓库，进入目录后，git bash输入 git init
                会出现.git目录
            3.添加文件到本地仓库
                git add readme.txt 文件2 文件3
                git commit -m "提交说明"
            4.什么撤销、修改、删除文件，用idea中的
            
            
                