---
title: "Configuración de puerto de Azure Relay | Microsoft Docs"
description: "Obtenga información sobre los valores de puerto de Azure Relay."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 5906495c565dad583e74a43b2e5eed57e0c68df1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-port-settings"></a><span data-ttu-id="0c780-103">Configuración de puerto de Relay de Azure</span><span class="sxs-lookup"><span data-stu-id="0c780-103">Azure Relay port settings</span></span>

<span data-ttu-id="0c780-104">En la tabla siguiente se describe la configuración que se requiere para los valores de los puerto de Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="0c780-104">The following table describes the required configuration for port values for Azure Relay.</span></span>

## <a name="hybrid-connections"></a><span data-ttu-id="0c780-105">conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="0c780-105">Hybrid Connections</span></span>
<span data-ttu-id="0c780-106">Las conexiones híbridas emplean protocolos WebSocket como mecanismo de transporte subyacente, utilizando solo **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="0c780-106">Hybrid Connections uses WebSockets as the underlying transport mechanism, which uses **HTTPS** only.</span></span> 

## <a name="wcf-relays"></a><span data-ttu-id="0c780-107">Relés de WCF</span><span class="sxs-lookup"><span data-stu-id="0c780-107">WCF Relays</span></span>
  
|<span data-ttu-id="0c780-108">Enlace</span><span class="sxs-lookup"><span data-stu-id="0c780-108">Binding</span></span>|<span data-ttu-id="0c780-109">Seguridad de transporte</span><span class="sxs-lookup"><span data-stu-id="0c780-109">Transport Security</span></span>|<span data-ttu-id="0c780-110">Port</span><span class="sxs-lookup"><span data-stu-id="0c780-110">Port</span></span>|  
|-------------|------------------------|----------|  
|<span data-ttu-id="0c780-111">[Clase BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (cliente)</span><span class="sxs-lookup"><span data-stu-id="0c780-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span></span>|<span data-ttu-id="0c780-112">Sí</span><span class="sxs-lookup"><span data-stu-id="0c780-112">Yes</span></span>|<span data-ttu-id="0c780-113">HTTPS</span><span class="sxs-lookup"><span data-stu-id="0c780-113">HTTPS</span></span>| 
| |<span data-ttu-id="0c780-114">"</span><span class="sxs-lookup"><span data-stu-id="0c780-114">"</span></span> |<span data-ttu-id="0c780-115">No</span><span class="sxs-lookup"><span data-stu-id="0c780-115">No</span></span>|<span data-ttu-id="0c780-116">HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-116">HTTP</span></span>|  
|<span data-ttu-id="0c780-117">[Clase BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (servicio)</span><span class="sxs-lookup"><span data-stu-id="0c780-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span></span>|<span data-ttu-id="0c780-118">Es posible usar el</span><span class="sxs-lookup"><span data-stu-id="0c780-118">Either</span></span>|<span data-ttu-id="0c780-119">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-119">9351/HTTP</span></span>|  
|<span data-ttu-id="0c780-120">[Clase NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (cliente)</span><span class="sxs-lookup"><span data-stu-id="0c780-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span></span>|<span data-ttu-id="0c780-121">Sí</span><span class="sxs-lookup"><span data-stu-id="0c780-121">Yes</span></span>|<span data-ttu-id="0c780-122">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="0c780-122">9351/HTTPS</span></span>|  
||<span data-ttu-id="0c780-123">"</span><span class="sxs-lookup"><span data-stu-id="0c780-123">"</span></span> |<span data-ttu-id="0c780-124">No</span><span class="sxs-lookup"><span data-stu-id="0c780-124">No</span></span>|<span data-ttu-id="0c780-125">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-125">9350/HTTP</span></span>|  
|<span data-ttu-id="0c780-126">[Clase NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (servicio)</span><span class="sxs-lookup"><span data-stu-id="0c780-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span></span>|<span data-ttu-id="0c780-127">Es posible usar el</span><span class="sxs-lookup"><span data-stu-id="0c780-127">Either</span></span>|<span data-ttu-id="0c780-128">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-128">9351/HTTP</span></span>|  
|<span data-ttu-id="0c780-129">[Clase NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (cliente o servicio)</span><span class="sxs-lookup"><span data-stu-id="0c780-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span></span>|<span data-ttu-id="0c780-130">Es posible usar el</span><span class="sxs-lookup"><span data-stu-id="0c780-130">Either</span></span>|<span data-ttu-id="0c780-131">5671/9352/HTTP (9352/9353 si se usa el modo híbrido)</span><span class="sxs-lookup"><span data-stu-id="0c780-131">5671/9352/HTTP (9352/9353 if using hybrid)</span></span>|  
|<span data-ttu-id="0c780-132">[Clase NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (cliente)</span><span class="sxs-lookup"><span data-stu-id="0c780-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span></span>|<span data-ttu-id="0c780-133">Sí</span><span class="sxs-lookup"><span data-stu-id="0c780-133">Yes</span></span>|<span data-ttu-id="0c780-134">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="0c780-134">9351/HTTPS</span></span>|  
||<span data-ttu-id="0c780-135">"</span><span class="sxs-lookup"><span data-stu-id="0c780-135">"</span></span> |<span data-ttu-id="0c780-136">No</span><span class="sxs-lookup"><span data-stu-id="0c780-136">No</span></span>|<span data-ttu-id="0c780-137">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-137">9350/HTTP</span></span>|  
|<span data-ttu-id="0c780-138">[Clase NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (servicio)</span><span class="sxs-lookup"><span data-stu-id="0c780-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span></span>|<span data-ttu-id="0c780-139">Es posible usar el</span><span class="sxs-lookup"><span data-stu-id="0c780-139">Either</span></span>|<span data-ttu-id="0c780-140">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-140">9351/HTTP</span></span>|  
|<span data-ttu-id="0c780-141">[Clase WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (cliente)</span><span class="sxs-lookup"><span data-stu-id="0c780-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span></span>|<span data-ttu-id="0c780-142">Sí</span><span class="sxs-lookup"><span data-stu-id="0c780-142">Yes</span></span>|<span data-ttu-id="0c780-143">HTTPS</span><span class="sxs-lookup"><span data-stu-id="0c780-143">HTTPS</span></span>|  
||<span data-ttu-id="0c780-144">"</span><span class="sxs-lookup"><span data-stu-id="0c780-144">"</span></span> |<span data-ttu-id="0c780-145">No</span><span class="sxs-lookup"><span data-stu-id="0c780-145">No</span></span>|<span data-ttu-id="0c780-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-146">HTTP</span></span>|  
|<span data-ttu-id="0c780-147">[Clase WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (servicio)</span><span class="sxs-lookup"><span data-stu-id="0c780-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span></span>|<span data-ttu-id="0c780-148">Es posible usar el</span><span class="sxs-lookup"><span data-stu-id="0c780-148">Either</span></span>|<span data-ttu-id="0c780-149">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-149">9351/HTTP</span></span>|  
|<span data-ttu-id="0c780-150">[Clase WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (cliente)</span><span class="sxs-lookup"><span data-stu-id="0c780-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span></span>|<span data-ttu-id="0c780-151">Sí</span><span class="sxs-lookup"><span data-stu-id="0c780-151">Yes</span></span>|<span data-ttu-id="0c780-152">HTTPS</span><span class="sxs-lookup"><span data-stu-id="0c780-152">HTTPS</span></span>|  
||<span data-ttu-id="0c780-153">"</span><span class="sxs-lookup"><span data-stu-id="0c780-153">"</span></span> |<span data-ttu-id="0c780-154">No</span><span class="sxs-lookup"><span data-stu-id="0c780-154">No</span></span>|<span data-ttu-id="0c780-155">HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-155">HTTP</span></span>|  
|<span data-ttu-id="0c780-156">[Clase WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (servicio)</span><span class="sxs-lookup"><span data-stu-id="0c780-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span></span>|<span data-ttu-id="0c780-157">Es posible usar el</span><span class="sxs-lookup"><span data-stu-id="0c780-157">Either</span></span>|<span data-ttu-id="0c780-158">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="0c780-158">9351/HTTP</span></span>|

## <a name="next-steps"></a><span data-ttu-id="0c780-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c780-159">Next steps</span></span>
<span data-ttu-id="0c780-160">Para obtener más información sobre Azure Relay, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="0c780-160">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="0c780-161">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="0c780-161">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="0c780-162">Preguntas más frecuentes acerca de Relay</span><span class="sxs-lookup"><span data-stu-id="0c780-162">Relay FAQ</span></span>](relay-faq.md)