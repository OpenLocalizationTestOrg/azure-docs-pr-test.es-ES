---
title: "Migración de VM a Resource Manager mediante la CLI de Azure | Microsoft Docs"
description: "Este artículo le guía por los pasos de migración de recursos compatible con la plataforma desde el modelo de implementación clásica hasta Azure Resource Manager mediante la CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: a63d758570b09b37b8e51c639267f729521d9ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="55ed6-103">Migración de recursos de IaaS de la implementación clásica a Azure Resource Manager con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="55ed6-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="55ed6-104">En estos pasos se describe cómo utilizar los comandos de la interfaz de la línea de comandos (CLI) de Azure para migrar recursos de infraestructura como servicio (IaaS) del modelo de implementación clásica al modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55ed6-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="55ed6-105">El artículo requiere la [CLI de Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="55ed6-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="55ed6-106">Todas las operaciones que se describen aquí son idempotentes.</span><span class="sxs-lookup"><span data-stu-id="55ed6-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="55ed6-107">Si tiene un problema diferente de una función no admitida o un error de configuración, se recomienda que vuelva a intentar la operación de preparación, anulación o confirmación.</span><span class="sxs-lookup"><span data-stu-id="55ed6-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="55ed6-108">De ese modo, la plataforma intentará de nuevo la acción.</span><span class="sxs-lookup"><span data-stu-id="55ed6-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="55ed6-109">Este es un diagrama de flujo para identificar el orden en que tienen que ejecutarse durante un proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="55ed6-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="55ed6-111">Paso 1: Preparación para la migración</span><span class="sxs-lookup"><span data-stu-id="55ed6-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="55ed6-112">Estos son algunos de los procedimientos recomendados a la hora de evaluar la migración de recursos de IaaS desde el modelo clásico a Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="55ed6-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="55ed6-113">Consulte la [lista de configuraciones o características no admitidas](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55ed6-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="55ed6-114">Si tiene máquinas virtuales que usan configuraciones o características no admitidas, se recomienda esperar a que se anuncie dicha compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="55ed6-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="55ed6-115">Como alternativa, puede quitar esa característica o salir de esa configuración para habilitar la migración si se ajusta a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="55ed6-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="55ed6-116">Si tiene actualmente scripts automatizados que implementan la infraestructura y las aplicaciones, intente crear una configuración de prueba similar usando esos scripts para la migración.</span><span class="sxs-lookup"><span data-stu-id="55ed6-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="55ed6-117">También puede configurar entornos de ejemplo mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="55ed6-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55ed6-118">Las puertas de enlace de aplicaciones no se admiten actualmente para realizar migraciones del modelo clásico al de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55ed6-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="55ed6-119">Si desea migrar una red virtual clásica con una instancia de Application Gateway, quite la puerta de enlace antes de ejecutar una operación de preparación para mover la red.</span><span class="sxs-lookup"><span data-stu-id="55ed6-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="55ed6-120">Después, cuando termine el proceso de migración, vuelva a conectar la puerta de enlace en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55ed6-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="55ed6-121">Las puertas de enlace de ExpressRoute que se conectan con circuitos de ExpressRoute en otra suscripción no se pueden migrar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="55ed6-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="55ed6-122">En esos casos, quite la puerta de enlace de ExpressRoute, migre la red virtual y vuelva a crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="55ed6-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="55ed6-123">Para obtener más información, consulte [Migración de circuitos de ExpressRoute y las redes virtuales asociadas del modelo de implementación clásica a Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="55ed6-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="55ed6-124">Paso 2: Establecimiento de la suscripción y registro del proveedor</span><span class="sxs-lookup"><span data-stu-id="55ed6-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="55ed6-125">Para los escenarios de migración, debe configurar el entorno para el modelo clásico y el de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55ed6-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="55ed6-126">[Instale la CLI de Azure](../../cli-install-nodejs.md) y [seleccione la suscripción](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="55ed6-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="55ed6-127">Inicie sesión en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="55ed6-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="55ed6-128">Seleccione la suscripción de Azure con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="55ed6-129">El registro es un paso que solo se realiza una vez pero que es necesario antes de intentar la migración.</span><span class="sxs-lookup"><span data-stu-id="55ed6-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="55ed6-130">Si no se registra, verá el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="55ed6-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="55ed6-131">*BadRequest: Subscription is not registered for migration* (BadRequest: la suscripción no está registrada para la migración)</span><span class="sxs-lookup"><span data-stu-id="55ed6-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="55ed6-132">Regístrese con el proveedor de recursos de migración mediante el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="55ed6-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="55ed6-133">Tenga en cuenta que, en algunos casos, se agota el tiempo de espera de este comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-133">Note that in some cases, this command times out.</span></span> <span data-ttu-id="55ed6-134">Sin embargo, el registro se realizará correctamente.</span><span class="sxs-lookup"><span data-stu-id="55ed6-134">However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="55ed6-135">Espere cinco minutos a que finalice el registro.</span><span class="sxs-lookup"><span data-stu-id="55ed6-135">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="55ed6-136">Puede comprobar el estado de la aprobación con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-136">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="55ed6-137">Asegúrese de que RegistrationState sea `Registered` antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="55ed6-137">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="55ed6-138">Ahora cambie CLI al modo `asm` .</span><span class="sxs-lookup"><span data-stu-id="55ed6-138">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="55ed6-139">Paso 3: Verificación para garantizar que dispone de suficientes núcleos de máquina virtual de Azure Resource Manager en la región de Azure de su VNET o implementación actual</span><span class="sxs-lookup"><span data-stu-id="55ed6-139">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="55ed6-140">Para este paso debe cambiar a modo `arm` .</span><span class="sxs-lookup"><span data-stu-id="55ed6-140">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="55ed6-141">Para ello, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-141">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="55ed6-142">Puede utilizar el siguiente comando de CLI para comprobar la cantidad de núcleos que tiene actualmente en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55ed6-142">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="55ed6-143">Para más información sobre las cuotas de núcleos, consulte [Límites y Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="55ed6-143">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="55ed6-144">Una vez comprobado este paso, puede volver a cambiar a modo `asm` .</span><span class="sxs-lookup"><span data-stu-id="55ed6-144">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="55ed6-145">Paso 4: Opción 1: Migración de máquinas virtuales de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="55ed6-145">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="55ed6-146">Obtenga la lista de servicios en la nube mediante el siguiente comando y seleccione luego el servicio en la nube que quiera migrar.</span><span class="sxs-lookup"><span data-stu-id="55ed6-146">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="55ed6-147">Tenga en cuenta que si las máquinas virtuales del servicio en la nube están en una red virtual o tienen roles web o de trabajo, recibirá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="55ed6-147">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="55ed6-148">Ejecute el siguiente comando para obtener el nombre de la implementación del servicio en la nube desde la salida detallada.</span><span class="sxs-lookup"><span data-stu-id="55ed6-148">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="55ed6-149">En la mayoría de los casos, el nombre de la implementación es el mismo que el nombre del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="55ed6-149">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="55ed6-150">Primero, valide si puede migrar el servicio en la nube con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="55ed6-150">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="55ed6-151">Prepare las máquinas virtuales del servicio en la nube para la migración.</span><span class="sxs-lookup"><span data-stu-id="55ed6-151">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="55ed6-152">Tiene dos opciones para elegir.</span><span class="sxs-lookup"><span data-stu-id="55ed6-152">You have two options to choose from.</span></span>

<span data-ttu-id="55ed6-153">Si quiere migrar las máquinas virtuales a una red virtual creada en una plataforma, use el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-153">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="55ed6-154">Si quiere migrar a una red virtual existente en el modelo de implementación de Resource Manager, utilice el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-154">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="55ed6-155">Una vez finalizada la operación de preparación, puede consultar la salida detallada para obtener el estado de migración de las máquinas virtuales y asegurarse de que están en estado `Prepared` .</span><span class="sxs-lookup"><span data-stu-id="55ed6-155">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="55ed6-156">Compruebe la configuración de los recursos preparados mediante la CLI o el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="55ed6-156">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="55ed6-157">Si no está preparado para la migración y desea volver al estado anterior, utilice el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-157">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="55ed6-158">Si la configuración preparada parece correcta, puede continuar y confirmar los recursos mediante el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-158">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="55ed6-159">Paso 4: Opción 2: Migración de máquinas virtuales de una red virtual</span><span class="sxs-lookup"><span data-stu-id="55ed6-159">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="55ed6-160">Seleccione la red virtual que quiere migrar.</span><span class="sxs-lookup"><span data-stu-id="55ed6-160">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="55ed6-161">Tenga en cuenta que si la red virtual contiene roles web o de trabajo, o bien máquinas virtuales con configuraciones no admitidas, recibirá un mensaje de error de validación.</span><span class="sxs-lookup"><span data-stu-id="55ed6-161">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="55ed6-162">Obtenga todas las redes virtuales de la suscripción con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-162">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="55ed6-163">El resultado tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="55ed6-163">The output will look something like this:</span></span>

![Captura de pantalla de la línea de comandos con todo el nombre de red virtual resaltado.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="55ed6-165">En el ejemplo anterior, **virtualNetworkName** es el nombre entero **"Group classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="55ed6-165">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="55ed6-166">En primer lugar, valide si puede migrar la red virtual con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="55ed6-166">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="55ed6-167">Prepare la red virtual de su elección para la migración mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="55ed6-167">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="55ed6-168">Compruebe la configuración de las máquinas virtuales preparadas mediante la CLI o el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="55ed6-168">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="55ed6-169">Si no está preparado para la migración y desea volver al estado anterior, utilice el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-169">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="55ed6-170">Si la configuración preparada parece correcta, puede continuar y confirmar los recursos mediante el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-170">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="55ed6-171">Paso 5: Migración de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="55ed6-171">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="55ed6-172">Cuando haya terminado de migrar las máquinas virtuales, se recomienda migrar la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="55ed6-172">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="55ed6-173">Prepare la cuenta de almacenamiento para la migración mediante el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-173">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="55ed6-174">Compruebe la configuración de la cuenta de almacenamiento preparada mediante la CLI o el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="55ed6-174">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="55ed6-175">Si no está preparado para la migración y desea volver al estado anterior, utilice el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-175">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="55ed6-176">Si la configuración preparada parece correcta, puede continuar y confirmar los recursos mediante el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55ed6-176">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="55ed6-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55ed6-177">Next steps</span></span>

* [<span data-ttu-id="55ed6-178">Información general sobre la migración compatible con la plataforma de recursos de IaaS desde el modelo de implementación clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="55ed6-178">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="55ed6-179">Profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="55ed6-179">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="55ed6-180">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Planificación de la migración de recursos de IaaS del modelo clásico a Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="55ed6-180">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* [<span data-ttu-id="55ed6-181">Migración de recursos de IaaS de la implementación clásica a Resource Manager con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="55ed6-181">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="55ed6-182">Herramientas de la comunidad para ayudar con la migración de recursos de IaaS de la versión clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="55ed6-182">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="55ed6-183">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="55ed6-183">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="55ed6-184">Revisión de las preguntas más frecuentes acerca de cómo migrar recursos de IaaS de la versión clásica a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="55ed6-184">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
