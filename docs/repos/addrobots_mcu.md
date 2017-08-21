# AddRobots MCU

## Build Instructions

The project is a Kinetis Design Studio 3.x project (KDS 3.2.0) [https://community.nxp.com/docs/DOC-330211](https://community.nxp.com/docs/DOC-330211) 

It takes advantage of the following projects:

* GNUARM Eclipse OpenOCD [https://gnuarmeclipse.github.io/](https://gnuarmeclipse.github.io/)
* MCU on Eclipse Processor Expert beans [https://mcuoneclipse.com/category/processor-expert/](https://mcuoneclipse.com/category/processor-expert/)

Install the tools from these projects into KDS, and then open the project. Then select `Generate Processor Expert Code` and that will generate code from the Process Expoert Beans. The project is likely in `Build Automatically` mode which means the project will build all the code. If it's not, then select `Build Project`. There will be a debug/run configuration called `addrobots_mcu (OpenOCD KL22F) (release)` that should run the code. It's a CMSIS/DAP program/run setup, so if there's compatible device on the USB bus, the IDE will program it and then run/debug the code.

## Project Improvements & Goals

NXP bought Freescale in 2016, and they soon deprecated KDS. They replaced it with a new IDE, MCU Xpresso that's not quite ready for a port of this project. It may be possible to bring Processor Expert into an Eclipse Neon version of MCU Xpresso: [https://mcuoneclipse.com/2017/04/09/mcuxpresso-ide-installing-processor-expert-into-eclipse-neon/](https://mcuoneclipse.com/2017/04/09/mcuxpresso-ide-installing-processor-expert-into-eclipse-neon/)