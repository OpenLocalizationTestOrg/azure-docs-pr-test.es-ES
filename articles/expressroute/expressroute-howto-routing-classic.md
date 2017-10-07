---
title: "¿Cómo tooconfigure enrutamiento (emparejamiento) por un circuito ExpressRoute: Azure: clásico | Documentos de Microsoft"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionamiento Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Creación y modificación del emparejamiento de un circuito ExpressRoute (clásica)
> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI de Azure](howto-routing-cli.md)
> * [Vídeo: pares privados](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo: pares públicos](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo: emparejamiento de Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-routing-classic.md)
> 

Este artículo le guía a través de hello pasos toocreate y administrar la configuración de enrutamiento para un circuito de ExpressRoute con el modelo de implementación clásica de hello y PowerShell. estos pasos Hello también le mostrará cómo actualizar, estado de hello toocheck, o eliminar y desaprovisionar los emparejamientos de un circuito de ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Información sobre los modelos de implementación de Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Requisitos previos de configuración
* Necesitará la versión más reciente de Hola de hello cmdlets de PowerShell de administración de servicio de Azure (SM). Para obtener más información, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/overview).  
* Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) página hello [requisitos de enrutamiento](expressroute-routing.md) hello y página [flujos de trabajo](expressroute-workflows.md) página antes de comenzar la configuración.
* Tiene que tener un circuito ExpressRoute activo. Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar. Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para usted toobe toorun capaz de hello cmdlets que se describe a continuación.

> [!IMPORTANT]
> Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente IPVPN, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.
> 
> 

Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute. Puede establecer las configuraciones entre pares en cualquier orden. Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Inicie sesión en tooyour cuenta de Azure y seleccione una suscripción
1. Abra la consola de PowerShell con derechos elevados y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que se conecta:

        Login-AzureRmAccount

2. Compruebe las suscripciones de hello para la cuenta de hello.

        Get-AzureRmSubscription

3. Si tiene más de una suscripción, seleccione Hola suscripción que desea toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. A continuación, usar hello siguiente cmdlet tooadd su tooPowerShell de suscripción de Azure para el modelo de implementación clásica de Hola.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Configuración entre pares privados de Azure
Esta sección proporciona instrucciones sobre cómo toocreate, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute. 

### <a name="toocreate-azure-private-peering"></a>toocreate emparejamiento privado de Azure
1. **Importe el módulo de PowerShell de Hola para ExpressRoute.**
   
    Debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola. Siguiente ejecución Hola comandos de módulos de Azure y ExpressRoute hello tooimport en la sesión de PowerShell de Hola.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Creación de un circuito ExpressRoute.**
   
    Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-classic.md) y hacer que se aprovisiona proveedor de conectividad de Hola. Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, siga estas instrucciones Hola. 
3. **Compruebe tooensure de circuito de ExpressRoute Hola se aprovisiona.**
   
    En primer lugar debe comprobar toosee si Hola circuito de ExpressRoute se aprovisionan y también habilitada. Vea el ejemplo de Hola a continuación.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Asegúrese de que el circuito de hello muestra como aprovisionado y habilitado. Si no es así, trabajar con su tooget de proveedor de conectividad el circuito toohello necesario al estado y.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurar Azure intercambio de tráfico privado para el circuito de Hola.**
   
    Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:
   
   * / 30 subred para el vínculo principal Hola. No debe ser parte de ningún espacio de direcciones reservado para redes virtuales.
   * / 30 subred para el vínculo secundario Hola. No debe ser parte de ningún espacio de direcciones reservado para redes virtuales.
   * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
   * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS. Puede usar un número AS privado para esta configuración entre pares. Asegúrese de que no usa 65515.
   * Hash MD5 si elige toouse uno. **Esto es opcional**.
     
    Puede ejecutar Hola después tooconfigure cmdlet Azure intercambio de tráfico privado para el circuito.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
     
    Puede utilizar la siguiente cmdlet de hello si elige toouse un hash MD5.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview privada emparejamiento detalles de Azure
Puede obtener detalles de configuración mediante el siguiente cmdlet de Hola

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuración de emparejamiento privada de Azure
Puede actualizar cualquier parte de configuración de hello mediante Hola siguiente cmdlet. En el ejemplo de Hola a continuación, Id. de VLAN del circuito de Hola Hola se está actualizando desde too500 100.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete emparejamiento privado de Azure
Puede quitar la configuración de intercambio de tráfico mediante la ejecución de hello siguiente cmdlet.

