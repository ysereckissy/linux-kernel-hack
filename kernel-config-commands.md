Chap2: Building the 6.x Linux Kernel from Source -- Part 1
-----------------------------------------------------------

Useful Commands:
----------------
uname -r 
git log --date-order --tags --simplify-by-decoration --pretty=format:'%ai %h %d' 
git clone https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git 
git clone https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git 
export LKP_KSRC=~/kernels/linux-6.1.25 
head Makefile 
scripts/get_maintainer.pl --nogit -f kernel/sched 
make help 
make mrproper 
make defconfig 
cp /boot/config-$(uname -r) ${LKP_KSRC}/.config 

lsmod > /tmp/lsmod.now 
cd ${LKP_KSRC} 
make LSMOD=/tmp/lsmod.now localmodconfig 

make oldconfig 
make listnewconfig 
make helpnewconfig 
make LSMOD=/tmp/lsmod.now LMC_KEEP="dirvers/usb:drivers/gpu:fs" localmodconfig 
make menuconfig 
grep -E "CONFIG_IKCONFIG|CONFIG_LOCALVERSION|CONFIG_HZ_300" .config 
scripts/diffconfig .config.old .config 
scripts/config --disable IKCONFIG --disable IKCONFIG_PROC 
grep IKCONFIG .config 
scripts/config --enable IKCONFIG --enable IKCONFIG_PROC 
grep IKCONFIG .config 
scripts/get_feat.pl --arch arm64 ls --> kernel feature support matrix 

Useful Links:
-------------
https://kernelnewbies.org 
https://kernelnewbies.org/LinuxVersions 
https://github.com/torvalds/linux/tags 
https://www.cip-project.org/ 
https://kernel.org/ 
https://cateee.net/lkddb/web-lkddb/ --> unofficial kernel config database 
https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html --> kernel parameters 
https://elixir.bootlin.com/linux/v6.1.25/source/Documentation/admin-guide/bootconfig.rst 



