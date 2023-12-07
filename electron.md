### 安装Node

* 前往官网下载Node离线包：[下载链接](https://nodejs.cn/download/)
* 将文件解压到目标目录：`~/`或者`/usr/local`
* 配置环境变量：`export PATH=$PATH:~/node/bin`
* 重新启动命令终端，使用`node -v`查看是否成功。

### 安装electron-forge

* 更改npm国内镜像
`npm config set registry https://registry.npmmirror.com`
* 安装cli
`npm install -g @electron-forge/cli`
* 配置环境变量，更改electron源
```
ELECTRON_MIRROR="https://npmmirror.com/mirrors/electron/"
ELECTRON_CUSTOM_DIR="{{ version }}"
```

### 初始化项目
```
electron-forge init demo  // 初始化
cd demo  // 进入目录
npm start  // 启动项目
npm run make // 打包
```

### 修改配置
在`forge.config.js`中可修改打包后的应用名称，如打包deb时如下所示：
```
makers: [
    {
        name:'@electron-forge/maker-deb'，
        config:{
            name:"demo",
            productName:"中文名称"，
            icon:"/src/*.png"
        }
    }
]
```
