
# Get a clean install of WSL

## Find and remove existing install 
 
* You may want to create a file at ~/ so once this process is completed you can verify its gone.
* --uninstall looks like --unregister but didn't leave me with a clean distro after install

> wsl --list

> wsl --unregister <DistributionName>

## Update WSL

> wsl --update

## Start a new install 

* --install defaults to to Ubuntu but you could specify another distro if you want
* --setdefault might not be necessary if you just run 'wsl --install'
* I had a competing docker-desktop distribution installed hence the need for --setdefault.

> wsl --list --online

> wsl --install Ubuntu

> wsl --setdefault Ubuntu

# Set up the WSL environment 

Run these commands from WSL

## Prevent leakage from windows environment

First we prevent our windows path from being used, so we don't have conflicting npm installs (see https://stackoverflow.com/questions/63716587/in-wsl2-ubuntu-20-04-for-windows-10-nodejs-is-installed-but-npm-is-not-working for reference)

> echo $PATH 

> sudo vi /etc/wsl.conf

Add the following snippet:

```
[interop]
appendWindowsPath=false
```

Restart wsl, and check 

> echo $PATH

## Install NVM/NPM/Node

> sudo apt update

> sudo apt install curl

> curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

Exit and restart WSL so path updates take effect.

> nvm --version
>> 0.39.1

> nvm install node

> npm --version
>> 11.6.0

> node --version
>> v24.9.0

## Install ASP.NET 10 (currently in prerelease)

> sudo add-apt-repository ppa:dotnet/previews

> sudo apt update

I guess this repository has updated for already installed things, as I was prompted to also

> sudo apt upgrade

> sudo apt install dotnet10

## Install Powershell

> sudo snap install powershell --classic

