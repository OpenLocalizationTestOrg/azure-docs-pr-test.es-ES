---
title: "tooresource aaaIntroduction solución de problemas en el Monitor de red de Azure | Documentos de Microsoft"
description: "Esta página proporciona una visión general de las capacidades de solución de problemas de recursos de Monitor de red de Hola"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="d0437-103">Tooresource de introducción para solucionar problemas de Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="d0437-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="d0437-104">Las puertas de enlace de red virtual proporcionan conectividad entre recursos locales y otras redes virtuales dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0437-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="d0437-105">Estas puertas de enlace y sus conexiones de supervisión es fundamental tooensuring comunicación no se interrumpe.</span><span class="sxs-lookup"><span data-stu-id="d0437-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="d0437-106">Monitor de red proporciona Hola capacidad tootroubleshoot puertas de enlace de red Virtual y las conexiones.</span><span class="sxs-lookup"><span data-stu-id="d0437-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="d0437-107">Se puede llamar a través del portal de hello, PowerShell, CLI o API de REST.</span><span class="sxs-lookup"><span data-stu-id="d0437-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="d0437-108">Cuando se llama, Monitor de red diagnostica mantenimiento Hola de puerta de enlace de red virtual de Hola o conexión y los resultados adecuados de hello devuelto.</span><span class="sxs-lookup"><span data-stu-id="d0437-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="d0437-109">Esta solicitud es una transacción de larga duración, se devuelve el resultado de hello cuando se complete el diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="d0437-111">Results</span><span class="sxs-lookup"><span data-stu-id="d0437-111">Results</span></span>

<span data-ttu-id="d0437-112">Hola preliminar resultados proporcionan una perspectiva general del estado de saludo del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="d0437-113">Puede proporcionar información más detallada para recursos tal y como se muestra en los pasos de la sección de hello:</span><span class="sxs-lookup"><span data-stu-id="d0437-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="d0437-114">Hello siguiente lista es la API de solucionar problemas de valores de hello devueltos con hello:</span><span class="sxs-lookup"><span data-stu-id="d0437-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="d0437-115">**startTime** -este valor es el tiempo de Hola Hola solucionar problemas de llamada de API que se inició.</span><span class="sxs-lookup"><span data-stu-id="d0437-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="d0437-116">**hora de finalización** -este valor es la hora hello en que finalizó la solución de problemas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="d0437-117">**code**: este valor es UnHealthy si se produce un único error de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="d0437-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="d0437-118">**resultados** -resultados es un conjunto de resultados devuelto en la puerta de enlace de red virtual de conexión o hello de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="d0437-119">**Id. de** -este valor es el tipo de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="d0437-120">**resumen** -este valor es un resumen de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="d0437-121">**detallada** -este valor proporciona una descripción detallada del error de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="d0437-122">**recommendedActions** -esta propiedad es una colección de las acciones recomendadas tootake.</span><span class="sxs-lookup"><span data-stu-id="d0437-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="d0437-123">**actionText** -este valor contiene texto hello que describe qué tootake de acción.</span><span class="sxs-lookup"><span data-stu-id="d0437-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="d0437-124">**actionUri** -este valor proporciona Hola URI toodocumentation acerca de cómo tooact.</span><span class="sxs-lookup"><span data-stu-id="d0437-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="d0437-125">**actionUriText** -este valor es una breve descripción de texto de acción de hello.</span><span class="sxs-lookup"><span data-stu-id="d0437-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="d0437-126">Hola siguientes tablas muestran Hola diferentes tipos de error (Id. en los resultados de hello precede a lista) que están disponibles y si el error de hello crea registros.</span><span class="sxs-lookup"><span data-stu-id="d0437-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="d0437-127">Puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="d0437-127">Gateway</span></span>

