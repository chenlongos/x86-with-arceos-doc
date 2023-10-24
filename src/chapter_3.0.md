# 第三阶段：文件系统分析
1. 阅读 ArceOS 文件系统实现源代码， 简单阅读即可

https://github.com/rcore-os/arceos/tree/main/modules/axfs/src/fs

2. 阅读 文件使用使用源代码 
do_cat 函数
https://github.com/rcore-os/arceos/blob/main/apps/fs/shell/src/cmd.rs#L124

```
fn do_cat(args: &str) {
    if args.is_empty() {
        print_err!("cat", "no file specified");
        return;
    }

    fn cat_one(fname: &str) -> io::Result<()> {
        let mut buf = [0; 1024];
        let mut file = File::open(fname)?;
        loop {
            let n = file.read(&mut buf)?;
            if n > 0 {
                io::stdout().write_all(&buf[..n])?;
            } else {
                return Ok(());
            }
        }
    }

    for fname in args.split_whitespace() {
        if let Err(e) = cat_one(fname) {
            print_err!("cat", fname, e);
        }
    }
}

```

