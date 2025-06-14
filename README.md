# redroid-with-libndk
原项目：https://github.com/remote-android/redroid-doc/

因为原项目的**Native Bridge Support**部分说明比较简单，[自动构建脚本](https://gitlab.com/android-generic/android_vendor_google_emu-x86)也有很多坑，故把提取完成的libndk放在这里。

仓库里有已经提取并修改好权限的native-bridge.tar，进入文件夹后可以直接输入以下命令构建：
```bash
docker build . -t redroid-with-libndk:11.0.0-amd64
```

# ubuntu 24.04 
```
## install required kernel modules
sudo apt install linux-modules-extra-`uname -r`
modprobe binder_linux devices="binder,hwbinder,vndbinder"
### optional module (removed since 5.18)
modprobe ashmem_linux
```
## `modprobe: FATAL`
```
modprobe: FATAL: Module ashmem_linux not found in directory /lib/modules/6.8.0-51-generic
```
忽略即可，后续你需要操作的是：
```
sudo apt install linux-modules-extra-`uname -r`
modprobe binder_linux devices="binder,hwbinder,vndbinder"

docker restart <your-redroid-container>
```
