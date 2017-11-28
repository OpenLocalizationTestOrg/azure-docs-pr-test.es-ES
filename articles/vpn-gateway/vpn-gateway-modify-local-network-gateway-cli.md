---
title: "Modificación de los prefijos de direcciones IP de puertas de enlace de red local y la dirección IP de VPN Gateway | Azure | CLI| Microsoft Docs"
description: "En este artículo se explica paso a paso cómo cambiar los prefijos de direcciones IP de la puerta de enlace de red local con la CLI de Azure."
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
ms.openlocfilehash: 7db1ad970ebb93d46d5a861f9a9b27bf121531a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-cli"></a><span data-ttu-id="b60b5-103">Modificación de la configuración de la puerta de enlace de red local mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b60b5-103">Modify local network gateway settings using the Azure CLI</span></span>

<span data-ttu-id="b60b5-104">A veces, cambia la configuración Prefijo de dirección o Dirección IP de la puerta de enlace de la puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="b60b5-104">Sometimes the settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="b60b5-105">Este artículo muestra cómo modificar la configuración de puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="b60b5-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="b60b5-106">También puede modificar estas configuraciones mediante un método diferente, si selecciona una opción diferente de la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="b60b5-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b60b5-107">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b60b5-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="b60b5-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b60b5-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="b60b5-109">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b60b5-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="b60b5-110"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b60b5-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="b60b5-111">Instale la versión más reciente de los comandos de la CLI (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="b60b5-111">Install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="b60b5-112">Para más información sobre la instalación de los comandos de la CLI, consulte [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b60b5-112">For information about installing the CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="b60b5-113"><a name="ipaddprefix"></a>Modificación de los prefijos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="b60b5-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="b60b5-114"><a name="gwip"></a>Modificación de la dirección IP de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="b60b5-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b60b5-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b60b5-115">Next steps</span></span>

<span data-ttu-id="b60b5-116">Puede comprobar la conexión de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b60b5-116">You can verify your gateway connection.</span></span> <span data-ttu-id="b60b5-117">Consulte [Comprobación de una conexión de puerta de enlace](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b60b5-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

