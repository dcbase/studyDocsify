
学习资料仅供参考，如有错误之处欢迎指出

本项目使用react-native版本为 0.59.0，目前react-native最新版本为 0.6x.x，使用 <0.60.0版本因为 0.60.0以上本版本去除webView及Geolocation（地理定位）功能，需另外引入


##### 前期准备环境

可参考[react-native官网](https://reactnative.cn/)




##### 基本环境

* node
      
    
    brew install node

* watchman
      
    
    //Watchman则是由 Facebook 提供的监视文件系统变更的工具。安装此工具可以提高开发时的性能
    （packager 可以快速捕捉文件的变化从而实现实时刷新）。
    
    brew install watchman
    
    
* 切换淘宝源


    # 使用nrm工具切换淘宝源
    npx nrm use taobao
    
    # 如果之后需要切换回官方源可使用 
    npx nrm use npm
    
* Yarn、React Native 的命令行工具（react-native-cli）


    //Yarn是 Facebook 提供的替代 npm 的工具，可以加速 node 模块的下载。React Native 的命令行工具
    用于执行创建、初始化、更新项目、运行打包服务（packager）等任务
    
    npm install -g yarn react-native-cli
    


#####  Mac/Windows 


Mac工具： xcode 


Windows工具：Android Studio / Android SDK 




##### 创建项目

1. 初始化项目


    react-native init baseApp    //初始化最新版本react-native项目 
    
    or
    
    react-native init baseApp --version 0.59.0   //初始化指定版本号react-native项目


2. 进入项目目录，安装依赖包，运行项目

   
    cd baseApp
    
    
    npm install
    
    
    react-native run-ios   or  react-native run-android
    
    
    /*
    * 注意:
    * 
    * 可能运行完成后会出现服务未启动提示，可至文档最后一章问题内查找，这里简略说下
    *
    * 终止服务，重新启动运行  npm start
    *
    *
    */






