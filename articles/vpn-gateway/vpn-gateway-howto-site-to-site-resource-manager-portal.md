---
title: 'Conectar su tooan de red local red virtual de Azure: VPN de sitio a sitio: Portal | Documentos de Microsoft'
description: "Una conexión de IPsec desde el entorno local de red tooan red virtual de Azure a través de toocreate de pasos Hola Internet pública. Estos pasos le ayudarán a crear una conexión de puerta de enlace VPN de sitio a sitio entre entornos mediante el portal de Hola."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Crear una conexión de sitio a sitio en hello portal de Azure

Este artículo muestra cómo toouse Hola toocreate portal Azure una conexión de puerta de enlace VPN de sitio a sitio desde su toohello de red local red virtual. pasos de Hello en este artículo aplican toohello modelo de implementación de administrador de recursos. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2). Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa. Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).

![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Antes de empezar

Compruebe que se ha cumplido hello siguiendo criterios antes de comenzar la configuración:

* Asegúrese de que tiene un dispositivo VPN compatible y alguna persona tooconfigure capaz de él. Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN. Esta dirección IP no puede estar detrás de un NAT.
* Si no está familiarizado con intervalos de direcciones IP de hello ubicados en configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted. Al crear esta configuración, debe especificar prefijos para intervalo de direcciones IP con hello que Azure enrutará la ubicación de tooyour local. Ninguna de las subredes de saludo de la red local puede enumerar sobre el regazo con subredes de red virtual de Hola que desee tooconnect a. 

### <a name="values"></a>Valores del ejemplo

ejemplos de Hello en este artículo utiliza Hola después de valores. Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.

* **Nombre de red virtual:** TestVNet1
* **Espacio de direcciones:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcional para este ejercicio)
* **Subredes:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (opcional para este ejercicio)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupo de recursos:** TestRG1
* **Ubicación:** este de EE. UU.
* **Servidor DNS:** opcional. dirección IP de saludo del servidor DNS.
* **Nombre de la puerta de enlace de red virtual:** VNet1GW
* **Dirección IP pública:** VNet1GWIP
* **Tipo de VPN:** basada en rutas
* **Tipo de conexión:** de sitio a sitio (IPsec)
* **Tipo de puerta de enlace:** VPN
* **Nombre de la puerta de enlace de red local:** Site2
* **Nombre de conexión:** VNet1toSite2

## <a name="CreatVNet"></a>1. Crear una red virtual

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Especificación de un servidor DNS

DNS no es necesario toocreate un sitio a sitio conexión. Sin embargo, si desea toohave la resolución de nombres para los recursos de red virtual tooyour implementada, debe especificar un servidor DNS. Esta opción permite especificar el servidor DNS de Hola que quiere toouse de resolución de nombres para esta red virtual. No crea un servidor DNS. Para más información acerca de la resolución de nombres, consulte [Resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Crear una subred de puerta de enlace de Hola

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Crear puerta de enlace VPN de Hola

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Crear puerta de enlace de red local de Hola

puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local. Se asigne un nombre mediante el cual Azure puede consulte tooit y luego especifique la dirección IP de Hola a sitio Hola de hello local VPN dispositivo toowhich creará una conexión. También especificar prefijos de direcciones IP de Hola que se enrutará a través del dispositivo VPN de toohello de puerta de enlace VPN de Hola. Especifique los prefijos de direcciones Hola son prefijos de hello ubicados en la red local. Si los cambios de red local o necesita toochange Hola la dirección IP para el dispositivo VPN de hello, puede actualizar fácilmente los valores de hello más tarde.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Configurar el dispositivo VPN

Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN. En este paso, se configura el dispositivo VPN. Al configurar el dispositivo VPN, necesita Hola siguiente:

- Una clave compartida. Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio. En estos ejemplos se utiliza una clave compartida básica. Se recomienda que generar un toouse clave más compleja.
- Hola dirección IP pública de la puerta de enlace de red virtual. Puede ver la dirección IP pública hello mediante Hola portal de Azure, PowerShell o CLI. Hola toofind dirección IP pública de la puerta de enlace VPN con hello portal de Azure, navegue demasiado**puertas de enlace de red Virtual**, a continuación, haga clic en nombre de saludo de la puerta de enlace.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Crear la conexión de VPN de Hola

Crear la conexión de VPN de sitio a sitio Hola entre la puerta de enlace de red virtual y el dispositivo VPN local.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Compruebe la conexión de VPN de Hola

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>máquina virtual de tooconnect tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>¿Cómo tooreset una puerta de enlace VPN

Restablecer una puerta de enlace de VPN de Azure es útil si se pierde la conectividad VPN entre locales en uno o varios túneles VPN de sitio a sitio. En esta situación, los dispositivos VPN local son todo funciona correctamente, pero son tooestablish imposibilidad de túneles de IPsec con puertas de enlace de VPN de Azure de Hola. Para conocer los pasos, consulte [Restablecimiento de una puerta de enlace de VPN](vpn-gateway-resetgw-classic.md).

## <a name="resize"></a>¿Cómo toochange una puerta de enlace de SKU (cambio de tamaño de una puerta de enlace)

Para los pasos de hello toochange una SKU de puerta de enlace, vea [SKU de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Para más información acerca de la tunelización forzada, consulte la [información acerca de la tunelización forzada](vpn-gateway-forced-tunneling-rm.md).
* Para obtener información acerca de las conexiones activo/activo de alta disponibilidad, consulte [Conectividad de alta disponibilidad entre locales y de red virtual a red virtual](vpn-gateway-highlyavailable.md).
