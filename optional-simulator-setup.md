---
description: >-
  Donkeycar also has a simulated environment available if real-world resources
  are unavailable to you.
---

# Optional: Simulator Setup

**OPTIONAL: Simulator Set-up and Configuration**

1. Create a directory in the root called projects

```
mkdir ~/projects
```

_Note: make sure you have python installed_

2. Inside of this directory, clone the donkeycar repository

```
cd ~/projects
git clone https://github.com/autorope/donkeycar.git
```

_Note: this should create a donkeycar directory inside of the projects directory_

3. Change to donkeycar directory and set it up

```
cd donkeycar
git checkout main
```

Installation for Linux and Windows

```
pip install -e [pc]
```

Installation for Mac

```
pip install -e .\[pc\]
```

4. Download and unzip the simulator for the host pc
   1. [https://github.com/tawnkramer/gym-donkeycar/releases](https://github.com/tawnkramer/gym-donkeycar/releases)
   2. Go to the latest release and click the zip file for your operating system
   3. Unzip the contents
   4. Remember the location and find the absolute file path of the executable file&#x20;

_Note: on Mac, it will download a zip, unzip it and inside of the file is a .app file, two-finger click it and click “Show Package Contents”_

5. Set aside the path which should look akin to: “/Users/kylezheng/Downloads/DonkeySimMac/donkey\_sim.app/Contents/MacOS/donkey\_sim”
6. Clone the donkeycar gym repo in projects and set it up

```
cd ~/projects
git clone https://github.com/tawnkramer/gym-donkeycar.git
cd gym-donkeycar
```

_Note: creates gym-donkeycar directory inside of the projects directory_

Installation for Windows and Linux:

```
pip install -e .[gym-donkeycar]
```

Installation for Mac:

```
pip install -e .\[gym-donkeycar\]
```

7. Creating donkey application

```
cd ~/projects
donkey createcar --path mycar
cd mycar
```

8. File configuration for Donkeycar gym and Simulator

```
nano myconfig.py
```

Use this keyboard shortcut: control + w. Type “gym” and press enter.

Find the area that reads:

```
DONKEY_GYM = False
DONKEY_SIM_PATH = “path to sim”
DONKEY_GYM_ENV_NAME = “donkey-generated-track-v0”
```

Uncomment all three lines by deleting the # at the beginning of the lines

Change the lines to read:

```
DONKEY_GYM = False
DONKEY_SIM_PATH = <path_to_executeable>
DONKEY_GYM_ENV_NAME = “donkey-generated-track-v0”
```

Inside of the <> is the absolute file path for the executable set aside in Step 5

9. Run the Simulator

```
python manage.py drive
```

In a moment, this will open a window with a car in simulated surroundings

_Note: You can not control the car from this window_

Open Google Chrome and type this url in:

```
http://localhost:8887
```

With Joystick mode on, our through a physical game controller, you can control the car, which should propagate from through both the WebUI and the Simulator Opened

_Note: Throttle can be changed from 100% to a lower number, preferably 10%_

10. Configuration&#x20;
    1. Go to the envs directory:
    2. Example file path:&#x20;

```
cd /Users/kylezheng/projects/gym-donkeycar/gym_donkeycar/envs
```

Inside of donkey\_env.py change steer\_limit to 0.5

Reinforcement learning can be found in donkey\_sim.py&#x20;

Other lower priority configurations can be changed from the same files

_Note: Do not attempt to use the simulator trained model in the real world! Remember the Simulator to Real Gap. Although there is a technique utilizing auto-encoders and Soft Actor Critic that allow for robust performance, documentation has not been included (yet)._

\
