## 参考文档
1. https://hub.docker.com/r/sulinggg/openwrt
2. https://mlapp.cn/376.html

## 安装步骤

### 1. 网卡（LAN口）开启混杂模式
```shell
ip link set enp1s0 promisc on 
```

### 2. 创建虚拟网卡，设置为宿主机网段和网关
```shell
docker network create -d macvlan --subnet=192.168.31.0/24 --gateway=192.168.31.1 -o parent=enp1s0 macnet
````

查看创建的网络
```shell
docker network ls
```

### 3. 创建容器（可以在CASAOS操作）
```shell
docker run --restart always --name openwrt -d --network macnet --privileged sulinggg/openwrt:x86_64	/sbin/init
```

### 4. 修改IP
```shell
docker exec -it openwrt bash

nano /etc/config/network

config interface 'lan'
        option type 'bridge'
        option ifname 'eth0'
        option proto 'static'
        option netmask '255.255.255.0'
        option ip6assign '60'
        option ipaddr '192.168.31.101'
        option gateway '192.168.31.1'
        option broadcast '192.168.31.255'
        option dns '192.168.31.1'

/etc/init.d/network restart

```

### 5. 设置Openwrt

登录地址：http://192.168.31.101
用户名：root
密码：password

#### 关闭桥接
![image](https://github.com/chenyjc/home-lab/assets/17583587/8b048f8b-13bd-4958-b923-e6a0dc77603a)

#### DNS缓存
![image](https://github.com/chenyjc/home-lab/assets/17583587/333ec8ad-46b8-47dd-9987-e20ff7ee8e13)

#### Passwall设置
![image](https://github.com/chenyjc/home-lab/assets/17583587/f3a74a76-71b4-4bd9-bf7b-b0f4c8e8127f)

        
