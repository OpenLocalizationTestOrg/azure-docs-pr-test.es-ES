---
title: 'Vincular un circuito de ExpressRoute de tooan de red virtual: portal de Azure | Documentos de Microsoft'
description: "Este documento proporciona información general sobre cómo toolink virtual redes circuitos de tooExpressRoute (Vnet)."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Conectarse a un circuito de ExpressRoute de tooan de red virtual
> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI de Azure](howto-linkvnet-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-linkvnet-classic.md)
> 

En este artículo le ayuda a vincular circuitos ExpressRoute de tooAzure de redes virtuales (Vnet) mediante el modelo de implementación del Administrador de recursos de Hola y Hola portal de Azure. Redes virtuales pueden ser Hola misma suscripción, o bien pueden formar parte de otra suscripción.

## <a name="before-you-begin"></a>Antes de empezar
* Hola de revisión [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
* Tiene que tener un circuito ExpressRoute activo.
  
  * Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y tener habilitada por el proveedor de conectividad de circuito de Hola.
  * Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito. Vea hello [configurar enrutamiento](expressroute-howto-routing-portal-resource-manager.md) artículo para las instrucciones de enrutamiento.
  * Asegúrese de que el emparejamiento privado Azure está configurado y Hola emparejamiento de BGP entre la red y Microsoft está activo para que se puede habilitar la conectividad de extremo a extremo.
  * Asegúrese de que ha creado y aprovisionado totalmente una red virtual y una puerta de enlace de red virtual. Siga las instrucciones de hello demasiado[crear una puerta de enlace de red virtual para ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Una puerta de enlace de red virtual para ExpressRoute usa Hola el GatewayType 'ExpressRoute', no VPN.

* Puede vincular una circuito de ExpressRoute estándar de too10 redes virtuales tooa. Todas las redes virtuales deben estar en hello misma región geopolíticos cuando se usa un circuito de ExpressRoute estándar. 
* Puede vincular una red virtual fuera de la región geopolítica de Hola de hello circuito de ExpressRoute o conectar un mayor número de redes virtuales tooyour circuito ExpressRoute si ha habilitado el complemento de hello ExpressRoute premium. Comprobar hello [preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más detalles sobre el complemento de hello premium.
* También puede [ver un vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) antes de principio toobetter saber cuáles son los pasos de Hola.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar una red virtual en hello mismo circuito de tooa de suscripción

### <a name="toocreate-a-connection"></a>toocreate una conexión

> [!NOTE]
> Información de configuración de BGP no aparecerá si el proveedor de capa 3 de hello configurado los emparejamientos. Si el circuito está en un estado de aprovisionamiento, debe ser capaz de toocreate conexiones.
>

1. Asegúrese de que el circuito ExpressRoute y el emparejamiento privado de Azure estén correctamente configurados. Siga las instrucciones de hello en [crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y [configurar enrutamiento](expressroute-howto-routing-arm.md). El circuito de ExpressRoute debe ser similar Hola después de imagen:

    ![Captura de pantalla de un circuito ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. Ahora puede iniciar aprovisionamiento de una conexión toolink su tooyour de puerta de enlace de red virtual circuito de ExpressRoute. Haga clic en **conexión** > **agregar** tooopen hello **Agregar conexión** hoja y, a continuación, configure los valores de hello.

    ![Adición de captura de pantalla de conexión](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. Después de que la conexión se ha configurado correctamente, el objeto de conexión mostrará información de Hola para conexión de Hola.

     ![Captura de pantalla de objeto de conexión](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete una conexión
Puede eliminar una conexión seleccionando hello **eliminar** icono en la hoja de hello para la conexión.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar una red virtual en un circuito de tooa otra suscripción
Puede compartir un circuito ExpressRoute entre varias suscripciones. Hola siguiente ilustración muestra un sencillo esquemática de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización.
- Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios, pero pueden compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local.
- Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola. Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.

    > [!NOTE]
    > Los cargos de conectividad y ancho de banda para el circuito dedicado de hello será propietario del circuito de ExpressRoute toohello aplicada. Todas las redes virtuales compartan Hola mismo ancho de banda.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Administración: los propietarios de circuito y los usuarios de circuito

Hola 'propietario del circuito' es un usuario autorizado de alimentación de hello recursos de circuito de ExpressRoute. propietario del circuito Hola puede crear autorizaciones que se pueden canjear por 'usuarios del circuito'. Los usuarios de circuito son propietarios de red virtual puertas de enlace que no están en Hola misma suscripción como Hola circuito de ExpressRoute. Los usuarios del circuito pueden canjear autorizaciones (una autorización por red virtual).

propietario del circuito Hello tiene Hola power toomodify y revocar las autorizaciones en cualquier momento. Revocar el resultado de una autorización en todas las conexiones de vínculo que se va a eliminar de suscripción de hello cuyo acceso se ha revocado.

### <a name="circuit-owner-operations"></a>Operaciones del propietario del circuito

**toocreate una autorización de conexión**

propietario del circuito Hola crea una autorización. Esto resulta en hello creación de una clave de autorización que puede ser utilizados por un tooconnect de usuario de circuito su toohello de puertas de enlace de red virtual circuito de ExpressRoute. Una autorización solo es válida para una conexión.

1. En la hoja de ExpressRoute de hello, haga clic en **autorizaciones** y, a continuación, escriba un **nombre** para la autorización de Hola y haga clic en **guardar**.

    ![Autorizaciones](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Una vez que se guarda la configuración de hello, copie hello **Id. de recurso** hello y **clave de autorización**.

    ![Clave de autorización](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete una autorización de conexión**

Puede eliminar una conexión seleccionando hello **eliminar** icono en la hoja de hello para la conexión.

### <a name="circuit-user-operations"></a>Operaciones del usuario del circuito

usuario de circuito de Hello necesita Id. de recurso de hello y una clave de autorización de propietario del circuito Hola. 

**tooredeem una autorización de conexión**

1.  Haga clic en hello **+ nuevo** botón.

    ![Haga clic en Nuevo](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Busque **"Conexión"** Hola Marketplace, selecciónelo y haga clic en **crear**.

    ![Búsqueda de conexión](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Asegúrese de hello seguro **tipo de conexión** se establece demasiado "ExpressRoute".


4.  Rellene los detalles de hello, a continuación, haga clic en **Aceptar** en la hoja de conceptos básicos de Hola.

    ![Hoja Básico](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  Hola **configuración** hoja, seleccione hello **puerta de enlace de red Virtual** y comprobar hello **canjear autorización** casilla de verificación.

6.  Escriba hello **clave de autorización** hello y **del mismo nivel circuito URI** y asigne un nombre de conexión de Hola. Haga clic en **Aceptar**.

    ![Hoja Configuración](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Revise la información de Hola Hola **resumen** hoja y haga clic en **Aceptar**.


**toorelease una autorización de conexión**

Puede liberar una autorización mediante la eliminación de la conexión de Hola que vincula la red virtual del toohello de circuito ExpressRoute Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).
