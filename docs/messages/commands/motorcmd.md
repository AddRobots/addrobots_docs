### MotorCmd

A motor command message is a single action followed by one or more command parameters, each encoded as a tuple: (param id, value, unit).

```
	message MotorCmd {
		MotorAction action = 1;
		repeated CmdParam paramList = 2;
	}
```

#### MotorAction
##### BRAKE
Stop the motor immediately where it is and apply holding torque.
##### FREEWHEEL
Release all of the windings so that the motor spinds freely.
##### RUN
Run the motor continuously.
##### GOTO_POS
Go to requested position, stop and apply holding torque.

#### CmdParam:
The motor command parameters are sent as a list of tuples: (ID, value, unit). The ID and unit come from an enumerated set and the value is string-encoded. The following is a list of command parameter IDs - we include the unit for clarity. The default value and unit are in paranthesis.
##### CLOCKWISE
The motor movement direction (true, BOOLEAN)
##### POSITION
The motor stop position (0.0, DEGREE)
##### VELOCITY
The motor velocity once fully accelerated (360.0, DEGREE/SEC)
##### ACCEL
The motor acceleration from the current velocity toward the target velocity (15 DEGREE/SEC^2)
##### HOLD_TORQUE
The amount of torque to apply in an attempt to hold the requested position for the commands GOTO_POS or BRAKE. (2.0, Newton)

##### BREAKAWAY

If the motor fails to hold a position, maintain a velocity or accelerate for this much time, it will freewheel. When set to 0 there is no breakaway behavior (0, SEC)

!!! warning
	NB: THIS IN NO WAY ASSURES A HUMAN-SAFE OPERATION - ALL HUMAN SAFETY SYSTEMS MUST BE EXTERNAL TO MOTOR CONTROL.

##### MIN_CURRENT_LIMIT

The minimum current the motor should try to maintain for the active operation. During the active operation, the controller will continuously detect the minimum current required to successfully complete the operation, but it will never go below the MIN_CURRENT_LIMIT. (0.0, AMP)

##### MAX_CURRENT_LIMIT

The maximum current the motor is allowed to draw for the active operation. During the active operation, the controller will continuously detect the minimum current required to successfully complete the operation, but it will never go above the MAX_CURRENT_LIMIT. When coupled with BREAKAWAY, this is a good way to create a safe-operation envelope. (0.5 AMP)

!!! warning
	NB: THIS IN NO WAY ASSURES A HUMAN-SAFE OPERATION - ALL HUMAN SAFETY SYSTEMS MUST BE EXTERNAL TO MOTOR CONTROL.

##### MIN_VOLT_VELOCITY

Apply the MIN_VOLT_LIMIT when the velocity is at or below this value. The controller uses a voltage slope from MIN_VOLT_LIMIT to MAX_VOLT_LIMIT when velocity is between MIN_VOLT_VELOCITY and MAX_VOLT_VELOCITY (180, DEGREE/SEC)

##### MAX_VOLT_VELOCITY

Apply the MAX_VOLT_LIMIT when the velocity is at or above this value. The controller uses a voltage slope from MIN_VOLT_LIMIT to MAX_VOLT_LIMIT when velocity is between MIN_VOLT_VELOCITY and MAX_VOLT_VELOCITY (360, DEGREE/SEC)

##### MIN_VOLT_LIMIT

The voltage to apply when the velocity is at or below MIN_VOLT_VELOCITY. (3, VOLT)

##### MAX_VOLT_LIMIT
The voltage to apply when the velocity is at or above MAX_VOLT_VELOCITY. (24, VOLT)
#### Units
##### STRING

##### INTEGER

##### DOUBLE

##### SECOND

##### DEGREE

##### AMP

##### VOLT

##### NEWTONS

##### UHENRY

#### Sample Commands

An simple motor positioning command might be:

	GOTO_POS
	(POSITION, 180.5, DEGREES)
	(DIRECTION, TRUE, CLOCKWISE)

This would command the motor to turn clockwise until it reached 180.5deg, and it would hold that position with the default torque.

If you need more control of the motor's behavior during that GOTO_POS command, you can add more parameters:

	GOTO_POS
	(POSITION, 180.5, DEGREES)
	(DIRECTION, TRUE, CLOCKWISE)
	(ACCEL, 0.5, DEGREE/SEC)
	(MIN_CURRENT_LIMIT, 0.2, AMP)
	(MAX_CURRENT_LIMIT, 2, AMP)

This would command the motor to turn clockwise, accelerating at 0.5deg/sec with a minimum current of 0.2 amps and a maximum current of 2 amps until the motor reached 180.75 deg and then hold that position by seeking the minimum required current needed to hold the position without going below or above the current limits.

The point is that you can use the motors simply, or with more control - both work.

