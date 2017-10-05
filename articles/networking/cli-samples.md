---
title: Ejemplos de la CLI de Azure | Microsoft Docs
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
ms.openlocfilehash: 7977460f61bfdabd399e45e86d9bbf2e5083992b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="c4503-103">Ejemplos de la CLI de Azure para redes</span><span class="sxs-lookup"><span data-stu-id="c4503-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="c4503-104">En la tabla siguiente se incluyen vínculos a scripts de Bash creados con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4503-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="c4503-105">**Conectividad entre recursos de Azure**</span><span class="sxs-lookup"><span data-stu-id="c4503-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="c4503-106">Creación de una red virtual para aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="c4503-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c4503-107">Creación de una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="c4503-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c4503-108">El tráfico a la subred de front-end está limitado a HTTP y SSH, mientras que el tráfico a la subred de back-end está limitado a MySQL, al puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="c4503-108">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> |
| [<span data-ttu-id="c4503-109">Emparejamiento de dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="c4503-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c4503-110">Creación y conexión de dos redes virtuales en la misma región.</span><span class="sxs-lookup"><span data-stu-id="c4503-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="c4503-111">Enrutamiento del tráfico por una aplicación virtual de red</span><span class="sxs-lookup"><span data-stu-id="c4503-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c4503-112">Creación de una red virtual con subredes de front-end y back-end y una máquina virtual que pueda enrutar el tráfico entre dos subredes.</span><span class="sxs-lookup"><span data-stu-id="c4503-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="c4503-113">Filtrado del tráfico de red entrante y saliente de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c4503-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c4503-114">Creación de una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="c4503-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c4503-115">El tráfico de red entrante a la subred de front-end está limitado a HTTP, HTTPS y SSH.</span><span class="sxs-lookup"><span data-stu-id="c4503-115">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH.</span></span> <span data-ttu-id="c4503-116">No se permite el tráfico saliente a Internet desde la subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="c4503-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="c4503-117">**Equilibrio de carga y dirección del tráfico**</span><span class="sxs-lookup"><span data-stu-id="c4503-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="c4503-118">Equilibrio de carga del tráfico a las máquinas virtuales para conseguir alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="c4503-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c4503-119">Crea varias máquinas virtuales de alta disponibilidad y una configuración de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="c4503-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="c4503-120">Equilibrio de carga entre varios sitios web en máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c4503-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c4503-121">Creación de dos máquinas virtuales con varias configuraciones de IP, unidas a un conjunto de disponibilidad de Azure, accesibles a través de una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="c4503-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="c4503-122">Dirección del tráfico entre varias regiones para conseguir alta disponibilidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c4503-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="c4503-123">Creación de dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="c4503-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
