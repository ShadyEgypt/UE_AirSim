# UE_AirSim

## PX4 + AirSim + ROS 2 (WSL) — Run Commands

This file lists **exactly which commands to run in each terminal** to launch:
- Unreal Engine (AirSim)
- PX4 SITL
- ROS 2 (PX4 topics)

---

## Unreal Engine (Windows)

1. Open the Unreal Engine project
2. Load the environment/map
3. Ensure:
   - AirSim plugin is enabled
   - GameMode Override = `AirSimGameMode`
4. Click **Play**

Leave Unreal running.

---

## Terminal 1 — PX4 SITL (WSL)

```bash
cd ~/Documents/PX4-Autopilot
make px4_sitl none_iris
```
PX4 will wait for AirSim and then connect via TCP.

## Terminal 2 — Micro XRCE DDS Agent (WSL)

```bash
MicroXRCEAgent udp4 -p 8888
```
Leave this terminal running.

## Terminal 3 — ROS 2 (WSL)
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
