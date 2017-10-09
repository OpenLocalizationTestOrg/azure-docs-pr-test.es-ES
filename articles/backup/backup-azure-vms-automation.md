---
title: "aaaDeploy y administrar las copias de seguridad para las máquinas virtuales implementadas por el Administrador de recursos mediante PowerShell | Documentos de Microsoft"
description: "Usar PowerShell toodeploy y administrar las copias de seguridad de Azure para máquinas virtuales implementadas por el Administrador de recursos"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Usar AzureRM.RecoveryServices.Backup cmdlets tooback las máquinas virtuales
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Clásico](backup-azure-vms-classic-automation.md)
>
>

Este artículo muestra cómo tooback de cmdlets de PowerShell de Azure toouse seguridad y recuperar una máquina virtual Azure (VM) de servicios de recuperación de un almacén. Un almacén de servicios de recuperación es un recurso de Azure Resource Manager y tooprotect usa datos y los activos de los servicios de copia de seguridad de Azure y Azure Site Recovery. Puede usar un tooprotect de almacén de servicios de recuperación máquinas virtuales implementadas por el Administrador de servicios de Azure y máquinas virtuales implementadas por el Administrador de recursos de Azure.

> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo es para su uso con máquinas virtuales creadas mediante el modelo de administrador de recursos de Hola.
>
>

Este artículo le guiará a través mediante PowerShell tooprotect una máquina virtual y restaurar datos desde un punto de recuperación.

## <a name="concepts"></a>Conceptos
Si no está familiarizado con hello servicio de copia de seguridad de Azure, para obtener información general del servicio de hello, visite [¿qué es la copia de seguridad de Azure?](backup-introduction-to-azure-backup.md) Antes de empezar, asegúrese de que cubren essentials Hola sobre hello toowork de requisitos previos necesarios con copia de seguridad de Azure y, Hola limitaciones de la solución de copia de seguridad de máquina virtual actual Hola.

toouse PowerShell de forma eficaz, es necesario toounderstand jerarquía de Hola de objetos y desde dónde toostart.