| <span data-ttu-id="d0437-128">Tipo de error</span><span class="sxs-lookup"><span data-stu-id="d0437-128">Fault Type</span></span> | <span data-ttu-id="d0437-129">Motivo</span><span class="sxs-lookup"><span data-stu-id="d0437-129">Reason</span></span> | <span data-ttu-id="d0437-130">Registro</span><span class="sxs-lookup"><span data-stu-id="d0437-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="d0437-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="d0437-131">NoFault</span></span> | <span data-ttu-id="d0437-132">Cuando no se detecta ningún error.</span><span class="sxs-lookup"><span data-stu-id="d0437-132">When no error is detected.</span></span> |<span data-ttu-id="d0437-133">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-133">Yes</span></span>|
| <span data-ttu-id="d0437-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="d0437-134">GatewayNotFound</span></span> | <span data-ttu-id="d0437-135">No se encuentra la puerta de enlace o no está aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="d0437-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="d0437-136">No</span><span class="sxs-lookup"><span data-stu-id="d0437-136">No</span></span>|
| <span data-ttu-id="d0437-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="d0437-137">PlannedMaintenance</span></span> |  <span data-ttu-id="d0437-138">La instancia de puerta de enlace está en mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="d0437-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="d0437-139">No</span><span class="sxs-lookup"><span data-stu-id="d0437-139">No</span></span>|
| <span data-ttu-id="d0437-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="d0437-140">UserDrivenUpdate</span></span> | <span data-ttu-id="d0437-141">Cuando hay una actualización del usuario en curso.</span><span class="sxs-lookup"><span data-stu-id="d0437-141">When a user update is in progress.</span></span> <span data-ttu-id="d0437-142">Podría tratarse de una operación de cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="d0437-142">This could be a resize operation.</span></span> | <span data-ttu-id="d0437-143">No</span><span class="sxs-lookup"><span data-stu-id="d0437-143">No</span></span> |
| <span data-ttu-id="d0437-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="d0437-144">VipUnResponsive</span></span> | <span data-ttu-id="d0437-145">No se puede llegar a la instancia principal de Hola de hello puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d0437-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="d0437-146">Esto sucede cuando se produce un error de sondeo de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="d0437-147">No</span><span class="sxs-lookup"><span data-stu-id="d0437-147">No</span></span> |
| <span data-ttu-id="d0437-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="d0437-148">PlatformInActive</span></span> | <span data-ttu-id="d0437-149">Hay un problema con la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="d0437-150">No</span><span class="sxs-lookup"><span data-stu-id="d0437-150">No</span></span>|
| <span data-ttu-id="d0437-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="d0437-151">ServiceNotRunning</span></span> | <span data-ttu-id="d0437-152">no se está ejecutando el servicio subyacente Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-152">hello underlying service is not running.</span></span> | <span data-ttu-id="d0437-153">No</span><span class="sxs-lookup"><span data-stu-id="d0437-153">No</span></span>|
| <span data-ttu-id="d0437-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="d0437-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="d0437-155">No hay ninguna conexión existe en la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="d0437-156">Esto es solo una advertencia.</span><span class="sxs-lookup"><span data-stu-id="d0437-156">This is only a warning.</span></span>| <span data-ttu-id="d0437-157">No</span><span class="sxs-lookup"><span data-stu-id="d0437-157">No</span></span>|
| <span data-ttu-id="d0437-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="d0437-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="d0437-159">Las conexiones no están conectadas.</span><span class="sxs-lookup"><span data-stu-id="d0437-159">Connections are not connected.</span></span> <span data-ttu-id="d0437-160">Esto es solo una advertencia.</span><span class="sxs-lookup"><span data-stu-id="d0437-160">This is only a warning.</span></span>| <span data-ttu-id="d0437-161">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-161">Yes</span></span>|
| <span data-ttu-id="d0437-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="d0437-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="d0437-163">uso de CPU de la puerta de enlace actual de Hello es > 95%.</span><span class="sxs-lookup"><span data-stu-id="d0437-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="d0437-164">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="d0437-165">Conexión</span><span class="sxs-lookup"><span data-stu-id="d0437-165">Connection</span></span>

