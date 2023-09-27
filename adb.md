### ADB命令
```
adb devices  - - 查看连接设备

adb connect <ip> - - 通过IP地址连接设备

adb install <apk地址> - - 安装apk

adb tcpip 5555 - - 解决无法连接设备问题(需要通过USB连接)
```

拉文件
```adb pull /mnt/internal_sd/logger /Users/*/Desktop```

启动app
`
adb shell am start -n com.***.ad_android/com.***.ad_android.Classes.Main.Activity.ConfigActivity
`

查看app版本号
`adb shell dumpsys package com.***.ad_android | grep "versionName"`
