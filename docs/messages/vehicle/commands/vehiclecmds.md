### Drive

A drive command message is a single action followed by six parameters.

```
message Drive {
	double velocity = 1;
	string direction = 2;
	double acceleration = 3;
	double distance = 4;
	double edgeDistance = 5;
	string edgeSide = 6;
}
```

#### velocity
The velocity in meters per second
#### direction
FORWARD, BACKWARD
#### acceleration
The acceleration in m/s^2
#### distance
The distance to travel in meters
#### edgeDistance
The distance to maintain from a side of the vehicle
#### edgeSide
PORT, STARBOARD

### Orbit

A drive command message is a single action followed by six parameters.

```
message Orbit {
	double velocity = 1;
	string direction = 2;
	double acceleration = 3;
	double degrees = 4;
}
```

#### velocity
The velocity in meters per second
#### direction
CLOCKWISE, COUTNERCLOCKWISE
#### acceleration
The acceleration in m/s^2
#### degress
The degrees to turn in direction

### Halt

A drive command message is a single action followed by six parameters.

```
message Halt {
	double acceleration = 1;
}
```

#### acceleration
The acceleration in m/s^2 (0 == instant acceleration)