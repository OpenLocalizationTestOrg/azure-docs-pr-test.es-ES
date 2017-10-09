# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Errores comunes durante clásico tooAzure migración del Administrador de recursos
Los catálogos de este artículo Hola más comunes de los errores y las mitigaciones durante la migración de Hola de recursos de IaaS de pila de Azure Resource Manager de toohello de modelo de implementación clásico de Azure.

## <a name="list-of-errors"></a>Lista de errores
| Cadena de error | Mitigación |
| --- | --- |
| Error interno del servidor |En algunos casos, se trata de un error transitorio que desaparece con un reintento. Si continúa toopersist, [póngase en contacto con soporte técnico de Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) como sea necesario, investigación de registros de la plataforma. <br><br> **Nota:** una vez que se realiza un seguimiento de equipo de soporte técnico de Hola de incidente de hello, no intente cualquier reducción automática que esto podría tener consecuencias no deseadas en su entorno. |
| No se admite la migración para la implementación {nombre de implementación} en HostedService {nombre del servicio hospedado} porque es una implementación PaaS (web/trabajo). |Esto sucede cuando una implementación contiene un rol web o de trabajo. Dado que solo se admite la migración de máquinas virtuales, quite consolidado Hola de implementación de Hola y reintente la migración. |
| Error de implementación de plantilla {nombre de plantilla}. CorrelationId={guid} |En hello back-end del servicio de migración, se usan recursos de Azure Resource Manager plantillas toocreate en pila de hello Azure Resource Manager. Puesto que las plantillas son idempotentes, normalmente sin ningún riesgo puede reintentar hello tooget de operación de migración más allá de este error. Si este error persiste toopersist, inicie [póngase en contacto con soporte técnico de Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) y asígneles Hola CorrelationId. <br><br> **Nota:** una vez que se realiza un seguimiento de equipo de soporte técnico de Hola de incidente de hello, no intente cualquier reducción automática que esto podría tener consecuencias no deseadas en su entorno. |
| red virtual de Hola {que virtual-network-name} no existe. |Esto puede ocurrir si ha creado Hola red Virtual en el nuevo portal de Azure Hola. nombre de red Virtual real Hola sigue el patrón de Hola "grupo * <VNET name>" |
| La máquina virtual {nombre de la máquina virtual} de HostedService {nombre del servicio hospedado} contiene la extensión {nombre de la extensión} que no se admite en Azure Resource Manager. Se recomienda toouninstall desde Hola VM antes de continuar con la migración. |Las extensiones XML como BGInfo 1.* no se admiten en Azure Resource Manager. Por lo tanto, no se pueden migrar estas extensiones. Si estas extensiones son izquierdo Hola instalados en virtual machine, se desinstalan automáticamente antes de completar la migración de Hola. |
| La máquina virtual {nombre de la máquina virtual} de HostedService {nombre del servicio hospedado} contiene la extensión VMSnapshot/VMSnapshotLinux que actualmente no se admite para migración. Desinstale de hello VM y agregarlo de nuevo mediante Azure Resource Manager después de completar Hola migración |Se trata de un escenario de Hola donde se configura la máquina virtual de Hola para copia de seguridad de Azure. Puesto que es actualmente un escenario no compatible, siga solución hello en https://aka.ms/vmbackupmigration |
| Máquina virtual {vm-name} en HostedService {hospedado-service-name} contiene extensión {nombre de extensión} cuyo estado no se está informando de hello máquina virtual. Por lo tanto, esta máquina virtual no se puede migrar. Asegúrese de que se está notificando que el estado de extensión de Hola o desinstalación Hola de hello VM y vuelva a intentar la migración. <br><br> La máquina virtual {nombre de la máquina virtual} en HostedService {nombre del servicio hospedado} contiene la extensión {nombre de la extensión} que notifica el estado del controlador: {estado del controlador}. Por lo tanto, no se pueden migrar Hola máquina virtual. Asegúrese de que se notifica el estado de controlador de extensión de hello es {estado del controlador} o desinstalarlo de hello VM y vuelva a intentar la migración. <br><br> Agente de máquina virtual para la máquina virtual {vm-name} en HostedService {hospedado-service-name} está informando Hola estado general del agente como no preparada. Por lo tanto, Hola VM puede no se migran, si tiene una extensión de migrable. Asegúrese de que ese agente de máquina virtual de hello es informar del estado de agente global como listo. Consulte toohttps://aka.ms/classiciaasmigrationfaqs. |Agente de invitado de Azure & extensiones de máquina virtual necesitan saliente internet access toohello VM almacenamiento cuenta toopopulate su estado. Entre las causas comunes del error de estado se incluyen: <li> un grupo de seguridad que bloquea el acceso de salida toohello internet <li> Si Hola red virtual tiene servidores DNS local y se pierde la conectividad DNS <br><br> Si continúa toosee un estado no compatible, puede desinstalar Hola extensiones tooskip esta comprobación y continuar con la migración. |
| No se admite la migración para la implementación {nombre de implementación} en HostedService {nombre del servicio hospedado} porque tiene varios conjuntos de disponibilidad. |Actualmente, solo se pueden migrar los servicios hospedados que tengan como mucho un conjunto de disponibilidad. toowork resolver este problema, mueva Hola adicional conjuntos de disponibilidad y servicio hospedado en máquinas virtuales en esas tooa de conjuntos de disponibilidad diferente. |
| No se admite la migración para la implementación {deployment-name} en HostedService {hospedado-service-name porque tiene máquinas virtuales que no forman parte del conjunto de disponibilidad de hello aunque hello HostedService contiene uno. |solución de Hola para este escenario es tooeither mover todas las máquinas virtuales de hello en la disponibilidad de una sola establecer o quitar todas las máquinas virtuales de hello que conjunto de disponibilidad en el servicio de hello hospedado. |
| Cuenta de almacenamiento/HostedService/Virtual red {que virtual-network-name} está en proceso de Hola de migrarse y por lo tanto, no se puede cambiar |Este error se produce cuando Hola "Preparación" la operación de migración se ha completado en el recurso de Hola y se desencadena una operación que podría hacer que un recurso de toohello de cambio. Debido a bloqueo de hello en el plano de la administración de hello después de la operación de "Preparación", se bloquean los recursos de toohello de cambios. plano de administración de hello toounlock, puede ejecutar Hola "Confirmar" operación toocomplete migración u Hola "Anular" migración operación tooroll volver Hola operación de "Preparación". |
| No se permite la migración para HostedService {nombre del servicio hospedado} porque tiene una máquina virtual {nombre de la máquina virtual} en estado: RoleStateUnknown. Se permite la migración solo al Hola máquina virtual está en uno de los siguientes Hola Estados - ejecución, detenido, se cancela la asignación de detenido. |Hello VM posible que se está llevando a cabo a través de una transición de estado, que normalmente se produce cuando durante una operación de actualización en hello servicio hospedado, como reiniciar el equipo, instalar la extensión etcetera. Se recomienda para toocomplete de operación de actualización de hello en hello HostedService antes de intentar la migración. |
| Implementación {deployment-name} en {hospedado-service-name} HostedService contiene una máquina virtual {vm-name} con el disco de datos {nombre de disco de datos} cuyos bytes de tamaño {size-of-the-vhd-blob-backing-the-data-disk} del blob físico no coincide con {de tamaño lógico de disco de datos de la máquina virtual de Hola bytes Size-of-the-Data-Disk-Specified-in-the-VM-API}. Migración continuará sin especificar un tamaño de disco de datos de Hola para hello VM de Azure Resource Manager. | Este error se produce si ha cambiado el tamaño del blob de disco duro virtual de hello sin actualizar el tamaño de hello en el modelo de la API de VM de Hola. [A continuación](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes), se describen los pasos de mitigación detallados.|
| Se produjo una excepción de almacenamiento durante la validación de datos de un disco {nombre de disco de datos} con el vínculo multimedia {URI de disco de datos} para la máquina virtual {nombre de máquina virtual} en el servicio en la nube {nombre del servicio en la nube}. Asegúrese de que ese vínculo de medios de disco duro virtual de hello es accesible para esta máquina virtual | Este error puede ocurrir si los discos de Hola de hello VM que se haya eliminado o ya no es accesible. Asegúrese de seguro discos Hola Hola existe la máquina virtual.|
| La máquina virtual {vm-name} de HostedService {cloud-service-name} contiene un disco con MediaLink {vhd-uri} que tiene un nombre de blob {vhd-blob-name} que no se admite en Azure Resource Manager. | Este error se produce cuando el nombre hello de blob de hello tiene un "/" en lo que no se admite actualmente en el proveedor de recursos de proceso. |
| No se permite la migración para la implementación {deployment-name} en HostedService {cloud-service-name} porque no está en ámbito regional Hola. Consulte toohttp://aka.ms/regionalscope para mover este ámbito de tooregional de implementación. | En 2014, Azure anunció que se moverán el recursos de red de un ámbito de tooregional de ámbito de nivel de clúster. Vea [http://aka.ms/regionalscope] para obtener más detalles (http://aka.ms/regionalscope). Este error se produce cuando la implementación de Hola que se está migrando no se ha realizado una operación de actualización, que automáticamente lo mueve tooa de ámbito regional. Solución recomendada es tooeither agregar una máquina virtual de punto de conexión tooa o datos toohello VM de disco y, a continuación, vuelva a intentar la migración. <br> Vea [cómo tooset extremos en una máquina virtual de Windows clásica en Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) o [conectar una máquina de virtual datos disco tooa Windows creada con el modelo de implementación clásica de Hola](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Mitigaciones detalladas

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>Máquina virtual con el disco de datos cuyo física blob de bytes de tamaño no coincide con los bytes de tamaño lógico de disco de datos de la máquina virtual de Hola.

Esto sucede cuando hello tamaño lógico de disco de datos puede dejan de estar sincronizado con el tamaño del blob de disco duro virtual real de Hola. Esto puede comprobar fácilmente por mediante Hola siguientes comandos:

#### <a name="verifying-hello-issue"></a>Comprobar el problema de Hola

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Mitigar el problema de Hola

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Mover VM tooa otra suscripción después de completar la migración

Después de completar el proceso de migración de hello, puede que desee suscripción tooanother de toomove Hola máquina virtual. Sin embargo, si tiene un certificado de secreto en hello mover la máquina virtual que se hace referencia a un recurso de almacén de claves, hello actualmente no se admite. Hola instrucciones a continuación le permitirá problema de hello tooworkaround. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>CLI de Azure 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
