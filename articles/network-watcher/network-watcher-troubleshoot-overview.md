---
title: "Introducción a la solución de problemas de recursos en Azure Network Watcher | Microsoft Docs"
description: "En esta página se proporciona una introducción a las funcionalidades de solución de problemas de recursos en Network Watcher."
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
ms.openlocfilehash: 0d5091b682d1b25c47b224394bcc2c46366eeb2a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="a1eff-103">Introducción a la solución de problemas de recursos en Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a1eff-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="a1eff-104">Las puertas de enlace de red virtual proporcionan conectividad entre recursos locales y otras redes virtuales dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1eff-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="a1eff-105">La supervisión de estas puertas de enlace y sus conexiones es esencial para garantizar la continuidad de la comunicación.</span><span class="sxs-lookup"><span data-stu-id="a1eff-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="a1eff-106">Network Watcher proporciona la funcionalidad para solucionar problemas con las puertas de enlace de red virtual y las conexiones.</span><span class="sxs-lookup"><span data-stu-id="a1eff-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="a1eff-107">Se puede llamar mediante el portal, PowerShell, la CLI o la API de REST.</span><span class="sxs-lookup"><span data-stu-id="a1eff-107">This can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="a1eff-108">Cuando se llama, Network Watcher diagnostica el estado de la puerta de enlace de red virtual o la conexión y devuelve los resultados pertinentes.</span><span class="sxs-lookup"><span data-stu-id="a1eff-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="a1eff-109">Esta solicitud es una transacción de larga duración; los resultados se devuelven cuando se completa el diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="a1eff-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="a1eff-111">Results</span><span class="sxs-lookup"><span data-stu-id="a1eff-111">Results</span></span>

<span data-ttu-id="a1eff-112">Los resultados preliminares devueltos proporcionan una perspectiva general del estado del recurso.</span><span class="sxs-lookup"><span data-stu-id="a1eff-112">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="a1eff-113">Se puede proporcionar información más detallada para recursos, tal como se muestra en la sección siguiente:</span><span class="sxs-lookup"><span data-stu-id="a1eff-113">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="a1eff-114">En la siguiente lista, se presentan los valores devueltos con la API de solución de problemas:</span><span class="sxs-lookup"><span data-stu-id="a1eff-114">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="a1eff-115">**startTime**: este valor es la hora de inicio de la llamada a la API de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a1eff-115">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="a1eff-116">**endTime**: este valor es la hora en que finalizó la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a1eff-116">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="a1eff-117">**code**: este valor es UnHealthy si se produce un único error de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="a1eff-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="a1eff-118">**results**: es una colección de resultados devueltos para la conexión o la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="a1eff-118">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="a1eff-119">**id**: este valor es el tipo de error.</span><span class="sxs-lookup"><span data-stu-id="a1eff-119">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="a1eff-120">**summary**: este valor es un resumen del error.</span><span class="sxs-lookup"><span data-stu-id="a1eff-120">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="a1eff-121">**detailed**: este valor proporciona una descripción detallada del error.</span><span class="sxs-lookup"><span data-stu-id="a1eff-121">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="a1eff-122">**recommendedActions**: esta propiedad es una colección de acciones recomendadas que llevar a cabo.</span><span class="sxs-lookup"><span data-stu-id="a1eff-122">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="a1eff-123">**actionText**: este valor contiene el texto que describe qué acción realizar.</span><span class="sxs-lookup"><span data-stu-id="a1eff-123">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="a1eff-124">**actionUri**: este valor proporciona el URI de documentación sobre cómo actuar.</span><span class="sxs-lookup"><span data-stu-id="a1eff-124">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="a1eff-125">**actionUriText**: este valor es una breve descripción del texto de acción.</span><span class="sxs-lookup"><span data-stu-id="a1eff-125">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="a1eff-126">En las siguientes tablas se muestran los diferentes tipos de error (id bajo results en la lista anterior) que existen y si el error crea registros.</span><span class="sxs-lookup"><span data-stu-id="a1eff-126">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="a1eff-127">Puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a1eff-127">Gateway</span></span>

