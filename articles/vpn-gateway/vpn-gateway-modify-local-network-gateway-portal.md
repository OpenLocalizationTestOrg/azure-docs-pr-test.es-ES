---
title: "Modificar los prefijos de direcciones IP de puerta de enlace de red local de Hola y dirección IP de puerta de enlace de VPN de hello | Azure | Portal | Documentos de Microsoft"
description: "Este artículo le guiará a través de cambiar los prefijos de direcciones IP para la puerta de enlace de red local con hello portal de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="e9650-103">Modifique la configuración de puerta de enlace de red local con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e9650-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="e9650-104">En ocasiones, cambian valores de hello para la puerta de enlace de red local AddressPrefix o GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="e9650-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="e9650-105">Este artículo muestra cómo toomodify la configuración de puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="e9650-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="e9650-106">También puede modificar estas opciones mediante un método diferente, seleccione una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9650-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9650-107">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e9650-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="e9650-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9650-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="e9650-109">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e9650-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="e9650-110"><a name="ipaddprefix"></a>Modificación de los prefijos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="e9650-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="e9650-111">Cuando se modifican prefijos de direcciones IP, pasos de Hola que seguir dependen de si la puerta de enlace de red local tiene una conexión.</span><span class="sxs-lookup"><span data-stu-id="e9650-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="e9650-112"><a name="gwip"></a>Modificar la dirección IP de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="e9650-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="e9650-113">Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian.</span><span class="sxs-lookup"><span data-stu-id="e9650-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="e9650-114">Al cambiar la dirección IP pública hello, pasos de hello que seguir dependen de si la puerta de enlace de red local tiene una conexión.</span><span class="sxs-lookup"><span data-stu-id="e9650-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e9650-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9650-115">Next steps</span></span>

<span data-ttu-id="e9650-116">Puede comprobar la conexión de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e9650-116">You can verify your gateway connection.</span></span> <span data-ttu-id="e9650-117">Consulte [Comprobación de una conexión de puerta de enlace](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e9650-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>