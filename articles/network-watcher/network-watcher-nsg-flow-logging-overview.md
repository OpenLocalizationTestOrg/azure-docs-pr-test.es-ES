---
title: "Introducción a los registros de flujo de grupos de seguridad de red con Azure Network Watcher | Microsoft Docs"
description: "Esta página explica cómo usar los registros de flujo de los grupos de seguridad de red, una característica de Azure Network Watcher."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="5ff0f-103">Introducción a los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="5ff0f-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="5ff0f-104">Los registros de flujo de grupos de seguridad de red son una característica de Network Watcher que permite ver información acerca del tráfico IP de entrada y de salida en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="5ff0f-105">Estos registros de flujo se escriben en formato JSON y muestran los flujos de entrada y salida en función de cada regla, la NIC a la que se aplica el flujo, información de 5-tupla sobre el flujo (IP de origen/destino, puerto de origen/destino, protocolo), y si se permitió o denegó el tráfico.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![información general de los registros de flujo][1]

<span data-ttu-id="5ff0f-107">Aunque los registros de flujo tienen como objetivo los grupos de seguridad de red, no se muestran como los demás registros.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="5ff0f-108">Los registros de flujo se almacenan solo dentro de una cuenta de almacenamiento y siguen la ruta de acceso del registro que se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ff0f-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="5ff0f-109">Las mismas directivas de retención vistas en otros registros se aplican a los registros de flujo.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="5ff0f-110">Los registros tienen una directiva de retención que se puede establecer entre 1 y 365 días.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="5ff0f-111">Si no se establece una directiva de retención, los registros se mantendrán indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="5ff0f-112">Archivo de registro</span><span class="sxs-lookup"><span data-stu-id="5ff0f-112">Log file</span></span>

<span data-ttu-id="5ff0f-113">Los registros de flujo tienen varias propiedades.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="5ff0f-114">En la lista siguiente puede ver una lista de las propiedades que se devuelven en el registro de flujo de un grupo de seguridad de red:</span><span class="sxs-lookup"><span data-stu-id="5ff0f-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="5ff0f-115">**time**: la hora en la que se registró el evento</span><span class="sxs-lookup"><span data-stu-id="5ff0f-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="5ff0f-116">**systemId**: el identificador de recurso del grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="5ff0f-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="5ff0f-117">**category**: la categoría del evento, esta siempre es NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="5ff0f-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="5ff0f-118">**resourceid**: el identificador del recurso del grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="5ff0f-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="5ff0f-119">**operationName**: siempre es NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="5ff0f-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="5ff0f-120">**properties**: una recopilación de las propiedades del flujo</span><span class="sxs-lookup"><span data-stu-id="5ff0f-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="5ff0f-121">**Version**: número de versión del esquema de eventos del registro de flujos</span><span class="sxs-lookup"><span data-stu-id="5ff0f-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="5ff0f-122">**flows**: una recopilación de flujos.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="5ff0f-123">Esta propiedad tiene varias entradas para diferentes reglas</span><span class="sxs-lookup"><span data-stu-id="5ff0f-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="5ff0f-124">**rule**: regla para la que se muestran los flujos</span><span class="sxs-lookup"><span data-stu-id="5ff0f-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="5ff0f-125">**flows**: una recopilación de flujos</span><span class="sxs-lookup"><span data-stu-id="5ff0f-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="5ff0f-126">**mac**: la dirección MAC de la NIC de la máquina virtual en la que se recopiló el flujo</span><span class="sxs-lookup"><span data-stu-id="5ff0f-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="5ff0f-127">**flowTuples**: una cadena que contiene varias propiedades de la tupla de flujo en un formato separado por comas</span><span class="sxs-lookup"><span data-stu-id="5ff0f-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="5ff0f-128">**Time Stamp**: este valor es la marca de tiempo de cuando se produjo el flujo en formato UNIX EPOCH</span><span class="sxs-lookup"><span data-stu-id="5ff0f-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="5ff0f-129">**Source IP**: la IP de origen</span><span class="sxs-lookup"><span data-stu-id="5ff0f-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="5ff0f-130">**Destination IP**: la IP de destino</span><span class="sxs-lookup"><span data-stu-id="5ff0f-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="5ff0f-131">**Source Port**: el puerto de origen</span><span class="sxs-lookup"><span data-stu-id="5ff0f-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="5ff0f-132">**Destination Port**: el puerto de destino</span><span class="sxs-lookup"><span data-stu-id="5ff0f-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="5ff0f-133">**Protocol**: el protocolo del flujo.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="5ff0f-134">Los valores válidos son **T** para TCP y **U** para UDP</span><span class="sxs-lookup"><span data-stu-id="5ff0f-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="5ff0f-135">**Traffic Flow**: la dirección del flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="5ff0f-136">Los valores válidos son **I** para el correo entrante y **O** para el saliente.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="5ff0f-137">**Traffic**: indica si el tráfico se permitió o se denegó.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="5ff0f-138">Los valores válidos son **A** para permitido y **D** para denegado.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="5ff0f-139">A continuación, se muestra un ejemplo de un registro de flujo.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="5ff0f-140">Como puede ver, hay varios registros que siguen la lista de propiedades que se describe en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="5ff0f-141">Los valores de la propiedad flowTuples son una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="5ff0f-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="5ff0f-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5ff0f-142">Next steps</span></span>

<span data-ttu-id="5ff0f-143">Aprenda a habilitar los registros de flujo visitando [Habilitamiento del registro de flujos](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5ff0f-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="5ff0f-144">Obtenga información acerca del registro de NSG visitando [Análisis del registro para grupos de seguridad de red (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="5ff0f-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="5ff0f-145">Averigüe si se permite o no el tráfico en una máquina virtual visitando [Comprobación del tráfico con la comprobación de flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5ff0f-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

