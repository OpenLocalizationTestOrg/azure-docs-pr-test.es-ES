---
title: 'Conectar su tooan de red local red virtual de Azure: VPN de sitio a sitio: CLI | Documentos de Microsoft'
description: "Una conexión de IPsec desde el entorno local de red tooan red virtual de Azure a través de toocreate de pasos Hola Internet pública. Estos pasos le ayudarán a crear una conexión de VPN Gateway de sitio a sitio entre locales mediante la CLI."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Creación de una red virtual con una conexión VPN de sitio a sitio mediante la CLI

Este artículo muestra cómo toouse hello Azure CLI toocreate una conexión de puerta de enlace VPN de sitio a sitio desde su toohello de red local red virtual. pasos de Hello en este artículo aplican toohello modelo de implementación de administrador de recursos. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:<br>

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2). Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa. Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Antes de empezar

Compruebe que se ha cumplido hello siguiendo criterios antes de comenzar la configuración:

* Asegúrese de que tiene un dispositivo VPN compatible y alguna persona tooconfigure capaz de él. Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN. Esta dirección IP no puede estar detrás de un NAT.
* Si no está familiarizado con intervalos de direcciones IP de hello ubicados en configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted. Al crear esta configuración, debe especificar prefijos para intervalo de direcciones IP con hello que Azure enrutará la ubicación de tooyour local. Ninguna de las subredes de saludo de la red local puede enumerar sobre el regazo con subredes de red virtual de Hola que desee tooconnect a.
* Compruebe que ha instalado una versión más reciente de los comandos de CLI de hello (2.0 o posteriores). Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli) y [empezar a trabajar con Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Valores del ejemplo

Puede usar hello después valores toocreate un entorno de prueba, o consultar valores toothese toobetter comprender los ejemplos de hello en este artículo:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Conectar tooyour suscripción

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Crear un grupo de recursos

Hello en el ejemplo siguiente se crea un grupo de recursos con el nombre 'TestRG1' en la ubicación de hello 'eastus'. Si ya tiene un grupo de recursos en la región de Hola que deseas toocreate la red virtual, puede usar en su lugar que uno.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Crear una red virtual

Si ya no tiene una red virtual, cree uno mediante hello [crear red virtual de red az](/cli/azure/network/vnet#create) comando. Al crear una red virtual, asegúrese de que los espacios de direcciones de hello especificados no superponen con cualquiera de los espacios de direcciones de Hola que existen en la red local.

Hello en el ejemplo siguiente se crea una red virtual con el nombre de una subred, 'Subred1' y 'TestVNet1'.

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Crear una subred de puerta de enlace de Hola

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Para esta configuración, también es necesaria una subred de la puerta de enlace. puerta de enlace de red virtual de Hello usa una subred de puerta de enlace que contiene direcciones IP de Hola que usan servicios de puerta de enlace VPN de Hola. Cuando se crea una subred de la puerta de enlace, debe tener el nombre 'GatewaySubnet'. Si le asigna otro nombre, crea una subred, pero Azure no la tratará como subred de puerta de enlace.

tamaño de Hola de subred de puerta de enlace de Hola que especifique depende en configuración de puerta de enlace VPN de Hola que desea toocreate. Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, le recomendamos que cree una subred mayor que incluya más direcciones seleccionando /27 o /28. Mediante una subred de puerta de enlace mayor permite suficiente IP direcciones tooaccommodate futuras configuraciones posibles.

Hola de uso [crear subredes de red virtual de red az](/cli/azure/network/vnet/subnet#create) subred de puerta de enlace de comando toocreate Hola.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Crear puerta de enlace de red local de Hola

puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local. Se asigne un nombre mediante el cual Azure puede consulte tooit y luego especifique la dirección IP de Hola a sitio Hola de hello local VPN dispositivo toowhich creará una conexión. También especificar prefijos de direcciones IP de Hola que se enrutará a través del dispositivo VPN de toohello de puerta de enlace VPN de Hola. Especifique los prefijos de direcciones Hola son prefijos de hello ubicados en la red local. Si cambia su red local, puede actualizar fácilmente los prefijos de Hola.

Usar hello siguientes valores:

* Hola *--dirección de ip de puerta de enlace* es la dirección IP de hello de dispositivo VPN local. El dispositivo VPN no se encuentra detrás de un NAT.
* Hola *--prefijos de direcciones local* son espacios de direcciones de sus instalaciones.

Hola de uso [crear az red local puerta de enlace](/cli/azure/network/local-gateway#create) comando tooadd una puerta de enlace de red local con varios prefijos de direcciones:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Solicite una dirección IP pública

Una puerta de enlace VPN debe tener una dirección IP pública. Solicitar el recurso de dirección IP hello y, a continuación, hacer referencia tooit al crear la puerta de enlace de red virtual. dirección IP de Hola se asigna dinámicamente toohello recursos cuando se crea la puerta de enlace VPN de Hola. Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*. No se puede solicitar una asignación de direcciones IP públicas estáticas. Sin embargo, esto no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN. cambios en la dirección IP pública hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear. No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.

Hola de uso [crear az red public-ip](/cli/azure/network/public-ip#create) comando toorequest una dirección IP pública dinámica.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Crear puerta de enlace VPN de Hola

Crear puerta de enlace VPN de red virtual de Hola. Crear una puerta de enlace VPN puede tardar hasta too45 minutos o más toocomplete.

Usar hello siguientes valores:

* Hola *: tipo de puerta de enlace* para un sitio a sitio es configuración *Vpn*. tipo de puerta de enlace de Hello siempre es configuración toohello específico que va a implementar. Para más información, consulte [Tipos de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwtype).
* Hola *--vpn-type* puede ser *RouteBased* (llamada tooas una puerta de enlace dinámico en algunos documentos), o *PolicyBased* (denominada tooas una puerta de enlace estática en algunos documentación). saludo es toorequirements específico del dispositivo de Hola que se va a conectar. Para más información sobre los tipos de puertas de enlace de VPN, consulte [Acerca de la información de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md#vpntype).
* Seleccione Hola SKU de puerta de enlace que desea toouse. Hay limitaciones de configuración para determinadas SKU. Consulte [SKU de puertas de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku) para más información.

Crear puerta de enlace VPN de hello con hello [crear enlace de red virtual de red az](/cli/azure/network/vnet-gateway#create) comando. Si ejecuta este comando usando hello '--sin - wait' parámetro, no ve los comentarios o la salida. Este parámetro permite toocreate de puerta de enlace de hello en segundo plano de Hola. Tardará aproximadamente 45 minutos toocreate una puerta de enlace.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Configurar el dispositivo VPN

Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN. En este paso, se configura el dispositivo VPN. Al configurar el dispositivo VPN, necesita Hola siguiente:

- Una clave compartida. Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio. En estos ejemplos se utiliza una clave compartida básica. Se recomienda que generar un toouse clave más compleja.
- Hola dirección IP pública de la puerta de enlace de red virtual. Puede ver la dirección IP pública hello mediante Hola portal de Azure, PowerShell o CLI. dirección IP toofind Hola pública de la puerta de enlace de red virtual, use hello [lista de ip pública de red az](/cli/azure/network/public-ip#list) comando. Para facilitar la lectura, la salida de hello es toodisplay con formato de lista de Hola de direcciones IP públicas en formato de tabla.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Crear la conexión de VPN de Hola

Crear la conexión de VPN de sitio a sitio Hola entre la puerta de enlace de red virtual y el dispositivo VPN local. Preste especial atención toohello compartido valor de clave, que debe coincidir con hello configurado comparte el valor de clave para el dispositivo VPN.

Crear conexión de hello mediante hello [crear conexión de vpn de red az](/cli/azure/network/vpn-connection#create) comando.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Después de un valor bajo al Hola se establecerá la conexión.

## <a name="toverify"></a>10. Compruebe la conexión de VPN de Hola

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Si desea toouse tooverify de otro método la conexión, consulte [comprobar una conexión de puerta de enlace VPN](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>máquina virtual de tooconnect tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Tareas comunes

Esta sección contiene comandos comunes que son útiles al trabajar con configuraciones de sitio a sitio. Para hello lista completa de los comandos de red de CLI, consulte [CLI de Azure - red](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Pasos siguientes

* Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.
* Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Para más información acerca de la tunelización forzada, consulte la [información acerca de la tunelización forzada](vpn-gateway-forced-tunneling-rm.md).
* Para obtener información acerca de las conexiones activo/activo de alta disponibilidad, consulte [Conectividad de alta disponibilidad entre locales y de red virtual a red virtual](vpn-gateway-highlyavailable.md).
* Para obtener una lista de comandos de red de la CLI de Azure, consulte [Networking - az network](https://docs.microsoft.com/cli/azure/network) (Redes: az network).