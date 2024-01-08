在Debian命令行上安装KVM（Kernel-based Virtual Machine）并在虚拟机中安装Windows是可行的。您可以使用一个名为"virt-manager"的工具，它提供了一个基于图形界面的管理界面，但请注意，它是一个GUI工具。如果您的Debian系统没有图形界面，您可以尝试使用一个称为"virt-viewer"的工具，它提供了一个简单的图形界面来查看虚拟机的控制台。

## 以下是在Debian上安装KVM和virt-viewer的基本步骤：

1. **安装KVM：**
   ```bash
   sudo apt update
   sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system
   ```

2. **添加用户到libvirt组（避免使用sudo）：**
   ```bash
   sudo adduser debian libvirt
   sudo adduser debian libvirt-qemu
   ```

   请将 `<your_username>` 替换为您的实际用户名。

3. **重启libvirt服务：**
   ```bash
   sudo systemctl restart libvirtd
   ```

4. **安装virt-viewer：**
   ```bash
   sudo apt install virt-viewer
   ```

5. **创建虚拟机(建议不使用命令行，稍等使用WebUI来创建)：**
   使用`virt-install`命令创建虚拟机，以下是一个简单的示例：
   ```bash
   sudo virt-install --name my-windows-vm --memory 2048 --vcpus 2 --disk size=20 --cdrom /path/to/windows.iso --os-type windows --os-variant win10
   ```

   请替换 `/path/to/windows.iso` 为您实际的Windows安装ISO文件路径。

6. **使用virt-viewer查看虚拟机控制台：**
   ```bash
   virt-viewer my-windows-vm
   ```

   替换 `my-windows-vm` 为您实际创建的虚拟机名称。

请注意，virt-viewer将在您的终端中打开一个简单的图形界面。如果您想在没有图形界面的情况下使用WebUI管理KVM虚拟机，可以考虑使用Web管理工具，例如Cockpit。 Cockpit是一个基于Web的管理界面，可以在没有桌面环境的情况下使用。

1. **安装Cockpit：**
   ```bash
   sudo apt install cockpit
   # 必须安装以下模块，否则看不到虚拟机管理界面
   sudo apt install cockpit-machines
   ```

2. **启动Cockpit服务：**
   ```bash
   sudo systemctl start cockpit
   ```

3. **启用Cockpit服务：**
   ```bash
   sudo systemctl enable cockpit
   ```

4. **访问Cockpit：**
   在浏览器中访问`https://your-server-ip:9090`，用实际的服务器IP地址替换 `your-server-ip`。

   您将能够使用Cockpit的Web界面管理您的KVM虚拟机。

## 安装Windows虚拟机，并允许局域网互通

创建时网络选择"Direct attachment" ，这样安装好以后就可以使用DHCP获取局域网IP（不同于宿主机）。

"Direct attachment" 是一种网络模式，通常用于虚拟机的网络配置。这种模式的特点是直接将虚拟机网络接口（vNIC）与物理网络接口（pNIC）直接连接，而不通过虚拟交换机。这种配置有时也称为"直通"（passthrough）或 "直接连接"。

"Direct attachment" 模式本质上是将虚拟机的网络接口（vNIC）直接连接到宿主机的物理网络接口（pNIC），而不通过虚拟交换机。在这种模式下，虚拟机可以与宿主机共享相同的物理网络接口，但不共享相同的 IP 地址。

在这种模式下，虚拟机将被分配一个独立的 IP 地址，就像它是网络中的一个独立设备一样。该 IP 地址通常由 DHCP 服务器分配，或者你可以手动配置虚拟机的静态 IP 地址。
![image](https://github.com/chenyjc/home-lab/assets/17583587/95d002de-5e63-42f0-a6dd-d4ff29ed4958)

