# High-Level Control

## Remote WebApp (ReactJS) control of local (Android) robot control

```sequence
Title: Peer-to-Peer Control
WebApp->Google Cloud Messaging: VehicleCmd (Protobuf)
Google Cloud Messaging->Android: VehicleCmd (Protobuf)
Android->Motor Control Board: MotorCmd (Protobuf)
Motor Control Board->Android: MotorData (Protobuf)
Android->Motor Control Board: PID-derived MotorCmd
```
