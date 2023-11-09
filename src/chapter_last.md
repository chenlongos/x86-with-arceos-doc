# 问答&bug
### 错误一、运行1.1的测试命令qemu还是这样然后就直接退出了，该怎么解决呢
```
3.Arceos 已经实现的版本参考代码已提交在
https://github.com/wfly1998/arceos/tree/feature/vga，测试用的命令为
make A=apps/helloworld ARCH=x86_64 LOG=trace GRAPHIC=on run
```
运行时直接闪退了。

【答】: 可能是没有切换到 feature/vga 分支


