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

[使用MicroPython库搭建ESP32的VsCode开发环境 – 九霄天空-IT技术分享学习](https://turbock79.cn/%e4%bd%bf%e7%94%a8micropython%e5%ba%93%e6%90%ad%e5%bb%baesp32%e7%9a%84vscode%e5%bc%80%e5%8f%91%e7%8e%af%e5%a2%83/)

[RT-Thread-packages/micropython: MicroPython port package for RT-Thread](https://github.com/RT-Thread-packages/micropython)

[MicroPython - 微控制器用的 Python](https://micropython.org/download/ESP32_GENERIC/)
