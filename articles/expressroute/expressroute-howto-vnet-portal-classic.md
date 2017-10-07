---
title: "aaaConfigure una red Virtual y puerta de enlace para ExpressRoute en Hola portal clásico | Documentos de Microsoft"
description: "Este artículo le guiará a través de configuración de una red virtual para ExpressRoute con el modelo de implementación clásica de Hola y el portal clásico de Hola."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Crear una red Virtual para ExpressRoute en portal clásico de Hola
pasos de Hello en este artículo le guiará a través de configuración de una red virtual y una puerta de enlace de red virtual para su uso con ExpressRoute mediante el modelo de implementación clásica de Hola y el portal clásico de Hola.

Si desea instrucciones para el modelo de implementación del Administrador de recursos de hello, puede usar Hola siguientes artículos: [crear una red virtual mediante PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md) y [agregar un administrador de recursos VNet tooa de puerta de enlace VPN para ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Información sobre los modelos de implementación de Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>Creación de una red virtual y puerta de enlace clásicas
Hello pasos siguientes crea una red virtual clásica y una puerta de enlace de red virtual. Si ya tiene una red virtual clásica, vea hello [configurar una red virtual clásica existente](#config) sección en este artículo.

1. Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com).
2. En hello esquina inferior izquierda de la pantalla de bienvenida, haga clic en **nuevo**. En el panel de navegación de hello, haga clic en **servicios de red**y, a continuación, haga clic en **red Virtual**. Haga clic en **creación personalizada** Asistente de configuración de toobegin Hola.
3. En hello **detalles de red Virtual** página, escriba Hola siguiente:
   
   * **Nombre** : nombre de la red virtual. Usará este nombre de red virtual al implementar las instancias de máquinas virtuales y PaaS, por lo que no puede toomake nombre de hello sea muy complicado.
   * **Ubicación** : Hola ubicación es toohello está directamente relacionado física (región) donde desea que su tooreside de recursos (máquinas virtuales). Por ejemplo, si desea que las máquinas virtuales de hello implementar toobe de red virtual toothis ubicado físicamente en este de EE., seleccione esa ubicación. No se puede cambiar la región de hello asociada a la red virtual después de haberlo creado.
4. En hello **servidores DNS y conectividad VPN** página, escriba Hola siguiente información y, a continuación, haga clic en hello flecha siguiente en la esquina inferior derecha de Hola. 
   
   * **Servidores DNS** : escriba el nombre del servidor DNS de Hola y la dirección IP, o seleccione un servidor DNS previamente registrado en menú contextual de Hola. Mediante este valor no se crea un servidor DNS. Permite a toospecify los servidores DNS Hola que quiere toouse de resolución de nombres para esta red virtual.
   * **Conectividad de sitio a sitio** : seleccione esta opción Hola casilla **configurar una VPN de sitio a sitio**.
   * **ExpressRoute** : seleccione Hola casilla **usar ExpressRoute**. Esta opción solo aparece si seleccionó **Configurar una VPN de sitio a sitio**.
   * **Red local** -son toohave requiere un sitio de red local para ExpressRoute. Sin embargo, en caso de hello de una conexión ExpressRoute, prefijos de direcciones de hello especificado para hello local se omitirá el sitio de red. En su lugar, los prefijos de direcciones de hello anuncian tooMicrosoft a través de hello circuito de ExpressRoute se usará para fines de enrutamiento.<BR>Si ya tiene una red local creada para la conexión ExpressRoute, puede seleccionar en lista desplegable de Hola. En caso contrario, seleccione **Especifique una nueva red local**.
5. Hola **conectividad de sitio a sitio** página aparece si se seleccionó toospecify una nueva red local en el paso anterior de Hola. tooconfigure la red local, escriba Hola siguiente información y, a continuación, haga clic en la flecha siguiente Hola. 
   
   * **Nombre de** -nombre de Hola que desea toocall local (local) el sitio de red.
   * **Espacio de direcciones** : incluidas la dirección IP de inicio y el CIDR (recuento de direcciones). Puede especificar cualquier intervalo de direcciones mientras no se superponga con el intervalo de direcciones de hello para la red virtual. Normalmente, esto debería especificar intervalos de direcciones de Hola para las redes locales, pero en caso de hello de ExpressRoute, no se utiliza esta configuración. Sin embargo, esta configuración es necesaria en la red local de order toocreate hello cuando utilizas el portal clásico de Hola.
   * **Agregar espacio de direcciones** : este ajuste no es relevante para ExpressRoute.
6. En hello **espacios de direcciones de red Virtual** página, escriba Hola siguiente información y, a continuación, haga clic en marca de verificación de hello en hello inferior derecho tooconfigure la red. 
   
   * **Espacio de direcciones** : incluidas la dirección IP de inicio y el recuento de direcciones. Compruebe que los espacios de direcciones de hello especificados no superponen con cualquiera de los espacios de direcciones de Hola que existen en la red local.
   * **Agregar subred** : incluidas Dirección IP de inicio y Recuento de direcciones. No se necesitan subredes adicionales.
   * **Agregar subred de puerta de enlace** -haga clic en la subred de puerta de enlace de tooadd Hola. subred de puerta de enlace de Hola se usa solo para la puerta de enlace de red virtual de Hola y es necesario para esta configuración.<BR>Hola subred CIDR (recuento de direcciones) de puerta de enlace para ExpressRoute debe ser/28 o superior (/ 27/26 etcetera.). Esto permite suficientes direcciones IP en ese toowork de configuración de subred tooallow Hola. En el portal clásico de hello, si ha seleccionado la casilla de verificación de hello toouse ExpressRoute, portal de hello especifica una subred de puerta de enlace con /28.  No se puede ajustar el recuento de direcciones CIDR de hello en el portal clásico de Hola. subred de puerta de enlace de Hello aparecerá como **puerta de enlace** en portal clásico de hello, aunque hello nombre real de la subred de puerta de enlace de Hola que se crea es realmente **GatewaySubnet**. Puede ver este nombre mediante el uso de PowerShell o en hello portal de Azure.
7. Haga clic en Hola marca de verificación en la parte inferior de Hola de página de Hola y empezará a la red virtual toocreate. Cuando finalice, verá **creado** aparecen en **estado** en hello **redes** página del portal clásico de Hola.

## <a name="gw"></a>Crear puerta de enlace de Hola
1. En hello **redes** página, haga clic en red virtual Hola recién creado, haga clic en **panel** al principio de Hola de página de Hola.
2. En parte inferior de Hola de hello **panel** página, haga clic en **crear puerta de enlace** y seleccione **enrutamiento dinámico**. Haga clic en **Sí** tooconfirm que desea toocreate una puerta de enlace.
3. Cuando la puerta de enlace de hello comienza a crear, verá un mensaje informándole de que esa puerta de enlace de Hola se ha iniciado. Puede tardar minutos too45 hello toocreate de puerta de enlace.
4. Vincule el circuito de tooa de red. Siga las instrucciones de hello en el artículo hello [cómo toolink redes virtuales tooExpressRoute circuitos](expressroute-howto-linkvnet-classic.md).

## <a name="config"></a>Configuración de una red virtual clásica existente para ExpressRoute
Si ya tiene una red virtual clásica, puede configurarlo tooconnect tooExpressRoute en portal clásico de Hola. configuración de Hola se Hola igual como secciones de hello anteriores, por lo que lea esas toobecome secciones familiarizado con hello requiere configuración. Si desea toocreate una conexión coexistentes ExpressRoute/sitio a sitio, consulte [este artículo](expressroute-howto-coexist-classic.md) para conocer los pasos Hola. Son diferentes de hello los pasos de este artículo.

1. Red local de toocreate Hola es necesario para actualizar el resto de hello de la configuración de red virtual. Haga clic en una nueva red local, que es necesaria al configurar ExpressRoute a través del portal clásico de hello, de toocreate **New**  **>**  **servicios de red**  **>**  **Red virtual**  **>**  **red local agregar**. Siga Hola Asistente toocreate pasos Hola red local.
2. Use **configurar** página rest de hello tooupdate de valores de hello para la red virtual y tooassociate Hola red virtual toohello red local.
3. Después de establecer la configuración de hello, continúe toohello [crear puerta de enlace de hello](#gw) sección de esta puerta de enlace de artículo toocreate Hola.

## <a name="next-steps"></a>Pasos siguientes
* Si desea que la red virtual del tooyour tooadd máquinas virtuales, consulte [máquinas virtuales de las rutas de acceso de aprendizaje](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/).
* Si desea más información sobre ExpressRoute toolearn, vea hello [ExpressRoute Overview](expressroute-introduction.md).

