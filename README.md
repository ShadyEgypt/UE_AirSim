# VR Project


## Setup A: PX4 + AirSim + ROS 2 (WSL)

The instructions below lists **exactly which commands to run in each terminal** to launch:
- Unreal Engine 4.27 (AirSim 1.8.1)
- PX4 SITL
- ROS 2 (PX4 topics)

---

### Unreal Engine (Windows)

1. Open the Unreal Engine project
2. Load the environment/map
3. Ensure:
   - AirSim plugin is enabled
   - GameMode Override = `AirSimGameMode`
4. Click **Play**

Leave Unreal running.

---

### Terminal 1 — PX4 SITL (WSL)

```bash
cd ~/Documents/PX4-Autopilot
make px4_sitl none_iris
```
PX4 will wait for AirSim and then connect via TCP.

### Terminal 2 — Micro XRCE DDS Agent (WSL)

```bash
MicroXRCEAgent udp4 -p 8888
```
Leave this terminal running.

### Terminal 3 — ROS 2 (WSL)
Source ROS 2 and workspace:
```bash
source /opt/ros/humble/setup.bash
source ~/ros2_ws/install/setup.bash
```
List PX4 topics:
```
ros2 topic list
```
Echo a PX4 topic:
```
ros2 topic echo /fmu/out/vehicle_odometry
```

## Setup B: Drone + Car + Python Client

The instructions below **exactly which commands to run in each terminal** to launch:
- Make sure to install and seutp Unreal Engine 4.25
- To setup AirSim 1.3.1 with modifications in the source files, follow these steps
```
git clone https://github.com/microsoft/AirSim.git
cd AirSim
git checkout v1.3.1
git submodule update --init --recursive
```
- Copy augmented files into AirSim directory and replace the original ones
- After that, open Visual Studio 2019 and Select Tools->Command Line->Developer Command Prompt
- Go to AirSim directory and do
```
./Build.cmd
```
- Create a new project in UE4.25 and add a c class so that you can open it in visual studio 2019
- Copy the folder Unreal\Plugins from AirSim folder and Paste it into the Project folder
- Build the project in visual studio 2019
- Then in the project directory, right click on MyProject.uproject and select GenerateProjectFiles
- Hopefully it finishes and then you open the project
- Make the game mode: AirSimGameMode
- Make sure you have the settings.json in Documents/AirSim directory.
- Click Play in UE and you will find the the two vehicles
---

