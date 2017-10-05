---
title: "Adición de una puerta de enlace de red virtual a una red virtual para ExpressRoute: PowerShell (Azure) | Microsoft Docs"
description: "En este artículo, se indican los pasos para agregar una puerta de enlace de red virtual a una red virtual de Resource Manager ya creada para ExpressRoute."
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
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="b1605-103">Configuración de una puerta de enlace de red virtual para ExpressRoute con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1605-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1605-104">Resource Manager: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b1605-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="b1605-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1605-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="b1605-106">Clásico: PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1605-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="b1605-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b1605-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="b1605-108">Este artículo lo guía por los pasos para agregar, cambiar el tamaño y quitar una puerta de enlace de red virtual (VNet) para una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="b1605-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="b1605-109">Los pasos de esta configuración son específicos para las redes virtuales que se crearon con el modelo de implementación de Resource Manager que se utilizarán en una configuración ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b1605-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="b1605-110">Para obtener más información acerca de las puertas de enlace de red virtual y la configuración de puerta de enlace para ExpressRoute, consulte [Acerca de las puertas de enlace de red virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="b1605-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="b1605-111">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="b1605-111">Before beginning</span></span>
<span data-ttu-id="b1605-112">Compruebe que haya instalado los cmdlets más recientes de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1605-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b1605-113">Si no, deberá hacerlo antes de comenzar con los pasos de configuración.</span><span class="sxs-lookup"><span data-stu-id="b1605-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="b1605-114">Para obtener más información, vea [Install and Configure Azure PowerShell](/powershell/azure/overview) (Instalación y configuración de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b1605-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b1605-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1605-115">Next steps</span></span>
<span data-ttu-id="b1605-116">Después de crear la puerta de enlace de red virtual, puede vincular la red virtual a un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b1605-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="b1605-117">Consulte el artículo [Vinculación de la red virtual a circuitos ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b1605-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

