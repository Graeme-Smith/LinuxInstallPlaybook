# Install Linux Mint
Download ISO image

Right click and create bootable USB

Use bootable USB to install Linux Mint

### Manual Setup of Ansible and git

```bash
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get install ansible
sudo apt-get install git
```

### Clone github repo

```bash
cd Desktop/
git clone https://github.com/Graeme-Smith/LinuxInstallPlaybook.git
```

# Bash Utilities (Installed via Ansible)

| Bash Utility | Description | Status |
|--------------|-------------|--------|
| docker       |             |        |
| gparted      | Managing disk partitions            |        |
| htop      |             |        |
| jq           | Parsing JSON files            |        |
| pavucontrol  |             |        |
| python3-pip  |             |        |
| tmux         |             |        |
| tree         |             |        |
| vim        |             |        |


## Run ansible playbook
```bash
ansible-galaxy install -r requirements.yml
sudo ansible-playbook local.yml
```

# Setup profiles

## Setup .bashrc profile
```bash
mv $HOME/Desktop/LinuxInstallPlaybook/.bashrc $HOME
```

## Setup .vimrc
```bash
mv $HOME/Desktop/LinuxInstallPlaybook/.vimrc $HOME
```

# Current list of manual installation

### Google Chrome
Search for 'download google chrome' and follow instructions

### Citrix Workspace
I downloaded the latest deb file for Citrix Workspace app for Linux from [https://www.citrix.com/en-gb/downloads/workspace-app/linux/workspace-app-for-linux-latest.html ](https://www.citrix.com/en-gb/downloads/workspace-app/legacy-workspace-app-for-linux/workspace-app-for-linux-latest2.html)

WARNING: When configurung the ICAclient during installation I installed it without the app protection as this interfered with other apps such as the Heroku CLI

For Citrix to work I needed to share the certificates used by FireFox:
```bash
sudo ln -s /usr/share/ca-certificates/mozilla/* /opt/Citrix/ICAClient/keystore/cacerts
```
### Install Miniconda
https://docs.conda.io/en/latest/miniconda.html#linux-installers
```bash
bash $HOME/Downloads/Miniconda3-py39_4.12.0-Linux-x86_64.sh
```
### Import conda environments from yml files TODO Redo these environments for python 3.9
```bash
conda env create -f $HOME/Desktop/LinuxInstallPlaybook/CondaEnvs/ngs.yml
conda env create -f $HOME/Desktop/LinuxInstallPlaybook/CondaEnvs/myDjangoEnv.yml
```
### Install davmail
```bash
sudo apt update
sudo apt install davmail
```

# Software

### Mendeley
Download https://www.mendeley.com/download-desktop-new/#download make the Appimage executable, and copy to Desktop.


### MS Teams
Download Deb at https://www.microsoft.com/en-us/microsoft-teams/download-app#desktopAppDownloadregion

### Zoom
https://zoom.us/download

### Snap
```bash
sudo rm /etc/apt/preferences.d/nosnap.pref
sudo apt update
sudo apt install snapd
```

### Slack
```bash
sudo snap install slack --classic
```

### Remmina
```bash
sudo snap install remmina
# some features, for example password storage via keyring is missing and must be fixed manually:
sudo snap connect remmina:audio-record :audio-record
sudo snap connect remmina:avahi-observe :avahi-observe # servers discovery
sudo snap connect remmina:cups-control :cups-control # printing
sudo snap connect remmina:mount-observe :mount-observe # mount management
sudo snap connect remmina:password-manager-service :password-manager-service # password manager
```
### ngrok
```bash
sudo snap install ngrok
ngrok authtoken <Auth Token Here>
```
### Gisto
```bash
sudo snap install gisto
```

### Install JavaScript
```bash
#Install NVM
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Install NODE
nvm install node
nvm install-latest-npm
npm cache clean --force
npm audit fix --force
```

### Timeular App
Download https://timeular.com/download/ make the Appimage executable, and copy to Desktop.


### R
```bash
sudo apt-get update
sudo apt-get install r-base r-base-dev
```

### RStudio
```bash
sudo apt-get install gdebi-core
wget https://download2.rstudio.org/server/jammy/amd64/rstudio-server-2022.07.1-554-amd64.deb
sudo gdebi rstudio-server-2022.07.1-554-amd64.deb
```

### Sublime Text
```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text
```

### VS Code
```bash
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code

# Install extensions listed in file
cd $HOME/Desktop/LinuxInstallPlaybook
cat vs_code_extensions_list.txt | xargs -n 1 code --install-extension
```

!!! Remember to disable biosyntax extension when not in use !!!

### Install GitLens to VS Code
```
ext install eamodio.gitlens
```
### Install Git Graph
```
ext install mhutchie.git-graph
```

# Setup GitHub

Follow the instructions at https://docs.github.com/en/authentication/connecting-to-github-with-ssh
* Generate SSH key if required
* Add key to Github

Add user email and user name
```bash
git config --global user.email "<email-address>"
git config --global user.name "Graeme-Smith"
```
Set LinuxInstallPlaybook repo to use ssh
```bash
git remote set-url origin git@github.com:Graeme-Smith/LinuxInstallPlaybook.git
```

# DNA Nexus utilities

## dx toolkit
```bash
pip3 install dxpy
# Allow tab completion:
eval "$(register-python-argcomplete dx|sed 's/-o default//')"
```

## dx upload agent
```bash
cd $HOME/Downloads
wget https://dnanexus-sdk.s3.amazonaws.com/dnanexus-upload-agent-1.5.33-linux.tar.gz -O - | tar -xzf -
mv dnanexus-upload-agent-*-linux $HOME/Software/
alias ua='$HOME/Software/dnanexus-upload-agent-1.5.33-linux/ua' 
```

# Bioinformatic tools installed via Bioconda
```bash
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

conda install samtools
conda install igv
conda install bamtools
conda install bcftools
conda install bedtools
conda install bioawk
conda install blast
conda install bowtie2
conda install bracken
conda install bwa
conda install bwa-mem
conda install canu
conda install fastqc
conda install fastx_toolkit
conda install kracken2
conda install minimap2
```


