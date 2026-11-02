# 来源与第三方许可

更新：2026-11-02。原仓库名 `alphanoah1.0`；原导入提交 `d7757becf5b55e24cd24a96f333f27eb87660a17`（2026-05-12）保留在Git历史中。改名不把上游成果改称AlphaNoah原创。

## NodeHexa基础

来源：[ViolinLee/NodeHexa](https://github.com/ViolinLee/NodeHexa)，作者ViolinLee / RoboticsCV。既有说明记载基于NodeHexa 2.1.0固件包；导入时没有记录对应上游Git提交，不能用当前master冒充当时版本。

原导入README及上游README声明GPL-3.0。根目录[LICENSE](LICENSE)补齐GNU GPL v3正文，项目新增桥接贡献与说明沿用GPL v3，保留原有版权与作者。GitHub许可识别不代替逐文件来源记录。

继承的来源链还包括：

- [SmallpTsai/hexapod-v2-7697](https://github.com/SmallpTsai/hexapod-v2-7697)：原运动控制来源之一。
- [ViolinLee/PiHexa18](https://github.com/ViolinLee/PiHexa18)：设计与控制参考。
- [78/xiaozhi-esp32](https://github.com/78/xiaozhi-esp32)：上游语音扩展参考，不表示本项目已新增并验证语音闭环。

硬件、结构、图片及原文档保留上游出处和原有开放范围。本项目不对上游未开放的四足PCB、标志或其他资产授予新权利。原导入README的完整署名、教程及链接可在原始提交查看。

## 保留的组件

| 组件 | 位置/版本 | 许可记录 |
|---|---|---|
| ArduinoJson，Benoit Blanchon | `firmware/lib/ArduinoJson/`，6.20.0 | MIT；组件内 `LICENSE.md` 保留 |
| ESP Async WebServer，Hristo Gochkov / me-no-dev | `firmware/lib/ESPAsyncWebServer/`，1.2.3 | 元数据写LGPL-3.0，源码头写LGPL-2.1-or-later；两者原样保留，附[LGPL 2.1](LICENSES/LGPL-2.1.txt)和[LGPL 3](LICENSES/LGPL-3.0.txt)正文 |
| 运动/HAL代码 | `firmware/src/`、`firmware/lib/hal/` | 保留NodeHexa来源和文件头，项目桥接贡献沿用GPL v3 |

ESP Async WebServer原仓库：[me-no-dev/ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)。没有修改其原始版权和LGPL文件头。

## 构建依赖

PlatformIO清单/库元数据引用Adafruit PWM Servo Driver Library、AsyncTCP、Arduino SPI与ESP32 Arduino核心。这些组件不因根目录GPL正文而被重新授权。再分发固件时，应保留实际依赖版本的许可、版权及相应源码要求；本次不生成新的二进制发布包。

许可正文取自GitHub License API的 `gpl-3.0`、`lgpl-2.1`、`lgpl-3.0` 条目，对应[GNU许可目录](https://www.gnu.org/licenses/)。
