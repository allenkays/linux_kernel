# Kernel
- kernel is a program with the name:
		- vmlinuz-<kernel version>
- It has a boot loader that loads it into memory
		 - most common grub
- It has an API 
		-sytem calls
		-virtual file systems
			- proc
			- sys
			- debug fs
		- device files (system calls)= device drivers
- Enforces privileges
- Executes supervisor instructions
- Implements security policies
- Controls access to hardware and other resources
	
## Kernel is Modular ##

- Kernel is small
- Kernel image is sufficient to boot to user space
- Optiona functionality added after boot
- Allows for alternatives; e.g loading only required drivers for present hardware.
	
- Kernel resides in 
	
> $ (/boot directory)
> $ currently running kernel can be viewed by runnning 
				   (uname -r )
	
## Hardware commands ##

- Applications call functions in libraries. Some of those functions invoke kernel system call.	
- some system calls interact with hardware:

> lshw and lspci
> lsusb and lsbk
> lscpu and lsdev
	
## Commands for HW Control and Config
	
> hdparm
> write()to proc, dev, sys
> inb and outb (disable keyboard )
> setpci 
	
## System Calls ##
	
- Functions implemented by kernel meant to called from user space.
- There are about 300 ~340
-  See:
			> include/uapi/asm-generic/unistd.h
			> documented in man section 2
- They are called through the standard library(e.g libc)
- Standard library uses architecture dependent means to invoke system call mechanism.
- Library involes kernel & determines the system calls to call
	
## System call Return Values:
	
- If an error occurs calls return a negative value to the library
	
> on error the library sets "errno" to abs(return value) and returns -1
>  grep -i read !$   #(greps)
> grep "define __NR_read"  unistd.h | wc -l # This unistd.h file is located in the kernel while unistd. h  is diffrent.
	
## Commands for different kernel info options: ##
> head  /proc/meminfo
				> strace -c <command> (Counts process calls to system calls)
				> strace |  & grep read
> to strace cd: vim cd.sh
					- #!/bin/bash
					- cd "$@"
> strace cd.sh /etc (chdir-system call for cd)
> find / -type d -name asm-generic; cd $_ ; grep "define __NR" unistd.h | wc -l (counts the number of system calls defined in kernel source)
> view unistd.h  (run search as below)
					- /syscalls (more calls than we saw )
					- /unassigned
	
> sleep 100 &
> cd /proc/<id of above (sleep) syscall>/fd  ; ls -l (to get how many files are opened by the sleep syscall)
# Kernel pci commands	
> lspci  | grep -i etherrnet
> find / -type f -name ip_forward 2>/dev/null
> sysctl -a 2>/dev/null | grep ip_forward

# Kernel Disk commands
> cd sys/blk; ls -l /dev/sda*
> strace fdisk -l |& grep sys/dev/block | grep openat |wc -l (How many files are opened by fdis -l )

#dmesg kernel commands
> dmesg | grep -i command
> grep -rl BOOT_IMAGE /
	
> cd /dev; ls -l null 
> ls -l | grep "^c" | grep " 1"	
>cd /tmp; mknod pickle c 1 2
> cat pickle
	


	 
	
	
			