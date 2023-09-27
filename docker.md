### 使用docker commit命令创建新镜像
① 停止容器服务 `docker stop tomcat8(容器名)`
② 构建新镜像  `docker commit tomcat8 tomcat8_new(镜像名)`
③ 使用新镜像重新创建容器  `docker run -d -p 8888:8080 -i --name tomcat88 tomcat8_new(:tag)`
④ 删除原有容器 `docker rm tomcat8`
⑤ 修改容器名称 `docker rename tomcat88 tomcat8`

### 生成镜像
`docker build -t paddleocr:cpu .`

###### 挂载目录+时区
`docker run -dp 8868:8866 -v /root/data/:/PaddleOCR/share/ -e TZ="Asia/Shanghai" --name ppocr paddleocr:2.0 `

###### dockerfile中添加cmd命令
`/bin/bash -c "hub install deploy/hubserving/ocr_system/ && hub install deploy/hubserving/ocr_rec/ && hub serving start -c deploy/hubserving/ocr_system/config.json > share/log/`date +'%Y-%m-%d'`.log"`


### 镜像导入导出
###### 导出
`docker save id > /opt/xxx.tar`

###### 导入
`docker load < xxx.tar`

###### 重新打 tag
`docker tag id xxx:tag`
