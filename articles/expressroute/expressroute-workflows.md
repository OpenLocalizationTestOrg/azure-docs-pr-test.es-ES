---
title: aaaWorkflows para configurar un circuito ExpressRoute | Documentos de Microsoft
description: "Esta página le guiará por los flujos de trabajo de Hola para configurar los emparejamientos y circuito de ExpressRoute"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute
Esta página le guiará por el aprovisionamiento del servicio de Hola y enrutamiento flujos de trabajo de configuración en un nivel superior.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Hello siguiente ilustración y los pasos correspondientes muestran tareas de hello que debe seguir en orden toohave una ExpressRoute circuito aprovisionada-to-end. 

1. Usar PowerShell tooconfigure un circuito ExpressRoute. Siga las instrucciones de Hola Hola [circuitos ExpressRoute crear](expressroute-howto-circuit-classic.md) artículo para obtener más detalles.
2. Conectividad de pedido de proveedor de servicios de Hola. Este proceso varía. Póngase en contacto con el proveedor de conectividad para obtener más información acerca de cómo tooorder conectividad.
3. Asegúrese de que el circuito de Hola se haya aprovisionado correctamente comprobando el circuito de ExpressRoute de hello estado a través de PowerShell de aprovisionamiento. 
4. Configure los dominios de enrutamiento. Si el proveedor de conectividad administra el nivel 3, configurará el enrutamiento del circuito. Si el proveedor de conectividad sólo ofrece servicios de nivel 2, debe configurar el enrutamiento por las directrices descritas en hello [requisitos de enrutamiento](expressroute-routing.md) y [configuración de enrutamiento](expressroute-howto-routing-classic.md) páginas.
   
   * Habilitar el emparejamiento privado de Azure, debe habilitar este emparejamiento tooVMs tooconnect / servicios implementados en redes virtuales en la nube.
   * Habilitar pares públicos de Azure: debe habilitar pares públicos de Azure si desea tooconnect tooAzure servicios hospedados en direcciones IP públicas. Se trata de un tooaccess requisito recursos de Azure si ha elegido el enrutamiento de tooenable predeterminado para el nivel privado de Azure.
   * Habilitar el emparejamiento de Microsoft: debe habilitar este tooaccess Office 365 y Dynamics 365. 
     
     > [!IMPORTANT]
     > Debe asegurarse de que usa a un proxy independiente ni borde tooconnect tooMicrosoft de Hola uno que utilice para Hola Internet. Uso de hello borde mismo de ExpressRoute y Hola Internet provocará enrutamiento asimétrico y causar interrupciones de la conectividad de la red.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Vinculación virtual redes circuitos tooExpressRoute: puede vincular circuito de ExpressRoute de tooyour de redes virtuales. Siga las instrucciones [toolink redes virtuales](expressroute-howto-linkvnet-arm.md) tooyour circuito. Estas redes virtuales pueden ser Hola misma suscripción de Azure como circuito de ExpressRoute de hello, o puede estar en una suscripción diferente.

## <a name="expressroute-circuit-provisioning-states"></a>Estados de aprovisionamiento de circuitos de ExpressRoute
Cada circuito ExpressRoute tiene dos estados:

* Estado de aprovisionamiento de proveedor de servicio
* Estado

Estado representa el estado de aprovisionamiento de Microsoft. Esta propiedad se establece tooEnabled cuando se crea un circuito Expressroute

estado de aprovisionamiento del proveedor de conectividad de Hello representa el estado de hello en el lado del proveedor de conectividad de Hola. Puede ser *No aprovisionado*, *Aprovisionando* o *Aprovisionado*. Hola circuito de ExpressRoute debe estar en estado aprovisionado para toobe pueda toouse lo.

### <a name="possible-states-of-an-expressroute-circuit"></a>Posibles estados de un circuito ExpressRoute
Esta sección se enumeran los posibles estados de Hola por un circuito ExpressRoute.

**En tiempo de creación**

Verá circuito de ExpressRoute de Hola Hola después estado tan pronto como se ejecute el circuito de ExpressRoute de hello PowerShell cmdlet toocreate Hola.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Al proveedor de conectividad está en proceso de Hola de aprovisionamiento del circuito de Hola**

Verá circuito de ExpressRoute de Hola Hola después estado en cuanto se pase el proveedor de conectividad de toohello clave de servicio de Hola y que se ha iniciado el proceso de aprovisionamiento de Hola.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**Cuando proveedor de conectividad ha completado el proceso de aprovisionamiento de Hola**

Verá Hola circuito de ExpressRoute en hello después estado tan pronto como proveedor de conectividad de hello ha completado el proceso de aprovisionamiento de Hola.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Aprovisionado y habilitado es hello solo circuito de Hola de estado que puede estar en para toobe pueda toouse. Si usa un proveedor de nivel 2, puede configurar el enrutamiento para el circuito solo cuando se encuentre en este estado.

**Cuando el proveedor de conectividad desaprovisionamiento circuito Hola**

Si se solicita el circuito de ExpressRoute de hello servicio proveedor toodeprovision hello, verá circuito Hola establece toohello después estado una vez completada la Hola proceso de desaprovisionamiento de proveedor de servicios de Hola.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Puede elegir habilitar toore, si es necesario, o ejecutar los cmdlets de PowerShell circuito de hello toodelete.  

> [!IMPORTANT]
> Si ejecuta Hola circuito de Hola de toodelete de PowerShell cmdlet hello ServiceProviderProvisioningState una vez aprovisionamiento o aprovisionado operación Hola se producirá un error. Coopere con el circuito de ExpressRoute de conectividad proveedor toodeprovision hello en primer lugar y, a continuación, eliminar el circuito de Hola. Microsoft seguirá circuito de hello toobill hasta que ejecute hello circuito de Hola de toodelete de cmdlet de PowerShell.
> 
> 

## <a name="routing-session-configuration-state"></a>Estado de configuración de sesión de enrutamiento
Hola estado de aprovisionamiento de BGP, sabrá si se ha habilitado la sesión BGP de hello en hello borde de Microsoft. Hello estado debe estar habilitado para toobe toouse capaz de hello emparejamiento.

Es importante toocheck estado de sesión BGP de hello especialmente para el emparejamiento de Microsoft. En el estado de aprovisionamiento de suma toohello BGP, hay otro estado llamado *anunciados estado prefijos públicos*. Hola anunciados estado prefijos públicos debe estar en *configurado* state, tanto para hello BGP sesión toobe seguridad y para su enrutamiento toowork-to-end. 

Si Hola anuncia el estado de prefijo pública se establece tooa *validación necesitado* estado, no está habilitada la sesión BGP de hello, tal como se advierte de hello prefijos no coincidía con hello como número en cualquiera de los registros de enrutamiento Hola. 

> [!IMPORTANT]
> Si Hola anunciados estado prefijos públicos se encuentra en *validación manual* estado, debe abrir una incidencia de soporte técnico con [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) y constituyen una prueba que pertenecen a las direcciones IP Hola anuncian a lo largo de con hello había asociado el número de sistema autónomo.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Configure su conexión ExpressRoute.
  
  * [Creación de un circuito ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configuración del enrutamiento](expressroute-howto-routing-arm.md)
  * [Vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-arm.md)

