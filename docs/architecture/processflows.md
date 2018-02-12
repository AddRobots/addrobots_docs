# High-Level Control

### Remote WebApp (ReactJS) to vehicle control

```sequence
Title: Remote Vehicle Control
WebApp->GCM: VehicleCmd
GCM->VCU: VehicleCmd
VCU->Shim: MotorCmd
Shim->MCU: MotorCmd
MCU->Shim: MotorData
Shim->VCU: MotorData
VCU->Shim: MotorCmd (PID)
Shim->MCU:  MotorCmd (PID)
```

### Remote WebApp (ReactJS) to direct motor control

```sequence
Title: Remote Motor Control
WebApp->GCM: MotorCmd
GCM->Shim: MotorCmd
Shim->MCU: MotorCmd
MCU->Shim: MotorData
Shim->GCM: MotorData
GCM->WebApp: MotorData
WebApp->GCM: MotorCmd (PID)
GCM->Shim: MotorCmd (PID)
Shim->MCU:  MotorCmd (PID)
```

### Decode

Code | Description
---|---
WebApp | The ReactJS webapp running on a user's device
GCM | Google Cloud Messaging
VCU | The vehicle control programming that runs the local robot's android device
Shim | The motor command handler background process that runs on the local robot's android device
MCU | The physical motor controller tied to Android by USB3 Type-C
