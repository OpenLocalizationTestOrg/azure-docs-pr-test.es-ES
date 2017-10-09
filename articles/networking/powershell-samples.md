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
# <a name="azure-powershell-samples-for-networking"></a>Ejemplos de Azure PowerShell para redes

Hello siguiente tabla incluye tooscripts vínculos creados con PowerShell de Azure.

| | |
|-|-|
|**Conectividad entre recursos de Azure**||
| [Creación de una red virtual para aplicaciones de niveles múltiples](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Creación de una red virtual con subredes de front-end y back-end. Subred de tráfico toohello front-end es tooHTTP limitado, al tráfico toohello subred back-end es tooSQL limitado, el puerto 1433. |
| [Emparejamiento de dos redes virtuales](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea y se conecta dos redes virtuales en hello misma región. |
| [Enrutamiento del tráfico por una aplicación virtual de red](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea una red virtual con una máquina virtual que pueda tooroute el tráfico entre subredes Hola dos y subredes de front-end y back-end. |
| [Filtrado del tráfico de red entrante y saliente de máquina virtual](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Creación de una red virtual con subredes de front-end y back-end. El tráfico de red entrante subred de front-end de toohello es tooHTTP limitado y HTTPS... No se permite el tráfico saliente toohello Internet de subred de back-end de Hola. |
|**Equilibrio de carga y dirección del tráfico**||
| [Cargar tooVMs de tráfico de equilibrio de alta disponibilidad](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea varias máquinas virtuales de alta disponibilidad y una configuración de equilibrio de carga. |
| [Equilibrio de carga entre varios sitios web en máquinas virtuales](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea dos máquinas virtuales con varias configuraciones de IP, tooan unido a Azure conjunto de disponibilidad, accesible a través de un equilibrador de carga de Azure. |
| [Dirección del tráfico entre varias regiones para conseguir alta disponibilidad de las aplicaciones](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Creación de dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager. |
| | |
