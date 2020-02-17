# Deep-Learning Server Setup

This is a short writeup on setting a deep-learning server (some aspects applicable for desktop too).

All writeup is for Ubuntu 18.x LTS (Bionic Beaver). But maybe applicable for newer versions.

Server installation is assumed, but everything is applicable for desktop installation too. 

[How to turn Desktop instalation into a server one](./DesktopAndServerInstallation.md)

## Nvidia drivers, CUDA, cuDNN

[Intructions for Nvidia drivers, CUDA, cuDNN installation](./NvidiaGraphicsAndCUDA.md)

## Adding a new user

To add a new user:

    sudo adduser <username>
  
To add a new user to sooders:

    sudo usermod -aG sudo <username>

## Installing openssh-server
It is already installed for Server instalation, but might be needed for Desktop installation.

    sudo apt-get install openssh-server
    sudo service ssh start

