---
title: "Migración a Resource Manager con PowerShell | Microsoft Docs"
description: "Este artículo lo guía a través de la migración de recursos de IaaS compatible con la plataforma de recursos, como máquinas virtuales, redes virtuales y cuentas de almacenamiento del modelo clásico al de Azure Resource Manager mediante comandos de Azure PowerShell."
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
ms.openlocfilehash: 489e6cc6bd3c5b36635f5f7e398d08fed681d2e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="b3554-103">Migración de recursos de IaaS de la implementación clásica a la de Resource Manager con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3554-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="b3554-104">En estos pasos se describe cómo utilizar los comandos de Azure PowerShell para migrar los recursos de infraestructura como servicio (IaaS) desde el modelo de implementación clásica al modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3554-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="b3554-105">Si lo desea, también puede migrar recursos mediante la [interfaz de línea de comandos de Azure (CLI de Azure)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b3554-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="b3554-106">Lea el artículo [Migración compatible con la plataforma de recursos de IaaS del modelo clásico a Azure Resource Manager](migration-classic-resource-manager-overview.md)para obtener información sobre los escenarios de migración que se admiten.</span><span class="sxs-lookup"><span data-stu-id="b3554-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="b3554-107">Si quiere obtener instrucciones detalladas y ver un tutorial de migración, consulte [Profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="b3554-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="b3554-108">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="b3554-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="b3554-109">Este es un diagrama de flujo para identificar el orden en que tienen que ejecutarse durante un proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="b3554-111">Paso 1: Planear la migración</span><span class="sxs-lookup"><span data-stu-id="b3554-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="b3554-112">Estos son algunos de los procedimientos recomendados a la hora de evaluar la migración de recursos de IaaS desde el modelo clásico a Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="b3554-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="b3554-113">Lea el artículo sobre [qué características y configuraciones se admiten y cuáles no](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3554-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="b3554-114">Si tiene máquinas virtuales que usan configuraciones o características no admitidas, se recomienda esperar a que se anuncie dicha compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="b3554-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span></span> <span data-ttu-id="b3554-115">De manera alternativa, si se ajusta a sus necesidades, quite esa característica o salga de esa configuración para habilitar la migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span></span>
* <span data-ttu-id="b3554-116">Si tiene actualmente scripts automatizados que implementan la infraestructura y las aplicaciones, intente crear una configuración de prueba similar usando esos scripts para la migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="b3554-117">También puede configurar entornos de ejemplo mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3554-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3554-118">Las puertas de enlace de aplicaciones no se admiten actualmente para realizar migraciones del modelo clásico al de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3554-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="b3554-119">Si desea migrar una red virtual clásica con una instancia de Application Gateway, quite la puerta de enlace antes de ejecutar una operación de preparación para mover la red.</span><span class="sxs-lookup"><span data-stu-id="b3554-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="b3554-120">Después, cuando termine el proceso de migración, vuelva a conectar la puerta de enlace en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3554-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="b3554-121">Las puertas de enlace de ExpressRoute que se conectan con circuitos de ExpressRoute en otra suscripción no se pueden migrar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b3554-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="b3554-122">En esos casos, quite la puerta de enlace de ExpressRoute, migre la red virtual y vuelva a crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b3554-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="b3554-123">Para obtener más información, consulte [Migración de circuitos de ExpressRoute y las redes virtuales asociadas del modelo de implementación clásica a Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b3554-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="b3554-124">Paso 2: instalar la versión más reciente de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3554-124">Step 2: Install the latest version of Azure PowerShell</span></span>
<span data-ttu-id="b3554-125">Hay dos opciones principales para instalar Azure PowerShell: la [Galería de PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) y el [Instalador de plataforma web (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="b3554-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="b3554-126">WebPI recibe actualizaciones mensuales.</span><span class="sxs-lookup"><span data-stu-id="b3554-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="b3554-127">La galería de PowerShell recibe actualizaciones de forma continua.</span><span class="sxs-lookup"><span data-stu-id="b3554-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="b3554-128">Este artículo se basa en los cmdlets de la versión 2.1.0 de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3554-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="b3554-129">Para ver las instrucciones de instalación, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3554-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-the-subscription-in-azure-portal"></a><span data-ttu-id="b3554-130">Paso 3: Asegurarse de que es un administrador de la suscripción en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b3554-130">Step 3: Ensure that you are an administrator for the subscription in Azure portal</span></span>
<span data-ttu-id="b3554-131">Para realizar esta migración, debe estar agregado como coadministrador de la suscripción en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3554-131">To perform this migration, you must be added as a co-administrator for the subscription in the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="b3554-132">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3554-132">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3554-133">En el menú de concentrador, seleccione **Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="b3554-133">On the Hub menu, select **Subscription**.</span></span> <span data-ttu-id="b3554-134">Si no lo ve, haga clic en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="b3554-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="b3554-135">Busque la entrada de la suscripción adecuada y después examine el campo **MI ROL**.</span><span class="sxs-lookup"><span data-stu-id="b3554-135">Find the appropriate subscription entry, then look at the **MY ROLE** field.</span></span> <span data-ttu-id="b3554-136">Para un coadministrador, el valor debe ser _Administrador de cuenta_.</span><span class="sxs-lookup"><span data-stu-id="b3554-136">For a co-administrator, the value should be _Account admin_.</span></span>

<span data-ttu-id="b3554-137">Si no puede agregar un coadministrador, póngase en contacto con un administrador del servicio o coadministrador de la suscripción para que le agreguen.</span><span class="sxs-lookup"><span data-stu-id="b3554-137">If you are not able to add a co-administrator, then contact a service administrator or co-administrator for the subscription to get yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="b3554-138">Paso 4: Establecimiento de la suscripción y registro para la migración</span><span class="sxs-lookup"><span data-stu-id="b3554-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="b3554-139">En primer lugar, inicie un símbolo del sistema de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3554-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="b3554-140">Para la migración, debe configurar el entorno para el modelo clásico y el de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3554-140">For migration, you need to set up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="b3554-141">Inicie sesión en su cuenta para el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3554-141">Sign in to your account for the Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="b3554-142">Puede encontrar las suscripciones disponibles ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-142">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="b3554-143">Establezca la suscripción de Azure para la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="b3554-143">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="b3554-144">En este ejemplo se establece el nombre de la suscripción predeterminado en **My Azure Subscription** (Mi suscripción de Azure).</span><span class="sxs-lookup"><span data-stu-id="b3554-144">This example sets the default subscription name to **My Azure Subscription**.</span></span> <span data-ttu-id="b3554-145">Reemplace el nombre de la suscripción de ejemplo por el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="b3554-145">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="b3554-146">El registro es un paso que solo se realiza una vez, pero debe hacerlo antes de intentar la migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="b3554-147">Si no se registra, recibirá el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="b3554-147">Without registering, you see the following error message:</span></span>
>
> <span data-ttu-id="b3554-148">*BadRequest: Subscription is not registered for migration* (BadRequest: la suscripción no está registrada para la migración)</span><span class="sxs-lookup"><span data-stu-id="b3554-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="b3554-149">Regístrese con el proveedor de recursos de migración ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b3554-149">Register with the migration resource provider by using the following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="b3554-150">Espere cinco minutos a que finalice el registro.</span><span class="sxs-lookup"><span data-stu-id="b3554-150">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="b3554-151">Puede comprobar el estado de la aprobación con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-151">You can check the status of the approval by using the following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="b3554-152">Asegúrese de que RegistrationState sea `Registered` antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="b3554-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="b3554-153">Ahora inicie sesión en su cuenta para el modelo clásico.</span><span class="sxs-lookup"><span data-stu-id="b3554-153">Now sign in to your account for the classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="b3554-154">Puede encontrar las suscripciones disponibles ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-154">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="b3554-155">Establezca la suscripción de Azure para la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="b3554-155">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="b3554-156">En este ejemplo se establece la suscripción predeterminada en **My Azure Subscription** (Mi suscripción de Azure).</span><span class="sxs-lookup"><span data-stu-id="b3554-156">This example sets the default subscription to **My Azure Subscription**.</span></span> <span data-ttu-id="b3554-157">Reemplace el nombre de la suscripción de ejemplo por el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="b3554-157">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="b3554-158">Paso 5: Verificación para garantizar que dispone de suficientes núcleos de máquina virtual de Azure Resource Manager en la región de Azure de su VNET o implementación actual</span><span class="sxs-lookup"><span data-stu-id="b3554-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="b3554-159">Puede utilizar el siguiente comando de PowerShell para comprobar la cantidad de núcleos que tiene actualmente en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3554-159">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="b3554-160">Para obtener más información sobre las cuotas de núcleos, consulte [Límites y Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="b3554-160">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="b3554-161">En este ejemplo se comprueba la disponibilidad en la región del **oeste de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="b3554-161">This example checks the availability in the **West US** region.</span></span> <span data-ttu-id="b3554-162">Reemplace el nombre de la región de ejemplo por el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="b3554-162">Replace the example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-to-migrate-your-iaas-resources"></a><span data-ttu-id="b3554-163">Paso 6: Ejecución de comandos para migrar los recursos de IaaS</span><span class="sxs-lookup"><span data-stu-id="b3554-163">Step 6: Run commands to migrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="b3554-164">Todas las operaciones que se describen aquí son idempotentes.</span><span class="sxs-lookup"><span data-stu-id="b3554-164">All the operations described here are idempotent.</span></span> <span data-ttu-id="b3554-165">Si tiene un problema diferente de una función no admitida o un error de configuración, se recomienda que vuelva a intentar la operación de preparación, anulación o confirmación.</span><span class="sxs-lookup"><span data-stu-id="b3554-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="b3554-166">La plataforma intenta nuevamente la acción.</span><span class="sxs-lookup"><span data-stu-id="b3554-166">The platform then tries the action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="b3554-167">Paso 6.1: Opción 1: Migración de máquinas virtuales en un servicio en la nube (no en una red virtual)</span><span class="sxs-lookup"><span data-stu-id="b3554-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="b3554-168">Obtenga la lista de servicios en la nube mediante el siguiente comando y seleccione luego el servicio en la nube que quiera migrar.</span><span class="sxs-lookup"><span data-stu-id="b3554-168">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="b3554-169">Si las máquinas virtuales del servicio en la nube están en una red virtual o si tienen roles web o de trabajo, el comando devolverá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="b3554-169">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="b3554-170">Obtenga el nombre de la implementación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="b3554-170">Get the deployment name for the cloud service.</span></span> <span data-ttu-id="b3554-171">En este ejemplo, el nombre de servicio es **My Service** (Mi servicio).</span><span class="sxs-lookup"><span data-stu-id="b3554-171">In this example, the service name is **My Service**.</span></span> <span data-ttu-id="b3554-172">Reemplace el nombre del servicio de ejemplo por el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="b3554-172">Replace the example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="b3554-173">Prepare las máquinas virtuales del servicio en la nube para la migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-173">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="b3554-174">Tiene dos opciones para elegir.</span><span class="sxs-lookup"><span data-stu-id="b3554-174">You have two options to choose from.</span></span>

* <span data-ttu-id="b3554-175">**Opción 1. Migrar las máquinas virtuales a una red virtual creada en una plataforma**</span><span class="sxs-lookup"><span data-stu-id="b3554-175">**Option 1. Migrate the VMs to a platform-created virtual network**</span></span>

    <span data-ttu-id="b3554-176">Primero, valide si puede migrar el servicio en la nube con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b3554-176">First, validate if you can migrate the cloud service using the following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="b3554-177">El comando anterior muestra cualquier advertencia y error que bloquee la migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-177">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="b3554-178">Si la validación se realiza correctamente, podrá pasar al siguiente paso de **preparación**:</span><span class="sxs-lookup"><span data-stu-id="b3554-178">If validation is successful, then you can move on to the **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="b3554-179">**Opción 2. Migrar a una red virtual existente en el modelo de implementación de Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="b3554-179">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span></span>

    <span data-ttu-id="b3554-180">En este ejemplo se establece el nombre del grupo de recursos en **myResourceGroup**, el nombre de red virtual en **myVirtualNetwork** y el nombre de la subred en **mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="b3554-180">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span></span> <span data-ttu-id="b3554-181">Reemplace los nombres del ejemplo por los nombres de sus propios recursos.</span><span class="sxs-lookup"><span data-stu-id="b3554-181">Replace the names in the example with the names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="b3554-182">En primer lugar, valide si puede migrar la red virtual con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-182">First, validate if you can migrate the virtual network using the following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="b3554-183">El comando anterior muestra cualquier advertencia y error que bloquee la migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-183">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="b3554-184">Si la validación se realiza correctamente, podrá continuar al siguiente paso de preparación:</span><span class="sxs-lookup"><span data-stu-id="b3554-184">If validation is successful, then you can proceed with the following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="b3554-185">Cuando la operación de preparación finalice correctamente con cualquiera de las opciones anteriores, consulte el estado de la migración de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b3554-185">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span></span> <span data-ttu-id="b3554-186">Asegúrese de que tienen el estado `Prepared` .</span><span class="sxs-lookup"><span data-stu-id="b3554-186">Ensure that they are in the `Prepared` state.</span></span>

<span data-ttu-id="b3554-187">En este ejemplo se establece el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="b3554-187">This example sets the VM name to **myVM**.</span></span> <span data-ttu-id="b3554-188">Reemplace el nombre del ejemplo por su propio nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b3554-188">Replace the example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="b3554-189">Compruebe la configuración de los recursos preparados mediante PowerShell o el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3554-189">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span></span> <span data-ttu-id="b3554-190">Si no está preparado para la migración y desea volver al estado anterior, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-190">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="b3554-191">Si la configuración preparada parece correcta, puede continuar y confirmar los recursos mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-191">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="b3554-192">Paso 6.1: Opción 2: Migración de máquinas virtuales en una red virtual</span><span class="sxs-lookup"><span data-stu-id="b3554-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="b3554-193">Para migrar máquinas virtuales de una red virtual, migre la red virtual.</span><span class="sxs-lookup"><span data-stu-id="b3554-193">To migrate virtual machines in a virtual network, you migrate the virtual network.</span></span> <span data-ttu-id="b3554-194">Las máquinas virtuales se migran automáticamente con la red virtual.</span><span class="sxs-lookup"><span data-stu-id="b3554-194">The virtual machines automatically migrate with the virtual network.</span></span> <span data-ttu-id="b3554-195">Seleccione la red virtual que quiere migrar.</span><span class="sxs-lookup"><span data-stu-id="b3554-195">Pick the virtual network that you want to migrate.</span></span>
> [!NOTE]
> <span data-ttu-id="b3554-196">[Migre una sola máquina virtual clásica](migrate-single-classic-to-resource-manager.md) creando una nueva máquina virtual de Resource Manager con discos administrados mediante los archivos de VHD (SO y datos) de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b3554-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="b3554-197">El nombre de red virtual podría ser diferente del que se muestra en el nuevo Portal.</span><span class="sxs-lookup"><span data-stu-id="b3554-197">The virtual network name might be different from what is shown in the new Portal.</span></span> <span data-ttu-id="b3554-198">El nuevo Azure Portal muestra el nombre como `[vnet-name]` pero el nombre de red virtual real es de tipo `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="b3554-198">The new Azure Portal displays the name as `[vnet-name]` but the actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="b3554-199">Antes de migrar, busque el nombre real de la red virtual con el comando `Get-AzureVnetSite | Select -Property Name` o consúltelo en el antiguo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b3554-199">Before migrating, lookup the actual virtual network name using the command `Get-AzureVnetSite | Select -Property Name` or view it in the old Azure Portal.</span></span> 

<span data-ttu-id="b3554-200">En este ejemplo se establece el nombre de red virtual en **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="b3554-200">This example sets the virtual network name to **myVnet**.</span></span> <span data-ttu-id="b3554-201">Reemplace el nombre de la red virtual de ejemplo por el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="b3554-201">Replace the example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="b3554-202">Si la red virtual contiene roles web o de trabajo, o bien máquinas virtuales con configuraciones no admitidas, recibe un mensaje de error de validación.</span><span class="sxs-lookup"><span data-stu-id="b3554-202">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="b3554-203">En primer lugar, valide si puede migrar la red virtual con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-203">First, validate if you can migrate the virtual network by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="b3554-204">El comando anterior muestra cualquier advertencia y error que bloquee la migración.</span><span class="sxs-lookup"><span data-stu-id="b3554-204">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="b3554-205">Si la validación se realiza correctamente, podrá continuar al siguiente paso de preparación:</span><span class="sxs-lookup"><span data-stu-id="b3554-205">If validation is successful, then you can proceed with the following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="b3554-206">Compruebe la configuración de las máquinas virtuales preparadas mediante Azure PowerShell o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b3554-206">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="b3554-207">Si no está preparado para la migración y desea volver al estado anterior, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-207">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="b3554-208">Si la configuración preparada parece correcta, puede continuar y confirmar los recursos mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-208">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="b3554-209">Paso 6.2: Migración de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b3554-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="b3554-210">Cuando haya terminado de migrar las máquinas virtuales, se recomienda migrar las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3554-210">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span></span>

<span data-ttu-id="b3554-211">Antes de migrar la cuenta de almacenamiento, lleve a cabo las comprobaciones de requisitos previos anteriores:</span><span class="sxs-lookup"><span data-stu-id="b3554-211">Before you migrate the storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="b3554-212">**Migración de máquinas virtuales clásicas cuyos discos se almacenan en la cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="b3554-212">**Migrate classic virtual machines whose disks are stored in the storage account**</span></span>

    <span data-ttu-id="b3554-213">El comando anterior devuelve las propiedades RoleName y DiskName de todos los discos de máquinas virtuales clásicas en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3554-213">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span></span> <span data-ttu-id="b3554-214">RoleName es el nombre de la máquina virtual a la que está conectado el disco.</span><span class="sxs-lookup"><span data-stu-id="b3554-214">RoleName is the name of the virtual machine to which a disk is attached.</span></span> <span data-ttu-id="b3554-215">Si el comando anterior devuelve discos, asegúrese de que las máquinas virtuales a las que están conectados estos discos se migraron antes de migrar la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3554-215">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="b3554-216">**Eliminación de discos de máquinas virtuales clásicas almacenados en la cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="b3554-216">**Delete unattached classic VM disks stored in the storage account**</span></span>

    <span data-ttu-id="b3554-217">Busque discos de máquinas virtual es clásicas en la cuenta de almacenamiento con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b3554-217">Find unattached classic VM disks in the storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="b3554-218">Si el comando anterior devuelve discos, elimínelos con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b3554-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="b3554-219">**Eliminación de imágenes de máquinas virtuales almacenadas en la cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="b3554-219">**Delete VM images stored in the storage account**</span></span>

    <span data-ttu-id="b3554-220">El comando anterior devuelve todas las imágenes de máquinas virtuales con el disco de SO almacenado en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3554-220">Preceding command returns all the VM images with OS disk stored in the storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="b3554-221">El comando anterior devuelve todas las imágenes de máquinas virtuales con discos de datos almacenados en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3554-221">Preceding command returns all the VM images with data disks stored in the storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="b3554-222">Elimine todas las imágenes de máquinas virtuales que se devolvieron usando el comando anterior:</span><span class="sxs-lookup"><span data-stu-id="b3554-222">Delete all the VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="b3554-223">Valide cada cuenta de almacenamiento para la migración mediante el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b3554-223">Validate each storage account for migration by using the following command.</span></span> <span data-ttu-id="b3554-224">En este ejemplo, el nombre de cuenta de almacenamiento es **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="b3554-224">In this example, the storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="b3554-225">Reemplace el nombre de ejemplo por el nombre de su propia cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b3554-225">Replace the example name with the name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="b3554-226">El paso siguiente consiste en preparar la cuenta de almacenamiento para la migración</span><span class="sxs-lookup"><span data-stu-id="b3554-226">Next step is to Prepare the storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="b3554-227">Compruebe la configuración de la cuenta de almacenamiento preparada mediante Azure PowerShell o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b3554-227">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="b3554-228">Si no está preparado para la migración y desea volver al estado anterior, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-228">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="b3554-229">Si la configuración preparada parece correcta, puede continuar y confirmar los recursos mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3554-229">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="b3554-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3554-230">Next steps</span></span>
* [<span data-ttu-id="b3554-231">Información general sobre la migración compatible con la plataforma de recursos de IaaS desde el modelo de implementación clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3554-231">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b3554-232">Profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3554-232">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="b3554-233">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Planificación de la migración de recursos de IaaS del modelo clásico a Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="b3554-233">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="b3554-234">Migración de recursos de IaaS de la implementación clásica a Azure Resource Manager con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b3554-234">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b3554-235">Herramientas de la comunidad para ayudar con la migración de recursos de IaaS de la versión clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3554-235">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b3554-236">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="b3554-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b3554-237">Revisión de las preguntas más frecuentes acerca de cómo migrar recursos de IaaS de la versión clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3554-237">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
