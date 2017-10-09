---
title: 'Agregar un tooa de puerta de enlace de red virtual red virtual para ExpressRoute: PowerShell: Azure | Documentos de Microsoft'
description: "En este artículo se explica cómo agregar un tooan de puerta de enlace de red virtual ya creado el Administrador de recursos VNet para ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>Configuración de una puerta de enlace de red virtual para ExpressRoute con PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager: Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Clásico: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Este artículo le guiará a través de hello pasos tooadd, cambiar el tamaño y quitar una puerta de enlace de red virtual (VNet) para una red virtual existente. pasos de Hola para esta configuración son específicos para redes virtuales que se crearon con el modelo de implementación de administrador de recursos de Hola que se usará en una configuración de ExpressRoute. Para obtener más información acerca de las puertas de enlace de red virtual y la configuración de puerta de enlace para ExpressRoute, consulte [Acerca de las puertas de enlace de red virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Antes de comenzar
Compruebe que ha instalado los cmdlets de PowerShell de Azure más recientes de Hola. Si no ha instalado los cmdlets más recientes de hello, necesita toodo así antes de comenzar los pasos de configuración de Hola. Para obtener más información, vea [Install and Configure Azure PowerShell](/powershell/azure/overview) (Instalación y configuración de Azure PowerShell).

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Después de haber creado la puerta de enlace de red virtual de hello, puede vincular el circuito de ExpressRoute de tooan de red virtual. Vea [vincular un circuito de ExpressRoute de red Virtual tooan](expressroute-howto-linkvnet-arm.md).

