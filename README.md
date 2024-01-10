## 记录X86小主机的设置过程。
1. 操作系统设置参见: [debian.md](debian.md)
2. 小雅安装设置参加：xiaoya.md
3. 软路由OpenWrt参见：openwrt.md
4. KVM虚拟机参见：kvm.md

## X86/64小主机的优点
- 可扩展性好：可以扩容内存硬盘
- 兼容性好：X86/64作为服务器系统软件生态更丰富
- 支持KVM：可以安装Windows，实现需要Windows的任务比如Quant
- 省电：比笔记本更省电(C92待机5W)
- 网速：一般都支持千兆网卡
- 便宜：老旧的二手mini电脑性能就足够了

## 其他选项
- 玩客云：买刷好Armbian的成品，价格50+，有千兆网卡，HDMI，内存1G+8G，主要做软路由和XiaoYa的话性能应该足够
- 魔百盒：价格50+，不建议做软路由因为网卡是百兆

## 操作系统
- Debian/Armbian：纯服务器，更稳定，能耗更低
- FydeOS: 轻娱乐，基于ChromeOS支持安卓和Linux程序
- Windows：轻办公+虚拟机安装OpenWrt
