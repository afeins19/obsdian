```sh
sudo pacman -S waybar 
```

# Dependencies 
- `otf-font-awesome` (for sway to work) - [OTF Fonts](https://fontawesome.com/how-to-use/on-the-desktop/setup/getting-started)

### Add to Sway Config File 
```sh 
# ~/.config/sway
bar swaybar_command waybar
```

or to the end of the sway config file append
```sh 
# ~/.config/sway
exec waybar
```
