---
title: "Introducción al próximo salto en Azure Network Watcher | Microsoft Docs"
description: "En esta página se proporciona una introducción a la funcionalidad de próximo salto de Network Watcher."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="87a49-103">Introducción al próximo salto en Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="87a49-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="87a49-104">El tráfico de una máquina virtual se envía a un destino en función de las rutas efectivas asociadas con una NIC.</span><span class="sxs-lookup"><span data-stu-id="87a49-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="87a49-105">La funcionalidad Próximo salto obtiene el tipo de próximo salto y la dirección IP de un paquete de una máquina virtual y una NIC específicas.</span><span class="sxs-lookup"><span data-stu-id="87a49-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="87a49-106">Esto sirve para determinar si el paquete se dirige hacia el destino o si el tráfico se está enviando a un agujero negro.</span><span class="sxs-lookup"><span data-stu-id="87a49-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="87a49-107">Una configuración incorrecta de las rutas por parte del usuario, en la que un determinado tráfico se dirige a una ubicación local o a un dispositivo virtual, puede causar problemas de conectividad.</span><span class="sxs-lookup"><span data-stu-id="87a49-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="87a49-108">La funcionalidad Próximo salto también devuelve la tabla de ruta asociada con el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="87a49-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="87a49-109">Al consultar un próximo salto, si la ruta se define como una ruta definida por el usuario, se devolverá esa ruta.</span><span class="sxs-lookup"><span data-stu-id="87a49-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="87a49-110">De lo contrario, la funcionalidad devolverá "Ruta de sistema".</span><span class="sxs-lookup"><span data-stu-id="87a49-110">Otherwise Next hop returns "System Route".</span></span>

![información general sobre próximo salto][1]

<span data-ttu-id="87a49-112">La siguiente es una lista de los tipos de próximo salto que se pueden devolver al consultar la funcionalidad Próximo salto.</span><span class="sxs-lookup"><span data-stu-id="87a49-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="87a49-113">Internet</span><span class="sxs-lookup"><span data-stu-id="87a49-113">Internet</span></span>
* <span data-ttu-id="87a49-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="87a49-114">VirtualAppliance</span></span>
* <span data-ttu-id="87a49-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="87a49-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="87a49-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="87a49-116">VnetLocal</span></span>
* <span data-ttu-id="87a49-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="87a49-117">HyperNetGateway</span></span>
* <span data-ttu-id="87a49-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="87a49-118">VnetPeering</span></span>
* <span data-ttu-id="87a49-119">None</span><span class="sxs-lookup"><span data-stu-id="87a49-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="87a49-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87a49-120">Next steps</span></span>

<span data-ttu-id="87a49-121">Aprenda a usar el próximo salto para detectar problemas de conectividad de red visitando [Comprobación del próximo salto en una máquina virtual](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="87a49-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













