# Obtaining the source code
## Official Kernel Source 
- Download from kernel.org/pub/linux/kernel
>wget http://kernel.org/pub/linux/kernel/v.4.x/linux-4.4.xz

-For RPM based distro
> yumdownloader -source kernel
> rpm -i kernel*.rpm
> cd ~/rpmbuild/SPECS(recipe for how to build)
> rpmbuilf -bp kernel.spec
> cd ../BUILD
> ls

For Debian based distro <Ubuntu>:
> git clone git://kernel.ubuntu.com/ubuntu-<release codename>.git
	
## The kernel Makefile

>-make help (for make options)
>-make menuconfig or xconfig  are common choices for configuring kernel.
- All configs are stored in .config(should not be edited by hand)
- Other important targets bzImage, modules, modules_install, install, clean

### make help:
*Cleaning Targets*
- clean - (removes all generated .ko files)
- mrproper (removes all generated files + config +various backup files)
-distclean -(mrproper +remove editor backup and patch files) 

*Configuration Targets* => updates current config utilising the listed programs 
- config - (line oriented program)
- nconfig - (ncurses menu based program)
- menuconfig - (menu based program)
- xconfig - (QT based front-end)
- gconfig - (GTK based front-end)
	
## Documentation -source code
- Check the Documentation sub-directory in the source tree
	
![[major_minor_nos 1.png]]
	
## Searching the kernel
*grep -rl* 
-is handy for finding stuff in the documentation directory
>grep -rl ftrace .| grep -v output/
>make dochelp
	
*cscope*
>make cscope -d (to launch)
- move top to bottom with tab key
- exit with Ctrl -d
	
*Tags*
	
- time make tags -(to time how long it takes to make tags)
- vi -t <TAG>
-tn (tag next in vi)
-Ctrl-t -(takes you back one step)
- tag atomic_inc
- tag file
- :tags (shows tag stacks)
	
## include subdirectory
- kernel has its own include file separate from /usr/include
## fs
-filesystem
- Virtual (proc and sysfs)
- On-disk (ext{2,3,4,}, btrfs, and xfs
- Network (nfs)
- Compatible(ntfs, fat and hfs{apple/mac})
## arch
- Support for the different architectures
- Contains config file for different machines in the config directory
## Security 
- security.c provides the fundamental hooks that SELinux and apparmor and other security systems use.

> vi -t sys_read
>Ctrl -] (on Symbol)- goes to the symbol definition
