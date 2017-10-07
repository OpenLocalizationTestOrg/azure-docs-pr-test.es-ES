---
title: "¿Cómo tooconfigure enrutamiento (emparejamiento) por un circuito ExpressRoute: el Administrador de recursos: PowerShell: Azure | Documentos de Microsoft"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionamiento Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Creación y modificación del emparejamiento de un circuito ExpressRoute mediante PowerShell

En este artículo le ayuda a crear y administrar la configuración de enrutamiento para un circuito ExpressRoute en modelo de implementación de administrador de recursos de hello mediante PowerShell. También puede comprobar el estado de hello, update o delete y desaprovisionar los emparejamientos de un circuito de ExpressRoute. Si desea toouse una toowork otro método con el circuito, seleccione un artículo de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI de Azure](howto-routing-cli.md)
> * [Vídeo: pares privados](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo: pares públicos](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo: emparejamiento de Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Requisitos previos de configuración

* Necesitará la versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). 
* Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) página hello [requisitos de enrutamiento](expressroute-routing.md) hello y página [flujos de trabajo](expressroute-workflows.md) página antes de comenzar la configuración.
* Tiene que tener un circuito ExpressRoute activo. Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar. Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para usted toobe toorun capaz de hello cmdlets en este artículo.

Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.

> [!IMPORTANT]
> Se actualmente no se publica emparejamientos configurados por los proveedores de servicios a través del portal de administración de servicios de Hola. Se está trabajando para habilitar esta funcionalidad pronto. Antes de configurar los emparejamientos BGP, realice las comprobaciones pertinentes con su proveedor de servicios.
> 
> 

Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute. Puede establecer las configuraciones entre pares en cualquier orden. Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez. 

## <a name="azure-private-peering"></a>Configuración entre pares privados de Azure

En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate emparejamiento privado de Azure

1. Importe el módulo de PowerShell de Hola para ExpressRoute.

  Debe instalar Hola installer más reciente de PowerShell de [Galería de PowerShell](http://www.powershellgallery.com/) e importar módulos de Azure Resource Manager hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola. Necesitará toorun PowerShell como administrador.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Importar todos los módulos de AzureRM.* hello en hello conocida el intervalo de versiones semántico de.

  ```powershell
  Import-AzureRM
  ```

  También puede importar un módulo seleccione dentro de hello conocida el intervalo de versiones semántico.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Inicie sesión en la cuenta de tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Seleccione la suscripción de hello desea toocreate circuito de ExpressRoute.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Crear un circuito ExpressRoute.

  Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-arm.md) y hacer que se aprovisiona proveedor de conectividad de Hola.

  Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.
3. Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado. Utilice el siguiente ejemplo de Hola:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  respuesta de Hello es similar toohello siguiente ejemplo:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurar Azure intercambio de tráfico privado para el circuito de Hola. Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:

  * / 30 subred para el vínculo principal Hola. subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.
  * / 30 subred para el vínculo secundario Hola. subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS. Puede usar un número AS privado para esta configuración entre pares. Asegúrese de que no usa 65515.
  * **Opcional:** un hash MD5 si elige toouse uno.

  Usar hello después tooconfigure Azure privada de emparejamiento para el circuito de ejemplo:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Si elige toouse un hash MD5, use Hola siguiente ejemplo:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview privada emparejamiento detalles de Azure

Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuración de emparejamiento privada de Azure

Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola. En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too500 100.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete emparejamiento privado de Azure

Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:

> [!WARNING]
> También debe asegurarse de que todas las redes virtuales se desvincula de hello circuito de ExpressRoute antes de ejecutar este ejemplo. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Configuración entre pares públicos de Azure

En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate pares públicos de Azure

