# XGO-Duck-Robot-
Hardware Architecture + Simulation Architecture + Complete GitHub Structure.




# XGO-Duck Robot: Complete Project Architecture, Simulation & Components

The goal is to create a new GitHub repository for an AI-powered, 3D-printed walking robot inspired by XGO-Duck. The repository should contain the mechanical design, electronics, firmware, simulation, motion-control software, and a roadmap for reinforcement learning.

I recommend structuring it as a complete robotics engineering project, so someone can understand the design, simulate the robot, assemble the hardware, and eventually train new walking behaviors.

## 1. Overall system architecture

### AI & Motion Planning

Walking policies · Reinforcement learning · Behavior commands

### Robot Control Runtime

Inverse kinematics · Gait generation · Joint trajectories · Safety limits

### Hardware Abstraction Layer

Servo drivers · PWM/I²C or serial communication · Sensors

Compute

Arduino UNO Q or compatible controller architecture

Actuation

15 servo joints, power distribution and mechanical linkages

Feedback

IMU, joint position feedback if supported, contact sensing

Simulation

Virtual joints, ground contact, physics and visualization

Important design principle: simulation and physical hardware should use the same high-level motion commands wherever possible. A simulated robot should not require an entirely different gait algorithm from the real robot.

The architecture above is a proposed implementation architecture, not a verified reproduction of every internal detail of the original XGO-Duck project.

## 2. Official GitHub repositories you should study

The XGO-Duck project is divided into three main repositories. Start with these original resources before creating your own repository.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub

+2



