---
title: "máquinas virtuales de aaaMigrate tooResource administrador mediante la CLI de Azure | Documentos de Microsoft"
description: "Este artículo le guía a través de migración de hello admitida por la plataforma de recursos de tooAzure clásico Administrador de recursos mediante CLI de Azure"
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
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="76945-103">Migrar recursos de IaaS de tooAzure clásico Administrador de recursos mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="76945-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="76945-104">Estos pasos muestra cómo toouse interfaz de línea de comandos (CLI) de Azure comandos toomigrate infraestructura como un recurso de servicio (IaaS) de modelo de implementación de Azure Resource Manager de toohello modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="76945-105">artículo de Hello requiere hello [CLI de Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="76945-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="76945-106">Todas las operaciones de hello descritas aquí son idempotentes.</span><span class="sxs-lookup"><span data-stu-id="76945-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="76945-107">Si tiene un problema que no sea una característica no compatible o un error de configuración, se recomienda que vuelva a intentar Hola preparar, anular o confirmar la operación.</span><span class="sxs-lookup"><span data-stu-id="76945-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="76945-108">plataforma de Hola, a continuación, intentará volver a la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="76945-109">Este es un orden de hello tooidentify de diagrama de flujo en el que es necesario pasos toobe ejecutado durante un proceso de migración</span><span class="sxs-lookup"><span data-stu-id="76945-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Captura de pantalla que muestra los pasos de migración de Hola](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="76945-111">Paso 1: Preparación para la migración</span><span class="sxs-lookup"><span data-stu-id="76945-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="76945-112">Estas son algunas prácticas recomendadas que se recomienda evaluar migrar recursos de IaaS de tooResource clásico Manager:</span><span class="sxs-lookup"><span data-stu-id="76945-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="76945-113">Lea hello [lista de configuraciones no admitidas o características](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76945-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="76945-114">Si tiene máquinas virtuales que usan configuraciones no admitidas o características, se recomienda que espere Hola característica/Configuración compatibilidad toobe anunciada.</span><span class="sxs-lookup"><span data-stu-id="76945-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="76945-115">Como alternativa, puede quitar esa característica o salir de que la migración de configuración tooenable si se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="76945-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="76945-116">Si han automatizado las secuencias de comandos que implementan la infraestructura y las aplicaciones de hoy en día, intente toocreate un programa de instalación de prueba similar con esos scripts para la migración.</span><span class="sxs-lookup"><span data-stu-id="76945-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="76945-117">Como alternativa, puede configurar entornos de ejemplo mediante el uso de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76945-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76945-118">Las puertas de enlace de la aplicación no se admiten actualmente para la migración de clásico tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="76945-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="76945-119">toomigrate una red virtual clásica con una puerta de enlace de aplicaciones, quitar la puerta de enlace de hello antes de ejecutar una red de Hola de toomove de operación de preparación.</span><span class="sxs-lookup"><span data-stu-id="76945-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="76945-120">Después de completar la migración de hello, vuelva a conectar la puerta de enlace de hello en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="76945-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="76945-121">Conectar los circuitos tooExpressRoute en otra suscripción de puertas de enlace de ExpressRoute no se pueden migrar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="76945-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="76945-122">En tales casos, quite la puerta de enlace de ExpressRoute de hello, migrar la red virtual de Hola y vuelva a puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="76945-123">Vea [ExpressRoute migrar circuitos y asociado redes virtuales de modelo de implementación de administrador de recursos de hello toohello clásico](../../expressroute/expressroute-migration-classic-resource-manager.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="76945-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="76945-124">Paso 2: Establecer la suscripción y registrar proveedor de Hola</span><span class="sxs-lookup"><span data-stu-id="76945-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="76945-125">Para escenarios de migración, necesita tooset del entorno para ambos clásico y Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="76945-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="76945-126">[Instale la CLI de Azure](../../cli-install-nodejs.md) y [seleccione la suscripción](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="76945-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="76945-127">Cuenta de inicio de sesión tooyour.</span><span class="sxs-lookup"><span data-stu-id="76945-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="76945-128">Seleccione Hola suscripción de Azure usando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="76945-129">El registro está paso de una sola vez pero necesita toobe realiza una vez antes de intentar la migración.</span><span class="sxs-lookup"><span data-stu-id="76945-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="76945-130">Sin registrar verá Hola siguiente mensaje de error</span><span class="sxs-lookup"><span data-stu-id="76945-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="76945-131">*BadRequest: Subscription is not registered for migration* (BadRequest: la suscripción no está registrada para la migración)</span><span class="sxs-lookup"><span data-stu-id="76945-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="76945-132">Registrar con el proveedor de recursos de migración de hello mediante Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="76945-133">Tenga en cuenta que, en algunos casos, se agota el tiempo de espera de este comando. Sin embargo, el registro de hello será correcto.</span><span class="sxs-lookup"><span data-stu-id="76945-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="76945-134">Espere cinco minutos para toofinish de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="76945-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="76945-135">Puede comprobar el estado de Hola de aprobación de hello usando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="76945-136">Asegúrese de que RegistrationState sea `Registered` antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="76945-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="76945-137">Ahora cambie CLI toohello `asm` modo.</span><span class="sxs-lookup"><span data-stu-id="76945-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="76945-138">Paso 3: Asegúrese de que tiene suficientes núcleos de máquina Virtual de Azure Resource Manager Hola región de Azure de su implementación actual o la red virtual</span><span class="sxs-lookup"><span data-stu-id="76945-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="76945-139">Para este paso deberá tooswitch demasiado`arm` modo.</span><span class="sxs-lookup"><span data-stu-id="76945-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="76945-140">Hacer esto con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="76945-141">Puede usar Hola después CLI comando toocheck Hola cantidad actual de núcleos que tiene en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="76945-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="76945-142">toolearn más información acerca de las cuotas de núcleo, consulte [hello Azure Resource Manager y límites](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="76945-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="76945-143">Una vez que haya terminado comprobar este paso, puede volver cambiar demasiado`asm` modo.</span><span class="sxs-lookup"><span data-stu-id="76945-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="76945-144">Paso 4: Opción 1: Migración de máquinas virtuales de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="76945-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="76945-145">Hola obtención de una lista de servicios en la nube mediante el uso de hello siguiente comando y, a continuación, servicio de nube de Hola de selección que desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="76945-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="76945-146">Tenga en cuenta que si hello las máquinas virtuales en el servicio de nube de Hola se encuentran en una red virtual o si tienen roles web y de trabajo, obtendrá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="76945-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="76945-147">Ejecute hello siguientes comando tooget Hola nombre de la implementación de servicio en la nube Hola de resultados detallados de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="76945-148">En la mayoría de los casos, nombre de la implementación de hello es Hola igual que el nombre del servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="76945-149">En primer lugar, validar si puede migrar servicio en la nube hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="76945-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="76945-150">Preparar las máquinas virtuales de Hola Hola del servicio en nube para la migración.</span><span class="sxs-lookup"><span data-stu-id="76945-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="76945-151">Tiene dos toochoose de opciones de.</span><span class="sxs-lookup"><span data-stu-id="76945-151">You have two options toochoose from.</span></span>

<span data-ttu-id="76945-152">Si desea toomigrate Hola máquinas virtuales tooa plataforma red virtual creada, utilice Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="76945-153">Si desea tooan toomigrate existente de la red virtual en el modelo de implementación del Administrador de recursos de hello, utilice Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="76945-154">Después de preparar Hola operación se realiza correctamente, puede buscar a través de estado de migración de hello resultados detallados tooget Hola de hello las máquinas virtuales y asegúrese de que se encuentran en hello `Prepared` estado.</span><span class="sxs-lookup"><span data-stu-id="76945-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="76945-155">Comprobar la configuración de Hola para hello preparado recursos con CLI u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76945-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="76945-156">Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, usar hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="76945-157">Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="76945-158">Paso 4: Opción 2: Migración de máquinas virtuales de una red virtual</span><span class="sxs-lookup"><span data-stu-id="76945-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="76945-159">Selección Hola red virtual que desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="76945-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="76945-160">Tenga en cuenta que si la red virtual de hello contiene roles web y de trabajo o máquinas virtuales con las configuraciones no compatibles, obtendrá un mensaje de error de validación.</span><span class="sxs-lookup"><span data-stu-id="76945-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="76945-161">Obtener todas las redes virtuales de hello en la suscripción de hello mediante Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="76945-162">salida de Hello tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="76945-162">hello output will look something like this:</span></span>

![Captura de pantalla de línea de comandos de hello con el nombre de toda la red virtual de hello resaltado.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="76945-164">Hola ejemplo anterior, Hola **virtualNetworkName** es el nombre completo de hello **"Grupo classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="76945-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="76945-165">En primer lugar, validar si se puede migrar la red virtual de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76945-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="76945-166">Prepare la red virtual de Hola de su elección para la migración mediante Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="76945-167">Comprobar la configuración de Hola para hello preparado las máquinas virtuales con CLI u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76945-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="76945-168">Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, usar hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="76945-169">Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="76945-170">Paso 5: Migración de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="76945-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="76945-171">Una vez que haya terminado la migración de máquinas virtuales hello, se recomienda que migre la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="76945-172">Preparar la cuenta de almacenamiento de Hola migración utilizando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="76945-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="76945-173">Comprobar la configuración de Hola para hello preparado cuenta de almacenamiento con CLI u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76945-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="76945-174">Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, usar hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="76945-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="76945-175">Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="76945-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="76945-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76945-176">Next steps</span></span>

* [<span data-ttu-id="76945-177">Información general de migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="76945-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="76945-178">Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="76945-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="76945-179">Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="76945-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="76945-180">Usar recursos de IaaS PowerShell toomigrate desde tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="76945-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="76945-181">Herramientas de la Comunidad para ayudar con la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="76945-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="76945-182">Revisión de los errores más comunes en la migración</span><span class="sxs-lookup"><span data-stu-id="76945-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="76945-183">Hola de revisión más preguntas más frecuentes acerca de cómo migrar recursos de IaaS de tooAzure clásico Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="76945-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