1. Importe el módulo de PowerShell de Hola para ExpressRoute.

  Debe instalar Hola installer más reciente de PowerShell de [Galería de PowerShell](http://www.powershellgallery.com/) e importar módulos de Azure Resource Manager hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola. Necesitará toorun PowerShell como administrador.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Importar todos los módulos de AzureRM.* hello en hello conocida el intervalo de versiones semántico de.

  ```powershell
  Import-AzureRM
  ```

  También puede importar un módulo seleccione dentro de hello conocida el intervalo de versiones semántico.

  ```powershell
  Import-Module AzureRM.Network
```

  Inicie sesión en la cuenta de tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Seleccione la suscripción de hello desea toocreate circuito de ExpressRoute.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Crear un circuito ExpressRoute.

  Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-arm.md) y hacer que se aprovisiona proveedor de conectividad de Hola.

  Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.
3. Compruebe tooensure de circuito de ExpressRoute Hola está aprovisionado y también está habilitado. Utilice el siguiente ejemplo de Hola:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  respuesta de Hello es similar toohello siguiente ejemplo:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configure pares públicos de Azure para el circuito de Hola. Asegúrese de que dispone de hello siguiente información antes de continuar.

  * / 30 subred para el vínculo principal Hola. Tiene que ser un prefijo IPv4 público válido.
  * / 30 subred para el vínculo secundario Hola. Tiene que ser un prefijo IPv4 público válido.
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
  * **Opcional:** un hash MD5 si elige toouse uno.

  Ejecute hello siguiendo el ejemplo tooconfigure pública de emparejamiento para el circuito de Azure

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Si elige toouse un hash MD5, use Hola siguiente ejemplo:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview Azure pública emparejamiento detalles

Puede obtener detalles de configuración mediante Hola siguiente cmdlet:

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuración de interconexión pública de Azure

Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola. En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too600 200.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete pares públicos de Azure

Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Emparejamiento de Microsoft

En esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute.

> [!IMPORTANT]
> Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft hello, incluso si no se definen los filtros de ruta. Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito. Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>emparejamiento de Microsoft toocreate

1. Importe el módulo de PowerShell de Hola para ExpressRoute.

  Debe instalar Hola installer más reciente de PowerShell de [Galería de PowerShell](http://www.powershellgallery.com/) e importar módulos de Azure Resource Manager hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola. Necesitará toorun PowerShell como administrador.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Importar todos los módulos de AzureRM.* hello en hello conocida el intervalo de versiones semántico de.

  ```powershell
  Import-AzureRM
  ```

  También puede importar un módulo seleccione dentro de hello conocida el intervalo de versiones semántico.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Inicie sesión en la cuenta de tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Seleccione la suscripción de hello desea toocreate circuito de ExpressRoute.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Crear un circuito ExpressRoute.

  Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-arm.md) y hacer que se aprovisiona proveedor de conectividad de Hola.

  Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.
3. Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado. Utilice el siguiente ejemplo de Hola:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  respuesta de Hello es similar toohello siguiente ejemplo:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurar Microsoft emparejamiento para el circuito de Hola. Asegúrese de que haya Hola siguiente información antes de continuar.

  * / 30 subred para el vínculo principal Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
  * / 30 subred para el vínculo secundario Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
  * Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola. Se aceptan solo prefijos de direcciones IP públicas. Si tiene previsto toosend un conjunto de prefijos, puede enviar una lista separada por comas. Estos prefijos deben ser tooyou registrado en un RIR / IRR.
  * **Opcional:** cliente ASN: si es que los prefijos de publicidad que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich están registrados.
  * Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.
  * **Opcional:** un hash MD5 si elige toouse uno.

   Usar hello siguiendo la emparejamiento de Microsoft tooconfigure de ejemplo para el circuito:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>detalles de emparejamiento de Microsoft tooget

Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configuración de emparejamiento de Microsoft tooupdate

Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola:

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>emparejamiento de Microsoft toodelete

Puede quitar la configuración de intercambio de tráfico mediante la ejecución de hello siguiente cmdlet:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Pasos siguientes

Siguiente paso, [vincular un circuito de ExpressRoute de red virtual tooan](expressroute-howto-linkvnet-arm.md).

* Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).
* Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).
* Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).
