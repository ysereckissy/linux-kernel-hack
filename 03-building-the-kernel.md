## Chap3 Building the Kernel

#### Useful Commands
ls -lh vmlinux System.map
ls -lh arch/x86/boot/bzImage
file arch/x86/boot/bzImage

##### Installing the Kernel modules

find . -name "*.ko"
find . -name "*.ko" | wc -l
find . -name "*.ko" -ls | egrep -i "vbox|msdos|uio" | awk '{printf "%-40s %9d\n", $11, $7}'

sudo make modules_install
export STG_MYKMODS=../staging/rootfs/my_kernel_modules
make INSTALL_MOD_PATH=${STG_MYKMODS} modules_install

##### Generating the initramfs image and bootloader setup
```bash
sudo make install
```
The initramfs contains a minimum fs with binaries and libraries needed by the kernel in the process of getting the user space ready and before the actual rootfs is mounted. let's say the kernel needs to mount the ext4 fs, but the ext4.ko file is somewhere in the root filsystem not mounted yet. this creates a chicken-egg kind of problem. to resolve that, the ext4.ko can be made par of the initramfs, mounted by the kernel from which it will load the ext4.ko and be able to actually mount the ext4 file system.

##### More on the initramfs framework
initramfs can also be used to get the C runtime ready in the order to decript a disk content.
```bash
lsinitramfs /boot/initrd.img-6.12.94 | wc -l
lsinitramfs /boot/initrd.img-6.12.94
```
Please take a look to the following scripts:
/usr/sbin/update-initramfs and /usr/sbin/mkinitramfs.

```bash
TMPDIR=$(mktemp -d)
unmkinitramfs /boot/initrd.img-6.12.94 ${TMPDIR}
tree ${TMPDIR}
```
#### Useful Links
https://linux.die.net/man/8/depmod
https://github.com/kaiwan/seals

