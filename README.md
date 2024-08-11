# Void Linux - How to install on Lenovo Legion 5 with AMD CPU and with Nvidia GPU

## Description of the problem

I have a lenovo Legion 5 with AMD Ryzen CPU with Nvidia RTX 3000 Series and when I tried to install Void Linux it give me an ACPI bug and then ERROR, then the installation of the live Kernel, that allows the user to install Void Linux by execute the cmd line to install Void Linux.

Thank you very much, to the the IRC members of Void Linux, they told me that there is a work around to this problem, and here I will write the steps of my installation.


## Steps

0. IMPORTANT NOTE: Do this steps at your own risk, I'm just reporting what worked for me, and not implying in any way or form that it will work for anybody else. I am not responsible in any way or form if you do the following steps and they don't work for your system, or if they cause you any kind of damage or malfunction on your system. I only write this for me to save the steps here, in this repository. For a future installation that I may need to make, in case I need to format my current Void Linux installation and reinstall it again. <br>

In my case I don't care about Windows so I removed it completely from my disk and this instructions will erase it from the disk by formatting all the disk.

1. Download the image for glibc with xfce from Void Linux site.

2. Save it to a pen with the free app for Windows or Linux, BalenaEtcher.
   [https://etcher.balena.io/](https://etcher.balena.io/)

3. Bios Change - When starting press F2 and the BIOS menu will come one, on the BIOS security folder, disable the Secure BOOT, I had to make this in order to install Linux on this computer.
I also have set in the BIOS the NVIDIA GPU to be always ON and not in a hybrid mode with the Intel GPU.

4. Save and Exit BIOS.

5. ShutDown the computer.

6. Insert the pen on USB Port of the right of the computer.

7. Turn On the computer and hit F12, it will appear a boot menu and there will be the name of the pen that you inserted and that has the Void Linux Image.

8. Select it.

9. When the boot menu appears press "e" key to change the pens Linux kernel boot parameters in GRUB. 

10. Then go to the linux line and at the end of it just before the 

```
\
```

add the following with a space before and a space after

```
nomodeset
```

then press ```F10 ( or alt + F12 )``` and start the booting process now it will not stop at the ACPI ERROR because it is a NVIDIA GPU card and it doesn't have the nvidia drivers that you have to install after installing the void-repo-nonfree  .

11. If you your keyboard is not "en", do the following in the terminal for example for portuguese keyboards, and alter for your language.

``` bash
setxkbmap pt
```

12. Then start the installation with
```
# anon or root user

sudo void-installer
```

13. For my partitions I have chosen cfdisk disk util and made the following partitions:

```

Size   Type               Optional   Mount Point
1G   FAT32 / LINUX_86_64  bootable  /boot/efi
8G   Linux Swap
478G (rest)  Linux ext 4            /

```

14. Then reboot the machine and remove the pen and do the procedure again of adding the parameter nomodeset to the Linux Kernel.

15. When the boot menu appears press "e" key to change the pens boot parameters in GRUB. 

16. Then go to the Linux line and at the end of it just before the 

```
\
```

add the following with a space before and a space after

```
nomodeset
```

then press ```F10 or alt + F10``` and start the booting process without stooping at the ACPI ERROR because it is a NVIDIA graphical card and it doesn't have the nvidia drivers that you have to install after installing the void-repo-nonfree  .


17. If you your keyboard is not "en", do the following in the terminal for example for portuguese keyboards, and alter for your language, in my case is pt_latin1.

``` bash
setxkbmap pt
```

18. Update and Upgrade your system after installation from from the repos.

``` bash
sudo xbps-install -Su
```

19. Install the void-non-free package in Void Linux with the following command in the terminal.

``` bash
sudo xbps-install -S void-repo-nonfree
sudo xbps-install -S
sudo xbps-install nvidia
```

20. Now Reboot and you don't have to add on more time the kernel parameter do the GRUB boot program.

21. Then set the X Keyboard Layout correctly to pt in the case of a portuguese keyboard Layout by creating the following file for your keymap and rebooting again.

``` bash
# X11 keyboard layout

# This will install the micro text editor that is much better then nano text editor :-)

sudo xbps-install micro

sudo micro /etc/X11/xorg.conf.d/10-keyboard.conf
```

```
Section "InputClass"
  Identifier      "libinput keyboard catchall"
  MatchIsKeyboard "on"
  MatchDevicePath "/dev/input/event*"
  Driver          "libinput"
  Option          "XkbLayout" "pt"
EndSection
```

```
# Do ctrl + s
# Do ctrl + q
```

22. And the rest is the normal configuration of any Void Linux.


## Have fun!
Best regards, <br>
João Carvalho
