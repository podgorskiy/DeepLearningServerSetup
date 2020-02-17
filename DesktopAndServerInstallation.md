# Ubuntu Desktop and Server Installation

Ubuntu Desktop and Server installation have identical kernels, and mainly differ in that Server installations doen't have some desktop packages.

In fact, one can use desktop installation for the deep-learning server.

You can choose to [delete all GUI](https://askubuntu.com/questions/856373/how-do-you-completely-remove-ubuntu-desktop-along-with-all-installed-packages-wi) [from the installation](https://www.techandme.se/completley-remove-ubuntu-desktop-from-a-ubuntu-server/) to save the disk space:

    sudo service gdm stop
    sudo apt purge ubuntu-desktop -y && sudo apt autoremove -y && sudo apt autoclean

To [remove splash screen and show boot messages](https://askubuntu.com/questions/248/how-can-i-show-or-hide-boot-messages-when-ubuntu-starts), you need to edit `/etc/default/grub`

    sudo nano /etc/default/grub
    
There, line `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` should be replaced by: `GRUB_CMDLINE_LINUX_DEFAULT=""`

Alternatevly, all GUI installation can be left as it is, but [disabled by default](https://unix.stackexchange.com/questions/164005/non-graphical-boot-with-systemd).

To do so, run:
  
    sudo systemctl enable multi-user.target --force

After reboot, it will use text mode. To launch GUI run: `startx`

### Disabling services that are part of Desktop installation:

Disabling some services, that won't be needed for deep-learning server

    sudo systemctl stop whoopsie.service
    sudo systemctl disable whoopsie.service
    sudo systemctl stop kerneloops.service
    sudo systemctl disable kerneloops.service
    sudo systemctl stop cups.service
    sudo systemctl disable cups.service
    sudo systemctl stop avahi-daemon.service
    sudo systemctl stop avahi-daemon.socket
    sudo systemctl disable avahi-daemon.service
    sudo systemctl stop ModemManager.service
    sudo systemctl disable ModemManager.service
    sudo systemctl stop ModemManager.service
    # sudo systemctl stop unattended-upgrades.service
    # sudo systemctl disable unattended-upgrades.service
    