| <span data-ttu-id="d0437-166">Tipo de error</span><span class="sxs-lookup"><span data-stu-id="d0437-166">Fault Type</span></span> | <span data-ttu-id="d0437-167">Motivo</span><span class="sxs-lookup"><span data-stu-id="d0437-167">Reason</span></span> | <span data-ttu-id="d0437-168">Registro</span><span class="sxs-lookup"><span data-stu-id="d0437-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="d0437-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="d0437-169">NoFault</span></span> | <span data-ttu-id="d0437-170">Cuando no se detecta ningún error.</span><span class="sxs-lookup"><span data-stu-id="d0437-170">When no error is detected.</span></span> |<span data-ttu-id="d0437-171">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-171">Yes</span></span>|
| <span data-ttu-id="d0437-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="d0437-172">GatewayNotFound</span></span> | <span data-ttu-id="d0437-173">No se encuentra la puerta de enlace o no está aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="d0437-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="d0437-174">No</span><span class="sxs-lookup"><span data-stu-id="d0437-174">No</span></span>|
| <span data-ttu-id="d0437-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="d0437-175">PlannedMaintenance</span></span> | <span data-ttu-id="d0437-176">La instancia de puerta de enlace está en mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="d0437-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="d0437-177">No</span><span class="sxs-lookup"><span data-stu-id="d0437-177">No</span></span>|
| <span data-ttu-id="d0437-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="d0437-178">UserDrivenUpdate</span></span> | <span data-ttu-id="d0437-179">Cuando hay una actualización del usuario en curso.</span><span class="sxs-lookup"><span data-stu-id="d0437-179">When a user update is in progress.</span></span> <span data-ttu-id="d0437-180">Podría tratarse de una operación de cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="d0437-180">This could be a resize operation.</span></span>  | <span data-ttu-id="d0437-181">No</span><span class="sxs-lookup"><span data-stu-id="d0437-181">No</span></span> |
| <span data-ttu-id="d0437-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="d0437-182">VipUnResponsive</span></span> | <span data-ttu-id="d0437-183">No se puede llegar a la instancia principal de Hola de hello puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d0437-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="d0437-184">Se produce cuando se produce un error de sondeo de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="d0437-185">No</span><span class="sxs-lookup"><span data-stu-id="d0437-185">No</span></span> |
| <span data-ttu-id="d0437-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="d0437-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="d0437-187">Falta una configuración de conexión.</span><span class="sxs-lookup"><span data-stu-id="d0437-187">Connection configuration is missing.</span></span> | <span data-ttu-id="d0437-188">No</span><span class="sxs-lookup"><span data-stu-id="d0437-188">No</span></span> |
| <span data-ttu-id="d0437-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="d0437-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="d0437-190">Hola conexión está marcada como "desconectada".</span><span class="sxs-lookup"><span data-stu-id="d0437-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="d0437-191">No</span><span class="sxs-lookup"><span data-stu-id="d0437-191">No</span></span>|
| <span data-ttu-id="d0437-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="d0437-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="d0437-193">servicio de Hello subyacente no tiene Hola que conexión configurada.</span><span class="sxs-lookup"><span data-stu-id="d0437-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="d0437-194">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-194">Yes</span></span> |
| <span data-ttu-id="d0437-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="d0437-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="d0437-196">Hola servicio subyacente está marcada como en espera.</span><span class="sxs-lookup"><span data-stu-id="d0437-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="d0437-197">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-197">Yes</span></span>|
| <span data-ttu-id="d0437-198">Autenticación</span><span class="sxs-lookup"><span data-stu-id="d0437-198">Authentication</span></span> | <span data-ttu-id="d0437-199">Error de coincidencia de clave previamente compartida.</span><span class="sxs-lookup"><span data-stu-id="d0437-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="d0437-200">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-200">Yes</span></span>|
| <span data-ttu-id="d0437-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="d0437-201">PeerReachability</span></span> | <span data-ttu-id="d0437-202">puerta de enlace de Hello del mismo nivel no está accesible.</span><span class="sxs-lookup"><span data-stu-id="d0437-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="d0437-203">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-203">Yes</span></span>|
| <span data-ttu-id="d0437-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="d0437-204">IkePolicyMismatch</span></span> | <span data-ttu-id="d0437-205">puerta de enlace de Hello del mismo nivel tiene directivas IKE que no son compatibles con Azure.</span><span class="sxs-lookup"><span data-stu-id="d0437-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="d0437-206">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-206">Yes</span></span>|
| <span data-ttu-id="d0437-207">Error de WfpParse</span><span class="sxs-lookup"><span data-stu-id="d0437-207">WfpParse Error</span></span> | <span data-ttu-id="d0437-208">Error al registro WFP Hola análisis.</span><span class="sxs-lookup"><span data-stu-id="d0437-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="d0437-209">Sí</span><span class="sxs-lookup"><span data-stu-id="d0437-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="d0437-210">Tipos de puerta de enlace admitidos</span><span class="sxs-lookup"><span data-stu-id="d0437-210">Supported Gateway types</span></span>

