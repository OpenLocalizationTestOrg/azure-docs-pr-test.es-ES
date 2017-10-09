---
title: "aaaDeploy y administrar copias de seguridad para las máquinas virtuales de Azure mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy y administrar copias de seguridad de Azure con PowerShell."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Usar AzureRM.Backup cmdlets tooback las máquinas virtuales
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Clásico](backup-azure-vms-classic-automation.md)
>
>

Este artículo muestra cómo toouse Azure PowerShell para copias de seguridad y recuperación de máquinas virtuales de Azure. Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: Resource Manager y el clásico. Este artículo incluye el uso de modelo de implementación de hello clásico tooback el almacén de copia de seguridad de datos tooa. Si no ha creado un almacén de copia de seguridad en su suscripción, vea la versión del Administrador de recursos de Hola de este artículo, [tooback de cmdlets de uso AzureRM.RecoveryServices.Backup las máquinas virtuales](backup-azure-vms-automation.md). Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

> [!IMPORTANT]
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell. **El 1 de noviembre de 2017**:
>- Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

## <a name="concepts"></a>Conceptos
Este artículo proporciona la información específica toohello cmdlets de PowerShell usa tooback las máquinas virtuales. Para ver una introducción a la protección de máquinas virtuales de Azure, consulte [Planeación de la infraestructura de copia de seguridad de máquinas virtuales en Azure](backup-azure-vms-introduction.md).

> [!NOTE]
> Antes de empezar, lea hello [requisitos previos](backup-azure-vms-prepare.md) toowork necesario con copia de seguridad de Azure y hello [limitaciones](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) de solución de copia de seguridad de máquina virtual actual Hola.
>
>

toouse PowerShell tomar de hecho, una jerarquía de hello toounderstand del momento de objetos y desde dónde toostart.