| <span data-ttu-id="a1eff-128">Tipo de error</span><span class="sxs-lookup"><span data-stu-id="a1eff-128">Fault Type</span></span> | <span data-ttu-id="a1eff-129">Motivo</span><span class="sxs-lookup"><span data-stu-id="a1eff-129">Reason</span></span> | <span data-ttu-id="a1eff-130">Registro</span><span class="sxs-lookup"><span data-stu-id="a1eff-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="a1eff-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="a1eff-131">NoFault</span></span> | <span data-ttu-id="a1eff-132">Cuando no se detecta ningún error.</span><span class="sxs-lookup"><span data-stu-id="a1eff-132">When no error is detected.</span></span> |<span data-ttu-id="a1eff-133">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-133">Yes</span></span>|
| <span data-ttu-id="a1eff-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="a1eff-134">GatewayNotFound</span></span> | <span data-ttu-id="a1eff-135">No se encuentra la puerta de enlace o no está aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="a1eff-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="a1eff-136">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-136">No</span></span>|
| <span data-ttu-id="a1eff-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="a1eff-137">PlannedMaintenance</span></span> |  <span data-ttu-id="a1eff-138">La instancia de puerta de enlace está en mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="a1eff-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="a1eff-139">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-139">No</span></span>|
| <span data-ttu-id="a1eff-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="a1eff-140">UserDrivenUpdate</span></span> | <span data-ttu-id="a1eff-141">Cuando hay una actualización del usuario en curso.</span><span class="sxs-lookup"><span data-stu-id="a1eff-141">When a user update is in progress.</span></span> <span data-ttu-id="a1eff-142">Podría tratarse de una operación de cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="a1eff-142">This could be a resize operation.</span></span> | <span data-ttu-id="a1eff-143">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-143">No</span></span> |
| <span data-ttu-id="a1eff-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="a1eff-144">VipUnResponsive</span></span> | <span data-ttu-id="a1eff-145">No se puede alcanzar la instancia principal de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a1eff-145">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="a1eff-146">Esto sucede cuando se produce un error en el sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="a1eff-146">This happens when the health probe fails.</span></span> | <span data-ttu-id="a1eff-147">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-147">No</span></span> |
| <span data-ttu-id="a1eff-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="a1eff-148">PlatformInActive</span></span> | <span data-ttu-id="a1eff-149">Hay un problema con la plataforma.</span><span class="sxs-lookup"><span data-stu-id="a1eff-149">There is an issue with the platform.</span></span> | <span data-ttu-id="a1eff-150">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-150">No</span></span>|
| <span data-ttu-id="a1eff-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="a1eff-151">ServiceNotRunning</span></span> | <span data-ttu-id="a1eff-152">No se está ejecutando el servicio subyacente.</span><span class="sxs-lookup"><span data-stu-id="a1eff-152">The underlying service is not running.</span></span> | <span data-ttu-id="a1eff-153">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-153">No</span></span>|
| <span data-ttu-id="a1eff-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="a1eff-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="a1eff-155">No existe ninguna conexión en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a1eff-155">No Connections exists on the gateway.</span></span> <span data-ttu-id="a1eff-156">Esto es solo una advertencia.</span><span class="sxs-lookup"><span data-stu-id="a1eff-156">This is only a warning.</span></span>| <span data-ttu-id="a1eff-157">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-157">No</span></span>|
| <span data-ttu-id="a1eff-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="a1eff-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="a1eff-159">Las conexiones no están conectadas.</span><span class="sxs-lookup"><span data-stu-id="a1eff-159">Connections are not connected.</span></span> <span data-ttu-id="a1eff-160">Esto es solo una advertencia.</span><span class="sxs-lookup"><span data-stu-id="a1eff-160">This is only a warning.</span></span>| <span data-ttu-id="a1eff-161">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-161">Yes</span></span>|
| <span data-ttu-id="a1eff-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="a1eff-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="a1eff-163">El uso de CPU de la puerta de enlace actual es >95 %.</span><span class="sxs-lookup"><span data-stu-id="a1eff-163">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="a1eff-164">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="a1eff-165">Conexión</span><span class="sxs-lookup"><span data-stu-id="a1eff-165">Connection</span></span>

