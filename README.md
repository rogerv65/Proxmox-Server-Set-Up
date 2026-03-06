# Proxmox-Server-Set-Up
## Introduction
I had an old laptop lying around that was going to get tossed, but made the decision to repurpose it. Now the laptop is the home of my **Proxmox VE server**. Essentially, I've upgraded my resource capacity, which has enablee me to create much bigger/complex labs without the worry of lacking resources or destroying my main laptop. The following are the steps I took to set-up and configure Proxmox VE on my old laptop. My goal is to inform and (hopefully) guide anyone who may be interested in what I have made.

## Installing Proxmox VE
### Prerequisites Before Installation
1) Since my laptop does not come with a built-in ethernet port, an ethernet adapter was purchased (research concluded that Proxmox VE is best utilized with a wired connection, especially after I encountered a problem when I attempted to set it up wirelessly).
2) Purchase a USB stick, and convert it into a bootable drive with Proxmox VE burnt into it (I used **Rufus** for this).
3) Lastly, I went into my old laptop’s BIOS setting and changed the boot order so that it boots from the bootable USB drive.
### Installation Process
1) With these prereuisites met, I powered on my laptop with the bootable USB stick plugged in.

    While going through the installation process, it is crucial that in **Management Inferface, wired connection** is selected.

2) After going through the process, Proxmox VE will begin download. Once complete the laptop will restart (ensure to unplug the USB stick as soon as it restarts or else it attempt to install Proxmox again).
3) Proxmox can now be accessed either from the host laptop, or via WebGUI (to do so, the IP address of my laptop needs to be searched).

## Configuring Proxmox
One downside is that Proxmox requires that the laptop remains open, and the screen does not turn off. Luckily we can circumvent these issues by modifying certain settings.
### Settings 1: Preventing Proxmox from going into Sleep Mode
1) Log into Proxmox from the host machine (my laptop) and enter the following command 
