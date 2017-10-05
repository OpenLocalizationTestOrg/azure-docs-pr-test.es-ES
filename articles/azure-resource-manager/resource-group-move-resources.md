---
title: "Traslado de recursos de Azure a una nueva suscripción o grupo de recursos | Microsoft Docs"
description: "Use Azure Resource Manager para trasladar recursos a un nuevo grupo de recursos o a una nueva suscripción."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="f4435-103">Traslado de los recursos a un nuevo grupo de recursos o a una nueva suscripción</span><span class="sxs-lookup"><span data-stu-id="f4435-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="f4435-104">En este tema se muestra cómo trasladar recursos a una nueva suscripción o un grupo de recursos en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="f4435-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="f4435-105">Puede usar el portal, PowerShell, la CLI de Azure o la API de REST para trasladar recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="f4435-106">Las operaciones de movimiento de este tema están disponibles sin ayuda del soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4435-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="f4435-107">Al mover los recursos, el grupo de origen y el grupo de destino se bloquean durante la operación.</span><span class="sxs-lookup"><span data-stu-id="f4435-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="f4435-108">Las operaciones de escritura y eliminación están bloqueadas en los grupos de recursos hasta que se completa el movimiento.</span><span class="sxs-lookup"><span data-stu-id="f4435-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="f4435-109">Este bloqueo significa que no puede agregar, actualizar ni eliminar recursos de los grupos de recursos, pero no que los recursos queden bloqueados.</span><span class="sxs-lookup"><span data-stu-id="f4435-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="f4435-110">Por ejemplo, si mueve un servidor SQL Server y su base de datos a un nuevo grupo de recursos, una aplicación que utiliza la base de datos no experimenta ningún tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="f4435-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="f4435-111">Todavía puede leer y escribir en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4435-111">It can still read and write to the database.</span></span>

