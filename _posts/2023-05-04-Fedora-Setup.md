# Fedora 38 Setup

### Install KDE

- Download the server iso and lunch it in [GitHub - ventoy/Ventoy: A new bootable USB solution.](https://github.com/ventoy/Ventoy)

- Create a user

- Select to install from mirror list use: [Fedora Mirrors - 38](https://admin.fedoraproject.org/mirrormanager/mirrors/Fedora/38)

- Select Software to Install. Use KDE for this Version

- Select the disk to use

### Initial Configuration

```bash
sudo dnf update -y
sudo dnf install kitty

mkdir Build
cd Build
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/denysdovhan/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"

nano ~/.zshrc
```

#### Configure oh-my-zys prompt inside .zshrc

`ZSH_THEME="fino"`

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

nano ~/.zshrc
```

#### Configure autosuggestions inside .zshrc

Configure autosuggestions 

change `plugins=(git)` to `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`

#### Compile .zshrc

```bash
source ~/.zshrc
```

#### Configure pyenv inside .zshrc

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init --path)"\nfi' >> ~/.zshrc
```

### Applications

- Install AppImageLauncher follow the steps in [Home · TheAssassin/AppImageLauncher Wiki · GitHub](https://github.com/TheAssassin/AppImageLauncher/wiki)

- Install Onlyoffice, use its [AppImage](https://www.onlyoffice.com/download-desktop.aspx)

- Add Marktext AppImage [latest release](https://github.com/marktext/marktext/releases/latest)

- neofetch

#### Setup GitHub

Create SSH key and setup. Follow the instructions at [Connecting to GitHub with SSH - GitHub Docs](https://docs.github.com/authentication/connecting-to-github-with-ssh). 

#### Setup Visual Studio Code

Follow the instructions in: [Running Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions)

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'

dnf check-update
sudo dnf install code
```

#### Install [Jekyll](https://jekyllrb.com) and setup for [Basically Basic Jekyll Theme](https://mmistakes.github.io/jekyll-theme-basically-basic/)

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
export GEM_HOME="$HOME/gems"
export PATH="$HOME/gems/bin:$PATH"
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

A permision error was trigger. Provide the permisions to the specified folder. This may be due to the missing path in the ~/.zshrc .

**Do not run** `bundle install`  **with root privilegies**




