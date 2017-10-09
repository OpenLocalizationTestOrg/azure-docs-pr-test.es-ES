---
title: "aaaReplicate tooAzure de máquinas virtuales de Hyper-V en el portal clásico de hello con PowerShell | Documentos de Microsoft"
description: "Automatizar la replicación de máquinas virtuales de Hyper-V en nubes VMM con Site Recovery y PowerShell en el portal clásico de Hola Hola"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="beba8-103">Replicar tooAzure de máquinas virtuales de Hyper-V con PowerShell en el portal clásico de Hola</span><span class="sxs-lookup"><span data-stu-id="beba8-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="beba8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="beba8-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="beba8-105">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="beba8-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="beba8-106">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="beba8-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="beba8-107">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="beba8-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="beba8-108">Información general</span><span class="sxs-lookup"><span data-stu-id="beba8-108">Overview</span></span>
<span data-ttu-id="beba8-109">Azure Site Recovery contribuye estrategia de recuperación (BCDR) ante desastres y continuidad del negocio de tooyour mediante la coordinación de replicación, la conmutación por error y la recuperación de máquinas virtuales en un número de escenarios de implementación.</span><span class="sxs-lookup"><span data-stu-id="beba8-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="beba8-110">Para obtener una lista completa de la implementación de escenarios vea hello [Introducción a Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="beba8-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="beba8-111">Este artículo muestra cómo las tareas comunes de toouse PowerShell tooautomate necesita tooperform al configurar máquinas de virtuales de Hyper-V de Azure Site Recovery tooreplicate en almacenamiento de tooAzure de nubes de System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="beba8-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="beba8-112">artículo de Hello incluye los requisitos previos de escenario de Hola y muestra también cómo instalar tooset un almacén de Site Recovery, hello Azure Site Recovery Provider Hola servidor VMM de origen, Registrar servidor hello en el almacén de hello, agregar una cuenta de almacenamiento de Azure, instalar hello Azure Agente de servicios de recuperación en los servidores de host de Hyper-V, configurar la protección para nubes VMM que será aplicado tooall protegido las máquinas virtuales y, a continuación, habilitar la protección de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="beba8-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="beba8-113">Finalice prueba toomake de conmutación por error de Hola que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="beba8-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="beba8-114">Si experimenta problemas al configurar este escenario, publicar sus preguntas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="beba8-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="beba8-115">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="beba8-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="beba8-116">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="beba8-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="beba8-117">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="beba8-117">Before you start</span></span>
<span data-ttu-id="beba8-118">Asegúrese de que tiene preparados estos requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="beba8-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="beba8-119">Requisitos previos de Azure</span><span class="sxs-lookup"><span data-stu-id="beba8-119">Azure prerequisites</span></span>
* <span data-ttu-id="beba8-120">Necesitará una cuenta de [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="beba8-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="beba8-121">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="beba8-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="beba8-122">Necesitará un toostore replicado de datos de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="beba8-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="beba8-123">cuenta de Hello tiene habilitada la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="beba8-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="beba8-124">Debe quedar en Hola misma región que el almacén de Azure Site Recovery de Hola y asociarse Hola misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="beba8-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="beba8-125">[Más información sobre Almacenamiento de Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="beba8-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="beba8-126">Necesitará toomake seguro de que se cumplan las máquinas virtuales que desee tooprotect [requisitos previos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="beba8-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="beba8-127">Requisitos previos de VMM</span><span class="sxs-lookup"><span data-stu-id="beba8-127">VMM prerequisites</span></span>
* <span data-ttu-id="beba8-128">Necesitará un servidor VMM que se ejecute en System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="beba8-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="beba8-129">Necesitará al menos una nube en el servidor VMM que desee tooprotect Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="beba8-130">en la nube Hola debe contener:</span><span class="sxs-lookup"><span data-stu-id="beba8-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="beba8-131">Uno o más grupos de hosts de VMM</span><span class="sxs-lookup"><span data-stu-id="beba8-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="beba8-132">Uno o más servidores host de Hyper-V o clústeres en cada grupo de hosts.</span><span class="sxs-lookup"><span data-stu-id="beba8-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="beba8-133">Máquinas virtuales de uno o más en el servidor de Hyper-V de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="beba8-134">Requisitos previos de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="beba8-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="beba8-135">Hello servidores host Hyper-V deben ejecutar al menos **Windows Server 2012** con el rol de Hyper-V o **Microsoft Hyper-V Server 2012** y ha hello las últimas actualizaciones instaladas.</span><span class="sxs-lookup"><span data-stu-id="beba8-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="beba8-136">Si está ejecutando Hyper-V en un clúster, tenga en cuenta que ese agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="beba8-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="beba8-137">Necesitará a un agente de clúster hello tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="beba8-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="beba8-138">toodo esto, en el administrador del servidor > Administrador de clústeres de conmutación por error, clúster toohello de conectarse, haga clic en **configurar rol** y seleccione **agente de réplica de Hyper-V** en hello **Seleccionar rol**pantalla del Asistente para alta disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="beba8-139">Cualquier servidor de host de Hyper-V o clúster que se desea protección toomanage debe incluirse en una nube de VMM.</span><span class="sxs-lookup"><span data-stu-id="beba8-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="beba8-140">Requisitos previos de asignación de redes</span><span class="sxs-lookup"><span data-stu-id="beba8-140">Network mapping prerequisites</span></span>
<span data-ttu-id="beba8-141">Al proteger las máquinas virtuales en mapas de asignación de red de Azure entre redes de VM Hola servidor VMM de origen y destino siguiente de hello tooenable de redes de Azure:</span><span class="sxs-lookup"><span data-stu-id="beba8-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="beba8-142">Todas las máquinas que conmutar por error en hello mismo pueden conectar tooeach otro, independientemente del plan de recuperación que se encuentran en red.</span><span class="sxs-lookup"><span data-stu-id="beba8-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="beba8-143">Si una puerta de enlace de red es el programa de instalación en red de Azure de destino de hello, máquinas virtuales pueden conectarse a máquinas virtuales de tooother local.</span><span class="sxs-lookup"><span data-stu-id="beba8-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="beba8-144">Si no configura la red asignación solo las máquinas virtuales que conmutan en hello mismo plan de recuperación será capaz de tooconnect tooeach otros después tooAzure de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="beba8-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="beba8-145">Si desea que la asignación de red toodeploy, necesitará la siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="beba8-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="beba8-146">Hello las máquinas virtuales que desee tooprotect Hola servidor VMM de origen debe ser una red de VM tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="beba8-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="beba8-147">Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="beba8-148">Puede conectar una red Azure toowhich replicado a máquinas virtuales después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="beba8-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="beba8-149">Esta red seleccionará en tiempo de Hola de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="beba8-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="beba8-150">red de Hello debe formar parte de hello misma región que su suscripción de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="beba8-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="beba8-151">Requisitos previos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="beba8-151">PowerShell prerequisites</span></span>
<span data-ttu-id="beba8-152">Asegúrese de que tiene listo toogo de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="beba8-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="beba8-153">Si ya usa PowerShell, deberá tooupgrade tooversion 0.8.10 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="beba8-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="beba8-154">Para obtener información acerca de cómo configurar PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="beba8-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="beba8-155">Una vez que se instala y configura PowerShell, puede ver todos los cmdlets disponibles de hello para el servicio de Hola de [aquí](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="beba8-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="beba8-156">toolearn acerca de las sugerencias que pueden ayudarle a usar los cmdlets de hello, como cómo normalmente se controlan los valores de parámetro, las entradas y salidas en Azure PowerShell, consulte [empezar a trabajar con Cmdlets de Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="beba8-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="beba8-157">Paso 1: Configurar la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="beba8-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="beba8-158">En PowerShell, ejecute estos cmdlets:</span><span class="sxs-lookup"><span data-stu-id="beba8-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="beba8-159">Reemplazar elementos Hola Hola "< >" con información específica de su.</span><span class="sxs-lookup"><span data-stu-id="beba8-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="beba8-160">Paso 2: Creación de un almacén de recuperación del sitio</span><span class="sxs-lookup"><span data-stu-id="beba8-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="beba8-161">En PowerShell, reemplazar elementos Hola Hola "< >" con información específica de su y ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="beba8-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="beba8-162">Paso 3: Generación de una clave de registro de almacén</span><span class="sxs-lookup"><span data-stu-id="beba8-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="beba8-163">Generar una clave de registro en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="beba8-164">Después de descargar hello Azure Site Recovery Provider e instalarlo en el servidor VMM hello, deberá usar este servidor VMM de hello tooregister clave en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="beba8-165">Obtener archivo de configuración de almacén de hello y establecer contexto de hello:</span><span class="sxs-lookup"><span data-stu-id="beba8-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="beba8-166">Establecer el contexto del almacén de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="beba8-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="beba8-167">Paso 4: Instalar hello Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="beba8-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="beba8-168">En la máquina VMM hello, cree un directorio ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="beba8-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="beba8-169">Extraiga los archivos de hello mediante el proveedor de hello descargado ejecutando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="beba8-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="beba8-170">Instalar a proveedor de hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="beba8-170">Install hello provider using hello following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="beba8-171">Espere Hola instalación toofinish.</span><span class="sxs-lookup"><span data-stu-id="beba8-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="beba8-172">Registrar servidor de hello en almacén de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="beba8-173">Paso 5: Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="beba8-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="beba8-174">Si no tiene una cuenta de almacenamiento de Azure, cree una cuenta de replicación geográfica habilitada mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="beba8-175">Tenga en cuenta que debe ser la cuenta de almacenamiento de hello en Hola misma región que el servicio de Azure Site Recovery de Hola y asociarse Hola misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="beba8-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="beba8-176">Paso 6: Instalar Hola agente de servicios de recuperación de Azure</span><span class="sxs-lookup"><span data-stu-id="beba8-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="beba8-177">Desde Hola portal de Azure, instalar el agente de servicios de recuperación de Azure de hello en cada servidor de host de Hyper-V ubicado en nubes VMM Hola desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="beba8-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="beba8-178">Ejecute hello siguiente comando en todos los hosts VMM:</span><span class="sxs-lookup"><span data-stu-id="beba8-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="beba8-179">Paso 7: Configuración de la protección de la nube</span><span class="sxs-lookup"><span data-stu-id="beba8-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="beba8-180">Crear una tooAzure de perfil de protección de nube mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="beba8-181">Obtener un contenedor de protección mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="beba8-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="beba8-182">Iniciar asociación Hola del contenedor de protección de Hola a nube hello:</span><span class="sxs-lookup"><span data-stu-id="beba8-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="beba8-183">Cuando haya finalizado el trabajo de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="beba8-184">Después de que el trabajo de hello ha finalizado el procesamiento, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-184">After hello job has finished processing, run hello following command:</span></span>

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



<span data-ttu-id="beba8-185">finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="beba8-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="beba8-186">Paso 8: Configuración de la asignación de red</span><span class="sxs-lookup"><span data-stu-id="beba8-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="beba8-187">Antes de empezar la asignación de red Compruebe que máquinas virtuales en el servidor VMM de origen Hola son red de VM tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="beba8-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="beba8-188">Además, cree una o varias redes virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="beba8-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="beba8-189">Tenga en cuenta que varias redes de VM pueden ser asignado tooa sola red de Azure.</span><span class="sxs-lookup"><span data-stu-id="beba8-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="beba8-190">Tenga en cuenta que si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="beba8-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="beba8-191">Si no hay una subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="beba8-192">Hola primer comando obtiene servidores de almacén de Azure Site Recovery de hello actual.</span><span class="sxs-lookup"><span data-stu-id="beba8-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="beba8-193">comando Hello almacena servidores de Microsoft Azure Site Recovery de hello en la variable de matriz de hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="beba8-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="beba8-194">Hola segundo comando obtiene red de recuperación de sitio de hello para el primer servidor de hello en la matriz de hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="beba8-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="beba8-195">comando Hello almacena redes hello en la variable de hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="beba8-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="beba8-196">Hola tercer comando obtiene las suscripciones de Azure mediante el cmdlet Get-AzureSubscription hello y, a continuación, almacena ese valor en la variable de hello $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="beba8-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="beba8-197">Hola cuarto comando obtiene redes virtuales de Azure utilizando el cmdlet Get-AzureVNetSite hello y, a continuación, ese valor en la variable de hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="beba8-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="beba8-198">Hola final cmdlet crea una asignación entre la red principal de Hola y de red de máquina virtual de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="beba8-199">Hola cmdlet especifica la red principal de hello como primer elemento de Hola de $Networks.</span><span class="sxs-lookup"><span data-stu-id="beba8-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="beba8-200">Hola cmdlet especifica una red de máquina virtual como primer elemento de Hola de $AzureVmNetworks mediante su identificador.</span><span class="sxs-lookup"><span data-stu-id="beba8-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="beba8-201">comando de Hello incluye el identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="beba8-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="beba8-202">Paso 9: Habilitación de la protección para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="beba8-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="beba8-203">Después de servidores, las nubes y las redes están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="beba8-204">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="beba8-204">Note hello following:</span></span>

<span data-ttu-id="beba8-205">Las máquinas virtuales deben cumplir [Requisitos previos de las máquinas virtuales de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="beba8-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="beba8-206">sistema operativo de tooenable protección hello y propiedades del disco de sistema operativo deben establecerse para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="beba8-207">Cuando se crea una máquina virtual en VMM mediante una plantilla de máquina virtual puede establecer la propiedad Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="beba8-208">También puede establecer estas propiedades para las máquinas virtuales existentes en hello **General** y **configuración de Hardware** fichas de propiedades de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="beba8-209">Si no establece estas propiedades en VMM estará tooconfigure capaz de ellas en el portal de Azure Site Recovery Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="beba8-210">protección de tooenable, ejecute hello después de contenedor de protección de hello tooget de comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="beba8-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="beba8-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="beba8-212">Obtener la entidad de protección de hello (VM) mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="beba8-213">Habilitar hello recuperación ante desastres para hello VM mediante la ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="beba8-214">Prueba de la implementación</span><span class="sxs-lookup"><span data-stu-id="beba8-214">Test your deployment</span></span>
<span data-ttu-id="beba8-215">plan de la implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una prueba de conmutación por error para hello tootest.</span><span class="sxs-lookup"><span data-stu-id="beba8-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="beba8-216">La conmutación por error de prueba simula su mecanismo de conmutación por error y recuperación en una red aislada.</span><span class="sxs-lookup"><span data-stu-id="beba8-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="beba8-217">Observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="beba8-217">Note that:</span></span>

* <span data-ttu-id="beba8-218">Si desea tooconnect toohello virtual machine en Azure mediante Escritorio remoto después de la conmutación por error de hello, habilite la conexión a Escritorio remoto en la máquina virtual de hello antes de ejecutar la conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="beba8-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="beba8-219">Después de la conmutación por error, deberá usar una máquina de virtual toohello pública del tooconnect de dirección IP en Azure mediante Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="beba8-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="beba8-220">Si desea toodo esto, asegúrese de que no hay ninguna directiva de dominio que impiden la conexión máquina virtual de tooa con una dirección pública.</span><span class="sxs-lookup"><span data-stu-id="beba8-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="beba8-221">finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="beba8-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="beba8-222">Creación de un plan de recuperación</span><span class="sxs-lookup"><span data-stu-id="beba8-222">Create a recovery plan</span></span>
1. <span data-ttu-id="beba8-223">Cree un archivo .xml como plantilla para el plan de recuperación con datos de Hola a continuación y, a continuación, guárdelo como "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="beba8-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="beba8-224">Cambie el nodo de RecoveryPlan Hola Id., nombre, PrimaryServerId y SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="beba8-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="beba8-225">Cambie el nodo de hello ProtectionEntity PrimaryProtectionEntityId (vmid de VMM).</span><span class="sxs-lookup"><span data-stu-id="beba8-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="beba8-226">Puede agregar más máquinas virtuales añadiendo más nodos ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="beba8-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="beba8-227">Rellene los datos de hello en plantilla hello:</span><span class="sxs-lookup"><span data-stu-id="beba8-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="beba8-228">Crear Hola RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="beba8-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="beba8-229">Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="beba8-229">Run a test failover</span></span>
1. <span data-ttu-id="beba8-230">Obtener objetos de hello RecoveryPlan ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="beba8-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="beba8-231">$RPObject = get-AzureSiteRecoveryRecoveryPlan-nombre $RPName;</span><span class="sxs-lookup"><span data-stu-id="beba8-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="beba8-232">Iniciar conmutación por error de prueba de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="beba8-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="beba8-233"><a name=monitor></a> Supervisión de la actividad</span><span class="sxs-lookup"><span data-stu-id="beba8-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="beba8-234">Usar hello después de la actividad de hello toomonitor de comandos.</span><span class="sxs-lookup"><span data-stu-id="beba8-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="beba8-235">Tenga en cuenta que tiene toowait entre los trabajos de hello toofinish de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="beba8-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="beba8-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="beba8-236">Next steps</span></span>
<span data-ttu-id="beba8-237">[Obtenga más información](/powershell/azure/overview) sobre cmdlets de PowerShell de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="beba8-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="beba8-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="beba8-238"></a>.</span></span>