<span data-ttu-id="d0437-211">Hello lista siguiente se muestran compatibilidad hello muestra que las puertas de enlace y las conexiones son compatibles con la solución de problemas de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="d0437-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="d0437-212">**Tipos de puerta de enlace**</span><span class="sxs-lookup"><span data-stu-id="d0437-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="d0437-213">VPN</span><span class="sxs-lookup"><span data-stu-id="d0437-213">VPN</span></span>      | <span data-ttu-id="d0437-214">Compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-214">Supported</span></span>        |
|<span data-ttu-id="d0437-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d0437-215">ExpressRoute</span></span> | <span data-ttu-id="d0437-216">No compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-216">Not Supported</span></span> |
|<span data-ttu-id="d0437-217">HyperNet</span><span class="sxs-lookup"><span data-stu-id="d0437-217">Hypernet</span></span> | <span data-ttu-id="d0437-218">No compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-218">Not Supported</span></span>|
|<span data-ttu-id="d0437-219">**Tipos de VPN**</span><span class="sxs-lookup"><span data-stu-id="d0437-219">**VPN types**</span></span> | |
|<span data-ttu-id="d0437-220">Basado en ruta</span><span class="sxs-lookup"><span data-stu-id="d0437-220">Route Based</span></span> | <span data-ttu-id="d0437-221">Compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-221">Supported</span></span>|
|<span data-ttu-id="d0437-222">Basado en directiva</span><span class="sxs-lookup"><span data-stu-id="d0437-222">Policy Based</span></span> | <span data-ttu-id="d0437-223">No compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-223">Not Supported</span></span>|
|<span data-ttu-id="d0437-224">**Tipos de conexión**</span><span class="sxs-lookup"><span data-stu-id="d0437-224">**Connection types**</span></span>||
|<span data-ttu-id="d0437-225">IPSec</span><span class="sxs-lookup"><span data-stu-id="d0437-225">IPSec</span></span>| <span data-ttu-id="d0437-226">Compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-226">Supported</span></span>|
|<span data-ttu-id="d0437-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="d0437-227">VNet2Vnet</span></span>| <span data-ttu-id="d0437-228">Compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-228">Supported</span></span>|
|<span data-ttu-id="d0437-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d0437-229">ExpressRoute</span></span>| <span data-ttu-id="d0437-230">No compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-230">Not Supported</span></span>|
|<span data-ttu-id="d0437-231">HyperNet</span><span class="sxs-lookup"><span data-stu-id="d0437-231">Hypernet</span></span>| <span data-ttu-id="d0437-232">No compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-232">Not Supported</span></span>|
|<span data-ttu-id="d0437-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="d0437-233">VPNClient</span></span>| <span data-ttu-id="d0437-234">No compatible</span><span class="sxs-lookup"><span data-stu-id="d0437-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="d0437-235">Archivos de registro</span><span class="sxs-lookup"><span data-stu-id="d0437-235">Log files</span></span>

