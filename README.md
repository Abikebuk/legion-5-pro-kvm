# LEGION 5 PRO - KVM w/ Single GPU Passtrough

# Disclaimer
This guide is aimed toward people that have experience with Linux. I won't advice you to follow this guide if you are not comfortable with Linux, especially for the KVM part. 


# My configuration
### **LEGION 5 Pro**
* **``CPU``** : Ryzen 7 5800H
* **``GPU``** : Nvidia RTX 3070
* **``RAM``** : 2 x Samsung 8GB (reference tbd)
* **``Disks``** : 
  * SK Hynix 512GB
  * Samsung 970 Evo 2TB

# Operating System
> I won't try any other distros.  
 
My choice is on **EndeavourOS**, an Arch-based distribution.  
However, I think any other Arch-based distro would work the same.

### Why Arch-based distribution?

* I'm really comfortable with Arch.
* I hate using any Debian-based distributions, package manager is a pain to use compared to Arch (no /etc/apt/source file to manipulate).
* I love OpenSUSE but had really poor success on it.
* I was also interested in Fedora but did not have time to try it.
* More importantly, from my experience, Arch being a *rolling-release* (that always has the latests stables updates) system, any piece of hardware that contain any piece that has been released recently always had better native compatibility on Arch.

# Installation of EndeavourOS

> Those steps are specific to EndeavourOS but might be similar for other distributions.
1. Get a USB Key with EndeavourOS.
2. Choose `Non Free` Drivers from the grub screen, thus you can get Nvidia drivers on the 
3. Install EndeavourOS  
   > **WARNING :** If you have the infamous Mediatek network card (the one that is shipped on every Legion 5 Pro) **DO NOT** choose ``LTS``  
   
   EndeavourOS let you choose additional packages such as the desktop environment. Take any you like. 

# Installation for any Arch-based distributions

1. Install ``yay`` (already installed on EndeavourOS)
2. Install Wifi drivers (if you wifi don't work for you)
   ```bash
   sudo pacman -S rtw89-dkms-git
   ```
3. Install Nvidia drivers / hybrid mode 
   ```bash
   sudo pacman -S nvidia-prime optimus-manager optimus-manager-qt-git
   sudo systemctl enable optimus-manager.service
   ```
   * ``nvidia-prime`` : Optimus driver
   * ``optimus-manager`` : permits the switch from hybrid, dedicated GPU only and integrated GPU only 
   * ``optimus-manager-qt-git`` : GUI of optimus-manager. Once launched can be found on the notification bar. Just right click on it, and you can switch on any modes you want without commands-line
4. reboot

# KVM 
```bash
sudo pacman -S libvirt virt-manager qemu edk2-ovmf dmidecode dnsmasq ebtables
sudo systemctl enable --now libvirtd.service
sudo usermod -aG <your_username> libvirt
sudo virsh net-autostart default
sudo virsh net
```

* open ``virt-manager``
* Click *File* > *Add Connection...*
* You should see ``Generated URI: QEMU:///system`` on the bottom of the popup.
* Click *Connect*
* Create a new virtual machine on Qemu/KVM ( *File* > *New Virtual Machine* or the first button on the toolbar)
* Choose ``Local install media``
* Browse the ISO of your choice by either add the directory of your ISOs files or use *Browse Local*
* **TODO**


