
# Sync (install)
for synchronizing your local repositories with the remote repositories 
```zsh
pacman -S <name_of_program(s)> 
```
- doing this by itself is not a valid operation 
### Refresh 
```zsh 
pacman -Sy                      # can run -Syy to force a refresh 
pacman -Sy <name_of_program(s)> # will only apple to these programs 
```
- analogous to running `git fetch` 
- synchronizes local package db to the remote db 
### System Upgrade
```zsh
pacman -Syu # refreshes and then upgrades the files that need upgrading 

# NOTE: this literally updates every single package on your system
# including linux itself 
```
- first fetches (refreshes) the most up to date files from the remote repo 
- downloads and installs the latest versions of your packages 

# Pacstrap 
a wrapper around pacman

### Installing Base Linux 
```zsh 
pacstrap -K /mnt base linux linux-firmware
```



