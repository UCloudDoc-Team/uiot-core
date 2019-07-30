
# C-SDK 快速入门

本章描述如何在 Ubuntu 环境，通过设备端 C-SDK 快速接入 UIoT-Core 平台服务。

## 准备开发环境

* 操作系统：**Ubuntu16.04**
* 必备软件：**make**, **gcc**, **git**, **cmake**

本SDK开发测试均在 64 位 Ubuntu16.04 进行，其他 Linux 版本尚未验证。为避免兼容性问题建议使用相同的编译及运行环境。Windows 环境下，建议使用 WSL(Ubuntu on Windows)。

可使用如下命令安装必备软件：

```bash
sudo apt-get install -y build-essential make git gcc cmake
```

## 获取 C-SDK

* ZIP [下载]() 

## 编译及运行

C-SDK支持 **GNU Make** 及 **CMake** 构建。

### GNU Make

1. 通过修改 C-SDK 顶层目录下的 make.settings 文件，配置开启或者关闭特定功能模块
2. 在SDK顶层目录运行如下命令:

   ```bash
   make clean
   make
   ```

3. 编译完成后, 生成的可执行文件在当前目录的 output/release/bin 及 output/release/unittest 目录下

### CMake

1. 在SDK顶层目录运行如下命令:

   ```bash
   cmake . -Bbuild && cd build && make
   ```

2. 编译完成后, 生成的可执行文件在当前目录的 build/samples 及 build/tests 目录下

