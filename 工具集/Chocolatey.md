# Chocolatey

Chocolatey 是 Windows 下的包管理器，功能虽然不及Linux中那些包管理器强大，但是也让Windows下的软件安装方便了不少。

## 安装

1. 以管理员权限打开命令提示符.
2. 运行：
```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

3. 验证：

```
choco
```

会出现版本号证明安装成功。

## 更新

```
choco upgrade chocolatey
```

## 安装软件

```
choco install yarn
```