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

