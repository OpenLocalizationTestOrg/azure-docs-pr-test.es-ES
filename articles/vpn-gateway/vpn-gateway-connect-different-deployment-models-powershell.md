---
title: "Conectar redes virtuales clásicas tooAzure VNets el Administrador de recursos: PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión VPN entre clásico redes virtuales y VNets el Administrador de recursos con puerta de enlace VPN y PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>Conexión de redes virtuales a partir de diferentes modelos de implementación con PowerShell



Este artículo muestra cómo tooconnect clásico redes virtuales tooResource Manager VNets tooallow Hola recursos ubicados en hello toocommunicate de modelos de implementación independiente entre sí. pasos de Hello en este artículo usan PowerShell, pero también puede crear esta configuración con hello portal de Azure, seleccione artículo hello en esta lista.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Conectar un tooa de red virtual clásica VNet el Administrador de recursos es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE. Puede crear una conexión entre redes virtuales que estén en diferentes suscripciones y en diferentes regiones. También puede conectar redes virtuales que ya tengan redes locales tooon de conexiones, siempre que sea de puerta de enlace de Hola que les ha configurado dinámica o basadas en enrutamiento. Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo. 

Si sus redes virtuales están en hello misma región, puede que desee tooinstead considerar realizar la conexión con el intercambio de tráfico de red virtual. El emparejamiento de VNET no usa VPN Gateway. Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md). 

## <a name="before-beginning"></a>Antes de comenzar

Hola pasos siguientes le ofrezca Hola configuración necesario tooconfigure una puerta de enlace dinámico o de ruta para cada red virtual y crear una conexión VPN entre puertas de enlace de Hola. Esta configuración no admite puertas de enlace estáticas o basadas en directivas.

### <a name="prerequisites"></a>Requisitos previos

* Se han creado ambas redes virtuales.
* intervalos de direcciones de Hola para hello redes virtuales no se superponen entre sí, ni se superponen con ninguno de los intervalos de Hola para otras conexiones que se pueden conectar las puertas de enlace de Hola a.
* Se ha instalado cmdlets de PowerShell de hello más recientes. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información. Asegúrese de que instalar Service Management (SM) de Hola y Hola cmdlets del Administrador de recursos (RM). 

### <a name="exampleref"></a>Configuración de ejemplo

Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.

**Configuración de redes virtuales clásicas**

Nombre de la red virtual = RedVClásica <br>
Ubicación = Oeste de EE. UU. <br>
Espacios de direcciones de red virtual = 10.0.0.0/24 <br>
Subred-1 = 10.0.0.0/27 <br>
Subred de la puerta de enlace= 10.0.0.32/29 <br>
Nombre de la red local = RedLocalRMV <br>
Tipo de puerta de enlace = EnrutamientoDinámico

**Configuración de redes virtuales de Resource Manager**

Nombre de red virtual = RedRMV <br>
Grupo de recursos = GR1 <br>
Espacios de direcciones IP de red virtual = 192.168.0.0/16 <br>
Subred-1 = 192.168.1.0/24 <br>
Subred de la puerta de enlace = 192.168.0.0/26 <br>
Ubicación = Este de EE. UU. <br>
Nombre IP público de puerta de enlace = pepip <br>
Puerta de enlace de red local = LocalRedVClásica <br>
Nombre de la puerta de enlace de red virtual = PuertaDeEnlaceRM <br>
Configuración de direccionamiento IP de puerta de enlace = configpeip

## <a name="createsmgw"></a>Sección 1: configurar red virtual clásica de Hola
### <a name="part-1---download-your-network-configuration-file"></a>Parte 1: exportación del archivo de configuración de red
1. Inicie sesión en tooyour cuenta de Azure en la consola de PowerShell de hello con derechos elevados. Hello siguiente cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure. Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell. Utilice hello toocomplete de cmdlets de PowerShell de SM esta parte de la configuración de Hola.

  ```powershell
  Add-AzureAccount
  ```
