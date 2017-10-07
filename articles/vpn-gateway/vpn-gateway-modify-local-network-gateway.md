---
title: "Modificar los prefijos de direcciones IP de puerta de enlace de red local de Hola y dirección IP de puerta de enlace de VPN de hello | Azure | PowerShell | Documentos de Microsoft"
description: "Este artículo explica paso a paso cómo cambiar los prefijos de direcciones IP de la puerta de enlace de red local con PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="61c21-103">Modificación de la configuración de la puerta de enlace de red local mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="61c21-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="61c21-104">En ocasiones, cambian valores de hello para la puerta de enlace de red local AddressPrefix o GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="61c21-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="61c21-105">Este artículo muestra cómo toomodify la configuración de puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="61c21-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="61c21-106">También puede modificar estas opciones mediante un método diferente, seleccione una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="61c21-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="61c21-107">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="61c21-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="61c21-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61c21-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="61c21-109">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="61c21-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="61c21-110"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="61c21-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="61c21-111">Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="61c21-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="61c21-112">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="61c21-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="61c21-113"><a name="ipaddprefix"></a>Modificación de los prefijos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="61c21-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="61c21-114"><a name="gwip"></a>Modificar la dirección IP de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="61c21-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="61c21-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61c21-115">Next steps</span></span>

<span data-ttu-id="61c21-116">Puede comprobar la conexión de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="61c21-116">You can verify your gateway connection.</span></span> <span data-ttu-id="61c21-117">Consulte [Comprobación de una conexión de puerta de enlace](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="61c21-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>