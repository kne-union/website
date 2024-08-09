# 解决国内docker镜像拉取不到的问题

1. 创建文件
```shell
/etc/docker/daemon.json 
```
2. 写入配置
```shell
{
   "registry-mirrors": [
   "https://dockerpull.com"
  ]
}
```
3. 重启docker
```shell
sudo systemctl daemon-reload
sudo systemctl restart docker
```

# 将docker镜像打包上传

```shell
# Save 镜像
docker save my-image > my-image.tar

# 在目标机器上 Load 镜像
docker load < my-image.tar
```
