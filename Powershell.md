## Powershell for Linux

 See [Install and configure Azure PowerShell on macOS and Linux](https://docs.microsoft.com/en-us/powershell/azure/install-azurermps-maclinux?view=azurermps-6.1.0)


You'll need to install two dependencies.

1. libcurl3
2. libicu57

This set of bash commands below will automate the installation of the dependencies, and Powershell

```bash
cd ~/Downloads && \
sudo apt install libcurl3 && \
wget http://launchpadlibrarian.net/317614660/libicu57_57.1-6_amd64.deb && \
sudo apt install ./libicu57_57.1-6_amd64.deb && \
wget https://github.com/PowerShell/PowerShell/releases/download/v6.1.0-preview.2/powershell_6.1.0-preview.2-1.ubuntu.17.04_amd64.deb && \
sudo dpkg -i powershell_6.1.0-preview.2-1.ubuntu.17.04_amd64.deb
```

Install Azure Powershell module.

```bash
sudo pwsh -Command Install-Module AzureRM.NetCore
```

Getting out of trouble if you have problems installing Powershell.

```bash
sudo apt --fix-broken install
```

To start Powershell

```bash
pwsh
```

Be sure to add the Powershell extension in Visual Studio Code.

Notes.


2. [Install Powershell in Ubuntu 17.04](https://askubuntu.com/questions/905018/install-powershell-in-ubuntu-17-04)
3. [libicu57 57.1-6 (amd64 binary) in ubuntu bionic](https://launchpad.net/ubuntu/bionic/amd64/libicu57/57.1-6)
4. [Powershell Releases](https://github.com/PowerShell/PowerShell/releases/tag/v6.1.0-preview.2)
