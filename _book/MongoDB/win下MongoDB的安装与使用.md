# 下载与安装

这很简单，就不用多说了，在这里我们以把 MongoDB 安装在 `D:\MongoDB` 下面为例。

# 设置为 windows服务

1. 在 `D:\MongoDB` 文件夹下新建 `data` 文件夹，`data` 文件夹下新建 `log` 和 `db` 文件夹;
2. 右击开始菜单，选择`命令提示符(管理员)`;
3. cmd 下进入`D:\MongoDB\bin`文件夹;
4. cmd 输入以下内容：
`mongod --dbpath "D:\MongoDB\data\db" --logpath 
"D:\MongoDB\data\log\MongoDB.log" --install --serviceName "MongoDB"`
5. 右击开始菜单->计算机管理->服务于应用程序->服务，找到 `MongoDB` 设置为自动并启动;