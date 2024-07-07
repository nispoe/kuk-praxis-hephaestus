# AI Machine Setup
These are the instructions and steps used to setup the AI experimentation machine used during my doctoral experimentation. Technically hardware can vary and versions will vary over time. These are some of my notes and lessons learned. I named the machine Hephaestus.

## Index

- [Rufus](#rufus)
- [Operating System](#operating-system)
- [Journal](#journal)

## Rufus
- used Rufus 4.4
- ubuntu-22.04.3-desktop-amd64.iso
- These are the settings selected on Rufus

  <img src="./images/rufus-drive-properties.png" alt="Rufus Settings" style="width: 400px; display: block; margin-left: 20px;" />

## Operating System
- Installed ubuntu-22.04.3-desktop-amd64.iso using rufus and usbc hard drive. This works fast if you have a 10Gbps drive.
    - Ubuntu (safe graphics)
    - Welcome = Install Ubuntu
    - Keyboard Layout = English (US)
    - Updates and other software
        - What apps would you like to install to start with? = Minimal Installation
        - Other options = uncheck all
    - Installation Type = Erase disk and install Ubuntu (3rd option)
    - Where are you? = Chicago
        - Your name = nispoe
        - Your computer’s name = hephaestus
        - Pick a username = nispoe
        - Password = what you normally put
- After install login and open a terminal window in Ubuntu (not remotely)
- Now is a good time to copy over some files
    - copy /usbc/kuk folder to /home/nispoe/kuk
- Fix problem with PCIe (Updated BIOS and Motherboard VGA Switch)
    - 2024-03-05 - problem with Asus WRX80e motherboard and usb being detected, but still have a problem…
    - 2024-03-06 - turn off the VGA switch on the motherboard, this works with BIOS update
    - 2024-03-06 - https://forum.level1techs.com/t/solved-asus-pro-ws-wrx80e-sage-se-wifi-not-detecting-all-my-nvme-drives-in-proxmox/189373
        1. `cd /etc/default/`
        2. `vim grub`
        3. edit line: `GRUB_CMDLINE_LINUX_Default="quiet"`
        4. update to: `GRUB_CMDLINE_LINUX_DEFAULT="quiet pci=nommconf"`
        5. Escape button → `:wq`
        6. `update-grub`
        7. Reboot the machine
    - 2024-03-07 - Updated BIOS to version 1302 date 12/08/2023, was version 1106 date 02/10/2023
- Install OpenSSH
    
    ```bash
    sudo systemctl status ssh
    sudo apt -y install openssh-server
    sudo ufw allow ssh
    ```
    
- Make sure to logout of the machine

## Journal
- 2023-05-24 - When using Hephaestus need to install using the EVGA 1030 video card I had laying around. Seems when using other more complex hardware will have problems loading the Ubuntu installer.  
- 2024-05-11 - Have turned off power on 4 3090s, and 2 4090s. Left only the one 4090 at slot 7 on with PSU running and this will allow me to install Ubuntu without any problems.