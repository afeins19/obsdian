the init system. The very first process that starts on the computer after the kernel boots up (pid=1). Systemd has many built-in daemons:
- timesyncd 
# Systemctl 
the system daemon. Manages the other daemons that you may be running 
### Status 
```shell
systemctl status <name_of_service> 
```
*note: systemctl will automatically assume the argument ends in .service if not specified*

### Start 
```shell 
systemctl start <name_of_service> 
```
*note: systemctl will not start the process again on the next boot*

### Stop 
```
systemctl stop <name_of_service>
```

### Enable/Disable
```
systemctl enable <name_of_service>    # auto-start on boot 
systemctl disable <name_of_service>   # remove auto-start on boot

# starting after enabling on next boot 
systemctl enable --now <name_of_service> 
```
*note: running the enalbe sub-command will not start the service automatically. User the `--now` to start after enabling.*








