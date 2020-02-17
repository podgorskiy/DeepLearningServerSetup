# Deep-Learning Server Setup
This is a short writeup on setting a deep-learning server (some aspects applicable for desktop too).

All writeup is for Ubuntu 18.x LTS (Bionic Beaver). But maybe applicable for newer versions.

Server installation is assumed, but everything is applicable for desktop installation too. 

[How to turn Desktop instalation into a server one](./DesktopAndServerInstallation.md)

## Nvidia drivers, CUDA, cuDNN
[Intructions for Nvidia drivers, CUDA, cuDNN installation](./NvidiaGraphicsAndCUDA.md)

## Enable universe or multiverse repositories
This should be enabled by default, unless it was disabeled during installation:

    sudo add-apt-repository universe
    sudo add-apt-repository multiverse
    sudo apt update
 
## Build essentials
Whether you need to build some native code or not, this might be helpfull to build python packages (e.g. dlib)

    sudo apt install build-essential
    sudo apt install cmake
 
## Installing python
If Server installation is used, then you will need to install python:
    
    sudo apt install python3
    
Then, to make command `python` reffer to python3:

    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10

If you have installed both python2 and python3, then you might need to do:

    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10
   
To change version of python:

    sudo update-alternatives --config python

Similar for pip:

    sudo install python3-pip
    sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 10

## Installing some frequently used python packages
I preffer to install frequently used packages globally with pip using sudo. It is not recommended, but to use sudo with pip, but if make a rule, to never install python packages with apt, that works fine. This way, all main packages will be immidiatly available for a new user, and disk space in home directory will not be wasted.

Some packages that make sence to install globally:

    sudo pip install torch torchvision tensorflow-gpu Keras pandas Pillow scipy dlib imageio ninja yacs cython matplotlib tqdm opencv-python scipy scikit-learn scikit-image sklearn  

## Adding a new user
To add a new user:

    sudo adduser <username>
  
To add a new user to sooders:

    sudo usermod -aG sudo <username>

## Installing openssh-server
It is already installed for Server instalation, but might be needed for Desktop installation.

    sudo apt-get install openssh-server
    sudo service ssh start

## IPMI tool and fan control
[Intructions for IPMI tool and fan control](./IPMI_fan_control.md)