| <span data-ttu-id="a1eff-166">Tipo de error</span><span class="sxs-lookup"><span data-stu-id="a1eff-166">Fault Type</span></span> | <span data-ttu-id="a1eff-167">Motivo</span><span class="sxs-lookup"><span data-stu-id="a1eff-167">Reason</span></span> | <span data-ttu-id="a1eff-168">Registro</span><span class="sxs-lookup"><span data-stu-id="a1eff-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="a1eff-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="a1eff-169">NoFault</span></span> | <span data-ttu-id="a1eff-170">Cuando no se detecta ningún error.</span><span class="sxs-lookup"><span data-stu-id="a1eff-170">When no error is detected.</span></span> |<span data-ttu-id="a1eff-171">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-171">Yes</span></span>|
| <span data-ttu-id="a1eff-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="a1eff-172">GatewayNotFound</span></span> | <span data-ttu-id="a1eff-173">No se encuentra la puerta de enlace o no está aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="a1eff-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="a1eff-174">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-174">No</span></span>|
| <span data-ttu-id="a1eff-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="a1eff-175">PlannedMaintenance</span></span> | <span data-ttu-id="a1eff-176">La instancia de puerta de enlace está en mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="a1eff-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="a1eff-177">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-177">No</span></span>|
| <span data-ttu-id="a1eff-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="a1eff-178">UserDrivenUpdate</span></span> | <span data-ttu-id="a1eff-179">Cuando hay una actualización del usuario en curso.</span><span class="sxs-lookup"><span data-stu-id="a1eff-179">When a user update is in progress.</span></span> <span data-ttu-id="a1eff-180">Podría tratarse de una operación de cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="a1eff-180">This could be a resize operation.</span></span>  | <span data-ttu-id="a1eff-181">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-181">No</span></span> |
| <span data-ttu-id="a1eff-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="a1eff-182">VipUnResponsive</span></span> | <span data-ttu-id="a1eff-183">No se puede alcanzar la instancia principal de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a1eff-183">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="a1eff-184">Sucede cuando se produce un error en el sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="a1eff-184">It happens when the health probe fails.</span></span> | <span data-ttu-id="a1eff-185">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-185">No</span></span> |
| <span data-ttu-id="a1eff-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="a1eff-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="a1eff-187">Falta una configuración de conexión.</span><span class="sxs-lookup"><span data-stu-id="a1eff-187">Connection configuration is missing.</span></span> | <span data-ttu-id="a1eff-188">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-188">No</span></span> |
| <span data-ttu-id="a1eff-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="a1eff-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="a1eff-190">La conexión está marcada como "desconectada".</span><span class="sxs-lookup"><span data-stu-id="a1eff-190">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="a1eff-191">No</span><span class="sxs-lookup"><span data-stu-id="a1eff-191">No</span></span>|
| <span data-ttu-id="a1eff-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="a1eff-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="a1eff-193">El servicio subyacente no tiene configurada la conexión.</span><span class="sxs-lookup"><span data-stu-id="a1eff-193">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="a1eff-194">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-194">Yes</span></span> |
| <span data-ttu-id="a1eff-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="a1eff-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="a1eff-196">El servicio subyacente está marcado como en espera activa.</span><span class="sxs-lookup"><span data-stu-id="a1eff-196">The underlying service is marked as standby.</span></span>| <span data-ttu-id="a1eff-197">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-197">Yes</span></span>|
| <span data-ttu-id="a1eff-198">Autenticación</span><span class="sxs-lookup"><span data-stu-id="a1eff-198">Authentication</span></span> | <span data-ttu-id="a1eff-199">Error de coincidencia de clave previamente compartida.</span><span class="sxs-lookup"><span data-stu-id="a1eff-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="a1eff-200">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-200">Yes</span></span>|
| <span data-ttu-id="a1eff-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="a1eff-201">PeerReachability</span></span> | <span data-ttu-id="a1eff-202">La puerta de enlace del mismo nivel no está accesible.</span><span class="sxs-lookup"><span data-stu-id="a1eff-202">The peer gateway is not reachable.</span></span> | <span data-ttu-id="a1eff-203">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-203">Yes</span></span>|
| <span data-ttu-id="a1eff-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="a1eff-204">IkePolicyMismatch</span></span> | <span data-ttu-id="a1eff-205">La puerta de enlace del mismo nivel tiene directivas IKE que no son compatibles con Azure.</span><span class="sxs-lookup"><span data-stu-id="a1eff-205">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="a1eff-206">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-206">Yes</span></span>|
| <span data-ttu-id="a1eff-207">Error de WfpParse</span><span class="sxs-lookup"><span data-stu-id="a1eff-207">WfpParse Error</span></span> | <span data-ttu-id="a1eff-208">Se produjo un error al analizar el registro de WFP.</span><span class="sxs-lookup"><span data-stu-id="a1eff-208">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="a1eff-209">Sí</span><span class="sxs-lookup"><span data-stu-id="a1eff-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="a1eff-210">Tipos de puerta de enlace admitidos</span><span class="sxs-lookup"><span data-stu-id="a1eff-210">Supported Gateway types</span></span>

