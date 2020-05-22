#svn学习
1.简介subversion
    SVN是一个 开源、集中式 版本控制系统。
2.运行原理
    多人都把代码放在svn服务器上，通过svn服务器来交互工作。
3.SVN服务端安装安装和使用VisualSVN Server
    1.window版本
        1.下载VisualSVN Server，网址为https://www.visualsvn.com/downloads/
        2.安装 选择 VisualSVN Server AND administrator tools 和 add 添加环境变量 
            指定安装路径 备份路径 仓库路径 port为8443
            选择SVN认证
        3.界面使用
            1.左边 仓库、用户、组、任务。了解仓库、用户、组就可以。
            2.新建仓库
                使用FSFS仓库-》空仓库-》指定权限 
                仓库地址为 ip:8443/svn/仓库名
                https://127.0.0.1:8443/svn/avfms
            3.新建用户和组
            4.为仓库指定权限，properties。
4.SVN客户端安装和使用TortoiseSVN
    1.window版本
        1.下载 TortoiseSVN
        2.安装 改变下安装路径就可以，然后一路下一步
        3.界面使用  
            1.checkOut检出服务器的仓库    https://127.0.0.1:8443/svn/avfms
                检出深度，使用默认的 fully recursive，检出版本，默认的最新的 head
                需要验证用户名和密码
                检出后，会有个.svn文件。
            2在本地仓库中添加、修改了文件后，commit提交文件到服务器的仓库中
                在本地仓库中右键，有提交选项，弹出页面，输入提交message，然后提交。文件就同步到服务器的仓库中了。
            3.更新本地仓库中
                在本地仓库中右键，更新，则会与服务器的仓库同步
                