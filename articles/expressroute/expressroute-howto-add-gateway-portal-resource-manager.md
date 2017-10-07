---
title: 'Agregar un tooa de puerta de enlace de red virtual red virtual para ExpressRoute: Portal: Azure | Documentos de Microsoft'
description: "En este artículo se explica cómo agregar un tooan de puerta de enlace de red virtual ya creado el Administrador de recursos VNet para ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Configurar una puerta de enlace de red virtual para ExpressRoute con hello portal de Azure
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Clásico: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Este artículo le guiará a través de hello pasos tooadd una puerta de enlace de red virtual para una red virtual existente. Este artículo le guiará a través de hello pasos tooadd, cambiar el tamaño y quitar una puerta de enlace de red virtual (VNet) para una red virtual existente. pasos de Hola para esta configuración son específicos para redes virtuales que se crearon con el modelo de implementación de administrador de recursos de Hola que se usará en una configuración de ExpressRoute. Para obtener más información acerca de las puertas de enlace de red virtual y la configuración de puerta de enlace para ExpressRoute, consulte [Acerca de las puertas de enlace de red virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Antes de comenzar

pasos de Hola para esta tarea, use una red virtual basan en valores Hola Hola después de la lista de referencias de configuración. Usamos esta lista en nuestros pasos de ejemplo. Puede copiar hello toouse de lista como referencia, reemplazando los valores de hello con sus propios.

**Lista de referencia de configuración**

* Nombre de red virtual = "TestVNet"
* Espacio de direcciones de red virtual = 192.168.0.0/16
* Nombre de subred = "FrontEnd" 
    * Espacio de direcciones de subred = "192.168.1.0/24"
* Grupo de recursos: "TestRG"
* Ubicación: = "East US"
* Nombre de subred de puerta de enlace: "GatewaySubnet" (siempre debe asignar a las subredes de puerta de enlace el nombre *GatewaySubnet*).
    * Espacio de direcciones de subred de puerta de enlace = "192.168.200.0/26"
* Nombre de puerta de enlace = "ERGW"
* Nombre de IP de puerta de enlace = "MyERGWVIP"
* Tipo de puerta de enlace = "ExpressRoute" (Este tipo es obligatorio para una configuración de ExpressRoute).
* Nombre de IP pública de puerta de enlace = "MyERGWVIP"

Puede ver un [vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) de estos pasos antes de comenzar la configuración.

## <a name="create-hello-gateway-subnet"></a>Crear una subred de puerta de enlace de Hola

1. Hola [portal](http://portal.azure.com), navegar por la red virtual del Administrador de recursos toohello que se desea toocreate una puerta de enlace de red virtual.
2. Hola **configuración** sección de la hoja de la red virtual, haga clic en **subredes** hoja de subredes de tooexpand Hola.
3. En hello **subredes** hoja, haga clic en **+ subred de puerta de enlace** tooopen hello **Agregar subred** hoja. 
   
    ![Agregar subred de puerta de enlace de hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Agregar subred de puerta de enlace de Hola")


4. Hola **nombre** para la subred se rellena automáticamente con hello valor "GatewaySubnet". Este valor es necesario en orden para la subred de Azure toorecognize hello como subred de puerta de enlace de Hola. Ajustar el relleno automático de hello **intervalo de direcciones** valores toomatch sus requisitos de configuración. Se recomienda crear una subred de puerta de enlace con un /27 o superior (/ 26, / 25, etc.). A continuación, haga clic en **Aceptar** toosave Hola valores y crear una subred de puerta de enlace de Hola.

    ![Agregar subred de hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "agregando la subred de Hola")

## <a name="create-hello-virtual-network-gateway"></a>Crear puerta de enlace de red virtual de Hola

1. En el portal de hello, en el lado izquierdo de hello, haga clic en  **+**  y escriba 'Puerta de enlace de red Virtual' en la búsqueda. Busque **puerta de enlace de red Virtual** en búsqueda de hello devolver y haga clic en la entrada de Hola. En hello **puerta de enlace de red Virtual** hoja, haga clic en **crear** final Hola de hoja de Hola. Se abrirá hello **crear puerta de enlace de red virtual** hoja.
2. En hello **crear puerta de enlace de red virtual** hoja, rellene los valores de hello para la puerta de enlace de red virtual.

    ![Campos de la hoja Create virtual network gateway (Crear puerta de enlace de red virtual)](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Campos de la hoja Create virtual network gateway (Crear puerta de enlace de red virtual)")
3. **Nombre**: asigne un nombre a la puerta de enlace. Esto es no Hola igual que una subred de puerta de enlace. Nombre de Hola de objeto de la puerta de enlace de Hola que está creando del.
4. **Tipo de puerta de enlace**: seleccione **ExpressRoute**.
5. **SKU**: puerta de enlace de hello seleccione SKU de la lista desplegable de Hola.
6. **Ubicación**: ajustar hello **ubicación** campo toopoint toohello ubicación donde se encuentra la red virtual. Si la ubicación de hello no señala región toohello donde reside la red virtual, red virtual de hello no aparece en hello 'Elegir una red virtual' desplegable.
7. Elija hello toowhich de red virtual que desee tooadd esta puerta de enlace. Haga clic en **red Virtual** tooopen hello **elegir una red virtual** hoja. Seleccione Hola red virtual. Si no ve la red virtual, que seguro Hola **ubicación** campo apunta región toohello en el que se encuentra la red virtual.
9. Elija una dirección IP pública. Haga clic en **dirección IP pública** tooopen hello **Elegir dirección IP pública** hoja. Haga clic en **+ crear nuevos** tooopen hello **crear módulo de dirección IP pública**. Escriba un nombre para la dirección IP pública. Esta hoja crea un toowhich de objeto de la dirección IP pública que se asignará dinámicamente una dirección IP pública. Haga clic en **Aceptar** toosave la hoja de toothis de cambios.
10. **Suscripción**: Compruebe que Hola correcto está seleccionada la suscripción.
11. **Grupo de recursos**: este valor viene determinado por hello red Virtual que seleccionó.
12. No ajustar hello **ubicación** después de que haya especificado la configuración anterior de Hola.
13. Compruebe la configuración de Hola. Si desea que su tooappear de puerta de enlace en el panel de hello, puede seleccionar **toodashboard Pin** final Hola de hoja de Hola.
14. Haga clic en **crear** toobegin crear puerta de enlace de Hola. configuración de Hola se validan y puerta de enlace de hello implementa. Crear puerta de enlace de red virtual puede tardar hasta too45 minutos toocomplete.

## <a name="next-steps"></a>Pasos siguientes
Después de haber creado la puerta de enlace de red virtual de hello, puede vincular el circuito de ExpressRoute de tooan de red virtual. Vea [vincular un circuito de ExpressRoute de red Virtual tooan](expressroute-howto-linkvnet-portal-resource-manager.md).
