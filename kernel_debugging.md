# Linux Kernel调试 (qemu + gdb)

## 环境搭建
1. 编译需要进行调试的Linux Kernel代码: 下载kernel[源码](https://cdn.kernel.org/pub/linux/kernel/)，进入kernel源码目录，执行```make defconfig```，生成默认```.config```文件，然后执行```make menuconfig```选择需要的编译选项 (勾选Kernel hacking => Compiler-time checks and compiler options => Compile the Kernel with debug info), 最后```make && make install```.

2. 安装qemu: ```sudo apt install qemu```.

3. 编译busybox: 下载busybox[源码](https://busybox.net/downloads/), 进入目录，执行```make menuconfig```选择需要的编译选项 (勾选Settings => Build Options => Build static binary), 最后```make && make install```.

## 制作rootfs磁盘镜像文件
1. 创建目录qemu_rootfs: ```mkdir qemu_rootfs```.

2. 切换到目录qemu_rootfs，并使用qemu-img命令生成磁盘镜像文件：```qemu-img create qemu_rootfs.img  50g```，其中qemu_rootfs.img是文件名，50g是磁盘大小.

3. 创建ext4文件系统: ```mkfs.ext4 qemu_rootfs.img```.

4. 挂载img文件到宿主系统: ```sudo mount -o loop qemu_rootfs.img .```, 这里-o loop的意思是将qemu_rootfs.img作为硬盘文件，挂载在qemu_rootfs目录下.


```sh
sudo qemu-system-x86_64 -kernel ./kernel_debugging/linux-5.16.10/arch/x86_64/boot/bzImage -hda qemu_rootfs.img -append "root=/dev/sda rootfstype=ext4 rw nokaslr" -s -S
```
