---
title: "Configuración de conexiones de ExpressRoute y VPN de sitio a sitio coexistentes: modelo de implementación clásica: Azure | Microsoft Docs"
description: "Este artículo le guiará a través de configuración de una conexión VPN de sitio a sitio que puede coexistir para el modelo de implementación clásica de Hola y ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Configuración de conexiones de ExpressRoute y de sitio a sitio coexistentes (modelo de implementación clásica)
> [!div class="op_single_selector"]
> * [PowerShell: administrador de recursos](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell: clásico](expressroute-howto-coexist-classic.md)
> 
> 

Tener capacidad de hello tooconfigure VPN de sitio a sitio y ExpressRoute tiene varias ventajas. Puede configurar VPN de sitio a sitio como una ruta de acceso seguro de conmutación por error para ExressRoute o usar VPN de sitio a sitio tooconnect toosites que no están conectados a través de ExpressRoute. Trataremos Hola pasos tooconfigure ambos escenarios en este artículo. En este artículo se aplica a modelos de implementación clásica de toohello. Esta configuración no está disponible en el portal de Hola.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Información sobre los modelos de implementación de Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> Circuitos ExpressRoute deben configurarse previamente antes de seguir estas instrucciones Hola. Asegúrese de que ha seguido las guías de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y [configurar el enrutamiento de](expressroute-howto-routing-classic.md) antes de seguir estos pasos Hola.
> 
> 

