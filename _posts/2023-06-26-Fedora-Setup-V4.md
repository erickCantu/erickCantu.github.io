---
title: "Fedora 38 Setup - Part IV - WSL" 
categories: 
    - Fedora 38
    - WSL Version
tags: 
    - Fedora 38
    - Work Station
    - Computer Setup
    - WSL
    - Windows
    - Data Science Workstation Setup

last_modified_at: 2023-06-16T23:00:00-01:00
image: /assets/images/posts/latex/ecantu_Create_a_captivating_website_top_banner_utilizing_the_en_a9ca0251-5ec3-43f6-8b95-7bf41c9874ad.png
---

From time to time, I need to use a windows laptop to run a native program there.  Nowadays, Windows allows us to have Linux kernel running as a subsystem. There are plently of examples on how to install Ubuntu as its available in the Windows Store. However as discussed previously I like much better Fedora.  

In this post I document how to setup Fedora 38 in WSL. The setup is based on information from [Install WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install) and from [Install Fedora 37 or earlier on Windows Subsystem for Linux (WSL) - DEV Community](https://dev.to/bowmanjd/install-fedora-on-windows-subsystem-for-linux-wsl-4b26).

# Fedora 3x as Windows subsystem (WSL2)

### Installing Fedora 38 Container Based Build

1. Ensure that Virtual Maschine is enabled in the BIOS and in Windows. 
   
   For the first step follow the computer manufacturer. Then follow the steps in [Install WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install).

2. Ensure WSL2 is running in Windows:
   
   ```bash
   wsl --set-default-version 2
   ```
   
   If errors arise, consult google or youtube to find how to setup WSL 2 in windows. Just search for *How to setup WSL2*. As an alternative you can read [Install WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install).

3. Download the latestest Fedora Container Base build from [Koji Fedora](https://koji.fedoraproject.org/koji/packageinfo?packageID=26387) eg. [Fedora-Container-Base-38-20230619.0 | Build Info | koji](https://koji.fedoraproject.org/koji/buildinfo?buildID=2217818). Be sure that the State has a green check mark and not a yellow *X* or red *-*. As this mean that the build was either canlleded or failed.  Download the [Fedora-Container-Base-38-20230619.0.x86_64.tar.xz](https://kojipkgs.fedoraproject.org//packages/Fedora-Container-Base/38/20230619.0/images/Fedora-Container-Base-38-20230619.0.x86_64.tar.xz) file and extract it, eg. WinRar. The content from the folder with the HEX name should containt the layer.tar file.  This is the required file to install Fedora.

4. Create a folder where Fedora will be installed. eg: C:\Users\User\AppData\Local\WSL2\Fedora38

5. Import the Fedora distribution into WSL. In this example, I am naming it Fedora38
   
   ```bash
   wsl --import Fedora38 C:\Users\User\AppData\Local\WSL2 C:\Users\User\Downloads\layer.tar
   ```

6. Now review the installed distros:
   
   ```bash
   wsl -l -v
     NAME        STATE           VERSION
   * Ubuntu      Stopped         2
     Fedora38    Stopped         2
   ```
   
   In this case Ubuntu is also installed. the *-v* parameter checks for the version. Ensure it is 2. Remembered that it was setup like that in Step number 2. 

7. Setup the Fedora38 as the default distribution:
   
   ```bash
   wsl -s Fedora38
   ```

8. To lunch it now  just type
   
   ```bash
   wsl
   ```

9. If you want to run other installed distro, eg. Ubuntu run:
   
   ```bash
   wsl -d Ubuntu
   ```
   
   Review the list of installed distros to find the correct name, see point 6.

10. In widnows I use [Oh My Posh]([GitHub - erickCantu/PowerShell_OhMP: A Template for Oh My Posh for Windows Powershell](https://github.com/erickCantu/PowerShell_OhMP)) with [Windows Terminal](https://www.microsoft.com/store/productId/9N0DX20HK701), there you can open a Terminal with Fedora, Powershell, Ubuntu, etc. 

11. If you want to find which other distros can be installed from terminal run:
    
    ```bash
    wsl --list --online
    ```

12. 

### Aferter install setup

There are additional steps to completelly setup Fedora in wsl.  These are not required from distros on the online list.

1. When running Fedora the first time, it will run as root. Be carefull on what you do.  

2. Update the distro
   
   ```bash
   dnf update
   ```
   
   If you cannot update the distro, there are issues resolving the DNS. See the *Ensure DNS is functioning* in the post [Install Fedora 37 or earlier on Windows Subsystem for Linux (WSL) - DEV Community](https://dev.to/bowmanjd/install-fedora-on-windows-subsystem-for-linux-wsl-4b26)

3. Install basic system utilities
   
   ```bash
   dnf install util-linux
   ```
   
   Exit the distro
   
   ```bash
   exit
   ```
   
   and therminate it in PowerShell:
   
   ```bash
   wsl -t Fedora38
   ```
   
   restart Fedora38

4. It is not recomended to run root as default. Create a user with sudo previledges. 
   
   ```bash
   dnf install passwd
   useradd -G wheel newuser
   passwd newuser
   ```
   
   Exit and reboot Fedora distro as in step 3.

5. Lunch Fedora38 with the *newuser* 
   
   ```bash
   wsl -u newuser
   ```

6. If the seupt worked properly you should now see:
   
   ```bash
   [newuser@computername WindowsUser]$
   ```
   
   instead of 
   
   ```bash
   [root@computername WindowsUser]$
   ```
   
   check for the sudo previledges:
   
   ```bash
   sudo cat /etc/shadow
   ```
   
   You should get the information regarding the users, it should include the *newuser* information.

7. Setup the user as default login. 
   
   ```bash
   printf "\n[user]\ndefault = newuser\n" | sudo tee -a /etc/wsl.conf
   ```
   
   This code adds the new user to the *wsl.conf* file

8. Restart Fedora38 as in step 3. And you are done.

### Additional steps.

The Fedora Container Base build has just the basic information lets install neofetch to find the current information

```bash
sudo dnf install neofetch
neofetch


             .',;::::;,'.                newuser@WINDOWS-COMPUTER-NAME
        .';:cccccccccccc:;,.            ---------------------
      .;cccccccccccccccccccccc;.         OS: Fedora Linux 38 (Container     
    .:cccccccccccccccccccccccccc:.       Kernel: 5.15.90.1-microsoft-st   
  .;ccccccccccccc;.:dddl:.;ccccccc;.     Uptime: 8 mins
 .:ccccccccccccc;OWMKOOXMWd;ccccccc:.    Packages: 417 (rpm)
.:ccccccccccccc;KMMc;cc;xMMc:ccccccc:.   Shell: bash 5.2.15
,cccccccccccccc;MMM.;cc;;WW::cccccccc,   Terminal: Windows Terminal
:cccccccccccccc;MMM.;cccccccccccccccc:   CPU: Intel i7-5500U (4) @ 2.39
:ccccccc;oxOOOo;MMM0OOk.;cccccccccccc:   Memory: 302MiB / 3868MiB
cccccc:0MMKxdd:;MMMkddc.;cccccccccccc;
ccccc:XM0';cccc;MMM.;cccccccccccccccc'
ccccc;MMo;ccccc;MMW.;ccccccccccccccc;
ccccc;0MNc.ccc.xMMd:ccccccccccccccc;
cccccc;dNMWXXXWM0::cccccccccccccc:,
cccccccc;.:odl:.;cccccccccccccc:,.
:cccccccccccccccccccccccccccc:'.
.:cccccccccccccccccccccc:;,..
  '::cccccccccccccc::;,.
```

There a re only 417 installed packages. 

Install fedora documentation. 

```bash
grep -v nodocs /etc/dnf/dnf.conf | sudo tee /etc/dnf/dnf.conf
sudo dnf install -y man man-pages
```

These ensure that the manual pages are installed. It requires to reinstall all packages. 

```bash
for pkg in $(dnf repoquery --installed --qf "%{name}"); do sudo dnf reinstall -qy $pkg; done
```

Clean the installation

```bash
sudo dnf clean all
```

### ZSH

Follow the steps in [Fedora 38 Setup - KDE - Server Version | An Intersection of Engineering, Agriculture, Data Science and Innovation](https://www.erickcantu.com/fedora%2038/kde/work%20station%20setup/2023/05/04/Fedora-Setup.html) to setup ZSH

The following packages and steps are required. 

```bash
dnf install util-linux-user
chsh -s $(which zsh)
```
