# docker笔记
## docker的安装
1. 启用Windows功能：
   * 打开“控制面板”，选择“程序”，然后点击“启用或关闭Windows功能”。
   * 在弹出的窗口中，勾选“虚拟机平台”和“适用于Linux的windows子系统”，点击“确定”并重启电脑。
2. 下载docker desktop安装包
   * 访问docker官网,windows-11版本下载: https://docs.docker.com/desktop/install/windows-install/
   * 下载好后别安装
3. 安装wsl
   * 执行命令:
        >wsl --install
    * 检查wsl版本
        >wsl --status
    * 需要升级wsl执行以下命令:
        >wsl --updated
    * 更新失败需手动下载Linux内核更新包：
        >https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-3---enable-virtual-machine-feature
    * 卸载安装好的ubuntu，重新执行:
        >wsl --install
    * 设置默认wsl版本
        >wsl --set-default-version 2 
    * 完成后输入用户名，密码能够显示正常Linux界面就是安装成功
    * 最后运行以下命令代表安装成功:
        >docker --verision 
## docker的image与container的关系
   * 镜像：包含了运行某个应用所需的一切内容，比如操作系统层、应用代码、库和依赖等。它是静态的，只读的。

   * 容器：是从镜像启动出来的运行实例，才是真正的运行环境。每个容器都有自己的进程、文件系统和网络接口，可以在其中执行代码。
## docker 拉取和运行容器
* 查看docker所有的镜像:
    >docker images
* 拉取镜像:
    >docker pull (images_name)

    > docker pull (images_name):(tag_name) 下载特定版本的镜像
*  运行容器:
    >docker run (images_name):(tag_name) 镜像可以存在也可以不存在，不存在直接拉取并运行容器

    >docker run -d (images_name):(tag_name) 在后台运行程序不显示运行信息，只显示运行ID

    >docker logs ID 显示容器的运行日志
* 查看正在运行的容器:
    >docker ps

    >docker ps -a  查看所有的容器包括不运行的