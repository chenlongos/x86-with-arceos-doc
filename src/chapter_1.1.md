#  ArceOS VGA驱动/彩色显示
1. 参考代码
https://github.com/phil-opp/blog_os/blob/post-12/src/vga_buffer.rs

2. redox 参考代码
跟踪源码，也可以找到和 vga 显示有关的代码在这里：
https://gitlab.redox-os.org/redox-os/bootloader/-/blob/master/src/os/bios/mod.rs

```
const VGA_ADDR: usize = 0xB8000;`

pub(crate) static VGA: Mutex<Vga> = Mutex::new(
    unsafe { Vga::new(VGA_ADDR, 80, 25) }
);
```

这个基地址和下面这个文件代码里的 0xb8000 是一致的

    https://github.com/phil-opp/blog_os/blob/post-12/src/vga_buffer.rs
```
    pub static ref WRITER: Mutex<Writer> = Mutex::new(Writer {
        column_position: 0,
        color_code: ColorCode::new(Color::Yellow, Color::Black),
        buffer: unsafe { &mut *(0xb8000 as *mut Buffer) },
    });
```
vga 这个 mod 的实现是在这个文件
https://gitlab.redox-os.org/redox-os/bootloader/-/blob/master/src/os/bios/vga.rs


3. ArceOS 已经实现的版本参考
代码已提交在 https://github.com/wfly1998/arceos/tree/feature/vga，测试用的命令为

```
make A=apps/helloworld ARCH=x86_64 LOG=trace GRAPHIC=on run
```

4. 显示framebuffer 驱动例子
https://github.com/rust-osdev/vga/blob/master/src/vga.rs 

5. 已经实现的 彩色显示的
![](https://user-images.githubusercontent.com/37299119/275340212-11344a04-033e-47f1-8c64-e2759e79bdce.png)
https://github.com/wfly1998/arceos/tree/feature/vga
```
make A=apps/helloworld ARCH=x86_64 LOG=trace GRAPHIC=on run
make A=apps/fs/shell ARCH=x86_64 GRAPHIC=on BLK=y run
```