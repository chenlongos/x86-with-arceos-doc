# 第二阶段：键盘驱动
1. rust ps2鼠标驱动例子 

https://github.com/rust-osdev/ps2-mouse 鼠标驱动

2. rust ps2 键盘驱动例子

https://gitlab.redox-os.org/redox-os/drivers/-/blob/master/ps2d/src/controller.rs ps2键盘驱动的例子

3. 键盘码和扫描码的对应
http://osdev.foofun.cn/index.php?title=PS/2_Keyboard

4. X86 读取键盘片段参考
```
; read_key函数，从键盘控制器的数据端口读取扫描码，并保存在al寄存器中
read_key:
    in al, 0x60 ; 从端口0x60读取扫描码
    ret ; 返回

; print_key函数，将al寄存器中的扫描码转换为ASCII码，并打印在屏幕上
print_key:
    cmp al, 0x01 ; 比较扫描码是否为Esc键（0x01）
    je exit ; 如果是，跳转到exit标签，结束程序
    cmp al, 0x02 ; 比较扫描码是否为1键（0x02）
    je print_1 ; 如果是，跳转到print_1标签，打印1
    cmp al, 0x03 ; 比较扫描码是否为2键（0x03）
    je print_2 ; 如果是，跳转到print_2标签，打印2
    cmp al, 0x04 ; 比较扫描码是否为3键（0x04）
    je print_3 ; 如果是，跳转到print_3标签，打印3
    cmp al, 0x05 ; 比较扫描码是否为4键（0x05）
    je print_4 ; 如果是，跳转到print_4标签，打印4
    cmp al, 0x06 ; 比较扫描码是否为5键（0x06）
    je print_5 ; 如果是，跳转到print_5标签，打印5
    cmp al, 0x07 ; 比较扫描码是否为6键（0x07）
    je print_6 ; 如果是，跳转到print_6标签，打印6
    cmp al, 0x08 ; 比较扫描码是否为7键（0x08）
    je print_7 ; 如果是，跳转到print_7标签，打印7
    cmp al, 0x09 ; 比较扫描码是否为8键（0x09）
    je print_8 ; 如果是，跳转到print_8标签，打印8
    cmp al, 0x0a ; 比较扫描码是否为9键（0x0a）
    je print_9 ; 如果是，跳转到print_9标签，打印9
    cmp al, 0x0b ; 比较扫描码是否为0键（0x0b）
    je print_0 ; 如果是，跳转到print_0标签，打印0
```