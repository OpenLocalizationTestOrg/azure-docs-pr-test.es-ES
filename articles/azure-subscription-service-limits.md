---
title: "suscripción aaaAzure límites y cuotas | Documentos de Microsoft"
description: "Se proporciona una lista de límites, cuotas y restricciones de suscripción y servicio comunes de Azure. Esto incluye información sobre cómo se limita tooincrease junto con los valores máximos."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="d0e62-104">Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d0e62-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="d0e62-105">Este documento enumeran algunos de los límites más comunes de Microsoft Azure hello, que a veces se denominan cuotas.</span><span class="sxs-lookup"><span data-stu-id="d0e62-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="d0e62-106">Actualmente, este documento no cubre todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e62-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="d0e62-107">Con el tiempo, lista de Hola se expandirá y actualiza toocover más de plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0e62-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="d0e62-108">Visite [información general de precios de Azure](https://azure.microsoft.com/pricing/) toolearn más información sobre precios de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e62-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="d0e62-109">Allí, puede calcular los costos mediante hello [Calculadora de precios de](https://azure.microsoft.com/pricing/calculator/) o visitando Hola precios página de detalles de un servicio (por ejemplo, [máquinas virtuales de Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="d0e62-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="d0e62-110">Para sugerencias toohelp administrar sus costos, vea [evitar costos inesperados con la administración de costos y facturación de Azure](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0e62-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d0e62-111">Si desea tooraise límite de Hola o cuota por encima de hello **límite predeterminado**, [abrir una solicitud de soporte al cliente en línea sin cargo](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="d0e62-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="d0e62-112">Hello límites no se generará anteriormente hello **límite máximo** valor mostrado en hello las tablas siguientes.</span><span class="sxs-lookup"><span data-stu-id="d0e62-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="d0e62-113">Si no hay ningún **límite máximo** columna, a continuación, recursos de hello no tiene límites ajustables.</span><span class="sxs-lookup"><span data-stu-id="d0e62-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="d0e62-114">Las suscripciones de evaluación gratuita no son aptas para aumentar el límite ni la cuota.</span><span class="sxs-lookup"><span data-stu-id="d0e62-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="d0e62-115">Si tiene una prueba gratuita, puede actualizar tooa [pago por uso](https://azure.microsoft.com/offers/ms-azr-0003p/) suscripción.</span><span class="sxs-lookup"><span data-stu-id="d0e62-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="d0e62-116">Para obtener más información, consulte [actualizar evaluación gratuita de Azure tooPay-como--Go](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="d0e62-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="d0e62-117">Límites y hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d0e62-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="d0e62-118">Ahora es posible toocombine varios recursos de Azure en tooa único grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e62-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="d0e62-119">Al utilizar grupos de recursos, los límites de una vez eran globales sea administrados a nivel regional con hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d0e62-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="d0e62-120">Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0e62-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="d0e62-121">En límites de Hola a continuación, una nueva tabla se ha agregado tooreflect las diferencias en los límites de cuando se usa hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d0e62-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="d0e62-122">Por ejemplo, hay una tabla de **Límites de suscripción** y una tabla de **Límites de suscripción - Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="d0e62-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="d0e62-123">Cuando un límite aplica a los escenarios de tooboth, solo se muestra en la primera tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0e62-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="d0e62-124">A menos que se indique lo contrario, los límites son globales en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="d0e62-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="d0e62-125">Es importante tooemphasize que las cuotas de recursos en los grupos de recursos de Azure son accesibles para la suscripción por región y no por suscripción, como las cuotas de administración del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0e62-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="d0e62-126">Usemos las cuotas de núcleo como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d0e62-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="d0e62-127">Si necesita toorequest una cuota aumentar con compatibilidad con núcleos, deberá toodecide cómo núcleos que desee toouse en cada región y, a continuación, realice una solicitud específica para el grupo de recursos de Azure principales cuotas para los importes de Hola y regiones que desee.</span><span class="sxs-lookup"><span data-stu-id="d0e62-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="d0e62-128">Por lo tanto, si necesita toouse 30 núcleos en Europa occidental toorun la aplicación en concreto, debe solicitar 30 núcleos en Europa occidental.</span><span class="sxs-lookup"><span data-stu-id="d0e62-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="d0e62-129">Pero no tendrá una cuota de núcleos de aumentar en ninguna otra región: Europa occidental solo tendrá cuota de núcleos de 30 Hola.</span><span class="sxs-lookup"><span data-stu-id="d0e62-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="d0e62-130">Como resultado, quizá le resulte útil tooconsider decidir lo que las cuotas de grupo de recursos de Azure necesitan toobe para la carga de trabajo en cualquier una región y de solicitud que importe en cada región en la que está considerando la implementación.</span><span class="sxs-lookup"><span data-stu-id="d0e62-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="d0e62-131">Consulte [solucionar problemas de implementación](resource-manager-common-deployment-errors.md) para obtener más ayuda para descubrir las cuotas actuales para regiones específicas.</span><span class="sxs-lookup"><span data-stu-id="d0e62-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="d0e62-132">Límites específicos del servicio</span><span class="sxs-lookup"><span data-stu-id="d0e62-132">Service-specific limits</span></span>
* [<span data-ttu-id="d0e62-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0e62-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="d0e62-134">API Management</span><span class="sxs-lookup"><span data-stu-id="d0e62-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="d0e62-135">App Service</span><span class="sxs-lookup"><span data-stu-id="d0e62-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="d0e62-136">Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d0e62-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="d0e62-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="d0e62-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="d0e62-138">Automatización</span><span class="sxs-lookup"><span data-stu-id="d0e62-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="d0e62-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d0e62-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="d0e62-140">Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="d0e62-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="d0e62-141">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="d0e62-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="d0e62-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d0e62-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="d0e62-143">Backup</span><span class="sxs-lookup"><span data-stu-id="d0e62-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="d0e62-144">Lote</span><span class="sxs-lookup"><span data-stu-id="d0e62-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="d0e62-145">Servicios de BizTalk</span><span class="sxs-lookup"><span data-stu-id="d0e62-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="d0e62-146">SERVICIO CDN</span><span class="sxs-lookup"><span data-stu-id="d0e62-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="d0e62-147">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="d0e62-148">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="d0e62-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="d0e62-149">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="d0e62-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="d0e62-150">Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="d0e62-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="d0e62-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d0e62-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="d0e62-152">DNS</span><span class="sxs-lookup"><span data-stu-id="d0e62-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="d0e62-153">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0e62-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="d0e62-154">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d0e62-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="d0e62-155">Key Vault</span><span class="sxs-lookup"><span data-stu-id="d0e62-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="d0e62-156">Log Analytics/Operational Insights</span><span class="sxs-lookup"><span data-stu-id="d0e62-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="d0e62-157">Media Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="d0e62-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0e62-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="d0e62-159">Mobile Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="d0e62-160">Supervisión</span><span class="sxs-lookup"><span data-stu-id="d0e62-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="d0e62-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d0e62-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="d0e62-162">Redes</span><span class="sxs-lookup"><span data-stu-id="d0e62-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="d0e62-163">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d0e62-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="d0e62-164">Servicio Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="d0e62-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="d0e62-165">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d0e62-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="d0e62-166">Scheduler</span><span class="sxs-lookup"><span data-stu-id="d0e62-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="d0e62-167">Search</span><span class="sxs-lookup"><span data-stu-id="d0e62-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="d0e62-168">Service Bus</span><span class="sxs-lookup"><span data-stu-id="d0e62-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="d0e62-169">Recuperación de sitios</span><span class="sxs-lookup"><span data-stu-id="d0e62-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="d0e62-170">SQL Database</span><span class="sxs-lookup"><span data-stu-id="d0e62-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="d0e62-171">Storage</span><span class="sxs-lookup"><span data-stu-id="d0e62-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="d0e62-172">Sistema de StorSimple</span><span class="sxs-lookup"><span data-stu-id="d0e62-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="d0e62-173">Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="d0e62-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="d0e62-174">Suscripción</span><span class="sxs-lookup"><span data-stu-id="d0e62-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="d0e62-175">Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="d0e62-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="d0e62-176">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="d0e62-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="d0e62-177">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d0e62-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="d0e62-178">Límites de suscripción</span><span class="sxs-lookup"><span data-stu-id="d0e62-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="d0e62-179">Límites de suscripción</span><span class="sxs-lookup"><span data-stu-id="d0e62-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="d0e62-180">Límites de suscripción - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d0e62-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="d0e62-181">Hola siguiendo los límites se aplica al utilizar grupos de recursos de Azure y hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d0e62-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="d0e62-182">Los límites que no han cambiado con hello Azure Resource Manager no se muestran a continuación.</span><span class="sxs-lookup"><span data-stu-id="d0e62-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="d0e62-183">Consulte la tabla anterior toohello para esos límites.</span><span class="sxs-lookup"><span data-stu-id="d0e62-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="d0e62-184">Para información sobre el control de límites en las solicitudes de Resource Manager, consulte ///[Throttling Resource Manager requests](resource-manager-request-limits.md) (Limitación de las solicitudes de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="d0e62-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="d0e62-185">Límites de grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="d0e62-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="d0e62-186">Límites de Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="d0e62-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="d0e62-187">Límites de Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="d0e62-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="d0e62-188">Límites de Virtual Machines: Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d0e62-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="d0e62-189">Hola siguiendo los límites se aplica al utilizar grupos de recursos de Azure y hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d0e62-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="d0e62-190">Los límites que no han cambiado con hello Azure Resource Manager no se muestran a continuación.</span><span class="sxs-lookup"><span data-stu-id="d0e62-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="d0e62-191">Consulte la tabla anterior toohello para esos límites.</span><span class="sxs-lookup"><span data-stu-id="d0e62-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="d0e62-192">Límites de los conjuntos de escalas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d0e62-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="d0e62-193">Límites de Container Instances</span><span class="sxs-lookup"><span data-stu-id="d0e62-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="d0e62-194">Límites de red</span><span class="sxs-lookup"><span data-stu-id="d0e62-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="d0e62-195">Límites de red</span><span class="sxs-lookup"><span data-stu-id="d0e62-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="d0e62-196">Límites de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d0e62-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="d0e62-197">Límites de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d0e62-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="d0e62-198">Límites de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d0e62-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="d0e62-199">Límites de DNS</span><span class="sxs-lookup"><span data-stu-id="d0e62-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="d0e62-200">Límites de Storage</span><span class="sxs-lookup"><span data-stu-id="d0e62-200">Storage limits</span></span>
<span data-ttu-id="d0e62-201">Para más información sobre los límites de la cuenta de almacenamiento, vea [Objetivos de escalabilidad y rendimiento de Azure Storage](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="d0e62-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="d0e62-202">Límites del servicio de Storage</span><span class="sxs-lookup"><span data-stu-id="d0e62-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="d0e62-203">Límites de discos de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d0e62-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="d0e62-204">Consulte [Tamaños de máquina virtual](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="d0e62-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="d0e62-205">Discos de máquinas virtuales administrados</span><span class="sxs-lookup"><span data-stu-id="d0e62-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="d0e62-206">Discos de máquinas virtuales no administrados</span><span class="sxs-lookup"><span data-stu-id="d0e62-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="d0e62-207">Límites de proveedor de recursos de Storage</span><span class="sxs-lookup"><span data-stu-id="d0e62-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="d0e62-208">Límites de Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="d0e62-209">Límites de App Service</span><span class="sxs-lookup"><span data-stu-id="d0e62-209">App Service limits</span></span>
<span data-ttu-id="d0e62-210">siguiente Hola que limita de servicio de aplicaciones incluye límites para las aplicaciones Web, aplicaciones móviles, aplicaciones de API y las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="d0e62-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="d0e62-211">Límites de Scheduler</span><span class="sxs-lookup"><span data-stu-id="d0e62-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="d0e62-212">Límites de Batch</span><span class="sxs-lookup"><span data-stu-id="d0e62-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="d0e62-213">Límites de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-213">BizTalk Services limits</span></span>
<span data-ttu-id="d0e62-214">Hello tabla siguiente muestran los límites de hello de servicios de Biztalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e62-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="d0e62-215">Límites de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d0e62-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="d0e62-216">Base de datos de Cosmos Azure es una base de datos de escala global en las que el rendimiento y el almacenamiento pueden toohandle escalado lo que requiere la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0e62-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="d0e62-217">Si tiene alguna pregunta sobre la escala de hello proporciona la base de datos de Azure Cosmos, envíe un correo electrónico tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="d0e62-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="d0e62-218">Límites de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0e62-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="d0e62-219">Límites de Search</span><span class="sxs-lookup"><span data-stu-id="d0e62-219">Search limits</span></span>
<span data-ttu-id="d0e62-220">Niveles de precios determinan la capacidad de Hola y límites de su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="d0e62-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="d0e62-221">Los planes incluyen:</span><span class="sxs-lookup"><span data-stu-id="d0e62-221">Tiers include:</span></span>

* <span data-ttu-id="d0e62-222">*Gratis* , compartido con otros suscriptores de Azure, se ha diseñado para proyectos de evaluación y de desarrollo de pequeña envergadura.</span><span class="sxs-lookup"><span data-stu-id="d0e62-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="d0e62-223">*Básico* proporciona recursos informáticos dedicados para cargas de trabajo de producción en una escala más pequeña, con seguridad de réplicas de toothree para cargas de trabajo de consulta de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="d0e62-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="d0e62-224">*Estándar (S1, S2, S3, S3 de alta densidad)* es para mayores cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="d0e62-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="d0e62-225">Varios niveles existen dentro de nivel estándar de Hola para que pueda elegir una configuración de recursos que mejor coincida con el perfil de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d0e62-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="d0e62-226">**Límites por suscripción**</span><span class="sxs-lookup"><span data-stu-id="d0e62-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="d0e62-227">**Límites por servicio de búsqueda**</span><span class="sxs-lookup"><span data-stu-id="d0e62-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="d0e62-228">toolearn más información acerca de los límites en un nivel más granular, como el tamaño del documento, las consultas por segundo, las claves, las solicitudes y respuestas, vea [límites en la búsqueda de Azure del servicio](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="d0e62-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="d0e62-229">Límites de Media Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="d0e62-230">Límites de red CDN</span><span class="sxs-lookup"><span data-stu-id="d0e62-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="d0e62-231">Límites de Mobile Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="d0e62-232">Límites de Monitor</span><span class="sxs-lookup"><span data-stu-id="d0e62-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="d0e62-233">Límites de servicio de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="d0e62-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="d0e62-234">Límites de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0e62-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="d0e62-235">Límites de Service Bus</span><span class="sxs-lookup"><span data-stu-id="d0e62-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="d0e62-236">Límites de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d0e62-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="d0e62-237">Límites de Data Factory</span><span class="sxs-lookup"><span data-stu-id="d0e62-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="d0e62-238">Límites de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d0e62-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="d0e62-239">Límites de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d0e62-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="d0e62-240">Límites de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0e62-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="d0e62-241">Límites de Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0e62-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="d0e62-242">Límites de Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="d0e62-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="d0e62-243">Límites de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d0e62-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="d0e62-244">Límites del sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="d0e62-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="d0e62-245">Límites de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d0e62-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="d0e62-246">Límites de Backup</span><span class="sxs-lookup"><span data-stu-id="d0e62-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="d0e62-247">Límites de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d0e62-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="d0e62-248">Límites de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d0e62-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="d0e62-249">Límites de API Management</span><span class="sxs-lookup"><span data-stu-id="d0e62-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="d0e62-250">Límites de Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="d0e62-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="d0e62-251">Límites de Key Vault</span><span class="sxs-lookup"><span data-stu-id="d0e62-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="d0e62-252">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d0e62-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="d0e62-253">Límites de Automation</span><span class="sxs-lookup"><span data-stu-id="d0e62-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="d0e62-254">Límites de SQL Database</span><span class="sxs-lookup"><span data-stu-id="d0e62-254">SQL Database limits</span></span>
<span data-ttu-id="d0e62-255">Para conocer los límites de SQL Database, vea [Límites de recursos de SQL Database](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d0e62-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d0e62-256">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d0e62-256">See also</span></span>
[<span data-ttu-id="d0e62-257">Concepto de límites de Azure y aumento de los mismos</span><span class="sxs-lookup"><span data-stu-id="d0e62-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="d0e62-258">Tamaños de máquinas virtuales y servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="d0e62-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="d0e62-259">Tamaños de Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d0e62-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

