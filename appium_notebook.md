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
## 安装安卓测试的依赖(使用androidstudio)
1. 安装Androidstudio
    >https://developer.android.com/studio?hl=zh-cn
2. 解压并安装,安装时最好在D盘设置sdktools给sdk
3. 进入设置->sdk manager,选择sdk platforms和sdk tools
4. sdk platforms中下载Android版本
5. sdk tools下载build-tools,android emulator,platform-tools
6. 在系统设置里配置ANDROID_HOME
![ANDROID_HOME_interface](/screen_shot/ANDROID_HOME_interface.png)
***变量值设置为存放sdk的文件夹位置***
7. 检查安卓测试依赖是否安装完成
![appium-doctor_android_interface](/screen_shot/appium-doctor_android_interface.png)
出现以下图片就代表安装完成
### 安装安卓虚拟设备
1. Open Android Studio

2. Go to "Tools" -> "AVD Manager" (or click the AVD Manager icon in the toolbar)
Or
        Android Studio > Preferences > Appearance & Behavior > System Settings > Android SDK > AVD Manager
        (on macOS)

3. Click "Create Virtual Device" and choose a desired device configuration (phone or tablet) with the required Android API level

4. Click "Next" and follow the steps to define the AVD configuration (name, RAM, storage etc.)

5. Click "Finish" to create the emulator

6. Launch the emulator from the AVD Manager

7. Check the emulator is available in Device Manager