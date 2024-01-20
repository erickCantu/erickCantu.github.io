---
title: "Fedora 39 - Python - Conda - Mamba" 
categories: 
    - Fedora 39
    - Python
    - Conda
    - Spyder-IDE
tags: 
    - Fedora 39
    - Work Station
    - Computer Setup
    - Python3
    - Conda
    - Mamba
    - Miniforge
    - Data Science Workstation Setup
last_modified_at: 2023-06-26T23:00:00-01:00
image: /assets/images/posts/latex/ecantu_Create_a_captivating_website_top_banner_utilizing_the_en_a9ca0251-5ec3-43f6-8b95-7bf41c9874ad.png

---

In this post I review the steps I follow to setup my workflow for *Python3*. I use mamba as package and environment manager, and *Spyder-IDE* as my choice of an Integrated Development Environment. 

## Install Mamba (python3) in Fedora39.

1. Download the bash script to install *miniforge* from *conda-forge*. Yes,  now miniforge contains mamba and its the recomended way to do it. Detail instructions are located at:  [GitHub - conda-forge/miniforge: A conda-forge distribution.](https://github.com/conda-forge/miniforge) 
   
   As noticed before, I have a folder named Build for downloading and building the software that I need. 
   
   **Do not forget to update Fedora before installing something.**
   
   ```bash
   sudo dnf update
   ```
   
   ```bash
   mkdir ~/Build/mamba
   cd ~/Build/mamba
   wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
   bash Miniforge3-Linux-x86_64.sh
   ```

2. Follow the instructions instructions in the bash script, prompted in the screen. Because I am a single user, I kept the default settings. Adjust as needed.  The installation's location is: ``~/miniforge3/ ``

3. Use `mamba` instructions the same way as `conda`. ***Most*** of them work the same way, be aware of what you are doing.  Here are some handy examples:
   
   Create an environment with Python 3.9 use:
   
   ```bash
   mamba create -n python39 python=3.9
   ```
   
   Do not forget to activate the environment before working on your projects, and installing the required libraries. Also do not forget to deactivate the environment after you are done.
   
   ```bash
   mamba activate python39
   ```
   
   ```bash
   mamba deactivate
   ```
   
   To install a single library, for example *pandas*, do:
   
   ```bash
   mamba install pandas
   ```
   
   To install a list of libraries saved in the file *requirements.txt* use:
   
   ```bash
   mamba install --file requirements.txt
   ```
   
   Here is the *requirements.txt* content:
   
   > altair==4.1.0<br>
   > jupyterlab==3.2.6<br>
   > ipywidgets==7.6.5<br>
   > matplotlib==3.5.1<br>
   > pandas==1.3.5<br>
   > jupyterlab-dash==0.1.0a3<br>
   > seaborn==0.11.1<br>
   > python-dotenv==0.19.0<br>
   > psycopg2==2.9.3<br>
   > SQLAlchemy==1.4.25<br>

## Installation and first steps in Spyder-IDE

I grew up as a Data Scientist using RStudio. Without it, I would not have follow  this career path. Since then I have been looking for an IDE that provides the same functionality that RStudio offers; in Python. This is where Spyder comes into play.  I am not a fan of Jupyter Notebooks.

1. Use mamba to install Spyder. Follow the conda instructions at: [Installation Guide; Spyder 5 documentation](https://docs.spyder-ide.org/current/installation.html#conda-based-distributions)
   
   ```bash
   mamba create -c conda-forge -n spyder-env spyder numpy scipy pandas matplotlib sympy cython
   ```
   
   ***Notice*** the ``-c`` command to force the source at *conda-forge*, and not to i.e. Anaconda. At the same time other libraries were also installed.

2. Activate the *spyder-env* environment and install the required additional plugins. Line profiler, Notebook and Terminal. The first as its name suggests, aids in line [profiling ](https://en.wikipedia.org/wiki/Profiling_(computer_programming)). The second allows the interaction with Jupyter Notebooks. And the last one integrates a terminal to the IDE. 
   
   ```bash
   mamba activate spyder-env
   mamba install spyder-line-profiler spyder-notebook spyder-terminal -c conda-forge
   ```

3. Launch Spyder-IDE from the terminal; remember to activate the spyder-env .
   
   ```bash
   mamba activate spyder-env
   spyder
   ```

4. Here is the RStudio Window Layout for the [Exploratory Data Analysis - Seattle, WA]({%post_url 2022-08-16-EDA %}) Project. ![Rstudio - Window - Layout in SpyderIDE](/assets/images/posts/mamba_spyder/rstudio_window_layout.png) 
   
   And here is the updated version:)
   
   ![My - Window - Layout in SypderIDE](/assets/images/posts/mamba_spyder/personal_window_layout.png)

5. Selecting the correct Kernell.
   
   By default Spyder uses the Python version in which it was installed. In the Spyder installation, I did not specified, it used the latest version installed in Fedora; 3.12.1. 
   
   To select the correct kernel to run your project. Select Preferences from the Tools menu and go to the Python interpreter section, there chose the appropriate interpreter. For details see [Sypder-IDE FAQ; using existing environment](https://docs.spyder-ide.org/current/faq.html#using-existing-environment)

6. To finish. Save your work. Close the Sypder-IDE window and in the terminal deactivate the environment. 
   
   ```bash
   mamba deactivate
   ```

7. **Final Notice**
   
   This Spyder-IDE setup has a big problem running in Fedora. It shows the following *Warning:*
   
   ```bash
   ❯ spyder
   Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
   fromIccProfile: failed minimal tag size sanity
   ```
   
   The root of this problem is the display version that by default the Fedora39 Workstation standard version comes with. Since Fedora25 is Wayland instead of Xorg11. Sypder is setup by default to display its interface in Xorg. And, although the IDE is displayed, the produced graphs appear as a black box.  This is an ongoing issue to be solve. The work around is to save the images as pdf or png files and open them in a separate program. This kills the benefits of having an IDE. So, be aware of this issue. I will update this post once I find a solution.  
   
   



Additional information:

[Welcome to Mamba’s documentation!](https://mamba.readthedocs.io/en/latest/index.html)

[GitHub - conda-forge/miniforge: A conda-forge distribution.](https://github.com/conda-forge/miniforge)

[Spyder - IDE for scientific programming in Python](https://www.spyder-ide.org/)

[Wayland vs. Xorg: Will Wayland Replace Xorg?](https://www.cbtnuggets.com/blog/technology/devops/wayland-vs-xorg-wayland-replace-xorg)


