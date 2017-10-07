---
title: aaaMigrate tooResource Manager con PowerShell | Documentos de Microsoft
description: "Este artículo le guía a través de migración de hello admitida por la plataforma de recursos de IaaS, como máquinas virtuales (VM) y redes virtuales (Vnet), las cuentas de almacenamiento de tooAzure clásico Resource Manager (ARM) mediante el uso de comandos de PowerShell de Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="e8565-103">Migrar recursos de IaaS de tooAzure clásico Administrador de recursos mediante el uso de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="e8565-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="e8565-104">Estos pasos muestra cómo toouse Azure PowerShell comandos toomigrate infraestructura como un recurso de servicio (IaaS) de modelo de implementación de Azure Resource Manager de toohello modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="e8565-105">Si lo desea, también puede migrar recursos mediante el uso de hello [interfaz de línea de comandos de Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e8565-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="e8565-106">Para obtener información sobre escenarios de migración admitidos, consulte [admitida por la plataforma de la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8565-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="e8565-107">Para obtener instrucciones detalladas y una guía de migración, consulte [técnica exhaustiva sobre la migración admitida por la plataforma de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="e8565-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="e8565-108">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="e8565-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="e8565-109">Este es un orden de hello tooidentify de diagrama de flujo en el que es necesario pasos toobe ejecutado durante un proceso de migración</span><span class="sxs-lookup"><span data-stu-id="e8565-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Captura de pantalla que muestra los pasos de migración de Hola](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="e8565-111">Paso 1: Planear la migración</span><span class="sxs-lookup"><span data-stu-id="e8565-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="e8565-112">Estas son algunas prácticas recomendadas que se recomienda evaluar migrar recursos de IaaS de tooResource clásico Manager:</span><span class="sxs-lookup"><span data-stu-id="e8565-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="e8565-113">Lea hello [admiten y cuáles no características y configuraciones](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8565-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="e8565-114">Si tiene máquinas virtuales que usan configuraciones no admitidas o características, se recomienda que espere Hola configuración o característica Compatibilidad con toobe anunciado.</span><span class="sxs-lookup"><span data-stu-id="e8565-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="e8565-115">O bien, si se adapte a sus necesidades, quitar esa característica o salir de que la migración de configuración tooenable.</span><span class="sxs-lookup"><span data-stu-id="e8565-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="e8565-116">Si han automatizado las secuencias de comandos que implementan la infraestructura y las aplicaciones de hoy en día, intente toocreate un programa de instalación de prueba similar con esos scripts para la migración.</span><span class="sxs-lookup"><span data-stu-id="e8565-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="e8565-117">Como alternativa, puede configurar entornos de ejemplo mediante el uso de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8565-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8565-118">Las puertas de enlace de la aplicación no se admiten actualmente para la migración de clásico tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="e8565-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="e8565-119">toomigrate una red virtual clásica con una puerta de enlace de aplicaciones, quitar la puerta de enlace de hello antes de ejecutar una red de Hola de toomove de operación de preparación.</span><span class="sxs-lookup"><span data-stu-id="e8565-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="e8565-120">Después de completar la migración de hello, vuelva a conectar la puerta de enlace de hello en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8565-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="e8565-121">Conectar los circuitos tooExpressRoute en otra suscripción de puertas de enlace de ExpressRoute no se pueden migrar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e8565-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="e8565-122">En tales casos, quite la puerta de enlace de ExpressRoute de hello, migrar la red virtual de Hola y vuelva a puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="e8565-123">Vea [ExpressRoute migrar circuitos y asociado redes virtuales de modelo de implementación de administrador de recursos de hello toohello clásico](../../expressroute/expressroute-migration-classic-resource-manager.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e8565-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="e8565-124">Paso 2: Instalar la versión más reciente de Hola de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="e8565-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="e8565-125">Hay dos opciones principales tooinstall PowerShell de Azure: [Galería de PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) o [instalador de plataforma Web (WPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="e8565-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="e8565-126">WebPI recibe actualizaciones mensuales.</span><span class="sxs-lookup"><span data-stu-id="e8565-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="e8565-127">La galería de PowerShell recibe actualizaciones de forma continua.</span><span class="sxs-lookup"><span data-stu-id="e8565-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="e8565-128">Este artículo se basa en los cmdlets de la versión 2.1.0 de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8565-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="e8565-129">Para obtener instrucciones de instalación, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8565-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="e8565-130">Paso 3: Asegúrese de que un administrador para la suscripción de hello en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e8565-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="e8565-131">tooperform esta migración, se debe agregar como Coadministrador de suscripción de Hola Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8565-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="e8565-132">Inicio de sesión en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8565-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e8565-133">En el menú del concentrador hello, seleccione **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="e8565-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="e8565-134">Si no lo ve, haga clic en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="e8565-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="e8565-135">Buscar entrada de suscripción adecuado de Hola y después examine hello **mi rol** campo.</span><span class="sxs-lookup"><span data-stu-id="e8565-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="e8565-136">De un Coadministrador, debe ser el valor de hello _Administrador de la cuenta_.</span><span class="sxs-lookup"><span data-stu-id="e8565-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="e8565-137">Si no es capaz de tooadd un Coadministrador, a continuación, póngase en contacto con un administrador de servicios o Coadministrador para hello suscripción tooget usted mismo agregado.</span><span class="sxs-lookup"><span data-stu-id="e8565-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="e8565-138">Paso 4: Establecimiento de la suscripción y registro para la migración</span><span class="sxs-lookup"><span data-stu-id="e8565-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="e8565-139">En primer lugar, inicie un símbolo del sistema de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8565-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="e8565-140">Para la migración, necesita tooset del entorno para ambos clásico y Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e8565-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="e8565-141">Inicie sesión en la cuenta de tooyour para el modelo de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="e8565-142">Obtener suscripciones disponibles hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="e8565-143">Establecer la suscripción de Azure para hello sesión actual.</span><span class="sxs-lookup"><span data-stu-id="e8565-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="e8565-144">Este ejemplo establece Hola nombre de la suscripción predeterminada demasiado**mi suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="e8565-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="e8565-145">Reemplace el nombre de suscripción de ejemplo de Hola por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="e8565-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="e8565-146">El registro es un paso que solo se realiza una vez, pero debe hacerlo antes de intentar la migración.</span><span class="sxs-lookup"><span data-stu-id="e8565-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="e8565-147">Sin registrar, vea Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="e8565-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="e8565-148">*BadRequest: Subscription is not registered for migration* (BadRequest: la suscripción no está registrada para la migración)</span><span class="sxs-lookup"><span data-stu-id="e8565-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="e8565-149">Registrar con el proveedor de recursos de migración de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="e8565-150">Espere cinco minutos para toofinish de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e8565-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="e8565-151">Puede comprobar el estado de Hola de aprobación de hello mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="e8565-152">Asegúrese de que RegistrationState sea `Registered` antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="e8565-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="e8565-153">Ahora, inicie sesión en tooyour cuenta para el modelo clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="e8565-154">Obtener suscripciones disponibles hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="e8565-155">Establecer la suscripción de Azure para hello sesión actual.</span><span class="sxs-lookup"><span data-stu-id="e8565-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="e8565-156">Este ejemplo establece suscripción predeterminada de hello demasiado**mi suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="e8565-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="e8565-157">Reemplace el nombre de suscripción de ejemplo de Hola por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="e8565-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="e8565-158">Paso 5: Asegúrese de que tiene suficientes núcleos de máquina Virtual de Azure Resource Manager Hola región de Azure de su implementación actual o la red virtual</span><span class="sxs-lookup"><span data-stu-id="e8565-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="e8565-159">Puede usar Hola siguiente PowerShell comando toocheck Hola actual número de núcleos que tiene en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8565-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="e8565-160">toolearn más información acerca de las cuotas de núcleo, consulte [hello Azure Resource Manager y límites](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="e8565-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="e8565-161">Este ejemplo comprueba la disponibilidad de Hola Hola **West US** región.</span><span class="sxs-lookup"><span data-stu-id="e8565-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="e8565-162">Reemplace el nombre de región de ejemplo de Hola por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="e8565-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="e8565-163">Paso 6: Ejecutar comandos toomigrate los recursos de IaaS</span><span class="sxs-lookup"><span data-stu-id="e8565-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="e8565-164">Todas las operaciones de hello descritas aquí son idempotentes.</span><span class="sxs-lookup"><span data-stu-id="e8565-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="e8565-165">Si tiene un problema que no sea una característica no compatible o un error de configuración, se recomienda que vuelva a intentar Hola preparar, anular o confirmar la operación.</span><span class="sxs-lookup"><span data-stu-id="e8565-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="e8565-166">plataforma de Hello, a continuación, intenta volver a la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="e8565-167">Paso 6.1: Opción 1: Migración de máquinas virtuales en un servicio en la nube (no en una red virtual)</span><span class="sxs-lookup"><span data-stu-id="e8565-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="e8565-168">Hola obtención de una lista de servicios en la nube mediante el uso de hello siguiente comando y, a continuación, servicio de nube de Hola de selección que desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="e8565-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="e8565-169">Si hello las máquinas virtuales en el servicio de nube de Hola se encuentran en una red virtual o si tienen roles web o de trabajo, el comando de hello devuelve un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="e8565-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="e8565-170">Obtener nombre de la implementación de Hola Hola servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="e8565-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="e8565-171">En este ejemplo, es el nombre del servicio de hello **mi servicio**.</span><span class="sxs-lookup"><span data-stu-id="e8565-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="e8565-172">Reemplace el nombre de servicio de ejemplo de Hola con su propio nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="e8565-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="e8565-173">Preparar las máquinas virtuales de Hola Hola del servicio en nube para la migración.</span><span class="sxs-lookup"><span data-stu-id="e8565-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="e8565-174">Tiene dos toochoose de opciones de.</span><span class="sxs-lookup"><span data-stu-id="e8565-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="e8565-175">**Opción 1. Migrar la red virtual para crear plataforma tooa de máquinas virtuales Hola**</span><span class="sxs-lookup"><span data-stu-id="e8565-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="e8565-176">En primer lugar, validar si puede migrar servicio en la nube hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e8565-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="e8565-177">Hello comando anterior muestra las advertencias y los errores que bloquear la migración.</span><span class="sxs-lookup"><span data-stu-id="e8565-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="e8565-178">Si la validación es correcta, puede mover en toohello **preparar** paso:</span><span class="sxs-lookup"><span data-stu-id="e8565-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="e8565-179">**Opción 2. Migrar tooan de red virtual existente en el modelo de implementación del Administrador de recursos de Hola**</span><span class="sxs-lookup"><span data-stu-id="e8565-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="e8565-180">Este ejemplo establece Hola nombre del grupo de recursos demasiado**myResourceGroup**, Hola nombre de red virtual demasiado**myVirtualNetwork** y Hola nombre de subred demasiado**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="e8565-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="e8565-181">Reemplazar nombres de hello en el ejemplo de Hola con nombres Hola de sus propios recursos.</span><span class="sxs-lookup"><span data-stu-id="e8565-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="e8565-182">En primer lugar, validar si se puede migrar la red virtual de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="e8565-183">Hello comando anterior muestra las advertencias y los errores que bloquear la migración.</span><span class="sxs-lookup"><span data-stu-id="e8565-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="e8565-184">Si la validación es correcta, puede continuar con hello siguiendo el paso de preparación:</span><span class="sxs-lookup"><span data-stu-id="e8565-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="e8565-185">Después de hello operación de preparación se realiza correctamente con cualquiera de hello anterior opciones, consultar el estado de migración de Hola de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e8565-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="e8565-186">Asegúrese de que se encuentran en hello `Prepared` estado.</span><span class="sxs-lookup"><span data-stu-id="e8565-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="e8565-187">Este ejemplo establece Hola nombre de máquina virtual demasiado**myVM**.</span><span class="sxs-lookup"><span data-stu-id="e8565-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="e8565-188">Reemplace el nombre de ejemplo de Hola con su propio nombre de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e8565-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="e8565-189">Comprobar la configuración de Hola para hello preparado recursos con PowerShell u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8565-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="e8565-190">Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="e8565-191">Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e8565-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="e8565-192">Paso 6.1: Opción 2: Migración de máquinas virtuales en una red virtual</span><span class="sxs-lookup"><span data-stu-id="e8565-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="e8565-193">toomigrate las máquinas virtuales en una red virtual, se migra la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="e8565-194">máquinas virtuales de Hello migrar automáticamente con la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="e8565-195">Selección Hola red virtual que desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="e8565-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="e8565-196">[Migrar máquina virtual solo en clásico](migrate-single-classic-to-resource-manager.md) mediante la creación de una nueva máquina virtual de administrador de recursos con discos administrados utilizando los archivos de (sistema operativo y datos) de disco duro virtual Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="e8565-197">nombre de red virtual de Hello puede ser diferente de lo que se muestra en hello nuevo Portal.</span><span class="sxs-lookup"><span data-stu-id="e8565-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="e8565-198">nuevo Portal de Azure Hello muestra nombre hello como `[vnet-name]` nombre de red virtual real de hello es del tipo `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="e8565-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="e8565-199">Antes de migrar, nombre de red virtual real de Hola de búsqueda con el comando de hello `Get-AzureVnetSite | Select -Property Name` o verlo en hello antiguo Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8565-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="e8565-200">Este ejemplo establece Hola nombre de red virtual demasiado**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="e8565-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="e8565-201">Reemplace el nombre de red virtual de ejemplo de Hola por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="e8565-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="e8565-202">Si la red virtual de Hola contiene web o roles de trabajo o máquinas virtuales con las configuraciones no compatibles, obtendrá un mensaje de error de validación.</span><span class="sxs-lookup"><span data-stu-id="e8565-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="e8565-203">En primer lugar, validar si se puede migrar la red virtual de hello usando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e8565-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="e8565-204">Hello comando anterior muestra las advertencias y los errores que bloquear la migración.</span><span class="sxs-lookup"><span data-stu-id="e8565-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="e8565-205">Si la validación es correcta, puede continuar con hello siguiendo el paso de preparación:</span><span class="sxs-lookup"><span data-stu-id="e8565-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="e8565-206">Comprobar la configuración de Hola para hello preparado máquinas virtuales mediante el uso de PowerShell de Azure u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8565-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="e8565-207">Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="e8565-208">Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e8565-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="e8565-209">Paso 6.2: Migración de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e8565-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="e8565-210">Una vez que haya terminado la migración de máquinas virtuales hello, se recomienda que migrar las cuentas de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="e8565-211">Antes de migrar cuentas de almacenamiento de hello, lleve a cabo anteriores comprobaciones de requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="e8565-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="e8565-212">**Migrar máquinas virtuales clásicas cuyos discos se almacenan en la cuenta de almacenamiento de Hola**</span><span class="sxs-lookup"><span data-stu-id="e8565-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="e8565-213">Anterior comando devuelve RoleName y DiskName de las propiedades de todos los discos de máquina virtual clásicas de hello en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="e8565-214">RoleName es nombre de Hola de hello toowhich de máquina virtual que un disco está conectado.</span><span class="sxs-lookup"><span data-stu-id="e8565-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="e8565-215">Si precede el comando devuelve los discos, a continuación, asegúrese de que toowhich de máquinas virtuales estos discos conectados se migran antes de migrar Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e8565-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="e8565-216">**Eliminar adjuntas clásicos discos de máquina virtual almacenados en la cuenta de almacenamiento de Hola**</span><span class="sxs-lookup"><span data-stu-id="e8565-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="e8565-217">Buscar adjuntas clásicos discos de máquina virtual en el almacenamiento de hello cuenta mediante comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e8565-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="e8565-218">Si el comando anterior devuelve discos, elimínelos con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e8565-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="e8565-219">**Eliminar imágenes de máquina virtual almacenadas en la cuenta de almacenamiento de Hola**</span><span class="sxs-lookup"><span data-stu-id="e8565-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="e8565-220">Anterior comando devuelve todas las imágenes de máquina virtual de hello con disco del sistema operativo almacenado en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="e8565-221">Anterior comando devuelve todas las imágenes de máquina virtual de hello con discos de datos almacenados en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8565-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="e8565-222">Eliminar todas las imágenes de máquina virtual de hello devueltos por encima de comandos mediante el comando anterior:</span><span class="sxs-lookup"><span data-stu-id="e8565-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="e8565-223">Validar cada cuenta de almacenamiento para la migración mediante Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="e8565-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="e8565-224">En este ejemplo, es el nombre de cuenta de almacenamiento de hello **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="e8565-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="e8565-225">Sustituir el nombre de ejemplo de Hola por Hola de su propia cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e8565-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="e8565-226">Siguiente paso es la cuenta de almacenamiento de hello tooPrepare para la migración</span><span class="sxs-lookup"><span data-stu-id="e8565-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="e8565-227">Comprobar la configuración de Hola para hello preparado cuenta de almacenamiento mediante el uso de PowerShell de Azure u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8565-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="e8565-228">Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e8565-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="e8565-229">Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e8565-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="e8565-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e8565-230">Next steps</span></span>
* [<span data-ttu-id="e8565-231">Información general de migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="e8565-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e8565-232">Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="e8565-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e8565-233">Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="e8565-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e8565-234">Usar recursos de IaaS CLI toomigrate de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="e8565-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e8565-235">Herramientas de la Comunidad para ayudar con la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="e8565-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e8565-236">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="e8565-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e8565-237">Hola de revisión más preguntas más frecuentes acerca de cómo migrar recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="e8565-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
