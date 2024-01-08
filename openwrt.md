## 参考文档
1. https://hub.docker.com/r/sulinggg/openwrt
2. https://mlapp.cn/376.html

## 安装步骤

### 1. 网卡（LAN口）开启混杂模式
ip link set enp1s0 promisc on 

### 2. 创建虚拟网卡，设置为宿主机网段和网关
docker network create -d macvlan --subnet=192.168.31.0/24 --gateway=192.168.31.1 -o parent=enp1s0 macnet

查看创建的网络
docker network ls

### 3. 创建容器（可以在CASAOS操作）
docker run --restart always --name openwrt -d --network macnet --privileged sulinggg/openwrt:x86_64	/sbin/init

### 4. 修改IP
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
### 5. 设置Openwrt（TBC）
        