2. Exportar el archivo de configuración de red de Azure ejecutando el siguiente comando de Hola. Puede cambiar la ubicación Hola Hola tooexport tooa diferentes de ubicación de archivos si es necesario.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. Archivo .xml de hello abierto que descargó tooedit lo. Para obtener un ejemplo de archivo de configuración de red de hello, vea hello [esquema de configuración de red](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Parte 2 - Compruebe la subred de puerta de enlace de Hola
Hola **VirtualNetworkSites** elemento, agregue un tooyour de subred de puerta de enlace red virtual si aún no ha creado ninguno. Cuando se trabaja con el archivo de configuración de red de hello, subred de puerta de enlace de hello debe denominarse "GatewaySubnet" o Azure no puede reconocer y utilizarlo como una subred de puerta de enlace.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Ejemplo:**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Parte 3: agregar sitio de red local de Hola
sitio de red local de Hello que agregará representa hello toowhich de red virtual de RM que desee tooconnect. Agregar un **LocalNetworkSites** elemento toohello file si no existe. En este momento en configuración de hello, Hola valor de VPNGatewayAddress puede ser cualquier dirección IP pública válida porque aún no hemos creado la puerta de enlace de Hola para hello VNet el Administrador de recursos. Una vez que se crea la puerta de enlace de hello, reemplazamos esta dirección IP de marcador de posición con hello correcto dirección IP pública que se ha asignado la puerta de enlace de toohello RM.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Parte 4: asocie Hola red virtual con el sitio de red local de Hola
En esta sección, se especifica el sitio de red local de Hola que desea tooconnect Hola VNet a. En este caso, es hello VNet el Administrador de recursos que hace referencia anteriormente. Que los nombres de Hola que coincidan con. En este paso no se crea una puerta de enlace. Especifica la red local de Hola que Hola puerta de enlace se conectará al.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>Parte 5: guardar el archivo hello y cargar
Guardar archivo hello, a continuación, importarlo tooAzure ejecutando el siguiente comando de Hola. Asegúrese de que se cambie la ruta de acceso Hola según sea necesario para su entorno.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Verá un resultado similar que muestra que la importación de Hola se realizó correctamente.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Parte 6: crear puerta de enlace de Hola

Antes de ejecutar este ejemplo, consulte toohello toosee espera que el archivo de configuración de red que ha descargado para nombres de hello exacto que Azure. archivo de configuración de red de Hello contiene valores de hello para las redes virtuales clásicas. A veces los nombres de Hola para clásico en que redes virtuales se cambian en el archivo de configuración de red de hello al crear la configuración de red virtual clásica Hola portal de Azure debido a diferencias de toohello en los modelos de implementación de Hola. Por ejemplo, si ha usado hello Azure portal toocreate una red virtual clásica denominado 'VNet clásico' y creado en un grupo de recursos con el nombre 'ClassicRG', nombre de Hola que se encuentra en el archivo de configuración de red de hello es convertido too'Group red virtual clásica de ClassicRG'. Al especificar el nombre de Hola de una red virtual que contiene espacios, use comillas en el valor de Hola.


Usar hello después toocreate una puerta de enlace de enrutamiento dinámico de ejemplo:

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

Puede comprobar estado de Hola de puerta de enlace de hello mediante hello **Get-AzureVNetGateway** cmdlet.

## <a name="creatermgw"></a>Sección 2: Configurar Hola puerta de enlace de red virtual de RM
toocreate una puerta de enlace VPN para hello RM red virtual, siga Hola siguiendo las instrucciones. No inicie pasos Hola hasta después de que se haya recuperado la dirección IP pública de Hola para puerta de enlace de hello clásico la red virtual. 

1. Inicie sesión en tooyour cuenta de Azure en la consola de PowerShell de Hola. Hello siguiente cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure. Después de iniciar sesión, la configuración de su cuenta se descarga para que estén disponible tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Si tiene más de una suscripción de Azure, obtenga una lista de todas ellas.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Especifique que desea toouse de suscripción de Hola.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Cree una puerta de enlace de red local. En una red virtual, puerta de enlace de red local de hello suele hacer referencia tooyour ubicación. En este caso, puerta de enlace de red local de hello hace referencia tooyour clásico de red virtual. Asígnele un nombre por el que Azure puede hacer referencia tooit y también especificar el prefijo de espacio de dirección de Hola. Azure utiliza el prefijo de dirección IP de hello especificar tooidentify qué tooyour toosend de tráfico ubicación local. Si necesita información de hello tooadjust aquí una versión posterior, antes de crear la puerta de enlace, puede modificar el ejemplo de Hola ejecución y valores de hello.
   
   **-Nombre** es nombre hello desee puerta de enlace de tooassign toorefer toohello red local.<br>
   **-AddressPrefix** es hello espacio de direcciones de la red virtual clásica.<br>
   **-GatewayIpAddress** es la dirección IP pública de Hola de puerta de enlace de hello clásico la red virtual. Asegúrese de ejemplo siguiente de hello toochange se tooreflect Hola dirección IP.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. Solicitar pública IP dirección toobe toohello asignado red virtual puerta de enlace de hello VNet el Administrador de recursos. No se puede especificar la dirección IP de Hola que desee toouse. dirección IP de Hola se asigna dinámicamente toohello puerta de enlace de red virtual. Sin embargo, esto implica cambios en la dirección IP Hola. cambios de dirección IP de puerta de enlace de red virtual de hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear. No cambia en el cambio de tamaño, restablecer o en otras actualizaciones y mantenimiento internos de puerta de enlace de Hola.

  En este paso, también se establece una variable que se utilizará en un paso posterior.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Compruebe que la red virtual tenga una subred de puerta de enlace. Si no existe ninguna subred de puerta de enlace, agregue una. Asegúrese de que se denomina subred de puerta de enlace de hello *GatewaySubnet*.
5. Recuperar la subred de hello usada para la puerta de enlace de hello ejecutando el siguiente comando de Hola. En este paso, también se establece una variable toobe usado en el paso siguiente de saludo.
   
   **-Nombre** es Hola nombre de la VNet del Administrador de recursos.<br>
   **-ResourceGroupName** es grupo de recursos de Hola que hello red virtual está asociado. subred de puerta de enlace de Hello ya debe existir para esta red virtual y debe denominarse *GatewaySubnet* toowork correctamente.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Crear configuración de direcciones IP de puerta de enlace de Hola. configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública. Use Hola ejemplo siguiente se toocreate la configuración de puerta de enlace.

  En este paso, Hola **- SubnetId** y **- PublicIpAddressId** parámetros deben pasarse propiedad de Id. de Hola de subred de Hola y objetos de dirección IP, respectivamente. No puede usar una cadena sencilla. Estas variables se establecen en hello paso toorequest una IP pública y Hola paso tooretrieve Hola subred.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Crear puerta de enlace de red virtual de administrador de recursos de hello ejecutando el siguiente comando de Hola. Hola `-VpnType` debe ser *RouteBased*. Puede tardar 45 minutos o más en hello toocreate de puerta de enlace.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Copie la dirección IP pública Hola una vez creada la puerta de enlace VPN de Hola. Se usa cuando configure los parámetros de la red virtual clásica Hola red local. Puede usar Hola siguiente cmdlet tooretrieve Hola la dirección IP pública. Hello dirección IP pública aparece en hello devuelto como *IpAddress*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>Sección 3: Modificar la configuración del sitio local de red virtual clásica de Hola

En esta sección, se trabaja con hello clásico red virtual. Reemplace la dirección IP de marcador de posición de Hola que usó al especificar la configuración de sitio local de Hola que será usado tooconnect toohello puerta de enlace de VNet Administrador de recursos. 

1. Exportar archivo de configuración de red de Hola.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Con un editor de texto, modifique el valor de hello para el valor de VPNGatewayAddress. Reemplace la dirección IP de marcador de posición de hello con dirección IP pública de Hola de puerta de enlace de administrador de recursos de hello y, a continuación, guarde los cambios de Hola.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. Hola de importación modificado tooAzure de archivo de configuración de red.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>Sección 4: Crear una conexión entre las puertas de enlace de Hola
Crear una conexión entre las puertas de enlace de hello requiere PowerShell. Puede que necesite tooadd la versión clásica de cuenta de Azure toouse Hola Hola de cmdlets de PowerShell. por lo tanto, use toodo **Add-AzureAccount**.

1. En la consola de PowerShell de hello, establezca la clave compartida. Antes de ejecutar los cmdlets de hello, consulte toohello toosee espera que el archivo de configuración de red que ha descargado para nombres de hello exacto que Azure. Al especificar el nombre de Hola de una red virtual que contiene espacios, use comillas simples en el valor de Hola.<br><br>En el ejemplo siguiente, **- VNetName** es nombre Hola de hello VNet clásico y **- LocalNetworkSiteName** es nombre hello que especificó para el sitio de red local de Hola. Hola **- SharedKey** es un valor que se generan y se especifica. En el ejemplo de Hola, hemos usado "abc123", pero puede generar y utilizar algo más complejo. Hola importante que es ese valor de Hola que especifique aquí debe ser Hola que mismo valor que especifique en el paso siguiente de hello al crear la conexión. Hola devuelto debería mostrar **estado: correcto**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Crear la conexión de VPN de hello ejecutando Hola siguientes comandos:
   
  Establecer variables de Hola.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Crear conexiones de Hola. Tenga en cuenta que hello **- ConnectionType** es IPsec, no Vnet2Vnet.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Sección 5: comprobación de las conexiones

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>conexión de hello tooverify desde su tooyour clásico de red virtual VNet el Administrador de recursos

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Azure Portal

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>conexión de hello tooverify desde el Administrador de recursos VNet tooyour red virtual clásica

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Azure Portal

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>P+F sobre conexiones de red virtual a red virtual

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

