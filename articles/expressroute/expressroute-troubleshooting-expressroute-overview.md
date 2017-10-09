---
title: "Comprobación de la conectividad: Guía de solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "Esta página proporciona instrucciones sobre la solución de problemas y validar la conectividad de tooend de final de un circuito de ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>Comprobación de la conectividad de ExpressRoute
ExpressRoute, que amplía una red local en la nube de Microsoft hello por medio de una conexión privada que se realiza mediante un proveedor de conectividad, implica Hola siguientes a tres zonas de red distintas:

-   Red del cliente
-   Red del proveedor
-   Centro de datos de Microsoft

Hola de este documento sirve toohelp usuario tooidentify donde (o incluso si) existe un problema de conectividad y en qué zona, con lo que se tooseek de Ayuda de problema de equipo adecuada tooresolve Hola. Si soporte técnico de Microsoft es necesario tooresolve un problema, abra una incidencia de soporte técnico con [Microsoft Support][Support].

> [!IMPORTANT]
> Este documento es toohelp previsto diagnosticar y corregir problemas sencillos. No está previsto toobe un sustituto de soporte técnico de Microsoft. Abra una incidencia de soporte técnico con [Microsoft Support] [ Support] si está toosolve no se puede problema de hello usando la orientación de hello proporcionado.
>
>

## <a name="overview"></a>Información general
Hello siguiente diagrama muestra hello lógica a la conectividad de una red de tooMicrosoft de red de cliente mediante ExpressRoute.
[![1]][1]

Hola anterior diagrama, los números de hello indican puntos clave de red. puntos de la red de Hola se hace referencia a menudo a través de este artículo por su número asociado.

Según la conectividad de ExpressRoute de hello modelo (ubicación compartida de Exchange en la nube, conexión Ethernet de punto a punto o (IPVPN) y a cualquier) Hola red puntos 3 y 4 pueden ser conmutadores (dispositivos de capa 2). puntos clave Hola se muestra son los siguientes:

1.  Dispositivo de proceso del cliente (por ejemplo, un servidor o equipo)
2.  CE: enrutadores en el lado del cliente 
3.  PE (hacia los CE): enrutadores o conmutadores del lado del proveedor orientados hacia los enrutadores del lado del cliente. Conoce tooas PE CEs en este documento.
4.  PE (hacia los MSEE): enrutadores o conmutadores del lado del proveedor orientados hacia los MSEE. Conoce tooas PE MSEEs en este documento.
5.  MSEEs: enrutadores de Microsoft Enterprise Edge (MSEE) ExpressRoute
6.  Puerta de enlace de Virtual Network (VNet)
7.  Dispositivo de red virtual de Azure Hola de proceso

Si se utilizan los modelos de conectividad de colocación de Exchange para la nube o una conexión Ethernet de punto a punto de hello, enrutador perimetral de cliente hello (2) ¿establecer BGP emparejamiento con MSEEs (5). Los puntos de red 3 y 4 todavía existirán, pero serán transparentes de forma parecida a los dispositivos de capa 2.

Si se usa el modelo de conectividad de Hola y a cualquier (IPVPN), Hola PEs (MSEE con conexión a) (4) podría establecer BGP emparejamiento con MSEEs (5). Las rutas, a continuación, podrían propagar toohello atrás de red de cliente a través de la red del proveedor de servicio de hello IPVPN.

>[!NOTE]
>Para lograr la alta disponibilidad de ExpressRoute, Microsoft requiere un par redundante de sesiones BGP entre los MSEE (5) y los PE-MSEE (4). También se recomienda establecer un par redundante de rutas de red entre la red del cliente y los PE-CE. Sin embargo, en el modelo de conexión y a cualquier (IPVPN), un único dispositivo CE (2) pueden tooone conectado o más PEs (3).
>
>

