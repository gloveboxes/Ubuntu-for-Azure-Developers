# Linux for Azure Developers

## Platform

|||
|----|---|
|Platform| Ubuntu 18.04|
|Date|May 2018|

##

1. Visual Studio Code 
2. Azure Storage Explorer
3. .NET Core 2
4. Azure Functions
5. Azure IoT Edge (Inlcuding cross compiling for ARM)


### Visual Studio Code

Easy. From Ubuntu Store, search for Visul Studio Code and install.

###$ Install GitHuh Client

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

4. [Download and Install Storage Explorer](https://www.microsoft.com/net/download/linux-package-manager/ubuntu18-04/sdk-current)

5. untar Storage Explorer .tar.gz file and copy to /opt directory

    ```bash
    $ sudo mkdir -p /opt/StorageExplorer-linux-x64 && sudo tar -C $_ -zxvf StorageExplorer-linux-x64.tar.gz
    ```

6. Create Storage Explorer Desktop Resource 

```bash
cat > ~/.local/share/applications/StorageExplorer.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Storage Explorer
Exec=/opt/StorageExplorer-linux-x64/StorageExplorer
Icon=/opt/StorageExplorer-linux-x64/resources/app/out/app/icon.png
Terminal=false
Type=Application
Categories=Development;
EOL
```