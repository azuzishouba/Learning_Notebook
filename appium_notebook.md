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
## 安装安卓测试的依赖(使用androidstudio GUI)
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
### 安装安卓虚拟设备(使用androidstudio GUI)
1. 打开安卓studio

2. 设置 -> AVD Manager (or click the AVD Manager icon in the toolbar)

3. 点击Create Virtual Device 选择设备 (phone or tablet) 和Android版本

4. 点击下一步并分配内存 (name, RAM, storage etc.)

5. 点击完成创建虚拟设备

6. 启动虚拟设备

7. 检查是否可以运行
### 安装物理安卓设备
1. 关于本机->版本信息->点击版本号三次
2. 系统更新->开发者选项->打开usb设备调试
3. 用数据线连接设备
4. 检查设备是否连接
```shell
    adb devices
```
### adb常用命令
1. 查看设备列表
```shell
adb devices
```
2. 重启设备
```shell
adb reboot
```
3. 推送文件到设备
```shell
adb push (local_file) (remote_location)
```
4. 设备拉取文件
```shell
adb pull (remote_file) (local_location)
```
5. 安装apk
```shell
adb install <apk_file_path>
```
6. 卸载apk
```shell
adb uninstall <package_name>
```
7. 查看已经安装的包
```shell
adb shell pm list packages
```
8. 查看设备日志
```shell
adb logcat
```
## 安装appium inspector(物理安卓设备)
1. 官网下载appium inspector
    > https://github.com/appium/appium-inspector
2. 往下划点击release,下载对应的Windows版本
3. 安装完成后打开,点击start session(在启动前确保启动appium服务器,网页端需要使用跨域启动appium)
4. 此时应该会看到" the error message for desired capabilities and not for appium server"
5. 添加设备相关信息
![capability_builder_interface](/screen_shot/capability_builder_interface.png)
* automationname:通常为自动化驱动,可以通过appium driver list查看,安卓通常为uiautomator2,苹果统称为xcuitest
* platformname:安卓是Android,苹果是iOS
* platformversion:系统版本,通过adb shell getprop ro.build.version.release查看
* devicename:设备名称,通过adb devices查看
* app:测试的app的位置
6. 也可用json文件
eg:
{
  "appium:automationName": "UiAutomator2",
  "appium:platformName": "Android",
  "appium:platformVersion": "11",
  "appium:deviceName": "4b316ae9",
  "appium:app": "/Users/raghavpal/Katalon Studio/Android Testing Project/androidapp/APIDemos.apk"
}
## ***安装appium inspector(虚拟安卓机)***
1. 启动appium服务器 appium --allow-cors 
2. 启动Emulator 或连接物理安卓设备
```shell
#所有虚拟机
emulator -list-avds
#启动特定虚拟机
emulator -avd AvdName
#保存应用和数据状态,但从头开始启动系统
emulator -avd avdname -no-snapshot-load
#恢复出厂设置
emulator -avd avdname -wipe-data
```
3. 设备相关信息同上
* automationname:通常为自动化驱动,可以通过appium driver list查看,安卓通常为uiautomator2,苹果统称为xcuitest
* platformname:安卓是Android,苹果是iOS
* platformversion:系统版本,通过adb shell getprop ro.build.version.release查看
* devicename:设备名称,通过adb devices查看
* app:测试的app的位置
4. 启动session
## appium inspector界面
![appium_inspector_interface](/screen_shot/appium_inspector_interface.png)
1. source(源):可以查看元素信息,可与元素互动,可以点击或者sendkeys
2. 命令(command):可以执行一些简单的命令和判断
3. 手势(gesture):执行一些触屏操作
4. 录制(record):进行手势操作时可以录制,录制后自动生成语言代码
5. 会话信息(session):当前会话的信息
### 手势(gesture)
1. 点击操作
实现逻辑:移动到特定点位->手指按下去->手指抬起来
   1. move,虚拟机上选取一个点,设定操作时间
   2. pointer down(左点击,触屏一般没右击)
   3. pointer up(左点击,触屏一般没右击)
2. 滑动操作
实现逻辑:移动到特定点位->手指按下去->移动到特定点位->手指抬起来
   1. move,虚拟机上选取一个点,设定操作时间 
   2. pointer down(左点击,触屏一般没右击)
   3. move,虚拟机上选取一个点,设定操作时间
   4. pointer up(左点击,触屏一般没右击)
3. zoom in和zoom out操作
实现逻辑:因为前面操作一只手指就可以操作,放缩操作需要两个手指,所以需要创建新的手指。左手指移动到特定点位->左手执按下去->移动到特定点位->左手指松开。右手指同样操作
![zoom_gesture_interface](/screen_shot/zoom_gesture_interface.png)
   1. move,虚拟机上选取一个点,设定操作时间 
   2. pointer down(左点击,触屏一般没右击)
   3. move,虚拟机上选取一个点,设定操作时间
   4. pointer up(左点击,触屏一般没右击)
   5. 添加右手指
   6. move,虚拟机上选取一个点,设定操作时间 
   7. pointer down(左点击,触屏一般没右击)
   8. move,虚拟机上选取一个点,设定操作时间
   9. pointer up(左点击,触屏一般没右击)