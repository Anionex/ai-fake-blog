# python虚拟环境venv使用教程（简洁版）

1. 安装venv

python3.6及以上已经默认安装，python3.5需要通过系统的包管理工具安装，例如在Ubuntu上，可以这么安装:

```bash
sudo apt install python3-venv
```

2. 创建虚拟环境

当前目录

```bash
python3 -m venv .\
```

默认创建一个和当前文件夹名称相同的虚拟环境

```bash
python3 -m venv myvenv # 这样可以创建别的名字
```

3. 启用虚拟环境

在Linux和Mac下

```bash
source ./bin/activate
```

在Windows下

```powershell
.\Scripts\Activate.ps1
```

4. 安装包

虚拟环境启用后，可直接使用pip安装包

```bash
pip install torch
```

相关链接：

pip调用后报错fatal error暴力解决方案 - Anion's Blog (web-of-anion.top)

5. 退出虚拟环境

```bash
deactivate
```

## 常见问题

想重命名项目文件夹or移动虚拟环境在系统中的路径

如果直接重命名或者移动，再次激活虚拟环境就会出现问题。因为虚拟环境配置中有当前文件夹所在的路径。

一种基础的办法是直接删除原来虚拟��境的所有文件，然后重新配置虚拟环境和安包

而以下方案在windows被验证有效，可以免除一些路径问题并且保留原来的packages文件，省去重新安装：

1. 删除python.exe所在的文件夹，比如`Scripts`
2. 备份site-packages文件夹
3. 改文件夹名称
4. 新建虚拟环境
5. 把备份的site-packages放回来
