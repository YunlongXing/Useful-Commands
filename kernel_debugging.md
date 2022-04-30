# Linux Kernel调试 (qemu + gdb)

## 环境搭建
1. 编译需要进行调试的Linux Kernel代码: 进入kernel源码目录，执行```make defconfig```，生成默认```.config```文件，然后执行```make menuconfig```选择需要的编译选项。

2. 
