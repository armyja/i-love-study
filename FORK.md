# Fork 说明

> 本文内容包含 [README](./README.md) 的补充说明及踩坑记录。

1. 获取已订阅的专栏 pid 数组：
    - 登录 Web 版极客时间。
    - 打开 Chrome Debugger，跳转到 [极客时间的所有课程列表](https://time.geekbang.org/resource)。
    - 在 Debugger 按 `serv/v3/lecture/list` 过滤请求。选中它，并在 **Preview** 选项卡右键单击根节点，选择 **将object存储为全局变量**。此时控制台会自动打印 `temp1` 变量。
    - 控制台输入 `temp1.data.list.filter(c=>c.has_sub && c.ptype==="c1").map(c=>c.pid).sort()`，获得已订阅专栏的 pid 数组。

2. 设置环境变量，以 PowerShell 为例：

    ```powershell
    PS D:\i-love-study> $env:GEEKT_GCID="{Cookie 的 GCID}";
    PS D:\i-love-study> $env:GEEKT_TOKEN="{Cookie 的 GCESS}";
    ```

3. 运行提示找不到 Pandoc，并打印 Path 路径。

    看上去并未使用 Python 环境里的 Lib，于是使用官网下载的 Pandoc，并配置 Path 环境变量。

4. 拉取极客时间课程时，文件名或者文件夹名不符合 Windows 规范。

    解决方案为正则表达式替换：

    ```python
    def fix_filename(title):
        return title.replace("/", "").replace("|", "-").replace("<", "‹").replace(">", "›").replace("?", "？").replace("\"", "'").replace("\x08", "").replace("*", "✳").replace(":", "：")
    ```

5. 提高 sleep 秒数为 5 ~ 10 秒，笔者测试，没有出现返回状态 451 的情况：

    ```diff
    - sleep(randrange(1, 5))
    + sleep(randrange(5, 10))
    ```

