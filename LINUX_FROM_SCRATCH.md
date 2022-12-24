# Linux From Scratch

# Disk layout

I create these partitions during the debian installation, I leave most of the efs4 partitions unmounted except host, that get mounted to / 'root' and debian is installed there.

- sda1 ESP 100 MB
- sda2 boot 200 MB, this allows us to test the same kernel with different version of lfs
- sda3 root 20 GB, this is where are production LFS will end up
- sda4 dev 20 GB, experimenting
- sda5 host 20 GB, debian 11 from live usb
- sda6 src 60 GB, mount will be /usr/src
- sda7 home 500 GB, final not used by the host system
- sda8 swap 8 GB

# Install and start sshd

    sudo apt=get install -y ssh
    sudo systemctl start sshd.service

# Mount the partitions (from chapter 2 section 6 and 7 )

    export LFS=/mnt/lfs
    sudo mkdir -pv $LFS
    sudo mount -v -t ext4 /dev/sda4 $LFS
    sudo mkdir -pv $LFS/home
    sudo mount -v -t ext4 /dev/sda7 $LFS/home
    sudo mkdir -pv $LFS/usr/src
    sudo mount -v -t ext4 /dev/sda6 $LFS/usr/src

# Create minimal set of directories

    sudo mkdir -pv $LFS/tools

