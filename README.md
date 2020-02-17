# Deep-Learning Server Setup Tips

This is a short writeup on setting a deep-learning server (some aspects applicable for desktop too).

All writeup is for Ubuntu 18.x LTS (Bionic Beaver). But maybe applicable for newer versions.

Server installation is assumed, but everything is applicable for desktop installation too. 

Adding a new user:

    sudo adduser <username>
  
Adding new yser to sooders:

    sudo usermod -aG sudo <username>

sudo apt-get install openssh-server
sudo service ssh start

sudo apt-get install nfs-common
sudo nano /etc/ftab

sudo mkdir /data
sudo mount -av
