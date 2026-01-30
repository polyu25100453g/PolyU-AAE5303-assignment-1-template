# AAE5303 Environment Setup Report


---

## 1. System Information

**Laptop model:**  
_[ROG Zephyrus M15]_

**CPU / RAM:**  
_[Intel(R) Core(TM) i7-10875H, 16GB RAM]_

**Host OS:**  
_[Windows 10 / Ubuntu 22.04]_

**Linux/ROS environment type:**  
_[Docker container]_

---

## 2. Python Environment Check

### 2.1 Steps Taken

I created a .venv folder with its own Python and pip in the project root. After activation, the shell uses .venv's Python and pip. With the venv activated, I installed all project packages (numpy, scipy, matplotlib, opencv-python, open3d, etc.) inside the venv. 

**Tool used:**  
_[venv]_

**Key commands I ran:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Any deviations from the default instructions:**  
_[Installed git, Python 3, and venv via apt (not present by default). Installed libgl1-mesa-glx/libgl1 for OpenCV/Open3D. Installed ROS 2 Humble and colcon via apt. Installed catkin_pkg, empy, and lark in the venv so colcon build works with the venv Python. Ran smoke tests with ROS sourced before activating the venv. ]_

### 2.2 Test Results

Run these commands and paste the actual terminal output:

```bash
python scripts/test_python_env.py
```

**Output:**
```
========================================
AAE5303 Environment Check (Python + ROS)
Goal: help you verify your environment and understand what each check means.
========================================

Step 1: Environment snapshot
  Why: We capture platform/Python/ROS variables to diagnose common setup mistakes (especially mixed ROS env).
Step 2: Python version
  Why: The course assumes Python 3.10+; older versions often break package wheels.
Step 3: Python imports (required/optional)
  Why: Imports verify packages are installed and compatible with your Python version.
Step 4: NumPy sanity checks
  Why: We run a small linear algebra operation so success means more than just `import numpy`.
Step 5: SciPy sanity checks
  Why: We run a small FFT to confirm SciPy is functional (not just installed).
Step 6: Matplotlib backend check
  Why: We generate a tiny plot image (headless) to confirm plotting works on your system.
Step 7: OpenCV PNG decoding (subprocess)
  Why: PNG decoding uses native code; we isolate it so corruption/codec issues cannot crash the whole report.
Step 8: Open3D basic geometry + I/O (subprocess)
  Why: Open3D is a native extension; ABI mismatches can segfault. Subprocess isolation turns crashes into readable failures.
Step 9: ROS toolchain checks
  Why: The course requires ROS tooling. This check passes if ROS 2 OR ROS 1 is available (either one is acceptable).
  Action: building ROS 2 workspace package `env_check_pkg` (this may take 1-3 minutes on first run)...
  Action: running ROS 2 talker/listener for a few seconds to verify messages flow...
Step 10: Basic CLI availability
  Why: We confirm core commands exist on PATH so students can run the same commands as in the labs.

=== Summary ===
✅ Environment: {
  "platform": "Linux-6.6.87.2-microsoft-standard-WSL2-x86_64-with-glibc2.35",
  "python": "3.10.12",
  "executable": "/root/PolyU-AAE5303-env-smork-test/.venv/bin/python",
  "cwd": "/root/PolyU-AAE5303-env-smork-test",
  "ros": {
    "ROS_VERSION": "2",
    "ROS_DISTRO": "humble",
    "ROS_ROOT": null,
    "ROS_PACKAGE_PATH": null,
    "AMENT_PREFIX_PATH": "/opt/ros/humble",
    "CMAKE_PREFIX_PATH": null
  }
}
✅ Python version OK: 3.10.12
✅ Module 'numpy' found (v2.2.6).
✅ Module 'scipy' found (v1.15.3).
✅ Module 'matplotlib' found (v3.10.8).
✅ Module 'cv2' found (v4.13.0).
✅ Module 'rclpy' found (vunknown).
✅ numpy matrix multiply OK.
✅ numpy version 2.2.6 detected.
✅ scipy FFT OK.
✅ scipy version 1.15.3 detected.
✅ matplotlib backend OK (Agg), version 3.10.8.
✅ OpenCV OK (v4.13.0), decoded sample image 128x128.
✅ Open3D OK (v0.19.0), NumPy 2.2.6.
✅ Open3D loaded sample PCD with 8 pts and completed round-trip I/O.
✅ ROS 2 CLI OK: /opt/ros/humble/bin/ros2
✅ ROS 1 tools not found (acceptable if ROS 2 is installed).
✅ colcon found: /usr/bin/colcon
✅ ROS 2 workspace build OK (env_check_pkg).
✅ ROS 2 runtime OK: talker and listener exchanged messages.
✅ Binary 'python3' found at /root/PolyU-AAE5303-env-smork-test/.venv/bin/python3

All checks passed. You are ready for AAE5303 🚀
```

