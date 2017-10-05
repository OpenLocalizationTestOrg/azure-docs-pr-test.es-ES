---
title: "Introducción a la topología de Azure Network Watcher | Microsoft Docs"
description: "En esta página se proporciona una introducción a las funcionalidades de la topología de Network Watcher."
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
ms.openlocfilehash: 42443f614b76b8180ac163b9889163021adbf048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a><span data-ttu-id="df90a-103">Introducción a la topología de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="df90a-103">Introduction to topology in Azure Network Watcher</span></span>

<span data-ttu-id="df90a-104">La topología devuelve un gráfo de recursos de red de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="df90a-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="df90a-105">El grafo traza la interconexión entre los recursos para representar la conectividad de red de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="df90a-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span></span>

![información general de la topología][1]

<span data-ttu-id="df90a-107">En el portal, la topología devuelve los objetos de recursos por cada red virtual.</span><span class="sxs-lookup"><span data-stu-id="df90a-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span></span> <span data-ttu-id="df90a-108">Las relaciones se representan mediante líneas entre los recursos. No se mostrarán los recursos fuera de la región de Network Watcher, aunque estén en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="df90a-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span></span> <span data-ttu-id="df90a-109">Los recursos que se devuelven en la vista de portal son un subconjunto de los componentes de red que se representan.</span><span class="sxs-lookup"><span data-stu-id="df90a-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span></span> <span data-ttu-id="df90a-110">Para ver la lista completa de los recursos de red, puede usar [PowerShell](network-watcher-topology-powershell.md) o [REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="df90a-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="df90a-111">Se requiere una instancia de Network Watcher en cada región en que desea ejecutar la topología.</span><span class="sxs-lookup"><span data-stu-id="df90a-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span></span>

<span data-ttu-id="df90a-112">Mientras los recursos devuelven la conexión entre ellos, se modelan con dos relaciones.</span><span class="sxs-lookup"><span data-stu-id="df90a-112">As resources are returned the connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="df90a-113">**Contención**: por ejemplo, la red virtual contiene un subconjunto que incluye una NIC.</span><span class="sxs-lookup"><span data-stu-id="df90a-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="df90a-114">**Asociación**: por ejemplo, una NIC está asociada a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="df90a-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="df90a-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df90a-115">Next steps</span></span>

<span data-ttu-id="df90a-116">Para obtener información sobre cómo usar PowerShell para recuperar la vista de topología, visite [Visualización de la topología de Network Watcher con PowerShell](network-watcher-topology-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="df90a-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
