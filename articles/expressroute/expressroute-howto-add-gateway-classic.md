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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="c3022-103">Configuración de una puerta de enlace de red virtual para ExpressRoute mediante PowerShell (clásica)</span><span class="sxs-lookup"><span data-stu-id="c3022-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3022-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3022-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="c3022-105">Clásico: PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3022-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="c3022-106">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c3022-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="c3022-107">En este artículo le guiará a través de hello pasos tooadd, cambiar el tamaño y quitar una puerta de enlace de red virtual (VNet) para una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c3022-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="c3022-108">Hello pasos para esta configuración son específicos para redes virtuales que se crearon con hello **modelo de implementación clásica** y que se puede utilizar en una configuración de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c3022-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="c3022-109">**Información sobre los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="c3022-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="c3022-110">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="c3022-110">Before beginning</span></span>
<span data-ttu-id="c3022-111">Compruebe que ha instalado los cmdlets de PowerShell de Azure de hello necesarios para esta configuración (versión 1.0.2 o posterior).</span><span class="sxs-lookup"><span data-stu-id="c3022-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="c3022-112">Si no tiene instalado Hola cmdlets, necesitará toodo así antes de comenzar los pasos de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3022-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="c3022-113">Para obtener más información acerca de cómo instalar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c3022-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c3022-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3022-114">Next steps</span></span>
<span data-ttu-id="c3022-115">Después de haber creado la puerta de enlace de red virtual de hello, puede vincular el circuito de ExpressRoute de tooan de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c3022-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="c3022-116">Vea [vincular un circuito de ExpressRoute de red Virtual tooan](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c3022-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

