# Booting
# Understading the Bootloader GRUB

## GRUB's Role
- GRUB comes after POST, and the POST
- GRUB loads the kernel, initial root filesystem, sets up the kernel command line, and then transfers control to the kernel.
- Works with filename completion

## GRUB Configuration
-  GRUB 1 had an editable config file, grub.conf
-  GRUB 2 is more complicated and is found under
> /etc/default/grub
> /etc/grub.d
> Edit or add a config file in /etc/grub.d Normally, edit 40_custom
> run grub2 -nkconfig to generate a new config file.


## Kernel Commandline parameters
- can be checked by dmesg or /proc/cmdline
- Also found in kernel source tree.
> Documentation/kernel-parameters.txt
- registered with  __setup()

- view kernel-parameters.txt
>search /rdinit (specifies what program the kernel should run when it starts up the ram file system image)
> rfkill.default_state (boots the kernel in airplane mode)

## The Initial Root Filesystem
- file sytem that contains /
- initrd(initial RAM disk/RAM filesystem) is used to mount the real filesystem
## The First Process(from Disk)
- when init from initrd terminates, the linux kernel starts init again; this time from the real filesystem.
- Used to be <init> now its <systemd>
- Responsible for starting up system services.
	
## System Services

- For older systems these scripts used to be found in </etc/rc.d>
- systemd service files are found under /etc/systemd/system
> ls -l /usr/sbin/init (shows that it has a soft link to </lib/sytemd /systemd>) 

- When we run file on </lib/systemd/systemd> we see that it is an  ELF 64-bit executable.
> ps -ef | grep init (reveals that init has process id of 1 and its parent process id is 0, meaning it was started by the kernel)
> ls -l /proc/<proc id>/exe ( reveals what executable is being run by the process.)
> ls -l /proc/1/exe (reveals the executable to be systemd)
	
![[init.png]]
	
	
## init RAMFS Images
	
- It is found in /boot (as initrd/initramfs)
- It should have extension .gz 
- If you are going to use the cpio command  to extract ensures < --no-absolute-filenames> or use gunzip or unzip
	
>> Booting with rdinit=/bin/sh will start a shell in the initramfs. 
>> Booting with init=/bin/bash will complete the initramfs and then start witha shellon the disk.
*whatever you program set it to should be from the root file system because that is all that is mounted initially. T he home directory is not yet mounted*