![Jerarquía de objetos](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Hola dos flujos más importantes se habilita la protección de una máquina virtual y restaurar los datos de un punto de recuperación. enfoque de Hola de este artículo es toohelp que esté acostumbrados a trabajar con tooenable de cmdlets de PowerShell de hello estos dos escenarios.

## <a name="setup-and-registration"></a>Instalación y registro
toobegin:

1. [Descargue la versión de PowerShell más reciente](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es: 1.0.0)
2. Encontrar Hola cmdlets de PowerShell de copia de seguridad de Azure disponibles, escriba Hola siguiente comando:

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

Hello siguiente configuración y tareas de registro pueden automatizarse con PowerShell:

* Creación de un almacén de copia de seguridad
* Registrar hello las máquinas virtuales con hello servicio de copia de seguridad de Azure

### <a name="create-a-backup-vault"></a>Creación de un almacén de copia de seguridad
> [!WARNING]
> Para los clientes mediante copia de seguridad de Azure Hola primera vez, deberá toobe de proveedor de copia de seguridad de Azure tooregister Hola usado con su suscripción. Puede hacerlo ejecutando el siguiente comando de hello: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"
>
>

Puede crear un nuevo almacén de copia de seguridad mediante hello **AzureRmBackupVault New** cmdlet. almacén de copia de seguridad de Hello es un recurso ARM, por lo que necesita tooplace dentro de un grupo de recursos. En una consola de Azure PowerShell con privilegios elevados, ejecute hello siguientes comandos:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Puede obtener una lista de todos los almacenes de copia de seguridad de hello en una suscripción determinada utilizando hello **AzureRmBackupVault Get** cmdlet.

> [!NOTE]
> Es objeto de almacén de copia de seguridad de hello toostore adecuada en una variable. objeto de almacén de Hola se necesita como entrada para muchos de los cmdlets de copia de seguridad de Azure.
>
>

### <a name="registering-hello-vms"></a>Registrar hello las máquinas virtuales
primer paso de Hola para configurar copias de seguridad con copias de seguridad de Azure es tooregister su máquina o máquina virtual con un almacén de copia de seguridad de Azure. Hola **AzureRmBackupContainer Register** cmdlet toma Hola información de entrada de una máquina virtual de IaaS de Azure y lo registra con el almacén especificado Hola. operación de registro de Hello asocia Hola máquina virtual de Azure con el almacén de copia de seguridad de Hola y pistas Hola VM a través del ciclo de vida de copia de seguridad de Hola.

Al registrar la máquina virtual con hello servicio de copia de seguridad de Azure, crea un objeto contenedor de nivel superior. Un contenedor normalmente contiene varios elementos que pueden ser una copia, pero en caso de hello de máquinas virtuales, habrá un único elemento de copia de seguridad para el contenedor de Hola.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Copias de seguridad de máquinas virtuales de Azure
### <a name="create-a-protection-policy"></a>Creación de una directiva de protección
No es obligatorio toocreate una nueva protección directiva toostart copia de seguridad de las máquinas virtuales. almacén de Hello viene con una "directiva predeterminada" que pueden ser utilizados tooquickly habilitar la protección y, a continuación, editar más adelante con detalles de la derecha Hola. Puede obtener una lista de directivas de hello disponibles en el almacén de hello mediante hello **AzureRmBackupProtectionPolicy Get** cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> zona horaria de Hello del campo de BackupTime hello en PowerShell es UTC. Sin embargo, cuando se muestre la hora de copia de seguridad de Hola Hola portal de Azure, zona horaria hello es sistema local de tooyour alineado junto con el desplazamiento de UTC de Hola.
>
>

Una directiva de copia de seguridad está asociada con al menos una directiva de retención. Directiva de retención de Hello define cuánto tiempo se conserva un punto de recuperación con copia de seguridad de Azure. Hola **AzureRmBackupRetentionPolicy New** crea objetos de PowerShell que contienen información de la directiva de retención. Estos objetos de directiva de retención se usan las entradas toohello *New-AzureRmBackupProtectionPolicy* cmdlet, o directamente con hello *AzureRmBackupProtection Enable* cmdlet.

Una directiva de copia de seguridad define cuándo y con qué frecuencia hello realizar copia de seguridad de un elemento. Hola **AzureRmBackupProtectionPolicy New** cmdlet crea un objeto de PowerShell que contiene información de la directiva de copia de seguridad. Hello directiva de copia de seguridad sirve como una entrada toohello *AzureRmBackupProtection Enable* cmdlet.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Habilitar protección
Habilitar la protección implica dos objetos: hello elemento y Hola directiva y ambos toohello de toobelong necesidad mismo del almacén. Una vez asociado con el elemento de hello directiva hello, flujo de trabajo de copia de seguridad de hello activará programación definida Hola.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>Copia de seguridad inicial
programación de copia de seguridad de Hola se encargará de hacer copia inicial completa de hello para el elemento de Hola y copia incremental de Hola para copias de seguridad posteriores Hola. Sin embargo, si desea que tooforce Hola inicial copia de seguridad toohappen en un momento determinado o incluso inmediatamente, a continuación, usar hello **AzureRmBackupItem de copia de seguridad** cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> Hola de zona horaria de hello StartTime y campos de hora de finalización se muestra en PowerShell es UTC. Sin embargo, cuando se muestra información similar de hello en hello portal de Azure, zona horaria de hello es el reloj del sistema local de tooyour alineado.
>
>

### <a name="monitoring-a-backup-job"></a>Supervisión de trabajos de copia de seguridad
La mayor parte de las operaciones de ejecución prolongada en Azure Backup se modelan como un trabajo. Esto hace fácil tootrack progreso sin necesidad de hello tookeep abierto de portal de Azure en todo momento.

estado más reciente de hello tooget de un trabajo en curso, use hello **AzureRmBackupJob Get** cmdlet.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

En lugar de sondear estos trabajos de finalización, que es código innecesario, adicional, resulta más sencillo Hola toouse **AzureRmBackupJob espera** cmdlet. Cuando se utiliza en una secuencia de comandos, Hola cmdlet pausará ejecución Hola hasta que finaliza el trabajo de Hola u Hola especificado se alcanza el valor de tiempo de espera.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Restauración de máquinas virtuales de Azure
Datos de pedidos toorestore copia de seguridad, necesita tooidentify Hola copia elementos y punto de recuperación de Hola que contiene los datos de punto en el tiempo de Hola. Esta información es proporcionada toohello AzureRmBackupItem restauración cmdlet tooinitiate una restauración de datos de la cuenta del cliente de hello almacén toohello.

### <a name="select-hello-vm"></a>Seleccione Hola VM
objeto de PowerShell de hello tooget que identifica Hola elemento derecha copia de seguridad, se necesita toostart de hello contenedor en el almacén de Hola y el camino hacia abajo de la jerarquía de objetos de trabajo. contenedor de hello tooselect que representa la máquina virtual, use Hola Hola **Get AzureRmBackupContainer** cmdlet y canalice dicha toohello **AzureRmBackupItem Get** cmdlet.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Elección de un punto de recuperación
Ahora puede enumerar todos los puntos de recuperación de Hola para elemento de copia de seguridad de hello utilizando hello **AzureRmBackupRecoveryPoint Get** cmdlet y elija toorestore de punto de recuperación de Hola. Normalmente los usuarios seleccionar más reciente de hello *AppConsistent* punto en la lista de Hola.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

variable de Hello ```$rp``` es una matriz de puntos de recuperación para hello seleccionado el elemento de copia de seguridad, ordenado en orden inverso de tiempo: punto de recuperación más reciente de hello está en el índice 0. Usar indización de punto de recuperación de hello toopick estándar matriz de PowerShell. Por ejemplo: ```$rp[0]``` seleccionará el punto de recuperación más reciente de Hola.

### <a name="restoring-disks"></a>Restauración de discos
Hay una diferencia clave entre las operaciones de restauración de hello realiza a través de hello portal de Azure y Azure PowerShell. Con PowerShell, la operación de restauración de Hola se detiene en restaurar discos hello y la información de configuración de punto de recuperación de Hola. No crea máquinas virtuales.

> [!WARNING]
> Hola AzureRmBackupItem de restauración no crea una máquina virtual. Solo restaura discos hello toohello la cuenta de almacenamiento especificada. Esto es no Hola mismo comportamiento experimentará Hola portal de Azure.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

Puede obtener detalles de Hola Hola de operación de restauración mediante hello **AzureRmBackupJobDetails Get** cmdlet una vez que ha completado el trabajo de restauración de Hola. Hola *ErrorDetails* propiedad disponen de información de hello necesarios toorebuild Hola máquina virtual.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Compilar Hola VM
Hola creación VM fuera de los discos de hello restaurar puede hacerse con los cmdlets de PowerShell de administración de servicio de Azure anteriores hello, Hola nuevas plantillas de Azure Resource Manager, o incluso con hello portal de Azure. En un ejemplo rápido, le mostraremos cómo tooget allí mediante cmdlets de administración de servicios de Azure Hola.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Para obtener más información sobre la restauración de discos toobuild una máquina virtual desde hello, lea acerca de hello siguientes cmdlets:

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Ejemplos de código
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. Obtener estado de finalización de Hola de subtareas de trabajo
estado de finalización de hello tootrack de subtareas individuales, puede usar hello **AzureRmBackupJobDetails Get** cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Crear un informe diario o semanal de los trabajos de copia de seguridad
Normalmente, los administradores deseen tooknow qué trabajos de copia de seguridad que se ejecutaron en hello últimas 24 horas, el estado de Hola de esos trabajos de copia de seguridad. Además, cantidad Hola de datos transferidos ofrece a los administradores una manera tooestimate uso mensual de sus datos. script de Hola siguiente extrae los datos sin procesar de Hola de hello servicio de copia de seguridad de Azure y muestra información de hello en la consola de PowerShell de Hola.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

Si desea tooadd gráficos de resultados del informe toothis capacidades, obtenga información acerca de la entrada de blog de TechNet de hello [gráficos con PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Pasos siguientes
Si prefiere usar PowerShell tooengage con los recursos de Azure, consulte el artículo de PowerShell de Hola para proteger Windows Server, [implementar y administrar copia de seguridad para Windows Server](backup-client-automation-classic.md). También hay un artículo de PowerShell sobre cómo administrar las copias de seguridad DPM: [Implementación y administración de copias de seguridad en Azure para servidores de Data Protection Manager (DPM) con PowerShell](backup-dpm-automation-classic.md). Estos dos artículos tienen una versión para las implementaciones de Resource Manager, así como las implementaciones clásicas.
