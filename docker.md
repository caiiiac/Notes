### 使用docker commit命令创建新镜像
① 停止容器服务 `docker stop tomcat8(容器名)`
② 构建新镜像  `docker commit 容器ID tomcat8_new:tag(镜像名:tag)`
③ 使用新镜像重新创建容器  `docker run -d -p 8888:8080 -i --name tomcat88 tomcat8_new(:tag)`
④ 删除原有容器 `docker rm tomcat8`
⑤ 修改容器名称 `docker rename tomcat88 tomcat8`

### 生成镜像
`docker build -t paddleocr:cpu .`

### 启动容器参数
* -v: 挂载服务器目录至 docker 容器
* -e: 设置容器的时区
* /bin/bash -c: 可以替换 cmd 的启动命令
* --restart=always: 保证每次docker服务重启后容器也自动重启
* 
###### 挂载目录+时区
`docker run -dp 8868:8866 -v /web/webfile/UploadFile/:/UploadFile/ -e TZ="Asia/Shanghai" --name ppocr paddleocr:v2.3`

###### dockerfile中添加cmd命令
`/bin/bash -c "hub install deploy/hubserving/ocr_system/ && hub install deploy/hubserving/ocr_rec/ && hub serving start -c deploy/hubserving/ocr_system/config.json"`


### 镜像导入导出
###### 导出
`docker save 镜像id > /opt/xxx.tar`
`docker export 容器id > /opt/xxx.tar`

###### 导入
`docker load < xxx.tar`

###### 重新打 tag
`docker tag id xxx:tag`


### 其它命令
##### 重启docker和容器
* 重启docker服务：`systemctl restart docker`
* 重启容器： `docker restart containers_id`

##### 日志
`docker logs -f 容器id`
> 执行此命令，会进入控制台等待日志输出，如果日志很长会刷屏很久。

`docker logs --tail 0 -f 容器id`
> 执行此命令，会进入控制台等待日志输出，不会加载之前的日志。

### 修改已停止容器内的文件
1. 将容器中的文件拷贝到宿主机
```
docker cp 容器id:容器内文件路径 宿主机路径
```

2. 修改拷贝出来的文件，再将文件拷贝回容器
```
docker cp 宿主机路径 容器id:容器内文件路径 
```

3. 重新启动容器即可