![Jerarquía de objetos de Recovery Services](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

Hola tooview referencia de cmdlets de AzureRm.RecoveryServices.Backup PowerShell, vea hello [copia de seguridad de Azure: Cmdlets de servicios de recuperación](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) Hola biblioteca de Azure.

## <a name="setup-and-registration"></a>Instalación y registro
toobegin:

1. [Descargar la versión más reciente de Hola de PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (Hola versión mínima necesaria es: 1.4.0)
2. Encontrar Hola cmdlets de PowerShell de copia de seguridad de Azure disponibles, escriba Hola siguiente comando:

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


Hola siguiente las tareas se puede automatizar con PowerShell:

* Creación de un almacén de Recovery Services
* Copia de seguridad de máquinas virtuales de Azure
* Desencadenamiento de un trabajo de copia de seguridad
* Supervisión de un trabajo de copia de seguridad
* Restauración de máquinas virtuales de Azure

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Servicios de recuperación
Hola pasos le guiará en el proceso de creación de un almacén de servicios de recuperación. Un almacén de Servicios de recuperación no es lo mismo que un almacén de copia de seguridad.

1. Si utilizas Azure Backup para hello primera vez, debe usar hello  **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister el proveedor de servicios de recuperación de Azure de hello con su suscripción.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hola almacén de servicios de recuperación es un recurso de administrador de recursos, por lo que necesita tooplace dentro de un grupo de recursos. Puede usar un grupo de recursos existente o crear un grupo de recursos con hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet. Al crear un grupo de recursos, especifique el nombre de Hola y ubicación para el grupo de recursos de Hola.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Hola de uso  **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate Hola del almacén de servicios de recuperación. Asegúrese de toospecify Hola misma ubicación para el almacén de Hola que utilizó para el grupo de recursos de Hola.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Especificar tipo de Hola de toouse de redundancia de almacenamiento; Puede usar [almacenamiento redundante local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [almacenamiento con redundancia geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello en el ejemplo siguiente se muestra hello - BackupStorageRedundancy opción testvault está establecida tooGeoRedundant.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Muchos de los cmdlets de copia de seguridad de Azure requieren el objeto de almacén de servicios de recuperación de hello como entrada. Por este motivo, resulta toostore conveniente Hola el objeto de almacén de servicios de recuperación de copia de seguridad en una variable.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Almacenes de Hola de vista en una suscripción
Use  **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview lista de Hola de todos los almacenes en la suscripción actual de Hola. Puede usar este toocheck de comando que ha creado un nuevo almacén o toosee Hola almacenes disponibles en la suscripción de Hola.

Ejecutar comandos de hello, Get-AzureRmRecoveryServicesVault, tooview todos los almacenes de credenciales en la suscripción de Hola. Hello en el ejemplo siguiente se muestra información de hello muestra para cada almacén.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a>Copia de seguridad de máquinas virtuales de Azure
Usar un tooprotect de almacén de servicios de recuperación de las máquinas virtuales. Antes de aplicar la protección de hello, establecer contexto de almacén de hello (tipo de saludo de los datos protegidos en el almacén de hello) y compruebe la directiva de protección de Hola. Directiva de protección de Hello es la programación de hello cuando ejecutan trabajos de copia de seguridad de Hola y cuánto tiempo se conserva cada instantánea de copia de seguridad.

### <a name="set-vault-context"></a>Establecer el contexto de almacén
Antes de habilitar la protección en una máquina virtual, use  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contexto de almacén de tooset Hola. Una vez que se establece el contexto de almacén de hello, aplica tooall posteriores cmdlets. Hello en el ejemplo siguiente se establece Hola de contexto de almacén para el almacén de hello, *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Creación de una directiva de protección
Cuando se crea un almacén de Recovery Services, este incluye las directivas de retención y protección predeterminadas. Directiva de protección predeterminado de Hello desencadena un trabajo de copia de seguridad cada día a una hora especificada. Directiva de retención predeterminada Hola conserva el punto de recuperación diarios de Hola durante 30 días. Puede usar predeterminado de hello tooquickly directiva proteger la máquina virtual y editar Directiva de hello más tarde con distintos detalles.

Use  **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview directivas de protección de hello en el almacén de Hola. Puede usar este cmdlet tooget una directiva específica, o directivas de hello tooview asociada a un tipo de carga de trabajo. Hola siguiente ejemplo obtiene las directivas para el tipo de carga de trabajo, AzureVM.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> zona horaria de Hello del campo de BackupTime hello en PowerShell es UTC. Sin embargo, cuando se muestre la hora de copia de seguridad de Hola Hola portal de Azure, tiempo de hello es zona horaria local de tooyour ajustada.
>
>

Una directiva de protección de copia de seguridad está asociada con al menos una directiva de retención. La directiva de retención define el tiempo que se conserva el punto de recuperación antes de que se elimine. Use  **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  directiva de retención predeterminada tooview Hola.  Del mismo modo puede usar  **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  directiva al programar tooobtain Hola de forma predeterminada. Hola  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet crea un objeto de PowerShell que contiene información de la directiva de copia de seguridad. Hello objetos de directiva de retención y programación se usan las entradas toohello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet. Hello en el ejemplo siguiente se almacena directiva al programar hello y directiva de retención de hello en variables. ejemplo de Hola use esos parámetros de Hola de toodefine de variables cuando se crea una directiva de protección, *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Habilitar protección
Una vez haya definido la directiva de copia de seguridad de protección de hello, todavía debe habilitar Directiva de Hola para un elemento. Use  **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable protección. Habilitar la protección requiere dos objetos - elemento de Hola y la directiva de Hola. Una vez que se ha asociado con el almacén de Hola directiva hello, flujo de trabajo de copia de seguridad de Hola se desencadena en tiempo de hello definido en la programación de la directiva de Hola.

Hola siguiendo en el ejemplo se habilita la protección Hola elemento, V2VM, mediante la directiva de hello, NewPolicy. protección de hello tooenable en las máquinas virtuales del Administrador de recursos sin cifrar

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

protección de hello tooenable en cifrado máquinas virtuales (cifradas mediante BEK y KEK), deberá claves tooread de permiso de servicio de copia de seguridad de Azure de toogive hello y secretos del almacén de claves.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

protección de hello tooenable en cifrado máquinas virtuales (cifradas solo mediante BEK), deberá toogive hello Azure Backup service permiso tooread los secretos del almacén de claves.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> Si utilizas una nube de Azure Government hello, utilice Hola valor ff281ffe-705c-4f53-9f37-a40e6f2c68f3 para el parámetro hello **- ServicePrincipalName** en [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .
>
>

Para máquinas virtuales clásicas

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Modificación de una directiva de protección
Directiva de protección de hello toomodify, use [AzureRmRecoveryServicesBackupProtectionPolicy conjunto](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy o RetentionPolicy objetos.

Hello en el ejemplo siguiente se cambia Hola recuperación punto retención too365 días.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Desencadenar una copia de seguridad
Puede usar  **[AzureRmRecoveryServicesBackupItem de copia de seguridad](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger un trabajo de copia de seguridad. Si no copia de seguridad inicial de hello, es una copia de seguridad completa. Las sucesivas copias de seguridad toman una copia incremental. Ser seguro toouse  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexto de almacén de hello antes de activar el trabajo de copia de seguridad de Hola. Hola siguiente ejemplo se da por supuesto que se ha establecido el contexto de almacén.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> zona horaria de Hola de campos de StartTime y EndTime hello en PowerShell es UTC. Sin embargo, cuando se muestre el tiempo de Hola Hola portal de Azure, tiempo de hello es zona horaria local de tooyour ajustada.
>
>

## <a name="monitoring-a-backup-job"></a>Supervisión de trabajos de copia de seguridad
Puede supervisar las operaciones de ejecución prolongada, como los trabajos de copia de seguridad, sin usar Hola portal de Azure. estado de hello tooget de un trabajo en curso, use hello  **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet. Este cmdlet obtiene los trabajos de copia de seguridad de Hola para un depósito concreto y ese almacén se especifica en el contexto de almacén de Hola. Hello en el ejemplo siguiente se obtiene el estado de saludo de un trabajo en curso como una matriz y almacena el estado de hello en la variable de hello $joblist.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

En lugar de sondeo estos trabajos de finalización, que es necesario código adicional, use hello  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet. Este cmdlet detiene la ejecución de hello hasta que finaliza el trabajo de Hola u Hola especificado se alcanza el valor de tiempo de espera.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Restauración de máquinas virtuales de Azure
Hay una diferencia clave entre Hola restaurar una máquina virtual usando Hola portal de Azure y restaurar una máquina virtual mediante PowerShell. Con PowerShell, operación de restauración de hello es completa, una vez creados los discos de Hola y la información de configuración de punto de recuperación de Hola.

> [!NOTE]
> operación de restauración de Hello no crea una máquina virtual.
>
>

toocreate una máquina virtual desde el disco, consulte la sección de hello, [Hola crear VM desde discos almacenados](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). pasos básicos de Hello toorestore una VM de Azure son:

* Seleccione Hola VM
* Elección de un punto de recuperación
* Restaurar discos Hola
* Crear Hola máquina virtual a partir de discos almacenados

Hello gráfico siguiente muestra la jerarquía de objetos de Hola de hello RecoveryServicesVault hacia abajo toohello BackupRecoveryPoint.

![Jerarquía de objetos de Recovery Services donde se muestra BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

datos de copia de seguridad de toorestore, identificar elementos de copia de seguridad de Hola y punto de recuperación de Hola que contiene datos de punto en el tiempo de saludo. Hola de uso  **[restauración AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cuenta del cliente de toohello del almacén de datos de toorestore de cmdlet de Hola.

### <a name="select-hello-vm"></a>Seleccione Hola VM
objeto de PowerShell de hello tooget que identifica Hola derecha copia de seguridad de elemento, iniciar desde el contenedor de hello en el almacén de Hola y Examinar hacia abajo de la jerarquía de objetos de Hola. contenedor de hello tooselect que representa la máquina virtual, use Hola Hola  **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet y canalice dicha toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Elección de un punto de recuperación
Hola de uso  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist cmdlet puntos de recuperación todos para elemento de copia de seguridad de Hola. A continuación, elija toorestore de punto de recuperación de Hola. Si no está seguro de qué toouse de punto de recuperación, es una buena práctica toochoose Hola RecoveryPointType más reciente = AppConsistent punto en la lista de Hola.

En la siguiente secuencia de comandos de hello, Hola variable, **$rp**, es una matriz de puntos de recuperación para saludo seleccionado elemento copia de seguridad, de hello últimos siete días. matriz de Hola se ordena en orden inverso de tiempo con el punto de recuperación más reciente de hello en el índice 0. Usar indización de punto de recuperación de hello toopick estándar matriz de PowerShell. En el ejemplo de Hola, $rp [0] selecciona el punto de recuperación más reciente de Hola.

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a>Restaurar discos Hola
Hola de uso  **[restauración AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore cmdlet datos del elemento que realiza una copia de seguridad y configuración tooa puntos de recuperación. Una vez que haya identificado un punto de recuperación, usarlo como valor de Hola para hello **- RecoveryPoint** parámetro. En el código de ejemplo anterior de hello, **$rp [0]** era toouse de punto de recuperación de Hola. En el siguiente código de ejemplo de Hola **$rp [0]** es hello toouse de punto de recuperación para restaurar el disco de Hola.

información de configuración y discos de Hola toorestore:

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Hola de uso  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait de cmdlet para toocomplete de trabajo de restauración de Hola.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Cuando haya completado el trabajo de restauración de hello, usar hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  detalles de hello tooget los cmdlets del programa Hola a la operación de restauración. Hola JobDetails propiedad tiene toorebuild necesarios Hola VM de hello información.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

Una vez que restaurar discos hello, vaya Hola de toocreate de sección toohello siguiente máquina virtual.

## <a name="create-a-vm-from-restored-disks"></a>Creación de una máquina virtual a partir de discos restaurados
Después de haber restaurado discos hello, utilice estos toocreate pasos y configurar la máquina virtual de Hola desde el disco.

> [!NOTE]
> toocreate cifrar las máquinas virtuales desde los discos restaurados, su rol de Azure debe tener la acción de permiso tooperform hello, **Microsoft.KeyVault/vaults/deploy/action**. Si su rol no tiene este permiso, cree un rol personalizado con esta acción. Para obtener más información, vea [Roles personalizados en RBAC de Azure](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Hola consulta restaura propiedades de disco para obtener detalles de trabajo de Hola.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Establecer contexto de almacenamiento de Azure de Hola y restaurar el archivo de configuración de JSON de Hola.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Utilice Hola JSON configuración archivo toocreate Hola VM configuración.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Adjuntar el disco del sistema operativo de Hola y discos de datos. Dependiendo de las máquinas virtuales de configuración de hello, haga clic en hello vínculo correspondiente tooview respectivos cmdlets: 
    - [Máquinas virtuales no administrados, sin cifrar](#non-managed-non-encrypted-vms)
    - [Máquinas virtuales no administrados y cifradas (sólo BEK)](#non-managed-encrypted-vms-bek-only)
    - [Máquinas virtuales no administrados y cifradas (BEK y KEK)](#non-managed-encrypted-vms-bek-and-kek)
    - [Máquinas virtuales administradas, sin cifrar](#managed-non-encrypted-vms)
    - [Cifradas máquinas virtuales administradas (BEK y KEK)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>Máquinas virtuales no administradas y no cifradas

    Usar hello según muestra para máquinas virtuales no administrado, sin cifrar.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>Máquinas virtuales cifradas no administradas (solo BEK)

    Para VM no administrados y cifradas (cifradas solo mediante BEK), necesita el almacén de claves secretas toohello toorestore Hola para poderla adjuntar discos. Para obtener más información, consulte el artículo de hello, [restaurar una máquina virtual cifrada desde un punto de recuperación de copia de seguridad de Azure](backup-azure-restore-key-secret.md). Hola siguiente ejemplo muestra cómo tooattach OS y discos de datos para cifran las máquinas virtuales.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>Máquinas virtuales cifradas no administradas (BEK y KEK)

    Para VM no administrados y cifradas (cifradas mediante BEK y KEK), necesitará toorestore clave de Hola y almacén de claves secretas toohello para poderla adjuntar discos. Para obtener más información, consulte el artículo de hello, [restaurar una máquina virtual cifrada desde un punto de recuperación de copia de seguridad de Azure](backup-azure-restore-key-secret.md). Hola siguiente ejemplo muestra cómo tooattach OS y discos de datos para cifran las máquinas virtuales.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a>Máquinas virtuales administradas y no cifradas

    Administrado sin cifrar las máquinas virtuales, podrá necesita toocreate administra los discos del almacenamiento de blobs y, a continuación, adjuntar discos Hola. Para obtener información detallada, vea el artículo de hello [adjuntar un tooa de disco de datos VM de Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hola siguiendo el ejemplo de código muestra cómo tooattach Hola discos de datos para las máquinas virtuales sin cifrar administradas.

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>Máquinas virtuales cifradas administradas (BEK y KEK)

    Administrado cifrados las máquinas virtuales (cifrada mediante BEK y KEK), podrá necesita toocreate administra los discos del almacenamiento de blobs y, a continuación, adjuntar discos Hola. Para obtener información detallada, vea el artículo de hello [adjuntar un tooa de disco de datos VM de Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hello código de ejemplo siguiente muestra cómo tooattach Hola discos de datos para máquinas virtuales cifradas administradas.

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. Configuración de red Hola.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Crear la máquina virtual de Hola.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Pasos siguientes
Si prefiere toouse PowerShell tooengage con los recursos de Azure, consulte el artículo de PowerShell de hello, [implementar y administrar copia de seguridad para Windows Server](backup-client-automation.md). Si administra las copias de seguridad DPM, consulte el artículo de hello, [implementar y administrar copias de seguridad de DPM](backup-dpm-automation.md). Estos dos artículos tienen una versión para las implementaciones de Resource Manager y las clásicas.  
