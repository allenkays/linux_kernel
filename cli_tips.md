# Just important configuration commands

> ethtool -i eth0 (shows network device drivers and other info)

# Tracking file changes
 
> touch NEWER

> find . -type f -newer NEWER -maxdepth 1 (checks what files have changed since we touched the NEWER file)
