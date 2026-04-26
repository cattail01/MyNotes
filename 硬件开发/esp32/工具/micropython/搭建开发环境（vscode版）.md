## 安装基础软件

### 1. VSCode

下载：[https://code.visualstudio.com/](https://code.visualstudio.com/)

### 2. Python

下载：[https://www.python.org/downloads/](https://www.python.org/downloads/)（需 3.8+）

安装时勾选 **Add Python to PATH**。

### 3. USB驱动

ESP32-WROOM 通常使用 **CP210x** 芯片：

下载：[Silicon Labs CP210x 驱动](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

安装后连接开发板，在设备管理器确认端口正常（如 COM3）。

### 4. VSCode 插件

在扩展商店搜索安装：

- **Python**（微软官方）
- **Pymakr**（MicroPython 设备连接、文件同步、串口监视）
- **RT-Thread MicroPython**（可选，国产插件）

### 5. Python 依赖包

```bash
# 串口/文件交互工具（Pymakr 依赖）
pip install adafruit-ampy rshell

# 固件烧录工具（ESP32/ESP8266）
pip install esptool
```

## 创建工程

根据【RT-Thread MicroPython】插件的readme进行环境搭建

---

参考链接

[RT-Thread-packages/micropython: MicroPython port package for RT-Thread](https://github.com/RT-Thread-packages/micropython)

*整理时间：2026-04-24*
在·