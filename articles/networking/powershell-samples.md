---
title: aaaAzure ejemplos de PowerShell | Documentos de Microsoft
description: Ejemplos de Azure PowerShell
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="250fa-103">Ejemplos de Azure PowerShell para redes</span><span class="sxs-lookup"><span data-stu-id="250fa-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="250fa-104">Hello siguiente tabla incluye tooscripts vínculos creados con PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="250fa-104">hello following table includes links tooscripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="250fa-105">**Conectividad entre recursos de Azure**</span><span class="sxs-lookup"><span data-stu-id="250fa-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="250fa-106">Creación de una red virtual para aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="250fa-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="250fa-107">Creación de una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="250fa-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="250fa-108">Subred de tráfico toohello front-end es tooHTTP limitado, al tráfico toohello subred back-end es tooSQL limitado, el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="250fa-108">Traffic toohello front-end subnet is limited tooHTTP, while traffic toohello back-end subnet is limited tooSQL, port 1433.</span></span> |
| [<span data-ttu-id="250fa-109">Emparejamiento de dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="250fa-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="250fa-110">Crea y se conecta dos redes virtuales en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="250fa-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="250fa-111">Enrutamiento del tráfico por una aplicación virtual de red</span><span class="sxs-lookup"><span data-stu-id="250fa-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="250fa-112">Crea una red virtual con una máquina virtual que pueda tooroute el tráfico entre subredes Hola dos y subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="250fa-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="250fa-113">Filtrado del tráfico de red entrante y saliente de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="250fa-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="250fa-114">Creación de una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="250fa-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="250fa-115">El tráfico de red entrante subred de front-end de toohello es tooHTTP limitado y HTTPS...</span><span class="sxs-lookup"><span data-stu-id="250fa-115">Inbound network traffic toohello front-end subnet is limited tooHTTP and HTTPS..</span></span> <span data-ttu-id="250fa-116">No se permite el tráfico saliente toohello Internet de subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="250fa-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="250fa-117">**Equilibrio de carga y dirección del tráfico**</span><span class="sxs-lookup"><span data-stu-id="250fa-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="250fa-118">Cargar tooVMs de tráfico de equilibrio de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="250fa-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="250fa-119">Crea varias máquinas virtuales de alta disponibilidad y una configuración de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="250fa-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="250fa-120">Equilibrio de carga entre varios sitios web en máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="250fa-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="250fa-121">Crea dos máquinas virtuales con varias configuraciones de IP, tooan unido a Azure conjunto de disponibilidad, accesible a través de un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="250fa-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="250fa-122">Dirección del tráfico entre varias regiones para conseguir alta disponibilidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="250fa-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="250fa-123">Creación de dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="250fa-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
