#git学习
1.简介
    Git是目前世界上 最先进 分布式版本 控制系统（没有之一）。
2.运行原理
    每个人的git仓库都可以当做服务器仓库，但是会有一台当做“中央服务器”仓库，为了方便“交换”修改。
3.git服务端安装和使用
    1.window版本
         1.下载 一路默认安装
                2.界面使用  
                    1.右键git bash，输入如下，本机所有Git仓库都会使用这个配置
                        $ git config --global user.name "Your Name"
                        $ git config --global user.email "email@example.com"
                    2.创建仓库，进入目录后，git bash输入 git init
                        会出现.git目录
                    3.添加文件到仓库
4.git客户端安装和使用