#  ArceOS X86 输入输出设备串口代码分析
 
键盘驱动和串口驱动都有共同点，可以作为输入设备。 参考串口的输入设备编写键盘的输入接口。

1. 代码地址
https://github.com/rcore-os/arceos/blob/main/modules/axhal/src/platform/x86_pc/uart16550.rs

2. 串口的类似原理

https://wenku.baidu.com/view/ea660c60862458fb770bf78a6529647d272834b0.html?_wkts_=1697784322531&needWelcomeRecommand=1

https://max.book118.com/html/2017/0729/124989181.shtm

根据以上资料 了解串口的初始化，波特率设置，读写

3. 目标任务
* 根据以上资料和代码 了解 端口的操作函数
* 了解 串口的硬件知识
* 分析 代码 如何实现 串口的 操作
* 串口 如何作为ArceOS的 输入输出 设备