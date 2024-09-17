## Project Setup Guide

### Warning: Absolute Paths

In **Main.qml**:
source = "file://" + "/your/path/to/project/images/generated/car_modified_" + modelData.id + ".svg"

In the **applyColorToSVG()** function of `SumoInterface.cpp`:
QString originalFilePath = "/your/path/to/project/images/car-cropped.svg";
QString uniqueFileName = "/your/path/to/project/images/generated/car_modified_" + id + ".svg";

### Work Environment Initialization

1. Update the path to `libsumo.h`:
   - Modify `#include "/your/path/to/project/sumo-integrator-master/lib/sumo/libsumo.h"` in **Sumo.h** to reflect your correct path.
   - Similarly, modify `#include "/your/path/to/project/sumo-integrator-master/lib/sumo/libsumo.h"` in **compound.h**.

2. Compile the project:
   - Run the following command, replacing the path with your Qt6 path:
   cmake -DCMAKE_PREFIX_PATH=/your/path/to/Qt/6.6.0/gcc_64/lib/cmake/Qt6 CMakeLists.txt

   - Then, compile using:
   make

3. Start the SUMO simulation:
   - To run the simulation, execute either of the following commands after generating the executable:
   sumo-gui --remote-port 6066 -c ./sumofiles/osm.sumocfg

   - Or use the shortcut:
   make run

4. Launch the application:
   - In a different terminal, run:
   ./appsumotest

   - Ensure this is done while the simulation is running.

5. Start the simulation in SUMO:
   - Click on the "Play/Run" button in SUMO to begin the simulation.
   - Note: The remote port can be modified by changing its value in `SumoInterface.cpp`.

### Additional Commands in Makefile

- **Run the simulation:**
run:
	sumogui --remote-port 6066 -c "./sumofiles/osm.sumocfg"
.PHONY: run

- **Restart the project (avoids repeating previous commands on each run):**
restart: clean all run
