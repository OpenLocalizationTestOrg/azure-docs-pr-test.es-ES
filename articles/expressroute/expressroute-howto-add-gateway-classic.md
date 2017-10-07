---
title: "Configuración de una puerta de enlace de red virtual para ExpressRoute mediante PowerShell: clásica (Azure) | Microsoft Docs"
description: "Configure una puerta de enlace de red virtual para un modelo de implementación clásica con PowerShell para una configuración de ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Configuración de una puerta de enlace de red virtual para ExpressRoute mediante PowerShell (clásica)
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Clásico: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

En este artículo le guiará a través de hello pasos tooadd, cambiar el tamaño y quitar una puerta de enlace de red virtual (VNet) para una red virtual existente. Hello pasos para esta configuración son específicos para redes virtuales que se crearon con hello **modelo de implementación clásica** y que se puede utilizar en una configuración de ExpressRoute. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Información sobre los modelos de implementación de Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Antes de comenzar
Compruebe que ha instalado los cmdlets de PowerShell de Azure de hello necesarios para esta configuración (versión 1.0.2 o posterior). Si no tiene instalado Hola cmdlets, necesitará toodo así antes de comenzar los pasos de configuración de Hola. Para obtener más información acerca de cómo instalar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Después de haber creado la puerta de enlace de red virtual de hello, puede vincular el circuito de ExpressRoute de tooan de red virtual. Vea [vincular un circuito de ExpressRoute de red Virtual tooan](expressroute-howto-linkvnet-classic.md).

