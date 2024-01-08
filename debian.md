## 测试硬盘性能
```shell
# dd if=/dev/zero of=/tmp/test bs=1G count=1 oflag=dsync
输入了 1+0 块记录
输出了 1+0 块记录
1073741824 字节 (1.1 GB, 1.0 GiB) 已复制，5.39567 s，199 MB/s

rm /tmp/test
```

## 硬盘寿命
```shell
sudo smartctl -t short /dev/sda1
# 几分钟后查看，如下输出则为全新
sudo smartctl -l selftest /dev/sda1

smartctl 7.3 2022-02-28 r5338 [x86_64-linux-6.1.0-15-amd64] (local build)
Copyright (C) 2002-22, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF READ SMART DATA SECTION ===
SMART Self-test log structure revision number 1
Num  Test_Description    Status                  Remaining  LifeTime(hours)  LBA_of_first_error
# 1  Extended offline    Completed without error       00%         0         -

```

## 设置按电源键不关机（避免误碰）
由于服务器是24*7运行的，避免误碰导致关机，需要进行如下设置：

具体步骤可能因发行版而异，以下是一些通用的指导：

1. 打开电源管理配置文件，通常是`/etc/systemd/logind.conf`。

```bash
sudo nano /etc/systemd/logind.conf
```

2. 找到并编辑以下行：

```plaintext
#HandlePowerKey=poweroff
```

将其修改为：

```plaintext
HandlePowerKey=ignore
```

3. 保存并关闭编辑器。

4. 重新加载systemd配置：

```bash
sudo systemctl daemon-reload
```

5. 重新启动systemd-logind服务：

```bash
sudo systemctl restart systemd-logind
```

这样配置后，按下电源按钮将不再触发关机操作。

请注意，这些方法可能在不同的Linux发行版上有所不同。建议查阅你所使用发行版的文档或社区支持以获取更具体的信息。
