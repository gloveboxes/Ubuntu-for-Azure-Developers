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

[Storage Explorer Release Notes](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-relnotes)

1. Install [.NET Core 2.0](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-relnotes)
2. Confim successful installation
    ```bash
    $ dotnet --version
    ```
3. [Microsoft Azure Storage Explorer release notes](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-relnotes)

https://answers.launchpad.net/ubuntu/bionic/amd64/libcanberra-gtk0

4. $ sudo apt install libgconf-2-4
5. $ sudo apt install libcanberra-gtk0
6. $ sudo apt install libgnome-keyring0

4. [Download and Install Storage Explorer](https://go.microsoft.com/fwlink/?LinkId=722418)
* Extract StorageExplorer-linux-x64.tar.gz
* Open terminal
    ```bash
    $ sudo cp -r StorageExplorer-linux-x64 /opt/
    ```

6. 

```bash
cat > ~/.local/share/applications/postman.desktop <<EOL
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