```bash
python scripts/test_open3d_pointcloud.py
```

**Output:**
```
ℹ️ Loading /root/PolyU-AAE5303-env-smork-test/data/sample_pointcloud.pcd ...
✅ Loaded 8 points.
   • Centroid: [0.025 0.025 0.025]
   • Axis-aligned bounds: min=[0. 0. 0.], max=[0.05 0.05 0.05]
✅ Filtered point cloud kept 7 points.
✅ Wrote filtered copy with 7 points to /root/PolyU-AAE5303-env-smork-test/data/sample_pointcloud_copy.pcd
   • AABB extents: [0.05 0.05 0.05]
   • OBB  extents: [0.08164966 0.07071068 0.05773503], max dim 0.0816 m
🎉 Open3D point cloud pipeline looks good.
```

**Screenshot:**  
_[Include screenshots showing both tests passing]_

<img width="1160" height="959" alt="image" src="https://github.com/user-attachments/assets/e1c69991-8352-4047-89ab-9c4dce86cbec" />
<img width="1163" height="960" alt="image" src="https://github.com/user-attachments/assets/cff8aa36-3b33-4ee1-b23d-8044f1d993e4" />
<img width="719" height="674" alt="image" src="https://github.com/user-attachments/assets/330d8cf1-fe70-4601-a3fe-80d7f745cbc3" />




---

## 3. ROS 2 Workspace Check

### 3.1 Build the workspace

Paste the build output summary (final lines only):

```bash
source /opt/ros/humble/setup.bash
colcon build
```

**Expected output:**
```
Summary: 1 package finished [x.xx s]
```

**My actual output:**
```
Starting >>> env_check_pkg
Finished <<< env_check_pkg [0.37s]

Summary: 1 package finished [1.10s]
```

### 3.2 Run talker and listener

Show both source commands:

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash
```

**Then run talker:**
```bash
ros2 run env_check_pkg talker.py
```

**Output (3–4 lines):**
```
[INFO] [1769722104.254602909] [env_check_pkg_talker]: AAE5303 talker ready (publishing at 2 Hz).
[INFO] [1769722104.754887199] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #0'
[INFO] [1769722105.254779369] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #1'
[INFO] [1769722105.754906651] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #2'
[INFO] [1769722106.254814522] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #3'
```

**Run listener:**
```bash
ros2 run env_check_pkg listener.py
```

**Output (3–4 lines):**
```
[INFO] [1769723459.393141753] [env_check_pkg_listener]: AAE5303 listener awaiting messages.
[INFO] [1769723500.845244172] [env_check_pkg_listener]: I heard: 'AAE5303 hello #0'
[INFO] [1769723501.345250141] [env_check_pkg_listener]: I heard: 'AAE5303 hello #1'
[INFO] [1769723501.845329638] [env_check_pkg_listener]: I heard: 'AAE5303 hello #2'
[INFO] [1769723502.345272830] [env_check_pkg_listener]: I heard: 'AAE5303 hello #3'
```

**Alternative (using launch file):**
```bash
ros2 launch env_check_pkg env_check.launch.py
```

**Screenshot:**  
_[Include one screenshot showing talker + listener running]_

<img width="1084" height="959" alt="image" src="https://github.com/user-attachments/assets/474736c8-cb82-4b00-a1bb-894ce3651a6e" />


---

## 4. Problems Encountered and How I Solved Them

### Issue 1: [The docker container cannot be run on the cursor terminal.]

**Cause / diagnosis:**  
_[There is already a container named "ubuntu22", which has prevented access to Docker in the current environment. The owner of the sudo configuration file in the system is incorrect, and sudo itself cannot function properly.]_

**Fix:**  
_[Delete the old container in the WSL terminal and create a new one.]_

```bash
docker stop ubuntu22
docker rm ubuntu22

