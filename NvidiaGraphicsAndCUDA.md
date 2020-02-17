# Installing Nvidia drivers

My preffered way to install nvidia drivers, is to use `apt-get` to install the driver from cannonical package repository.
For CUDA driver and cuDNN I preffer to install it from Pop!_OS repositories.

## Installing Nvidia graphics driver

To list available nvidia drivers, run:

    apt search nvidia-driver
   
If installing for server installation you will need headless version:

    sudo apt install nvidia-headless-440
    sudo apt install nvidia-utils-440

If installing for Desktop version with GUI installed, you can install (not recommended for headless installation):
  
    sudo apt install nvidia-driver-440

You might need to add Pop!_OS repository first (see below), for the most recent drivers.

To check ndivia driver installation, run:

    cat /proc/driver/nvidia/version

Or:

    nvidia-smi
    
If it gives an error `Failed to initialize NVML: Driver/library version mismatch`, either reboot or run:

    sudo rmmod nvidia_uvm
    sudo rmmod nvidia_drm
    sudo rmmod nvidia_modeset
    sudo rmmod nvidia
    sudo modprobe nvidia


## CUDA and cuDNN
[Add Pop!_OS repository](https://support.system76.com/articles/cuda/):

    sudo echo "deb http://apt.pop-os.org/proprietary bionic main" | sudo tee -a /etc/apt/sources.list.d/pop-proprietary.list
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key 204DD8AEC33A7AFF
    sudo apt update

If that doen't work, it might be due to a firewall, then try:

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key 204DD8AEC33A7AFF
    sudo apt update
    
Then, install CUDA and cuDNN:
   
    sudo apt install system76-cuda-latest
    sudo apt install system76-cudnn-10.1
   
You can install more than one version of CUDA. To switch versions, run:

    sudo update-alternatives --config cuda
    
To check CUDA installation, run

    nvcc -V
    
To check that CUDA code is compilable and runable, create a file `cuda_test.cpp` with the following content:

    #include <cuda_runtime.h>
    #include <stdio.h>

    int main()
    {
        int count;
        if (cudaGetDeviceCount(&count) != 0)
        {
            printf("cudaGetDeviceCount return error\n");
        }
        printf("Number of devices available: %d\n", count);
        return 0;
    }

Then run:

    nvcc cuda_test.cpp -o cuda_test
    ./cuda_test
    
It should comiple and run without error and print number of available gpus.
  
### If it does not work
In certain cases (e.g. CUDA was installed some other way), you might need to run `sudo nano /etc/environment` and add `/usr/lib/cuda/bin` to the `PATH` variable, e.g.:

    PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/cuda/bin"
    
You might need to check `/etc/ld.so.conf.d/`, it should contain a file cuda-*.conf file with `/usr/lib/cuda/lib64`. If there is no one, you will need to create one.

After that, you will need to run:
    
    sudo ldconfig


    
  
