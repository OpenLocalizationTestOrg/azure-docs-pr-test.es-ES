---
title: salto de toonext aaaIntroduction en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de Monitor de red de Hola capacidad de salto siguiente"
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="986ca-103">Salto de toonext de introducción en el Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="986ca-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="986ca-104">El tráfico de una máquina virtual se envía un destino tooa basándose en rutas efectivas Hola asociadas con una NIC.</span><span class="sxs-lookup"><span data-stu-id="986ca-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="986ca-105">Próximo salto obtiene tipo hello de próximo salto y la dirección IP de un paquete desde una máquina virtual específica y la NIC.</span><span class="sxs-lookup"><span data-stu-id="986ca-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="986ca-106">Esto ayuda a toodetermine si hello paquete se está dirigido toohello destino o se holed de tráfico de Hola que se va a negro.</span><span class="sxs-lookup"><span data-stu-id="986ca-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="986ca-107">Una configuración incorrecta de las rutas por usuario de hello, donde un tráfico es dirigido tooan local ubicación o un dispositivo virtual, puede dar lugar a problemas de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="986ca-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="986ca-108">Próximo salto también devuelve la tabla de rutas de hello asociada de próximo salto Hola.</span><span class="sxs-lookup"><span data-stu-id="986ca-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="986ca-109">Al consultar un próximo salto si Hola ruta se define como una ruta definida por el usuario, se devolverá esa ruta.</span><span class="sxs-lookup"><span data-stu-id="986ca-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="986ca-110">De lo contrario, la funcionalidad devolverá "Ruta de sistema".</span><span class="sxs-lookup"><span data-stu-id="986ca-110">Otherwise Next hop returns "System Route".</span></span>

![información general sobre próximo salto][1]

<span data-ttu-id="986ca-112">Hola aquí te mostramos una lista de hello tipos de próximo salto que se pueden devolver al consultar el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="986ca-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="986ca-113">Internet</span><span class="sxs-lookup"><span data-stu-id="986ca-113">Internet</span></span>
* <span data-ttu-id="986ca-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="986ca-114">VirtualAppliance</span></span>
* <span data-ttu-id="986ca-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="986ca-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="986ca-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="986ca-116">VnetLocal</span></span>
* <span data-ttu-id="986ca-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="986ca-117">HyperNetGateway</span></span>
* <span data-ttu-id="986ca-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="986ca-118">VnetPeering</span></span>
* <span data-ttu-id="986ca-119">None</span><span class="sxs-lookup"><span data-stu-id="986ca-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="986ca-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="986ca-120">Next steps</span></span>

<span data-ttu-id="986ca-121">Obtenga información acerca de cómo toouse siguiente salto toofind problemas con conectividad de red visitando [comprobación Hola de próximo salto en una máquina virtual](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="986ca-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













