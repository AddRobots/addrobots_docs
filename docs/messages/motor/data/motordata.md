### MotorData

A motor data message is a single action followed by one or more command parameters, each encoded as a tuple: (param id, value, unit).

```
	message MotorData {
		DataAction action = 1;
		repeated DataParam paramList = 2;
	}
```

#### DataAction
##### GET

The MotorData message that requests the motor send to send back a MotorData message that contains values for each requested parameter.

##### RESULT

The MotorData message that contains one or more motor data values.

#### DataParam
##### VERSION

Motor version number. The manufacturer controls this value, and it has no meaning with motor control. (The system uses protocol buffers in a backward compatibly way, so versioning should not be necessary.)

##### MFG_DATE

The manufacturing date encoded as YYYYMMDD. The manufacturer controls this value, and it has no meaning with motor control. 

##### MFG_ID

The manufacturer's ID. The manufacturer controls this value, and it has no meaning with motor control. 

##### MODEL_ID

The motor's model ID. The manufacturer controls this value, and it has no meaning with motor control. 

##### INDUCTANCE

The motor's inductance in Henries. This allows the control program to estimate total torque under different voltages and currents.

##### POSITION

The motor's current position in degrees.

##### CURRENT

The instantaneously measured current supplied to the motor windings.

##### VOLTAGE

The instantaneously measured voltage supplied to the motor windings.