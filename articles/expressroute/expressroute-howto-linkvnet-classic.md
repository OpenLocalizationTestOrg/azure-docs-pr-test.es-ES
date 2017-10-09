---
title: "Vincular un circuito de ExpressRoute de tooan de red virtual: PowerShell: clásico: Azure | Documentos de Microsoft"
description: "Este documento proporciona información general sobre cómo toolink virtual redes (redes virtuales) tooExpressRoute circuitos utilizando el modelo de implementación clásica de Hola y PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Conectarse a un circuito de ExpressRoute de tooan de red virtual con PowerShell (clásico)
> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI de Azure](howto-linkvnet-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-linkvnet-classic.md)
>

Este artículo le ayudará a vincular circuitos ExpressRoute de tooAzure de redes virtuales (Vnet) mediante el modelo de implementación clásica de Hola y PowerShell. Redes virtuales pueden ser en Hola misma suscripción o puede formar parte de otra suscripción.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Información sobre los modelos de implementación de Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Requisitos previos de configuración
1. Necesita la versión más reciente de Hola de módulos de PowerShell de Azure de Hola. Puede descargar módulos de PowerShell más recientes de Hola de hello sección PowerShell de hello [página de descargas de Azure](https://azure.microsoft.com/downloads/). Siga las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener instrucciones paso a paso acerca de cómo tooconfigure los módulos de PowerShell de Azure de equipo toouse Hola.
2. Necesita hello tooreview [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
3. Tiene que tener un circuito ExpressRoute activo.
   * Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y tener el proveedor de conectividad habilitar circuito Hola.
   * Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito. Vea hello [configurar enrutamiento](expressroute-howto-routing-classic.md) artículo para las instrucciones de enrutamiento.
   * Asegúrese de que el emparejamiento privado Azure está configurado y Hola emparejamiento de BGP entre la red y Microsoft está activo para que se puede habilitar la conectividad de extremo a extremo.
   * Debe crear y aprovisionar totalmente una red virtual y una puerta de enlace de red virtual. Siga las instrucciones de hello demasiado[configurar una red virtual para ExpressRoute](expressroute-howto-vnet-portal-classic.md).

Puede vincular una too10 redes virtuales tooan circuito de ExpressRoute. Todas las redes virtuales deben estar en hello misma región geopolíticos. Puede vincular un mayor número de redes virtuales tooyour circuito de ExpressRoute o vincular redes virtuales que se encuentran en otras regiones geopolíticas si ha habilitado el complemento de hello ExpressRoute premium. Comprobar hello [preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más detalles sobre el complemento de hello premium.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar una red virtual en hello mismo circuito de tooa de suscripción
Puede vincular un circuito de ExpressRoute de tooan de red virtual mediante el siguiente cmdlet de Hola. Asegúrese de que esa puerta de enlace de red virtual de Hola se crea y está listo para crear un vínculo antes de ejecutar el cmdlet de Hola.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar una red virtual en un circuito de tooa otra suscripción
Puede compartir un circuito ExpressRoute entre varias suscripciones. Hola figura siguiente muestra un sencillo esquema de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.

Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización. Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios--pero departamentos Hola puede compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local. Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola. Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.

> [!NOTE]
> Los cargos de conectividad y ancho de banda para el circuito dedicado de hello será propietario del circuito de ExpressRoute toohello aplicada. Todas las redes virtuales compartan Hola mismo ancho de banda.
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Administración
Hola *propietario del circuito* es Hola administrador o coadministrator de suscripción de hello en qué hello ExpressRoute se crea el circuito. Hello propietario del circuito puede autorizar a los administradores/coadministrators de otras suscripciones, que se hace referencia tooas *a los usuarios de circuito*, toouse Hola dedicado circuito que les pertenecen. Los usuarios de circuito que son can de circuito de ExpressRoute de la organización de toouse autorizados Hola vinculan la red virtual de hello en su toohello suscripción circuito ExpressRoute después de que están autorizados.

propietario del circuito Hello tiene Hola power toomodify y revocar las autorizaciones en cualquier momento. Revocación de una autorización provocará que todos los vínculos que se va a eliminar de suscripción de hello cuyo acceso se ha revocado.

### <a name="circuit-owner-operations"></a>Operaciones del propietario del circuito

**Creación de una autorización**

Hello propietario del circuito autoriza a los administradores de Hola de otras suscripciones toouse Hola especificado circuito. En el siguiente ejemplo de Hola, Administrador de hello del circuito de hello (TI de Contoso) habilita a administrador Hola de otro toolink de suscripción (desarrollo de prueba) de circuito de toohello de tootwo redes virtuales. Administrador de TI de Contoso de Hello hace posible mediante la especificación de hello Id. de desarrollo y pruebas de Microsoft. Hola cmdlet no envía correo electrónico toohello especificado identificador de Microsoft. propietario del circuito Hola necesita tooexplicitly notificar Hola otro propietario de la suscripción que Hola autorización ha finalizado.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Revisión de las autorizaciones**

propietario del circuito Hola puede revisar todas las autorizaciones que se ejecutan en un circuito concreto mediante la ejecución de hello siguiente cmdlet:

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Actualización de autorizaciones**

propietario del circuito Hola puede modificar las autorizaciones mediante Hola siguiente cmdlet:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Eliminación de autorizaciones**

propietario del circuito Hola puede revocar o eliminar un autorizaciones toohello usuario ejecutando Hola siguiente cmdlet:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Operaciones del usuario del circuito

**Revisión de las autorizaciones**

usuario de circuito de Hello puede revisar las autorizaciones mediante Hola siguiente cmdlet:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Canjear autorizaciones de vínculo**

usuario de circuito de Hello puede ejecutar Hola siguiente cmdlet tooredeem una autorización de vínculo:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Ejecute este comando en la suscripción de hello recién vinculado para la red virtual de hello:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).

