# ProtoBuf Messages

The system uses Google protocol buffers to encode all messages sent/received by the various subsystems. 

## Vehicle Messages

The top-level vehicle message contains one fields, a union field that contains either a Drive, Orbit or Halt command. The VehicleMsg.proto file contains the following definition for the top-level motor message:

```
message VcuWrapper {
	oneof msg {
		Drive drive = 1;
		Orbit orbit = 2;
		Halt halt = 3;
	}
}
```

## Motor Messages

The top-level motor message contains two fields, a UUID to address the message to a particular motor followed by a union field that contains either a MotorCmd or MotorData. The MotorMsg.proto file contains the following definition for the top-level motor message:

```
message McuWrapper {
	string uuid = 1;
	oneof content {
		MotorData motorData = 2;
		MotorCmd motorCmd = 3;
	}
}
```

### UUID

The motor's universally unique ID as a string. Identifying the motors by UUID means we do not need a central authority to mint new motors that are uniquely addressable.  Any of the UUID encoding formats are fine as long as the stored value is the canonical string representation of 32 base16 digits in the form `8-4-4-4-12` for a total of 36 characters.

