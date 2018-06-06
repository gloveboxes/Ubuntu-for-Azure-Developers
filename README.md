# Kubuntu for Azure Developers

|Author|Dave Glover, Microsoft Australia|
|----|---|
|Platform| [Kubuntu 18.04](https://kubuntu.org/). Also see [Ubuntu 18.04 for Azure Developers](Ubuntu1804.md) and [Ubuntu 16.04 for Azure Developers](Ubuntu1604.md)|
|Date|As at June 2018|
|System| Lenovo ThinkPad X1 Carbon Gen 1|

<!-- TOC -->

- [Kubuntu for Azure Developers](#kubuntu-for-azure-developers)
    - [Getting started with Azure](#getting-started-with-azure)
    - [Installing the Essentials](#installing-the-essentials)
        - [Visual Studio Code](#visual-studio-code)
        - [Visual Studio Extensions](#visual-studio-extensions)
        - [GitHub Client](#github-client)
        - [Installing the latest .NET Core SDK](#installing-the-latest-net-core-sdk)
        - [Azure Storage Explorer](#azure-storage-explorer)
        - [Azure CLI (Command Line Interface)](#azure-cli-command-line-interface)
    - [Azure Functions with Visual Studio Code](#azure-functions-with-visual-studio-code)
        - [Install Azure Functions Core Tools](#install-azure-functions-core-tools)
    - [Toolkit](#toolkit)
        - [Docker](#docker)
        - [Postman](#postman)
        - [Fiddler](#fiddler)
        - [VirtualBox](#virtualbox)
    - [Internet of Things](#internet-of-things)
        - [Azure IoT Hub Explorer](#azure-iot-hub-explorer)
        - [Azure IoT Edge](#azure-iot-edge)
            - [Building ARM Docker Images from an x64 Ubuntu Host](#building-arm-docker-images-from-an-x64-ubuntu-host)
    - [Microsoft SQL Server for Linux](#microsoft-sql-server-for-linux)
        - [Microsoft SQL Server for Linux (Dockerised)](#microsoft-sql-server-for-linux-dockerised)
        - [Microsoft SQL Server Operations Studio](#microsoft-sql-server-operations-studio)
        - [Microsoft SQL Server Extension for Visual Studio Code](#microsoft-sql-server-extension-for-visual-studio-code)
    - [Embedded Development](#embedded-development)
        - [Arduino](#arduino)
        - [Fritzing](#fritzing)
    - [Samples](#samples)
        - [Azure IoT Edge Samples](#azure-iot-edge-samples)
        - [Debugging .NET Core apps in Docker Containers from Visual Studio Code on Linux](#debugging-net-core-apps-in-docker-containers-from-visual-studio-code-on-linux)

<!-- /TOC -->

Developing on Linux for Azure is a great experience and there is superb open source tooling support from Microsoft (and others) for Azure across Windows, Mac and Linux.

I've tended to stick with the LTS releases of Linux, better support, examples, documentation etc. With the release of [Ubuntu 18.04 LTS](https://www.ubuntu.com/desktop) I decided it was time to upgrade from Ubuntu 16.04 LTS system. After a few false starts for my system (X1 Carbon) I found the [Kubuntu](https://kubuntu.org/) flavour to be more stable and I also like the level of customization.

So here are the applications, command line tools and SDKs that I have installed for my Azure centric Kubuntu 18.04 developer desktop. Enjoy:)

This guide assumes you have some experience with Linux and you will open Terminal and Ctrl-Shift-V to paste in [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) commands.

Given Kubuntu 18.04 is still fresh I documented the additional libraries you'll need to install.

**Feel free to contribute to this guide.**

## Getting started with Azure

If you are new to Azure then the following resources are a great place to start.

1. [Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/)
2. [Architecting Distributed Cloud Applications video series](https://www.youtube.com/watch?v=xJMbkZvuVO0&list=PL9XzOCngAkqs0Q8ZRdafnSYExKQurZrBY)
3. [Microsoft Azure Blog](https://azure.microsoft.com/en-us/blog/)
4. [Channel9 Technical Training](https://channel9.msdn.com/)

## Installing the Essentials

### Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com/) is a must have IDE, open source, extensible, great language, debugging and tooling support.  

Head to [Visual Studio Code](https://code.visualstudio.com/) and download the .deb file for Debian and Ubuntu then install with QApt Package Installer.

### Visual Studio Extensions

There are a stack of great extensions for Visual Studio Code. This are the ones that I find most useful.

1. Azure Account, Azure Functions, Azure CLI Tools, Azure Event Hub Explorer, Azure Cosmos DB, Azure IoT Edge, Azure IoT Toolkit, mssql, C#, Docker, Python, C/C++, JSON Tools, Powershell, Azure Application Insights, Azure App Services, Arduino, Azure Resource Manager Tools, Azure Storage, Tools for AI and more...

### GitHub Client

When you start Visual Studio Code for the first time you'll be prompted to install the GitHub client.

```bash
sudo apt install git
```

Before you can commit any changes against GitHub you'll need to configure who you are.

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

If you are using GitHub two-factor authentication then you'll need to create a GitHub token that you need to store securely. See [Creating a personal access token for the command line](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) for more information. You'll need to use this token in place of your password when pushing changes to GitHub.

Check out [Caching your GitHub password in Git](https://help.github.com/articles/caching-your-github-password-in-git/) to cache your GitHub credentials so you won't be asked for your credentials every time you push/sync you repository. 

In summary you need to run the following commands. Personally I use a much bigger number than 3600.

```bash
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'
```

If you are using Visual Studio Team Services then checkout [Use Git Credential Managers to Authenticate to VSTS](https://docs.microsoft.com/en-gb/vsts/git/set-up-credential-managers?view=vsts)

### Installing the latest .NET Core SDK

1. Install the latest release of the [.NET Core SDK](https://www.microsoft.com/net/download/linux-package-manager/ubuntu18-04/sdk-current)

2. Confirm successful installation of .NET Core SDK

```bash
dotnet --version
```

### Azure Storage Explorer

1. Install required dependency

```bash
sudo apt install libgnome-keyring0
```

2. Next [Download and Install Storage Explorer. Be sure to select Linux from the drop-down.](https://azure.microsoft.com/en-au/features/storage-explorer/)

5. The following Bash commands extract the Storage Explorer .tar.gz file to the /opt directory, and add a symbolic link to the StorageExplorer executable.

```bash
cd ~/Downloads && \
sudo mkdir -p /opt/StorageExplorer-linux-x64 && \
sudo tar -C $_ -zxvf StorageExplorer-linux-x64.tar.gz && \
sudo ln -s /opt/StorageExplorer-linux-x64/StorageExplorer /usr/bin/StorageExplorer

```

6. Create Storage Explorer [Ubunutu/KDE](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) Desktop Resource

```bash
mkdir -p ~/.local/share/applications && \
cat > ~/.local/share/applications/StorageExplorer.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Storage Explorer
Exec=StorageExplorer
Icon=/opt/StorageExplorer-linux-x64/resources/app/out/app/icon.png
Terminal=false
Type=Application
Categories=Development;
EOL

```

Notes.
* [Microsoft Azure Storage Explorer release notes](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-relnotes)
* https://answers.launchpad.net/ubuntu/bionic/amd64/libcanberra-gtk0

### Azure CLI (Command Line Interface)

Be sure that 'curl' is installed.

```bash
sudo apt install curl
```

[Install Azure CLI 2.0 with apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest)

## Azure Functions with Visual Studio Code

[Code and test Azure Functions locally](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)

### Install Azure Functions Core Tools

At the May 2018 I used the Ubuntu 17.04 (artful) release of the Azure Function Core tools.

````bash
cd ~/Downloads && \
sudo apt install curl -y && \
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && \
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg && \
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-artful-prod artful main" > /etc/apt/sources.list.d/dotnetdev.list' && \
sudo apt-get update && \
sudo apt-get install azure-functions-core-tools

````

## Toolkit

### Docker

```bash
sudo apt install docker.io && \
sudo systemctl start docker && \
sudo systemctl enable docker
```

It's useful to add your user sudo rights to Docker. Note, you'll need to restart your system for this setting to take effect.

```bash
sudo usermod <Your User Name> -aG docker
```

Notes.

* [How to Install Docker On Ubuntu 18.04 Bionic Beaver](https://linuxconfig.org/how-to-install-docker-on-ubuntu-18-04-bionic-beaver)


### Postman

Install library dependency

```bash
sudo apt install libgconf-2-4
```

Download and Install Postman

```bash
cd ~/Downloads && \
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz && \
sudo tar -xzf postman.tar.gz -C /opt && \
rm postman.tar.gz && \
sudo ln -s /opt/Postman/app/Postman /usr/bin/postman

```

Create Postman Desktop Resource

```bash
cat > ~/.local/share/applications/postman.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Postman
Exec=postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
EOL

```

Notes.

* Follow instruction at [How to Install the Postman Native App in Ubuntu 16.04](https://blog.bluematador.com/posts/postman-how-to-install-on-ubuntu-1604/)

### Fiddler

See [Use Fiddler in Ubuntu](https://medium.com/@rajsek/use-fiddler-in-ubuntu-82b1dfd80848)

### VirtualBox

```bash
sudo apt-get install virtualbox
```

## Internet of Things

### Azure IoT Hub Explorer

```bash
az extension add --name azure-cli-iot-ext
```

[az iot Command Guide](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-iot-ext/iot?view=azure-cli-latest)

Example IoT Hub command

```bash
az iot hub monitor-events --hub-name IotHubName
```

Notes.

* [Installing and using iothub-explorer](https://github.com/Azure/iothub-explorer)
* [Microsoft Azure IoT Extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md)


### Azure IoT Edge

* [Develop and deploy a C# IoT Edge module to your simulated device - preview](https://docs.microsoft.com/en-us/azure/iot-edge/tutorial-csharp-module)

#### Building ARM Docker Images from an x64 Ubuntu Host

If you are targeting ARM for your Docker builds then you will need to run the following command before you do your Docker build.

```bash
docker run --rm --privileged multiarch/qemu-user-static:register --reset
```

Notes.

* If your docker ARM base image is already built to include QEMU then register QEMU in the build agent as follows.
* Otherwise follow the instruction on [How to Build ARM Docker Images on Intel host](http://www.hotblackrobotics.com/en/blog/2018/01/22/docker-images-arm/)

## Microsoft SQL Server for Linux

### Microsoft SQL Server for Linux (Dockerised)

[Install SQL Server and create a database on Ubuntu](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-linux-2017)

Note, deleting a Microsoft SQL Server Docker container will also delete its data. So docker run to download and create and run the docker SQL Container and then use docker stop and start to control.

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
-p 1433:1433 --name sql1 \
-d microsoft/mssql-server-linux:2017-latest

```

To **stop** the Microsoft SQL Server Docker container.

```bash
docker stop sql1
```

To **start** the Microsoft SQL Server Docker container.

```bash
docker start sql1
```

Notes.

* [Run the SQL Server 2017 container image with Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-linux-2017)

### Microsoft SQL Server Operations Studio

Follow the notes for [Installing Microsoft SQL Operations Studio](https://docs.microsoft.com/en-gb/sql/sql-operations-studio/what-is?view=sql-server-linux-2017)

### Microsoft SQL Server Extension for Visual Studio Code

[Use Visual Studio Code to create and run Transact-SQL scripts for SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-vscode?view=sql-server-linux-2017)

## Embedded Development

### Arduino

Download the [Arduino IDE](https://www.arduino.cc/en/Main/Software)

### Fritzing

Download from [Fritzing Download Site](http://fritzing.org/download/).

I install in to a non system directory as Fritzing will complain that it doesn't have access rights to create parts bins.

```bash
cd ~/Downloads && \
mkdir -p ~/Apps && \
tar -C $_ -xvjf fritzing-0.9.3b.linux.AMD64.tar.bz2 && \
sudo ln -s ~/Apps/fritzing-0.9.3b.linux.AMD64/Fritzing /usr/bin/fritzing

```

Create Fritzing Desktop Resource file

```bash
cat > ~/.local/share/applications/fritzing.desktop <<EOL
[Desktop Entry]
Version=0.9.3b
Name=Fritzing
GenericName=Fritzing
Comment=Electronic Design Automation software
Exec=fritzing 
Icon=/home/dave/Apps/fritzing-0.9.3b.linux.AMD64/icons/fritzing_icon.png
Terminal=false
Type=Application
Categories=Development;IDE;Electronics;EDA;
X-SuSE-translate=false
StartupNotify=true
Categories=PCB;
MimeType=application/x-fritzing-fz;application/x-fritzing-fzz;application/x-fritzing-fzp;application/x-fritzing-fzpz;application/x-fritzing-fzb;application/x-fritzing-fzbz;application/x-fritzing-fzm;
EOL

```

## Samples

### Azure IoT Edge Samples

[Hands-on Grove Starter Kit for Azure IoT Edge](https://azure-samples.github.io/azure-iot-starter-kits/seeed/)

### Debugging .NET Core apps in Docker Containers from Visual Studio Code on Linux

[This is a sample that demonstrates how to use vscode to build and debug dotnet core 2.0 console application in docker container](https://github.com/gloveboxes/docker.dotnet.debug)