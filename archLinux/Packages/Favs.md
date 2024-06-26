1. format the drive
2. mount it to the installation media
3. install packages with pacstrap ```pacstrap /<machine location> <big list o' packages>```

# Base Packages (Required) - USING PACSTRAP
- [x] base (basic utilities)
- [x] linux (kernel)
- [x] linux-firmware (firmware)
- [x] grub (bootloader)
- [x] networkmanager (networking)
- [x] man-db
- [x] man-pages
- [x] texinfo
- [x] intel-ucode
- [x] nano 
- [x] less

# Pacstrap (the command that installs arch)
runs in the installer - use it to download files

# Terminals (options)
- [ ] kitty
- [ ] gnome-terminal

# Graphics Drivers
- [ ] Mesa
- [ ] vulkan-radeon

# Desktop 
- [ ] **GOOD DISPLAY SERVER** HYPERLAND 
- [ ] sddm (display manager)
- [ ] redshift (warm colors at night)
- [ ] mesa (OpenGL implementation) 

# Daemons 
- [ ] Dundst (notification daemon)

# Internet
- [ ] firefox 
- [ ] thunderbird (mail client)
- [ ] discord 
- [ ] signal-desktop (signal messenger)
- [ ] zoom 

# Bluetooth 
- [ ] bluez

# Productivity
- [ ] okular (doc viewer)
- [ ] obsidian (da bomb)
- [ ] cups (printing system)
- [ ] cups-pdf (pdf printer)
- [ ] texlive-most (latex)
- [ ] onlyoffice (office suite)
- [ ] zotero (bibliiography manager?)

# Fonts
- [ ] nerdfonts (heard it was good)
- [ ] noto-fonts
- [ ] noto-fonts-emoji
- [ ] notofonts-cjk

# Audio
- [ ] pipewire (audio processor/router)
- [ ] pipewire-pulse (Pulse Audio replacement)
- [ ] pipewire-jack (JACK replacement?)
- [ ] pamixer (CLI mixer)
- [ ] helvum (Pipewire Patchbay)
- [ ] ffmpeg (Audio/Video Converted)
- [ ] vlc (multimedia player)
- [ ] mixxx (djing)
- [ ] spotify 
- [ ] obs-studio (streaming)

# Graphics
- [ ] gimp (image editor)
- [ ] inkscape (vector graphics editor?)

# Development 
- [ ] base-devel (basic build tools)
- [ ] dotnet-sdk (.NET Core)
- [ ] swi-prolog (Prolog Environment)
- [ ] vscodium (non-telemetry based vscode)
- [ ] ninja (build system)
- [ ] clang (c/c++ support)
- [ ] sqlite (embedded databases)
- [ ] nodejs (js runtime)
- [ ] jdk-openjdk (java)
- [ ] gradle (jvm build tool)
- [ ] maven (another jvm build tool)
- [ ] ruby (script language)
- [ ] rustup (rust toolchain installer)
- [ ] go (go compiler)
- [ ] valgrind (Memory debugger)
- [ ] rider ide (figure out how to git it to make c# stuff)
- [ ] pycharm-community-edition

# Container 
- [ ] podman (OCI runner)
- [ ] podman-compose (compose file runner)

# Server 
- [ ] [`traefik`](https://archlinux.org/packages/community/x86_64/traefik/) (Reverse proxy)
- [ ] [`nginx`](https://archlinux.org/packages/extra/x86_64/nginx/) (Web server)
- [ ] [`postgresql`](https://archlinux.org/packages/extra/x86_64/postgresql/) (Database)
- [ ] [`shairport-sync`](https://archlinux.org/packages/community/x86_64/shairport-sync/) (AirPlay server)

# Sysadmin
- [ ] ansible (IT Automation)

# CLI Tools
- [ ] yay (AUR helper)
- [ ] antidote (zsh package manager) 
- [ ] trash-cli (trash helper)
- [ ] tree (directory listing command)
- [ ] fzf (fuzzy finder)
- [ ] jq (JSON processor)
- [ ] zip (zip archiver)
- [ ] unzip (zip unarchiver)
- [ ] whois (whois client)
- [ ] wget (CLI Downlader)
- [ ] rlwrap (readline wrapper?)
- [ ] pacman - packagedownloader 
- [ ] malcontent - flatpack content blocker
- [ ] dwb or chromium - browser 
- [ ] youtube-dl - youtube downloader 
- [ ] mpv - video player
- [ ] bashtop- system monitor
- [ ] tmux - terminal multiplexer 
- [ ] tor - browser 
- [ ] proxychains-ng - use proxy on app?
- [ ] linux-pf - filters ip data
- [ ] irssi - text chat client 
- [ ] gnome-terminal - best terminal? 
- [ ] open-ssh - remote ssh
- [ ] zsh -scripting 
- [ ] python - code
- [ ] socat - connecting different apps? 
- [ ] pacaur - rpc interface for dependency trees? 
- [ ] zaw-git and grml-zsh-config-git - fancy zsh
- [ ] nodejs - javascript
- [ ] vim 
- [ ] `irqbalance` Balances IRQ on multiple CPU cores
- [ ] `curl` gorks those URLs
- [ ] `python-pip` and `requests`, `httpie`
- [ ] `john` crack passwords
- [ ] `gcc` 
- [ ] `wireshark` to sniff packets
