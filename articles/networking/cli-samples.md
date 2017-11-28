---
title: Ejemplos de CLI aaaAzure | Documentos de Microsoft
description: Ejemplos de la CLI de Azure
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="e9a9b-103">Ejemplos de la CLI de Azure para redes</span><span class="sxs-lookup"><span data-stu-id="e9a9b-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="e9a9b-104">Hello tabla siguiente incluye vínculos toobash scripts creados con hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="e9a9b-105">**Conectividad entre recursos de Azure**</span><span class="sxs-lookup"><span data-stu-id="e9a9b-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="e9a9b-106">Creación de una red virtual para aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="e9a9b-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="e9a9b-107">Creación de una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="e9a9b-108">Subred de tráfico toohello front-end es tooHTTP limitado y SSH, al tráfico toohello subred back-end es tooMySQL limitado, puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="e9a9b-109">Emparejamiento de dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="e9a9b-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="e9a9b-110">Crea y se conecta dos redes virtuales en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="e9a9b-111">Enrutamiento del tráfico por una aplicación virtual de red</span><span class="sxs-lookup"><span data-stu-id="e9a9b-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="e9a9b-112">Crea una red virtual con una máquina virtual que pueda tooroute el tráfico entre subredes Hola dos y subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="e9a9b-113">Filtrado del tráfico de red entrante y saliente de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e9a9b-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="e9a9b-114">Creación de una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="e9a9b-115">El tráfico de red entrante toohello la subred front-end es limitado tooHTTP, SSH y HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="e9a9b-116">No se permite el tráfico saliente toohello Internet de subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="e9a9b-117">**Equilibrio de carga y dirección del tráfico**</span><span class="sxs-lookup"><span data-stu-id="e9a9b-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="e9a9b-118">Cargar tooVMs de tráfico de equilibrio de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="e9a9b-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="e9a9b-119">Crea varias máquinas virtuales de alta disponibilidad y una configuración de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="e9a9b-120">Equilibrio de carga entre varios sitios web en máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e9a9b-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="e9a9b-121">Crea dos máquinas virtuales con varias configuraciones de IP, tooan unido a Azure conjunto de disponibilidad, accesible a través de un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="e9a9b-122">Dirección del tráfico entre varias regiones para conseguir alta disponibilidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e9a9b-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="e9a9b-123">Creación de dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e9a9b-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
