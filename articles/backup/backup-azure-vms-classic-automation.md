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
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="62dab-103">Usar AzureRM.Backup cmdlets tooback las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="62dab-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62dab-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62dab-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="62dab-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="62dab-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="62dab-106">Este artículo muestra cómo toouse Azure PowerShell para copias de seguridad y recuperación de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="62dab-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="62dab-107">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="62dab-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="62dab-108">Este artículo incluye el uso de modelo de implementación de hello clásico tooback el almacén de copia de seguridad de datos tooa.</span><span class="sxs-lookup"><span data-stu-id="62dab-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="62dab-109">Si no ha creado un almacén de copia de seguridad en su suscripción, vea la versión del Administrador de recursos de Hola de este artículo, [tooback de cmdlets de uso AzureRM.RecoveryServices.Backup las máquinas virtuales](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="62dab-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="62dab-110">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62dab-111">Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="62dab-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="62dab-112">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="62dab-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="62dab-113">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="62dab-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="62dab-114">Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62dab-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="62dab-115">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="62dab-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="62dab-116">Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="62dab-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="62dab-117">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="62dab-118">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="62dab-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="62dab-119">Conceptos</span><span class="sxs-lookup"><span data-stu-id="62dab-119">Concepts</span></span>
<span data-ttu-id="62dab-120">Este artículo proporciona la información específica toohello cmdlets de PowerShell usa tooback las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="62dab-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="62dab-121">Para ver una introducción a la protección de máquinas virtuales de Azure, consulte [Planeación de la infraestructura de copia de seguridad de máquinas virtuales en Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62dab-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="62dab-122">Antes de empezar, lea hello [requisitos previos](backup-azure-vms-prepare.md) toowork necesario con copia de seguridad de Azure y hello [limitaciones](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) de solución de copia de seguridad de máquina virtual actual Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="62dab-123">toouse PowerShell tomar de hecho, una jerarquía de hello toounderstand del momento de objetos y desde dónde toostart.</span><span class="sxs-lookup"><span data-stu-id="62dab-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Jerarquía de objetos](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="62dab-125">Hola dos flujos más importantes se habilita la protección de una máquina virtual y restaurar los datos de un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="62dab-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="62dab-126">enfoque de Hola de este artículo es toohelp que esté acostumbrados a trabajar con tooenable de cmdlets de PowerShell de hello estos dos escenarios.</span><span class="sxs-lookup"><span data-stu-id="62dab-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="62dab-127">Instalación y registro</span><span class="sxs-lookup"><span data-stu-id="62dab-127">Setup and Registration</span></span>
<span data-ttu-id="62dab-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="62dab-128">toobegin:</span></span>

1. <span data-ttu-id="62dab-129">[Descargue la versión de PowerShell más reciente](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="62dab-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="62dab-130">Encontrar Hola cmdlets de PowerShell de copia de seguridad de Azure disponibles, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="62dab-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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

<span data-ttu-id="62dab-131">Hello siguiente configuración y tareas de registro pueden automatizarse con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="62dab-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="62dab-132">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="62dab-132">Create a backup vault</span></span>
* <span data-ttu-id="62dab-133">Registrar hello las máquinas virtuales con hello servicio de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="62dab-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="62dab-134">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="62dab-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="62dab-135">Para los clientes mediante copia de seguridad de Azure Hola primera vez, deberá toobe de proveedor de copia de seguridad de Azure tooregister Hola usado con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="62dab-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="62dab-136">Puede hacerlo ejecutando el siguiente comando de hello: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="62dab-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="62dab-137">Puede crear un nuevo almacén de copia de seguridad mediante hello **AzureRmBackupVault New** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62dab-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="62dab-138">almacén de copia de seguridad de Hello es un recurso ARM, por lo que necesita tooplace dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="62dab-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="62dab-139">En una consola de Azure PowerShell con privilegios elevados, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="62dab-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="62dab-140">Puede obtener una lista de todos los almacenes de copia de seguridad de hello en una suscripción determinada utilizando hello **AzureRmBackupVault Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62dab-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="62dab-141">Es objeto de almacén de copia de seguridad de hello toostore adecuada en una variable.</span><span class="sxs-lookup"><span data-stu-id="62dab-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="62dab-142">objeto de almacén de Hola se necesita como entrada para muchos de los cmdlets de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="62dab-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="62dab-143">Registrar hello las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="62dab-143">Registering hello VMs</span></span>
<span data-ttu-id="62dab-144">primer paso de Hola para configurar copias de seguridad con copias de seguridad de Azure es tooregister su máquina o máquina virtual con un almacén de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="62dab-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="62dab-145">Hola **AzureRmBackupContainer Register** cmdlet toma Hola información de entrada de una máquina virtual de IaaS de Azure y lo registra con el almacén especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="62dab-146">operación de registro de Hello asocia Hola máquina virtual de Azure con el almacén de copia de seguridad de Hola y pistas Hola VM a través del ciclo de vida de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="62dab-147">Al registrar la máquina virtual con hello servicio de copia de seguridad de Azure, crea un objeto contenedor de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="62dab-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="62dab-148">Un contenedor normalmente contiene varios elementos que pueden ser una copia, pero en caso de hello de máquinas virtuales, habrá un único elemento de copia de seguridad para el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="62dab-149">Copias de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="62dab-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="62dab-150">Creación de una directiva de protección</span><span class="sxs-lookup"><span data-stu-id="62dab-150">Create a protection policy</span></span>
<span data-ttu-id="62dab-151">No es obligatorio toocreate una nueva protección directiva toostart copia de seguridad de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="62dab-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="62dab-152">almacén de Hello viene con una "directiva predeterminada" que pueden ser utilizados tooquickly habilitar la protección y, a continuación, editar más adelante con detalles de la derecha Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="62dab-153">Puede obtener una lista de directivas de hello disponibles en el almacén de hello mediante hello **AzureRmBackupProtectionPolicy Get** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="62dab-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="62dab-154">zona horaria de Hello del campo de BackupTime hello en PowerShell es UTC.</span><span class="sxs-lookup"><span data-stu-id="62dab-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="62dab-155">Sin embargo, cuando se muestre la hora de copia de seguridad de Hola Hola portal de Azure, zona horaria hello es sistema local de tooyour alineado junto con el desplazamiento de UTC de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="62dab-156">Una directiva de copia de seguridad está asociada con al menos una directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="62dab-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="62dab-157">Directiva de retención de Hello define cuánto tiempo se conserva un punto de recuperación con copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="62dab-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="62dab-158">Hola **AzureRmBackupRetentionPolicy New** crea objetos de PowerShell que contienen información de la directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="62dab-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="62dab-159">Estos objetos de directiva de retención se usan las entradas toohello *New-AzureRmBackupProtectionPolicy* cmdlet, o directamente con hello *AzureRmBackupProtection Enable* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62dab-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="62dab-160">Una directiva de copia de seguridad define cuándo y con qué frecuencia hello realizar copia de seguridad de un elemento.</span><span class="sxs-lookup"><span data-stu-id="62dab-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="62dab-161">Hola **AzureRmBackupProtectionPolicy New** cmdlet crea un objeto de PowerShell que contiene información de la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="62dab-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="62dab-162">Hello directiva de copia de seguridad sirve como una entrada toohello *AzureRmBackupProtection Enable* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62dab-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="62dab-163">Habilitar protección</span><span class="sxs-lookup"><span data-stu-id="62dab-163">Enable protection</span></span>
<span data-ttu-id="62dab-164">Habilitar la protección implica dos objetos: hello elemento y Hola directiva y ambos toohello de toobelong necesidad mismo del almacén.</span><span class="sxs-lookup"><span data-stu-id="62dab-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="62dab-165">Una vez asociado con el elemento de hello directiva hello, flujo de trabajo de copia de seguridad de hello activará programación definida Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="62dab-166">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="62dab-166">Initial backup</span></span>
<span data-ttu-id="62dab-167">programación de copia de seguridad de Hola se encargará de hacer copia inicial completa de hello para el elemento de Hola y copia incremental de Hola para copias de seguridad posteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="62dab-168">Sin embargo, si desea que tooforce Hola inicial copia de seguridad toohappen en un momento determinado o incluso inmediatamente, a continuación, usar hello **AzureRmBackupItem de copia de seguridad** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="62dab-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="62dab-169">Hola de zona horaria de hello StartTime y campos de hora de finalización se muestra en PowerShell es UTC.</span><span class="sxs-lookup"><span data-stu-id="62dab-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="62dab-170">Sin embargo, cuando se muestra información similar de hello en hello portal de Azure, zona horaria de hello es el reloj del sistema local de tooyour alineado.</span><span class="sxs-lookup"><span data-stu-id="62dab-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="62dab-171">Supervisión de trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="62dab-171">Monitoring a backup job</span></span>
<span data-ttu-id="62dab-172">La mayor parte de las operaciones de ejecución prolongada en Azure Backup se modelan como un trabajo.</span><span class="sxs-lookup"><span data-stu-id="62dab-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="62dab-173">Esto hace fácil tootrack progreso sin necesidad de hello tookeep abierto de portal de Azure en todo momento.</span><span class="sxs-lookup"><span data-stu-id="62dab-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="62dab-174">estado más reciente de hello tooget de un trabajo en curso, use hello **AzureRmBackupJob Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62dab-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="62dab-175">En lugar de sondear estos trabajos de finalización, que es código innecesario, adicional, resulta más sencillo Hola toouse **AzureRmBackupJob espera** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62dab-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="62dab-176">Cuando se utiliza en una secuencia de comandos, Hola cmdlet pausará ejecución Hola hasta que finaliza el trabajo de Hola u Hola especificado se alcanza el valor de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="62dab-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="62dab-177">Restauración de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="62dab-177">Restore an Azure VM</span></span>
<span data-ttu-id="62dab-178">Datos de pedidos toorestore copia de seguridad, necesita tooidentify Hola copia elementos y punto de recuperación de Hola que contiene los datos de punto en el tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="62dab-179">Esta información es proporcionada toohello AzureRmBackupItem restauración cmdlet tooinitiate una restauración de datos de la cuenta del cliente de hello almacén toohello.</span><span class="sxs-lookup"><span data-stu-id="62dab-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="62dab-180">Seleccione Hola VM</span><span class="sxs-lookup"><span data-stu-id="62dab-180">Select hello VM</span></span>
<span data-ttu-id="62dab-181">objeto de PowerShell de hello tooget que identifica Hola elemento derecha copia de seguridad, se necesita toostart de hello contenedor en el almacén de Hola y el camino hacia abajo de la jerarquía de objetos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="62dab-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="62dab-182">contenedor de hello tooselect que representa la máquina virtual, use Hola Hola **Get AzureRmBackupContainer** cmdlet y canalice dicha toohello **AzureRmBackupItem Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62dab-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="62dab-183">Elección de un punto de recuperación</span><span class="sxs-lookup"><span data-stu-id="62dab-183">Choose a recovery point</span></span>
<span data-ttu-id="62dab-184">Ahora puede enumerar todos los puntos de recuperación de Hola para elemento de copia de seguridad de hello utilizando hello **AzureRmBackupRecoveryPoint Get** cmdlet y elija toorestore de punto de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="62dab-185">Normalmente los usuarios seleccionar más reciente de hello *AppConsistent* punto en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="62dab-186">variable de Hello ```$rp``` es una matriz de puntos de recuperación para hello seleccionado el elemento de copia de seguridad, ordenado en orden inverso de tiempo: punto de recuperación más reciente de hello está en el índice 0.</span><span class="sxs-lookup"><span data-stu-id="62dab-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="62dab-187">Usar indización de punto de recuperación de hello toopick estándar matriz de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62dab-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="62dab-188">Por ejemplo: ```$rp[0]``` seleccionará el punto de recuperación más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="62dab-189">Restauración de discos</span><span class="sxs-lookup"><span data-stu-id="62dab-189">Restoring disks</span></span>
<span data-ttu-id="62dab-190">Hay una diferencia clave entre las operaciones de restauración de hello realiza a través de hello portal de Azure y Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62dab-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="62dab-191">Con PowerShell, la operación de restauración de Hola se detiene en restaurar discos hello y la información de configuración de punto de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="62dab-192">No crea máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="62dab-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="62dab-193">Hola AzureRmBackupItem de restauración no crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="62dab-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="62dab-194">Solo restaura discos hello toohello la cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="62dab-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="62dab-195">Esto es no Hola mismo comportamiento experimentará Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="62dab-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="62dab-196">Puede obtener detalles de Hola Hola de operación de restauración mediante hello **AzureRmBackupJobDetails Get** cmdlet una vez que ha completado el trabajo de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="62dab-197">Hola *ErrorDetails* propiedad disponen de información de hello necesarios toorebuild Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="62dab-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="62dab-198">Compilar Hola VM</span><span class="sxs-lookup"><span data-stu-id="62dab-198">Build hello VM</span></span>
<span data-ttu-id="62dab-199">Hola creación VM fuera de los discos de hello restaurar puede hacerse con los cmdlets de PowerShell de administración de servicio de Azure anteriores hello, Hola nuevas plantillas de Azure Resource Manager, o incluso con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="62dab-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="62dab-200">En un ejemplo rápido, le mostraremos cómo tooget allí mediante cmdlets de administración de servicios de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="62dab-201">Para obtener más información sobre la restauración de discos toobuild una máquina virtual desde hello, lea acerca de hello siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="62dab-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="62dab-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="62dab-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="62dab-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="62dab-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="62dab-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="62dab-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="62dab-205">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="62dab-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="62dab-206">1. Obtener estado de finalización de Hola de subtareas de trabajo</span><span class="sxs-lookup"><span data-stu-id="62dab-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="62dab-207">estado de finalización de hello tootrack de subtareas individuales, puede usar hello **AzureRmBackupJobDetails Get** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="62dab-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="62dab-208">2. Crear un informe diario o semanal de los trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="62dab-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="62dab-209">Normalmente, los administradores deseen tooknow qué trabajos de copia de seguridad que se ejecutaron en hello últimas 24 horas, el estado de Hola de esos trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="62dab-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="62dab-210">Además, cantidad Hola de datos transferidos ofrece a los administradores una manera tooestimate uso mensual de sus datos.</span><span class="sxs-lookup"><span data-stu-id="62dab-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="62dab-211">script de Hola siguiente extrae los datos sin procesar de Hola de hello servicio de copia de seguridad de Azure y muestra información de hello en la consola de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="62dab-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

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

<span data-ttu-id="62dab-212">Si desea tooadd gráficos de resultados del informe toothis capacidades, obtenga información acerca de la entrada de blog de TechNet de hello [gráficos con PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="62dab-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="62dab-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="62dab-213">Next steps</span></span>
<span data-ttu-id="62dab-214">Si prefiere usar PowerShell tooengage con los recursos de Azure, consulte el artículo de PowerShell de Hola para proteger Windows Server, [implementar y administrar copia de seguridad para Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="62dab-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="62dab-215">También hay un artículo de PowerShell sobre cómo administrar las copias de seguridad DPM: [Implementación y administración de copias de seguridad en Azure para servidores de Data Protection Manager (DPM) con PowerShell](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="62dab-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="62dab-216">Estos dos artículos tienen una versión para las implementaciones de Resource Manager, así como las implementaciones clásicas.</span><span class="sxs-lookup"><span data-stu-id="62dab-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
