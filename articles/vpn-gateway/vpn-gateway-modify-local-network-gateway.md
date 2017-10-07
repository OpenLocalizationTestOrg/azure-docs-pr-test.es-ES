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
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Modificación de la configuración de la puerta de enlace de red local mediante PowerShell

En ocasiones, cambian valores de hello para la puerta de enlace de red local AddressPrefix o GatewayIPAddress. Este artículo muestra cómo toomodify la configuración de puerta de enlace de red local. También puede modificar estas opciones mediante un método diferente, seleccione una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [CLI de Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Antes de empezar

Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.

## <a name="ipaddprefix"></a>Modificación de los prefijos de direcciones IP

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Modificar la dirección IP de puerta de enlace de Hola

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Puede comprobar la conexión de la puerta de enlace. Consulte [Comprobación de una conexión de puerta de enlace](vpn-gateway-verify-connection-resource-manager.md).