> [!WARNING]
> También debe asegurarse de que todas las redes virtuales se desvincula de hello circuito de ExpressRoute antes de ejecutar este cmdlet. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Configuración entre pares públicos de Azure
Esta sección proporciona instrucciones sobre cómo toocreate, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate pares públicos de Azure
1. **Importe el módulo de PowerShell de Hola para ExpressRoute.**
   
    Debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola. Siguiente ejecución Hola comandos de módulos de Azure y ExpressRoute hello tooimport en la sesión de PowerShell de Hola. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Creación de un circuito ExpressRoute**
   
    Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-classic.md) y hacer que se aprovisiona proveedor de conectividad de Hola. Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure pública de emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, siga estas instrucciones Hola.
3. **Compruebe tooensure de circuito de ExpressRoute se aprovisiona**
   
    En primer lugar debe comprobar toosee si Hola circuito de ExpressRoute se aprovisionan y también habilitada. Vea el ejemplo de Hola a continuación.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Asegúrese de que el circuito de hello muestra como aprovisionado y habilitado. Si no es así, trabajar con su tooget de proveedor de conectividad el circuito toohello necesario al estado y.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurar Azure el emparejamiento público para el circuito de Hola**
   
    Asegúrese de que tiene Hola siguiente información antes de continuar.
   
   * / 30 subred para el vínculo principal Hola. Tiene que ser un prefijo IPv4 público válido.
   * / 30 subred para el vínculo secundario Hola. Tiene que ser un prefijo IPv4 público válido.
   * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
   * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
   * Hash MD5 si elige toouse uno. **Esto es opcional**.
     
    Puede ejecutar Hola después tooconfigure cmdlet pares públicos de Azure para el circuito
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
     
    Puede usar el cmdlet de hello si elige toouse un hash MD5
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Asegúrese de especificar su número AS como ASN de configuración entre pares y no como cliente ASN.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview Azure pública emparejamiento detalles
Puede obtener detalles de configuración mediante el siguiente cmdlet de Hola

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuración de interconexión pública de Azure
Puede actualizar cualquier parte de configuración de hello mediante el siguiente cmdlet de Hola

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Id. de VLAN del circuito de Hola Hola se está actualizando de 200 too600 Hola ejemplo anterior.

### <a name="toodelete-azure-public-peering"></a>toodelete pares públicos de Azure
Puede quitar la configuración de emparejamiento ejecutando el siguiente cmdlet de Hola

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Emparejamiento de Microsoft
Esta sección proporciona instrucciones sobre cómo toocreate, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute. 

### <a name="toocreate-microsoft-peering"></a>emparejamiento de Microsoft toocreate
1. **Importe el módulo de PowerShell de Hola para ExpressRoute.**
   
    Debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola. Siguiente ejecución Hola comandos de módulos de Azure y ExpressRoute hello tooimport en la sesión de PowerShell de Hola.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Creación de un circuito ExpressRoute**
   
    Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-classic.md) y hacer que se aprovisiona proveedor de conectividad de Hola. Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, siga estas instrucciones Hola.
3. **Compruebe tooensure de circuito de ExpressRoute se aprovisiona**
   
    En primer lugar debe comprobar toosee si Hola circuito de ExpressRoute se encuentra en estado aprovisionado y habilitado.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Asegúrese de que el circuito de hello muestra como aprovisionado y habilitado. Si no es así, trabajar con su tooget de proveedor de conectividad el circuito toohello necesario al estado y.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurar Microsoft emparejamiento para el circuito de Hola**
   
    Asegúrese de que haya Hola siguiente información antes de continuar.
   
   * / 30 subred para el vínculo principal Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
   * / 30 subred para el vínculo secundario Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
   * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
   * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
   * Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola. Se aceptan solo prefijos de direcciones IP públicas. Puede enviar una lista separada por comas si tiene previsto toosend un conjunto de prefijos. Estos prefijos deben ser tooyou registrado en un RIR / IRR.
   * Cliente ASN: Si se anuncian prefijos que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich que están registrados. **Esto es opcional**.
   * Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.
   * Un hash MD5, si elige toouse uno. **Esto es opcional.**
     
    Puede ejecutar Hola después pering de Microsoft tooconfigure de cmdlet para el circuito
     
        New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>detalles de emparejamiento de Microsoft tooview
Puede obtener detalles de configuración mediante el siguiente cmdlet de Hola.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>configuración de emparejamiento de Microsoft tooupdate
Puede actualizar cualquier parte de configuración de hello mediante Hola siguiente cmdlet.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>emparejamiento de Microsoft toodelete
Puede quitar la configuración de intercambio de tráfico mediante la ejecución de hello siguiente cmdlet.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Pasos siguientes
Después, [vincular un circuito de ExpressRoute de red virtual tooan](expressroute-howto-linkvnet-classic.md).

* Para obtener más información sobre los flujos de trabajo, consulte [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).
* Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).

