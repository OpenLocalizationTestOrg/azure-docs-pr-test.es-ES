---
title: "aaaMove toonew suscripción o recurso de grupo de recursos de Azure | Documentos de Microsoft"
description: "Use el Administrador de recursos de Azure toomove recursos tooa nuevo grupo de recursos o suscripción."
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
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="5389b-103">Mover grupo de recursos de toonew de recursos o suscripción</span><span class="sxs-lookup"><span data-stu-id="5389b-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="5389b-104">Este tema muestra cómo toomove recursos tooeither una nueva suscripción o en un nuevo recurso de grupo en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="5389b-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="5389b-105">Puede usar el portal de hello, PowerShell, CLI de Azure u Hola recursos toomove de API de REST.</span><span class="sxs-lookup"><span data-stu-id="5389b-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="5389b-106">las operaciones de movimiento de Hello en este tema están disponible tooyou sin ayuda de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="5389b-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="5389b-107">Al mover los recursos, los grupos de código fuente de Hola y Hola destino se bloquean durante la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="5389b-108">Escribir y eliminar operaciones están bloqueados en grupos de recursos de hello hasta que se completa el movimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="5389b-109">Este bloqueo significa que no se puede agregar, actualizar o eliminar los recursos en grupos de recursos de hello, pero no significa que se inmovilizan recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="5389b-110">Por ejemplo, si mueve un servidor SQL Server y su grupo de recursos de base de datos tooa nuevo, una aplicación que utiliza la base de datos de hello no experimenta ningún tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="5389b-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="5389b-111">Todavía puede leer y escribir toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="5389b-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="5389b-112">No se puede cambiar la ubicación de hello del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="5389b-113">Mover un recurso solo mueve tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="5389b-114">nuevo grupo de recursos de Hello puede tener una ubicación diferente, pero no cambiar la ubicación de hello del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="5389b-115">Este artículo describe cómo cuenta oferta toomove recursos dentro de un Azure existente.</span><span class="sxs-lookup"><span data-stu-id="5389b-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="5389b-116">Si realmente desea toochange su cuenta de Azure de la oferta (por ejemplo, la actualización de pago por uso toopre-pay) mientras continúa toowork con los recursos existentes, consulte [cambiar su oferta de suscripción de Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="5389b-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="5389b-117">Lista de comprobación antes de mover recursos</span><span class="sxs-lookup"><span data-stu-id="5389b-117">Checklist before moving resources</span></span>
<span data-ttu-id="5389b-118">Hay algunos tooperform pasos importantes antes de mover un recurso.</span><span class="sxs-lookup"><span data-stu-id="5389b-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="5389b-119">Puede evitar errores mediante la comprobación de estas condiciones.</span><span class="sxs-lookup"><span data-stu-id="5389b-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="5389b-120">Hello las suscripciones de origen y de destino deben existir en hello mismo [inquilino de Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5389b-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="5389b-121">toocheck que ambas suscripciones han Hola mismo identificador de inquilino, usar Azure PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5389b-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="5389b-122">Para Azure PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="5389b-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="5389b-123">Para la CLI de Azure 2.0, use:</span><span class="sxs-lookup"><span data-stu-id="5389b-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="5389b-124">Si Hola inquilino identificadores para las suscripciones de origen y destino de hello no son Hola mismo, puede tratar de directorio de hello toochange para la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="5389b-125">Sin embargo, esta opción está solo disponible tooService los administradores que han iniciado sesión con una cuenta de Microsoft (no una cuenta profesional).</span><span class="sxs-lookup"><span data-stu-id="5389b-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="5389b-126">tooattempt cambiando el directorio de hello, inicio de sesión toohello [portal clásico](https://manage.windowsazure.com/)y seleccione **configuración**y seleccione la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="5389b-127">Si hello **editar directorio** icono está disponible, seleccione toochange Hola asociados Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5389b-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![editar directorio](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="5389b-129">Si este icono no está disponible, debe ponerse en contacto con el soporte técnico toomove Hola recursos tooa nuevo inquilino.</span><span class="sxs-lookup"><span data-stu-id="5389b-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="5389b-130">servicio de Hello debe habilitar recursos de hello capacidad toomove.</span><span class="sxs-lookup"><span data-stu-id="5389b-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="5389b-131">Este tema enumeran los servicios que permiten mover recursos y los servicios que no permiten el traslado de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="5389b-132">suscripción de destino de Hello debe estar registrada para el proveedor de recursos de Hola de recurso de Hola que se va a mover.</span><span class="sxs-lookup"><span data-stu-id="5389b-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="5389b-133">Si no es así, recibirá un error que indica que hello **suscripción no está registrada para un tipo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="5389b-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="5389b-134">Podría encontrar este problema al mover una nueva suscripción de recursos tooa, pero esa suscripción nunca se ha utilizado con ese tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="5389b-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="5389b-135">toolearn cómo toocheck Hola estado de registro y registrar proveedores de recursos, consulte [proveedores de recursos y los tipos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="5389b-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="5389b-136">¿Cuándo admitirá toocall</span><span class="sxs-lookup"><span data-stu-id="5389b-136">When toocall support</span></span>
<span data-ttu-id="5389b-137">Puede mover la mayoría de los recursos a través de operaciones de autoservicio de Hola que se muestra en este tema.</span><span class="sxs-lookup"><span data-stu-id="5389b-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="5389b-138">Usar operaciones de autoservicio de Hola para:</span><span class="sxs-lookup"><span data-stu-id="5389b-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="5389b-139">Trasladar recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5389b-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="5389b-140">Mover los recursos clásicos según toohello [limitaciones de implementación clásica](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="5389b-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="5389b-141">Llame a soporte técnico cuando necesite:</span><span class="sxs-lookup"><span data-stu-id="5389b-141">Call support when you need to:</span></span>

* <span data-ttu-id="5389b-142">Mueva la cuenta de Azure nuevo recursos tooa (y los inquilinos de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5389b-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="5389b-143">Mover los recursos clásicos pero están teniendo problemas con las limitaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="5389b-144">Servicios que permiten el traslado</span><span class="sxs-lookup"><span data-stu-id="5389b-144">Services that enable move</span></span>
<span data-ttu-id="5389b-145">Por ahora, servicios de Hola que habilite móvil tooboth un nuevo grupo de recursos y la suscripción son:</span><span class="sxs-lookup"><span data-stu-id="5389b-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="5389b-146">API Management</span><span class="sxs-lookup"><span data-stu-id="5389b-146">API Management</span></span>
* <span data-ttu-id="5389b-147">App Service apps (Web Apps) - consulte las [limitaciones de App Service](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="5389b-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="5389b-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="5389b-148">Application Insights</span></span>
* <span data-ttu-id="5389b-149">Automation</span><span class="sxs-lookup"><span data-stu-id="5389b-149">Automation</span></span>
* <span data-ttu-id="5389b-150">Batch</span><span class="sxs-lookup"><span data-stu-id="5389b-150">Batch</span></span>
* <span data-ttu-id="5389b-151">Mapas de Bing</span><span class="sxs-lookup"><span data-stu-id="5389b-151">Bing Maps</span></span>
* <span data-ttu-id="5389b-152">CDN</span><span class="sxs-lookup"><span data-stu-id="5389b-152">CDN</span></span>
* <span data-ttu-id="5389b-153">Cloud Services (consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5389b-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5389b-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="5389b-154">Cognitive Services</span></span>
* <span data-ttu-id="5389b-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="5389b-155">Content Moderator</span></span>
* <span data-ttu-id="5389b-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="5389b-156">Data Catalog</span></span>
* <span data-ttu-id="5389b-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="5389b-157">Data Factory</span></span>
* <span data-ttu-id="5389b-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5389b-158">Data Lake Analytics</span></span>
* <span data-ttu-id="5389b-159">Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="5389b-159">Data Lake Store</span></span>
* <span data-ttu-id="5389b-160">DNS</span><span class="sxs-lookup"><span data-stu-id="5389b-160">DNS</span></span>
* <span data-ttu-id="5389b-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5389b-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="5389b-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5389b-162">Event Hubs</span></span>
* <span data-ttu-id="5389b-163">Clústeres de HDInsight: consulte [Limitaciones de HDInsight](#hdinsight-limitations).</span><span class="sxs-lookup"><span data-stu-id="5389b-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="5389b-164">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="5389b-164">IoT Hubs</span></span>
* <span data-ttu-id="5389b-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="5389b-165">Key Vault</span></span>
* <span data-ttu-id="5389b-166">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="5389b-166">Load Balancers</span></span>
* <span data-ttu-id="5389b-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5389b-167">Logic Apps</span></span>
* <span data-ttu-id="5389b-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5389b-168">Machine Learning</span></span>
* <span data-ttu-id="5389b-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="5389b-169">Media Services</span></span>
* <span data-ttu-id="5389b-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5389b-170">Mobile Engagement</span></span>
* <span data-ttu-id="5389b-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="5389b-171">Notification Hubs</span></span>
* <span data-ttu-id="5389b-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="5389b-172">Operational Insights</span></span>
* <span data-ttu-id="5389b-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="5389b-173">Operations Management</span></span>
* <span data-ttu-id="5389b-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="5389b-174">Power BI</span></span>
* <span data-ttu-id="5389b-175">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="5389b-175">Redis Cache</span></span>
* <span data-ttu-id="5389b-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="5389b-176">Scheduler</span></span>
* <span data-ttu-id="5389b-177">Search</span><span class="sxs-lookup"><span data-stu-id="5389b-177">Search</span></span>
* <span data-ttu-id="5389b-178">Servidor de administración</span><span class="sxs-lookup"><span data-stu-id="5389b-178">Server Management</span></span>
* <span data-ttu-id="5389b-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="5389b-179">Service Bus</span></span>
* <span data-ttu-id="5389b-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5389b-180">Service Fabric</span></span>
* <span data-ttu-id="5389b-181">Storage</span><span class="sxs-lookup"><span data-stu-id="5389b-181">Storage</span></span>
* <span data-ttu-id="5389b-182">Storage (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5389b-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5389b-183">Stream Analytics: los trabajos de Stream Analytics no se pueden mover si se encuentran en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="5389b-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="5389b-184">Servidor de base de datos SQL: hello base de datos y el servidor deben residir en hello mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="5389b-185">Cuando se mueve un servidor SQL Server, se mueven también todas sus bases de datos.</span><span class="sxs-lookup"><span data-stu-id="5389b-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="5389b-186">Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="5389b-186">Traffic Manager</span></span>
* <span data-ttu-id="5389b-187">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5389b-187">Virtual Machines</span></span>
* <span data-ttu-id="5389b-188">Máquinas virtuales con certificado almacenado en el almacén de claves - mover el grupo de recursos de toonew en la misma suscripción está habilitada, pero no está habilitado el movimiento de suscripción cruzado.</span><span class="sxs-lookup"><span data-stu-id="5389b-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="5389b-189">Virtual Machines (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5389b-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5389b-190">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5389b-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="5389b-191">Virtual Networks: por el momento, no se puede mover una red virtual emparejada hasta que el emparejamiento de la red virtual se haya inhabilitado.</span><span class="sxs-lookup"><span data-stu-id="5389b-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="5389b-192">Una vez deshabilitado, Hola red Virtual se podrá mover correctamente y se puede habilitar el intercambio de tráfico de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="5389b-193">Además, una red Virtual no puede ser movida tooa otra suscripción si Hola red Virtual contiene ninguna subred con vínculos de navegación de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="5389b-194">Por ejemplo, una subred de red virtual tiene un vínculo de navegación de recursos cuando se implementa un recurso de redis Microsoft.Cache en esta subred.</span><span class="sxs-lookup"><span data-stu-id="5389b-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="5389b-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="5389b-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="5389b-196">Servicios que no permiten el traslado</span><span class="sxs-lookup"><span data-stu-id="5389b-196">Services that do not enable move</span></span>
<span data-ttu-id="5389b-197">Servicios de Hola que actualmente no se permiten mover un recurso son:</span><span class="sxs-lookup"><span data-stu-id="5389b-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="5389b-198">Servicios de dominio de AD</span><span class="sxs-lookup"><span data-stu-id="5389b-198">AD Domain Services</span></span>
* <span data-ttu-id="5389b-199">Servicio de mantenimiento híbrido de AD</span><span class="sxs-lookup"><span data-stu-id="5389b-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="5389b-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="5389b-200">Application Gateway</span></span>
* <span data-ttu-id="5389b-201">Conjuntos de disponibilidad con Virtual Machines con discos administrados</span><span class="sxs-lookup"><span data-stu-id="5389b-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="5389b-202">Servicios de BizTalk</span><span class="sxs-lookup"><span data-stu-id="5389b-202">BizTalk Services</span></span>
* <span data-ttu-id="5389b-203">Container Service</span><span class="sxs-lookup"><span data-stu-id="5389b-203">Container Service</span></span>
* <span data-ttu-id="5389b-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5389b-204">Express Route</span></span>
* <span data-ttu-id="5389b-205">Laboratorios de desarrollo y pruebas - mover el grupo de recursos de toonew en la misma suscripción está habilitado, pero entre el movimiento de suscripción no está habilitado.</span><span class="sxs-lookup"><span data-stu-id="5389b-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="5389b-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="5389b-206">Dynamics LCS</span></span>
* <span data-ttu-id="5389b-207">Imágenes creadas a partir de discos administrados</span><span class="sxs-lookup"><span data-stu-id="5389b-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="5389b-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5389b-208">Managed Disks</span></span>
* <span data-ttu-id="5389b-209">Aplicaciones administradas</span><span class="sxs-lookup"><span data-stu-id="5389b-209">Managed Applications</span></span>
* <span data-ttu-id="5389b-210">Almacén de servicios de recuperación: también ¿Hola no movimiento Hola proceso, red y almacenamiento de recursos asociados con los servicios de recuperación del almacén, vea [limitaciones de servicios de recuperación](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="5389b-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="5389b-211">Seguridad</span><span class="sxs-lookup"><span data-stu-id="5389b-211">Security</span></span>
* <span data-ttu-id="5389b-212">Instantáneas creadas a partir de discos administrados</span><span class="sxs-lookup"><span data-stu-id="5389b-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="5389b-213">Administrador de dispositivos de StorSimple</span><span class="sxs-lookup"><span data-stu-id="5389b-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="5389b-214">Virtual Machines con discos administrados</span><span class="sxs-lookup"><span data-stu-id="5389b-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="5389b-215">Virtual Networks (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="5389b-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="5389b-216">Virtual Machines creadas a partir de recursos de Marketplace (no se pueden mover entre suscripciones).</span><span class="sxs-lookup"><span data-stu-id="5389b-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="5389b-217">Recurso necesita toobe canceló el aprovisionamiento en la suscripción actual de Hola y volver a implementarse en nueva suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="5389b-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="5389b-218">Limitaciones de App Service</span><span class="sxs-lookup"><span data-stu-id="5389b-218">App Service limitations</span></span>
<span data-ttu-id="5389b-219">Si se trabaja con aplicaciones de App Service, no se puede mover solo un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="5389b-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="5389b-220">aplicaciones de servicio de aplicaciones de toomove, las opciones son:</span><span class="sxs-lookup"><span data-stu-id="5389b-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="5389b-221">Mover hello plan de servicio de aplicaciones y todos los demás recursos de servicio de aplicaciones en dicho recurso grupo tooa nuevo grupo de recursos que ya no tiene los recursos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5389b-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="5389b-222">Este requisito significa que se debe mover incluso Hola recursos de servicio de aplicaciones que no están asociados con hello plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5389b-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="5389b-223">Mover grupo de recursos distinto de hello aplicaciones tooa, pero tenga todos los planes de servicio de aplicaciones en el grupo de recursos de hello original.</span><span class="sxs-lookup"><span data-stu-id="5389b-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="5389b-224">Hello plan no es necesario tooreside en el servicio de aplicaciones Hola mismo grupo de recursos como aplicación hello para hello aplicación toofunction correctamente.</span><span class="sxs-lookup"><span data-stu-id="5389b-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="5389b-225">Por ejemplo, si el grupo de recursos contiene:</span><span class="sxs-lookup"><span data-stu-id="5389b-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="5389b-226">**web-a** asociada a **plan-a**</span><span class="sxs-lookup"><span data-stu-id="5389b-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="5389b-227">**web-b** asociada a **plan-b**</span><span class="sxs-lookup"><span data-stu-id="5389b-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="5389b-228">Tendrá las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="5389b-228">Your options are:</span></span>

* <span data-ttu-id="5389b-229">Trasladar **web-a**, **plan-a**, **web-b** y **plan-b**</span><span class="sxs-lookup"><span data-stu-id="5389b-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="5389b-230">Trasladar **web-a** y **web-b**</span><span class="sxs-lookup"><span data-stu-id="5389b-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="5389b-231">Mover **web-a**</span><span class="sxs-lookup"><span data-stu-id="5389b-231">Move **web-a**</span></span>
* <span data-ttu-id="5389b-232">Mover **web-b**</span><span class="sxs-lookup"><span data-stu-id="5389b-232">Move **web-b**</span></span>

<span data-ttu-id="5389b-233">Todas las demás combinaciones implican dejar un tipo de recurso que debe trasladarse al mover un plan de App Service (cualquier tipo de recurso de App Service).</span><span class="sxs-lookup"><span data-stu-id="5389b-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="5389b-234">Si la aplicación web se encuentra en un grupo de recursos diferente que su plan de servicio de aplicaciones, pero desea toomove ambos tooa nuevo grupo de recursos, debe realizar el movimiento de hello en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="5389b-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="5389b-235">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5389b-235">For example:</span></span>

* <span data-ttu-id="5389b-236">**web-a** reside en **web-group**.</span><span class="sxs-lookup"><span data-stu-id="5389b-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="5389b-237">**plan-a** reside en **plan-group**.</span><span class="sxs-lookup"><span data-stu-id="5389b-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="5389b-238">Desea **web-a** y **un plan** tooreside en **grupo combinado**</span><span class="sxs-lookup"><span data-stu-id="5389b-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="5389b-239">tooaccomplish Esto mueve, realizar dos operaciones de movimiento independientes en hello sigue secuencia:</span><span class="sxs-lookup"><span data-stu-id="5389b-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="5389b-240">Mover hello **web-a** demasiado**grupo de plan**</span><span class="sxs-lookup"><span data-stu-id="5389b-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="5389b-241">Mover **web-a** y **un plan** demasiado**grupo combinado**.</span><span class="sxs-lookup"><span data-stu-id="5389b-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="5389b-242">Puede mover un nuevo grupo de recursos de certificado de servicio de aplicación tooa o suscripción sin ningún problema.</span><span class="sxs-lookup"><span data-stu-id="5389b-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="5389b-243">Sin embargo, si la aplicación web incluye un certificado SSL que adquirió externamente y toohello aplicación ha cargado, debe eliminar certificado de hello antes de la aplicación móvil de web de hello.</span><span class="sxs-lookup"><span data-stu-id="5389b-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="5389b-244">Por ejemplo, puede realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5389b-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="5389b-245">Eliminar certificado de hello cargado desde la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="5389b-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="5389b-246">Mueva la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="5389b-246">Move hello web app</span></span>
3. <span data-ttu-id="5389b-247">Cargar la aplicación web de hello certificado toohello</span><span class="sxs-lookup"><span data-stu-id="5389b-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="5389b-248">Limitaciones de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="5389b-248">Recovery Services limitations</span></span>
<span data-ttu-id="5389b-249">Movimiento no está habilitada para el almacenamiento, red, o los recursos de proceso usan tooset la recuperación ante desastres con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5389b-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="5389b-250">Por ejemplo, suponga que ha configurado la replicación de la cuenta de almacenamiento de tooa de máquinas locales (Storage1) y desee Hola protegido máquina toocome seguridad después de la conmutación por error tooAzure como una máquina virtual (VM1) había conectado a la red virtual de tooa (Network1).</span><span class="sxs-lookup"><span data-stu-id="5389b-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="5389b-251">No se puede mover cualquiera de estos recursos de Azure - Storage1, VM1, y Network1 - a través de recursos grupos dentro de hello misma suscripción o a través de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="5389b-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="5389b-252">Limitaciones de HDInsight</span><span class="sxs-lookup"><span data-stu-id="5389b-252">HDInsight limitations</span></span>

<span data-ttu-id="5389b-253">Puede mover HDInsight clústeres tooa nueva suscripción o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="5389b-254">Sin embargo, no se puede mover a través de hello suscripciones redes de clúster de HDInsight toohello vinculado de recursos (por ejemplo, la red virtual de hello, NIC o equilibrador de carga).</span><span class="sxs-lookup"><span data-stu-id="5389b-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="5389b-255">Además, no se puede mover el grupo de recursos nuevo tooa una NIC que está adjunto tooa virtual machine para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="5389b-256">Al mover una suscripción nuevo de tooa de clúster de HDInsight, mueva primero otros recursos (como cuenta de almacenamiento de hello).</span><span class="sxs-lookup"><span data-stu-id="5389b-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="5389b-257">A continuación, mover el clúster de HDInsight de Hola por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="5389b-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="5389b-258">limitaciones de la implementación clásica</span><span class="sxs-lookup"><span data-stu-id="5389b-258">Classic deployment limitations</span></span>
<span data-ttu-id="5389b-259">Hello opciones para mover recursos implementados a través del modelo clásico Hola varían en función de si va a mover recursos Hola dentro de una suscripción o tooa nuevo.</span><span class="sxs-lookup"><span data-stu-id="5389b-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="5389b-260">Misma suscripción</span><span class="sxs-lookup"><span data-stu-id="5389b-260">Same subscription</span></span>
<span data-ttu-id="5389b-261">Al mover los recursos del grupo de recursos tooanother un recurso de grupo dentro de la misma suscripción, Hola siguientes restricciones se aplican de Hola:</span><span class="sxs-lookup"><span data-stu-id="5389b-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="5389b-262">No se pueden mover redes virtuales (clásico).</span><span class="sxs-lookup"><span data-stu-id="5389b-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="5389b-263">Máquinas virtuales (clásicas) se deben mover con el servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="5389b-264">Servicio de nube solo puede aplicarse al movimiento de hello incluye todas sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5389b-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="5389b-265">Solo se puede mover un servicio en la nube cada vez.</span><span class="sxs-lookup"><span data-stu-id="5389b-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="5389b-266">Solo se puede mover una cuenta de almacenamiento (clásico) cada vez.</span><span class="sxs-lookup"><span data-stu-id="5389b-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="5389b-267">No se puede mover la cuenta de almacenamiento (clásica) en hello misma operación con una máquina virtual o un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="5389b-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="5389b-268">toomove recursos clásicos tooa nuevo grupo de recursos en Hola misma suscripción, utilice las operaciones de movimiento estándar de Hola a través de hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), o [API de REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="5389b-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="5389b-269">Usa Hola mismas operaciones que use para mover recursos del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="5389b-270">Suscripción nueva</span><span class="sxs-lookup"><span data-stu-id="5389b-270">New subscription</span></span>
<span data-ttu-id="5389b-271">Al mover tooa nueva suscripción de recursos, se aplica Hola siguientes restricciones:</span><span class="sxs-lookup"><span data-stu-id="5389b-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="5389b-272">Se deben mover todos los recursos clásicos de suscripción de Hola Hola misma operación.</span><span class="sxs-lookup"><span data-stu-id="5389b-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="5389b-273">suscripción de destino de Hello no debe contener ningún otro recurso clásico.</span><span class="sxs-lookup"><span data-stu-id="5389b-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="5389b-274">Hola movimiento solo se puede solicitar a través de una API de REST independiente para movimientos clásicos.</span><span class="sxs-lookup"><span data-stu-id="5389b-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="5389b-275">comandos de movimiento de administrador de recursos estándar de Hello no funcionan al mover la nueva suscripción de recursos clásicos tooa.</span><span class="sxs-lookup"><span data-stu-id="5389b-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="5389b-276">toomove recursos clásicos tooa nueva suscripción, operaciones de REST de Hola de uso son recursos tooclassic específicos.</span><span class="sxs-lookup"><span data-stu-id="5389b-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="5389b-277">toouse REST, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5389b-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="5389b-278">Compruebe si la suscripción de origen Hola puede participar en una suscripción entre mover.</span><span class="sxs-lookup"><span data-stu-id="5389b-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="5389b-279">Usar hello después de operación:</span><span class="sxs-lookup"><span data-stu-id="5389b-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="5389b-280">En el cuerpo de la solicitud de hello, incluya:</span><span class="sxs-lookup"><span data-stu-id="5389b-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="5389b-281">respuesta de Hello para la operación de validación de hello es Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="5389b-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="5389b-282">Compruebe si la suscripción de destino de hello puede participar en una suscripción entre mover.</span><span class="sxs-lookup"><span data-stu-id="5389b-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="5389b-283">Usar hello después de operación:</span><span class="sxs-lookup"><span data-stu-id="5389b-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="5389b-284">En el cuerpo de la solicitud de hello, incluya:</span><span class="sxs-lookup"><span data-stu-id="5389b-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="5389b-285">respuesta de Hello es en el mismo formato que la validación de suscripción del origen de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="5389b-286">Si ambas suscripciones pasan la validación, mover todos los recursos clásicos de suscripción de tooanother de una suscripción con hello después de operación:</span><span class="sxs-lookup"><span data-stu-id="5389b-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="5389b-287">En el cuerpo de la solicitud de hello, incluya:</span><span class="sxs-lookup"><span data-stu-id="5389b-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="5389b-288">operación de Hello puede llevar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="5389b-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="5389b-289">Mediante el portal</span><span class="sxs-lookup"><span data-stu-id="5389b-289">Use portal</span></span>
<span data-ttu-id="5389b-290">toomove recursos, seleccione grupo de recursos de Hola que contiene esos recursos y, a continuación, seleccione hello **mover** botón.</span><span class="sxs-lookup"><span data-stu-id="5389b-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Mover recursos](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="5389b-292">Seleccione si va a mover Hola recursos tooa nuevo grupo de recursos o una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="5389b-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="5389b-293">Seleccione toomove de recursos de Hola y el grupo de recursos de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="5389b-294">Confirmar que necesite tooupdate scripts para estos recursos y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5389b-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="5389b-295">Si ha seleccionado el icono de suscripción de edición de hello en el paso anterior de hello, también debe seleccionar la suscripción de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![seleccionar destino](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="5389b-297">En **notificaciones**, verá que Hola mover la operación se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="5389b-297">In **Notifications**, you see that hello move operation is running.</span></span>

![mostrar el estado del traslado](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="5389b-299">Cuando se ha completado, se le notificará de resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="5389b-299">When it has completed, you are notified of hello result.</span></span>

![mostrar el resultado del traslado](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="5389b-301">Uso de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5389b-301">Use PowerShell</span></span>
<span data-ttu-id="5389b-302">existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello `Move-AzureRmResource` comando.</span><span class="sxs-lookup"><span data-stu-id="5389b-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="5389b-303">Hola el primer ejemplo se muestra cómo toomove un recurso tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="5389b-304">Hola segundo ejemplo se muestra cómo toomove varios recursos tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="5389b-305">toomove tooa nueva suscripción, especifique un valor para hello `DestinationSubscriptionId` parámetro.</span><span class="sxs-lookup"><span data-stu-id="5389b-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="5389b-306">Se le pide tooconfirm que desea toomove Hola de los recursos especificados.</span><span class="sxs-lookup"><span data-stu-id="5389b-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="5389b-307">Uso de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5389b-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="5389b-308">existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello `az resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="5389b-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="5389b-309">Proporcionar Hola identificadores de recursos de hello recursos toomove.</span><span class="sxs-lookup"><span data-stu-id="5389b-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="5389b-310">Puede obtener Id. de recurso con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5389b-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="5389b-311">Hola de ejemplo siguiente muestra cómo toomove un almacenamiento cuenta tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="5389b-312">Hola `--ids` parámetro, proporcionan una lista separada por espacios de toomove de identificadores de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="5389b-313">toomove tooa nueva suscripción, proporcione hello `--destination-subscription-id` parámetro.</span><span class="sxs-lookup"><span data-stu-id="5389b-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="5389b-314">Uso de CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="5389b-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="5389b-315">existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello `azure resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="5389b-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="5389b-316">Proporcionar Hola identificadores de recursos de hello recursos toomove.</span><span class="sxs-lookup"><span data-stu-id="5389b-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="5389b-317">Puede obtener Id. de recurso con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5389b-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="5389b-318">Que devuelve Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="5389b-318">Which returns hello following format:</span></span>

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

<span data-ttu-id="5389b-319">Hola de ejemplo siguiente muestra cómo toomove un almacenamiento cuenta tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5389b-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="5389b-320">Hola `-i` parámetro, proporcione una lista separada por comas de toomove de identificadores de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5389b-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="5389b-321">Se le pide tooconfirm que desea toomove Hola el recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="5389b-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="5389b-322">Use la API de REST</span><span class="sxs-lookup"><span data-stu-id="5389b-322">Use REST API</span></span>
<span data-ttu-id="5389b-323">grupo de recursos de recursos existente de toomove tooanother o suscripción, ejecute:</span><span class="sxs-lookup"><span data-stu-id="5389b-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="5389b-324">En el cuerpo de la solicitud de hello, especifique el grupo de recursos de destino de Hola y Hola recursos toomove.</span><span class="sxs-lookup"><span data-stu-id="5389b-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="5389b-325">Para obtener más información acerca de la operación de REST de movimiento de hello, consulte [mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="5389b-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5389b-326">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5389b-326">Next steps</span></span>
* <span data-ttu-id="5389b-327">toolearn acerca de los cmdlets de PowerShell para administrar su suscripción, vea [con Azure PowerShell con el Administrador de recursos](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5389b-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="5389b-328">toolearn acerca de los comandos de CLI de Azure para administrar su suscripción, vea [Using Hola CLI de Azure con el Administrador de recursos](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5389b-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="5389b-329">toolearn acerca de características del portal para administrar su suscripción, vea [uso de recursos de Azure toomanage portal hello](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5389b-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="5389b-330">toolearn acerca de cómo aplicar un recurso de tooyour organización lógica, consulte [mediante etiquetas tooorganize los recursos de](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="5389b-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
