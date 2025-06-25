# 3D Lidar SLAM Challenge

![Screenshot from 2023-09-13 17-06-27](https://github.com/ros2/rclpy/assets/71234974/470940da-0adf-496d-bcbd-3f824eba70c9)

## Background

In the AI & Robotics team, we have been increasingly devoting more resources to 3D lidar-based autonomy. For that reason, we want to propose a challenge that resembles what you would do in your day-to-day work when interacting with this technology.The most important use cases for 3D lidars in our tech stack are mapping, localization and perception. This challenge will focus on the first two.

Simultaneous Localization and Mapping (SLAM) sits at the core of our mapping stack. It is a crucial technology for autonomous navigation in various applications including self-driving cars, mobile robots, and drones. By utilizing precise distance measurements from a lidar sensor, SLAM algorithms can construct accurate 3D maps of the environment while simultaneously tracking the robot's pose within that environment.

While SLAM focuses on building maps and localizing simultaneously, lidar-based localization is equally important. Localization in a pre-existing map allows robots to determine their precise position and orientation without needing to build the map from scratch. This is particularly valuable in scenarios where maps are already available, enabling more efficient navigation and operation.

The project evaluation will consist of a presentation of all your results and a QA session. You may be asked to send your code afterwards as well. Though you won't be asked to deliver a written report or a presentation, we recommend you to do it anyway as it will help you to organize your thoughts and prepare for the QA session.

## Challenge Overview

You will have to run some research on existing SLAM frameworks, choose one, set it up to work with a rosbag we will provide you with, and build a simple evaluation stack that calculates relevant metrics. At the end you should have a 3D map built and a script for calculating the metrics. Optionally you may choose to run a second SLAM stack and compare both of them.

This challenge is designed to familiarize you with the fundamentals of 3D lidar-based SLAM, and to test your abilities to tackle a longer horizon problem that requires some research, planning and execution. You will:

1. Understand and work with point cloud data from lidar sensors
2. Implement or optimize algorithms for real-world scenarios
3. Create accurate 3D maps and/or evaluate localization performance
4. Process and analyze data in a ROS2 (Robot Operating System) environment


## Environment Setup

This repository includes a `.devcontainer` configuration that provides a ready-to-use development environment with:

- ROS2 Humble Hawksbill
- Point cloud processing libraries (PCL)
- Visualization tools (RViz2, PlotJuggler)
- Common dependencies for lidar processing

### Getting Started

1. Ensure you have [Docker](https://www.docker.com/get-started) and [Visual Studio Code](https://code.visualstudio.com/) with the [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension installed.

2. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/3D-Lidar-Slam.git
   cd 3D-Lidar-Slam
   ```

3. Open the project in VS Code and when prompted, click "Reopen in Container" or use the command palette (F1) and select "Remote-Containers: Reopen in Container".

4. The container setup will automatically install all dependencies and configure the workspace.

## Walkthrough

This is a more detailed walkthrough of what you may do

### 1. Setup and Configuration
- Download the provided ROS bag data from [here](https://storage.googleapis.com/autonomy-vision/shared_rosbags/Interviews/med_split.mcap). A map of the area in which the data was generated is also available [here](https://storage.googleapis.com/autonomy-vision/shared_rosbags/Interviews/med_map.pcd). You can view the rosbag using foxglove and the map using CloudCompare
- Build the development environment as described in the getting started section
- [This map](https://kiwi-potree.netlify.app/examples/viewer.html) was generated with the provided rosbag, you can use it as reference for how the map should look like

### 2. SLAM Research
- Run some research on 3D lidar SLAM, there are a ton of open source repositories out there. Some popular ones are:
  - LIO-SAM
  - Kiss-SLAM
  - glim
  - FAST-LIO
  - li_slam_ros2
  - liorf
- Based on the rosbag inspection, choose at least two algorithms that you think are most likely to perform well on this data. You can explore other (newer) options if you want to.
- Clone the repositories and build them in the provided environment. Feel free to change the dockerfile to install more dependencies if needed.
- NOTE: the dockerfile uses ROS2 Humble, but you are also free to chage the distro or even switch to ROS1 if you want to.
- **TODO**: You will be asked questions about SLAM on your project's defense. Be ready.

### 3. Data Processing and Initial Testing
- Set up the SLAM system to process the ROS bag with default parameters. Iterate over the parameters to refine the result.
- Familizarize yourself with the output of SLAM systems
- Save the output maps and trajectories, usually you can view them in CloudCompare, which you can install in your host (outside the container)
- **TODO**: You will be asked to show a live demo of the SLAM package you chose during your project's defense. Be ready.
- **TODO**: You will be asked to show us the maps you built
- After some time trying you may find that:
  - You are unable to make the system work, 
  - It fails after some time and its unable to process the whole rosbag
  - It does not work the same way every time you run the rosbag
- **TODO**: If the above happens, be ready to answer why you think that is and what could be changed to make it work better. This is not supposed to happen though, it should be possible to make it work.


### 4. Quantitative Evaluation
- Run some research on relevant metrics for SLAM, some examples are:
  - Absolute Trajectory Error (w.r.t to a ground truth trajectory, you may use the GPS when accuracy is 1.4cm)
  - Point to Point Error when the system goes through the same place twice
  - Map point cloud density and coverage
  - Processing time per frame
  - CPU/RAM usage
- Choose at least 1 metric and create a script to calculate it from the live output of the SLAM system
- **TODO**: You will be asked to show us the script and walk us through your implementation.
- Organize results in tables and/or graphs
- **TODO** You will be asked to run the script on the live demo of the SLAM system and to show the calculated metric in a graphical manner. A time plot would be nice.

### 5. [OPTIONAL] Algorithm comparison
This section is completely optional, however doing it will give you a significant advantage over the other candidates.
- Choose an additional SLAM algorithm and set it up to run with the data
- Evaluate the metric you chose running both algorithms
- Compare the trajectories and maps generated by both algorithms
- Tell us which one is better and why
- **TODO - Optional** You will be asked to show a live demo of the second algorithm, and to provide a good, technically grounded explanation on why one may be better than the other.
- **TODO - Optional** If you fail to make this one work, be ready to answer the questions for this scenario on the first algoritm

### 6. Final Analysis and Report
- Though we don't ask for a written report, we recommend you to do one anyway as it will help you to organize your thoughts and prepare for the QA session. Some useful material for it could be:
  - A table comparing pros/cons of the systems you did research on
  - Plots with the specific metrics you calculated
  - Insights on the impact of SLAM parameters on the system performance
  - A specific recommendation with reasoning
  - A visualization of the maps side by side (if you did not do the optional, you can compare to the pre-built map we shared)
  - Videos or gifs of the systems in action
- Package all code, data, and analysis into a well-organized repository. Have it ready to be sent as a zip file.


## Evaluation Criteria

There's not a right answer to this challenge, we are more interested in evaluating you ability to tackle a complex problem and the steps you take to solve it rather than in the final results. Some things we will consider are:

- How you do research
- How you translate that research into a solution
- How you design the solution
- How you implement the solution
- How you test the solution
- How you analyze the results
- How you present the results
- How you tackle smaller problems that may arise on the way