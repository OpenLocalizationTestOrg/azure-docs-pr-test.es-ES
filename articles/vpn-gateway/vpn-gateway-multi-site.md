---
title: "Conectarse a un sitio de sitios de red virtual toomultiple con puerta de enlace VPN y PowerShell: clásico | Documentos de Microsoft"
description: "En este artículo le guiará a través de conectar varias instalaciones locales sitios tooa red virtual con una puerta de enlace de VPN para el modelo de implementación clásica de Hola."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Agregar una tooa de conexión de sitio a sitio red virtual con una conexión de puerta de enlace VPN existente (clásica)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (clásico)](vpn-gateway-multi-site.md)
>
>

Este artículo le guiará a través mediante PowerShell tooadd sitio a sitio (S2S) conexiones tooa puerta de enlace VPN que tiene una conexión existente. Este tipo de conexión es a menudo tooas que se hace referencia una configuración de "varios sitio". Hello pasos descritos en este artículo aplican redes toovirtual creadas mediante el modelo de implementación clásica de hello (también conocido como administración de servicios). Estos pasos no aplican las configuraciones de conexión coexistentes tooExpressRoute/sitio a sitio.

### <a name="deployment-models-and-methods"></a>Modelos de implementación y métodos

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Esta tabla se actualiza cada vez que hay nuevos artículos y nuevas herramientas disponibles para esta configuración. Cuando un artículo está disponible, vinculamos directamente tooit de esta tabla.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>Acerca de la conexión

Puede conectar varios sitios tooa único virtual red local. Esto resulta especialmente atractivo para crear soluciones híbridas en la nube. Crear una puerta de enlace de red virtual de Azure de conexión de varios sitios tooyour es toocreating similar otras conexiones de sitio a sitio. De hecho, puede usar una puerta de enlace de VPN de Azure existente, como puerta de enlace de hello es dinámico (basado en ruta).

Si ya tiene una red virtual de puerta de enlace estática tooyour conectado, puede cambiar toodynamic de tipo de puerta de enlace de hello sin necesidad de red virtual de toorebuild hello en varios sitios de orden tooaccommodate. Antes de cambiar el tipo de enrutamiento de hello, asegúrese de que la puerta de enlace VPN local admite configuraciones de VPN basadas en enrutamiento.

