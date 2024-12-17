# appium笔记
## appium的安装
1. 检查nodejs是否安装,以及npm(JavaScript包管理)是否安装
```shell
    node -v
    npm -v
```
2. 没有安装需要安装nodejs
    >https://nodejs.org/en/download/prebuilt-installer
3. 安装appium
```shell
    npm install -g appium
```
4. 检查是否成功安装appium
```shell
   appium --version
   which appium(查看appium位置)
```
5. 运行appium服务器(ctrl+c停止)
```shell
    appium 
```
6. 安装appium-doctor,检查依赖是否安装完全
```shell
npm install -g appium-doctor
```
7. 检查是否安装成功
```shell
appium-doctor --version
```
8. 运行appium-doctor
```shell
#查看运行帮助
appium doctor -h
#查看Android运行环境
appium doctor --android
# 查看iOS运行环境
appium doctor --ios 
```
9. 检查驱动是否安装
```shell
#查看安装的驱动
appium driver list
#安装Android驱动
appium driver install uiautomator2
#安装iOS驱动
appium driver install xcuitest
#查看可更新的驱动
appium driver list --updates
```
10. 运行appium server
```shell
appium
#需要跨域时
appium --allow-cors
```