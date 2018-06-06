## Powershell for Linux

 See [Installing PowerShell Core on Linux](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-powershell-core-on-linux?view=powershell-6)

Install Azure Powershell module.

```bash
sudo pwsh -Command Install-Module AzureRM.NetCore
```


To start Powershell

```bash
pwsh
```


[Install and configure Azure PowerShell on macOS and Linux](https://docs.microsoft.com/en-us/powershell/azure/install-azurermps-maclinux?view=azurermps-6.1.0)

In summary

```Powershell
Install-Module AzureRM.NetCore
Import-Module AzureRM.Netcore
Import-Module AzureRM.Profile.Netcore
```

Test Azure Powershell Module

```
Connect-AzureRmAccount
```


Add

Be sure to add the Powershell extension in Visual Studio Code.

Notes.


4. [Powershell Releases](https://github.com/PowerShell/PowerShell/releases/tag/v6.1.0-preview.2)