toovalidate un circuito de ExpressRoute, Hola pasos se tratan (con el punto de red de hello indicado por el número de asociados de hello):
1. [Validación del aprovisionamiento y el estado del circuito (5)](#validate-circuit-provisioning-and-state)
2. [Validación de que hay al menos un emparejamiento de ExpressRoute configurado (5)](#validate-peering-configuration)
3. [Validar a ARP entre el proveedor de servicios de Microsoft y hello (vínculo entre 4 y 5)](#validate-arp-between-microsoft-and-the-service-provider)
4. [Validar BGP y las rutas de hello MSEE (BGP entre too5 4 y 5 too6 si está conectada a una red virtual)](#validate-bgp-and-routes-on-the-msee)
5. [Hola de comprobación de las estadísticas de tráfico (tráfico que pasa a través de 5)](#check-the-traffic-statistics)

Más validaciones y comprobaciones se agregarán en hello futuras, consulte esta página mensualmente!

##<a name="validate-circuit-provisioning-and-state"></a>Validación del aprovisionamiento y el estado del circuito
Independientemente del modelo de conectividad a hello, tiene un circuito ExpressRoute toobe creado y, por tanto, un servicio en la clave generada para el aprovisionamiento del circuito. El aprovisionamiento de un circuito ExpressRoute establece conexiones redundantes de capa 2 entre los PE-MSEE (4) y los MSEE (5). Para obtener más información acerca de cómo toocreate, modificar, aprovisionar y comprobar un circuito ExpressRoute, consulte el artículo de hello [crear y modificar un circuito ExpressRoute][CreateCircuit].

>[!TIP]
>Una clave de servicio identifica de forma única un circuito ExpressRoute. Esta clave es necesaria para la mayoría de los comandos de powershell de hello mencionados en este documento. Además, si necesita asistencia de Microsoft o de un tootroubleshoot de socio comercial de ExpressRoute un problema de ExpressRoute, proporcionar servicio hello tooreadily clave identificar circuito Hola.
>
>

###<a name="verification-via-hello-azure-portal"></a>Comprobación a través de hello portal de Azure
Hola portal de Azure, se puede comprobar el estado Hola de un circuito ExpressRoute seleccionando ![2][2] en hello menú de barra de lado izquierda y, a continuación, seleccionando Hola circuito de ExpressRoute. Al seleccionar una ExpressRoute circuito aparecen en "Todos los recursos" abre una hoja de circuito de ExpressRoute Hola. Hola ![3][3] sección de hoja de hello, hello ExpressRoute essentials aparecen como se muestra en la siguiente captura de pantalla de hello:

![4][4]    

Hola Essentials de ExpressRoute, *Circuit estado* indica el estado de saludo del circuito de hello en hello side de Microsoft. *Estado del proveedor* indica si se ha circuito hello *aprovisionado/no aprovisionado* en lado de proveedor de servicios de Hola. 

Para toobe de circuito ExpressRoute operativa, Hola *Circuit estado* debe ser *habilitado* hello y *estado del proveedor* debe ser *aprovisionado*.

>[!NOTE]
>Si hello *Circuit estado* no es habilitado, póngase en contacto con [Microsoft Support][Support]. Si hello *estado del proveedor* no es aprovisionado, póngase en contacto con su proveedor de servicios.
>
>

###<a name="verification-via-powershell"></a>Comprobación a través de PowerShell
toolist Hola a todos los circuitos ExpressRoute en un grupo de recursos, utilice Hola siguiente comando:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>Puede obtener el nombre del grupo de recursos a través de hello portal de Azure. Vea Hola subsección anterior de este documento y tenga en cuenta que ese nombre de grupo de recursos de Hola se muestra en la captura de pantalla de ejemplo de Hola.
>
>

tooselect un circuito de ExpressRoute determinado en un grupo de recursos, Hola de uso siguiente comando:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Una respuesta de ejemplo es:

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm si un circuito ExpressRoute está operativo, preste toohello especial atención siguientes campos:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Si hello *CircuitProvisioningState* no es habilitado, póngase en contacto con [Microsoft Support][Support]. Si hello *ServiceProviderProvisioningState* no es aprovisionado, póngase en contacto con su proveedor de servicios.
>
>

###<a name="verification-via-powershell-classic"></a>Comprobación a través de PowerShell (Clásico)
toolist Hola a todos los circuitos ExpressRoute en una suscripción, utilice Hola siguiente comando:

    Get-AzureDedicatedCircuit

tooselect un circuito de ExpressRoute determinado, use Hola siguiente comando:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Una respuesta de ejemplo es:

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm si está operativo, un circuito ExpressRoute pagar toohello especial atención siguientes campos: ServiceProviderProvisioningState: estado de aprovisionamiento: habilitado

>[!NOTE]
>Si hello *estado* no es habilitado, póngase en contacto con [Microsoft Support][Support]. Si hello *ServiceProviderProvisioningState* no es aprovisionado, póngase en contacto con su proveedor de servicios.
>
>

##<a name="validate-peering-configuration"></a>Validación de la configuración de emparejamiento
Después de que el proveedor de servicios de hello tiene completado Hola aprovisionamiento del circuito de ExpressRoute de hello, se pueden crear una configuración de enrutamiento en hello circuito de ExpressRoute entre MSEE-PR (4) y MSEEs (5). Cada circuito de ExpressRoute puede tener uno, dos o tres contextos de enrutamiento habilitados: el emparejamiento privado Azure (tráfico tooprivate redes virtuales en Azure), el emparejamiento público Azure (direcciones IP de tráfico toopublic en Azure) y (tráfico tooOffice 365 de emparejamiento de Microsoft y Dynamics 365). Para obtener más información acerca de cómo toocreate y modificar la configuración de enrutamiento, consulte el artículo de hello [crear y modificar el enrutamiento de un circuito de ExpressRoute][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Comprobación a través de hello portal de Azure
>[!IMPORTANT]
>Hay un problema conocido en hello portal de Azure donde están los emparejamientos de ExpressRoute *no* muestran en el portal de hello si configurado por el proveedor de servicios de Hola. Adición de emparejamientos de ExpressRoute a través del portal de Hola o PowerShell *sobrescribe la configuración del proveedor de servicio de hello*. Esta acción interrumpe Hola enrutamiento en el circuito de ExpressRoute de Hola y requiere soporte de Hola Hola proveedor toorestore Hola de opciones de servicios y restablecer la distribución normal. Modificar solo hello ExpressRoute emparejamientos si que dicho proveedor de servicios de hello proporciona servicios de nivel 2 solo!
>
>

<p/>
>[!NOTE]
>Si capa 3 se proporciona por hello emparejamientos de hello y proveedor de servicio están en blanco en el portal de hello, PowerShell puede ser usado toosee Hola servicio proveedor configurado configuración.
>
>

Hola portal de Azure, se puede comprobar el estado de un circuito ExpressRoute seleccionando ![2][2] en hello menú de barra de lado izquierda y, a continuación, seleccionando Hola circuito de ExpressRoute. Al seleccionar una ExpressRoute circuito aparecen en "Todos los recursos" abriría hoja de circuito de ExpressRoute Hola. Hola ![3][3] sección de hoja de hello, hello ExpressRoute essentials aparecerá como se muestra en la siguiente captura de pantalla de hello:

![5][5]

En el anterior ejemplo de Hola, como se indicó Azure privada emparejamiento enrutamiento se ha habilitado el contexto, mientras que Azure pública y contextos de enrutamiento de emparejamiento de Microsoft no están habilitadas. Un contexto de emparejamiento se habilitó correctamente también tendría subredes de punto a punto principal y secundaria (requerido para BGP) Hola enumerados. subredes de Hello /30 se usan para dirección IP de la interfaz de Hola de hello MSEEs y MSEEs PE. 

>[!NOTE]
>Si no está habilitado un emparejamiento, compruebe si coincide con subredes principal y secundaria de hello asignadas configuración hello en MSEEs PE. Si no es así, toochange Hola configuración en los enrutadores MSEE, consulte demasiado[crear y modificar el enrutamiento de un circuito de ExpressRoute][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>Comprobación a través de PowerShell
tooget hello Azure privada emparejamiento detalles de configuración, utilice Hola siguientes comandos:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Una respuesta de ejemplo para un emparejamiento privado configurado correctamente es:

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Un contexto de emparejamiento se habilitó correctamente tendría prefijos de dirección principal y secundaria de hello enumerados. subredes de Hello /30 se usan para dirección IP de la interfaz de Hola de hello MSEEs y MSEEs PE.

tooget hello Azure pública emparejamiento detalles de configuración, utilice Hola siguientes comandos:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget Hola emparejamiento configuración detalles de Microsoft, use Hola siguientes comandos:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Si no se configura un emparejamiento, aparecerá un mensaje de error. Una respuesta de ejemplo, cuando Hola indique emparejamiento (públicos de Azure emparejamiento en este ejemplo) no está configurada en el circuito de hello:

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Si no está habilitado un emparejamiento, comprobar si Hola principal y secundaria subredes asignadas coincidencia Hola configuración en hello vinculado MSEE PE. También compruebe si hello corregir *VlanId*, *AzureASN*, y *PeerASN* se utilizan en MSEEs y si estos valores se asigna toohello aquellas que se usan en hello vinculado MSEE PE. Si se elige el hash MD5, una clave compartida Hola debe coincidir en MSEE y PE MSEE par. la configuración de hello toochange en los enrutadores MSEE hello, demasiado, consulte [crear y modificar el enrutamiento por un circuito ExpressRoute] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>Comprobación a través de PowerShell (Clásico)
Hola tooget Azure privada emparejamiento detalles de configuración, utilice Hola siguiente comando:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Una respuesta de ejemplo de un emparejamiento privado configurado correctamente es:

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

Se ha habilitado correctamente, un contexto emparejamiento tendría subredes del mismo nivel principal y secundaria de hello enumerados. subredes de Hello /30 se usan para dirección IP de la interfaz de Hola de hello MSEEs y MSEEs PE.

tooget hello Azure pública emparejamiento detalles de configuración, utilice Hola siguientes comandos:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget Hola emparejamiento configuración detalles de Microsoft, use Hola siguientes comandos:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Si emparejamientos de capa 3 se establecieron por el proveedor de servicios de hello, establecer Hola emparejamientos de ExpressRoute a través del portal de Hola o PowerShell sobrescribe la configuración del proveedor de servicio de Hola. Restablecer la configuración de emparejamiento de lado de proveedor de hello requiere soporte de Hola Hola del proveedor de servicios. Modificar solo hello ExpressRoute emparejamientos si que dicho proveedor de servicios de hello proporciona servicios de nivel 2 solo!
>
>

<p/>
>[!NOTE]
>Si no está habilitado un emparejamiento, comprobar si configuración Hola del mismo nivel principal y secundaria subredes asignadas coincidencia hello en hello vinculado MSEE PE. También compruebe si hello corregir *VlanId*, *AzureAsn*, y *PeerAsn* se utilizan en MSEEs y si estos valores se asigna toohello aquellas que se usan en hello vinculado MSEE PE. la configuración de hello toochange en los enrutadores MSEE hello, demasiado, consulte [crear y modificar el enrutamiento por un circuito ExpressRoute] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Validar a ARP entre el proveedor de servicios de Microsoft y Hola
Esta sección utiliza comandos de PowerShell (clásico). Si ha estado utilizando los comandos del Administrador de recursos de Azure PowerShell, asegúrese de que dispone de acceso de administrador o Coadministrador toohello suscripción a través de [portal de Azure clásico][OldPortal]. Para solucionar problemas con el Administrador de recursos de Azure comandos, consulte toohello [tablas de ARP obtener en el modelo de implementación del Administrador de recursos de hello] [ ARP] documento.

>[!NOTE]
>se puede utilizar tooget ARP, Hola portal de Azure y comandos de PowerShell del Administrador de recursos de Azure. Si se producen errores con los comandos de PowerShell del Administrador de recursos de Azure de hello, comandos de PowerShell clásicos deben funcionar como PowerShell clásico comandos también funcionan con circuitos ExpressRoute de administrador de recursos de Azure.
>
>

tooget Hola tabla ARP del enrutador MSEE principal de hello para el nivel privado de hello, usar hello siguiente comando:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Una respuesta de ejemplo de comando de hello, en caso de éxito hello:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

De forma similar, puede comprobar la tabla ARP de hello MSEE Hola Hola *principal*/*secundaria* ruta de acceso, para *privada* /  *Pública*/*Microsoft* emparejamientos.

Hello el ejemplo siguiente se muestra hello respuesta del comando de Hola para un emparejamiento no existe.

    ARP Info:
       
>[!NOTE]
>Si no dispone de hello tabla ARP direcciones IP de interfaces de hello asignan direcciones tooMAC, Hola revisión siguiente información:
>1. Si Hola primera asignará dirección IP de subred de hello /30 para hello vínculo entre Hola PR MSEE y MSEE se utiliza en la interfaz de Hola de MSEE de int Azure usa siempre la dirección IP de la segunda Hola para MSEEs.
>2. Compruebe si Hola cliente (C-Tag) y las etiquetas VLAN de servicio (S-Tag) coinciden con ambos en par MSEE PR y MSEE.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>Validar BGP y las rutas de hello MSEE
Esta sección utiliza comandos de PowerShell (clásico). Si ha estado utilizando los comandos del Administrador de recursos de Azure PowerShell, asegúrese de que dispone de acceso de administrador o Coadministrador toohello suscripción a través de [portal de Azure clásico][OldPortal]

>[!NOTE]
>tooget información sobre BGP, ambos Hola portal de Azure y comandos de PowerShell del Administrador de recursos de Azure se pueden usar. Si se producen errores con los comandos de PowerShell del Administrador de recursos de Azure de hello, comandos de PowerShell clásicos deben funcionar como PowerShell clásico comandos también funcionan con circuitos ExpressRoute de administrador de recursos de Azure.
>
>

tooget Hola tabla de enrutamiento (vecino BGP) resumen para un determinado contexto de enrutamiento, usar hello siguiente comando:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Ejemplo de respuesta:

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Tal y como se muestra en el anterior ejemplo de Hola, comando hello es útil toodetermine de cuánto tiempo se ha establecido el contexto de enrutamiento Hola. También indica el número de prefijos de rutas que anuncia Hola emparejamiento enrutador.

>[!NOTE]
>Si el estado de hello en activo o inactivo, comprobar si configuración Hola del mismo nivel principal y secundaria subredes asignadas coincidencia hello en hello vinculado MSEE PE. También compruebe si hello corregir *VlanId*, *AzureAsn*, y *PeerAsn* se utilizan en MSEEs y si estos valores se asigna toohello aquellas que se usan en hello vinculado MSEE PE. Si se elige el hash MD5, una clave compartida Hola debe coincidir en MSEE y PE MSEE par. la configuración de hello toochange en los enrutadores MSEE hello, demasiado, consulte[crear y modificar el enrutamiento de un circuito de ExpressRoute][CreatePeering].
>
>

<p/>
>[!NOTE]
>Si algunos destinos no son accesibles a través de un emparejamiento determinado, compruebe la tabla de rutas de Hola de MSEEs Hola que pertenecen a ese contexto concreto emparejamiento toohello. Si un prefijo coincidente (podría ser NATed IP) se encuentra en la tabla de enrutamiento de hello, a continuación, compruebe si hay firewalls/NSG/ACL en la ruta de acceso de Hola y permitir el tráfico de Hola.
>
>

tooget Hola completa tabla de enrutamiento de MSEE hello *principal* ruta de acceso de hello determinado *privada* contexto de enrutamiento, Hola de uso siguiente comando:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Es un resultado correcto de ejemplo de comando de hello:

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

De forma similar, puede comprobar la tabla de enrutamiento de Hola de hello MSEE Hola *principal*/*secundaria* ruta de acceso, para *privada* / *Pública*/*Microsoft* un contexto de emparejamiento.

Hello el ejemplo siguiente se muestra hello respuesta del comando de Hola para un emparejamiento no existe:

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Hola de comprobación de las estadísticas de tráfico
Hola tooget combina estadísticas de tráfico de la ruta de acceso principal y secundaria: bytes de entrada y salida, de un contexto de intercambio de tráfico, Hola de uso siguiente comando:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Es un resultado de ejemplo de Hola comando:

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

Es un resultado de ejemplo de comando de Hola para un emparejamiento inexistente:

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información o ayuda, visite Hola siguientes vínculos:

- [Ayuda y soporte técnico de Microsoft][Support]
- [Creación y modificación de un circuito ExpressRoute][CreateCircuit]
- [Creación y modificación del enrutamiento de un circuito ExpressRoute][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity" (Conectividad lógica de Expressroute)
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icono All resources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icono Overview"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Captura de pantalla de ejemplo de Essentials de ExpressRoute"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Captura de pantalla de ejemplo de Essentials de ExpressRoute"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