<span data-ttu-id="d0437-236">los archivos de registro para solucionar problemas de recursos de Hola se almacenan en una cuenta de almacenamiento una vez finalizada la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="d0437-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="d0437-237">Hello siguiente imagen muestra contenido de ejemplo de Hola de una llamada que generó un error.</span><span class="sxs-lookup"><span data-stu-id="d0437-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![Archivo ZIP][1]

> [!NOTE]
> <span data-ttu-id="d0437-239">En algunos casos, solo un subconjunto de archivos de registro de hello se escribe toostorage.</span><span class="sxs-lookup"><span data-stu-id="d0437-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="d0437-240">Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d0437-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d0437-241">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="d0437-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="d0437-242">Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="d0437-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="d0437-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="d0437-243">ConnectionStats.txt</span></span>

<span data-ttu-id="d0437-244">Hola **ConnectionStats.txt** archivo contiene estadísticas generales de hello conexión, incluidos los bytes de entrada y salida, el estado de conexión y Hola Hola de tiempo se estableció la conexión.</span><span class="sxs-lookup"><span data-stu-id="d0437-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="d0437-245">Si Hola llamada toohello solución de problemas de API devuelve correcto, lo único que Hola devolvió en el archivo zip de hello es un **ConnectionStats.txt** archivo.</span><span class="sxs-lookup"><span data-stu-id="d0437-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="d0437-246">contenido de Hola de este archivo es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0437-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="d0437-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="d0437-247">CPUStats.txt</span></span>

<span data-ttu-id="d0437-248">Hola **CPUStats.txt** archivo que contiene el uso de CPU y memoria disponible en el tiempo de presentación de las pruebas.</span><span class="sxs-lookup"><span data-stu-id="d0437-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="d0437-249">contenido de Hola de este archivo es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0437-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="d0437-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="d0437-250">IKEErrors.txt</span></span>

<span data-ttu-id="d0437-251">Hola **IKEErrors.txt** archivo contiene los errores de IKE que se encontraron durante la supervisión.</span><span class="sxs-lookup"><span data-stu-id="d0437-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="d0437-252">Hello en el ejemplo siguiente se muestra hello contenido de un archivo IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="d0437-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="d0437-253">Los errores pueden variar según el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="d0437-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="d0437-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="d0437-255">Hola **Scrubbed wfpdiag.txt** archivo de registro contiene el registro de wfp Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="d0437-256">Este registro contiene el registro de errores de IKE y AuthIP, y de pérdida de paquetes.</span><span class="sxs-lookup"><span data-stu-id="d0437-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="d0437-257">Hello en el ejemplo siguiente se muestra contenido de hello del archivo de Scrubbed wfpdiag.txt de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="d0437-258">En este ejemplo, una clave compartida Hola de una conexión no era correcta como se puede ver desde la línea 3 de Hola desde la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="d0437-259">Hola siguiente ejemplo es un fragmento de código de registro completo de hello, como registro de hello puede tardar mucho tiempo según el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0437-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="d0437-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="d0437-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="d0437-261">Hola **wfpdiag.txt.sum** archivo es un registro que muestra los búferes de Hola y eventos procesados.</span><span class="sxs-lookup"><span data-stu-id="d0437-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="d0437-262">Hello en el ejemplo siguiente se es Hola contenido de un archivo wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="d0437-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="d0437-263">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0437-263">Next steps</span></span>

<span data-ttu-id="d0437-264">Obtenga información acerca de cómo toodiagnose puertas de enlace de VPN y conexiones a través de Hola portal visitando [solución de problemas de puerta de enlace: portal de Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0437-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
