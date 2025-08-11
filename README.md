# cuRobo-nvblox-pink-wbc

A demo integrating [nvblox](https://nvidia-isaac-ros.github.io/concepts/scene_reconstruction/nvblox/index.html) and [cuRobo](https://curobo.org/) for **dynamic collision avoidance** in servoing applications.

## 🚀 Setup

### Prerequisites

1. **JetPack Installation**  
   Flash the Jetson AGX Orin with **JetPack 6.2.1** using the [NVIDIA SDK Manager](https://developer.nvidia.com/sdk-manager) from another Ubuntu or Windows PC.

2. **Storage Upgrade**  
   Install an [NVMe SSD](https://nvidia-isaac-ros.github.io/getting_started/hardware_setup/compute/jetson_storage.html).  
   > The base storage is insufficient for NVIDIA’s Docker-based [developer environment](https://nvidia-isaac-ros.github.io/getting_started/dev_env_setup.html). The SSD will host the Docker directory.

---

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

### 🛠 Development

- Start the environment:

  ```bash
  isaacdev
  ```

  This mounts your workspace into the container.  
- Run `isaacdev` in another terminal to attach to the same container.