[超能花钱鸭 Fanduck｜Microduck 1:1 个人研究复刻记录](https://images.openai.com/static-rsc-4/UICPoDYxkbvYV_PZzW8sIe1L1FfRlkmzMFFjTRjUZgp5mJ2pQNbmnLUK9eleL9Tb_fsJUCpO1ny9eZjspnyyaQoCbD37JnD8IT_n6WfaECL0NvY0stForz-Ku0RXR-6hV0foOgLXLPL5VsVlNFo5_POxoxYbiHsmX6rBpPXe-9E?purpose=inline)

1\. Hardware and mechanical design

3D models, electronics, assembly guide and bill of materials.

[Open xgoduck_hardware on GitHub](https://github.com/LuwuDynamics/xgoduck_hardware?utm_source=chatgpt.com)

[Arduino Uno Q 2GB/16GB - Raspberry Pi board - LDLC](https://images.openai.com/static-rsc-4/So1v1Rw2X5iot8UulmItfzGcYDW7oqLPI5m0QD15cc6icHzUKTT3ENoOn0XPTr0ceQzhzq-59kNTPZIaCpvBkIcfFRI01vJ-3nCtLhDRhaMa1VKOh8ixHr48pgq6176-ZGgQYlvipH1YgbkOwge3p7QalU9hRlLrsSr9E1gjS_g?purpose=inline)

2\. Runtime and firmware

Servo control, sensor communication, ONNX inference and browser-based robot control.

[Open xgoduck_runtime_arduino on GitHub](https://github.com/LuwuDynamics/xgoduck_runtime_arduino?utm_source=chatgpt.com)

[Open Duck Mini V2 - TechOdyssey](https://images.openai.com/static-rsc-4/GEmGtMpnN42PZ62jly7aubmeONojr858E4GnI5ez4SFLDHA3Tdcr5tNbbrwd99xvzwNS-8wl5WzS_PhTXoxTBbWzyRsY0GMdwUQ33fjJmNqfFWHtOgFevQ03JLii5Qt8x4rz2pZJEOS6lMglKDfpCjy9W16r8BwOirpl9lypWE8?purpose=inline)

3\. Simulation and reinforcement learning

MuJoCo-based robot model, PPO training, simulation environments and ONNX policy export.

[Open xgoduck_rl on GitHub](https://github.com/LuwuDynamics/xgoduck_rl?utm_source=chatgpt.com)

You can also study the original foundation project: [Pollen Robotics Microduck](https://github.com/pollen-robotics/microduck?utm_source=chatgpt.com).

## 3. Complete components list

The following hardware specifications are based on the XGO-Duck hardware documentation. The exact BOM and assembly guide should be your final purchasing references.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub

+1



### A. Mechanical components

| Component                      | Quantity            | Purpose                        |
| ------------------------------ | ------------------- | ------------------------------ |
| 3D-printed body and torso      | 1 set               | Main frame                     |
| Leg and foot components        | 1 set               | Biped walking                  |
| Neck, head and beak components | 1 set               | Duck appearance and movement   |
| TPU foot soles and soft parts  | As designed         | Ground grip and flexible parts |
| Bearings, screws and fasteners | As specified in BOM | Joint assembly                 |
| Servo mounting hardware        | As required         | Secure actuator installation   |

Printing: Use the original STL files and assembly instructions for the matching hardware revision. PLA is a reasonable prototype material to evaluate, but verify the original material recommendations and joint strength before final assembly.

### B. Electronics and sensors

| Component                            | Quantity    | Purpose                                                   |
| ------------------------------------ | ----------- | --------------------------------------------------------- |
| Arduino UNO Q, 2 GB or 4 GB          | 1           | Linux computing and real-time microcontroller             |
| Feetech 1910 serial servos           | 15          | Ten leg joints, four head/neck joints and one mouth joint |
| Matching UNO Q expansion PCB         | 1           | Servo bus, power distribution and IMU interface           |
| QMI8658A 6-axis IMU                  | 1           | Acceleration and angular-velocity feedback                |
| Compatible serial bus cables         | As required | Communication with servos                                 |
| Regulated servo power supply/battery | 1 set       | Actuator power                                            |
| USB-C cable and development computer | 1 each      | Setup, coding and debugging                               |

The UNO Q combines a Linux-capable Qualcomm processor with an STM32 microcontroller. This allows high-level policy inference on Linux while the microcontroller handles time-sensitive hardware communication.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.arduino.cc\&sz=32)

Arduino Docs

+1



### C. Tools and development equipment

- 3D printer and suitable filament/TPU.
- Screwdrivers, hex keys, wire tools and multimeter.
- Computer capable of running Python and the simulation environment.
- A CUDA-capable GPU for the documented reinforcement-learning training workflow.
- USB-C power/data accessories and a suitable servo power setup.

### D. Important power and compatibility considerations

- Do not power 15 servos directly from the Arduino's logic supply.
- Use the matching expansion board and a properly rated servo power system.
- Confirm voltage, current capacity, wiring polarity and grounding before connecting actuators.
- The servo bus and joint calibration must match the actual hardware.
- Keep hands clear of the legs and joints during initial testing.

Do not assume the Arduino UNO R4 Minima can replace the UNO Q in the original runtime. The original implementation depends on the UNO Q's Linux host, ONNX Runtime and MCU communication architecture. An R4-based adaptation would need a different control and inference design.

## 4. Software architecture and technology stack

User interface

Browser dashboard for setup, calibration, motion selection, status and diagnostics.

Technology: HTML, CSS, JavaScript or the original runtime UI

AI inference and policy layer

Loads a trained model, receives robot observations and produces target joint actions.

Technology: Python, ONNX Runtime, exported ONNX policies

Simulation and training

Simulates body dynamics, joint limits, contact with the ground and reward-based learning.

Technology: MuJoCo, mjlab, PPO, BAM actuator models

Embedded control

Communicates with the servo bus, reads IMU data and reports joint state to the host.

Technology: C++/Arduino firmware, Zephyr-based MCU environment and Arduino Bridge

The original runtime documents a 50 Hz neural policy loop and a 100 Hz microcontroller bus loop. Treat these as reference implementation rates, not guaranteed performance for a modified robot.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

LuwuDynamics/xgoduck_runtime_arduino · GitHub

+1



## 5. Simulation architecture and setup

The recommended simulation stack is the one used by the XGO-Duck reinforcement-learning repository: MuJoCo physics through mjlab, PPO training, and ONNX model export.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

LuwuDynamics/xgoduck_rl · GitHub

+1



1\. Robot model

MJCF · Meshes · Mass and inertia · Joint definitions

2\. Physics simulation

Gravity · Ground contact · Servo dynamics · Joint limits

3\. Reinforcement-learning environment

Observations · Actions · Rewards · Episode termination

4\. PPO training

Learn to stand, balance and walk across many parallel simulated environments

5\. Export and validation

PyTorch checkpoint → ONNX policy → runtime compatibility tests

### Recommended simulation setup

The documented XGO-Duck RL project specifies Python 3.12, `uv`, a CUDA-capable GPU, and an mjlab-based training environment.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

LuwuDynamics/xgoduck_rl · GitHub

+1



1. Install a compatible NVIDIA driver and CUDA setup for your system.
2. Install Python 3.12 and the `uv` package manager.
3. Clone the official RL repository and enter its directory.
4. Install the dependencies using the project's lockfile.
5. Run a training task and inspect the resulting checkpoint.
6. Export the selected checkpoint to ONNX and validate its input/output interface.

Example commands for the official repository:

```

git clone https://github.com/LuwuDynamics/xgoduck_rl.git
cd xgoduck_rl

uv sync

# List available training tasks
uv run list-envs

# Train a walking policy
uv run train Mjlab-Velocity-Flat-XgoDuck

# Evaluate the trained policy
uv run play Mjlab-Velocity-Flat-XgoDuck

```

The official project documents additional tasks for standing up, rough terrain, picking objects and other behaviors. Training hundreds or thousands of simulated environments can be resource-intensive; start with a smaller supported environment count if your hardware permits it.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

LuwuDynamics/xgoduck_rl · GitHub

+1



### Simulation features your own repository should document

- Robot body dimensions and mass properties.
- Joint names, axes, limits and servo-to-joint mapping.
- Ground contact and friction assumptions.
- IMU observations and sensor noise.
- Action scaling and actuator dynamics.
- Walking rewards, fall detection and episode termination.
- Training configuration, checkpoints and evaluation results.
- Sim-to-real calibration and safety procedures.

Important: a robot that walks successfully in simulation is not automatically safe or stable in the real world. Validate joint ranges, torque limits, servo direction, timing and power requirements before enabling learned policies on physical hardware.

## 6. Recommended structure for your new GitHub repository

Create one main repository that documents the complete project and connects all three upstream repositories.

```

xgo-duck-robotics/
├── README.md
├── LICENSE
├── THIRD_PARTY_NOTICES.md
├── CONTRIBUTING.md
├── .gitignore
│
├── docs/
│   ├── system-architecture.md
│   ├── hardware-assembly.md
│   ├── electronics-and-power.md
│   ├── simulation-guide.md
│   ├── reinforcement-learning.md
│   ├── deployment-guide.md
│   └── troubleshooting.md
│
├── hardware/
│   ├── README.md
│   ├── bill-of-materials.md
│   ├── mechanical-design.md
│   └── electronics.md
│
├── firmware/
│   ├── README.md
│   ├── communication-protocol.md
│   └── calibration.md
│
├── simulation/
│   ├── README.md
│   ├── robot-model.md
│   ├── environment-configs/
│   └── evaluation/
│
├── ai/
│   ├── README.md
│   ├── observation-design.md
│   ├── reward-design.md
│   └── policy-export.md
│
├── scripts/
│   ├── setup.sh
│   └── validate-environment.sh
│
└── upstream/
    ├── hardware/     # Git submodule
    ├── runtime/      # Git submodule
    └── rl/           # Git submodule

```

This structure separates your own engineering documentation and tools from the original source code. The `upstream/` folders can track the original repositories without copying all their files into a new repository.

Note that `environment-configs/` and the other documentation files above are proposed folders; they are not claims that these exact files already exist in the upstream repositories.

## 7. Create your new GitHub repository and upload the project

My recommendation is to name your repository `xgo-duck-robotics`. It will serve as the main project page, with the original hardware, runtime and simulation repositories connected as Git submodules.

### Step 1 — Create a new repository

Open [GitHub — Create a new repository](https://github.com/new?utm_source=chatgpt.com).

Use these settings:

- Repository name: `xgo-duck-robotics`
- Description: `Complete XGO-Duck robotics project featuring 3D-printed hardware, embedded control, physics simulation, and reinforcement learning.`
- Visibility: Public, if you want others to explore and contribute.
- Initialize with README: Leave unchecked if you are uploading an existing local project.

### Step 2 — Clone the three original repositories into your project

Run the following commands in your terminal:

```

mkdir xgo-duck-robotics
cd xgo-duck-robotics

git init
mkdir upstream

git submodule add https://github.com/LuwuDynamics/xgoduck_hardware.git upstream/hardware

git submodule add https://github.com/LuwuDynamics/xgoduck_runtime_arduino.git upstream/runtime

git submodule add https://github.com/LuwuDynamics/xgoduck_rl.git upstream/rl

git submodule add https://github.com/pollen-robotics/microduck.git upstream/microduck

```

These commands register the original projects as submodules rather than copying their source files. Git records the particular revision of each submodule, helping you keep track of compatible versions.

### Step 3 — Add your own documentation

Create a `README.md` in the root directory. You can use the following starter content.

```

# XGO-Duck Robotics

An open-source robotics engineering project focused on
biped locomotion, embedded systems, simulation, and
reinforcement learning.

## Project Goals

- Understand and document the XGO-Duck architecture.
- Explore the 3D-printed mechanical structure.
- Study embedded servo and sensor control.
- Simulate robot motion using MuJoCo and mjlab.
- Train and evaluate reinforcement-learning policies.
- Document safe deployment from simulation to hardware.

## System Components

- Arduino UNO Q
- 15 serial servos
- QMI8658A IMU
- Custom expansion PCB
- 3D-printed mechanical assembly
- MuJoCo / mjlab simulation
- PPO training and ONNX policy inference

## Repository Layout

- `upstream/hardware/` - Original hardware project
- `upstream/runtime/` - Embedded runtime
- `upstream/rl/` - Simulation and RL training
- `upstream/microduck/` - Upstream reference project
- `docs/` - My architecture, setup and test documentation

## Getting Started

Review the hardware BOM and assembly guide first.
Then inspect the runtime and simulation documentation
before attempting physical deployment.

## Attribution

This project builds on the XGO-Duck and Microduck
open-source ecosystems. See THIRD_PARTY_NOTICES.md
and the original repositories for licensing information.

## Project Status

Documentation and integration in progress.
Hardware and simulation results will be added
as they are verified.

```

### Step 4 — Commit and push to GitHub

After adding `README.md`, create your documentation folders and add your other files. Then run:

```

git add .
git commit -m "Initial XGO-Duck robotics project structure"

git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/xgo-duck-robotics.git

git push -u origin main

```

Replace `YOUR_USERNAME` with your GitHub username. Make sure you have created the repository online first.

When someone clones your new repository, they can retrieve the connected source repositories with:

```

git clone --recurse-submodules https://github.com/YOUR_USERNAME/xgo-duck-robotics.git

```

## 8. Important: if you want every source file inside one repository

Git submodules are not the same as placing all the source files directly inside one repository. If you specifically want one self-contained repository, you have two alternatives:

- Fork the original repositories individually to preserve their histories, then maintain your own integration repository.
- Vendor their files into your repository only after checking the applicable licenses, preserving required notices, and documenting the source revisions.

The XGO-Duck hardware project identifies its relationship to Pollen Robotics' Microduck, and its upstream documentation warns that the exact source and permissions still need to be checked. The RL repository identifies its own Apache 2.0 license; do not assume that every file across all repositories has identical licensing terms.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub

+2



## 9. Final development roadmap

1. Phase 1 — Repository and documentation: Create the GitHub repository, add the architecture diagram, document dependencies and track upstream revisions.
2. Phase 2 — Hardware: Verify the BOM, mechanical model, PCB revision, servo specifications and power system.
3. Phase 3 — Simulation: Set up the documented MuJoCo/mjlab environment, run an existing walking task and record reproducible results.
4. Phase 4 — Control and AI: Study the runtime communication protocol, inspect the pretrained policy and test ONNX compatibility.
5. Phase 5 — Physical testing: Calibrate the servos, validate the IMU, test with suitable support and progressively verify safe movements.
6. Phase 6 — Your own innovations: Add original walking experiments, new simulation tasks, better documentation and verified improvements.

My recommendation: first build a clean, professional integration repository that links the three original projects. Once you understand how the hardware, firmware and simulation work together, develop your own modifications in clearly separated folders and document what you have personally implemented and tested.

That gives you a stronger engineering portfolio than simply uploading copied files: it demonstrates architecture, reproducibility, simulation, embedded systems and AI integration.


![Uploading image.png…]()
