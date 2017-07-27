## The Project Repos

### addrobots_proto 
the core protocol buffer message definitions. it also includes the top-level project documentation. (For convenience, this project also includes the high-level commands, encoded as protocol buffers, for the reference application.)
### addrobots_webconsole
 a Firebase + ReactJS webapp that acts as a vehicle control console for the reference application.
### addrobots_service
an Android background service that tracks and controls the motors over the USB bus. It provides a simple message-passing API so that any high-level application (that has permission) can control the motors.
### addrobots_vcu
the android "vehicle control unit" reference application that combines drive logic with a PID loop that uses local sensor data, such as OpenCV, Firebase messaging, addrobots_service, and the local IMU.
### addrobots_mcu
an ARM CortexM4 based motor controller firmware that encodes/decodes the USB commands, drives the motor controller ICs, controls the PMIC, and collects/sends any sensor data (rotary encoder, PMIC values, etc).
### addrobots_pcb
the PCB designs for the motor control boards that physically attach to the motor.


