### 安装Flutter

* 下载与系统匹配的SDK：[下载链接](https://flutter.cn/docs/release/archive)
* 将文件解压到目标目录：`~/`或者`/usr/local`
* 配置环境变量：`export PATH=“$PATH:'pwd'/flutter/bin”`
* 运行 flutter doctor 命令,查看当前环境是否需要安装其他的依赖（-v 可查看更详细的输出）

### 常用命令
```
flutter doctor 查看flutter的状态，查看环境配置是否有问题
flutter doctor -v 查看flutter 状态的详细信息
flutter build apk 打包安卓包
flutter build ios 打包苹果ipa
flutter run 运行项目 默认--debug
flutter run --profile 运行线上测试包
flutter run --release 运行线上包
flutter channel 查看flutter 的所有分支
flutter channel stable 切换到具体的分支
flutter upgrade 升级flutter
flutter upgrade --force 如果升级flutter出现问题可以尝试 强制更新
flutter logs 当链接到某一个设备的时候，通过此命令可以查看到当前设备的log
flutter screenshot 可以截取项目当前屏幕展示的图到项目里
futter clean 清除缓存
flutter create 创建一个flutter 新项目
```

### 打包deb
* 编译，生成的目录在 build/linux/x86/release/bundle
`flutter build linux --release`
* 新建以下目录结构，将编译生成的 bundle 文件复制到`usr/local`下，并重命名为 demo
```
package/
└── flutter_build_demo
    ├── DEBIAN
    │   ├── control
    │   ├── postinst
    │   └── postrm
    └── usr
    │   ├── local
    │       └── demo
    │           ├── data
    │           ├── demo
    │           └── lib
        └── share
            ├── applications
            │   └── demo.desktop
            └── icons
                └── demo.png
```
* control
描述软件包的名称（Package），版本（Version），描述（Description）等，是 deb 包必须具备的描述性文件，以便于软件的安装管理和索引
```
Package: demo
Version: 1.0.0
Section: free
Priority: optional
Essential: no
Architecture: all
Maintainer: caiiiac <caiiiac@163.com>
Provides: demo
Description: flutter build demo
```

* demo.desktop
Name可设置中文名称
```
[Desktop Entry]
Name=Flutter Build Demo
Name[zh_CN]=打包示例
Comment=Flutter Build Demo application
Exec=/usr/local/demo/demo
Icon=/usr/share/icons/demo.png
Terminal=false
Type=Application
Categories=Network;WebBrowser;
MimeType=text/html;text/xml;application/xhtml+xml;application/xml;application/rss+xml;application/rdf+xml;image/gif;image/jpeg;image/png;x-scheme-handler/http;
StartupNotify=true
```

* 打包
执行命令`sudo dpkg-deb -b demo demo_1.0.0.deb`，完成后就会在当前目录生成 demo_1.0.0.deb 的文件，后面就可以使用 `dpkg -i` 命令对这个 deb 包进行安装。

* 安装
`sudo dpkg -i demo_1.0.0.deb`

* 后续更新打包，可使用脚本 packge.sh 完成。
```
#!/bin/bash

# flutter 编译
flutter build linux --release
# 拷贝编译后的文件到打包目录
cp -r /build/linux/x64/release/bundle/* pacakge/demo/usr/local/demo/
# 打包
sudo dpkg-deb -b pacakge/demo pacakge/demo_1.0.0.deb
```
