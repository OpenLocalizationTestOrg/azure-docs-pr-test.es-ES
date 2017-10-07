---
title: "Configuración de la tunelización forzada para conexiones de sitio a sitio de Azure: modelo clásico | Microsoft Docs"
description: "Cómo tooredirect o 'force' todos los tooyour de espera de tráfico de vinculado a Internet en ubicación y local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Configurar la tunelización forzada mediante modelo de implementación clásica de Hola

Forzada permite redirigir o "forzar" todos los vinculado a Internet tráfico tooyour back-ubicación de local a través de un túnel VPN de sitio a sitio para inspección y auditoría de túnel. Se trata de un requisito de seguridad crítico en la mayoría de las directivas de las empresas de TI. Sin la tunelización forzada, tráfico de Internet desde las máquinas virtuales en Azure atravesará siempre desde la infraestructura de red de Azure directamente out toohello Internet, sin Hola opción tooallow se tooinspect o auditoría tráfico Hola. Acceso de Internet no autorizado puede provocar potencialmente la divulgación de tooinformation u otros tipos de infracciones de seguridad.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Este artículo le guiará a través de configuración forzada de túnel para redes virtuales creadas mediante el modelo de implementación clásica de Hola. La tunelización forzada puede configurarse mediante el uso de PowerShell, no a través del portal de Hola. Si desea tooconfigure tunelización para modelo de implementación del Administrador de recursos de hello forzada, seleccione artículo clásico de hello después de la lista desplegable:

> [!div class="op_single_selector"]
> * [PowerShell: clásico](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell: administrador de recursos](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Requisitos y consideraciones
La tunelización forzada en Azure se configura a través de rutas definidas por el usuario (UDR) de redes virtuales. Redirigir el tráfico tooan local de sitio se expresa como una puerta de enlace de VPN de Azure de toohello de ruta predeterminada. Hello siguiente sección enumeran hello las limitaciones actuales de la tabla de enrutamiento de Hola y rutas para una red Virtual de Azure:

* Cada subred de la red virtual tiene una tabla de enrutamiento del sistema integrada. tabla de enrutamiento de sistema de Hello tiene Hola los tres grupos de rutas siguientes:

  * **Las rutas de red virtual locales:** directamente toohello máquinas virtuales de destino en hello misma red virtual.
  * **Rutas locales:** toohello puerta de enlace de VPN de Azure.
  * **Ruta predeterminada:** toohello directamente Internet. Los paquetes destinados toohello las direcciones IP privadas no cubiertas por las rutas de hello dos anteriores que se van a quitar.
* Con la versión de Hola de rutas definidas por el usuario, puede crear un tooadd de tabla de enrutamiento una ruta predeterminada y, a continuación, asociar Hola enrutamiento tabla tooyour red virtual subredes tooenable forzado túnel en esas subredes.
* Deberá tooset un sitio denominado"predeterminado" entre la red virtual de hello entre entornos sitios locales toohello conectado.
* La tunelización forzada debe asociarse a una red virtual que tiene una puerta de enlace de VPN de enrutamiento dinámico (no una puerta de enlace estática).
* La tunelización forzada de ExpressRoute no se configura mediante este mecanismo, pero en su lugar, se habilita de forma anunciando una ruta predeterminada a través de hello BGP de ExpressRoute sesiones de emparejamiento. Vea hello [documentación de ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) para obtener más información.

## <a name="configuration-overview"></a>Información general sobre la configuración
En el siguiente ejemplo de Hola Hola front-end no se fuerza la subred de túnel. las cargas de trabajo de Hello en la subred de front-end de hello pueden continuar tooaccept y responder las solicitudes de toocustomer de hello Internet directamente. Hello subredes de nivel intermedio y back-end se convierten obligatoriamente túnel. Las conexiones de salida de estos toohello dos subredes Internet será tooan forzado o redirigida volver al sitio local a través de una de hello que túneles VPN S2S.

Esto le permite toorestrict e inspeccionar el acceso a Internet desde las máquinas virtuales o servicios de nube de Azure, mientras continúa tooenable su arquitectura de servicio de varios niveles necesaria. También puede aplicar forzada túnel toohello todo redes virtuales si no hay ningún cargas de trabajo orientado a Internet en las redes virtuales.

![Tunelización forzada](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Antes de empezar
Compruebe que dispone de hello siguientes elementos antes de empezar la configuración.

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Una red virtual configurada. 
* versión más reciente de Hola de hello cmdlets de PowerShell de Azure. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.

## <a name="configure-forced-tunneling"></a>Configuración de la tunelización forzada
Hola procedimiento le ayudará a especificar la tunelización forzada de una red virtual. pasos de configuración de Hello corresponden toohello archivo de configuración de red de red virtual.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

En este ejemplo, la red virtual de hello 'Red virtual de varios niveles' no tiene tres subredes: subredes 'Front-end', 'Nivel intermedio' y "Back-end", con las conexiones locales de entre cuatro: 'DefaultSiteHQ' y tres bifurcaciones. 

pasos de Hello establecer hello 'DefaultSiteHQ' como conexión de sitio predeterminado de hello para el túnel forzado y configurar Hola nivel intermedio y back-end subredes toouse tunelización forzada.

1. Cree una tabla de enrutamiento. Usar hello siguiente cmdlet toocreate su tabla de rutas.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Agregar una tabla de enrutamiento de toohello de ruta predeterminada. 

  Hello en el ejemplo siguiente se agrega una ruta toohello tabla de enrutamiento predeterminada creada en el paso 1. Tenga en cuenta que solo se admite la ruta de Hola es el prefijo de destino de Hola de toohello "0.0.0.0/0" salto "VPNGateway".

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Asociar subredes de hello enrutamiento tabla toohello. 

  Después de una tabla de enrutamiento se crea y agrega una ruta, use después tooadd de ejemplo de Hola o asociar la subred de red virtual de hello ruta tabla tooa. ejemplo de Hola agrega Hola ruta tabla "MyRouteTable" toohello nivel intermedio y back-end subredes de varios niveles de VNet a VNet.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Asigne un sitio predeterminado para la tunelización forzada. 

  Hola anterior paso, scripts de cmdlet de ejemplo de Hola crean la tabla de enrutamiento de Hola y asociadas hello tootwo de tabla de ruta de subredes de red virtual de Hola. paso restante de Hello es tooselect un sitio local entre las conexiones de varios sitios de Hola de red virtual de hello como sitio predeterminado de Hola o de túnel.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Cmdlets de PowerShell adicionales
### <a name="toodelete-a-route-table"></a>toodelete una tabla de rutas

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist una tabla de rutas

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete una ruta de una tabla de rutas

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove una ruta de subred

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>tabla de rutas de hello toolist asociada a una subred

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove un sitio predeterminado de una puerta de enlace de VPN de VNet

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```