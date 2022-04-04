- An object file with .ko suffix
- It contains code to run in kernel
- It Dynamically adds functionality to the running kernel
- It's usually kernel specific.
## Kernel Module Installation
- Installed under /lib/modules 
- module file can be in any directory but the mod probe utility is designed to look under /lib/modules/'uname -r'
- Only used modules built for your specific kernel module and its specific configuration.
- Modules run in kernel mode with full privileges

## Kernel Modules Commands
> lsmod (lists modules loaded, chronologically)
> 
-lsmod | wc -l  (shows all the loaded modules)
-lsmod | grep cifs (shows if cifs module is loaded)
-find / -name '*.ko' | grep 'cifs' (we can see the module dependencies after the colon)
![[cifs_module.png]]
>
> rmmod (removes module) 
> rmmod -f (forcefully removes a module)
> modules dependencies cannot  be removed before the module that uses them is removed.
> 
> ![[rmmod_command.png]]
>  
> modinfo (module info)
> depmod (generates .dep files)
> insmod (inserts module, if it fails or succeeds details of the error can be seen through <dmesg \| tail>) - the insmod command does not load module dependecies automatically.
> 
>  ![[insmod_command.png]]
> 
> modprobe (loads module and its dependencies and also removes modules and dependecies.)
> 
> ![[modprobe_command.png]]
> 
		
## Compiling Modules
> \$make -C /lib/modules/$(uname -r)/build M=\$PWD modules
> - (runs the mod.c file and a makefile with the line <obj-m := mod.o) - the kernel make file will make modules out of '*.o' assigned to the macro <obj -m>
>
>  ![[example_module.png]]
>  
> - the module is made from the mod.o file which is made from the mode.c
> - \<mod.c\> gets compiled into <mod.o>which is then built into the <mod.ko> by the make command above as shown below:
> - mod.c-> mod.o -> mod.ko

- Here is source code for a simple module
- The initialization function is registered using the macro module init
> The exit function is registered using the macro_module exit 
> And the macro license module says the license is GPL
> ![[simple_module.png]]

> Compiling the module
> The path is saved into the current path variable s
> ![[building_module 1.png]]

> inserting and removing the module. 
> ![[insmod_rm_simplemod.png]]


## Modifiable kernel module params
> -modinfo -p  <module.ko>
> -sudo insmod <somemodule.ko> number =9080 word = "Module_params"
> ![[modifiable params 1.png]]

