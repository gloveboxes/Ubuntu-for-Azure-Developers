# 1. Ubuntu 20.04 for Azure Developers

[Ubuntu for Azure Developers](../README.md)

|Author|Dave Glover, Microsoft |
|----|---|
|Date|As at Mar 2020|

- [1. Ubuntu 20.04 for Azure Developers](#1-ubuntu-2004-for-azure-developers)
	- [Visual Studio Code](#visual-studio-code)
	- [Useful apps](#useful-apps)
		- [Utilities](#utilities)
		- [C/C++ Development](#cc-development)
	- [Visual Studio Extensions](#visual-studio-extensions)
	- [GitHub Client](#github-client)
	- [Installing the latest .NET Core SDK](#installing-the-latest-net-core-sdk)
	- [Azure Storage Explorer](#azure-storage-explorer)
	- [Azure Storage Emulator](#azure-storage-emulator)
	- [Azure CLI (Command Line Interface)](#azure-cli-command-line-interface)
	- [Azure Functions with Visual Studio Code](#azure-functions-with-visual-studio-code)
	- [Install Azure Functions Core Tools](#install-azure-functions-core-tools)
	- [Docker](#docker)
	- [Install Azure SQL Edge with Docker](#install-azure-sql-edge-with-docker)
		- [Learn more about Azure SQL Edge](#learn-more-about-azure-sql-edge)
		- [Learn about Docker persistent storage volumes](#learn-about-docker-persistent-storage-volumes)
		- [Create Docker Data Volume](#create-docker-data-volume)
		- [Start Azure SQL Edge](#start-azure-sql-edge)
		- [Azure SQL Management Tools](#azure-sql-management-tools)
			- [Windows only (Full featured)](#windows-only-full-featured)
			- [Cross platform Linux, macOS, Windows (Lighter weight)](#cross-platform-linux-macos-windows-lighter-weight)
		- [SQL Server Samples Databases](#sql-server-samples-databases)
		- [SQL Edge ONNX Tutorial](#sql-edge-onnx-tutorial)
		- [Microsoft SQL Server Extension for Visual Studio Code](#microsoft-sql-server-extension-for-visual-studio-code)
	- [Install MySql](#install-mysql)
	- [Installing Anaconda Distribution 5](#installing-anaconda-distribution-5)
	- [Tensorflow](#tensorflow)
		- [Python Support](#python-support)
		- [Installing locally with nVidia GPU support](#installing-locally-with-nvidia-gpu-support)
		- [NVIDIA Container Runtime for Docker](#nvidia-container-runtime-for-docker)
		- [Microsoft Cognitive Toolkit](#microsoft-cognitive-toolkit)
		- [With nVidia CPU Support](#with-nvidia-cpu-support)
	- [Postman](#postman)
	- [Fiddler](#fiddler)
	- [VirtualBox](#virtualbox)
	- [Azure IoT Hub Explorer](#azure-iot-hub-explorer)
	- [Azure IoT Edge](#azure-iot-edge)
	- [Building ARM Docker Images from an x64 Ubuntu Host](#building-arm-docker-images-from-an-x64-ubuntu-host)
	- [Fritzing](#fritzing)
	- [Useful Utilities](#useful-utilities)
		- [grub customizer](#grub-customizer)
		- [Onedrive Support](#onedrive-support)
		- [Windows 10 Stick Notes on the Web](#windows-10-stick-notes-on-the-web)
		- [Gnome Tweak](#gnome-tweak)

This guide assumes you have some experience with Linux and you will open Terminal and Ctrl-Shift-V to paste in [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) commands.

**Feel free to contribute to this guide.**

## Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com/) is a must have IDE, open source, extensible, great language, debugging and tooling support.  

Head to [Visual Studio Code](https://code.visualstudio.com/) and download the .deb file for Debian and Ubuntu then install with QApt Package Installer.

---

## Useful apps

### Utilities

```bash
sudo apt install neofetch htop
```

### C/C++ Development

```bash
sudo apt install build-essential gdb cmake 
```

---

## Visual Studio Extensions

There are a stack of great extensions for Visual Studio Code. These are the ones that I find most useful.

1. Azure Account, Azure Functions, Azure CLI Tools, Azure Event Hub Explorer, Azure Cosmos DB, Azure IoT Edge, Azure IoT Toolkit, SQL Server, C#, Docker, Python, C/C++, JSON Tools, JSON Escaper, Powershell, Azure Application Insights, Azure App Services, Arduino, Azure Resource Manager Tools, Azure Storage, Tools for AI, Markdown TOC, Code Spell Checker, Docker, Docs Authoring Pack, and more...

---

## GitHub Client

Before you can commit any changes against GitHub you'll need to configure who you are.

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

---

## Installing the latest .NET Core SDK


1. Snap install .NET Core 5

	```bash
	sudo snap install dotnet-sdk --classic --channel=5.0
	sudo snap alias dotnet-sdk.dotnet dotnet
	sudo ln -sv /snap/dotnet-sdk/current/dotnet /usr/local/bin/dotnet
	```

2. Confirm successful installation of .NET Core SDK

```bash
dotnet --version
```

References:

* Install the latest release of the [.NET Core SDK](https://docs.microsoft.com/en-gb/dotnet/core/install/linux-ubuntu)
* https://github.com/OmniSharp/omnisharp-vscode/issues/4201


---

## Azure Storage Explorer

[How to install Microsoft Azure Storage Explorer
on Ubuntu](https://snapcraft.io/install/storage-explorer/ubuntu)

---

## Azure Storage Emulator

Install [Azurite](https://github.com/azure/azurite), a lightweight server clone of Azure Blob, Queue, and Table Storage that simulates most of the commands supported by it with minimal dependencies.

```bash
docker run -p 10000:10000 -p 10001:10001 mcr.microsoft.com/azure-storage/azurite
```

Notes.
* [Configure Azure Storage connection strings](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)
* [Connect to the emulator account using the well-known account name and key](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#connect-to-the-emulator-account-using-the-well-known-account-name-and-key)

---

## Azure CLI (Command Line Interface)

Be sure that 'curl' is installed.

```bash
sudo apt install curl
```

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

[Install Azure CLI 2.0 with apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest)

---

## Azure Functions with Visual Studio Code

[Code and test Azure Functions locally](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)

[Azure Functions Core Tools (note updated instructions for Ubuntu 18.04)](https://github.com/Azure/azure-functions-core-tools/blob/master/README.md)

---

## Install Azure Functions Core Tools

As at August 2018 see [Install the Azure Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local#linux)

````bash
cd ~/Downloads && \
sudo apt install curl -y

curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-get update

sudo apt-get install azure-functions-core-tools

````

---

## Docker

```bash
sudo apt -y install docker.io && sudo usermod -aG docker $USER
```

Enable the docker service to start after reboot.

```bash
sudo systemctl enable docker.service
```

Followed with system reboot.

---

## Install Azure SQL Edge with Docker

### Learn more about Azure SQL Edge

[Azure SQL Edge documentation](https://docs.microsoft.com/en-us/azure/azure-sql-edge/)

### Learn about Docker persistent storage volumes

[Docker Containers Tutorial – Persistent Storage Volumes and Stateful Containers](http://www.ethernetresearch.com/docker/docker-tutorial-persistent-storage-volumes-and-stateful-containers/)

### Create Docker Data Volume

Create a new persistent storage volume in the Host Machine.

```bash
docker volume create azure-sql-edge-data
```

Inspect the storage volume to get more detailed information.

```bash
docker volume inspect azure-sql-edge-data
```

Check the data in the storage volume

```bash
sudo ls /var/lib/docker/volumes/azure-sql-edge-data/_data
```

Remove a docker data volume

```bash
 docker volume rm azure-sql-edge-data
```

### Start Azure SQL Edge

```bash
docker run --cap-add SYS_PTRACE -e 'ACCEPT_EULA=1' -e 'MSSQL_SA_PASSWORD=<Your password>' --restart always -p 1433:1433 --name azuresqledge  -v azure-sql-edge-data:/var/opt/mssql -d mcr.microsoft.com/azure-sql-edge
```

### Azure SQL Management Tools

#### Windows only (Full featured)

[SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15)

#### Cross platform Linux, macOS, Windows (Lighter weight)

[Azure Data Studio](https://docs.microsoft.com/en-us/sql/azure-data-studio/what-is?view=sql-server-ver15)

### SQL Server Samples Databases

Northwind is a great starting point

[Northwind and pubs sample databases for Microsoft SQL Server](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)

### SQL Edge ONNX Tutorial

[Machine learning and AI with ONNX in SQL Edge](https://docs.microsoft.com/en-us/azure/azure-sql-edge/onnx-overview)


### Microsoft SQL Server Extension for Visual Studio Code

[Use Visual Studio Code to create and run Transact-SQL scripts for SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-vscode?view=sql-server-linux-2017)

---

## Install MySql

[Docker Containers Tutorial – Persistent Storage Volumes and Stateful Containers](http://www.ethernetresearch.com/docker/docker-tutorial-persistent-storage-volumes-and-stateful-containers/)

Create a new persistent storage volume in the Host Machine.

```bash
docker volume create mysql-data
```

Inspect the storage volume to get more detailed information.

```bash
docker volume inspect mysql-data
```

Check the data in the storage volume

```bash
sudo ls /var/lib/docker/volumes/mysql-data/_data
```

```bash
docker run --name mysql1 -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_HOST=% -e MYSQL_ROOT_PASSWORD="<Your Password>" --restart always -p 3306:3306 -d mysql/mysql-server
```

---


## Installing Anaconda Distribution 5

It is a free, easy-to-install package manager, environment manager and Python distribution with a collection of 1,000+ open source packages with free community support. Anaconda is platform-agnostic, so you can use it whether you are on Windows, macOS or Linux.

[Installing Anaconda on Linux](https://docs.anaconda.com/anaconda/install/linux)

Create an Anaconda Navigator Desktop Resource

```bash
mkdir -p ~/.local/share/applications && \
cat > ~/.local/share/applications/anaconda-navigator.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Anaconda
Exec=/home/dave/anaconda3/bin/anaconda-navigator
Icon=/home/dave/anaconda3/lib/python3.6/site-packages/anaconda_navigator/static/images/anaconda-icon-256x256.png
Terminal=false
Type=Application
Categories=Development;
EOL
```

Notes.

1. [Anaconda Cheat Sheet](https://docs.anaconda.com/_downloads/Anaconda-Starter-Guide-Cheat-Sheet.pdf)
2. [How to check your Anaconda version and updating](https://medium.com/@mauridb/how-to-check-your-anaconda-version-c092400c9978)
3. [Stop Installing Tensorflow using pip for performance sake!](https://towardsdatascience.com/stop-installing-tensorflow-using-pip-for-performance-sake-5854f9d9eb0c)

---

## Tensorflow

### Python Support

If you want Tensorflow with GPU support for use with Python then by far the easiest way to install is with Anaconda as it will install the complete CUDA toolkit and cuDNN library into your selected environment. But note, this is community supported, and not officially supported.

1. Create the Anaconda environment

    This would create a Anaconda environment with tensorflow-gpu support (requires an tensorflow capable nVida GPU, alternatively specify tersorflow-cpu), targeting Python 3.5, plus adds pylint useful in Visual Studio Code, and Jupyter Notebook support.

    ```bash
    conda create -n <envName> python=3.5 tensorflow-gpu pylint scipy jupyter requests scikit-learn
    ```

2. Activate the Anaconda environment

    Activate the Anaconda environment

    ```bash
    source activate <envName>
    ```

3. Deactivate an Anaconda Environment

    ```bash
    source deactivate
    ```

    Anaconda Navigator is the easiest way to manage Anaconda environments and launch environments.

    ```bash
    anaconda-navigator
    ```

4. Create your Python Project, open it with Visual Studio Code add a python file and select the Tensorflow environment you just created.

### Installing locally with nVidia GPU support

See 

1. [Installing Tensorflow GPU on Ubuntu 18.04 LTS](https://medium.com/@taylordenouden/installing-tensorflow-gpu-on-ubuntu-18-04-89a142325138)
2. [Installing Tensorlow, using pip in Anaconda](https://www.tensorflow.org/install/install_linux#InstallingAnaconda)


```bash
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.10.1-cp35-cp35m-linux_x86_64.whl pylint scipy
```

---

### NVIDIA Container Runtime for Docker

If your PC has a nVidia GPU and you want to developer with  Docker and TensorFlow-GPU support. Simpler than installing CUDA Driver and Toolkit on to local system.

![](https://cloud.githubusercontent.com/assets/3028125/12213714/5b208976-b632-11e5-8406-38d379ec46aa.png)

Notes.

1. [Using TensorFlow via Docker](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/docker/README.md)
2. [NVIDIA Container Runtime for Docker](https://github.com/NVIDIA/nvidia-docker)


### Microsoft Cognitive Toolkit

For information on setting up [CNTK Docker Containers](https://docs.microsoft.com/en-us/cognitive-toolkit/CNTK-Docker-Containers).

### With nVidia CPU Support

1. Ensure the [NVIDIA Container Runtime for Docker](https://github.com/nvidia/nvidia-docker) is installed.

    ```bash
    nvidia-docker run -d -p 8888:8888 --name cntk-jupyter-notebooks -t microsoft/cntk
    ```

2. Start Jupyter Notebook server in your Docker container:

    ```bash
    docker exec -it cntk-jupyter-notebooks bash -c "source /cntk/activate-cntk && jupyter-notebook --no-browser --port=8888 --ip=0.0.0.0 --notebook-dir=/cntk/Tutorials --allow-root"
    ```

---

## Postman

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

---

## Fiddler

See [Use Fiddler in Ubuntu](https://medium.com/@rajsek/use-fiddler-in-ubuntu-82b1dfd80848)

---

## VirtualBox

```bash
sudo apt-get install virtualbox
```

---

## Azure IoT Hub Explorer

[Microsoft Azure IoT extension for Azure CLI](https://github.com/Azure/azure-iot-cli-extension)

```bash
az extension add --name azure-iot
```

[az iot Command Guide](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-iot-ext/iot?view=azure-cli-latest)

Example IoT Hub command

```bash
az iot hub monitor-events --hub-name IotHubName
```

Notes.

* [Installing and using iothub-explorer](https://github.com/Azure/iothub-explorer)
* [Microsoft Azure IoT Extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md)


---

## Azure IoT Edge

* [Develop and deploy a C# IoT Edge module to your simulated device - preview](https://docs.microsoft.com/en-us/azure/iot-edge/tutorial-csharp-module)

---

## Building ARM Docker Images from an x64 Ubuntu Host

If you are targeting ARM for your Docker builds then you will need to run the following command before you do your Docker build.

```bash
docker run --rm --privileged multiarch/qemu-user-static:register --reset
```

Notes.

* If your docker ARM base image is already built to include QEMU then register QEMU in the build agent as follows.
* Otherwise follow the instruction on [How to Build ARM Docker Images on Intel host](http://www.hotblackrobotics.com/en/blog/2018/01/22/docker-images-arm/)

---

## Fritzing

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

---

## Useful Utilities

### grub customizer

[How to Install Grub Customizer](http://ubuntuhandbook.org/index.php/2018/10/install-grub-customizer-5-1-0-ubuntu-18-10/)

### Onedrive Support

[How To Mount OneDrive In Linux Using Rclone](https://www.linuxuprising.com/2018/07/how-to-mount-onedrive-in-linux-using.html)

### Windows 10 Stick Notes on the Web

[Access Windows 10 Sticky Notes via your browser - very handy for casual note taking](https://www.onenote.com/stickynotes)

### Gnome Tweak

[Gnome Tweak Tool](https://linuxconfig.org/how-to-install-tweak-tool-on-ubuntu-18-04-bionic-beaver-linux)

