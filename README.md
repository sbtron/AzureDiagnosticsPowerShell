# AzureDiagnosticsPowerShell
Sample powershell scripts for Azure Diagnostics. Modified from VSO to work with generic extension version.


## Deploy-CloudService
Deploy the package output from visual studio including the diagnostics extensions.



- Will create a Service with the name -ServiceName if it doesn't exist
- *StorageAccount* is used to upload the package files as well as the diagnostics storage account if no account is specified in the diagnostics config.
- Make sure the Extensions directory is present along with the cspkg and cscfg files if you want the diagnostics config to be picked up.

e.g.

	$Svc = "<FullPathtoExtensionsFolder>"
	$StorageAccountName = "<StorageAccountName>"
	$cspkg = "<FullPathToServicePackage>.cspkg"
	$cscfg = "<FullPathToServiceConfig>.Cloud.cscfg"
	
	.\Deploy-CloudService.ps1 -ServiceName $Svc -StorageAccount $StorageAccountName -ServiceLocation "Central US" -servicePackageFile $cspkg -serviceConfigFile $cscfg -Slot "Production" -AllowUpgrade "true" -AppendDateTimeToLabel "true"

## Update-CloudServiceDiagnostics
Update an existing CloudService with new diagnostics config

- For *extensionsPath* make sure to include the Extensions sub-folder in the full path
- *StorageAccount* is used to upload the package files as well as the diagnostics storage account if no account is specified in the diagnostics config.

e.g.


	$Svc = "<FullPathtoExtensionsFolder>"
	$StorageAccountName = "<StorageAccountName>"
	$extpath = "<FullPathtoExtensionsFolder>"
	
	.\Update-CloudServiceDiagnostics.ps1 -ServiceName $Svc -StorageAccount $StorageAccountName -Slot "Production" -extensionsPath $extpath -Verbose