docker run -d --name ubuntu22 ubuntu:22.04 sleep infinity
```

**Reference:**  
_[Official cursor docs and AI assistant]_

---

### Issue 2: [Docker cannot be run within the Ubuntu 22 container.]

**Cause / diagnosis:**  
_[Docker is not installed in current Ubuntu 22 container.]_

**Fix:**  
_[Install Docker on the host machine. In the container, only run the application, not Docker.]_

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world
```

**Reference:**  
_[CSDN and AI assistant]_

---

## 5. Use of Generative AI (Required)

The docker container cannot be run on the cursor terminal.

### 5.1 Exact prompt I asked

**My prompt:**
```
run the container directly
```

### 5.2 Key helpful part of the AI's answer

**AI's response:**
```
Currently, it is not possible to directly run the container for you in this environment because:
Docker permissions: The current environment cannot access Docker (permission denied... docker.sock).
Sudo issues: The owner of the sudo configuration file in the system is incorrect, and sudo itself cannot execute normally.
Therefore, you need to execute it in your own terminal on the local machine (do not use the sandboxed terminal provided by Cursor).
Please open a terminal on your computer (such as bash in WSL, wsl in PowerShell, etc.), and then execute:

docker run -d --name ubuntu22 ubuntu:22.04 sleep infinity

If prompted with insufficient permissions, try again:

sudo docker run -d --name ubuntu22 ubuntu:22.04 sleep infinity

After the execution is successful, use the following command to enter the container:

docker exec -it ubuntu22 bash
```

### 5.3 What I changed or ignored and why

**My explanation:**  
_[AI inspired me to make adjustments when containers couldn't be run in the cursor terminal, by using the WSL terminal instead, and to modify the underlying permissions. Because the process of installing WSL2 and Docker went smoothly, I almost forgot about them. AI did not provide unsafe advice. I created a new container based on its concept and further refined the AI's suggestions. The above operations are in line with the security and feasibility requirements specified in the official documents.]_

### 5.4 Final solution I applied

```bash
docker stop ubuntu22
docker rm ubuntu22

docker run -d --name ubuntu22 ubuntu:22.04 sleep infinity

docker exec -i -t ubuntu22 bash
```

**Why this worked:**  
_[Deleting the old container and creating a new one has resolved the original integration issue and facilitated subsequent operations (installing Docker and connecting the cursor).]_

---

## 6. Reflection

**My reflection:**

_[I believe that when configuring the environment, one should not overly rely on a single reference material. Because for different computers, for various reasons, sometimes they will yield different results when performing the same operation. This requires the operator to have a sharp sense of observation and the ability to adapt flexibly to changing circumstances. Fortunately, the application of AI can help us enhance this ability.I was surprised by the significant role that AI played in this process. Configuring the environment used to be a very challenging task, but with the help of AI, it has become much easier.Next time when I undertake such a task, I will carefully study the thinking process of the AI to enhance my ability to identify problems, rather than simply copying the error messages. Now I am quite confident in debugging ROS/Python issues.]_

---

## 7. Declaration

✅ **I confirm that I performed this setup myself and all screenshots/logs reflect my own environment.**

**Name:**  
_[Jiazheng NIE]_

**Student ID:**  
_[25100453g]_

**Date:**  
_[30 January 2026]_

---

**End of Report**
