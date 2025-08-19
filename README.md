# cuRobo-nvblox-pink-wbc

## Setup

### Prerequisites

1. **JetPack Installation**  
   Flash the Jetson AGX Orin with **JetPack 6.2.1** using the [NVIDIA SDK Manager](https://developer.nvidia.com/sdk-manager) from another Ubuntu or Windows PC.

2. **Storage Upgrade**  
   Install an [NVMe SSD](https://nvidia-isaac-ros.github.io/getting_started/hardware_setup/compute/jetson_storage.html).  
   The base storage is insufficient for NVIDIA’s Docker-based [developer environment](https://nvidia-isaac-ros.github.io/getting_started/dev_env_setup.html). The SSD will host the Docker directory.

### ROS Workspace Setup

1. **Set Workspace Path**  

   ```bash
   echo 'export ISAAC_ROS_WS="$HOME/isaac_ros_ws"' >> ~/.bashrc
   source ~/.bashrc
   ```

2. **Clone Repository**  

   ```bash
   mkdir -p $ISAAC_ROS_WS/src
   cd $ISAAC_ROS_WS/src
   git clone git@github.com:jarkenau/cuRobo-nvblox-pink-wbc.git
   ```

3. **Fetch Dependencies (via VCS)**  

   ```bash
   vcs import < cuRobo-nvblox-pink-wbc/dependencies.repos --recursive
   ```

4. **Dev Environment Alias**  

   ```bash
   echo "alias isaacdev='cd \${ISAAC_ROS_WS}/src/isaac_ros_common && ./scripts/run_dev.sh'" >> ~/.bashrc
   source ~/.bashrc
   ```

### Development

- To start the Docker-based development environment, run:

  ```bash
  isaacdev
  ```

  On the first run, this process may take over an hour because the Docker image will be built directly on the Jetson, with many dependencies from source.

  **Tip:** Check the example sections below for any instructions about rebuilding the Docker image. If rebuilding is required, complete those steps *before* the initial build so you only build it once.

  This command also mounts your workspace into the container.

- In a separate terminal, run `isaacdev` again to attach to the same container.

- **Important:** Dependencies installed inside a running container will only persist for that container’s lifetime. If you need them permenantly add them to the Dockerfile.

## RealSense Example

1. Set up the RealSense camera by following the [official setup guide](https://nvidia-isaac-ros.github.io/getting_started/hardware_setup/sensors/realsense_setup.html).  
   **Note:** This step will trigger a partial Docker image rebuild, which may take some time.

2. Build the ROS workspace:

   ```bash
   colcon build --symlink-install --packages-up-to nvblox_examples_bringup
   source install/setup.bash
   ```

3. Run the example:

   ```bash
   ros2 launch nvblox_examples_bringup realsense_example.launch.py
   ```
