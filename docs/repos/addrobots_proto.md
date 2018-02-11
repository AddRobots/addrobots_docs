# AddRobots Protocol Buffers

## Message Processing

The addrobots_proto repo contains the protocol buffer message definitions. We process the raw proto files into code using the `protoc` command.

!!! note "Code Generation"
	We generate and commit the message source code to the repo, so you usually don't need to do this unless you're changing the message prototype files.

### Build script

There is a build script that runs all of the below message code generation. You can still do this by-hand using the sections below this one, or you can run the command:

	> cd ~/git/addrobots_proto/
	
	> ./build.sh
	
This will generate all of the message source code and copy it into the right places.
	
### Protoc

The protoc command comes from the Google github repo: [https://github.com/google/protobuf](https://github.com/google/protobuf). How you build and install protoc is dependent on you. The commands below are correct for protoc v3.3.1.

### NanoPB (protoc for embedded)

In order to generate embedded C message code below, we need to use the NanoPB project: [https://github.com/nanopb/nanopb](https://github.com/nanopb/nanopb). Once you check out this repo, execute the following commands to generate the distribution version:

	> cd ~/git/nanopb
	
	> ./tools/make_XXX_package.sh (where XXX is [linux, mac or windows])
	
This will create a release directory in the NanoPB project's `dist` folder. Use the path to the created sub-folder in the commands below.

### Generate source code

#### Java/Kotlin message generation

	> cd ~/git/addrobots_proto/

	> protoc --proto_path=./SourceMessages/ --java_out=./Production/Java/ ./SourceMessages/VehicleMsg.proto

	> protoc --proto_path=./SourceMessages/ --java_out=./Production/Java/ ./SourceMessages/MotorMsg.proto

#### Javascript message generation

	> cd ~/git/addrobots_proto/

	> protoc --proto_path=./SourceMessages/ --js_out=import_style=commonjs,binary:./Production/Javascript/ ./SourceMessages/VehicleMsg.proto

	> protoc --proto_path=./SourceMessages/ --js_out=import_style=commonjs,binary:./Production/Javascript/ ./SourceMessages/MotorMsg.proto

#### Python message generation

	> cd ~/git/addrobots_proto/

	> protoc --proto_path=./SourceMessages/ --python_out=./Production/Python/ ./SourceMessages/VehicleMsg.proto

	> protoc --proto_path=./SourceMessages/ --python_out=./Production/Python/ ./SourceMessages/MotorMsg.proto

#### Embedded C message generation

	> cd ~/git/addrobots_proto/Production

	> protoc --plugin=nanopb=~/git/nanopb/dist/nanopb-0.3.8-28-g14efb1a-macosx-x86/generator/protoc-gen-nanopb --include_imports=~/git/nanopb/dist/nanopb-0.3.8-28-g14efb1a-macosx-x86/generator/proto/nanopb.proto --proto_path=../SourceMessages -o./MotorMsg.pb ../SourceMessages/MotorMsg.proto

	> python ~/git/nanopb/dist/nanopb-0.3.8-28-g14efb1a-macosx-x86/generator/nanopb_generator.py -f ../SourceMessages/MotorMsg.options --output-dir=../Production/NanoPB MotorMsg.pb

!!! note "NanoPB Dist Folder Version"
	The reason for using the version in the dist folder is because we generated them using protoc v3.3.2 (locally) to support the `proto3` keyword in nanopb. At the moment (25JUL17) the NanoPB project does not support the `proto3` keyword in the default release code.
