
# Additional Hardware 

### GPU 
Tasks:
- transcoding 
- offloading image tasks (video over shell or something)

- [Dell AMD Radeon R5 430 2GB GDDR5 PCIE 3.0 Graphics Card (109-C86957-00)](https://www.ebay.com/itm/185901995275?_skw=amd+gpu&epid=10037548729&itmmeta=01JG0CHT3KHY5NYK61Q32175MT&hash=item2b489f550b:g:SCsAAOSwhQBkZRvo&itmprp=enc%3AAQAJAAAA4HoV3kP08IDx%2BKZ9MfhVJKkPWpzqoiij9G5s%2BdWqYYw6o4iThMVUPFYINs7i4m%2Bc04hQYseymBJUkyVF1QMWsS0ZcB8B76NdPajsfVidDaoDezYzitM9xg33qYHMEJ4Irw%2Bvr6nPhLmmQF7SzPbDiDdKlWj%2Fnc3BkV0WHVGCgCbi3zm5cS3EBl7GEt3ZyOxBBCRbFv5BVaLOyZV9Q47CIsMBVrYPiONkWBP5icwcJLKD6BAp9Hi%2FFuRaLl42mc3ukNUnFUTZ7GYAWLErzRXVDhZFxweIvcMzOSv23TRJtr6s%7Ctkp%3ABFBM-KHHjIBl)
- [(Fanless) RX 580 8gb (SETUP FOR MINING)](https://www.ebay.com/itm/126813973923?_skw=amd+gpu&itmmeta=01JG0CV42YR1J90G6YTWD0746C&hash=item1d86b3ada3:g:MLYAAOSwLH5nRO7n&itmprp=enc%3AAQAJAAAA4HoV3kP08IDx%2BKZ9MfhVJKk%2B9CzQEkK8jwr8dgBMcknQL5T8%2FG3E4xwJ2NvqOb8qk60vnqEFLBuIz3Mnz2BCp%2F%2BNa0FlY%2BErh1vy8uSeOvLXX6SphRzVQ1z70fyhhyYuen9efXSfWJe9U6gG7ajjCRFNsLR0Na9NQC4v5q8gru6KKYQCxZw3m9h3s6wqyzZIAuVPFa27GUeUnOs1Sy22JVSWEmAKb99dQ%2B7CdM6%2FGlDUTZRB1MeGi9s8xsBLskr%2FLBJv%2Fp5sMWXYjw6KXqr0bqI6L6YXawZGhnM%2FeryA2QLY%7Ctkp%3ABFBMxMHsjIBl)

# OS Boot Drive
- nvme0n1     259:2    0 465.8G  0 disk

# Storage Drives
- 1 x 4tb drive
- 2 x 2tb drive
- 1 x 1tb drive

# Programs
- PhotoPrism - ai photo catalogger 
- Jellyfin 
	- Radarr
	- Sonarr
	- transmission - download client
	- jacket - indexing 
- Mullvad VPN
	- use over wireguard for routing 

# Services that will use Docker

### Media Server - running on KVM 
Jellyfin 
	- Radarr
	- Sonarr
	- transmission - download client
	- jacket - indexing 
 Mullvad VPN
	- use over wireguard for routing 

# LXC 
- linux container - virtualization technology that allows users to run multiple linux os on a single machine

### KVM  
kernel based virtual machines -> required for running docker 
- virtual machine for linux

Computer: https://support.apple.com/en-us/112308

- [ ] Hypervisor: Proxmox (containers and VMs) -> lean into this 

# VM Vs. Container
- container is only the user space
- VM is kernel or hardware level cutoff 


# Software 
- openssh-server
- htop 
- iotop 
- iftop
- et-tools 
- curl
- wget 
- dnsutils
- nfs-kernel-server 
- samba 
- rsync
- docker
- docker-compose
- rclone
- jellyfin
- sonarr
- radarr
- cockpit
- netdata
- fail2ban
- certbot
- python3-certbot-nginx
- git
- python3
- python3-pip
- build-essential
- nodejs 
- npm
- nginx
- wireguard