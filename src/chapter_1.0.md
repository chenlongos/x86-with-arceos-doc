## 了解x86系统启动原理
1、 地址空间分配

https://blog.csdn.net/pwl999/article/details/78212508

http://117.50.182.35/Linux%E5%86%85%E6%A0%B8/x86CPU%E5%9C%B0%E5%9D%80%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D/

2、引导扇区
https://zhuanlan.zhihu.com/p/38562168

https://www.cnblogs.com/CasonChan/p/4546658.html


3、引导过程 
https://zhuanlan.zhihu.com/p/358796403

## 使用 grub启动ArceOS
按下面的流程完成实验，
要求 U盘能启动显示 ArceOS 启动Logo（文字版本）

https://gitee.com/chenlongos/os-x86-iso

## 如何制作u盘启动OS的iso文件

Thanks to <https://os.phil-opp.com/multiboot-kernel/>

### 下载项目
```
$ git clone https://gitee.com/chenlongos/os-x86-iso.git
Cloning into 'os-x86-iso'...
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (14/14), done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 14 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (14/14), done.

$ cd os-x86-iso/
$ tree
.
├── Makefile
├── README.md
└── src
    └── arch
        └── x86_64
            ├── boot.asm
            ├── grub.cfg
            ├── linker.ld
            └── multiboot_header.asm

```

### Ubuntu 安装依赖
```
sudo aptitude  install nasm mtools xorriso
```

## 无需编译，直接验证

### 快速烧写验证
最终iso文件 ./build/os-x86_64.iso 已经推入仓库，可以直接用 make dd 进行烧写验证

```
$ make dd

diskutil unmountDisk /dev/disk3
Unmount of all volumes on disk3 was successful

sudo dd if=./build/os-x86_64.iso of=/dev/disk3
Password:
22580+0 records in
22580+0 records out
11560960 bytes transferred in 22.977369 secs (503146 bytes/sec)

diskutil eject /dev/disk3
Disk /dev/disk3 ejected

```

## 编译源码，了解细节

### 编译生成 iso
```
$ make
mkdir -p build/arch/x86_64
nasm -felf64 src/arch/x86_64/boot.asm -o build/arch/x86_64/boot.o
mkdir -p build/arch/x86_64
nasm -felf64 src/arch/x86_64/multiboot_header.asm -o build/arch/x86_64/multiboot_header.o
ld -n -T src/arch/x86_64/linker.ld -o build/kernel-x86_64.bin  build/arch/x86_64/boot.o  build/arch/x86_64/multiboot_header.o

$ make iso
mkdir -p build/isofiles/boot/grub
cp build/kernel-x86_64.bin build/isofiles/boot/kernel.bin
cp src/arch/x86_64/grub.cfg build/isofiles/boot/grub
grub-mkrescue -o build/os-x86_64.iso build/isofiles 2> /dev/null
rm -r build/isofiles

$ ls -l build/os-x86_64.iso
-rw-r--r-- 1 root root 9097216 Oct  5 22:56 build/os-x86_64.iso
```

### 烧写iso文件到u盘
```
$ sudo dd if=./build/os-x86_64.iso of=/dev/disk3
Password:
17768+0 records in
17768+0 records out
9097216 bytes transferred in 17.312507 secs (525471 bytes/sec)
```
