---
title: "aaaReplicate máquinas virtuales de Hyper-V con PowerShell y el Administrador de recursos de Azure | Documentos de Microsoft"
description: "Automatizar la replicación de Hola de máquinas virtuales de Hyper-V tooAzure con Azure Site Recovery con PowerShell y el Administrador de recursos de Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="25343-103">Replicación entre máquinas virtuales de Hyper-V local y Azure con PowerShell y Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25343-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25343-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="25343-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="25343-105">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="25343-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="25343-106">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="25343-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="25343-107">Información general</span><span class="sxs-lookup"><span data-stu-id="25343-107">Overview</span></span>
<span data-ttu-id="25343-108">Azure Site Recovery contribuye estrategia de recuperación de desastres y la continuidad del negocio tooyour mediante la coordinación de replicación, la conmutación por error y la recuperación de máquinas virtuales en un número de escenarios de implementación.</span><span class="sxs-lookup"><span data-stu-id="25343-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="25343-109">Para obtener una lista completa de escenarios de implementación, vea hello [Introducción a Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25343-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="25343-110">Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25343-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="25343-111">Puede trabajar con dos tipos de módulos: Hola módulo perfil de Azure o un módulo de Azure Resource Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="25343-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="25343-112">Los cmdlets de PowerShell de Site Recovery que están disponibles con Azure PowerShell para Azure Resource Manager le permiten proteger y recuperar los servidores en Azure.</span><span class="sxs-lookup"><span data-stu-id="25343-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="25343-113">Este artículo se describe cómo Windows PowerShell, junto con Azure Resource Manager, toodeploy Site Recovery tooconfigure toouse y orquestar tooAzure de protección del servidor.</span><span class="sxs-lookup"><span data-stu-id="25343-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="25343-114">ejemplo de Hola usado en este artículo muestra cómo tooprotect, conmutación por error y recuperar las máquinas virtuales en un tooAzure de host de Hyper-V mediante PowerShell de Azure con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="25343-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="25343-115">Hello cmdlets de PowerShell de recuperación de sitio actualmente permiten hello tooconfigure siguientes: tooanother de sitio de un administrador de la máquina Virtual y un tooAzure de sitio de Virtual Machine Manager, un tooAzure de sitio de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="25343-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="25343-116">No es necesario toobe un toouse experto de PowerShell en este artículo, pero es necesario toounderstand conceptos básicos de hello, como módulos, cmdlets y las sesiones.</span><span class="sxs-lookup"><span data-stu-id="25343-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="25343-117">Para obtener más información acerca de Windows PowerShell, consulte [Introducción a Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="25343-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="25343-118">Lea más sobre el [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="25343-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="25343-119">Pueden configurar y administrar la protección de servidores de sus clientes partners de Microsoft que forman parte del programa de proveedor de soluciones de nube (CSP) de hello respectivos CSP las suscripciones tootheir clientes (suscripciones de los inquilinos).</span><span class="sxs-lookup"><span data-stu-id="25343-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="25343-120">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="25343-120">Before you start</span></span>
<span data-ttu-id="25343-121">Asegúrese de que tiene preparados estos requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="25343-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="25343-122">Una cuenta de [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="25343-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="25343-123">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25343-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="25343-124">También puede leer sobre los precios del [Administrador de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="25343-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="25343-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="25343-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="25343-126">Para obtener información acerca de esta versión y cómo tooinstall, consulte [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="25343-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="25343-127">Hola [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) y [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) módulos.</span><span class="sxs-lookup"><span data-stu-id="25343-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="25343-128">Puede obtener versiones más recientes de Hola de estos módulos de hello [Galería de PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="25343-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="25343-129">Este artículo se explica cómo toouse Powershell de Azure con Azure Resource Manager tooconfigure y administrar la protección de los servidores.</span><span class="sxs-lookup"><span data-stu-id="25343-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="25343-130">ejemplo de Hola usado en este artículo muestra cómo tooprotect una máquina virtual, que se ejecuta en un host de Hyper-V, tooAzure.</span><span class="sxs-lookup"><span data-stu-id="25343-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="25343-131">Hola siguiendo los requisitos previos es ejemplo toothis específico.</span><span class="sxs-lookup"><span data-stu-id="25343-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="25343-132">Para un conjunto más completo de requisitos para saludo diversos escenarios de recuperación de sitio, consulte la documentación de toohello pertenecen toothat escenario.</span><span class="sxs-lookup"><span data-stu-id="25343-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="25343-133">Necesitará un host de Hyper-V que ejecute Windows Server 2012 R2 o Microsoft Hyper-V Server 2012 R2 que contenga una o varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="25343-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="25343-134">Servidores de Hyper-V conectados toohello Internet, ya sea directamente o a través de un servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="25343-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="25343-135">máquinas virtuales que desea tooprotect Hello deben cumplir las con [requisitos previos de la máquina Virtual](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="25343-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="25343-136">Paso 1: Iniciar sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="25343-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="25343-137">Abra una consola de PowerShell y ejecute este comando toosign en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="25343-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="25343-138">Hola cmdlet, se abrirá una página web que le solicitará las credenciales de cuenta.</span><span class="sxs-lookup"><span data-stu-id="25343-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="25343-139">Como alternativa, también se incluyen en sus credenciales de cuenta como un parámetro toohello `Login-AzureRmAccount` cmdlet, mediante el uso de hello `-Credential` parámetro.</span><span class="sxs-lookup"><span data-stu-id="25343-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="25343-140">Si es socio CSP funciona en nombre de un inquilino, especificar a cliente hello como inquilino, mediante su nombre de dominio principal de tenantID o inquilino.</span><span class="sxs-lookup"><span data-stu-id="25343-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="25343-141">Una cuenta puede tener varias suscripciones, por lo que deberá asociar suscripción Hola desea toouse con cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="25343-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="25343-142">Compruebe que la suscripción está registrada toouse Hola proveedores de Azure para los servicios de recuperación y recuperación del sitio, mediante el uso de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="25343-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="25343-143">En la salida de hello de estos comandos, si hello **RegistrationState** se establece demasiado**registrado**, puede continuar tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="25343-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="25343-144">Si no es así, debe registrar proveedor de falta de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="25343-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="25343-145">Hola tooregister el proveedor de Azure para la recuperación de sitio y servicios de recuperación, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="25343-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="25343-146">Compruebe que los proveedores de Hola registran correctamente mediante Hola siga los comandos: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` y `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="25343-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="25343-147">Paso 2: Configurar Hola que del almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="25343-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="25343-148">Crear un grupo de recursos de Azure Resource Manager en el que podrá crear almacén de Hola o usar un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="25343-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="25343-149">Puede crear un nuevo grupo de recursos mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25343-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="25343-150">donde variable hello $ResourceGroupName contiene el nombre de Hola Hola del grupo de recursos que desee toocreate y variable hello $Geo contiene hello Azure región en qué grupo de recursos de hello toocreate (por ejemplo, "Sur de Brasil").</span><span class="sxs-lookup"><span data-stu-id="25343-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="25343-151">Puede obtener una lista de grupos de recursos en su suscripción mediante hello `Get-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25343-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="25343-152">Cree un nuevo almacén de Servicios de recuperación de Azure como sigue:</span><span class="sxs-lookup"><span data-stu-id="25343-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="25343-153">Puede recuperar una lista de los almacenes existentes mediante hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25343-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="25343-154">Si desea que las operaciones de tooperform en almacenes de Site Recovery creados mediante el portal clásico de Hola o el módulo de administración de servicio de Azure PowerShell hello, puede recuperar una lista de estos almacenes mediante hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25343-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="25343-155">Debe crear un nuevo almacén de Servicios de recuperación para todas las operaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="25343-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="25343-156">almacenes de Site Recovery de Hola que creó anteriormente se admiten, pero no tienen características más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="25343-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="25343-157">Paso 3: Establecer contexto de almacén de servicios de recuperación de Hola</span><span class="sxs-lookup"><span data-stu-id="25343-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="25343-158">Establecer el contexto del almacén de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25343-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="25343-159">Paso 4: Crear un sitio de Hyper-V y generar una nueva clave de registro de almacén para el sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="25343-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="25343-160">Cree un nuevo sitio de Hyper-V como sigue:</span><span class="sxs-lookup"><span data-stu-id="25343-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="25343-161">Este cmdlet inicia un sitio de recuperación del sitio trabajo toocreate hello y devuelve un objeto de trabajo de recuperación del sitio.</span><span class="sxs-lookup"><span data-stu-id="25343-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="25343-162">Espere Hola trabajo toocomplete y compruebe que el trabajo de Hola se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="25343-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="25343-163">Puede recuperar el objeto de trabajo de hello y, por tanto, comprobar estado actual de Hola de trabajo de hello, usando el cmdlet Get-AzureRmSiteRecoveryJob Hola.</span><span class="sxs-lookup"><span data-stu-id="25343-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="25343-164">Generar y descargar una clave de registro para el sitio de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="25343-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="25343-165">Hola de copia había descargado host de Hyper-V de clave toohello.</span><span class="sxs-lookup"><span data-stu-id="25343-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="25343-166">Necesita hello tooregister clave Hola Hyper-V host toohello sitio.</span><span class="sxs-lookup"><span data-stu-id="25343-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="25343-167">Paso 5: Instalar el proveedor de Azure Site Recovery hello y agente de servicios de recuperación de Azure en su host de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="25343-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="25343-168">Descargar el instalador de hello para la versión más reciente de Hola de proveedor de Hola desde [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="25343-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="25343-169">Instalador de ejecución hello en el host de Hyper-V y al final de Hola de instalación de hello continuar paso de registro toohello.</span><span class="sxs-lookup"><span data-stu-id="25343-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="25343-170">Cuando se le solicite, proporcione Hola descarga clave de registro del sitio y completar el registro del sitio de toohello de host de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="25343-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="25343-171">Comprobar que hospedan Hola Hyper-V se sitio toohello registrados mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25343-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="25343-172">Paso 6: Crear una directiva de replicación y asociarla con el contenedor de protección de Hola</span><span class="sxs-lookup"><span data-stu-id="25343-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="25343-173">Cree una directiva de replicación como sigue:</span><span class="sxs-lookup"><span data-stu-id="25343-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="25343-174">Comprobación de hello devuelve tooensure de trabajo que la creación de directiva de replicación de hello tiene éxito.</span><span class="sxs-lookup"><span data-stu-id="25343-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="25343-175">Hello cuenta de almacenamiento especificada debe ser en Hola la misma región de Azure como el almacén de servicios de recuperación y debe tener habilitada la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="25343-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="25343-176">Si Hola especifica recuperación cuenta de almacenamiento es de tipo de almacenamiento de Azure (clásica), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (clásico).</span><span class="sxs-lookup"><span data-stu-id="25343-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="25343-177">Si Hola especifica la cuenta de almacenamiento de recuperación es de tipo de almacenamiento de Azure (Administrador de recursos de Azure), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (Administrador de recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="25343-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="25343-178">Obtener Hola protección contenedor toohello sitio correspondiente, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="25343-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="25343-179">Iniciar asociación Hola del contenedor de protección de hello con la directiva de replicación de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="25343-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="25343-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="25343-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="25343-181">Espere a toocomplete de trabajo de asociación de Hola y asegúrese de que se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="25343-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="25343-182">Paso 7: Habilitación de la protección para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="25343-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="25343-183">Obtener Hola protección entidad correspondiente toohello VM desea tooprotect, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="25343-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="25343-184">Empezar a proteger máquina virtual de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="25343-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="25343-185">Hello cuenta de almacenamiento especificada debe ser en Hola la misma región de Azure como el almacén de servicios de recuperación y debe tener habilitada la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="25343-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="25343-186">Si Hola especifica recuperación cuenta de almacenamiento es de tipo de almacenamiento de Azure (clásica), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (clásico).</span><span class="sxs-lookup"><span data-stu-id="25343-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="25343-187">Si Hola especifica la cuenta de almacenamiento de recuperación es de tipo de almacenamiento de Azure (Administrador de recursos de Azure), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (Administrador de recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="25343-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="25343-188">Si Hola VM que se va a proteger tiene más de un disco tooit adjunto, especifique el disco del sistema operativo de hello con hello *OSDiskName* parámetro.</span><span class="sxs-lookup"><span data-stu-id="25343-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="25343-189">Espere a que tooreach de máquinas virtuales de hello un estado protegido después de la replicación inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="25343-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="25343-190">Esto puede tardar bastante tiempo, dependiendo de factores como la cantidad de Hola de toobe de datos replicada y Hola tooAzure de nivel superior de ancho de banda disponible.</span><span class="sxs-lookup"><span data-stu-id="25343-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="25343-191">Estado del trabajo de Hola y EstadoDescripción se actualizan como se indica a continuación, en hello VM llegar a un estado protegido.</span><span class="sxs-lookup"><span data-stu-id="25343-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="25343-192">Actualizar propiedades de recuperación, como Hola tamaño de rol de máquina virtual y conmutación por error de hello Azure red tooattach hello de la máquina virtual red interfaz tarjetas tooupon.</span><span class="sxs-lookup"><span data-stu-id="25343-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="25343-193">Paso 8: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="25343-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="25343-194">Ejecute un trabajo de conmutación por error de prueba, como sigue:</span><span class="sxs-lookup"><span data-stu-id="25343-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="25343-195">Compruebe que se crea la VM en Azure de la prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="25343-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="25343-196">(trabajo de conmutación por error de prueba de hello está suspendido, después de crear la máquina virtual de prueba de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="25343-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="25343-197">Hola completa limpiando los artefactos de hello creado al reanudar trabajo hello, como se muestra en el paso siguiente Hola.)</span><span class="sxs-lookup"><span data-stu-id="25343-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="25343-198">Hola completa probar conmutación por error, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="25343-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="25343-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25343-199">Next Steps</span></span>
<span data-ttu-id="25343-200">[Más información](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre los cmdlets de PowerShell de Azure Site Recovery con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="25343-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
