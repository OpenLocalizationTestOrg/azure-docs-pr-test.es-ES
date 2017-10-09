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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="b4956-103">Configuración de una puerta de enlace de red virtual para ExpressRoute con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4956-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4956-104">Resource Manager: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b4956-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="b4956-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4956-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="b4956-106">Clásico: PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4956-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="b4956-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b4956-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="b4956-108">Este artículo le guiará a través de hello pasos tooadd, cambiar el tamaño y quitar una puerta de enlace de red virtual (VNet) para una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="b4956-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="b4956-109">pasos de Hola para esta configuración son específicos para redes virtuales que se crearon con el modelo de implementación de administrador de recursos de Hola que se usará en una configuración de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b4956-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="b4956-110">Para obtener más información acerca de las puertas de enlace de red virtual y la configuración de puerta de enlace para ExpressRoute, consulte [Acerca de las puertas de enlace de red virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="b4956-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="b4956-111">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="b4956-111">Before beginning</span></span>
<span data-ttu-id="b4956-112">Compruebe que ha instalado los cmdlets de PowerShell de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4956-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b4956-113">Si no ha instalado los cmdlets más recientes de hello, necesita toodo así antes de comenzar los pasos de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4956-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="b4956-114">Para obtener más información, vea [Install and Configure Azure PowerShell](/powershell/azure/overview) (Instalación y configuración de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b4956-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b4956-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4956-115">Next steps</span></span>
<span data-ttu-id="b4956-116">Después de haber creado la puerta de enlace de red virtual de hello, puede vincular el circuito de ExpressRoute de tooan de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b4956-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="b4956-117">Vea [vincular un circuito de ExpressRoute de red Virtual tooan](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b4956-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

