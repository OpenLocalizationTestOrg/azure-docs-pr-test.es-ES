---
title: "Replicación de máquinas virtuales de Hyper-V con PowerShell y Azure Resource Manager | Microsoft Docs"
description: "Automatice la replicación de máquinas virtuales de Hyper-V en Azure con Azure Site Recovery mediante PowerShell y Azure Resource Manager."
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
ms.openlocfilehash: dbd562b73b0caecd0feb993bd6fb796dddb0438c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="709e3-103">Replicación entre máquinas virtuales de Hyper-V local y Azure con PowerShell y Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="709e3-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="709e3-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="709e3-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="709e3-105">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="709e3-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="709e3-106">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="709e3-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="709e3-107">Información general</span><span class="sxs-lookup"><span data-stu-id="709e3-107">Overview</span></span>
<span data-ttu-id="709e3-108">Azure Site Recovery contribuye a su estrategia de continuidad de negocio y recuperación ante desastres mediante la organización de la replicación, la conmutación por error y la recuperación de máquinas virtuales en varios escenarios de implementación.</span><span class="sxs-lookup"><span data-stu-id="709e3-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="709e3-109">Para obtener una lista completa de los escenarios de implementación, vea la [Información general sobre Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="709e3-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="709e3-110">Azure PowerShell es un módulo que ofrece cmdlets para administrar Azure mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="709e3-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="709e3-111">Puede funcionar con dos tipos de módulos: el módulo de perfil de Azure o el módulo de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="709e3-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="709e3-112">Los cmdlets de PowerShell de Site Recovery que están disponibles con Azure PowerShell para Azure Resource Manager le permiten proteger y recuperar los servidores en Azure.</span><span class="sxs-lookup"><span data-stu-id="709e3-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="709e3-113">En este artículo se describe cómo usar Windows PowerShell, junto con Azure Resource Manager, para implementar Site Recovery con el fin de configurar y orquestar la protección de los servidores.</span><span class="sxs-lookup"><span data-stu-id="709e3-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="709e3-114">El ejemplo que se usa en este artículo muestra cómo proteger, realizar conmutaciones por error y recuperar máquinas virtuales en un host de Hyper-V en Azure, mediante Azure PowerShell con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="709e3-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="709e3-115">Los cmdlets de PowerShell de Site Recovery actualmente le permiten configurar lo siguiente: un sitio de Virtual Machine Manager en otro sitio, un sitio de Virtual Machine Manager en Azure y un sitio Hyper-V en Azure.</span><span class="sxs-lookup"><span data-stu-id="709e3-115">The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.</span></span>
>
>