<span data-ttu-id="a1eff-211">En la lista siguiente se muestra qué puertas de enlace y conexiones son compatibles con la solución de problemas de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a1eff-211">The following list shows the support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="a1eff-212">**Tipos de puerta de enlace**</span><span class="sxs-lookup"><span data-stu-id="a1eff-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="a1eff-213">VPN</span><span class="sxs-lookup"><span data-stu-id="a1eff-213">VPN</span></span>      | <span data-ttu-id="a1eff-214">Compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-214">Supported</span></span>        |
|<span data-ttu-id="a1eff-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a1eff-215">ExpressRoute</span></span> | <span data-ttu-id="a1eff-216">No compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-216">Not Supported</span></span> |
|<span data-ttu-id="a1eff-217">HyperNet</span><span class="sxs-lookup"><span data-stu-id="a1eff-217">Hypernet</span></span> | <span data-ttu-id="a1eff-218">No compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-218">Not Supported</span></span>|
|<span data-ttu-id="a1eff-219">**Tipos de VPN**</span><span class="sxs-lookup"><span data-stu-id="a1eff-219">**VPN types**</span></span> | |
|<span data-ttu-id="a1eff-220">Basado en ruta</span><span class="sxs-lookup"><span data-stu-id="a1eff-220">Route Based</span></span> | <span data-ttu-id="a1eff-221">Compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-221">Supported</span></span>|
|<span data-ttu-id="a1eff-222">Basado en directiva</span><span class="sxs-lookup"><span data-stu-id="a1eff-222">Policy Based</span></span> | <span data-ttu-id="a1eff-223">No compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-223">Not Supported</span></span>|
|<span data-ttu-id="a1eff-224">**Tipos de conexión**</span><span class="sxs-lookup"><span data-stu-id="a1eff-224">**Connection types**</span></span>||
|<span data-ttu-id="a1eff-225">IPSec</span><span class="sxs-lookup"><span data-stu-id="a1eff-225">IPSec</span></span>| <span data-ttu-id="a1eff-226">Compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-226">Supported</span></span>|
|<span data-ttu-id="a1eff-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="a1eff-227">VNet2Vnet</span></span>| <span data-ttu-id="a1eff-228">Compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-228">Supported</span></span>|
|<span data-ttu-id="a1eff-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a1eff-229">ExpressRoute</span></span>| <span data-ttu-id="a1eff-230">No compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-230">Not Supported</span></span>|
|<span data-ttu-id="a1eff-231">HyperNet</span><span class="sxs-lookup"><span data-stu-id="a1eff-231">Hypernet</span></span>| <span data-ttu-id="a1eff-232">No compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-232">Not Supported</span></span>|
|<span data-ttu-id="a1eff-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="a1eff-233">VPNClient</span></span>| <span data-ttu-id="a1eff-234">No compatible</span><span class="sxs-lookup"><span data-stu-id="a1eff-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="a1eff-235">Archivos de registro</span><span class="sxs-lookup"><span data-stu-id="a1eff-235">Log files</span></span>

