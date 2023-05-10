---
title: "Fedora 38 Setup - KDE - Server Version" 
categories: 
    - Fedora 38
    - KDE
    - Work Station Setup
tags: 
    - Fedora 38
    - Work Station
    - Computer Setup
    - Root Expansion
    - Data Science Workstation Setup

last_modified_at: 2023-05-05T23:00:00-01:00
image: /assets/images/posts/fedora38_KDE/ecantu_Create_an_abstract_paint_that_illustrates_the_fusion_of__8c2afd06-0892-4da2-9ad3-4aa9e5a236d2.png
---

I have run Ubuntu on and off through the years,  almost since the beginning around 17 years ago. Back then it was great. It helped me to get into the Linux world. Noadays, it seems just bootloaded.  Specially the eternity that takes to update the libraries. And, I do not like todays gnome in a Workstation. To me it is great in a laptop where a track pad is available. But not for a dedicated mouse.  I know I could use a diferent flavor, but how old the libraries are in it, is a no in today's world. 

For some time I tried with Linux Mint and popOS in a laptop.  It was fine, still gnome in a laptop. But, since the beginning of the year I have been using Fedora 37 on an old Surface Go2,  it runs amazing; for a Surface Go2 with 3Gb of RAM. No complains, 12 Gb of space to run in comparison to the 30 sometings of Windows. It came back to life, yes the camera still does not work as intendet, but everything else is great. Thanks to the people in  [GitHub - linux-surface/linux-surface: Linux Kernel for Surface Devices](https://github.com/linux-surface/linux-surface). It is an amazing work. 

With all these in mind and because I decided, "Finaly", to move to Linux as my main driver and have Windows as backup. And, since Fedora 38 just lunched.... well here we are.  This is my personal implentation. It is mainly to document the steps that I followed.  And by nomeans is the best implementation. 

*The post image was created with midjourney. Prompt: /imagine Create an abstract paint that illustrates the fusion of engineering and innovation with Data Science, navigating the crossroads of expertise to create sustainable and efficient solutions using oil as the medium, with the impasto technique, emphasizing depth and contrast, and featuring a stunning midnight blue and dark green color palette. --no Letters, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark, Human, Person, People. --aspect 7:4 --s 750 --v 5 --q 2*  

### Install Ferdora Server with KDE

- Download the server iso and lunch it in [GitHub - ventoy/Ventoy: A new bootable USB solution.](https://github.com/ventoy/Ventoy)

- In the anaconda installer:
  
  - Create a user
  
  - Select to install from mirror list use: [Fedora Mirrors - 38](https://admin.fedoraproject.org/mirrormanager/mirrors/Fedora/38)
  
  - Select Software to Install. Use KDE for this Version. Un select firefox and libreoffice.
  
  - Select the disk to use. Use Automate version. 

### Initial Configuration

Because I am installing the server version and adding KDE without firefox and libreoffice, the  defaut size for `/` is 15Gb.  I expanded it to the maximum possible size. First update the installation and install *git, kitty and zsh*.

```bash
[erick@fedora ~]$ sudo dnf update -y
[erick@fedora ~]$ sudo dnf install git kitty zsh
```

Now expand root size. Fore details see: [Fedora Server Install not Using entire disk. - YouTube](https://www.youtube.com/watch?v=MfGkBe8Y5Nk)

I am not convinced this is the correct way to move forward with the implementation. I have the feeling that *home* is out of the scope in this implementation. And, that I am not using *root* as intendet. I do not have a message board, but feel free to contact me if you have any ideas or opinions about this. 

```bash
[erick@fedora ~]$ sudo lvdisplay
[sudo] password for erick:
  --- Logical volume ---
  LV Path                /dev/fedora/root

[erick@fedora ~]$ sudo lvresize -r -l +100%FREE /dev/fedora/root
   Logical volume fedora/root successfully resized.
```

The first part, *lvdisplay*, provides the required path name for *lvresize*.

Now create a folder to build the setup. Eventually everything that needs to be build lands here. 

```bash
mkdir Build
cd Build
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/denysdovhan/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"

nano ~/.zshrc
```

once in nano, configure *oh-my-zsh* prompt inside *.zshrc*. Replace the `ZSH_THEME=XXX` with:

`ZSH_THEME="fino"`

Finaly add a couple of pluggins to highlight the commands and generate autosuggestions. 

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

nano ~/.zshrc
```

Configure the plugins inside .zshrc

change `plugins=(git)` to `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`

### Compile .zshrc

```bash
source ~/.zshrc
```

### Install Vivaldi with dnfdragora package installer.

```bash
mkdir vivaldi
cd vivaldi
wget https://downloads.vivaldi.com/stable/vivaldi-stable-6.0.2979.18-1.x86_64.rpm
```

After downloading it. Go to the folder location within Dolphin. Select run with dnfdragora package installer by doing right click to the rpm file. The 6.0.2979.18-1.x86_64 version is the latest at the time this post is being publish. Review the latest version.

### Install the following programs and applications

- Install AppImageLauncher follow the steps in [Home · TheAssassin/AppImageLauncher Wiki · GitHub](https://github.com/TheAssassin/AppImageLauncher/wiki). Use dnfdragora package installer. Same procedure as with Vivaldi

- Onlyoffice AppImage, use its [AppImage](https://www.onlyoffice.com/download-desktop.aspx)

- Marktext AppImage [latest release](https://github.com/marktext/marktext/releases/latest)

- neofetch 

```bash
sudo dnf install neofetch
```

### Setup GitHub

Create SSH key and setup. Follow the instructions at [Connecting to GitHub with SSH - GitHub Docs](https://docs.github.com/authentication/connecting-to-github-with-ssh). 

### Setup Visual Studio Code

Follow the instructions in: [Running Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions)

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'

dnf check-update
sudo dnf install code
```

### Install and configure pyenv inside .zshrc

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init --path)"\nfi' >> ~/.zshrc
```

### Install [Jekyll](https://jekyllrb.com) and setup for [Basically Basic Jekyll Theme](https://mmistakes.github.io/jekyll-theme-basically-basic/)

Follow the installation steps [Jekyll on Linux](https://jekyllrb.com/docs/installation/other-linux/) 

In brief install prerequisites. 

```
sudo dnf install ruby ruby-devel openssl-devel redhat-rpm-config @development-tools
```

Add gems to path with:

```bash
nano ~/.zshrc
```

```bash
# Install Ruby Gems to ~/gems
export GEM_HOME="$(ruby -e 'puts Gem.user_dir')"
export PATH="$GEM_HOME/bin:$PATH"
export GEM_BINN="$HOME/bin"
export PATH="$GEM_BINN:$PATH"
```

```bash
source ~/.zshrc
```

Install Jekyll and Bundler gems

```
gem update
gem install jekyll bundler
```

There was missing a library `make: g++: No such file or directory`.

Solve it installing 

```bash
dnf install gcc-c++
```

Follow the instuctions [Basically Basic Jekyll Theme](https://mmistakes.github.io/jekyll-theme-basically-basic/), run 

```bash
bundle install
```

Ruby suggest to update it to its latest verssion. Howerver a permision error was trigger. 

A solution is to install it as a super user. However ruby shows the message: **Do not run** `bundle install`  **with root privilegies.** Because the Ruby gems was installed with dnf, it was installed as superuser. The right way to update ruby gems in this case is to use Fedora dnf. But this will not have the latest version. Which may not be needed in this case. 

A solution would be to install Ruby Gems according to  [Download RubyGems / your community gem host](https://rubygems.org/pages/download). But that is out of the scope of my usage. 

So far is were we are. I am still missing  Pandoc, LuaLaTex,  pdftk, TexLive and TexStudio. Advance data science setup, yes NVIDIA drivers... 
