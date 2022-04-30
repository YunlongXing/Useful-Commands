# Linux Kernel调试 (qemu + gdb)

## 环境搭建
1. 下载kernel源码[https://cdn.kernel.org/pub/linux/kernel/]编译需要进行调试的Linux Kernel代码: 进入kernel源码目录，执行```make defconfig```，生成默认```.config```文件，然后执行```make menuconfig```选择需要的编译选项。

2. 

```sh
sudo qemu-system-x86_64 -kernel ./kernel_debugging/linux-5.16.10/arch/x86_64/boot/bzImage -hda qemu_rootfs.img -append "root=/dev/sda rootfstype=ext4 rw nokaslr" -s -S
```
