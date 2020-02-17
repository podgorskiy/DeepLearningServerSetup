# Deep-Learning Server Setup
This writeup is my notes on setting up a deep-learning server (some aspects applicable for a desktop machine too).
Pullrequests are welcome.

All writeup is for Ubuntu 18.x LTS (Bionic Beaver). But maybe applicable for newer versions.

Server installation is assumed, but everything is applicable for desktop installation too. 

[Desktop and server instalations](./DesktopAndServerInstallation.md)

## Installing openssh-server
Needed for remote ssh access. During Server installation, it will ask if openssh-server should be installed. If it was not installed, or for the Desktop installation, run: 

    sudo apt-get install openssh-server
    sudo service ssh start

## Setting up NFS and SSHFS
[Intructions for NFS and SSHFS](./SettingUpNFS.md)

## Setting up direct ethernet connection between machines.
[Intructions direct ethernet connection between machines](./DirectEthernetConnection.md)

## Nvidia drivers, CUDA, cuDNN
[Intructions for Nvidia drivers, CUDA, cuDNN installation](./NvidiaGraphicsAndCUDA.md)

## IPMI tool and fan control
[Intructions for IPMI tool and fan control](./IPMI_fan_control.md)

## Build essentials
Whether you need to build some native code or not, this might be helpful to build python packages (e.g., dlib)

    sudo apt install build-essential
    sudo apt install cmake
 
## Python
Ubuntu 18.04 does not include /usr/bin/python (Python 2) by default, but it does include /usr/bin/python3 (Python 3).
Because of that, running command `python` will result in error `Command 'python' not found`.
To address that, since python2 is obsolete, I prefer to make a symlink using `update-alternatives`.
Then, to make command `python` refer to python3:

    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10

This will essentially make a symlink /usr/bin/python3 to /usr/bin/python. later on, you can change that with `sudo update-alternatives --config python`

To install pip:

    sudo install python3-pip
    
Similarly, make a symlink pip 

    sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 10

If you have installed both python2 along with python3, then you might need to do (on older distributives, prior 18.x, it may break things):

    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10
   
To change the version of python:

    sudo update-alternatives --config python

    
## Installing some frequently used python packages
I prefer to install frequently used packages globally with pip using sudo. It is not recommended using sudo with pip, but if adhere to a rule to never install python packages with apt, that works fine. This way, all main packages will be immediately available for a new user, and disk space in home directory will not be wasted.

Some packages that make sence to install globally:

    sudo pip install torch torchvision tensorflow-gpu Keras pandas Pillow scipy dlib imageio ninja yacs cython matplotlib tqdm opencv-python scipy scikit-learn scikit-image sklearn  

## Adding a new user
To add a new user:

    sudo adduser <username>
  
To add a new user to sooders:

    sudo usermod -aG sudo <username>

## Enable universe or multiverse repositories
This should be enabled by default unless it was disabled during installation:

    sudo add-apt-repository universe
    sudo add-apt-repository multiverse
    sudo apt update
 
