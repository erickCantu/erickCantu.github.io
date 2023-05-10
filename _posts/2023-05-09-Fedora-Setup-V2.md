---
title: "Fedora 38 Setup - Part II - Workstation Version" 
categories: 
    - Fedora 38
    - Worksation Version
    - Work Station Setup
tags: 
    - Fedora 38
    - Work Station
    - Computer Setup
    - Root Expansion
    - Data Science Workstation Setup

last_modified_at: 2023-05-09T23:00:00-01:00
image: /assets/images/posts/fedora38_KDE/ecantu_Create_an_abstract_paint_that_illustrates_the_fusion_of__0af24d51-1ddd-4b05-99e1-fb2ef32ee269.png
---

WELL.. The KDE server version did not work well. The computer reboot when streaming while the CPU got temperatures around 61&deg;C. Installing NVIDIA drivers did not resolved the issue. Black screens came after booting.. A possiblity could be, missing the configuration in the boot setup to use the nvidia driver instead of the nouveau divers. Additionally there was mouse freezing, which could be fixed by using the solaar package. Bud did not had the oportunity to test it. I tried the KDE ISO version whit the same results than using the server version. 

So, I am trying GNOME.  After installing the Workstation ISO and seting up as in the previous post, the rebooting problem remains. It seems that is a recurring problem with the nouveau drivers ([ABRT Analytics - Report #617657 - xorg-x11-drv-nouveau in gf100_gr_reset](https://retrace.fedoraproject.org/faf/reports/617657/)). This means that NVIDIA drivers are required; atleast is what I pressume. While using Ubuntu and loading the proprietary NVIDIA drivers, the workstation woked without any issues. In this post I am documenting how to install them. 

*The post image was created with midjourney. Prompt: /imagine Create an abstract paint that illustrates the fusion of engineering and innovation with Data Science, navigating the crossroads of expertise to create sustainable and efficient solutions using oil as the medium, with the impasto technique, emphasizing depth and contrast, and featuring a stunning midnight blue color palette. --no Letters, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark, Human, Person, People. --aspect 7:4 --s 750 --v 5 --q 2*  

---

## Fix the Logitech drivers

Before starting with configuring with the video card drivers, I setup the logitech mouse. 

```bash
sudo dnf update
sudo dnf install solaar 
```

---

## Install NVIDIA Drivers

I followed the how to documentation in [Howto/NVIDIA - RPM Fusion](https://rpmfusion.org/Howto/NVIDIA?highlight=%28%5CbCategoryHowto%5Cb%29). The documentation provides all the required steps before and after the drivers configuration. Read the complete page before installing the drivers. 

### Configure RPM Fusion

```bash
sudo dnf update
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf groupupdate core
```

### Secure Boot

1. Install *akmods* package. 
   
   ```bash
   sudo dnf install akmods
   ```

2. Read the README file to review the proper steps to follow.
   
   ```bash
   nano /usr/share/doc/akmods/README.secureboot
   ```

3. Enroll process with Akmods
   
   ```bash
   sudo /usr/sbin/kmodgenca
   ```

4. Enter the certificate information
   
   ```bash
   -----
   You are about to be asked to enter information that will be incorporated
   into your certificate request.
   What you are about to enter is what is called a Distinguished Name or a DN.
   There are quite a few fields but you can leave some blank
   For some fields there will be a default value,
   If you enter '.', the field will be left blank.
   -----
   Organization Name (eg, company) [akmods local]: erickcantu
   Organizational Unit Name (eg, section) [akmods]:ecantu
   Email Address [akmods@localhost.localdomain]:erick@erickcantu
   Locality Name (eg, city) [None]:
   State or Province Name (full name) [None]:
   Country Name (2 letter code) [XX]:
   Common Name (eg, your name or your server's hostname) [akmods local signing CA]:
   ```

5. Enroll new keypair with certificate and enter its password. It will be asked when the computer reboots. 
   
   ```bash
   sudo mokutil --import /etc/pki/akmods/certs/public_key.der
   input password: 
   input password again: 
   ```

6. Rebooting the system is needed for MOK to enroll the new public key. BE SURE YOU HAVE A WIRED KEYBOARD!!!
   
   On next boot MOK Management is launched and you have to choose
   "Enroll MOK".
   
   Choose "Continue" to enroll the key or "View key 0" to show the keys
   already enrolled.
   
   Confirm enrollment by selecting "Yes".
   
   You will be invited to enter the password generated above.
   WARNING: keyboard is mapped to QWERTY!
   
   The new key is enrolled, and system ask you to reboot.
   
   You can confirm the enrollment of the new keypair once the system
   rebooted with:
   
   ```bash
   mokutil --list-enrolled | grep Issuer
   ```
   
   or with:
   
   ```bash
   sudo mokutil --test-key /etc/pki/akmods/certs/public_key.der
   ```
   
   which should return
   
   ```bash
   /etc/pki/akmods/certs/public_key.der is already enrolled
   ```

#### House keeping

I already have 10 enrolled keys, which I habe been creating in the last days. Lets remove the ones that are not needed. For details see: [uefi - Is it possible to delete an enrolled key using mokutil without the original .der file? - Ask Ubuntu](https://askubuntu.com/questions/805152/is-it-possible-to-delete-an-
enrolled-key-using-mokutil-without-the-original-der)

1. Create a mokkeys directory.
   
   ```bash
   mkdir mokkeys
   cd mokkeys
   ```

2. List the enrolled keys by exporting them to the mokkeys directory. I use zsh, therefore the *lsa* command. Use *ll* in bash. 
   
   ```bash
   mokutil --export
   lsa
   ```

3. Review the keys content. Be careful to select only the keys that are not needed. You do not want to re-install everything again.
   
   ```bash
   mokutil -l | less
   ```

4. Delete they selected keys by erasing the files name *MOK000x.der*. The command is going to ask you for a password that is needed after rebooting. Use the same password for each key. Idealy the same one that was used to enroll them.
   
   ```bash
   sudo mokutil --delete MOK000x.der
   ```

5. You need to reboot the system. You will come to the blue screen that is going to ask you if you want to dele the selected keys. You do this part in a bash. Not per individual key. Reboot the system. 

### Install NVIDA Drivers from rpmfusion

```bash
sudo dnf update -y
sudo dnf install akmod-nvidia
```

```bash
Installed:
  akmod-nvidia-3:530.41.03-1.fc38.x86_64                                                                  
  egl-gbm-1.1.0-4.fc38.x86_64                                                                             
  egl-wayland-1.1.11-3.fc38.x86_64                                                                        
  nvidia-settings-3:530.41.03-1.fc38.x86_64                                                               
  xorg-x11-drv-nvidia-3:530.41.03-1.fc38.x86_64                                                           
  xorg-x11-drv-nvidia-cuda-libs-3:530.41.03-1.fc38.x86_64                                                 
  xorg-x11-drv-nvidia-kmodsrc-3:530.41.03-1.fc38.x86_64                                                   
  xorg-x11-drv-nvidia-libs-3:530.41.03-1.fc38.x86_64                                                      
  xorg-x11-drv-nvidia-power-3:530.41.03-1.fc38.x86_64      
```

The documentation provides a suggestion to install cuda. But, I will try with [Howto/CUDA - RPM Fusion](https://rpmfusion.org/Howto/CUDA?highlight=%28%5CbCategoryHowto%5Cb%29) in the next post.

Reboot the computer. 

### IT BOOT TO A BLACK SCREEN

It happened again, the same mistake as with the KDE version. The boot was to a black screen. This but is well documented, and according to rpmfusion documentation, the solution is in place. But, for the 530.41.03 driver version is not. Therefore you need to run the commands that are part of the[KMS (Kernel Mode Setting")](https://rpmfusion.org/Howto/NVIDIA?highlight=%28%5CbCategoryHowto%5Cb%29#KMS). Now I wonder if I should go back to the minimalistic KDE version.

```bash
sudo grubby --update-kernel=ALL --args='nvidia-drm.modeset=1'
```

### Ensure the suspend command works

```bash
sudo dnf install xorg-x11-drv-nvidia-power
sudo systemctl enable nvidia-{suspend,resume,hibernate}
```

The package is already installed. I pressume the configuration is also available. Will see if after it suspends. 

### Video Acceleration

Video reproduction or streaming requires video acceleration. No need for ffmpeg drivers or media drivers. The following code is enough. 

```bash
sudo dnf install nvidia-vaapi-driver libva-utils vdpauinfo
```

### Nouveau verification

Review that Nouveau is not running the following code should produce nothing.

```bash
lsmod |grep nouveau
```



In the next post, I will review installing CUDA. 
