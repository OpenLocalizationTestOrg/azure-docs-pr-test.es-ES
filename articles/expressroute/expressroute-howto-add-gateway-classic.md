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
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="062dd-103">Configuración de una puerta de enlace de red virtual para ExpressRoute mediante PowerShell (clásica)</span><span class="sxs-lookup"><span data-stu-id="062dd-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="062dd-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="062dd-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="062dd-105">Clásico: PowerShell</span><span class="sxs-lookup"><span data-stu-id="062dd-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="062dd-106">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="062dd-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="062dd-107">Este artículo le guiará por los pasos para agregar, cambiar el tamaño y quitar una puerta de enlace de red virtual (VNet) para una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="062dd-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="062dd-108">Los pasos de esta configuración son específicos para las redes virtuales que se crearon con el **modelo de implementación clásica** y que se utilizarán en una configuración ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="062dd-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="062dd-109">**Información acerca de los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="062dd-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="062dd-110">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="062dd-110">Before beginning</span></span>
<span data-ttu-id="062dd-111">Compruebe que ha instalado los cmdlets de Azure PowerShell necesarios para esta configuración (1.0.2 o posterior).</span><span class="sxs-lookup"><span data-stu-id="062dd-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="062dd-112">Si no, deberá hacerlo antes de comenzar con los pasos de configuración.</span><span class="sxs-lookup"><span data-stu-id="062dd-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="062dd-113">Para más información sobre cómo instalar Azure PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="062dd-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="062dd-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="062dd-114">Next steps</span></span>
<span data-ttu-id="062dd-115">Después de crear la puerta de enlace de red virtual, puede vincular la red virtual a un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="062dd-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="062dd-116">Consulte el artículo [Vinculación de la red virtual a circuitos ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="062dd-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

