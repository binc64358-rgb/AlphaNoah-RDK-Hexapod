# AlphaNoah 1.0 Firmware Notes

This repository is based on the NodeHexa 2.1.0 firmware package, with a small RDK X5 control bridge added in `firmware/src/main.cpp`.

## Key changes

- Safe boot: servo PWM output is disabled by default.
- USB `Serial` text protocol for RDK X5 control.
- `Serial2` UART JSON frame protocol is preserved.
- SPIFFS Web UI, calibration pages, WebSocket `/cmd`, AP configuration, battery monitor, LED tasks, and motion controllers are preserved.

## RDK X5 text commands

Commands are newline terminated:

```text
PING
ENABLE_SERVOS
DISABLE_SERVOS
CALIBRATE
SERVO <id> <angle>
STAND
SIT
WALK forward 50
WALK backward 50
TURN left
TURN right
STOP
I2C_SCAN
GET_ANGLES
```

## Build

```text
cd firmware
python -m platformio run -e nodemcu-32s
python -m platformio run -e nodemcu-32s -t buildfs
```

Compiled binaries are also copied under `firmware_bin/`.

## Arduino reference

`arduino_reference/alphanoah1_0_rdk_bridge_reference.ino` is a reference copy of the modified `main.cpp` for easier reading in Arduino IDE. The actual build target remains the PlatformIO project under `firmware/`.
