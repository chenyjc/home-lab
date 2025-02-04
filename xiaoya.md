## 参考文档
https://xiaoyaliu.notion.site/xiaoya-docker-69404af849504fa5bcf9f2dd5ecaa75f

## 安装
```shell
bash -c "$(curl http://docker.xiaoya.pro/update_new.sh)" -s host
```
或者下载下来，执行：
```shell
./update_new.sh host
```
## 导入CASAOS
如果使用CASAOS，在界面点击会提醒导入。输入IP和端口（6789）。然后点击三个点里的重建/rebuild。重建完成后可以删除旧容器。

## 索引
重建等待10分钟后再访问。会自动完成索引。

## 每日更新
```
sudo su
crontab -e

# Restart xiaoya everyday at 6
0 6 * * * docker restart xiaoya
```

## 挂载硬盘
```shell
sudo mkdir /mnt/alist
sudo mount -t davfs http://192.168.31.100:6789/dav/ /mnt/alist -o rw,uid=debian,gid=debian
```
输入账号密码：
Please enter the username to authenticate with server
```text
http://192.168.31.100:6789/dav/ or hit enter for none.
  Username: guest
Please enter the password to authenticate user guest with server
guest_Api789
```
随后可以在CASAOS的Files里设置共享，然后在其他电脑或者设备就可以看到共享文件夹。
