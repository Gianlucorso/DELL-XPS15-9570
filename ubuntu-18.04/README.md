# Ubuntu 18.04 on DELL XPS 15 (9570)

INSTALL UBUNTU 18.04 ON DELL XPS 15 9570

My model is the 4k touchscreen one.

I got the starting instructions from
< https://github.com/rcasero/doc/wiki/Ubuntu-linux-on-Dell-XPS-15-(9560) >
which was found on
< https://www.reddit.com/r/Dell/comments/8f9sme/ubuntu_1804_on_xps_9560/ >]

These steps are taken from
< https://medium.com/@peterpang_84917/personal-experience-of-installing-ubuntu-18-04-lts-on-xps-15-9570-3e53b6cfeefe >

## 1. Preparation steps on Windows

These steps are needed in case something goes wrong (may happen) and you need to
restore your PC at factory status.

- Boot on Windows and check that the latest version of SupportAssist is installed
  (you may need to register your product at DELL. I totally suggest to do that)
  Downloadable at < https://www.dell.com/support/contents/us/en/19/article/product-support/self-support-knowledgebase/software-and-downloads/supportassist >
  
- Search in the search-bar "My Dell" and launch it. 
  Once opened, click on Support (square on bottom right side of the screen) and
  run all scanning services.
  
- Update all drivers (in particular BIOS).

- Check if there are available updates for NVIDIA graphic card.
  You can check this also on their official website.

