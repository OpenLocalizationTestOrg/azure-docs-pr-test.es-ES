---
title: "Modificar los prefijos de direcciones IP de puerta de enlace de red local de Hola y dirección IP de puerta de enlace de VPN de hello | Azure | CLI | Documentos de Microsoft"
description: "Este artículo le guiará a través de cambiar los prefijos de direcciones IP para la puerta de enlace de red local con hello CLI de Azure."
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="4eb92-103">Modifique la configuración de puerta de enlace de red local con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4eb92-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="4eb92-104">En ocasiones, cambian valores de hello para el prefijo de dirección de puerta de enlace de red local o la dirección IP de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4eb92-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="4eb92-105">Este artículo muestra cómo toomodify la configuración de puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="4eb92-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="4eb92-106">También puede modificar estas opciones mediante un método diferente, seleccione una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="4eb92-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4eb92-107">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4eb92-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="4eb92-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4eb92-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="4eb92-109">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4eb92-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="4eb92-110"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4eb92-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="4eb92-111">Instale la versión más reciente de Hola de comandos de CLI de hello (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="4eb92-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="4eb92-112">Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4eb92-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="4eb92-113"><a name="ipaddprefix"></a>Modificación de los prefijos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="4eb92-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="4eb92-114"><a name="gwip"></a>Modificar la dirección IP de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="4eb92-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4eb92-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4eb92-115">Next steps</span></span>

<span data-ttu-id="4eb92-116">Puede comprobar la conexión de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4eb92-116">You can verify your gateway connection.</span></span> <span data-ttu-id="4eb92-117">Consulte [Comprobación de una conexión de puerta de enlace](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4eb92-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

