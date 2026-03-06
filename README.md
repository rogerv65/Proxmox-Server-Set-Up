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
### Setting 1: Preventing Proxmox from going into Sleep Mode
1) Log into Proxmox from the host machine (my laptop) and enter the following command:

    `nano /etc/systemd/logind.conf`
   
2) Next, remove the comments and set the following values to ignore:
   
    `HandleLidSwitch=suspend` -> `HandleLidSwitch=ignore`
   
    `….ExternealPower=suspend` -> `….ExternealPower=ignore`
   
    `….Docked=ignore`
   
4) Next, remove the comments for the following:

    `IdleAction=ignore`

    `IdleActionSec=30min`
   
5) Change the value of `IdleActionSec` to **0**
6) Save these changes, and reset the system with the following command:

    `systemctl restart systemd-logind`
   
7) With all these settings, the laptop can now be closed!

## Setting 2: Turning off the Backlight
1) Enter the following command:

    `nano /etc/default/grub`

2) Locate the following:

`GRUB_CMDLINE_LINUX_DEFAULT=”quiet”`

4) Within the quotation, but after `quiet` write the following:

    `“... consoleblank=30”`

5) Save the changes and upgrade grub with the following:

    `Update-group`

6) Then reboot the server:

    `Reboot`
   
7) With all this, my laptop can now mimic a server and I don’t need to access unless required.

### Setting 3: Update Proxmox
1) Since I’ll only be using Proxmox for non-production use, navigate to the desired node, then click:

    *updates>repositories.*
   
2) From here disable all the enterprise repo’s, and add both PVE and Ceph no subscription repo’s. Move back to updates and click *refresh*, then *upgrade*.
3) Now we get updates without needing to pay for a subscription.



