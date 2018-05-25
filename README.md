# Linux for Azure Developers

## Platform

|||
|----|---|
|Platform| Ubuntu 18.04|
|Date|As at May 2018|

##

1. Visual Studio Code 
2. Azure Storage Explorer
3. Lastest .NET Core SDK
4. Azure CLI
4. Azure Functions
5. Docker (Including cross compiling for ARM)
5. Azure IoT Edge 
6. Postman
7. Microsoft SQL for Linux (and Management Tools)



### Visual Studio Code

Easy. From Ubuntu Store, search for Visul Studio Code and install.

### Install GitHub Client

```bash
$ sudo apt install git
```



Useful Extensions.

1. Azure Account
1. Azure Functions
1. Azure Cosmos DB
2. Azure IoT Edge
3. Azure IoT Toolkit
4. C#
5. Docker
6. Python


### Azure Storage Explorer

1. [Microsoft Azure Storage Explorer release notes](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-relnotes)
2. https://answers.launchpad.net/ubuntu/bionic/amd64/libcanberra-gtk0

1. Install curent release of the [.NET Core SDK](https://www.microsoft.com/net/download/linux-package-manager/ubuntu18-04/sdk-current)
2. Confim successful installation of .NET Core SDK
    ```bash
    $ dotnet --version
    ```
3. Install required dependencies
    ```bash
    $ sudo apt install libgconf-2-4 libcanberra-gtk0 libgnome-keyring0
    ```

4. [Download and Install Storage Explorer. Be sure to select Linux from the dropdown.](https://azure.microsoft.com/en-au/features/storage-explorer/)

5. Extract the Storage Explorer .tar.gz file and copy to /opt directory

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

## Install Azure CLI

Install Curl
```bash
$ sudo apt install curl
```

Follow instruction for [Install Azure CLI 2.0 with apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest)

## Postman

Follow instruction at [How to Install the Postman Native App in Ubuntu 16.04](https://blog.bluematador.com/posts/postman-how-to-install-on-ubuntu-1604/)

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

### Docker

[How to Install Docker On Ubuntu 18.04 Bionic Beaver](https://linuxconfig.org/how-to-install-docker-on-ubuntu-18-04-bionic-beaver)

```bash
sudo apt install docker.io && \
sudo systemctl start docker && \
sudo systemctl enable docker
```

It's useful to add your user sudo rights to Docker. Note, you'll need to restart your system.

```bash
sudo usermod <Your User Name> -aG docker
```
#### Building ARM Docker Images from an x64 Ubuntu Host

If your docker ARM base image is already built to include QEMU then register QEMU in the build agent as follows.

```bash
docker run --rm --privileged multiarch/qemu-user-static:register --reset
```

Otherwise follow the instruction on [How to Build ARM Docker Images on Intel host](http://www.hotblackrobotics.com/en/blog/2018/01/22/docker-images-arm/)


## Azure Functions with Visual Studio Code

[Code and test Azure Functions locally](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)

[Install Node.js using Standard Ubuntu 18.04 Repository](https://linuxconfig.org/how-to-install-node-js-on-ubuntu-18-04-bionic-beaver-linux)

At the time of writting (May 25, 2018) the npm install sucessfully installed the latest Azure Function Core Tools.

#### Install Azure Funcion Core Tools with npm Package Management

```bash
sudo apt install nodejs && \
sudo apt install npm && \
sudo npm install -g azure-functions-core-tools@core
```


#### Install Azure Functions Core Tools with apt Package Management


```bash
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-bionic-prod <version> main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-get update

sudo apt-get install azure-functions-core-tools
```

## Microsoft SQL Server for Linux

[Install SQL Server and create a database on Ubuntu](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-linux-2017)

### Dockerised MS SQL

Note, running MS SQL in a container does not save data when the container is stopped.

[Run the SQL Server 2017 container image with Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-linux-2017)

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -d microsoft/mssql-server-linux:2017-latest
```

### Microsoft SQL Operations Studio

[Install Microsoft SQL Operations Studio](https://docs.microsoft.com/en-gb/sql/sql-operations-studio/what-is?view=sql-server-linux-2017)


### MS SQL Extension for Visual Studio Code

[Use Visual Studio Code to create and run Transact-SQL scripts for SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-vscode?view=sql-server-linux-2017)

From Visual Studio Code

1. Press CTRL+SHIFT+P (or F1) to open the Command Palette in VS Code.
2. Select Install Extension and type mssql.
3. Click install mssql. 


### 