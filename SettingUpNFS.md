# Setting up NFS

## NFS

First, install `nfs-common`

    sudo apt install nfs-common

Then, you will need to change `etc/fstab` file:

    sudo nano /etc/fstab

Add a line to that file:

    192.168.1.3:/	/data	nfs	rw,_netdev	0 0

Where:
* `192.168.1.3` should be replace by whatever address you need.
* `/data` should be replace by whatever mounting point you need.

Them you will need to create folder for mounting point:

    sudo mkdir /data

And then mount everything from fstab:

    sudo mount -av

Depending on the setup of NFS server, you will need to add IP adsress of the NFS cleant to the exports file:

    sudo nano /etc/exports

For example:

    /export  192.168.1.1(rw,sync,no_subtree_check,crossmnt,fsid=0)\
             192.168.1.2(rw,sync,no_subtree_check,crossmnt,fsid=0)
             
## SSHFS
Install sshfs:
  
    sudo apt install sshfs
    
Then, you will need to change `etc/fstab` file:

    sudo nano /etc/fstab

Add line:

    username@host:pathon_host            /mountpoint_path    fuse.sshfs delay_connect,_netdev,user,idmap=user,transform_symlinks,identityfile=path_to_identity_file,allow_other,default_permissions,uid=user_uid,gid=user_gid 0 0

            
Where:
* `192.168.1.3` should be replace by whatever address you need.
* `/data` should be replace by whatever mounting point you need.

For example

    stpidhorskyi@someserver-address.com:/   /data     fuse.sshfs delay_connect,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/stpidhorskyi/.ssh/id_rsa,allow_other,default_permissions,uid=1008,gid=1008 0 0