<span data-ttu-id="f4435-112">No puede cambiar la ubicación del recurso.</span><span class="sxs-lookup"><span data-stu-id="f4435-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="f4435-113">Si se mueve un recurso, solo se mueve a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="f4435-114">El nuevo grupo de recursos puede tener una ubicación diferente, pero no cambia la ubicación del recurso.</span><span class="sxs-lookup"><span data-stu-id="f4435-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="f4435-115">En este artículo se describe cómo mover los recursos de una oferta de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4435-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="f4435-116">Si realmente desea cambiar la oferta de cuenta de Azure (por ejemplo, actualizar de pago por uso a prepago) sin dejar de trabajar con los recursos existentes, consulte [Cambio a otra oferta de Azure](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="f4435-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="f4435-117">Lista de comprobación antes de mover recursos</span><span class="sxs-lookup"><span data-stu-id="f4435-117">Checklist before moving resources</span></span>
<span data-ttu-id="f4435-118">Hay algunos pasos importantes que deben realizarse antes de mover un recurso.</span><span class="sxs-lookup"><span data-stu-id="f4435-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="f4435-119">Puede evitar errores mediante la comprobación de estas condiciones.</span><span class="sxs-lookup"><span data-stu-id="f4435-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="f4435-120">Las suscripciones de origen y destino deben existir en el mismo [inquilino de Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f4435-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="f4435-121">Para comprobar que ambas suscripciones tienen el mismo identificador de inquilino, utilice Azure PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4435-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="f4435-122">Para Azure PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f4435-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="f4435-123">Para la CLI de Azure 2.0, use:</span><span class="sxs-lookup"><span data-stu-id="f4435-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="f4435-124">Si los identificadores de inquilino para las suscripciones de origen y destino no son los mismos, puede intentar cambiar el directorio de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="f4435-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="f4435-125">Sin embargo, esta opción solo está disponible para los administradores de servicios que han iniciado sesión con una cuenta de Microsoft (no una cuenta de organización).</span><span class="sxs-lookup"><span data-stu-id="f4435-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="f4435-126">Para tratar de cambiar el directorio, inicie sesión en el [portal clásico](https://manage.windowsazure.com/) y seleccione **Configuración** y, después, la suscripción.</span><span class="sxs-lookup"><span data-stu-id="f4435-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="f4435-127">Si el icono **Editar directorio** está disponible, selecciónelo para cambiar el entorno de Azure Active Directory asociado.</span><span class="sxs-lookup"><span data-stu-id="f4435-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![editar directorio](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="f4435-129">Si este icono no está disponible, debe ponerse en contacto con el soporte técnico para mover los recursos a un nuevo inquilino.</span><span class="sxs-lookup"><span data-stu-id="f4435-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="f4435-130">El servicio debe permitir la capacidad de traslado de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="f4435-131">Este tema enumeran los servicios que permiten mover recursos y los servicios que no permiten el traslado de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="f4435-132">La suscripción de destino correspondiente al proveedor de recursos del recurso que se traslada debe estar registrada.</span><span class="sxs-lookup"><span data-stu-id="f4435-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="f4435-133">Si no es así, recibirá un error en el que se indicará que la **suscripción no está registrada para un tipo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="f4435-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="f4435-134">Podría encontrar este problema al mover un recurso a una nueva suscripción que nunca se ha utilizado el suscripción con ese tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="f4435-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="f4435-135">Para obtener más información sobre cómo comprobar el estado de registro y registrar proveedores de recursos, consulte [Tipos y proveedores de recursos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="f4435-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="f4435-136">Al llamar al soporte técnico</span><span class="sxs-lookup"><span data-stu-id="f4435-136">When to call support</span></span>
<span data-ttu-id="f4435-137">Puede trasladar la mayoría de los recursos a través de las operaciones de autoservicio que se muestran en este tema.</span><span class="sxs-lookup"><span data-stu-id="f4435-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="f4435-138">Utilice las operaciones de autoservicio para:</span><span class="sxs-lookup"><span data-stu-id="f4435-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="f4435-139">Trasladar recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f4435-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="f4435-140">Trasladar recursos clásicos conforme a las [limitaciones de implementación clásica](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="f4435-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="f4435-141">Llame a soporte técnico cuando necesite:</span><span class="sxs-lookup"><span data-stu-id="f4435-141">Call support when you need to:</span></span>

* <span data-ttu-id="f4435-142">Mueva los recursos a una nueva cuenta de Azure (y el inquilino de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f4435-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="f4435-143">Trasladar recursos clásicos, pero que tienen problemas con las limitaciones.</span><span class="sxs-lookup"><span data-stu-id="f4435-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="f4435-144">Servicios que permiten el traslado</span><span class="sxs-lookup"><span data-stu-id="f4435-144">Services that enable move</span></span>
<span data-ttu-id="f4435-145">Por ahora, los servicios que permiten el traslado a un nuevo grupo de recursos y a una nueva suscripción son:</span><span class="sxs-lookup"><span data-stu-id="f4435-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="f4435-146">API Management</span><span class="sxs-lookup"><span data-stu-id="f4435-146">API Management</span></span>
* <span data-ttu-id="f4435-147">App Service apps (Web Apps) - consulte las [limitaciones de App Service](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="f4435-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="f4435-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="f4435-148">Application Insights</span></span>
* <span data-ttu-id="f4435-149">Automation</span><span class="sxs-lookup"><span data-stu-id="f4435-149">Automation</span></span>
* <span data-ttu-id="f4435-150">Batch</span><span class="sxs-lookup"><span data-stu-id="f4435-150">Batch</span></span>
* <span data-ttu-id="f4435-151">Mapas de Bing</span><span class="sxs-lookup"><span data-stu-id="f4435-151">Bing Maps</span></span>
* <span data-ttu-id="f4435-152">CDN</span><span class="sxs-lookup"><span data-stu-id="f4435-152">CDN</span></span>
* <span data-ttu-id="f4435-153">Cloud Services (consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f4435-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f4435-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="f4435-154">Cognitive Services</span></span>
* <span data-ttu-id="f4435-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="f4435-155">Content Moderator</span></span>
* <span data-ttu-id="f4435-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="f4435-156">Data Catalog</span></span>
* <span data-ttu-id="f4435-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="f4435-157">Data Factory</span></span>
* <span data-ttu-id="f4435-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f4435-158">Data Lake Analytics</span></span>
* <span data-ttu-id="f4435-159">Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="f4435-159">Data Lake Store</span></span>
* <span data-ttu-id="f4435-160">DNS</span><span class="sxs-lookup"><span data-stu-id="f4435-160">DNS</span></span>
* <span data-ttu-id="f4435-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f4435-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="f4435-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f4435-162">Event Hubs</span></span>
* <span data-ttu-id="f4435-163">Clústeres de HDInsight: consulte [Limitaciones de HDInsight](#hdinsight-limitations).</span><span class="sxs-lookup"><span data-stu-id="f4435-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="f4435-164">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="f4435-164">IoT Hubs</span></span>
* <span data-ttu-id="f4435-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="f4435-165">Key Vault</span></span>
* <span data-ttu-id="f4435-166">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="f4435-166">Load Balancers</span></span>
* <span data-ttu-id="f4435-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f4435-167">Logic Apps</span></span>
* <span data-ttu-id="f4435-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f4435-168">Machine Learning</span></span>
* <span data-ttu-id="f4435-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="f4435-169">Media Services</span></span>
* <span data-ttu-id="f4435-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f4435-170">Mobile Engagement</span></span>
* <span data-ttu-id="f4435-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="f4435-171">Notification Hubs</span></span>
* <span data-ttu-id="f4435-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="f4435-172">Operational Insights</span></span>
* <span data-ttu-id="f4435-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="f4435-173">Operations Management</span></span>
* <span data-ttu-id="f4435-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="f4435-174">Power BI</span></span>
* <span data-ttu-id="f4435-175">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="f4435-175">Redis Cache</span></span>
* <span data-ttu-id="f4435-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="f4435-176">Scheduler</span></span>
* <span data-ttu-id="f4435-177">Search</span><span class="sxs-lookup"><span data-stu-id="f4435-177">Search</span></span>
* <span data-ttu-id="f4435-178">Servidor de administración</span><span class="sxs-lookup"><span data-stu-id="f4435-178">Server Management</span></span>
* <span data-ttu-id="f4435-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="f4435-179">Service Bus</span></span>
* <span data-ttu-id="f4435-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f4435-180">Service Fabric</span></span>
* <span data-ttu-id="f4435-181">Storage</span><span class="sxs-lookup"><span data-stu-id="f4435-181">Storage</span></span>
* <span data-ttu-id="f4435-182">Storage (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f4435-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f4435-183">Stream Analytics: los trabajos de Stream Analytics no se pueden mover si se encuentran en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f4435-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="f4435-184">Servidor de SQL Database: la base de datos y el servidor deben residir en el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="f4435-185">Cuando se mueve un servidor SQL Server, se mueven también todas sus bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f4435-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="f4435-186">Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="f4435-186">Traffic Manager</span></span>
* <span data-ttu-id="f4435-187">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f4435-187">Virtual Machines</span></span>
* <span data-ttu-id="f4435-188">Virtual Machines con certificado almacenados en Key Vault: el traslado al nuevo grupo de recursos en la misma suscripción está habilitado pero no el traslado de suscripción cruzado.</span><span class="sxs-lookup"><span data-stu-id="f4435-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="f4435-189">Virtual Machines (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f4435-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f4435-190">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f4435-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="f4435-191">Virtual Networks: por el momento, no se puede mover una red virtual emparejada hasta que el emparejamiento de la red virtual se haya inhabilitado.</span><span class="sxs-lookup"><span data-stu-id="f4435-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="f4435-192">Una vez deshabilitada, se podrá mover correctamente la Virtual Network y habilitar el emparejamiento de VNet.</span><span class="sxs-lookup"><span data-stu-id="f4435-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="f4435-193">Además, una red virtual no se puede mover a otra suscripción si la red virtual contiene una subred con vínculos de navegación de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="f4435-194">Por ejemplo, una subred de red virtual tiene un vínculo de navegación de recursos cuando se implementa un recurso de redis Microsoft.Cache en esta subred.</span><span class="sxs-lookup"><span data-stu-id="f4435-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="f4435-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="f4435-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="f4435-196">Servicios que no permiten el traslado</span><span class="sxs-lookup"><span data-stu-id="f4435-196">Services that do not enable move</span></span>
<span data-ttu-id="f4435-197">Los servicios que actualmente no permiten trasladar un recurso son:</span><span class="sxs-lookup"><span data-stu-id="f4435-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="f4435-198">Servicios de dominio de AD</span><span class="sxs-lookup"><span data-stu-id="f4435-198">AD Domain Services</span></span>
* <span data-ttu-id="f4435-199">Servicio de mantenimiento híbrido de AD</span><span class="sxs-lookup"><span data-stu-id="f4435-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="f4435-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f4435-200">Application Gateway</span></span>
* <span data-ttu-id="f4435-201">Conjuntos de disponibilidad con Virtual Machines con discos administrados</span><span class="sxs-lookup"><span data-stu-id="f4435-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="f4435-202">Servicios de BizTalk</span><span class="sxs-lookup"><span data-stu-id="f4435-202">BizTalk Services</span></span>
* <span data-ttu-id="f4435-203">Container Service</span><span class="sxs-lookup"><span data-stu-id="f4435-203">Container Service</span></span>
* <span data-ttu-id="f4435-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f4435-204">Express Route</span></span>
* <span data-ttu-id="f4435-205">DevTest Labs: el traslado al nuevo grupo de recursos en la misma suscripción está habilitado pero no el traslado de suscripción cruzado.</span><span class="sxs-lookup"><span data-stu-id="f4435-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="f4435-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="f4435-206">Dynamics LCS</span></span>
* <span data-ttu-id="f4435-207">Imágenes creadas a partir de discos administrados</span><span class="sxs-lookup"><span data-stu-id="f4435-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="f4435-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="f4435-208">Managed Disks</span></span>
* <span data-ttu-id="f4435-209">Aplicaciones administradas</span><span class="sxs-lookup"><span data-stu-id="f4435-209">Managed Applications</span></span>
* <span data-ttu-id="f4435-210">Almacén de Recovery Services: no mueva tampoco los recursos de Compute, Network y Storage asociados con el almacén de Recovery Services, vea [Limitaciones de Recovery Services](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="f4435-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="f4435-211">Seguridad</span><span class="sxs-lookup"><span data-stu-id="f4435-211">Security</span></span>
* <span data-ttu-id="f4435-212">Instantáneas creadas a partir de discos administrados</span><span class="sxs-lookup"><span data-stu-id="f4435-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="f4435-213">Administrador de dispositivos de StorSimple</span><span class="sxs-lookup"><span data-stu-id="f4435-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="f4435-214">Virtual Machines con discos administrados</span><span class="sxs-lookup"><span data-stu-id="f4435-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="f4435-215">Virtual Networks (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f4435-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f4435-216">Virtual Machines creadas a partir de recursos de Marketplace (no se pueden mover entre suscripciones).</span><span class="sxs-lookup"><span data-stu-id="f4435-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="f4435-217">Es necesario desaprovisionar el recurso en la suscripción activa y volver a implementarlo en la nueva suscripción</span><span class="sxs-lookup"><span data-stu-id="f4435-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="f4435-218">Limitaciones de App Service</span><span class="sxs-lookup"><span data-stu-id="f4435-218">App Service limitations</span></span>
<span data-ttu-id="f4435-219">Si se trabaja con aplicaciones de App Service, no se puede mover solo un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="f4435-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="f4435-220">Para mover las aplicaciones de App Service, las opciones son:</span><span class="sxs-lookup"><span data-stu-id="f4435-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="f4435-221">Trasladar el plan de App Service y el resto de recursos de App Service de ese grupo de recursos a un nuevo grupo que aún no tenga recursos de App Service.</span><span class="sxs-lookup"><span data-stu-id="f4435-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="f4435-222">Este requisito significa que debe trasladar incluso los recursos de App Service que no estén asociados al plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="f4435-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="f4435-223">Mover las aplicaciones a un grupo de recursos distinto, pero mantener todos los planes de App Service del grupo de recursos original.</span><span class="sxs-lookup"><span data-stu-id="f4435-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="f4435-224">Sin embargo, no es necesario que el plan de App Service resida en el mismo grupo de recursos que la aplicación para que esta funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="f4435-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="f4435-225">Por ejemplo, si el grupo de recursos contiene:</span><span class="sxs-lookup"><span data-stu-id="f4435-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="f4435-226">**web-a** asociada a **plan-a**</span><span class="sxs-lookup"><span data-stu-id="f4435-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="f4435-227">**web-b** asociada a **plan-b**</span><span class="sxs-lookup"><span data-stu-id="f4435-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="f4435-228">Tendrá las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="f4435-228">Your options are:</span></span>

* <span data-ttu-id="f4435-229">Trasladar **web-a**, **plan-a**, **web-b** y **plan-b**</span><span class="sxs-lookup"><span data-stu-id="f4435-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="f4435-230">Trasladar **web-a** y **web-b**</span><span class="sxs-lookup"><span data-stu-id="f4435-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="f4435-231">Mover **web-a**</span><span class="sxs-lookup"><span data-stu-id="f4435-231">Move **web-a**</span></span>
* <span data-ttu-id="f4435-232">Mover **web-b**</span><span class="sxs-lookup"><span data-stu-id="f4435-232">Move **web-b**</span></span>

<span data-ttu-id="f4435-233">Todas las demás combinaciones implican dejar un tipo de recurso que debe trasladarse al mover un plan de App Service (cualquier tipo de recurso de App Service).</span><span class="sxs-lookup"><span data-stu-id="f4435-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="f4435-234">Si la aplicación web se encuentra en un grupo de recursos distinto al de su plan de App Service, pero desea mover ambos a un nuevo grupo de recursos, debe realizar el traslado en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="f4435-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="f4435-235">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f4435-235">For example:</span></span>

* <span data-ttu-id="f4435-236">**web-a** reside en **web-group**.</span><span class="sxs-lookup"><span data-stu-id="f4435-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="f4435-237">**plan-a** reside en **plan-group**.</span><span class="sxs-lookup"><span data-stu-id="f4435-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="f4435-238">Desea que **web-a** y **plan-a** residan en **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="f4435-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="f4435-239">Para realizar este movimiento, debe llevar a cabo dos operaciones de traslado distintas en el siguiente orden:</span><span class="sxs-lookup"><span data-stu-id="f4435-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="f4435-240">Trasladar **web-a** a **plan-group**.</span><span class="sxs-lookup"><span data-stu-id="f4435-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="f4435-241">Trasladar **web-a** y **plan-a** a **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="f4435-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="f4435-242">Puede mover una instancia de App Service Certificate a un nuevo grupo de recursos o a una nueva suscripción sin ningún problema.</span><span class="sxs-lookup"><span data-stu-id="f4435-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="f4435-243">Sin embargo, si la aplicación web incluye un certificado SSL que adquirió externamente y que cargó en la aplicación, debe eliminar el certificado antes de trasladar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f4435-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="f4435-244">Por ejemplo, puede realizar los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4435-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="f4435-245">Eliminar el certificado cargado desde la aplicación web</span><span class="sxs-lookup"><span data-stu-id="f4435-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="f4435-246">Trasladar la aplicación web</span><span class="sxs-lookup"><span data-stu-id="f4435-246">Move the web app</span></span>
3. <span data-ttu-id="f4435-247">Cargar el certificado a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="f4435-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="f4435-248">Limitaciones de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="f4435-248">Recovery Services limitations</span></span>
<span data-ttu-id="f4435-249">No se admite el traslado para recursos de Storage, Network o Compute que se usan para configurar la recuperación ante desastres de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f4435-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="f4435-250">Por ejemplo, suponga que ha configurado la replicación de las máquinas locales en una cuenta de almacenamiento (Storage1) y desea que la máquina protegida aparezca después de la conmutación por error en Azure como una máquina virtual (VM1) conectada a una red virtual (Network1).</span><span class="sxs-lookup"><span data-stu-id="f4435-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="f4435-251">No puede mover ninguno de estos recursos de Azure, Storage1, VM1 y Network1, en grupos de recursos dentro de la misma suscripción o entre suscripciones.</span><span class="sxs-lookup"><span data-stu-id="f4435-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="f4435-252">Limitaciones de HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4435-252">HDInsight limitations</span></span>

<span data-ttu-id="f4435-253">Puede mover clústeres de HDInsight a una nueva suscripción o un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="f4435-254">Sin embargo, no puede mover entre suscripciones los recursos de red vinculados al clúster de HDInsight (por ejemplo, la red virtual, una NIC o un equilibrador de carga).</span><span class="sxs-lookup"><span data-stu-id="f4435-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="f4435-255">Además, tampoco se puede mover a un nuevo grupo de recursos una NIC que está conectada a una máquina virtual del clúster.</span><span class="sxs-lookup"><span data-stu-id="f4435-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="f4435-256">Al mover un clúster de HDInsight a una nueva suscripción, mueva primero otros recursos (por ejemplo, la cuenta de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="f4435-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="f4435-257">Después, mover el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4435-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="f4435-258">limitaciones de la implementación clásica</span><span class="sxs-lookup"><span data-stu-id="f4435-258">Classic deployment limitations</span></span>
<span data-ttu-id="f4435-259">Las opciones para mover recursos implementados mediante el modelo clásico varían en función de si traslada los recursos dentro de una misma suscripción o a una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="f4435-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="f4435-260">Misma suscripción</span><span class="sxs-lookup"><span data-stu-id="f4435-260">Same subscription</span></span>
<span data-ttu-id="f4435-261">Al mover recursos de un grupo de recursos a otro dentro de la misma suscripción, se aplican las restricciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4435-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="f4435-262">No se pueden mover redes virtuales (clásico).</span><span class="sxs-lookup"><span data-stu-id="f4435-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="f4435-263">Las máquinas virtuales (clásico) se deben mover con el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="f4435-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="f4435-264">El servicio en la nube solo se puede mover cuando el traslado incluye todas sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f4435-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="f4435-265">Solo se puede mover un servicio en la nube cada vez.</span><span class="sxs-lookup"><span data-stu-id="f4435-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="f4435-266">Solo se puede mover una cuenta de almacenamiento (clásico) cada vez.</span><span class="sxs-lookup"><span data-stu-id="f4435-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="f4435-267">No se puede mover una cuenta de almacenamiento (clásico) con una máquina virtual o un servicio en la nube en la misma operación de traslado.</span><span class="sxs-lookup"><span data-stu-id="f4435-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="f4435-268">Para trasladar recursos clásicos a un grupo de recursos nuevo dentro de la misma suscripción, utilice las operaciones de traslado estándar a través del [portal](#use-portal), [Azure PowerShell](#use-powershell), la [CLI de Azure](#use-azure-cli) o la [API de REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="f4435-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="f4435-269">Utilice las mismas operaciones que utiliza para trasladar recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f4435-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="f4435-270">Suscripción nueva</span><span class="sxs-lookup"><span data-stu-id="f4435-270">New subscription</span></span>
<span data-ttu-id="f4435-271">Al trasladar recursos a una nueva suscripción, se aplican las restricciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4435-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="f4435-272">Todos los recursos clásicos de la suscripción se deben mover en la misma operación.</span><span class="sxs-lookup"><span data-stu-id="f4435-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="f4435-273">La suscripción de destino no debe contener otros recursos clásicos.</span><span class="sxs-lookup"><span data-stu-id="f4435-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="f4435-274">El traslado solo puede solicitarse a través de una API de REST independiente para el traslado de recursos clásicos.</span><span class="sxs-lookup"><span data-stu-id="f4435-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="f4435-275">Los comandos de movimiento estándar de Resource Manager no funcionan para mover recursos clásicos a una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="f4435-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="f4435-276">Para trasladar recursos clásicos a una nueva suscripción, use operaciones REST específicas para recursos clásicos.</span><span class="sxs-lookup"><span data-stu-id="f4435-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="f4435-277">Para usar REST, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f4435-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="f4435-278">Compruebe si la suscripción de origen puede participar en un movimiento entre suscripciones.</span><span class="sxs-lookup"><span data-stu-id="f4435-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="f4435-279">Utilice la siguiente operación:</span><span class="sxs-lookup"><span data-stu-id="f4435-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="f4435-280">En el cuerpo de la solicitud, incluya:</span><span class="sxs-lookup"><span data-stu-id="f4435-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="f4435-281">La respuesta para la operación de validación está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4435-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="f4435-282">Compruebe si la suscripción de destino puede participar en un movimiento entre suscripciones.</span><span class="sxs-lookup"><span data-stu-id="f4435-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="f4435-283">Utilice la siguiente operación:</span><span class="sxs-lookup"><span data-stu-id="f4435-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="f4435-284">En el cuerpo de la solicitud, incluya:</span><span class="sxs-lookup"><span data-stu-id="f4435-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="f4435-285">La respuesta está en el mismo formato que la validación de la suscripción de origen.</span><span class="sxs-lookup"><span data-stu-id="f4435-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="f4435-286">Si ambas suscripciones superan la validación, traslade todos los recursos clásicos de una suscripción a otra con la siguiente operación:</span><span class="sxs-lookup"><span data-stu-id="f4435-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="f4435-287">En el cuerpo de la solicitud, incluya:</span><span class="sxs-lookup"><span data-stu-id="f4435-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="f4435-288">Es posible que esta operación tarde varios minutos.</span><span class="sxs-lookup"><span data-stu-id="f4435-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="f4435-289">Mediante el portal</span><span class="sxs-lookup"><span data-stu-id="f4435-289">Use portal</span></span>
<span data-ttu-id="f4435-290">Para trasladar recursos, seleccione el grupo de recursos que contiene esos recursos y, después, el botón **Mover**.</span><span class="sxs-lookup"><span data-stu-id="f4435-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![Mover recursos](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="f4435-292">Seleccione si va a mover los recursos a un nuevo grupo de recursos o a una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="f4435-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="f4435-293">Seleccione los recursos que trasladar y el grupo de recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="f4435-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="f4435-294">Confirme que tiene que actualizar los scripts para estos recursos y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f4435-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="f4435-295">Si ha seleccionado el icono de edición de la suscripción en el paso anterior, también debe seleccionar la suscripción de destino.</span><span class="sxs-lookup"><span data-stu-id="f4435-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![seleccionar destino](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="f4435-297">En **Notificaciones**, podrá ver que la operación de traslado está en curso.</span><span class="sxs-lookup"><span data-stu-id="f4435-297">In **Notifications**, you see that the move operation is running.</span></span>

![mostrar el estado del traslado](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="f4435-299">Cuando haya finalizado, se le notificará del resultado.</span><span class="sxs-lookup"><span data-stu-id="f4435-299">When it has completed, you are notified of the result.</span></span>

![mostrar el resultado del traslado](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="f4435-301">Uso de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4435-301">Use PowerShell</span></span>
<span data-ttu-id="f4435-302">Para trasladar recursos existentes a otro grupo de recursos o a una suscripción, use el comando `Move-AzureRmResource`.</span><span class="sxs-lookup"><span data-stu-id="f4435-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="f4435-303">El primer ejemplo muestra cómo trasladar un recurso a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="f4435-304">El segundo ejemplo muestra cómo trasladar varios recursos a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="f4435-305">Para moverlos a una nueva suscripción, especifique un valor para el parámetro `DestinationSubscriptionId`.</span><span class="sxs-lookup"><span data-stu-id="f4435-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="f4435-306">Se le pedirá que confirme que quiere mover los recursos especificados.</span><span class="sxs-lookup"><span data-stu-id="f4435-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="f4435-307">Uso de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f4435-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="f4435-308">Para trasladar recursos existentes a otro grupo de recursos o a una suscripción, use el comando `az resource move`.</span><span class="sxs-lookup"><span data-stu-id="f4435-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="f4435-309">Proporcione los identificadores de recursos de los recursos que se van a mover.</span><span class="sxs-lookup"><span data-stu-id="f4435-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="f4435-310">Puede obtener los identificadores de recurso con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f4435-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="f4435-311">En el siguiente ejemplo se muestra cómo trasladar una cuenta de almacenamiento a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="f4435-312">En el parámetro `--ids`, ofrezca una lista separada por espacios de los identificadores de recurso que se van a trasladar.</span><span class="sxs-lookup"><span data-stu-id="f4435-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="f4435-313">Para mover a una nueva suscripción, proporcione el parámetro `--destination-subscription-id`.</span><span class="sxs-lookup"><span data-stu-id="f4435-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="f4435-314">Uso de CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f4435-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="f4435-315">Para trasladar recursos existentes a otro grupo de recursos o a una suscripción, use el comando `azure resource move`.</span><span class="sxs-lookup"><span data-stu-id="f4435-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="f4435-316">Proporcione los identificadores de recursos de los recursos que se van a mover.</span><span class="sxs-lookup"><span data-stu-id="f4435-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="f4435-317">Puede obtener los identificadores de recurso con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f4435-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="f4435-318">Que devuelve el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="f4435-318">Which returns the following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="f4435-319">En el siguiente ejemplo se muestra cómo trasladar una cuenta de almacenamiento a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4435-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="f4435-320">En el parámetro `-i`, ofrezca una lista separada por comas de los identificadores de recurso que se van a trasladar.</span><span class="sxs-lookup"><span data-stu-id="f4435-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="f4435-321">Se le pedirá que confirme que quiere mover el recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="f4435-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="f4435-322">Use la API de REST</span><span class="sxs-lookup"><span data-stu-id="f4435-322">Use REST API</span></span>
<span data-ttu-id="f4435-323">Para trasladar recursos existentes a otro grupo de recursos o a una suscripción, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f4435-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="f4435-324">En el cuerpo de la solicitud, especifique el grupo de recursos de destino y los recursos a mover.</span><span class="sxs-lookup"><span data-stu-id="f4435-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="f4435-325">Para obtener más información acerca de la operación REST de movimiento, consulte [Mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4435-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4435-326">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4435-326">Next steps</span></span>
* <span data-ttu-id="f4435-327">Para obtener información sobre los cmdlets de PowerShell que permiten administrar su suscripción, vea [Uso de Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f4435-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="f4435-328">Para obtener información sobre los comandos de la CLI de Azure para administrar su suscripción, vea [Uso de la CLI de Azure para Mac, Linux y Windows con Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f4435-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="f4435-329">Si desea conocer las funciones del portal que permiten administrar la suscripción, consulte [Uso del Azure Portal para implementar y administrar los recursos de Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4435-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="f4435-330">Para aprender a aplicar una organización lógica a los recursos, consulte [Uso de etiquetas para organizar los recursos de Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="f4435-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