![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")

## <a name="points-tooconsider"></a>Puntos tooconsider

**No será la red virtual de toouse capaz de hello toomake portal cambios toothis.** Necesita el archivo de configuración de red toomake cambios toohello en lugar de usar el portal de Hola. Si realiza cambios en el portal de hello, sobrescribirán la configuración de referencia de varios sitios para esta red virtual.

Deben sentirse cómodos utilizando el archivo de configuración de red de Hola por tiempo Hola ha completado procedimiento de varios sitios de Hola. Sin embargo, si hay varias personas trabajando en la configuración de red, necesitará toomake seguro de que todas conocen esta limitación. Esto no significa que no puede usar el portal de hello en absoluto. Puede utilizarlo para todo lo demás, excepto que realiza la red virtual concreto de toothis de cambios configuración.

## <a name="before-you-begin"></a>Antes de empezar

Antes de comenzar, compruebe que dispone de los siguientes hello:

* Hardware VPN compatible para cada ubicación local. Comprobar [acerca de los dispositivos VPN para la conectividad de red Virtual](vpn-gateway-about-vpn-devices.md) tooverify si el dispositivo de Hola que desea toouse es algo que se conoce toobe compatible.
* Una dirección IP IPv4 pública orientada externamente para cada dispositivo VPN. dirección IP de Hello no puede estar situado detrás de un dispositivo NAT. Esto es un requisito.
* Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell de Azure. Asegúrese de que instalar versión de Service Management (SM) de hello en la versión de administrador de recursos de toohello de adición. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información.
* Alguna persona con experiencia en configuración de hardware de VPN Tendrá toohave una comprensión segura del cómo tooconfigure su dispositivo VPN o trabajar con alguien que lo tiene.
* intervalos de direcciones IP de Hola que quiere toouse de la red virtual (si ya no ha creado una).
* intervalos de direcciones IP de Hola para cada uno de los sitios de red local de Hola que se va a conectar. Necesitará toomake seguro de que intervalos de direcciones IP de Hola para cada uno de los sitios de red local de Hola que desea tooconnect toodo no se superponen. En caso contrario, el portal de Hola o hello API de REST rechazará configuración Hola que se va a cargar.<br>Por ejemplo, si tiene dos sitios de red local que ambos contienen Hola IP dirección intervalo 10.2.3.0/24 y tiene un paquete con una dirección de destino 10.2.3.3, Azure no sabría qué sitio va intervalos de direcciones de toosend Hola paquete toobecause Hola son que se superponen. problemas de enrutamiento tooprevent, Azure no permite tooupload un archivo de configuración que tiene intervalos solapados.

## <a name="1-create-a-site-to-site-vpn"></a>1. Crear una VPN de sitio a sitio
Si ya tiene una VPN de sitio a sitio con una puerta de enlace de enrutamiento dinámico, perfecto. Puede continuar demasiado[exportar opciones de configuración de red virtual de hello](#export). Si no es así, Hola siguientes:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Si ya dispone de una red virtual de sitio a sitio, pero con una puerta de enlace de enrutamiento estático (basada en directivas):
1. Cambiar el enrutamiento de toodynamic de tipo de puerta de enlace. Una VPN de varios sitios requiere una puerta de enlace de enrutamiento dinámico (también denominada basada en ruta). tipo de la puerta de enlace de toochange, es necesita puerta de enlace de toofirst delete Hola existente y crear uno nuevo. Para obtener instrucciones, consulte [cómo toochange Hola tipo de enrutamiento de VPN para la puerta de enlace](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Configure la nueva puerta de enlace y cree un túnel de VPN. Para obtener instrucciones, consulte [configurar una puerta de enlace de VPN en el Portal de Azure clásico hello](vpn-gateway-configure-vpn-gateway-mp.md). En primer lugar, cambie la ruta de toodynamic de tipo de puerta de enlace.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Si no dispone de una red virtual de sitio a sitio:
1. Crear la red virtual de sitio a sitio usando estas instrucciones: [crear una red Virtual con una conexión de VPN de sitio a sitio en el Portal de Azure clásico hello](vpn-gateway-site-to-site-create.md).  
2. Configure una puerta de enlace de enrutamiento dinámico con estas instrucciones: [Configuración de una VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md). Ser seguro tooselect **enrutamiento dinámico** para el tipo de puerta de enlace.

## <a name="export"></a>2. Exportar archivo de configuración de red de Hola
Exportar el archivo de configuración de red de Azure ejecutando el siguiente comando de Hola. Puede cambiar la ubicación Hola Hola tooexport tooa diferentes de ubicación de archivos si es necesario.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Archivo de configuración de red de hello abierto
Abra el archivo de configuración de red de Hola que descargó en el último paso de Hola. Use el editor xml que desee. archivo de Hello debería ser similar siguiente toohello:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Agregar referencias de varios sitios
Al agregar o quitar información de referencia de sitio, podrá realizar cambios de configuración toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef. Agregando una nueva referencia de sitio local desencadena un nuevo túnel toocreate de Azure. En el siguiente ejemplo de Hola, configuración de red de hello es para una conexión de sitio único. Guardar archivo hello cuando haya terminado de realizar los cambios.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

tooadd referencias a sitios adicionales (crear una configuración de varios sitio), basta con agregar líneas de "LocalNetworkSiteRef" adicionales, como se muestra en el ejemplo de Hola siguiente:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Importar archivo de configuración de red de Hola
Importar archivo de configuración de red de Hola. Al importar este archivo con cambios de hello, se agregarán nuevos túneles de Hola. túneles de Hello usará Hola puerta de enlace dinámico que creó anteriormente. Puede usar portal clásico de Hola o archivo de hello tooimport de PowerShell.

## <a name="6-download-keys"></a>6. Descargar las claves
Una vez que se han agregado los túneles nuevos, use Hola PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Hola claves IPsec/IKE compartidas previamente para cada túnel.

Por ejemplo:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

Si lo prefiere, también puede usar hello *Get Virtual Network Gateway Shared Key* tooget de API de REST Hola claves previamente compartidas.

## <a name="7-verify-your-connections"></a>7. Comprobación de las conexiones
Comprobar estado de túnel de varios sitios de Hola. Después de descargar las claves de Hola para cada túnel, le interesará tooverify conexiones. Utilice tooget 'Get-AzureVnetConnection' túnel de una lista de red virtual, como se muestra en el siguiente ejemplo de Hola. VNet1 es nombre Hola de hello red virtual.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Valor devuelto del ejemplo:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de las puertas de enlace de VPN, consulte [acerca de puertas de enlace VPN](vpn-gateway-about-vpngateways.md).
