#Install file

Busybox
git clone git://git.busybox.net/busybox

Last linux
git clone --depth 1 git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git

#Make

In directory busybox :
    * [Required] Libncurses-dev

    sudo make defconfig
    sudo make menuconfig (general setup, static linking)
    make
    make install

In the directory deeper:

    sudo dd if=/dev/zero of=disk.img bs=1M count 16
    sudo mkfs.ext4 disk.img -L root
    sudo mkdir mnt
    cp -r busybox/_install/* mnt

    cd mnt
    sudo mkdir -p /etc/init.d proc sys dev
    echo "proc      /proc   proc    defaults" >> etc/fstab
    echo "sysfs     /sys    sysfs   defaults" >> etc/fstab
    echo "mount -a" >> etc/init.d/rcS
    sudo chmod +x etc/init.d/rcS

In the directory Linux:
    sudo make defconfig
    sudo make

run with Qemu:

/usr/bin/qemu-system-x86_64 -kernel linux/arch/x86/boot/bzImage -hda disk.img -apend "root=/dev/sda console=/ttys0" -nographic


