For Proxmox on a 2008 Mac Pro, there are a few special considerations:

1. When creating the Proxmox USB installer:
    - You'll need to format it the same way (GPT partition table, FAT32)
    - You can use the same `dd` command method to write the Proxmox ISO
2. The main potential issues you might face are:
    - The Mac Pro uses EFI, but it's an older implementation
    - The graphics card might cause issues during initial install (you might see a black screen)

If you encounter a black screen during boot:

- Try adding `nomodeset` to the boot parameters
- You can do this by pressing 'e' when the GRUB menu appears
- Add `nomodeset` after `quiet` in the boot options

Otherwise, once you get it booting, the installation process is pretty standard:

- It will format the drive
- Set up networking
- Create the root password
- Configure basic system settings

Would you like me to provide the specific commands for preparing the USB drive for Proxmox?