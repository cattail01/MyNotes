## vscode插件 

搜索并安装vscode插件：

Python（Microsoft 官方） → 代码提示、语法检查

Pymakr（pycom） → 连接开发板、上传代码、串口终端（最常用）

MicroPico / RT-Thread MicroPython（二选一） → 补全与工程模板

推荐组合：Python + Pymakr（ESP32/ESP8266 最稳）

## 安装 MicroPython 依赖工具（命令行）

```bash
# 1. 串口/文件交互工具（Pymakr 依赖） 
pip install adafruit-ampy rshell 
# 2. 固件烧录工具（ESP32/ESP8266） 
pip install esptool
```



---

参考链接

[RT-Thread-packages/micropython: MicroPython port package for RT-Thread](https://github.com/RT-Thread-packages/micropython)
