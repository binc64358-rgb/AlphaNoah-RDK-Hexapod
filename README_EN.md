# AlphaNoah RDK Hexapod

**A D-Robotics RDK X5 + ESP32 hexapod integration project.**

[中文](README.md) · [RDK integration](docs/RDK_X5_INTEGRATION.md) · [Attribution](THIRD_PARTY_NOTICES.md)

Based on the [ViolinLee/NodeHexa](https://github.com/ViolinLee/NodeHexa) 2.1.0 firmware package, this project adds an RDK X5 USB serial bridge. The RDK is the upper-level computing/control platform. The ESP32 executes motion commands and drives the hexapod through PCA9685 boards.

**Hardware status:** on 2026-11-02, the maintainer confirmed that the physical RDK X5 and hexapod already communicate and operate together. This is a maintainer-reported result, not an independent hardware test performed for this documentation release. Command-level evidence, photos and video remain to be archived.

## Architecture and scope

```text
RDK X5 upper-level application
  -> USB serial / 115200 baud / newline-delimited commands
  -> ESP32 processRdkCommand()
  -> motion, calibration and output control
  -> PCA9685 / hexapod servos
```

The repository contains the ESP32 firmware and its RDK-facing protocol. The actual RDK-side application has not yet been archived here as a standalone client. The existing `Serial2` UART JSON interface is separate.

The USB bridge and enable/disable, movement and diagnostic handlers exist in source. Physical integration is maintainer-confirmed. Web control, calibration and motion-planning code is inherited from upstream. No validated vision, autonomous inspection, navigation or AI-driven motion loop is claimed here.

Important limitations: `GET_ANGLES` returns a software cache, not measured joint feedback. `SIT` selects the same standby movement as `STAND`; it is not a distinct sitting pose. `STOP` clears software state and is not a physical power-cut emergency stop. See the [protocol](docs/RDK_X5_INTEGRATION.md).

## Build

The firmware target is ESP32 / NodeMCU-32S, PlatformIO + Arduino. In an already configured environment, from the repository root:

```bash
python -m platformio run -d firmware -e nodemcu-32s
python -m platformio run -d firmware -e nodemcu-32s -t buildfs
```

This documentation publication did not install dependencies, rebuild, flash or operate hardware. The configuration retains historical Windows port settings; select the actual device explicitly before any upload. Exact dependency versions are not fully locked. Historical files in `firmware_bin/` are not proof of a fresh reproducible build.

## Layout

- `firmware/`: actual PlatformIO project.
- `arduino_reference/`: reading reference, not a standalone complete Arduino sketch.
- `firmware_bin/`: historical binaries and SPIFFS image.
- `hardware/`, `mechanism/`, `resource/`: preserved upstream reference materials.
- `workspace/pathTool/`: upstream motion-path tools, not the RDK runtime client.
- `docs/`: integration protocol and publication checks.

The primary integration target is the hexapod. Retained quadruped files do not establish RDK validation on a quadruped. Legacy artifact filenames and the inherited `2.1.0` firmware macro are unchanged.

## DDC 2026 baseline

This repository records pre-event work. Future submissions must distinguish it from work completed during the hackathon, including actual hardware results and AI-assisted development records. See the [official event site](https://hackathon.d-robotics.cc/).

The optional [rdk-docs MCP guide](https://developer.d-robotics.cc/rdk-docs-mcp.md) helps retrieve documentation. It is not a firmware runtime dependency.

## License and contributions

Project software is distributed under GNU GPL v3.0; see [LICENSE](LICENSE). RDK integration contributions follow the same license. Third-party components retain their own notices and terms. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md); no ownership or expanded rights are claimed over upstream hardware, mechanical designs or images.

Contributions should include board/version details, reproducible steps and redacted logs. RDK client code, wiring records, calibration evidence and physical demonstration video are welcome. See [SECURITY.md](SECURITY.md) and [CHANGELOG.md](CHANGELOG.md).
