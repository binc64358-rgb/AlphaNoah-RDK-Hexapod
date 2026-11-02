# AlphaNoah RDK Hexapod firmware notes

Previously named `alphanoah1.0`, this project is based on the NodeHexa 2.1.0 firmware package with an RDK X5 USB serial bridge in `firmware/src/main.cpp`.

- The maintainer-confirmed physical RDK/hexapod integration is now described in [README.md](README.md).
- Actual build target: `firmware/platformio.ini`, environment `nodemcu-32s`.
- `arduino_reference/alphanoah1_0_rdk_bridge_reference.ino` is a reading reference. Its legacy name is retained.
- The inherited `FIRMWARE_VERSION="2.1.0"` macro is not a new DDC release.
- `firmware_bin/` contains historical files; no rebuild or flashing was performed for this documentation publication.
- RDK-side runtime code and command-level captures remain to be archived before claiming a complete reproducible RDK application.

Build commands are in [README.md](README.md). Exact command semantics and limitations are in [docs/RDK_X5_INTEGRATION.md](docs/RDK_X5_INTEGRATION.md).

Original import: `d7757becf5b55e24cd24a96f333f27eb87660a17` (2026-05-12). See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for attribution.
