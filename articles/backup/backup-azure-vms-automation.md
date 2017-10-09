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
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="0281e-103">Usar AzureRM.RecoveryServices.Backup cmdlets tooback las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="0281e-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0281e-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0281e-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="0281e-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="0281e-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="0281e-106">Este artículo muestra cómo tooback de cmdlets de PowerShell de Azure toouse seguridad y recuperar una máquina virtual Azure (VM) de servicios de recuperación de un almacén.</span><span class="sxs-lookup"><span data-stu-id="0281e-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="0281e-107">Un almacén de servicios de recuperación es un recurso de Azure Resource Manager y tooprotect usa datos y los activos de los servicios de copia de seguridad de Azure y Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0281e-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="0281e-108">Puede usar un tooprotect de almacén de servicios de recuperación máquinas virtuales implementadas por el Administrador de servicios de Azure y máquinas virtuales implementadas por el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0281e-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="0281e-109">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0281e-110">Este artículo es para su uso con máquinas virtuales creadas mediante el modelo de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="0281e-111">Este artículo le guiará a través mediante PowerShell tooprotect una máquina virtual y restaurar datos desde un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0281e-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="0281e-112">Conceptos</span><span class="sxs-lookup"><span data-stu-id="0281e-112">Concepts</span></span>
<span data-ttu-id="0281e-113">Si no está familiarizado con hello servicio de copia de seguridad de Azure, para obtener información general del servicio de hello, visite [¿qué es la copia de seguridad de Azure?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="0281e-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="0281e-114">Antes de empezar, asegúrese de que cubren essentials Hola sobre hello toowork de requisitos previos necesarios con copia de seguridad de Azure y, Hola limitaciones de la solución de copia de seguridad de máquina virtual actual Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="0281e-115">toouse PowerShell de forma eficaz, es necesario toounderstand jerarquía de Hola de objetos y desde dónde toostart.</span><span class="sxs-lookup"><span data-stu-id="0281e-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Jerarquía de objetos de Recovery Services](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="0281e-117">Hola tooview referencia de cmdlets de AzureRm.RecoveryServices.Backup PowerShell, vea hello [copia de seguridad de Azure: Cmdlets de servicios de recuperación](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) Hola biblioteca de Azure.</span><span class="sxs-lookup"><span data-stu-id="0281e-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="0281e-118">Instalación y registro</span><span class="sxs-lookup"><span data-stu-id="0281e-118">Setup and Registration</span></span>
<span data-ttu-id="0281e-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="0281e-119">toobegin:</span></span>

1. <span data-ttu-id="0281e-120">[Descargar la versión más reciente de Hola de PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (Hola versión mínima necesaria es: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="0281e-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="0281e-121">Encontrar Hola cmdlets de PowerShell de copia de seguridad de Azure disponibles, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0281e-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="0281e-122">Hola siguiente las tareas se puede automatizar con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0281e-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="0281e-123">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="0281e-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="0281e-124">Copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="0281e-124">Back up Azure VMs</span></span>
* <span data-ttu-id="0281e-125">Desencadenamiento de un trabajo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="0281e-125">Trigger a backup job</span></span>
* <span data-ttu-id="0281e-126">Supervisión de un trabajo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="0281e-126">Monitor a backup job</span></span>
* <span data-ttu-id="0281e-127">Restauración de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="0281e-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="0281e-128">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="0281e-128">Create a recovery services vault</span></span>
<span data-ttu-id="0281e-129">Hola pasos le guiará en el proceso de creación de un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0281e-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="0281e-130">Un almacén de Servicios de recuperación no es lo mismo que un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0281e-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="0281e-131">Si utilizas Azure Backup para hello primera vez, debe usar hello  **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister el proveedor de servicios de recuperación de Azure de hello con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="0281e-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="0281e-132">Hola almacén de servicios de recuperación es un recurso de administrador de recursos, por lo que necesita tooplace dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0281e-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="0281e-133">Puede usar un grupo de recursos existente o crear un grupo de recursos con hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0281e-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="0281e-134">Al crear un grupo de recursos, especifique el nombre de Hola y ubicación para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="0281e-135">Hola de uso  **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate Hola del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0281e-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="0281e-136">Asegúrese de toospecify Hola misma ubicación para el almacén de Hola que utilizó para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="0281e-137">Especificar tipo de Hola de toouse de redundancia de almacenamiento; Puede usar [almacenamiento redundante local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [almacenamiento con redundancia geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="0281e-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="0281e-138">Hello en el ejemplo siguiente se muestra hello - BackupStorageRedundancy opción testvault está establecida tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="0281e-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="0281e-139">Muchos de los cmdlets de copia de seguridad de Azure requieren el objeto de almacén de servicios de recuperación de hello como entrada.</span><span class="sxs-lookup"><span data-stu-id="0281e-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="0281e-140">Por este motivo, resulta toostore conveniente Hola el objeto de almacén de servicios de recuperación de copia de seguridad en una variable.</span><span class="sxs-lookup"><span data-stu-id="0281e-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="0281e-141">Almacenes de Hola de vista en una suscripción</span><span class="sxs-lookup"><span data-stu-id="0281e-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="0281e-142">Use  **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview lista de Hola de todos los almacenes en la suscripción actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="0281e-143">Puede usar este toocheck de comando que ha creado un nuevo almacén o toosee Hola almacenes disponibles en la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="0281e-144">Ejecutar comandos de hello, Get-AzureRmRecoveryServicesVault, tooview todos los almacenes de credenciales en la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="0281e-145">Hello en el ejemplo siguiente se muestra información de hello muestra para cada almacén.</span><span class="sxs-lookup"><span data-stu-id="0281e-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="0281e-146">Copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="0281e-146">Back up Azure VMs</span></span>
<span data-ttu-id="0281e-147">Usar un tooprotect de almacén de servicios de recuperación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0281e-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="0281e-148">Antes de aplicar la protección de hello, establecer contexto de almacén de hello (tipo de saludo de los datos protegidos en el almacén de hello) y compruebe la directiva de protección de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="0281e-149">Directiva de protección de Hello es la programación de hello cuando ejecutan trabajos de copia de seguridad de Hola y cuánto tiempo se conserva cada instantánea de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0281e-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="0281e-150">Establecer el contexto de almacén</span><span class="sxs-lookup"><span data-stu-id="0281e-150">Set vault context</span></span>
<span data-ttu-id="0281e-151">Antes de habilitar la protección en una máquina virtual, use  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contexto de almacén de tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="0281e-152">Una vez que se establece el contexto de almacén de hello, aplica tooall posteriores cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0281e-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="0281e-153">Hello en el ejemplo siguiente se establece Hola de contexto de almacén para el almacén de hello, *testvault*.</span><span class="sxs-lookup"><span data-stu-id="0281e-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="0281e-154">Creación de una directiva de protección</span><span class="sxs-lookup"><span data-stu-id="0281e-154">Create a protection policy</span></span>
<span data-ttu-id="0281e-155">Cuando se crea un almacén de Recovery Services, este incluye las directivas de retención y protección predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="0281e-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="0281e-156">Directiva de protección predeterminado de Hello desencadena un trabajo de copia de seguridad cada día a una hora especificada.</span><span class="sxs-lookup"><span data-stu-id="0281e-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="0281e-157">Directiva de retención predeterminada Hola conserva el punto de recuperación diarios de Hola durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="0281e-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="0281e-158">Puede usar predeterminado de hello tooquickly directiva proteger la máquina virtual y editar Directiva de hello más tarde con distintos detalles.</span><span class="sxs-lookup"><span data-stu-id="0281e-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="0281e-159">Use  **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview directivas de protección de hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="0281e-160">Puede usar este cmdlet tooget una directiva específica, o directivas de hello tooview asociada a un tipo de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0281e-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="0281e-161">Hola siguiente ejemplo obtiene las directivas para el tipo de carga de trabajo, AzureVM.</span><span class="sxs-lookup"><span data-stu-id="0281e-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="0281e-162">zona horaria de Hello del campo de BackupTime hello en PowerShell es UTC.</span><span class="sxs-lookup"><span data-stu-id="0281e-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="0281e-163">Sin embargo, cuando se muestre la hora de copia de seguridad de Hola Hola portal de Azure, tiempo de hello es zona horaria local de tooyour ajustada.</span><span class="sxs-lookup"><span data-stu-id="0281e-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="0281e-164">Una directiva de protección de copia de seguridad está asociada con al menos una directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="0281e-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="0281e-165">La directiva de retención define el tiempo que se conserva el punto de recuperación antes de que se elimine.</span><span class="sxs-lookup"><span data-stu-id="0281e-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="0281e-166">Use  **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  directiva de retención predeterminada tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="0281e-167">Del mismo modo puede usar  **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  directiva al programar tooobtain Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0281e-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="0281e-168">Hola  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet crea un objeto de PowerShell que contiene información de la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0281e-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="0281e-169">Hello objetos de directiva de retención y programación se usan las entradas toohello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0281e-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="0281e-170">Hello en el ejemplo siguiente se almacena directiva al programar hello y directiva de retención de hello en variables.</span><span class="sxs-lookup"><span data-stu-id="0281e-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="0281e-171">ejemplo de Hola use esos parámetros de Hola de toodefine de variables cuando se crea una directiva de protección, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="0281e-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="0281e-172">Habilitar protección</span><span class="sxs-lookup"><span data-stu-id="0281e-172">Enable protection</span></span>
<span data-ttu-id="0281e-173">Una vez haya definido la directiva de copia de seguridad de protección de hello, todavía debe habilitar Directiva de Hola para un elemento.</span><span class="sxs-lookup"><span data-stu-id="0281e-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="0281e-174">Use  **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable protección.</span><span class="sxs-lookup"><span data-stu-id="0281e-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="0281e-175">Habilitar la protección requiere dos objetos - elemento de Hola y la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="0281e-176">Una vez que se ha asociado con el almacén de Hola directiva hello, flujo de trabajo de copia de seguridad de Hola se desencadena en tiempo de hello definido en la programación de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="0281e-177">Hola siguiendo en el ejemplo se habilita la protección Hola elemento, V2VM, mediante la directiva de hello, NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="0281e-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="0281e-178">protección de hello tooenable en las máquinas virtuales del Administrador de recursos sin cifrar</span><span class="sxs-lookup"><span data-stu-id="0281e-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="0281e-179">protección de hello tooenable en cifrado máquinas virtuales (cifradas mediante BEK y KEK), deberá claves tooread de permiso de servicio de copia de seguridad de Azure de toogive hello y secretos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="0281e-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="0281e-180">protección de hello tooenable en cifrado máquinas virtuales (cifradas solo mediante BEK), deberá toogive hello Azure Backup service permiso tooread los secretos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="0281e-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="0281e-181">Si utilizas una nube de Azure Government hello, utilice Hola valor ff281ffe-705c-4f53-9f37-a40e6f2c68f3 para el parámetro hello **- ServicePrincipalName** en [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .</span><span class="sxs-lookup"><span data-stu-id="0281e-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="0281e-182">Para máquinas virtuales clásicas</span><span class="sxs-lookup"><span data-stu-id="0281e-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="0281e-183">Modificación de una directiva de protección</span><span class="sxs-lookup"><span data-stu-id="0281e-183">Modify a protection policy</span></span>
<span data-ttu-id="0281e-184">Directiva de protección de hello toomodify, use [AzureRmRecoveryServicesBackupProtectionPolicy conjunto](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy o RetentionPolicy objetos.</span><span class="sxs-lookup"><span data-stu-id="0281e-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="0281e-185">Hello en el ejemplo siguiente se cambia Hola recuperación punto retención too365 días.</span><span class="sxs-lookup"><span data-stu-id="0281e-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="0281e-186">Desencadenar una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="0281e-186">Trigger a backup</span></span>
<span data-ttu-id="0281e-187">Puede usar  **[AzureRmRecoveryServicesBackupItem de copia de seguridad](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger un trabajo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0281e-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="0281e-188">Si no copia de seguridad inicial de hello, es una copia de seguridad completa.</span><span class="sxs-lookup"><span data-stu-id="0281e-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="0281e-189">Las sucesivas copias de seguridad toman una copia incremental.</span><span class="sxs-lookup"><span data-stu-id="0281e-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="0281e-190">Ser seguro toouse  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexto de almacén de hello antes de activar el trabajo de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="0281e-191">Hola siguiente ejemplo se da por supuesto que se ha establecido el contexto de almacén.</span><span class="sxs-lookup"><span data-stu-id="0281e-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="0281e-192">zona horaria de Hola de campos de StartTime y EndTime hello en PowerShell es UTC.</span><span class="sxs-lookup"><span data-stu-id="0281e-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="0281e-193">Sin embargo, cuando se muestre el tiempo de Hola Hola portal de Azure, tiempo de hello es zona horaria local de tooyour ajustada.</span><span class="sxs-lookup"><span data-stu-id="0281e-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="0281e-194">Supervisión de trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="0281e-194">Monitoring a backup job</span></span>
<span data-ttu-id="0281e-195">Puede supervisar las operaciones de ejecución prolongada, como los trabajos de copia de seguridad, sin usar Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0281e-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="0281e-196">estado de hello tooget de un trabajo en curso, use hello  **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0281e-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="0281e-197">Este cmdlet obtiene los trabajos de copia de seguridad de Hola para un depósito concreto y ese almacén se especifica en el contexto de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="0281e-198">Hello en el ejemplo siguiente se obtiene el estado de saludo de un trabajo en curso como una matriz y almacena el estado de hello en la variable de hello $joblist.</span><span class="sxs-lookup"><span data-stu-id="0281e-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="0281e-199">En lugar de sondeo estos trabajos de finalización, que es necesario código adicional, use hello  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0281e-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="0281e-200">Este cmdlet detiene la ejecución de hello hasta que finaliza el trabajo de Hola u Hola especificado se alcanza el valor de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="0281e-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="0281e-201">Restauración de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="0281e-201">Restore an Azure VM</span></span>
<span data-ttu-id="0281e-202">Hay una diferencia clave entre Hola restaurar una máquina virtual usando Hola portal de Azure y restaurar una máquina virtual mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0281e-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="0281e-203">Con PowerShell, operación de restauración de hello es completa, una vez creados los discos de Hola y la información de configuración de punto de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="0281e-204">operación de restauración de Hello no crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0281e-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="0281e-205">toocreate una máquina virtual desde el disco, consulte la sección de hello, [Hola crear VM desde discos almacenados](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="0281e-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="0281e-206">pasos básicos de Hello toorestore una VM de Azure son:</span><span class="sxs-lookup"><span data-stu-id="0281e-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="0281e-207">Seleccione Hola VM</span><span class="sxs-lookup"><span data-stu-id="0281e-207">Select hello VM</span></span>
* <span data-ttu-id="0281e-208">Elección de un punto de recuperación</span><span class="sxs-lookup"><span data-stu-id="0281e-208">Choose a recovery point</span></span>
* <span data-ttu-id="0281e-209">Restaurar discos Hola</span><span class="sxs-lookup"><span data-stu-id="0281e-209">Restore hello disks</span></span>
* <span data-ttu-id="0281e-210">Crear Hola máquina virtual a partir de discos almacenados</span><span class="sxs-lookup"><span data-stu-id="0281e-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="0281e-211">Hello gráfico siguiente muestra la jerarquía de objetos de Hola de hello RecoveryServicesVault hacia abajo toohello BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="0281e-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Jerarquía de objetos de Recovery Services donde se muestra BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="0281e-213">datos de copia de seguridad de toorestore, identificar elementos de copia de seguridad de Hola y punto de recuperación de Hola que contiene datos de punto en el tiempo de saludo.</span><span class="sxs-lookup"><span data-stu-id="0281e-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="0281e-214">Hola de uso  **[restauración AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cuenta del cliente de toohello del almacén de datos de toorestore de cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="0281e-215">Seleccione Hola VM</span><span class="sxs-lookup"><span data-stu-id="0281e-215">Select hello VM</span></span>
<span data-ttu-id="0281e-216">objeto de PowerShell de hello tooget que identifica Hola derecha copia de seguridad de elemento, iniciar desde el contenedor de hello en el almacén de Hola y Examinar hacia abajo de la jerarquía de objetos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="0281e-217">contenedor de hello tooselect que representa la máquina virtual, use Hola Hola  **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet y canalice dicha toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0281e-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="0281e-218">Elección de un punto de recuperación</span><span class="sxs-lookup"><span data-stu-id="0281e-218">Choose a recovery point</span></span>
<span data-ttu-id="0281e-219">Hola de uso  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist cmdlet puntos de recuperación todos para elemento de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="0281e-220">A continuación, elija toorestore de punto de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="0281e-221">Si no está seguro de qué toouse de punto de recuperación, es una buena práctica toochoose Hola RecoveryPointType más reciente = AppConsistent punto en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="0281e-222">En la siguiente secuencia de comandos de hello, Hola variable, **$rp**, es una matriz de puntos de recuperación para saludo seleccionado elemento copia de seguridad, de hello últimos siete días.</span><span class="sxs-lookup"><span data-stu-id="0281e-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="0281e-223">matriz de Hola se ordena en orden inverso de tiempo con el punto de recuperación más reciente de hello en el índice 0.</span><span class="sxs-lookup"><span data-stu-id="0281e-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="0281e-224">Usar indización de punto de recuperación de hello toopick estándar matriz de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0281e-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="0281e-225">En el ejemplo de Hola, $rp [0] selecciona el punto de recuperación más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="0281e-226">Restaurar discos Hola</span><span class="sxs-lookup"><span data-stu-id="0281e-226">Restore hello disks</span></span>
<span data-ttu-id="0281e-227">Hola de uso  **[restauración AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore cmdlet datos del elemento que realiza una copia de seguridad y configuración tooa puntos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0281e-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="0281e-228">Una vez que haya identificado un punto de recuperación, usarlo como valor de Hola para hello **- RecoveryPoint** parámetro.</span><span class="sxs-lookup"><span data-stu-id="0281e-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="0281e-229">En el código de ejemplo anterior de hello, **$rp [0]** era toouse de punto de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="0281e-230">En el siguiente código de ejemplo de Hola **$rp [0]** es hello toouse de punto de recuperación para restaurar el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="0281e-231">información de configuración y discos de Hola toorestore:</span><span class="sxs-lookup"><span data-stu-id="0281e-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="0281e-232">Hola de uso  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait de cmdlet para toocomplete de trabajo de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="0281e-233">Cuando haya completado el trabajo de restauración de hello, usar hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  detalles de hello tooget los cmdlets del programa Hola a la operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="0281e-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="0281e-234">Hola JobDetails propiedad tiene toorebuild necesarios Hola VM de hello información.</span><span class="sxs-lookup"><span data-stu-id="0281e-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="0281e-235">Una vez que restaurar discos hello, vaya Hola de toocreate de sección toohello siguiente máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0281e-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="0281e-236">Creación de una máquina virtual a partir de discos restaurados</span><span class="sxs-lookup"><span data-stu-id="0281e-236">Create a VM from restored disks</span></span>
<span data-ttu-id="0281e-237">Después de haber restaurado discos hello, utilice estos toocreate pasos y configurar la máquina virtual de Hola desde el disco.</span><span class="sxs-lookup"><span data-stu-id="0281e-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="0281e-238">toocreate cifrar las máquinas virtuales desde los discos restaurados, su rol de Azure debe tener la acción de permiso tooperform hello, **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="0281e-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="0281e-239">Si su rol no tiene este permiso, cree un rol personalizado con esta acción.</span><span class="sxs-lookup"><span data-stu-id="0281e-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="0281e-240">Para obtener más información, vea [Roles personalizados en RBAC de Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="0281e-241">Hola consulta restaura propiedades de disco para obtener detalles de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="0281e-242">Establecer contexto de almacenamiento de Azure de Hola y restaurar el archivo de configuración de JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="0281e-243">Utilice Hola JSON configuración archivo toocreate Hola VM configuración.</span><span class="sxs-lookup"><span data-stu-id="0281e-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="0281e-244">Adjuntar el disco del sistema operativo de Hola y discos de datos.</span><span class="sxs-lookup"><span data-stu-id="0281e-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="0281e-245">Dependiendo de las máquinas virtuales de configuración de hello, haga clic en hello vínculo correspondiente tooview respectivos cmdlets:</span><span class="sxs-lookup"><span data-stu-id="0281e-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="0281e-246">Máquinas virtuales no administrados, sin cifrar</span><span class="sxs-lookup"><span data-stu-id="0281e-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="0281e-247">Máquinas virtuales no administrados y cifradas (sólo BEK)</span><span class="sxs-lookup"><span data-stu-id="0281e-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="0281e-248">Máquinas virtuales no administrados y cifradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="0281e-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="0281e-249">Máquinas virtuales administradas, sin cifrar</span><span class="sxs-lookup"><span data-stu-id="0281e-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="0281e-250">Cifradas máquinas virtuales administradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="0281e-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="0281e-251">Máquinas virtuales no administradas y no cifradas</span><span class="sxs-lookup"><span data-stu-id="0281e-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="0281e-252">Usar hello según muestra para máquinas virtuales no administrado, sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="0281e-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="0281e-253">Máquinas virtuales cifradas no administradas (solo BEK)</span><span class="sxs-lookup"><span data-stu-id="0281e-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="0281e-254">Para VM no administrados y cifradas (cifradas solo mediante BEK), necesita el almacén de claves secretas toohello toorestore Hola para poderla adjuntar discos.</span><span class="sxs-lookup"><span data-stu-id="0281e-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="0281e-255">Para obtener más información, consulte el artículo de hello, [restaurar una máquina virtual cifrada desde un punto de recuperación de copia de seguridad de Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="0281e-256">Hola siguiente ejemplo muestra cómo tooattach OS y discos de datos para cifran las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0281e-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="0281e-257">Máquinas virtuales cifradas no administradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="0281e-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="0281e-258">Para VM no administrados y cifradas (cifradas mediante BEK y KEK), necesitará toorestore clave de Hola y almacén de claves secretas toohello para poderla adjuntar discos.</span><span class="sxs-lookup"><span data-stu-id="0281e-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="0281e-259">Para obtener más información, consulte el artículo de hello, [restaurar una máquina virtual cifrada desde un punto de recuperación de copia de seguridad de Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="0281e-260">Hola siguiente ejemplo muestra cómo tooattach OS y discos de datos para cifran las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0281e-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="0281e-261">Máquinas virtuales administradas y no cifradas</span><span class="sxs-lookup"><span data-stu-id="0281e-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="0281e-262">Administrado sin cifrar las máquinas virtuales, podrá necesita toocreate administra los discos del almacenamiento de blobs y, a continuación, adjuntar discos Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="0281e-263">Para obtener información detallada, vea el artículo de hello [adjuntar un tooa de disco de datos VM de Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="0281e-264">Hola siguiendo el ejemplo de código muestra cómo tooattach Hola discos de datos para las máquinas virtuales sin cifrar administradas.</span><span class="sxs-lookup"><span data-stu-id="0281e-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="0281e-265">Máquinas virtuales cifradas administradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="0281e-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="0281e-266">Administrado cifrados las máquinas virtuales (cifrada mediante BEK y KEK), podrá necesita toocreate administra los discos del almacenamiento de blobs y, a continuación, adjuntar discos Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="0281e-267">Para obtener información detallada, vea el artículo de hello [adjuntar un tooa de disco de datos VM de Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="0281e-268">Hello código de ejemplo siguiente muestra cómo tooattach Hola discos de datos para máquinas virtuales cifradas administradas.</span><span class="sxs-lookup"><span data-stu-id="0281e-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="0281e-269">Configuración de red Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="0281e-270">Crear la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0281e-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="0281e-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0281e-271">Next steps</span></span>
<span data-ttu-id="0281e-272">Si prefiere toouse PowerShell tooengage con los recursos de Azure, consulte el artículo de PowerShell de hello, [implementar y administrar copia de seguridad para Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="0281e-273">Si administra las copias de seguridad DPM, consulte el artículo de hello, [implementar y administrar copias de seguridad de DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="0281e-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="0281e-274">Estos dos artículos tienen una versión para las implementaciones de Resource Manager y las clásicas.</span><span class="sxs-lookup"><span data-stu-id="0281e-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
