# simple operating system
 very small OS (fitting into a bootloader) and have very few features
 
 I am using Kali Linux. Get all the tools you need to follow this guide by entering this in a terminal window:

sudo apt-get install build-essential qemu nasm

This gets you the development toolchain (compiler etc.), QEMU PC emulator and the NASM assembler, which converts assembly language into raw machine code executable files.

T build the OS in your home directory, enter:

nasm -f bin -o myfirst.bin myfirst.asm

Here we assemble the code from our text file into a raw binary file of machine-code instructions. With the -f bin flag, we tell NASM that we want a plain binary file (not a complicated Linux executable - we want it as plain as possible!). The -o myfirst.bin part tells NASM to generate the resulting binary in a file called myfirst.bin.

Now we need a virtual floppy disk image to which we can write our bootloader-sized kernel. Copy mikeos.flp from the disk_images/ directory of the MikeOS bundle into your home directory, and rename it myfirst.flp. Then enter:

dd status=noxfer conv=notrunc if=myfirst.bin of=myfirst.flp

This uses the 'dd' utility to directly copy our kernel to the first sector of the floppy disk image. When it's done, we can boot our new OS using the QEMU PC emulator as follows:

qemu-system-i386 -fda myfirst.flp

And there you are! Your OS will boot up in a virtual PC. If you want to use it on a real PC, you can write the floppy disk image to a real floppy and boot from it, or generate a CD-ROM ISO image. For the latter, make a new directory called cdiso and move the myfirst.flp file into it. Then, in your home directory, enter:

mkisofs -o myfirst.iso -b myfirst.flp cdiso/

This generates a CD-ROM ISO image called myfirst.iso with bootable floppy disk emulation, using the virtual floppy disk image from before. Now you can burn that ISO to a CD-R and boot your PC from it! (Note that you need to burn it as a direct ISO image and not just copy it onto a disc.)