- Create a Windows recovery USB stick so that you can reset the laptop to factory 
  settings if things go wrong. 
  You can find a guide in the following link.
  Enter your registering number of your device (You can find such number in 
  "My Dell" application.
  
  < https://www.dell.com/support/home/it/it/itbsdt1/Drivers/OSISO/WT64A >
  
  So follow the procedure to create it (at least a 16GB pendrive is required).


[ Source: https://medium.com/@peterpang_84917/personal-experience-of-installing-ubuntu-18-04-lts-on-xps-15-9570-3e53b6cfeefe ] 

## 2. Enable AHCI mode

In order to install Ubuntu, you need to set the storage drive to AHCI mode.

- Run Command Prompt as an admin.
- Run: bcdedit /set {current} safeboot minimal .
- Reboot.
- Press F2 when you see the Dell logo.
- Select AHCI mode in the SATA option under System Configuration.
- Press “Apply” then “Exit”.
- Login as usual.
- Open the Command Prompt as an admin again and type: bcdedit /deletevalue {current} safeboot .
- Reboot.

## 3. Partition storage drive

Open the start menu.

- Type disk management and open Disk Management.
- Select the Windows partition (most likely to be the largest one).
- Right click on it and select “Shrink Volume”.
- Shrink to desired amount. (I shrank 200GB for Ubuntu)
- See if a partition of “Unallocated space” is shown.

## 4. Install Ubuntu

### 4.1

We are now ready for the installation of Ubuntu.

- Insert the Ubuntu USB into the computer.
- Reboot.
- Press F12 when you see the Dell logo.
- Select the one with the words “Boot from UEFI” in it.
[ You have to BOOT from the pendrive ]
- Hover over the option “Try Ubuntu without installing”.

**TIP:** "Hover" means just select with cursor an option in the list and do nothing 
     else.
     
- Press e.
- Add nomodeset after the words quiet splash. Detailed instructions can be found in here.

In my case it was "[..somestuff..] quiet splash ---" and I changed it in 
"[..somestuff..] quiet splash nomodeset ---"

- Press F10.

### 4.2 Live USB Ubuntu

- Launch the Ubuntu installer on the desktop.
- Select “Enable Insecure Boot mode” during the installation and remember the password for it.

  a. Enable: 
      - install updates during installation
      - install third-parties softwares for graphic and wifi
      - turn off secure boot and insert a password
      
  b. Select “Something else”  and click
     “continue".
  c. Select free space (~ 200 GB, if you followed precisely the steps, otherwise 
     it should be almost equal to the shrinked amount of space you have decided)
  d. Click on "+" button
  e. Leave the default size and select as "Mount point" option "/" and then 
     click "Ok" button.
  f. Select the new ext4 partition that before was called "free space" and click 
     on "Install Now" button.
  g. A window should appear asking for swap partition, click on "continue" button.
  h. Another window should appear asking for writing changes to disk, click on 
     "continue" button.
  i. Select the place in which you are click on "continue" button.
  m. Select the layout of your keyboard (you can use also autodetect tool).
  n. Write your name, choose username and password, but DO NOT enable option 
     "Encrypt my home folder" (I personally experienced troubles when installed 
     Ubuntu with that option enabled, not on Dell Xps 15 9570, but on an old asus 
     K55vm, so this means that on Dell xps 15 9570 it may work, but I did not try).
  o. Click on "continue" button.
  p. Installation process should start.
  q. When completed a window should appear asking for restarting the system,
     click on "Restart Now" button
  r. A message should appear to remove the USB stick and press Enter.
     If the computer blocks at this point just force the shutdown by holding the
     power button until the monitor shut down. If so, turn on again the PC.

## 5. After-installation procedure

### 5.1 BIOS 

Now the Ubuntu is installed. There are still things to do. 
After the installation and reboot, you will be greeted by a blue screen 
“Perform MOK management”.

- Select “Change Secure Boot State”
- Enter your the n-th word in your passwords as it specified.
- Select “Yes” for “Disable Secure Boot”.
 
Thus it is telling you to wait until blue screen with message "Perform MOK 
management", but it does not specify you that you have some time to do press any 
key. If you, like me, hesitate you should see the windows disappear and the 
Ubuntu launch menu appear. In this case DO not panic, select from that menu 
"system setup". The computer should reboot and BIOS menu should be opened. Here 
go in Secure Boot and then Secure Boot Enable. There uncheck "Secure Boot Enable" 
option. A warning message should appear, just click on "Yes" button. Then click 
on "Apply" button and in the next windows that appears, check "Save as Custom 
User Settings" and then press "Ok" button.
Now just click on "Exit" button and the PC should reboot. 

### 5.2 Ubuntu launch menù

After that, the computer will reboot and you will be greeted by a screen with booting options.

- Hover over the option “Ubuntu”
- Press e.
- Add nouveau.modeset=0 after the words quiet splash. Detailed instructions can be found here, except the phase is changed from nomodeset to nouveau.modeset=0.

  In my case I add them between "quiet splash" and "vt_handoff", keeping a white 
  space between them.
  If you are italian like me and you are struggling to find [=] character, since
  the keyboard in that windows is setted in us, for an italian keyboard [=] is 
  in the key [ì] (the one after on the right key [']). Just press it and you will
  be fine.

- Press F10.

All the troublesome boot-options edits allow the computer to boot into Ubuntu or Ubuntu bootable USB.
If you want to boot into Ubuntu, you can add either nomodeset or nouveau.modeset=0 in the boot option. However you cannot adjust the screen brightness if you use the former one. And remember, only nomodeset works for installing Ubuntu. Using nouveau.modeset=0 for the installation boot will fail.
[This is may be ignored because when I decided to reinstall Ubuntu, passing from 
 16 to 18 thorugh a new clean&fresh installation, more true, because I wrongly 
 forgot to do that and the bightness could be changed using fn keys. Anyway after
 noticing that I add those lines at the launch menù of Ubuntu. So I invite you
 to do that.]

### 5.3 it's "grub" time!

Now the computer will boot into Ubuntu. There is still one step for Ubuntu to boot smoothly every time.

- Open the terminal.
- Type `$ sudo gedit /etc/default/grub` .
- Change the line GRUB_CMDLINE_LINUX_DEFAULT="quiet splash" to GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nouveau.modeset=0" .
- Press “Save” and close the window.
- In the terminal, type `$ sudo update-grub2` .
- (OPTIONAL) Install updates that the system suggested before rebooting. 
- Reboot.
- Select Ubuntu.

### 5.4 Status

+------------------------------------------------------------------------------+
|              |        Status         |                                       |
|     Item     |-----------------------|                 Notes                 |
|              | Working | NOT Working |                                       |
+------------------------------------------------------------------------------+
| Wifi         |    X    |             |                                       |
+------------------------------------------------------------------------------+
| Bluetooth    |    X    |             | not visible on my Redmi Note 3 pro,   |
|              |         |             | I could connect my phone from PC side.|
+------------------------------------------------------------------------------+
| Touch-screen |    X    |             | Works perfectly, very smooth and when |
|              |         |             | you open a window in which you can    |
|              |         |             | write, a screen keyboard appears.     |
+------------------------------------------------------------------------------+
| Speakers     |    X    |             |                                       |
+------------------------------------------------------------------------------+
| Webcam       |    X    |             | Tested on Skype.                      |
+------------------------------------------------------------------------------+
| Headset      |    X    |             | Tested on Skype (audio + mic).        |
+------------------------------------------------------------------------------+
| Suspend mode |    X    |             | Working, but when pc is in suspend    |
|              |         |             | mode the fans do not turn off.        |
|              |         |             | **Update: now it works.**             |
+------------------------------------------------------------------------------|


### 5.4 Fixing and improvements

Here I reported the command to check your kernel version:

`$ uname -a`

and I reported my result using that command in terminal:
 
> Linux [somestuff] 4.18.0-24-generic #25~18.04.1-Ubuntu [somestuff] x86_64 x86_64 x86_64 GNU/Linux

#### 5.4.1 Tweaks_xps script**

- Start by cloning the following repository I cloned it in Downloads

`$ git clone https://github.com/JackHack96/dell-xps-9570-ubuntu-respin.git`

- Then

```
$ cd /[...path_to_cloned_repo]/dell-xps-9570-ubuntu-respin

$ sudo ./xps-tweaks.sh
```

+-------------------
| **TIPS:**
|
| - When it asks you about proceeding or not in installing something (yes/no questions)
|   type "1" for yes, 2 for "no".
|
| - When a License agreement appears use keys to read it and to move the cursor on <ok>
|   then press Enter 
|
| - When running that script I accepted everything except for Meltdown/Spectre path
|   disabling part
-------------------  

- Reboot now


- when I tried to type

```
$ sudo prime-select nvidia
$ sudo nvidia-smi
```

It said at first "impossible to communicate [somestuff]" and then "no devices 
were found".

**Update**: solution at ### 5.4.4

#### 5.4.2 Touchpad & Enable Touchpad Right Click**

I took these steps from:

https://github.com/rcasero/doc/wiki/Ubuntu-linux-on-Dell-XPS-15-(9560)

```
$ sudo apt install xserver-xorg-core

$ sudo apt-get install xserver-xorg-input-libinput

$ sudo apt-get remove --purge xserver-xorg-input-synaptics

$ sudo reboot now
```

The following command is taken from:

https://gloveboxes.github.io/Ubuntu-for-Azure-Developers/docs/dellxps15.html

`$  gsettings set org.gnome.desktop.peripherals.touchpad click-method areas`

Now the touchpad right click button should work.

#### 5.4.3 Windows/linux Dual Boot Time**

I took this command from:

https://gloveboxes.github.io/Ubuntu-for-Azure-Developers/docs/dellxps15.html

`$ timedatectl set-local-rtc 1 --adjust-system-clock`

#### 5.4.4 Fix NVIDIA driver installation**

After having run the Tweaks_xps script, NVIDIA drivers may not work.

I tried different method but they did not work. I gave up until once I searched 
and tried again.

The following method worked!!

[ Source : https://www.mvps.net/docs/install-nvidia-drivers-ubuntu-18-04-lts-bionic-beaver-linux/ ]

"Before we start installing the correct driver, we need to clean the system of 
any previously installed driver that might create software issues.
You can do that by using the following command:"

`$ sudo apt-get purge nvidia*`

"Add the graphic-driver PPA using the following command:"

`$ sudo add-apt-repository ppa:graphics-drivers`

"To retrieve information about the latest version of the packages listed in the repository we run:"

`$ sudo apt-get update`

Then visit the following link to check which package version is compatible with
your system.

What I did was looking for the exact version of Ubuntu. In order to do this type 
in a terminal this command:

`$ uname -a`

In my case the output was **18.04.1**
Linux <myusername>-XPS-15-9570 5.0.0-31-generic #33~18.04.1-Ubuntu SMP <day> <month> 1 <hours>:<minutes>:<seconds> <timezone> <year> x86_64 x86_64 x86_64 GNU/Linux

> I used <something> to replace useless info, that you are out of scope from
this tutorial. 


Then I visited this link:

<https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa>

and I pressed CTRL + F to search for "18.04.1" and to check which package version
of NVIDIA drivers was compatible with that version of Ubuntu.
In my case the latest package version that was compatible was "nvidia-graphics-drivers-430".

Therefore I installed it through this command:

`$ sudo apt-get install nvidia-driver-430`

Then reboot your pc.

`$ sudo reboot now`

Once rebooted, check if evrything went fine with this command:

`$ nvidia-smi`

It should return something like this:

Sun Oct 13 10:32:28 2019 
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 430.50       Driver Version: 430.50       CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 105...  Off  | 00000000:01:00.0 Off |                  N/A |
| N/A   41C    P3    N/A /  N/A |    855MiB /  4042MiB |      3%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1905      G   /usr/lib/xorg/Xorg                           467MiB |
|    0      2395      G   /usr/bin/gnome-shell                         383MiB |
|    0      3380      G   /usr/lib/firefox/firefox                       3MiB |
+-----------------------------------------------------------------------------+

Then I suggested to select "intel-profile" to increase battery life when you
are not intending to use NVIDIA graphic card. Thus:

`$ sudo prime-select intel`

or, use ubuntu search menu. Search for "nvidia xserver", open that application.
If the installation went fine you should see many options in the list menu on 
the left. The last one should be "PRIME Profiles". Click on it and on the right
you should be able to select which profile you prefer.
Select "Intel" when you are not intending to use your NVIDIA graphic card (this 
will increase the battery life), otherwise "NVIDIA" profile.

## 9. If you want to erase Ubuntu and reinstall it or install another version of it

**Assumptions:** no changes in BIOS (still AHCI option enabled), still the same Ubuntu 
partition you did at that time you installed Ubuntu.

If you are in that situation then skip steps below and jump to next subsection,
otherwise do these preliminary steps before reinstalling Ubuntu.

- If you do not have anymore the recovery pendrive prepared in step 1, then 
  do that procedure again.

- Then if you changed anything in the BIOS (AHCI), then redo steps at point 2

- If you do not have anymore partition with Ubuntu **ignore next subsection** and 
  redo all points starting from point 3.

### 9.1 Reinstalling Ubuntu

- Insert the Ubuntu USB into the computer.
- Reboot.
- Press F12 when you see the Dell logo.
- Select the one with the words “Boot from UEFI” in it.
[ You have to BOOT from the pendrive ]
- Hover over the option “Try Ubuntu without installing”.

**TIP:** 
"Hover" means just select with cursor an option in the list and do nothing else.
     
- Press e.
- Add nomodeset after the words quiet splash. Detailed instructions can be found in here.

In my case it was "[..somestuff..] quiet splash ---" and I changed it in 
"[..somestuff..] quiet splash nomodeset ---"

- Press F10.
- Launch the Ubuntu installer on the desktop.

NB: usually at this point here you should (I am citing section 4.2)

Select “Enable Insecure Boot mode” during the installation and remember the password for it.

but this time I did not notice this option, so I continued the installation ignoring
this. After the steps reported here, usually you should go into the bios and disable 
secure boot (I am citing section 5.1). 
Since I did not turned on it, I ignored those steps.
I checked on the bios after installing Ubuntu and "Secure boot enable" option 
was unchecked.

- In installation procedure you have to:
  a. enable: 
      - install updates during installation
      - install third-parties softwares for graphic and wifi
      
  b. select "Erase Ubuntu XX.YY.Z and reinstall option
  c. click "continue" button.
  d. a warning window will appear asking you to confirm changes to the partition
     (since I installed Ubuntu on partition #7 on my device labelled as /dev/nvme0n1
      I can be sure that only the partition with Ubuntu will be erased and not the one
      on which Windows is installed).
  e. If everything seems to be ok click on "continue" button
  f. proceed in the installation steps
  g. pick username and password then click on "continue" button
  h. installation procedure will be completed
  q. When completed a window should appear asking for restarting the system,
     click on "Restart Now" button
  r. A message should appear to remove the USB stick and press Enter.
     Remove the pendrive and wait some seconds, then click Enter.
     If the computer blocks at this point just force the shutdown by holding the
     power button until the monitor shut down. If so, turn on again the PC.
     
- At this point you can go back at section 5.2 and redo all steps for setting up
  Ubuntu after installing it.


## How to run Windows?                                                          

Simply select option "Windows Boot Manager (on / ...somestuff)" and press Enter.
Windows boot should be launched. 
A blue screen may appear asking for entering the Recovery Key in order to 
disable BitLocker for the current drive. Just simply the instrunctions shown
(something like connect to your microsoft account associated to the Microsoft
account used to set up your Dell XPS 15, following the link provided and copy
the key reported in the box).



## Other useful resources

https://github.com/rcasero/doc/wiki/Ubuntu-linux-on-Dell-XPS-15-(9560)#installation-steps

https://gist.github.com/tomwwright/f88e2ddb344cf99f299935e1312da880

