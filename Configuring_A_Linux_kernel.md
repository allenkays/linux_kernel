

![[kernel_feature_opts.png]]
## make menuconfig
-\[ \] - two choices (boolean)
- <> tristate- (means you have 3 choices)

## Dependencies 
 -greyed out features
 
 ## Search
 /term
 
 ## make xconfig
 **Navigation**
 - mouse oriented
 - click to expand and contract choices

**For choices**
-A dot is for module
 -A check mark is for statically built into kernel
 -Empty means not built
 
 **Searching**
 -there is find under edit menu option
 
 **Saving and Loading**
 - save can be done from the save icon
 - load from the file menu

## .config
- default file 
- found in /boot for different distros
- we can copy the config file of our current kernel 
> cp /boot/config-$(uname -r) .config

*to know the our network driver*
> ethtool -i eth0

**config under arch subdir**
- linux kernel source tree
- A kernel can be configured to store its own config file in the /proc directory

**Kconfig files**
-store instructions to menuconfig or xconfig