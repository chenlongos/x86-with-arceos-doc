# 第四阶段：httpserver代码分析
1.  阅读ArceOS httpserver源代码
https://github.com/rcore-os/arceos/blob/main/apps/net/httpserver/src/main.rs

2. 修改返回的内容
```
const CONTENT: &str = r#"<html>
<head>
  <title>Hello, ArceOS</title>
</head>
<body>
  <center>
    <h1>Hello, <a href="https://github.com/rcore-os/arceos">ArceOS</a></h1>
  </center>
  <hr>
  <center>
    <i>Powered by <a href="https://github.com/rcore-os/arceos/tree/main/apps/net/httpserver">ArceOS example HTTP server</a> v0.1.0</i>
  </center>
</body>
</html>
"#;
```

3.  仿照参考例子 ，修改成在 x86下可以执行

```
make A=apps/net/httpserver ARCH=aarch64 LOG=info SMP=4 run NET=y
```

寻找文档，并成功执行httpserver例子 