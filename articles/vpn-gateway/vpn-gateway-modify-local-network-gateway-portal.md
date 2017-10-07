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
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Modifique la configuración de puerta de enlace de red local con hello portal de Azure

En ocasiones, cambian valores de hello para la puerta de enlace de red local AddressPrefix o GatewayIPAddress. Este artículo muestra cómo toomodify la configuración de puerta de enlace de red local. También puede modificar estas opciones mediante un método diferente, seleccione una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [CLI de Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>Modificación de los prefijos de direcciones IP

Cuando se modifican prefijos de direcciones IP, pasos de Hola que seguir dependen de si la puerta de enlace de red local tiene una conexión.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Modificar la dirección IP de puerta de enlace de Hola

Si el dispositivo VPN de Hola que desea tooconnect toohas cambia su dirección IP pública, debe toomodify tooreflect de puerta de enlace de red local de Hola que cambian. Al cambiar la dirección IP pública hello, pasos de hello que seguir dependen de si la puerta de enlace de red local tiene una conexión.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Puede comprobar la conexión de la puerta de enlace. Consulte [Comprobación de una conexión de puerta de enlace](vpn-gateway-verify-connection-resource-manager.md).