## <a name="limits-and-limitations"></a>Límites y limitaciones
* **No se admite el enrutamiento transitorio.** No se puede realizar un enrutamiento (a través de Azure) entre una red local conectada a través de una VPN sitio a sitio y una red local conectada a través de ExpressRoute.
* **No se admite el punto a sitio.** No se puede habilitar point-to-site VPN conexiones toohello misma red virtual que está conectado tooExpressRoute. Point-to-site VPN y ExpressRoute no pueden coexistir para hello misma red virtual.
* **No se puede habilitar la tunelización forzada en la puerta de enlace VPN de sitio a sitio de Hola.** Solo puede "forzar" todo vinculado a Internet tráfico tooyour back-local de red a través de ExpressRoute.
* **No se admite la puerta de enlace de la SKU de nivel Básico.** Debe usar una puerta de enlace básico SKU que no sea para ambos hello [puerta de enlace ExpressRoute](expressroute-about-virtual-network-gateways.md) hello y [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Solo se admite la VPN Gateway basada en rutas.** Debe usar una [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) basada en rutas.
* **Se debe configurar una ruta estática para VPN Gateway.** Si la red local está conectado tooboth ExpressRoute y un sitio a sitio VPN, debe tener una ruta estática configurada en su toohello de conexión de red local tooroute Hola sitio a sitio VPN Internet pública.
* **Primero debe configurarse la puerta de enlace de ExpressRoute.** Debe crear puerta de enlace de ExpressRoute de hello primero antes de agregar la puerta de enlace VPN de sitio a sitio de Hola.

## <a name="configuration-designs"></a>Diseños de configuración
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configuración de una VPN de sitio a sitio como una ruta de acceso de conmutación por error para ExpressRoute
Puede configurar una conexión VPN de sitio a sitio como una copia de seguridad para ExpressRoute. Esto aplica solo toovirtual redes vinculado toohello Azure ruta privada de intercambio de tráfico. No hay ninguna solución de conmutación por error basada en VPN para servicios accesibles a través de emparejamientos de Microsoft y públicos de Azure. Hola circuito de ExpressRoute no distingue vínculo principal Hola. Datos fluirá a través de la ruta de acceso VPN de sitio a sitio Hola solo si se produce un error en hello circuito de ExpressRoute. 

> [!NOTE]
> Mientras se prefiere circuito de ExpressRoute a través de VPN de sitio a sitio cuando ambas rutas se Hola igual, Azure utilizará ruta de hello más larga prefijo coincidencia toochoose Hola hacia el destino del paquete de saludo.
> 
> 

![Coexistencia](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurar una toosites de tooconnect VPN de sitio a sitio no está conectado a través de ExpressRoute
Puede configurar la red donde algunos sitios conectan directamente tooAzure a través de VPN de sitio a sitio y algunos de los sitios a través de ExpressRoute. 

![Coexistencia](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> No se puede configurar una red virtual como un enrutador de tránsito.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Seleccionar Hola pasos toouse
Hay dos conjuntos diferentes de toochoose de procedimientos de en las conexiones de tooconfigure de orden que pueden coexistir. procedimiento de configuración de Hola que seleccione dependerá de si tiene una red virtual existente que desea tooconnect a, o desea toocreate una nueva red virtual.

* No tiene una red virtual y necesita toocreate uno.
  
    Si ya no tiene una red virtual, este procedimiento le guiará a través de la creación de una nueva red virtual mediante el modelo de implementación clásica de Hola y para crear nuevas conexiones de VPN de sitio a sitio y de ExpressRoute. tooconfigure, siga los pasos en la sección del artículo Hola Hola [toocreate una nueva red virtual y las conexiones coexistentes](#new).
* Ya tengo una red virtual con el modelo de implementación clásico.
  
    Puede que ya tenga una red virtual con una conexión VPN de sitio a sitio o una conexión ExpressRoute existentes. Hola sección artículo [tooconfigure coexsiting conexiones para una red virtual existente ya](#add) le guiará a través de la eliminación de puerta de enlace de hello y, a continuación, crear nuevas conexiones de ExpressRoute y VPN de sitio a sitio. Tenga en cuenta que al crear nuevas conexiones de hello, pasos de hello deben realizarse en un orden muy específico. No utilice instrucciones de hello en otro artículos toocreate sus conexiones y las puertas de enlace.
  
    En este procedimiento, creación de conexiones que pueden coexistir necesitarán toodelete la puerta de enlace y, a continuación, configurar nuevas puertas de enlace. Esto significa que tendrá tiempo de inactividad para las conexiones entre entornos al eliminar y volver a crear la puerta de enlace y las conexiones, pero no tendrá que toomigrate cualquiera de su máquinas virtuales o servicios tooa nueva red virtual. Las máquinas virtuales y servicios se seguirán toocommunicate capaz de salida a través del equilibrador de carga de hello al configurar la puerta de enlace si están toodo configurado así.

## <a name="new"></a>toocreate una nueva red virtual y las conexiones coexistentes
Este procedimiento le guiará en la creación de una red virtual y conexiones de sitio a sitio y ExpressRoute que coexistirán.

1. Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell de Azure. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola. Tenga en cuenta que los cmdlets de Hola que va a utilizar para esta configuración puede ser ligeramente diferentes de lo que es posible que esté familiarizado con. Cmdlets de hello toouse seguro especificar en estas instrucciones. 
2. Cree un esquema para la red virtual. Para obtener más información acerca del esquema de configuración de hello, consulte [esquema de configuración de red Virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    Cuando se crea el esquema, asegúrese de que utilizar Hola siguientes valores:
   
   * subred de puerta de enlace de Hello para la red virtual de hello debe ser /27 o un prefijo más corto (por ejemplo, /26 o /25).
   * tipo de conexión de puerta de enlace de Hola "dedicado".
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. Después de crear y configurar el archivo de esquema xml, cargar archivo hello. Esto creará la red virtual.
   
    Usar hello siguiente cmdlet tooupload el archivo, reemplazando el valor de Hola por los suyos propios.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>Cree una puerta de enlace de ExpressRoute. Ser seguro toospecify Hola GatewaySKU como *estándar*, *HighPerformance*, o *UltraPerformance* y Hola el GatewayType como *DynamicRouting*.
   
    Usar hello según muestra, sustituyendo los valores de hello para su propio.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Vínculo de circuito de ExpressRoute de toohello de puerta de enlace de ExpressRoute de Hola. Una vez completado este paso, se establece la conexión de hello entre la red local y Azure, a través de ExpressRoute.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>A continuación, cree la puerta de enlace de la VPN de sitio a sitio. Hello GatewaySKU debe ser *estándar*, *HighPerformance*, o *UltraPerformance* y hello el GatewayType debe ser *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    configuración de puerta de enlace de red virtual de hello tooretrieve, incluidos los Id. de puerta de enlace de Hola y Hola IP pública, usa hello `Get-AzureVirtualNetworkGateway` cmdlet.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Cree una entidad de puerta de enlace de VPN de sitio local. Este comando no configura la puerta de enlace de VPN local. En su lugar, permite a tooprovide la configuración de puerta de enlace local hello, como la dirección IP pública de Hola y Hola local espacio de direcciones, por lo que hello puerta de enlace VPN de Azure puede conectarse tooit.
   
   > [!IMPORTANT]
   > sitio local Hola Hola VPN de sitio a sitio no está definido en hello netcfg. En su lugar, debe usar estos parámetros de cmdlet toospecify Hola sitio local. No se puede definir mediante el portal o archivo de netcfg Hola.
   > 
   > 
   
    Usar hello según muestra, reemplazar valores de hello por los suyos propios.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Si la red local tiene varias rutas, puede pasar todas ellas en una matriz.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    configuración de puerta de enlace de red virtual de hello tooretrieve, incluidos los Id. de puerta de enlace de Hola y Hola IP pública, usa hello `Get-AzureVirtualNetworkGateway` cmdlet. Vea el siguiente ejemplo de Hola.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Configurar la VPN dispositivo tooconnect toohello nueva puerta de enlace local. Utilice la información de Hola que recuperó en el paso 6 al configurar el dispositivo VPN. Para obtener más información sobre la configuración del dispositivo VPN, vea [Configuración de dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
2. Vínculo Hola VPN de sitio a sitio puerta de enlace en Azure toohello puerta de enlace local.
   
    En este ejemplo, connectedEntityId es el Id. de puerta de enlace local de hello, que puede encontrar mediante la ejecución de `Get-AzureLocalNetworkGateway`. También puede encontrar virtualNetworkGatewayId mediante hello `Get-AzureVirtualNetworkGateway` cmdlet. Después de este paso, se establece la conexión de hello entre la red local y Azure a través de hello conexión VPN de sitio a sitio.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>tooconfigure coexsiting conexiones para una red virtual existente
Si tiene una red virtual existente, compruebe el tamaño de subred de puerta de enlace de Hola. Si está en la subred de puerta de enlace de hello /28 o /29, primero debe eliminar la puerta de enlace de red virtual de Hola y aumentar el tamaño de subred de puerta de enlace de Hola. Hello pasos de esta sección le mostrará cómo toodo que.

Si está de subred de puerta de enlace de hello /27 o superior y red virtual de hello está conectado a través de ExpressRoute, puede omitir estos pasos hello y continuar demasiado["Paso 6: crear una puerta de enlace VPN de sitio a sitio"](#vpngw) en la sección anterior de Hola.

> [!NOTE]
> Cuando se elimina la puerta de enlace existente hello, sus instalaciones locales perderá red virtual de hello conexión tooyour mientras se trabaja con esta configuración.
> 
> 

1. Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell del Administrador de recursos de Azure. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola. Tenga en cuenta que los cmdlets de Hola que va a utilizar para esta configuración puede ser ligeramente diferentes de lo que es posible que esté familiarizado con. Cmdlets de hello toouse seguro especificar en estas instrucciones. 
2. Eliminar Hola VPN de sitio a sitio o ExpressRoute puerta de enlace existente. Usar hello siguiente cmdlet, reemplazando los valores de hello con sus propios.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Exportar el esquema de la red virtual de Hola. Usar hello siguiente cmdlet de PowerShell, reemplazar valores de hello por los suyos propios.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Editar el esquema de archivo de configuración de red de Hola para que la subred de puerta de enlace de hello es /27 o un prefijo más corto (por ejemplo, /26 o /25). Vea el siguiente ejemplo de Hola. 
   
   > [!NOTE]
   > Si no tiene suficientes direcciones IP que se mantienen en el tamaño de subred de puerta de enlace de red virtual tooincrease hello, deberá tooadd más espacio de direcciones IP. Para obtener más información acerca del esquema de configuración de hello, consulte [esquema de configuración de red Virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Si la puerta de enlace anterior era una VPN de sitio a sitio, también debe cambiar el tipo de conexión de hello demasiado**dedicado**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. Ya tiene una red virtual sin puertas de enlace. toocreate nuevas puertas de enlace y completar las conexiones, puede continuar con la [paso 4: crear una puerta de enlace de ExpressRoute](#gw), que se encuentra en hello anterior conjunto de pasos.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md)

