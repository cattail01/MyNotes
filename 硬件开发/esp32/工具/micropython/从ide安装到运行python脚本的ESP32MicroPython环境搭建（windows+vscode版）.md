## 代码库

### MicroPython

- 下载micropython库路径: [https://micropython.org/download/](https://micropython.org/download/)
- MicroPython库路径: [https://docs.micropython.org/en/latest/library/machine.html](https://docs.micropython.org/en/latest/library/machine.html) machine库

配置

```json
{
  "python.languageServer": "Pylance",
  "python.analysis.extraPaths": [
    "D:/micropython-lib/micropython",
    "D:/micropython-lib/python-stdlib"
  ],
  "python.autoComplete.extraPaths": ["D:/micropython-lib/micropython"]
}


## vscode插件

RT-Thread MicroPython


```

## 下载固件、烧录芯片

```bash
esptool.py erase_flash

esptool.py --baud 460800 write_flash 0x1000 ESP32_BOARD_NAME-DATE-VERSION.bin
```

## 连接开发板、创建工程并测试

对照RT-Thread MicroPython主页的步骤进行操作即可

---

## 最终效果

![[Pasted image 20260426131240.png]]

boost文件夹：负责写入固件

![[Pasted image 20260426130608.png|697]]

项目文件：负责开发

![[1dffd9a9-4958-4392-b512-b586490ea190 1.png]]

---

参考链接

[使用MicroPython库搭建ESP32的VsCode开发环境 – 九霄天空-IT技术分享学习](https://turbock79.cn/%e4%bd%bf%e7%94%a8micropython%e5%ba%93%e6%90%ad%e5%bb%baesp32%e7%9a%84vscode%e5%bc%80%e5%8f%91%e7%8e%af%e5%a2%83/)

[RT-Thread-packages/micropython: MicroPython port package for RT-Thread](https://github.com/RT-Thread-packages/micropython)

[MicroPython - 微控制器用的 Python](https://micropython.org/download/ESP32_GENERIC/)
