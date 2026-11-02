# AlphaNoah RDK Hexapod

**基于地瓜 RDK X5 与 ESP32 的六足机器人集成项目。**

[English](README_EN.md) · [RDK 接入与协议](docs/RDK_X5_INTEGRATION.md) · [来源与许可](THIRD_PARTY_NOTICES.md)

本项目在 [ViolinLee/NodeHexa](https://github.com/ViolinLee/NodeHexa) 2.1.0 固件包的基础上，增加 RDK X5 到 ESP32 的 USB 串口控制桥。**RDK X5 负责上位计算与控制，ESP32 执行运动控制，PCA9685 驱动舵机。**

实机状态：维护者于 **2026-11-02 确认 RDK X5 已接入六足机器人并能联动**。这是维护者对既有工作的确认；本次仓库整理未重新连接实机、烧录或录制运动结果。逐命令验证、实机照片和演示视频仍待归档。

## 系统架构

```text
地瓜 RDK X5：上位控制程序 / 后续感知与交互扩展
                 |
                 | USB 串口，115200 baud，换行分隔命令
                 v
ESP32 / NodeMCU-32S：RDK 命令桥、运动、校准与输出控制
                 |
                 | I2C；桥接代码检查 0x40 / 0x41
                 v
PCA9685 -> 六足机器人关节
```

当前仓库包含 **ESP32 端固件及 RDK 接口协议**。RDK X5 实机上的上位控制程序尚未作为独立客户端归档在这里；`workspace/pathTool/` 不是该客户端。既有 `Serial2` UART JSON 接口继续保留，与 USB 文本桥分开。

## 当前能力

| 能力 | 证据与边界 |
|---|---|
| RDK X5 与六足实机联动 | 维护者确认；本轮未独立复测 |
| USB 串口桥 | `firmware/src/main.cpp` 的 `processRdkCommand()`；115200、换行结束 |
| 舵机软件输出开关 | 启动标志关闭；支持显式使能/禁用 |
| 动作与调试命令 | 前后行走、转向、待机、停止、单舵机测试与 I2C 检查；语义见协议 |
| Web 控制、校准、动作编排 | 保留上游代码，不全部计为本项目新增工作 |
| 视觉识别、自动巡检、自主导航、AI 自主运动 | 尚无本仓库中已验证的端到端闭环，不作为已完成能力 |

`GET_ANGLES` 返回软件缓存，不是编码器反馈。当前 `SIT` 与 `STAND` 都选择 `MOVEMENT_STANDBY`，没有独立趴下动作。`STOP` 清除软件运动状态，不等于物理断电急停。详见 [协议与操作边界](docs/RDK_X5_INTEGRATION.md)。

## 硬件与构建

主线目标为 RDK X5、ESP32 / NodeMCU-32S、PCA9685 与六足结构。具体 RDK 系统版本、供电、舵机批次和实机接线照片尚未归档，不补造参数。结构/紧固件见 [mechanism/README.md](mechanism/README.md)，上游硬件资料见 [hardware/README.md](hardware/README.md)。四足参考资料不代表 RDK 桥已在四足上验证。

实际构建入口为 `firmware/platformio.ini`。在已经配置好 PlatformIO 的环境中，从仓库根目录执行：

```bash
python -m platformio run -d firmware -e nodemcu-32s
python -m platformio run -d firmware -e nodemcu-32s -t buildfs
```

本次仅整理文档与许可，**未安装构建依赖、未重新编译或烧录**。这些是既有构建入口，不是本次已通过的结果。配置保留历史 Windows 串口设置；实际设备由操作者确认，构建与上传分开。依赖版本尚未完整锁定，不保证任意新环境自动复现。

## 目录

| 路径 | 内容 |
|---|---|
| `firmware/` | ESP32 PlatformIO 工程，实际编译入口 |
| `arduino_reference/` | 便于阅读的桥接参考副本，不是独立完整 Arduino 工程 |
| `firmware_bin/` | 历史固件/SPIFFS 镜像，本次未重建 |
| `hardware/`、`mechanism/`、`resource/` | 保留的上游硬件、结构及图片资料 |
| `workspace/pathTool/` | 上游运动路径工具 |
| `docs/` | RDK 协议与公开整理核验 |

历史文件名中的 `alphanoah1.0` 以及固件宏 `FIRMWARE_VERSION="2.1.0"` 予以保留，避免误称这次文档改名生成了新固件。原构建记录入口为 [ALPHANOAH_BUILD_NOTES.md](ALPHANOAH_BUILD_NOTES.md)。

## DDC 2026 赛前基础

本仓库记录已有的六足硬件、固件桥和 RDK 联动基础。后续应分开记录比赛期间新增代码、AI 辅助开发过程、真机结果与失败样本，不把旧功能计作现场新成果。最终要求见 [地瓜机器人黑客松官网](https://hackathon.d-robotics.cc/)。

[RDK 官方文档](https://developer.d-robotics.cc/rdk_doc_center/)和[rdk-docs MCP 说明](https://developer.d-robotics.cc/rdk-docs-mcp.md)可用于查阅资料；MCP不是运行本固件的依赖。

## 开源与贡献

项目软件按 **GNU GPL v3.0** 发布，见 [LICENSE](LICENSE)。新增 RDK 桥接与说明沿用该许可。第三方模块保留原作者、文件头和许可，见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。上游硬件、结构和图片不宣称为 AlphaNoah 原创，也不扩大其原有开放范围。

欢迎补充 RDK 侧客户端、真实接线图、版本信息、控制链视频和逐命令结果。Issue/PR请附板型、脱敏日志与复现步骤，不提交私人 Wi-Fi 配置、账号凭证或未经授权图像。参见 [SECURITY.md](SECURITY.md)、[CHANGELOG.md](CHANGELOG.md)和[本次核验](docs/PUBLICATION_CHECKS.md)。