<span data-ttu-id="709e3-116">No es necesario ser un experto en PowerShell para leer este artículo, pero sí debe conocer los conceptos básicos, como módulos, cmdlets y sesiones.</span><span class="sxs-lookup"><span data-stu-id="709e3-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="709e3-117">Para obtener más información acerca de Windows PowerShell, consulte [Introducción a Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="709e3-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="709e3-118">Lea más sobre el [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="709e3-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="709e3-119">Los asociados de Microsoft que forman parte del programa Proveedor de soluciones en la nube (CSP) pueden configurar y administrar la protección de los servidores de sus clientes en las suscripciones a CSP correspondientes de los clientes (suscripciones de inquilino).</span><span class="sxs-lookup"><span data-stu-id="709e3-119">Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="709e3-120">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="709e3-120">Before you start</span></span>
<span data-ttu-id="709e3-121">Asegúrese de que tiene preparados estos requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="709e3-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="709e3-122">Una cuenta de [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="709e3-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="709e3-123">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="709e3-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="709e3-124">También puede leer sobre los precios del [Administrador de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="709e3-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="709e3-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="709e3-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="709e3-126">Para obtener información acerca de esta versión y cómo instalarla, consulte [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="709e3-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="709e3-127">Los módulos [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) y [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/).</span><span class="sxs-lookup"><span data-stu-id="709e3-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="709e3-128">Puede obtener las últimas versiones de estos módulos en la [Galería de PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="709e3-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="709e3-129">En este artículo se muestra cómo usar Azure PowerShell con Azure Resource Manager para configurar y administrar la protección de los servidores.</span><span class="sxs-lookup"><span data-stu-id="709e3-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="709e3-130">El ejemplo utilizado en este artículo muestra cómo proteger una máquina virtual, que se ejecuta en un host de Hyper-V en Azure.</span><span class="sxs-lookup"><span data-stu-id="709e3-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="709e3-131">Los siguientes requisitos previos son específicos para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="709e3-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="709e3-132">Para consultar un conjunto más amplio de requisitos para los distintos escenarios de Site Recovery, vea la documentación correspondiente a cada escenario.</span><span class="sxs-lookup"><span data-stu-id="709e3-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="709e3-133">Necesitará un host de Hyper-V que ejecute Windows Server 2012 R2 o Microsoft Hyper-V Server 2012 R2 que contenga una o varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="709e3-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="709e3-134">Los servidores de Hyper-V deben estar conectados a Internet, directamente o a través de un proxy.</span><span class="sxs-lookup"><span data-stu-id="709e3-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="709e3-135">Las máquinas virtuales que quiere proteger deben cumplir los [requisitos previos para las máquinas virtuales](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="709e3-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="709e3-136">Paso 1: Inicio de sesión en la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="709e3-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="709e3-137">Abra una consola de PowerShell y ejecute este comando para iniciar sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="709e3-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="709e3-138">El cmdlet abrirá una página web que le solicitará las credenciales de cuenta.</span><span class="sxs-lookup"><span data-stu-id="709e3-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="709e3-139">Como alternativa, también puede incluir las credenciales de cuenta como un parámetro en el cmdlet `Login-AzureRmAccount` utilizando el parámetro `-Credential`.</span><span class="sxs-lookup"><span data-stu-id="709e3-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="709e3-140">Si usted es un asociado CSP que trabaja en nombre de un inquilino, especifique el cliente como inquilino usando su TenantID o su nombre de dominio principal de inquilino.</span><span class="sxs-lookup"><span data-stu-id="709e3-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="709e3-141">Una cuenta puede tener varias suscripciones, por lo que deberá asociar la suscripción que desee usar con la cuenta.</span><span class="sxs-lookup"><span data-stu-id="709e3-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="709e3-142">Compruebe que su suscripción está registrada para usar los proveedores de Azure para Recovery Services y Site Recovery con los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="709e3-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="709e3-143">Si **RegistrationState** está establecido en el valor **Registrado** en la salida de estos comandos, puede continuar con el paso 2.</span><span class="sxs-lookup"><span data-stu-id="709e3-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="709e3-144">Si no es así, debe registrar al proveedor que falta en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="709e3-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="709e3-145">Para registrar el proveedor de Azure en Site Recovery y Servicios de recuperación, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="709e3-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="709e3-146">Compruebe que los proveedores se registraron correctamente mediante los comandos `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` y `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="709e3-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="709e3-147">Paso 2: Configuración del almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="709e3-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="709e3-148">Cree un grupo de recursos Azure Resource Manager en el que podrá crear el almacén, o bien use un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="709e3-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="709e3-149">Puede crear un grupo de recursos nuevo mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="709e3-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="709e3-150">donde la variable $ResourceGroupName contiene el nombre del grupo de recursos que desea crear y la variable $Geo contiene la región de Azure en la que se va a crear el grupo de recursos (por ejemplo: "Sur de Brasil").</span><span class="sxs-lookup"><span data-stu-id="709e3-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="709e3-151">Puede obtener una lista de grupos de recursos en la suscripción con el cmdlet `Get-AzureRmResourceGroup` .</span><span class="sxs-lookup"><span data-stu-id="709e3-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="709e3-152">Cree un nuevo almacén de Servicios de recuperación de Azure como sigue:</span><span class="sxs-lookup"><span data-stu-id="709e3-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="709e3-153">Puede recuperar una lista de los almacenes existentes con el cmdlet `Get-AzureRmRecoveryServicesVault`.</span><span class="sxs-lookup"><span data-stu-id="709e3-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="709e3-154">Si desea realizar operaciones en los almacenes de Site Recovery creados mediante el portal clásico o el módulo PowerShell de Administración de servicios de Azure, puede recuperar una lista de dichos almacenes con el cmdlet `Get-AzureRmSiteRecoveryVault`.</span><span class="sxs-lookup"><span data-stu-id="709e3-154">If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="709e3-155">Debe crear un nuevo almacén de Servicios de recuperación para todas las operaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="709e3-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="709e3-156">Los almacenes de Site Recovery que ha creado anteriormente son compatibles, pero no tienen las últimas características.</span><span class="sxs-lookup"><span data-stu-id="709e3-156">The Site Recovery vaults you've created earlier are supported, but don't have the latest features.</span></span>
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="709e3-157">Paso 3: Configuración del contexto de almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="709e3-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="709e3-158">Establezca el contexto de almacén mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="709e3-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="709e3-159">Paso 4: Creación de un sitio Hyper-V y generación de una nueva clave de registro de almacén para el sitio.</span><span class="sxs-lookup"><span data-stu-id="709e3-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="709e3-160">Cree un nuevo sitio de Hyper-V como sigue:</span><span class="sxs-lookup"><span data-stu-id="709e3-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="709e3-161">Este cmdlet inicia un trabajo de Site Recovery para crear el sitio y devuelve un objeto de trabajo de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="709e3-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="709e3-162">Espere a que el trabajo se complete y compruebe que se ha hecho correctamente.</span><span class="sxs-lookup"><span data-stu-id="709e3-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="709e3-163">Puede recuperar el objeto de trabajo y, por tanto, comprobar el estado actual del trabajo mediante el cmdlet Get-AzureRmSiteRecoveryJob.</span><span class="sxs-lookup"><span data-stu-id="709e3-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="709e3-164">Genere y descargue una clave de registro para el sitio; para ello, proceda como sigue:</span><span class="sxs-lookup"><span data-stu-id="709e3-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="709e3-165">Copie la clave descargada en el host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="709e3-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="709e3-166">Necesita la clave para registrar el host de Hyper-V en el sitio</span><span class="sxs-lookup"><span data-stu-id="709e3-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="709e3-167">Paso 5: Instalación del proveedor de Azure Site Recovery y del agente de Servicios de recuperación de Azure en el host de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="709e3-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="709e3-168">Descargue el instalador de la última versión del proveedor de [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="709e3-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="709e3-169">Ejecute el instalador en el host de Hyper-V y al final de la instalación continúe con el paso de registro.</span><span class="sxs-lookup"><span data-stu-id="709e3-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="709e3-170">Cuando se le solicite, proporcione la clave de registro descargada del sitio y complete el registro del host de Hyper-V en el sitio.</span><span class="sxs-lookup"><span data-stu-id="709e3-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="709e3-171">Compruebe que el host de Hyper-V se ha registrado en el sitio mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="709e3-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="709e3-172">Paso 6: Creación de una directiva de replicación y su asociación con el contenedor de protección</span><span class="sxs-lookup"><span data-stu-id="709e3-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="709e3-173">Cree una directiva de replicación como sigue:</span><span class="sxs-lookup"><span data-stu-id="709e3-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="709e3-174">Compruebe el trabajo devuelto para asegurarse de que la creación de la directiva de replicación se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="709e3-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="709e3-175">La cuenta de almacenamiento especificada debe estar en la misma región de Azure que el almacén de Servicios de recuperación y debe tener habilitada la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="709e3-175">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="709e3-176">Si la cuenta de almacenamiento de recuperación especificada es del tipo Almacenamiento de Azure (clásico), la conmutación por error de las máquinas protegidas recupera la máquina en Azure IaaS (clásico).</span><span class="sxs-lookup"><span data-stu-id="709e3-176">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="709e3-177">Si la cuenta de almacenamiento de recuperación especificada es del tipo Almacenamiento de Azure (Azure Resource Manager), la conmutación por error de las máquinas protegidas recupera la máquina en Azure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="709e3-177">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="709e3-178">Obtenga el contenedor de protección correspondiente al sitio; para ello, proceda como sigue:</span><span class="sxs-lookup"><span data-stu-id="709e3-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="709e3-179">Inicie la asociación del contenedor de protección con la directiva de replicación:</span><span class="sxs-lookup"><span data-stu-id="709e3-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="709e3-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="709e3-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="709e3-181">Espere a que el trabajo de asociación se complete y asegúrese de que se ha hecho correctamente.</span><span class="sxs-lookup"><span data-stu-id="709e3-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="709e3-182">Paso 7: Habilitación de la protección para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="709e3-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="709e3-183">Obtenga la entidad de protección correspondiente a la máquina virtual que desea proteger:</span><span class="sxs-lookup"><span data-stu-id="709e3-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="709e3-184">Inicie la protección de la máquina virtual, como sigue:</span><span class="sxs-lookup"><span data-stu-id="709e3-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="709e3-185">La cuenta de almacenamiento especificada debe estar en la misma región de Azure que el almacén de Servicios de recuperación y debe tener habilitada la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="709e3-185">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="709e3-186">Si la cuenta de almacenamiento de recuperación especificada es del tipo Almacenamiento de Azure (clásico), la conmutación por error de las máquinas protegidas recupera la máquina en Azure IaaS (clásico).</span><span class="sxs-lookup"><span data-stu-id="709e3-186">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="709e3-187">Si la cuenta de almacenamiento de recuperación especificada es del tipo Almacenamiento de Azure (Azure Resource Manager), la conmutación por error de las máquinas protegidas recupera la máquina en Azure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="709e3-187">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="709e3-188">Si la máquina virtual que se protege tiene más de un disco conectado, especifique el disco del sistema operativo con el parámetro *OSDiskName* .</span><span class="sxs-lookup"><span data-stu-id="709e3-188">If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="709e3-189">Espere a que las máquinas virtuales lleguen a un estado protegido después de la replicación inicial.</span><span class="sxs-lookup"><span data-stu-id="709e3-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="709e3-190">Esta operación puede tardar unos minutos, en función de factores como el volumen de datos que se van a replicar y el ancho de banda del canal de subida disponible en Azure.</span><span class="sxs-lookup"><span data-stu-id="709e3-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="709e3-191">Los valores State y StateDescription del trabajo se actualizan como se indica a continuación, cuando la máquina virtual alcanza un estado protegido.</span><span class="sxs-lookup"><span data-stu-id="709e3-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="709e3-192">Actualice las propiedades de recuperación, como el tamaño de rol de VM y la red de Azure para asociar a las tarjetas de interfaz de red de la máquina virtual tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="709e3-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

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
        DisplayName      : Update the virtual machine
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



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="709e3-193">Paso 8: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="709e3-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="709e3-194">Ejecute un trabajo de conmutación por error de prueba, como sigue:</span><span class="sxs-lookup"><span data-stu-id="709e3-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="709e3-195">Compruebe que la prueba de la máquina virtual se crea en Azure.</span><span class="sxs-lookup"><span data-stu-id="709e3-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="709e3-196">(El trabajo de conmutación por error de prueba está suspendido, después de crear la máquina virtual de prueba en Azure.</span><span class="sxs-lookup"><span data-stu-id="709e3-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="709e3-197">El trabajo se completa limpiando los artefactos creados al reanudar el trabajo, como se muestra en el paso siguiente).</span><span class="sxs-lookup"><span data-stu-id="709e3-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="709e3-198">Ejecute la conmutación por error de prueba de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="709e3-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="709e3-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="709e3-199">Next Steps</span></span>
<span data-ttu-id="709e3-200">[Más información](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre los cmdlets de PowerShell de Azure Site Recovery con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="709e3-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
