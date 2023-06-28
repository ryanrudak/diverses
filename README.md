![grafik](https://github.com/ryanrudak/diverses/assets/51046918/8d1f0d4d-974a-45ab-9e3e-7b0793e014a4)# diverses
Mount-DiskImage (ISO Mounts)


Get-WindowsImage
	Get-WindowsImage -ImagePath 'C:\mediaRefresh\oldMedia\Windows 11 22H2\install.esd'


Export-WindowsImage
	Export-WindowsImage -SourceImagePath 'C:\mediaRefresh\oldMedia\Windows 11 22H2\install.esd' -SourceIndex 5 -DestinationImagePath 'C:\mediaRefresh\oldMedia\Windows 11 22H2\install_W11Pro.wim' -CheckIntegrity


Mount-WindowsImage
	Mount-WindowsImage -ImagePath C:\mediaRefresh\oldMedia\install.wim -Path C:\_Mounting -Index 1
	Mount-WindowsImage -ImagePath "C:\mediaRefresh\newMedia\Windows 10 22H2\install_W10Pro.wim" -Path C:\_Mounting -Index 1
	Mount-WindowsImage -ImagePath "C:\mediaRefresh\oldMedia\Windows 10 22H2\install_W10Pro.wim" -Path C:\_Mount -Index 1


Add-WindowsPackage
	Add-WindowsPackage -Path C:\_Mount -PackagePath 'C:\mediaRefresh\packages\2023-02 Dynamic Cumulative Update for Windows 10 Version 22H2 for x64-based Systems (KB5022834)\windows10.0-kb5022834-x64_8a1d81f6aabb9ef983de43606e319bedb7b7dd44.cab'

Add-WindowsDriver
	Add-WindowsDriver -Driver D:\updates\PV15.40.48.64.5171\Graphics\igdlh64.inf  -Path C:\_Mounting

Dismount-WindowsImage
Dismount-WindowsImage -Path C:\_Mounting -Save
Dismount-WindowsImage -Path C:\_Mount -Save -CheckIntegrity
