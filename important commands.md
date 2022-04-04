> ethtool -i eth0 (shows network device drivers and other info)
> touch NEWER
>find . -type f -newer NEWER -maxdepth 1 (checks what files have changed since we touched the NEWER file)