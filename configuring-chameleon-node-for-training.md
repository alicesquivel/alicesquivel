---
description: >-
  When you launch your raspberry pi using our image, donkeycar is installed
  automatically for you. But for the baremetal node, we will have to install it
  ourselves.
---

# Configuring Chameleon Node for Training

1. Ssh into the Chameleon instance from your own computer. Run this command in your terminal. You can find the ip address on the Chameleon dashboard under Compute->Instances.

```
ssh cc@<ip address>
```

2. Clone the donkeycar directory into the Chameleon instance in the root directory

```
git clone https://github.com/ChameleonCloud/donkeycar.git

```

3. Move to the donkeycar directory and set up:

```
cd donkeycar
git checkout main
python -m venv .venv
source .venv/bin/activate
pip install -e .[pc] tensorflow==2.12
donkey createcar --path ~/mycar
```

_NOTE: make sure you are always inside your virtual python environment from this point forward. The virtual environment is important so that the compatible version of python is used. You can check if you are in the virtual environment if the prompt in the terminal has a (venv) before the name of the device._

```
(.venv) cc@<device name>:~$
```

**For Nodes with GPU Only: Additional Setup**

1. Run the following commands to utilize the GPU for training with CUDA:

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt install cuda=11.8.0-1
sudo apt show libcudnn8 -a | grep 11.8
```

2. The last command will print output of cudnn versions to the screen. You will have to copy that version into the placeholder in this next command.

```
sudo apt install libcudnn8=<whatever has 11.8>
```

_example: (your version may be different)_

```
sudo apt install libcudnn8=8.9.2.26-1+cuda11.8
```

3. Reboot the machine:

```
sudo reboot
```

4. Check if GPU is seen by the machine

```
python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```

_This line will output information about tensorflow and whether it is able to use the GPU. There may be some warnings at the top of the output, but at the bottom should be information about the GPU._

```
```
