# 问答&bug
### 错误一、运行1.1的测试命令qemu还是这样然后就直接退出了，该怎么解决呢
```
3.Arceos 已经实现的版本参考代码已提交在
https://github.com/wfly1998/arceos/tree/feature/vga，测试用的命令为
make A=apps/helloworld ARCH=x86_64 LOG=trace GRAPHIC=on run
```
运行时直接闪退了。

【答】: 可能是没有切换到 feature/vga 分支


### 错误二、虚拟机下运行1.1的测试命令 make A=apps/fs/shell ARCH=x86_64 GRAPHIC=on BLK=y run 显示找不到disk.img

> **qemu-system-x86 64: -drive id-disko,if=none,format=raw,file=disk.img: Could not open 'disk.img': No such file or directory**

【答】: fs依赖块设备文件，执行 make disk_img 命令生产一个disk.img即可。

### 错误三、提示 no global memory allocator found but one is required; link to std or add #[global_allocator] to a static item that implements the GlobalAlloc trait

【答】: 删掉 modules/axhal/src/lib.rs 中 extren crate alloc 这行即可
