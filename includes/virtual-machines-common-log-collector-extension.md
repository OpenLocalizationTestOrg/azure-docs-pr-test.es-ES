
Diagnosticar problemas relacionados con un servicio de nube de Microsoft Azure requiere la recopilación de archivos de registro del servicio de hello en máquinas virtuales cuando se producen problemas de Hola. Puede usar una sola recopilación de tooperfom de hello extensión AzureLogCollector a petición de registros desde uno o más máquinas virtuales del servicio de nube (desde roles web y roles de trabajo) y transferencia Hola recopilan archivos tooan cuenta de almacenamiento de Azure, todo sin iniciar sesión en tooany de hello las máquinas virtuales.

> [!NOTE]
> Puede encontrar descripciones para la mayoría de hello registrado información en http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.
> 
> 

Hay dos modos de colección depende de los tipos de Hola de toobe archivos recopilados.

* Solo los registros del agente invitado de Azure (disponibilidad general). Este modo de recopilación incluye todos los agentes de invitado tooAzure relacionados de hello registros y otros componentes de Azure.
* Todos los registros (completo). Este modo de recopilación recopilará todos los archivos en modo GA además de:
  
  * los registros de eventos de aplicación y del sistema
  * registros de errores HTTP
  * Registros IIS
  * Registros de configuración
  * otros registros del sistema

En ambos modos de recopilación, se pueden especificar carpetas de la recopilación de datos adicionales mediante una colección de hello siguiendo la estructura:

* **Nombre**: Hola nombre de colección de hello, que se usará como nombre de saludo de la subcarpeta incluida toobe de archivo zip de Hola recogió.
* **Ubicación**: carpetas de toohello de ruta de acceso de hello en la máquina virtual de Hola donde se van a recopilar archivos.
* **SearchPattern**: patrón Hola de nombres de Hola de toobe archivos recopilados. El valor predeterminado es "*".
* **Recursiva**: si se van a archivos de hello recopilarán de forma recursiva en la carpeta de Hola.

## <a name="prerequisites"></a>Requisitos previos
* Necesitará toohave una cuenta de almacenamiento para archivos de extensión toosave genera zip.
* Asegúrese de que está usando los cmdlets de Azure PowerShell V0.8.0 o superior. Para más información, consulte [Descargas de Azure](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Agregar extensión de Hola
Puede usar [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets o [API de REST de administración de servicios](https://msdn.microsoft.com/library/ee460799.aspx) tooadd Hola extensión AzureLogCollector.

Servicios de nube, Hola cmdlet de Powershell de Azure existente, **Set-AzureServiceExtension**, puede ser usado tooenable Hola extensión en instancias de rol Servicio de nube. Cada vez que esta extensión se habilita a través de este cmdlet, recopilación de registros se desencadena en instancias de rol de hello seleccionado de los roles seleccionados.

Para máquinas virtuales, Hola cmdlet de Powershell de Azure existente, **Set-AzureVMExtension**, puede ser la extensión de hello tooenable utilizados en máquinas virtuales. Cada vez que esta extensión se habilita a través de los cmdlets de hello, recopilación de registros se desencadena en cada instancia.

Internamente, esta extensión utiliza hello PublicConfiguration basada en JSON y PrivateConfiguration. Hola aquí te mostramos diseño Hola de una muestra de JSON para la configuración pública y privada.

### <a name="publicconfiguration"></a>PublicConfiguration
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> Esta extensión no necesita la clase **privateConfiguration**. Basta con que proporcione una estructura vacía para hello **– PrivateConfiguration** argumento.
> 
> 

Puede seguir uno de dos Hola siguiendo los pasos tooadd hello AzureLogCollector tooone o más instancias de un servicio de nube o una máquina Virtual de los roles seleccionados, los desencadenadores que Hola recopilaciones en cada máquina virtual toorun y envían archivos de hello recopilan tooAzure cuenta especificado.

## <a name="adding-as-a-service-extension"></a>Agregar como extensión de servicio
1. Siga suscripción tooyour de hello instrucciones tooconnect PowerShell de Azure.
2. Especifique el nombre del servicio de hello, ranura, roles y toowhich de instancias de rol que desee tooadd y habilitar la extensión de hello AzureLogCollector.
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. Especificar la carpeta de datos adicionales de hello para el que se van a recopilar archivos (este paso es opcional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > Puede usar el token `%roleroot%` toospecify Hola unidad raíz del rol ya que no utiliza una unidad fija.
   > 
   > 
4. Proporcione el nombre de cuenta de almacenamiento de Azure de Hola y archivos de clave toowhich recopilado se cargará.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Llame a hello SetAzureServiceLogCollector.ps1 (incluido al final de hello del artículo hello) como extensión de sigue tooenable hello AzureLogCollector para un servicio de nube. Una vez que haya completado la ejecución de hello, puede encontrar Hola cargar archivos en`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

Hola aquí te mostramos definición Hola de parámetros de hello pasados toohello script. (También se copia a continuación).

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* *ServiceName*: el nombre del servicio en la nube.
* *Roles*: una lista de roles, como "WebRole1" o "WorkerRole1".
* *Instancias*: una lista de nombres de Hola de instancias de rol separados por coma: utilice la cadena de caracteres comodín de hello ("*") para todas las instancias de rol.
* *Slot*: nombre de la ranura. “Production” o “Staging”.
* *Mode*: modo de recopilación. “Full” o “GA”.
* *StorageAccountName*: nombre de la cuenta de almacenamiento de Azure para almacenar los datos recopilados.
* *StorageAccountKey*: nombre de la clave de la cuenta de almacenamiento de Azure.
* *AdditionalDataLocationList*: una lista de hello siguiente estructura:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Agregar como extensión de servicio de máquina virtual
Siga suscripción tooyour de hello instrucciones tooconnect PowerShell de Azure.

1. Especifique el nombre del servicio de hello, la VM y modo de recopilación de Hola.
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. Proporcione el nombre de cuenta de almacenamiento de Azure de Hola y archivos de clave toowhich recopilado se cargará.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Llame a hello SetAzureVMLogCollector.ps1 (incluido al final de hello del artículo hello) como extensión de sigue tooenable hello AzureLogCollector para un servicio de nube. Una vez que haya completado la ejecución de hello, puede encontrar el archivo de hello cargado en https://YouareStorageAccountName.BLOB.Core.Windows.NET/vmlogs

Hola aquí te mostramos definición Hola de parámetros de hello pasados toohello script. (También se copia a continuación).

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* ServiceName: nombre del servicio en la nube.
* Nombre de hello VMName de hello máquina virtual.
* Mode: modo de recopilación. “Full” o “GA”.
* StorageAccountName: nombre de la cuenta de almacenamiento de Azure para almacenar los datos recopilados.
* StorageAccountKey: nombre de la clave de la cuenta de almacenamiento de Azure.
* AdditionalDataLocationList: Una lista de hello siguiente estructura:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>Archivos del script de PowerShell de extensión
SetAzureServiceLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


SetAzureVMLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a>Pasos siguientes
Ahora puede examinar o copiar los registros desde una ubicación muy sencilla.

