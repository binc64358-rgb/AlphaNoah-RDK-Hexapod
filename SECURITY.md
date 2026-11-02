# Security and hardware operation

This is experimental robot firmware/integration software, not a safety-certified controller.

- Use a trusted local environment; legacy Web/serial interfaces do not establish production authentication or isolation.
- Software STOP is not physical emergency power isolation. Enabling outputs can move joints; disabling them can remove support torque.
- Mechanically support the robot and verify calibration, clearance and power before motion.
- Do not forward model-generated motion or shell text directly to a device.
- Upstream default AP credentials are factory/reference settings, not protection for public deployment.
- Do not commit private Wi-Fi settings, tokens, device credentials or runtime NVS/flash dumps.
- Historical dependencies have not received a fresh vulnerability audit in this documentation release.

Public Issues should contain only redacted logs and reproduction details, never live credentials or private endpoints. Pattern-based publication checks cannot prove that every secret or vulnerability is absent.
