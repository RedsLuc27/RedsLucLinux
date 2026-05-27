# RedsLucLinux

Here is my own linux, running on kernel 7.1.0-rc5 ! 
I'm planning to do update to add features and newer kernels!

# How to run it:

- You can download the iso file from the release or build it yourself!

# How to build it:

You need: 
- gcc
- make
- grub-mkrescue (to make the iso)
- xorriso
- cpio
- qemu-system-x86_64 (for testing)

You need to build the kernel:
(First you need to download it)

make menuconfig
make -j$(nproc)

And then copy the bzImage into the boot directory:
cp arch/x86/boot/bzImage ../iso/boot/

Now the initramfs:
cd iso/boot/initramfs/
find . | cpio -o -H newc > ../initramfs.cpio

If needed move it to the boot directory:
mv ../initramfs.cpio ../

# How to start your fresh build:
- The iso:
in the boot directory run: 
grub-mkrescue -o RedsLucLinux.iso iso
You will have the iso to run in VMWare

User are:
root: without passwd
user: without passwd

- Qemu:
qemu-system-x86_64     -kernel bzImage     -initrd initramfs.cpio     -append "console=tty0"


And voila!

# BE CAREFUL:
This is an initramfs linux so each time you power off the machine NOTHING is saved! 
