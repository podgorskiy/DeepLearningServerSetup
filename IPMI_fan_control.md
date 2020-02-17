# IPMI fan control

Install IMPI tool:

    sudo apt install ipmitool
    
The most complete guide that I found:  https://forums.servethehome.com/index.php?resources/supermicro-x9-x10-x11-fan-speed-control.20/

To read data from sensors:

    sudo ipmitool sensor
    
To read current fan mode:
    
    sudo ipmitool raw 0x30 0x45 0x00
  
It will return a number, that corresponds to:

* Standard: 0
* Full: 1
* Optimal: 2
* Heavy IO: 4

To set fans to Full:

    sudo ipmitool raw 0x30 0x45 0x01 0x01
    

To set fans to Optimal:

    sudo ipmitool raw 0x30 0x45 0x01 0x02
    
To set fans to Heavy IO:

    sudo ipmitool raw 0x30 0x45 0x01 0x04
    
Standard seems to not work.

It almost always makes sence to set Heavy IO mode. If you notice throttling of GPUs, then it will make sence to set Full for the time of trainig.

