---
title: "Creación y modificación de un circuito ExpressRoute mediante Azure Portal | Microsoft Docs"
description: "Este artículo describe cómo toocreate, aprovisionar, compruebe, actualizar, eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Creación y modificación de un circuito ExpressRoute
> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI de Azure](howto-circuit-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-circuit-classic.md)
>

Este artículo describe cómo toocreate un circuito de ExpressRoute de Azure mediante el uso de hello Azure modelo de implementación de Azure Resource Manager hello y portal. Hola siguientes pasos también muestra cómo actualizarlo, estado de hello toocheck del circuito de hello, o eliminar y Cancelar.


## <a name="before-you-begin"></a>Antes de empezar
* Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
* Asegúrese de que tiene acceso toohello [portal de Azure](https://portal.azure.com).
* Asegúrese de que dispone de recursos de red nuevos permisos toocreate. Si no tiene los permisos adecuados de hello, póngase en contacto con el Administrador de cuentas.
* También puede [ver un vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de comenzar en orden toobetter comprender los pasos de Hola.

## <a name="create-and-provision-an-expressroute-circuit"></a>Creación y aprovisionamiento de un circuito ExpressRoute
### <a name="1-sign-in-toohello-azure-portal"></a>1. Inicie sesión en toohello portal de Azure
Desde un explorador, navegue toohello [portal de Azure](http://portal.azure.com) e inicie sesión con su cuenta de Azure.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Creación de un circuito ExpressRoute.
> [!IMPORTANT]
> El circuito de ExpressRoute se cobrará desde el momento de Hola que se emite una clave de servicio. Asegúrese de que lleva a cabo esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.
> 
> 

1. Puede crear un circuito ExpressRoute seleccionando Hola opción toocreate un nuevo recurso. Haga clic en **New** > **red** > **ExpressRoute**, tal y como se muestra en hello después de imagen:
   
    ![Creación de un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Tras hacer clic en **ExpressRoute**, verá hello **circuito de ExpressRoute crear** hoja. Cuando está rellena los valores de hello en esta hoja, asegúrese de que se especifique nivel correcto de la SKU de Hola y medición de datos.
   
   * **Nivel** determina si está habilitado un complemento estándar o premium de ExpressRoute. Puede especificar **estándar** tooget Hola SKU estándar o **Premium** para el complemento de hello premium.
   * **Medición de datos** determina el tipo de facturación de Hola. Puede especificar **Metered** (Limitado) para un plan de datos limitado y **Unlimited** (Ilimitado) para un plan de datos ilimitado. Tenga en cuenta que puede cambiar el tipo de facturación de Hola de **Metered** demasiado**Unlimited**, pero no se puede cambiar tipo hello de **Unlimited** demasiado**Metered**.
     
     ![Configurar el nivel de la SKU de Hola y medición de datos](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Ten en cuenta esa ubicación de emparejamiento de hello indica hello [ubicación física](expressroute-locations.md) donde están emparejamiento con Microsoft. Se trata de **no** vinculado demasiado propiedad "Location", que hace referencia geography toohello donde se encuentra Hola proveedor de recursos de red de Azure. Aunque no están relacionadas, es un toochoose recomendable una ubicación de emparejamiento del circuito de Hola de proveedor de recursos de red geográficamente cerrar toohello. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Vista Hola circuitos y propiedades
**Ver todos los circuitos de Hola**

Puede ver todos los circuitos de Hola que creaste seleccionando **todos los recursos** en el menú del lado izquierdo de Hola.

![Visualización de circuitos](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Ver propiedades de Hola**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Ver propiedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento
En esta hoja, **estado del proveedor** proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola. **Estado de circuito** proporciona el estado de hello en hello side de Microsoft. Para obtener más información acerca de los Estados de aprovisionamiento del circuito, vea hello [flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states) artículo.

Cuando se crea un nuevo circuito de ExpressRoute, circuito Hola estará en hello siguiente estado:

Estado de proveedor: No aprovisionado<BR>
Estado de circuito: Habilitado

![Inicio del proceso de aprovisionamiento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

circuito Hola cambiará toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:

Estado de proveedor: Aprovisionamiento<BR>
Estado de circuito: Habilitado

Para toobe pueda toouse un circuito ExpressRoute, debe estar en hello siguiente estado:

Estado de proveedor: Aprovisionado<BR>
Estado de circuito: Habilitado

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola
Puede ver propiedades de Hola de circuito de Hola que le interesa, selecciónelo. Comprobar hello **estado del proveedor** y asegúrese de que se ha movido demasiado**aprovisionado** antes de continuar.

![Estado del circuito y proveedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Creación de la configuración de enrutamiento
Para obtener instrucciones detalladas, consulte toohello [circuito de ExpressRoute de configuración de enrutamiento](expressroute-howto-routing-portal-resource-manager.md) artículo toocreate y modificar los emparejamientos de circuito.

> [!IMPORTANT]
> Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Vincular un circuito de ExpressRoute de tooan de red virtual
A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual. Hola de uso [vinculación virtual redes tooExpressRoute circuitos](expressroute-howto-linkvnet-arm.md) artículo cuando se trabaja con el modelo de implementación del Administrador de recursos de Hola.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Obtener el estado de saludo de un circuito ExpressRoute
Puede ver el estado de Hola de un circuito, selecciónelo. 

![Estado de un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Modificación de un circuito ExpressRoute
Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.

Puede hacer Hola sigue sin tiempo de inactividad:

* Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.
* Ancho de banda de Hola de aumento de su circuito de ExpressRoute proporciona hay capacidad disponible en el puerto de Hola. Tenga en cuenta que no se admite la degradación de ancho de banda de Hola de un circuito. 
* Cambiar Hola plan desde tooUnlimited datos limitados de datos de disponibilidad. Tenga en cuenta ese plan de disponibilidad de hello cambiante de tooMetered datos ilimitados que datos no se admiten.
* Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).

Para obtener más información sobre los límites y limitaciones, consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).

toomodify un circuito ExpressRoute, haga clic en hello **configuración** tal y como se muestra en la siguiente ilustración de Hola.

![Modificación del circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Puede modificar el ancho de banda de hello, SKU, modelo de facturación y permiten operaciones clásicas dentro de la hoja de configuración de Hola.

> [!IMPORTANT]
> Puede tener circuito de ExpressRoute de hello toorecreate si hay capacidad inadecuada en el puerto existente Hola. No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.
>
> No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones. Degradar de ancho de banda requiere circuito de ExpressRoute de toodeprovision hello y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.
> 
> Deshabilitar complemento premium puede producir un error en la operación si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desaprovisionamiento y eliminación de un circuito ExpressRoute
Puede eliminar el circuito de ExpressRoute seleccionando hello **eliminar** icono. Tenga en cuenta los siguiente hello:

* Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute. Si se produce un error en esta operación, compruebe si las redes virtuales están vinculadas toohello circuito.
* Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado** debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados. Se continuará tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.
* Si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de hello (proveedor de servicios de hello estado de aprovisionamiento se establece demasiado**no aprovisionado**), a continuación, puede eliminar el circuito de Hola. Se detendrá la facturación para el circuito de Hola

## <a name="next-steps"></a>Pasos siguientes
Después de crear el circuito, asegúrese de que Hola siguientes:

* [Crear y modificar el enrutamiento para el circuito ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
* [Vincular el circuito de ExpressRoute de tooyour de red virtual](expressroute-howto-linkvnet-arm.md)

