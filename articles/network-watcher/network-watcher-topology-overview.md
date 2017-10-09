---
title: aaaIntroduction tootopology en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de las capacidades de topología de Monitor de red de Hola"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="177a4-103">Introducción tootopology en Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="177a4-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="177a4-104">La topología devuelve un gráfo de recursos de red de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="177a4-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="177a4-105">gráfico de Hola traza la interconexión Hola entre conectividad de red tooend de hello recursos toorepresent Hola final.</span><span class="sxs-lookup"><span data-stu-id="177a4-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![información general de la topología][1]

<span data-ttu-id="177a4-107">En el portal de hello, topología devuelve objetos de recursos de hello en un cada red virtual.</span><span class="sxs-lookup"><span data-stu-id="177a4-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="177a4-108">relaciones de Hola se representan mediante líneas entre recursos de hello recursos fuera de la región de Monitor de red de hello, aunque en recursos de hello grupo no se mostrará.</span><span class="sxs-lookup"><span data-stu-id="177a4-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="177a4-109">recursos de Hola devueltos en la vista de hello portal son un subconjunto de los componentes de red de Hola que se representan.</span><span class="sxs-lookup"><span data-stu-id="177a4-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="177a4-110">lista completa de hello toosee de recursos de red puede usar [PowerShell](network-watcher-topology-powershell.md) o [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="177a4-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="177a4-111">Se requiere una instancia del Monitor de red en cada región que desee toorun topología en.</span><span class="sxs-lookup"><span data-stu-id="177a4-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="177a4-112">Los recursos se devuelven conexión Hola entre ellos se modelan en dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="177a4-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="177a4-113">**Contención**: por ejemplo, la red virtual contiene un subconjunto que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="177a4-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="177a4-114">**Asociación**: por ejemplo, una NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="177a4-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="177a4-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="177a4-115">Next steps</span></span>

<span data-ttu-id="177a4-116">Obtenga información acerca de cómo ver toouse PowerShell tooretrieve Hola topología visitando [topología de Monitor de red con PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="177a4-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
