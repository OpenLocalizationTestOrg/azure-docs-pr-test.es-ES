---
title: "Implementación y administración de copias de seguridad de máquinas virtuales implementadas con el modelo de Resource Manager mediante PowerShell | Microsoft Docs"
description: "Use PowerShell para implementar y administrar copias de seguridad de Azure para máquinas virtuales implementadas según el modelo de Resource Manager."
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
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="bb44e-103">Uso de los cmdlets AzureRM.RecoveryServices.Backup para realizar copias de seguridad de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="bb44e-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb44e-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bb44e-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="bb44e-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="bb44e-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="bb44e-106">En este artículo se muestra cómo usar cmdlets de Azure PowerShell para realizar la copia de seguridad y recuperación de una máquina virtual (VM) de Azure desde un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bb44e-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="bb44e-107">Un almacén de Recovery Services es un recurso de Azure Resource Manager y se utiliza para proteger datos y recursos en los servicios Azure Backup y Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bb44e-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="bb44e-108">Puede usar un almacén de Recovery Services para proteger máquinas virtuales implementadas según el modelo de Azure Service Manager (ASM) o según el modelo de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb44e-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="bb44e-109">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bb44e-110">La información de este artículo es para su uso con las máquinas virtuales creadas con el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb44e-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="bb44e-111">Este artículo le guiará en el uso de PowerShell para proteger una máquina virtual y restaurar datos a partir de un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bb44e-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="bb44e-112">Conceptos</span><span class="sxs-lookup"><span data-stu-id="bb44e-112">Concepts</span></span>
<span data-ttu-id="bb44e-113">Si no está familiarizado con el servicio Azure Backup, puede obtener información general al respecto en [¿Qué es Azure Backup?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="bb44e-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="bb44e-114">Antes de comenzar, asegúrese de que se tratan los aspectos fundamentales sobre los requisitos previos necesarios para trabajar con Azure Backup y las limitaciones de la solución actual de copia de seguridad de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bb44e-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="bb44e-115">Para usar PowerShell de forma eficaz, es preciso conocer la jerarquía de los objetos y desde dónde empezar.</span><span class="sxs-lookup"><span data-stu-id="bb44e-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![Jerarquía de objetos de Recovery Services](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="bb44e-117">Para ver la referencia del cmdlet de PowerShell AzureRm.RecoveryServices.Backup, vea [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) (Azure Backup: cmdlets de Recovery Services) en la biblioteca de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb44e-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="bb44e-118">Instalación y registro</span><span class="sxs-lookup"><span data-stu-id="bb44e-118">Setup and Registration</span></span>
<span data-ttu-id="bb44e-119">Para empezar:</span><span class="sxs-lookup"><span data-stu-id="bb44e-119">To begin:</span></span>

1. <span data-ttu-id="bb44e-120">[Descargue la versión más reciente de PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (la versión mínima necesaria es 1.4.0).</span><span class="sxs-lookup"><span data-stu-id="bb44e-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="bb44e-121">Para buscar los cmdlets de PowerShell para Azure Backup disponibles, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bb44e-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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


<span data-ttu-id="bb44e-122">Las siguientes tareas se pueden automatizar con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bb44e-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="bb44e-123">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="bb44e-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="bb44e-124">Copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="bb44e-124">Back up Azure VMs</span></span>
* <span data-ttu-id="bb44e-125">Desencadenamiento de un trabajo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="bb44e-125">Trigger a backup job</span></span>
* <span data-ttu-id="bb44e-126">Supervisión de un trabajo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="bb44e-126">Monitor a backup job</span></span>
* <span data-ttu-id="bb44e-127">Restauración de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="bb44e-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="bb44e-128">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="bb44e-128">Create a recovery services vault</span></span>
<span data-ttu-id="bb44e-129">Los siguientes pasos le guiarán por el proceso de creación de un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bb44e-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="bb44e-130">Un almacén de Recovery Services no es lo mismo que un almacén de Backup.</span><span class="sxs-lookup"><span data-stu-id="bb44e-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="bb44e-131">Si es la primera vez que usa Azure Backup, debe usar el cmdlet **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** para registrar el proveedor de Azure Recovery Services en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="bb44e-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="bb44e-132">El almacén de Recovery Services es un recurso de Resource Manager, por lo que deberá colocarlo dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="bb44e-133">Puede usar un grupo de recursos existente o crear uno con el cmdlet **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**.</span><span class="sxs-lookup"><span data-stu-id="bb44e-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="bb44e-134">Al crear un grupo de recursos, especifique el nombre y la ubicación.</span><span class="sxs-lookup"><span data-stu-id="bb44e-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="bb44e-135">Use el cmdlet **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** para crear el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bb44e-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="bb44e-136">Asegúrese de especificar para el almacén la misma ubicación del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="bb44e-137">Especifique el tipo de redundancia de almacenamiento que se usará: [almacenamiento con redundancia local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [almacenamiento con redundancia geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="bb44e-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="bb44e-138">En el ejemplo siguiente se muestra que la opción -BackupStorageRedundancy para testvault está establecida en GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="bb44e-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="bb44e-139">Muchos de los cmdlets de Azure Backup requieren el objeto de almacén de Recovery Services como entrada.</span><span class="sxs-lookup"><span data-stu-id="bb44e-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="bb44e-140">Por este motivo, es conveniente almacenar el objeto de almacén de Recovery Services de Backup en una variable.</span><span class="sxs-lookup"><span data-stu-id="bb44e-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="bb44e-141">Visualización de los almacenes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="bb44e-141">View the vaults in a subscription</span></span>
<span data-ttu-id="bb44e-142">Utilice **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** para ver la lista de todos los almacenes de la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="bb44e-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="bb44e-143">Puede usar este comando para comprobar que se haya creado un almacén o para ver los almacenes disponibles en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="bb44e-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="bb44e-144">Ejecute el comando Get-AzureRmRecoveryServicesVault para ver todos los almacenes de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="bb44e-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="bb44e-145">En el ejemplo siguiente se ve la información que se muestra para cada almacén.</span><span class="sxs-lookup"><span data-stu-id="bb44e-145">The following example shows the information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="bb44e-146">Copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="bb44e-146">Back up Azure VMs</span></span>
<span data-ttu-id="bb44e-147">Use un almacén de Recovery Services para proteger sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bb44e-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="bb44e-148">Antes de aplicar la protección, establezca el contexto de almacén (el tipo de datos protegido en el almacén) y compruebe la directiva de protección.</span><span class="sxs-lookup"><span data-stu-id="bb44e-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="bb44e-149">La directiva de protección consiste en la programación que indica cuándo se debe ejecutar el trabajo de copia de seguridad y cuánto tiempo se conserva cada instantánea de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bb44e-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="bb44e-150">Establecer el contexto de almacén</span><span class="sxs-lookup"><span data-stu-id="bb44e-150">Set vault context</span></span>
<span data-ttu-id="bb44e-151">Antes de habilitar la protección en una máquina virtual, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** para establecer el contexto de almacén.</span><span class="sxs-lookup"><span data-stu-id="bb44e-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="bb44e-152">Una vez que se haya establecido el contexto de almacén, se aplica a todos los cmdlets posteriores.</span><span class="sxs-lookup"><span data-stu-id="bb44e-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="bb44e-153">En el ejemplo siguiente se establece el contexto del almacén *testvault*.</span><span class="sxs-lookup"><span data-stu-id="bb44e-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="bb44e-154">Creación de una directiva de protección</span><span class="sxs-lookup"><span data-stu-id="bb44e-154">Create a protection policy</span></span>
<span data-ttu-id="bb44e-155">Cuando se crea un almacén de Recovery Services, este incluye las directivas de retención y protección predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="bb44e-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="bb44e-156">La directiva de protección predeterminada activa un trabajo de copia de seguridad cada día a la hora indicada.</span><span class="sxs-lookup"><span data-stu-id="bb44e-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="bb44e-157">La directiva de retención predeterminada conserva el punto de recuperación diario durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="bb44e-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="bb44e-158">Puede utilizar la directiva predeterminada para proteger rápidamente la máquina virtual y modificar la directiva más adelante con detalles diferentes.</span><span class="sxs-lookup"><span data-stu-id="bb44e-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="bb44e-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** para ver las directivas de protección del almacén.</span><span class="sxs-lookup"><span data-stu-id="bb44e-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="bb44e-160">Puede usar este cmdlet para obtener una directiva específica o para ver las directivas asociadas a un tipo de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bb44e-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="bb44e-161">En el ejemplo siguiente se obtienen las directivas para el tipo de carga de trabajo AzureVM.</span><span class="sxs-lookup"><span data-stu-id="bb44e-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="bb44e-162">La zona horaria del campo BackupTime en PowerShell es UTC.</span><span class="sxs-lookup"><span data-stu-id="bb44e-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="bb44e-163">Sin embargo, cuando el tiempo de copia de seguridad se muestra en Azure Portal, la hora se ajusta a la zona horaria local.</span><span class="sxs-lookup"><span data-stu-id="bb44e-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="bb44e-164">Una directiva de protección de copia de seguridad está asociada con al menos una directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="bb44e-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="bb44e-165">La directiva de retención define el tiempo que se conserva el punto de recuperación antes de que se elimine.</span><span class="sxs-lookup"><span data-stu-id="bb44e-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="bb44e-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** para ver la directiva de retención predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bb44e-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="bb44e-167">Del mismo modo, puede usar **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** para obtener la directiva de programación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bb44e-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="bb44e-168">El cmdlet **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** crea un objeto de PowerShell que contiene información de la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bb44e-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="bb44e-169">Los objetos de directiva de retención y programación se usan como entradas para el cmdlet **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**.</span><span class="sxs-lookup"><span data-stu-id="bb44e-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="bb44e-170">En el ejemplo siguiente se almacenan la directiva de programación y la directiva de retención en variables.</span><span class="sxs-lookup"><span data-stu-id="bb44e-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="bb44e-171">En el ejemplo se usan esas variables para definir los parámetros al crear la directiva de protección *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="bb44e-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="bb44e-172">Habilitar protección</span><span class="sxs-lookup"><span data-stu-id="bb44e-172">Enable protection</span></span>
<span data-ttu-id="bb44e-173">Una vez que haya definido la directiva de protección de copia de seguridad, todavía debe habilitar la directiva para un elemento.</span><span class="sxs-lookup"><span data-stu-id="bb44e-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="bb44e-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** para habilitar la protección.</span><span class="sxs-lookup"><span data-stu-id="bb44e-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="bb44e-175">Para habilitar la protección son necesarios dos objetos: el elemento y la directiva.</span><span class="sxs-lookup"><span data-stu-id="bb44e-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="bb44e-176">Después de que la directiva se haya asociado con el almacén, el flujo de trabajo de copia de seguridad se desencadena a la hora definida en la programación de la directiva.</span><span class="sxs-lookup"><span data-stu-id="bb44e-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="bb44e-177">En el ejemplo siguiente se habilita la protección para el elemento V2VM mediante la directiva NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="bb44e-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="bb44e-178">Procedimiento para habilitar la protección de máquinas virtuales de Resource Manager sin cifrar</span><span class="sxs-lookup"><span data-stu-id="bb44e-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="bb44e-179">Para habilitar la protección de máquinas virtuales cifradas (mediante BEK y KEK), debe conceder permiso al servicio Azure Backup para que lea las claves y los secretos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="bb44e-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="bb44e-180">Para habilitar la protección en máquinas virtuales cifradas (cifradas solo mediante BEK), debe conceder permiso al servicio Azure Backup para que lea los secretos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="bb44e-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="bb44e-181">Si está usando la nube de Azure Government, use el valor ff281ffe-705c-4f53-9f37-a40e6f2c68f3 para el parámetro **-ServicePrincipalName** en el cmdlet [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy).</span><span class="sxs-lookup"><span data-stu-id="bb44e-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="bb44e-182">Para máquinas virtuales clásicas</span><span class="sxs-lookup"><span data-stu-id="bb44e-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="bb44e-183">Modificación de una directiva de protección</span><span class="sxs-lookup"><span data-stu-id="bb44e-183">Modify a protection policy</span></span>
<span data-ttu-id="bb44e-184">Para modificar la directiva de protección, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) para modificar los objetos SchedulePolicy o RetentionPolicy.</span><span class="sxs-lookup"><span data-stu-id="bb44e-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="bb44e-185">En el ejemplo siguiente se cambia la retención del punto de recuperación a 365 días.</span><span class="sxs-lookup"><span data-stu-id="bb44e-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="bb44e-186">Desencadenar una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="bb44e-186">Trigger a backup</span></span>
<span data-ttu-id="bb44e-187">Puede usar **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** para desencadenar un trabajo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bb44e-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="bb44e-188">Si se trata de la copia de seguridad inicial, es una copia de seguridad completa.</span><span class="sxs-lookup"><span data-stu-id="bb44e-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="bb44e-189">Las sucesivas copias de seguridad toman una copia incremental.</span><span class="sxs-lookup"><span data-stu-id="bb44e-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="bb44e-190">Asegúrese de usar **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** para establecer el contexto de almacén antes de desencadenar el trabajo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bb44e-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="bb44e-191">En el siguiente ejemplo se da por supuesto que se ha establecido el contexto de almacén.</span><span class="sxs-lookup"><span data-stu-id="bb44e-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="bb44e-192">La zona horaria de los campos de StartTime y EndTime en PowerShell es UTC.</span><span class="sxs-lookup"><span data-stu-id="bb44e-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="bb44e-193">Sin embargo, cuando la hora se muestra en Azure Portal, esta se ajusta a la zona horaria local.</span><span class="sxs-lookup"><span data-stu-id="bb44e-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="bb44e-194">Supervisión de trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="bb44e-194">Monitoring a backup job</span></span>
<span data-ttu-id="bb44e-195">Puede supervisar las operaciones de ejecución prolongada, como los trabajos de copia de seguridad, sin usar Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bb44e-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="bb44e-196">Para obtener el estado de un trabajo en curso, use el cmdlet **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="bb44e-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="bb44e-197">Este cmdlet obtiene los trabajos de copia de seguridad de un almacén específico, y dicho almacén se especifica en el contexto de almacén.</span><span class="sxs-lookup"><span data-stu-id="bb44e-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="bb44e-198">En el ejemplo siguiente se obtiene el estado de un trabajo en curso como una matriz y se almacena el estado en la variable $joblist.</span><span class="sxs-lookup"><span data-stu-id="bb44e-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="bb44e-199">En lugar de sondear si estos trabajos han finalizado (lo que supone un código adicional innecesario), use el cmdlet **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="bb44e-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="bb44e-200">Este cmdlet detiene la ejecución hasta que el trabajo se complete o se alcance el valor de tiempo de espera especificado.</span><span class="sxs-lookup"><span data-stu-id="bb44e-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="bb44e-201">Restauración de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="bb44e-201">Restore an Azure VM</span></span>
<span data-ttu-id="bb44e-202">Hay una diferencia clave entre restaurar una máquina virtual mediante Azure Portal y hacerlo con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb44e-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="bb44e-203">Con PowerShell, la operación de restauración se completa una vez que se creen los discos y la información de configuración a partir del punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bb44e-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="bb44e-204">La operación de restauración no crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb44e-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="bb44e-205">Para crear una máquina virtual desde el disco, vea la sección sobre la [creación de la máquina virtual a partir de los discos almacenados](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="bb44e-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="bb44e-206">Los pasos básicos para restaurar una máquina virtual de Azure son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="bb44e-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="bb44e-207">Selección de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bb44e-207">Select the VM</span></span>
* <span data-ttu-id="bb44e-208">Elección de un punto de recuperación</span><span class="sxs-lookup"><span data-stu-id="bb44e-208">Choose a recovery point</span></span>
* <span data-ttu-id="bb44e-209">Restauración de los discos</span><span class="sxs-lookup"><span data-stu-id="bb44e-209">Restore the disks</span></span>
* <span data-ttu-id="bb44e-210">Creación de la máquina virtual a partir de los discos almacenados</span><span class="sxs-lookup"><span data-stu-id="bb44e-210">Create the VM from stored disks</span></span>

<span data-ttu-id="bb44e-211">En el siguiente gráfico se muestra la jerarquía de objetos desde RecoveryServicesVault hasta BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="bb44e-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![Jerarquía de objetos de Recovery Services donde se muestra BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="bb44e-213">Para restaurar los datos de una copia de seguridad, identifique el elemento del que se realizó la copia de seguridad y el punto de recuperación que contiene los datos de un momento específico.</span><span class="sxs-lookup"><span data-stu-id="bb44e-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="bb44e-214">Use el cmdlet **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** para restaurar los datos del almacén en la cuenta del cliente.</span><span class="sxs-lookup"><span data-stu-id="bb44e-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="bb44e-215">Selección de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bb44e-215">Select the VM</span></span>
<span data-ttu-id="bb44e-216">Para obtener el objeto de PowerShell que identifica el elemento de copia de seguridad correcto, comience en el contenedor del almacén y avance hacia abajo por la jerarquía de objetos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="bb44e-217">Para seleccionar el contenedor que representa la máquina virtual, use el cmdlet **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** y canalícelo al cmdlet **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**.</span><span class="sxs-lookup"><span data-stu-id="bb44e-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="bb44e-218">Elección de un punto de recuperación</span><span class="sxs-lookup"><span data-stu-id="bb44e-218">Choose a recovery point</span></span>
<span data-ttu-id="bb44e-219">Use el cmdlet **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** para enumerar todos los puntos de recuperación del elemento de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bb44e-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="bb44e-220">Después, elija el punto de recuperación que se debe restaurar.</span><span class="sxs-lookup"><span data-stu-id="bb44e-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="bb44e-221">Si no está seguro de qué punto de recuperación debe usar, se recomienda elegir el punto RecoveryPointType = AppConsistent más reciente de la lista.</span><span class="sxs-lookup"><span data-stu-id="bb44e-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="bb44e-222">En el siguiente script, la variable **$rp**es una matriz de puntos de recuperación para el elemento de copia de seguridad seleccionado de los últimos siete días.</span><span class="sxs-lookup"><span data-stu-id="bb44e-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="bb44e-223">La matriz se ordena en orden inverso de tiempo con el punto de recuperación más reciente en el índice 0.</span><span class="sxs-lookup"><span data-stu-id="bb44e-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="bb44e-224">Use la indexación de matrices de PowerShell estándar para seleccionar el punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bb44e-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="bb44e-225">En el ejemplo, $rp[0] selecciona el último punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bb44e-225">In the example, $rp[0] selects the latest recovery point.</span></span>

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



### <a name="restore-the-disks"></a><span data-ttu-id="bb44e-226">Restauración de los discos</span><span class="sxs-lookup"><span data-stu-id="bb44e-226">Restore the disks</span></span>
<span data-ttu-id="bb44e-227">Use el cmdlet **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** para restaurar los datos y la configuración de un elemento de copia de seguridad a un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bb44e-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="bb44e-228">Una vez que haya identificado un punto de recuperación, úselo como el valor del parámetro **-RecoveryPoint** .</span><span class="sxs-lookup"><span data-stu-id="bb44e-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="bb44e-229">En el código de ejemplo anterior, **$rp[0]** era el punto de recuperación que usar.</span><span class="sxs-lookup"><span data-stu-id="bb44e-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="bb44e-230">En el código de ejemplo siguiente, **$rp[0]** es el punto de recuperación que se va a restaurar en el disco.</span><span class="sxs-lookup"><span data-stu-id="bb44e-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="bb44e-231">Para restaurar los discos y la información de configuración:</span><span class="sxs-lookup"><span data-stu-id="bb44e-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="bb44e-232">Use el cmdlet **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** para esperar a que se complete el trabajo de restauración.</span><span class="sxs-lookup"><span data-stu-id="bb44e-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="bb44e-233">Una vez que se haya completado el trabajo de recuperación, use el cmdlet **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** para obtener los detalles de la operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="bb44e-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="bb44e-234">La propiedad JobDetails tiene la información necesaria para recompilar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb44e-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="bb44e-235">Una vez que restaure los discos, vaya a la siguiente sección para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb44e-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="bb44e-236">Creación de una máquina virtual a partir de discos restaurados</span><span class="sxs-lookup"><span data-stu-id="bb44e-236">Create a VM from restored disks</span></span>
<span data-ttu-id="bb44e-237">Tras haber restaurado los discos, siga estos pasos para crear y configurar la máquina virtual a partir de ellos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="bb44e-238">Para crear máquinas virtuales cifradas a partir de discos restaurados, el rol de Azure debe tener permiso para realizar la acción, **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="bb44e-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="bb44e-239">Si su rol no tiene este permiso, cree un rol personalizado con esta acción.</span><span class="sxs-lookup"><span data-stu-id="bb44e-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="bb44e-240">Para obtener más información, vea [Roles personalizados en RBAC de Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="bb44e-241">Realice una consulta destinada a las propiedades de los discos restaurados para obtener los detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="bb44e-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="bb44e-242">Establezca el contexto de Azure Storage y restaure el archivo de configuración JSON.</span><span class="sxs-lookup"><span data-stu-id="bb44e-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="bb44e-243">Utilice el archivo de configuración JSON para crear la configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb44e-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="bb44e-244">Conecte el disco del sistema operativo y los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="bb44e-245">Según la configuración de las máquinas virtuales, haga clic en el vínculo correspondiente para ver los cmdlets correspondientes:</span><span class="sxs-lookup"><span data-stu-id="bb44e-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="bb44e-246">Máquinas virtuales no administrados, sin cifrar</span><span class="sxs-lookup"><span data-stu-id="bb44e-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="bb44e-247">Máquinas virtuales no administrados y cifradas (sólo BEK)</span><span class="sxs-lookup"><span data-stu-id="bb44e-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="bb44e-248">Máquinas virtuales no administrados y cifradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="bb44e-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="bb44e-249">Máquinas virtuales administradas, sin cifrar</span><span class="sxs-lookup"><span data-stu-id="bb44e-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="bb44e-250">Cifradas máquinas virtuales administradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="bb44e-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="bb44e-251">Máquinas virtuales no administradas y no cifradas</span><span class="sxs-lookup"><span data-stu-id="bb44e-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="bb44e-252">Use el ejemplo siguiente para máquinas virtuales sin administrar y sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="bb44e-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="bb44e-253">Máquinas virtuales cifradas no administradas (solo BEK)</span><span class="sxs-lookup"><span data-stu-id="bb44e-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="bb44e-254">En el caso de las máquinas virtuales cifradas no administradas (cifradas solo mediante BEK), debe restaurar el secreto en el almacén de claves para poder asociar discos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="bb44e-255">Para obtener más información, vea el artículo [Restauración de una máquina virtual de Azure desde un punto de recuperación de Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="bb44e-256">En el ejemplo siguiente se muestra cómo adjuntar discos del sistema operativo y de datos para máquinas virtuales cifradas.</span><span class="sxs-lookup"><span data-stu-id="bb44e-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="bb44e-257">Máquinas virtuales cifradas no administradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="bb44e-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="bb44e-258">En el caso de las máquinas virtuales cifradas no administradas (cifradas mediante BEK y KEK), debe restaurar la clave y el secreto en el almacén de claves para poder asociar discos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="bb44e-259">Para obtener más información, vea el artículo [Restauración de una máquina virtual de Azure desde un punto de recuperación de Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="bb44e-260">En el ejemplo siguiente se muestra cómo adjuntar discos del sistema operativo y de datos para máquinas virtuales cifradas.</span><span class="sxs-lookup"><span data-stu-id="bb44e-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="bb44e-261">Máquinas virtuales administradas y no cifradas</span><span class="sxs-lookup"><span data-stu-id="bb44e-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="bb44e-262">En el caso de máquinas virtuales administradas y no cifradas, deberá crear discos administrados desde Blob Storage y, después, adjuntar los discos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="bb44e-263">Para obtener información detallada, vea el artículo [Adjuntar un disco de datos a una máquina virtual de Windows mediante PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="bb44e-264">En el ejemplo de código siguiente se muestra cómo adjuntar discos de datos para máquinas virtuales administradas y no cifradas.</span><span class="sxs-lookup"><span data-stu-id="bb44e-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="bb44e-265">Máquinas virtuales cifradas administradas (BEK y KEK)</span><span class="sxs-lookup"><span data-stu-id="bb44e-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="bb44e-266">En el caso de las máquinas virtuales administradas y cifradas (cifradas mediante BEK y KEK), debe crear discos administrados desde Blob Storage y luego asociar los discos.</span><span class="sxs-lookup"><span data-stu-id="bb44e-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="bb44e-267">Para obtener información detallada, vea el artículo [Adjuntar un disco de datos a una máquina virtual de Windows mediante PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="bb44e-268">En el ejemplo de código siguiente se muestra cómo adjuntar discos de datos para máquinas virtuales administradas y cifradas.</span><span class="sxs-lookup"><span data-stu-id="bb44e-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="bb44e-269">Ajuste la configuración de la red.</span><span class="sxs-lookup"><span data-stu-id="bb44e-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="bb44e-270">Cree la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb44e-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="bb44e-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb44e-271">Next steps</span></span>
<span data-ttu-id="bb44e-272">Si prefiere usar PowerShell para interactuar con los recursos de Azure, vea el artículo de PowerShell [Implementación y administración de copia de seguridad para Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="bb44e-273">Si administra copias de seguridad de DPM, vea el artículo [Implementación y administración de copias de seguridad para DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="bb44e-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="bb44e-274">Estos dos artículos tienen una versión para las implementaciones de Resource Manager y las clásicas.</span><span class="sxs-lookup"><span data-stu-id="bb44e-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
