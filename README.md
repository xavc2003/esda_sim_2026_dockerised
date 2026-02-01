## 2026 ESDA Vehicle Simulation
### 1. Set up
#### 1.1. Install Necessary Dependencies

#### 1.2. Building the Project
- Please clone the repository into the `src` folder of your work space, your folder structure should look like this:
```
|_workspace_name
    |_src
        |_esda_simulation_2025
```
- When you are trying to build the project, please do it in the `\workspace_name` level. So the `log`, `build` and `install` folders are generated next to the `src` folder. 
```
|_workspace_name
    |_src
        |_esda_simulation_2025
    |_install
    |_build
    |_log
```
- To source your local build into the current path, so it can be seen by ros2.
```
source install/setup.bash
```

### 2. Launching Project

#### 2.1. Using the Simulation Manager GUI (Recommended)

The easiest way to run the simulation is using the graphical interface:

```bash
python3 src/esda_simulation_2025/scripts/ui_launch.py
```

The **ESDA Simulation Manager** provides a simple interface to control all aspects of the simulation:

1. **Build** - Click "Colcon Build" to compile changes
2. **Select World** - Choose your .sdf world file from the dropdown
3. **Select Costmap** - Choose "[New Costmap]" for mapping mode, or select an existing map for navigation
4. **Launch Simulation** - Starts Gazebo with your selected world
5. **Launch SLAM** - Start mapping (for new environments)
6. **Launch AMCL** - Start localization (requires existing map)
7. **Launch Nav2** - Enable autonomous navigation
8. **Launch RViz2** - Visualize robot, map, and camera feed
9. **Launch WASD Teleop** - Control robot with keyboard (W/A/S/D keys)
10. **Kill All Processes** - Emergency stop and reset

**Quick Start Workflow:**
- For **Mapping**: Launch Simulation → Launch SLAM → Launch RViz2 → Launch Teleop (drive around to build map)
- For **Navigation**: Select existing costmap → Launch Simulation → Launch AMCL → Launch Nav2 → Launch RViz2

#### 2.2. Manual Launch (Advanced)

If you prefer command-line control:

**Launch Simulator:**
```bash
ros2 launch esda_simulation_2025 launch_sim.launch.py
```

**Teleop (WASD control):**
```bash
python3 src/esda_simulation_2025/scripts/teleop_wasd.py
```
- **W**: Forward | **S**: Backward | **A**: Turn Left | **D**: Turn Right | **X**: Stop
- **U/J**: Increase/Decrease Linear Speed | **I/K**: Increase/Decrease Angular Speed

**SLAM Mapping:**
```bash
ros2 launch esda_simulation_2025 online_async_launch.py use_sim_time:=true
```

**AMCL Localization:**
```bash
ros2 launch esda_simulation_2025 localization_launch.py use_sim_time:=true map:=/path/to/map.yaml
```

**Nav2 Navigation:**
```bash
ros2 launch esda_simulation_2025 navigation_launch.py use_sim_time:=true map_subscribe_transient_local:=true
```
