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