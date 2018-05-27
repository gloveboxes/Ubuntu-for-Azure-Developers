# Linux for Azure Developers

Setting up a developer environment to build Azure based solutions is now very well supported across Windows, Mac and Linux. 

I find myself developing more and more for Azure from Ubuntu Desktop. It's a great experience and there is superb first class open source tooling support from Microsoft (and others) for Azure across Windows, Mac and Linux. 

I've tended to stick with the LTS releases of Linux, better support, examples, documentaton etc. With the release of [Ubuntu 18.04 LTS](https://www.ubuntu.com/desktop) I decided is was time to upgrade from Ubuntu 16.04 LTS. Yup, I could have done an inplace upgrade but sometimes it's just better to start afresh.

So here are the applications, command line tools and SDKs that I installed for my Azure centric Ubuntu 18.04 developer desktop.

This guide assumes you have some experience with Linux. Terminal and Ctrl-Shift-V to paste in [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) commands is your friend. 

Given Ubuntu 18.04 is still fresh I documentated the additional libraries you'll need to install.


|||
|----|---|
|Platform| Ubuntu 18.04|
|Date|As at May 2018|

## The Essentials

1. Visual Studio Code (#1 GitHub project by contributors)
2. GitHub client
3. Lastest .NET Core SDK (in top 10 most discussed GitHub projects)
4. Azure Storage Explorer
5. Azure CLI
5. Azure Functions
6. Azure Event Hub

## Tools
1. Azure IoT Edge (an Azure CLI Extension)

## Apps

1. Docker
2. Docker Cross Compiling for ARM
3. Postman
4. Fiddler

## Microsoft SQL Server
7. Microsoft SQL Server for Linux 
8. Micrsoft SQL Managament tools for Linux

## Embedded Development

1. Arduino
2. Fritzing


## Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com/) is a must have IDE, open source, extensible, great language, debugging and tooling support.  

installation is easy, in fact it's a [Snap](https://en.wikipedia.org/wiki/Snappy_(package_manager)). From Ubuntu Store, search for Visul Studio Code and install.

### Visual Studio Extensions

There are a stack of great extensions for Visual Studio Code
Useful Extensions.

1. Azure Account, Azure Functions, Azure Event Hub Explorer, Azure Cosmos DB, Azure IoT Edge, Azure IoT Toolkit, mssql, C#, Docker, Python, C/C++.


## GitHub Client

You'll be prompted what you start Visual Studio Code to install, it's simple too.


```bash
sudo apt install git
```

You'll need to create a GitHub token that you need to store securely. See [Creating a personal access token for the command line](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) for more information. You'll need to use this token in place of your password when pushing changes to GitHub.



## Latest .NET Core SDK

1. Install the latest release of the [.NET Core SDK](https://www.microsoft.com/net/download/linux-package-manager/ubuntu18-04/sdk-current)

2. Confim successful installation of .NET Core SDK

    ```bash
    dotnet --version
    ```


## Azure Storage Explorer


1. Install required dependencies

    ```bash
    sudo apt install libgconf-2-4 libcanberra-gtk0 libgnome-keyring0
    ```



2. [Download and Install Storage Explorer. Be sure to select Linux from the dropdown.](https://azure.microsoft.com/en-au/features/storage-explorer/)

5. Extract the Storage Explorer .tar.gz file, copy to /opt directory, and add a symbolic link to the StorageExplorer executable.

    ```bash
    sudo mkdir -p /opt/StorageExplorer-linux-x64 && \
    sudo tar -C $_ -zxvf StorageExplorer-linux-x64.tar.gz && \
    sudo ln -s /opt/StorageExplorer-linux-x64/StorageExplorer /usr/bin/StorageExplorer
    ```

6. Create Storage Explorer Desktop Resource 

    ```bash
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
 

## Install Azure CLI (Command Line Interface)

    Install Curl
    ```bash
    $ sudo apt install curl
    ```

Notes.

* [Install Azure CLI 2.0 with apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest)



## Postman


Install library dependency

```bash
$ sudo apt install libgconf-2-4
```
Download and Install Postman

```bash
cd ~/Downloads && \
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz && \
sudo tar -xzf postman.tar.gz -C /opt && \
rm postman.tar.gz && \
sudo ln -s /opt/Postman/Postman /usr/bin/postman
```

Create Postman Desktop Resource

```bash
cat > ~/.local/share/applications/postman.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Postman
Exec=postman
Icon=/opt/Postman/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
EOL
```

Notes.
* Follow instruction at [How to Install the Postman Native App in Ubuntu 16.04](https://blog.bluematador.com/posts/postman-how-to-install-on-ubuntu-1604/)

## Fidler

[Use Fiddler in Ubuntu](https://medium.com/@rajsek/use-fiddler-in-ubuntu-82b1dfd80848)


## Docker


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


## Building ARM Docker Images from an x64 Ubuntu Host


```bash
docker run --rm --privileged multiarch/qemu-user-static:register --reset
```

Notes.
* If your docker ARM base image is already built to include QEMU then register QEMU in the build agent as follows.
* Otherwise follow the instruction on [How to Build ARM Docker Images on Intel host](http://www.hotblackrobotics.com/en/blog/2018/01/22/docker-images-arm/)


## Azure Functions with Visual Studio Code

[Code and test Azure Functions locally](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)

[Install Node.js using Standard Ubuntu 18.04 Repository](https://linuxconfig.org/how-to-install-node-js-on-ubuntu-18-04-bionic-beaver-linux)

At the time of writting (May 25, 2018) I had more success installing the latest Azure Function Core Tools via npm than apt.

### Install Azure Funcion Core Tools with npm Package Management

    ```bash
    sudo apt install nodejs && \
    sudo apt install npm && \
    sudo npm install -g azure-functions-core-tools@core
    ```


### Install Azure Functions Core Tools with apt Package Management


    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

    sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

    sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-bionic-prod <version> main" > /etc/apt/sources.list.d/dotnetdev.list'

    sudo apt-get update

    sudo apt-get install azure-functions-core-tools
    ```

## Microsoft SQL Server for Linux

[Install SQL Server and create a database on Ubuntu](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-linux-2017)

### Dockerised Microsoft SQL Server

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


## Microsoft SQL Server Operations Studio

[Install Microsoft SQL Operations Studio](https://docs.microsoft.com/en-gb/sql/sql-operations-studio/what-is?view=sql-server-linux-2017)


## Microsoft SQL Server Extension for Visual Studio Code

[Use Visual Studio Code to create and run Transact-SQL scripts for SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-vscode?view=sql-server-linux-2017)

From Visual Studio Code

1. Press CTRL+SHIFT+P (or F1) to open the Command Palette in VS Code.
2. Select Install Extension and type mssql.
3. Click install mssql. 


## Azure IoT Edge

[Develop and deploy a C# IoT Edge module to your simulated device - preview](https://docs.microsoft.com/en-us/azure/iot-edge/tutorial-csharp-module)

Excellent Samples

[Hands-on Grove Starter Kit for Azure IoT Edge](https://azure-samples.github.io/azure-iot-starter-kits/seeed/)

## Azure Event Hub monitor

Install Visual Studio Code Extention "[Azure Event Hub Explorer](https://marketplace.visualstudio.com/items?itemName=Summer.azure-event-hub-explorer)"


## Install Azure IoT Hub Explorer

[Installing and using iothub-explorer](https://github.com/Azure/iothub-explorer)

[Microsoft Azure IoT Extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md)




    ```bash
    az extension add --name azure-cli-iot-ext
    ```

[az iot Command Guide](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-iot-ext/iot?view=azure-cli-latest)

Example IoT Hub command

    ```bash
    * az iot hub monitor-events --hub-name IotHubName
    ```


# Embedded Development

## Optional Fritzing

Download from [Fritzing Download Site](http://fritzing.org/download/)

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