<span data-ttu-id="a1eff-236">Los archivos de registro de la solución de problemas de recursos se guardan en una cuenta de almacenamiento una vez finalizada dicha solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a1eff-236">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="a1eff-237">En la siguiente imagen se muestra el contenido de ejemplo de una llamada que generó un error.</span><span class="sxs-lookup"><span data-stu-id="a1eff-237">The following image shows the example contents of a call that resulted in an error.</span></span>

![Archivo ZIP][1]

> [!NOTE]
> <span data-ttu-id="a1eff-239">En algunos casos, solo se escribe un subconjunto de los archivos de registro en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a1eff-239">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="a1eff-240">Para instrucciones sobre cómo descargar archivos desde cuentas de Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a1eff-240">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a1eff-241">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="a1eff-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a1eff-242">Encontrará más información acerca del Explorador de Storage en el siguiente vínculo: [Explorador de Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="a1eff-242">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="a1eff-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="a1eff-243">ConnectionStats.txt</span></span>

<span data-ttu-id="a1eff-244">El archivo **ConnectionStats.txt** contiene estadísticas generales de la conexión, incluidos los bytes de entrada y salida, el estado de la conexión y la hora en que se estableció esta.</span><span class="sxs-lookup"><span data-stu-id="a1eff-244">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="a1eff-245">Si la llamada a la API de solución de problemas devuelve un estado correcto, lo único que se devuelve en el archivo ZIP es un archivo **ConnectionStats.txt**.</span><span class="sxs-lookup"><span data-stu-id="a1eff-245">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="a1eff-246">El contenido de este archivo es similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a1eff-246">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="a1eff-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="a1eff-247">CPUStats.txt</span></span>

<span data-ttu-id="a1eff-248">El archivo **CPUStats.txt** contiene el uso de la CPU y la memoria disponible en el momento de realizarse las pruebas.</span><span class="sxs-lookup"><span data-stu-id="a1eff-248">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="a1eff-249">El contenido de este archivo es similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a1eff-249">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="a1eff-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="a1eff-250">IKEErrors.txt</span></span>

<span data-ttu-id="a1eff-251">El archivo **IKEErrors.txt** contiene los errores de IKE que se encontraran durante la supervisión.</span><span class="sxs-lookup"><span data-stu-id="a1eff-251">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="a1eff-252">En el ejemplo siguiente se muestra el contenido de un archivo IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="a1eff-252">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="a1eff-253">Los errores pueden variar según el problema.</span><span class="sxs-lookup"><span data-stu-id="a1eff-253">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="a1eff-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="a1eff-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="a1eff-255">El archivo de registro **Scrubbed-wfpdiag.txt** contiene el registro de WFP.</span><span class="sxs-lookup"><span data-stu-id="a1eff-255">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="a1eff-256">Este registro contiene el registro de errores de IKE y AuthIP, y de pérdida de paquetes.</span><span class="sxs-lookup"><span data-stu-id="a1eff-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="a1eff-257">En el ejemplo siguiente se muestra el contenido del archivo Scrubbed-wfpdiag.txt.</span><span class="sxs-lookup"><span data-stu-id="a1eff-257">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="a1eff-258">En este ejemplo, la clave compartida de una conexión no era correcta, como se aprecia a partir de la tercera línea desde abajo.</span><span class="sxs-lookup"><span data-stu-id="a1eff-258">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="a1eff-259">El ejemplo siguiente es un fragmento del código del registro completo, el cual puede ser extenso en función del problema.</span><span class="sxs-lookup"><span data-stu-id="a1eff-259">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="a1eff-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="a1eff-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="a1eff-261">El archivo **wfpdiag.txt.sum** es un registro que muestra los búferes y los eventos procesados.</span><span class="sxs-lookup"><span data-stu-id="a1eff-261">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="a1eff-262">El ejemplo siguiente es el contenido de un archivo wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="a1eff-262">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="a1eff-263">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1eff-263">Next steps</span></span>

<span data-ttu-id="a1eff-264">Visite [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md) (Solución de problemas de puerta de enlace: Azure Portal) para saber cómo diagnosticar las conexiones y las puertas de enlace de VPN a través del portal.</span><span class="sxs-lookup"><span data-stu-id="a1eff-264">Learn how to diagnose VPN Gateways and Connections through the portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
