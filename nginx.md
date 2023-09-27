### 启动
服务器的操作系统是CentOS7.4及以上，直接输入：`nginx`

直接启动，这时候可能出现两种情况：
* 第一种，就是Nginx已经启动过了，会提示端口被占用，启动失败。

我们尝试杀掉占用端口的进程，然后重启
`systemctl start nginx.service`

* 第二种就是无任何提示。
无任何提示的情况下，我们需要查看一下Nginx的运行状态

`ps aux | grep nginx`



### 停止

- 立即停止服务
`nginx  -s stop`
这种方法比较强硬，无论进程是否在工作，都直接停止进程。

- 从容停止服务
`nginx -s quit`
这种方法较stop相比就比较温和一些了，需要进程完成当前工作后再停止。

- killall 方法杀死进程
`killall nginx`
