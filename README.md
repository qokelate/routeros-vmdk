```

# 下载ISO
curl -LORk 'https://github.com/elseif/MikroTikPatch/releases/download/7.16.2/mikrotik-7.16.2.iso'

# 生成vhd
truncate -s 1G ros.img

# 安装ROS
qemu-system-x86_64 \
-enable-kvm \
-cpu host \
-m 512 \
-drive 'file=$PWD/mikrotik-7.16.2.iso,media=cdrom' -boot c \
-drive "if=none,id=disk00,format=raw,file=$PWD/ros.img" \
-device "ide-hd,drive=disk00,bus=ide.0,serial=00000000000000000001,model=VMware Virtual IDE Hard Drive" \
-nographic -vnc :0

# 运行ROS
qemu-system-x86_64 \
-enable-kvm \
-cpu host \
-m 512 \
-drive "if=none,id=disk00,format=raw,file=$PWD/ros.img" \
-device "ide-hd,drive=disk00,bus=ide.0,serial=00000000000000000001,model=VMware Virtual IDE Hard Drive" \
-boot d \
-nographic

```
