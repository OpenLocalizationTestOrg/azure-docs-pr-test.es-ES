---
title: registro de tooflow aaaIntroduction para grupos de seguridad de red con Monitor de red de Azure | Documentos de Microsoft
description: "Esta página explica cómo el flujo NSG toouse registra una característica del Monitor de red de Azure"
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
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="c0b04-103">Registro de tooflow de introducción para grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="c0b04-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="c0b04-104">Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c0b04-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="c0b04-105">Estos registros de flujo se escriben en formato json y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.</span><span class="sxs-lookup"><span data-stu-id="c0b04-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![información general de los registros de flujo][1]

<span data-ttu-id="c0b04-107">Mientras el flujo de registros de grupos de seguridad de red de destino, no se muestran mismo Hola como Hola otros registros.</span><span class="sxs-lookup"><span data-stu-id="c0b04-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="c0b04-108">Registros de flujo se almacenan dentro de una cuenta de almacenamiento y la siguiente ruta de acceso de registro de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c0b04-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="c0b04-109">Hola mismo tooflow registros aplican las directivas de retención, tal como se muestra en otros registros.</span><span class="sxs-lookup"><span data-stu-id="c0b04-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="c0b04-110">Los registros tienen una directiva de retención que se pueden establecer en 1 día too365 días.</span><span class="sxs-lookup"><span data-stu-id="c0b04-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="c0b04-111">Si no se establece una directiva de retención, Hola registros se mantienen indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="c0b04-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="c0b04-112">Archivo de registro</span><span class="sxs-lookup"><span data-stu-id="c0b04-112">Log file</span></span>

<span data-ttu-id="c0b04-113">Los registros de flujo tienen varias propiedades.</span><span class="sxs-lookup"><span data-stu-id="c0b04-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="c0b04-114">Hello lista siguiente es una lista de propiedades de Hola que se devuelven en el registro de flujo de hello NSG:</span><span class="sxs-lookup"><span data-stu-id="c0b04-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="c0b04-115">**tiempo** : tiempo cuando se registra el evento de Hola</span><span class="sxs-lookup"><span data-stu-id="c0b04-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="c0b04-116">**systemId**: el identificador de recurso del grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="c0b04-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="c0b04-117">**categoría** -categoría Hola de evento de hello, esto siempre es ser NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="c0b04-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="c0b04-118">**ResourceID** -Hola recursos Id. de hello NSG</span><span class="sxs-lookup"><span data-stu-id="c0b04-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="c0b04-119">**operationName**: siempre es NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="c0b04-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="c0b04-120">**propiedades** -una colección de propiedades de flujo de Hola</span><span class="sxs-lookup"><span data-stu-id="c0b04-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="c0b04-121">**Versión** -número de versión de esquema de eventos de flujo de registro de hello</span><span class="sxs-lookup"><span data-stu-id="c0b04-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="c0b04-122">**flows**: una recopilación de flujos.</span><span class="sxs-lookup"><span data-stu-id="c0b04-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="c0b04-123">Esta propiedad tiene varias entradas para diferentes reglas</span><span class="sxs-lookup"><span data-stu-id="c0b04-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="c0b04-124">**regla** -regla qué Hola se muestran cuatro flujos</span><span class="sxs-lookup"><span data-stu-id="c0b04-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="c0b04-125">**flows**: una recopilación de flujos</span><span class="sxs-lookup"><span data-stu-id="c0b04-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="c0b04-126">**Mac** -Hola dirección MAC de hello NIC para hello VM que se recopiló el flujo de Hola</span><span class="sxs-lookup"><span data-stu-id="c0b04-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="c0b04-127">**flowTuples** -una cadena que contiene varias propiedades de tupla de flujo de hello en un formato separado por comas</span><span class="sxs-lookup"><span data-stu-id="c0b04-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="c0b04-128">**Marca de tiempo** -este valor es la marca de tiempo hello cuando se produjo el flujo de hello en formato de la ÉPOCA de UNIX</span><span class="sxs-lookup"><span data-stu-id="c0b04-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="c0b04-129">**IP de origen** : hello IP de origen</span><span class="sxs-lookup"><span data-stu-id="c0b04-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="c0b04-130">**Destino IP** -Hola IP de destino</span><span class="sxs-lookup"><span data-stu-id="c0b04-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="c0b04-131">**Puerto de origen** : hello puerto de origen</span><span class="sxs-lookup"><span data-stu-id="c0b04-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="c0b04-132">**Puerto de destino** -Hola puerto de destino</span><span class="sxs-lookup"><span data-stu-id="c0b04-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="c0b04-133">**Protocolo** -Hola protocolo de flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0b04-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="c0b04-134">Los valores válidos son **T** para TCP y **U** para UDP</span><span class="sxs-lookup"><span data-stu-id="c0b04-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="c0b04-135">**Flujo del tráfico** -Hola dirección del flujo de tráfico de Hola de.</span><span class="sxs-lookup"><span data-stu-id="c0b04-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="c0b04-136">Los valores válidos son **I** para el correo entrante y **O** para el saliente.</span><span class="sxs-lookup"><span data-stu-id="c0b04-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="c0b04-137">**Traffic**: indica si el tráfico se permitió o se denegó.</span><span class="sxs-lookup"><span data-stu-id="c0b04-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="c0b04-138">Los valores válidos son **A** para permitido y **D** para denegado.</span><span class="sxs-lookup"><span data-stu-id="c0b04-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="c0b04-139">Hola aquí te mostramos un ejemplo de un registro de flujo.</span><span class="sxs-lookup"><span data-stu-id="c0b04-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="c0b04-140">Como puede ver, hay varios registros que siguen la lista de propiedades de Hola se describe en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0b04-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0b04-141">Valores de propiedad de hello flowTuples son una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="c0b04-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="c0b04-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0b04-142">Next steps</span></span>

<span data-ttu-id="c0b04-143">Obtenga información acerca de cómo se registra tooenable flujo visitando [habilitar el flujo de registro](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c0b04-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="c0b04-144">Obtenga información acerca del registro de NSG visitando [Análisis del registro para grupos de seguridad de red (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="c0b04-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="c0b04-145">Averigüe si se permite o no el tráfico en una máquina virtual visitando [Comprobación del tráfico con la comprobación de flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c0b04-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

