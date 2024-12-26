To ensure the Mac can boot from USB:

1. First, let's properly prepare the USB drive:
    - Format the USB drive using 'Disk Utility' on a Mac if you have access to one, or
    - On your Linux machine, use these commands:
```bash 
sudo fdisk /dev/sdX  # Replace X with your USB drive letter
# Create a new GPT partition table
# Create a FAT32 partition
sudo mkfs.vfat -F 32 /dev/sdX1
```

2. Then create the bootable USB:

- Download the Ubuntu Server ISO
- Use `dd` command on Linux:
```bash 
sudo dd if=ubuntu-server.iso of=/dev/sdX bs=4M status=progress
```

3. On the Mac Pro:
    - Power on while holding the Option key
    - If the USB still doesn't show up, try:
        - Reset the PRAM/NVRAM by holding Command + Option + P + R during startup
        - Try different USB ports (preferably USB 2.0 ports, as they're often more reliable for booting)

Once you can boot from the USB, you can proceed with the installation to the SSD. During installation, make sure to:

- Choose "UEFI" mode when prompted
- Create an EFI boot partition (the installer should do this automatically)