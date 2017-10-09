---
title: 'Agregar varios tooa de conexiones de sitio a sitio de la puerta de enlace VPN red virtual: Portal de Azure: Administrador de recursos | Documentos de Microsoft'
description: "Agregar varios sitio S2S conexiones tooa puerta de enlace VPN que tiene una conexión existente"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Agregar una tooa de conexión de sitio a sitio red virtual con una conexión de puerta de enlace VPN existente

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (clásico)](vpn-gateway-multi-site.md)
>
> 

Este artículo le guiará a través de hello tooadd portal Azure sitio a sitio (S2S) conexiones tooa puerta de enlace VPN que tiene una conexión existente. Este tipo de conexión es a menudo tooas que se hace referencia una configuración de "varios sitio". Puede agregar una tooa de conexión de S2S red virtual que ya tiene una conexión de S2S, la conexión de punto a sitio o la conexión de red virtual a red virtual. Existen algunas limitaciones al agregar conexiones. Comprobar hello [antes de comenzar](#before) sección en este artículo de tooverify antes de iniciar la configuración. 

En este artículo se aplica tooVNets creados mediante el modelo de implementación del Administrador de recursos de Hola que tienen una puerta de enlace de VPN RouteBased. Estos pasos no aplican las configuraciones de conexión coexistentes tooExpressRoute/sitio a sitio. Consulte [conexiones coexistentes de ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) para obtener información sobre las conexiones coexistentes.

### <a name="deployment-models-and-methods"></a>Modelos de implementación y métodos
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Esta tabla se actualiza cada vez que hay nuevos artículos y nuevas herramientas disponibles para esta configuración. Cuando un artículo está disponible, vinculamos directamente tooit de esta tabla.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Antes de empezar
Comprobar Hola siguientes elementos:

* No está creando una conexión coexistente ExpressRoute/S2S.
* Tener una red virtual que se creó mediante el modelo de implementación del Administrador de recursos de hello con una conexión existente.
* puerta de enlace de red virtual de Hello para la red virtual es RouteBased. Si tiene una puerta de enlace PolicyBased VPN, debe eliminar la puerta de enlace de red virtual de Hola y crear una nueva puerta de enlace VPN como del tipo routebased..
* Ninguno de los intervalos de direcciones de Hola se superponen para cualquiera de hello redes virtuales que se está conectando a esta red virtual.
* Dispondrá de dispositivo VPN compatible y alguna persona tooconfigure capaz de él. Consulte [Acerca de los dispositivos VPN para conexiones de red virtual de sitio a sitio](vpn-gateway-about-vpn-devices.md). Si no está familiarizado con la configuración de dispositivo VPN, o si está familiarizado con los intervalos de direcciones IP de hello ubicados en la configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted.
* Tiene una dirección IP pública externa para el dispositivo VPN. Esta dirección IP no puede estar detrás de un NAT.

## <a name="part1"></a>Parte 1: Configuración de una conexión
1. Desde un explorador, navegue toohello [portal de Azure](http://portal.azure.com) y, si es necesario, inicie sesión con su cuenta de Azure.
2. Haga clic en **todos los recursos** y busque el **puerta de enlace de red virtual** de lista de Hola de recursos y haga clic en él.
3. En hello **puerta de enlace de red Virtual** hoja, haga clic en **conexiones**.
   
    ![Hoja de conexiones](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Hoja de conexiones")<br>
4. En hello **conexiones** hoja, haga clic en **+ agregar**.
   
    ![Botón de agregar conexión](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "botón de agregar conexión")<br>
5. En hello **Agregar conexión** hoja, rellene Hola siguientes campos:
   
   * **Nombre:** nombre hello desea toogive toohello sitio va a crear la conexión de Hola a.
   * **Tipo de conexión:** seleccione **Sitio a sitio (IPsec)**.
     
     ![Agregar hoja de conexión](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "hoja de agregar conexión")<br>

## <a name="part2"></a>Parte 2: Agregar una puerta de enlace de red local
1. Haga clic en **Puerta de enlace de red local** ***Elegir una puerta de enlace de red local***. Se abrirá hello **puerta de enlace de red local elija** hoja.
   
    ![Puerta de enlace de red local elija](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "elegir puerta de enlace de red local")<br>
2. Haga clic en **crear nuevo** tooopen hello **crear puerta de enlace de red local** hoja.
   
    ![Hoja de puerta de enlace de red local crear](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "crear puerta de enlace de red local")<br>
3. En hello **crear puerta de enlace de red local** hoja, rellene Hola siguientes campos:
   
   * **Nombre:** nombre hello desea recurso de puerta de enlace de red local de toogive toohello.
   * **Dirección IP:** Hola dirección IP pública del dispositivo VPN de hello en el sitio de Hola que desee tooconnect a.
   * **Espacio de direcciones:** espacio de direcciones de Hola que desea toobe enruta toohello nuevo sitio de red local.
4. Haga clic en **Aceptar** en hello **crear puerta de enlace de red local** cambios de hoja toosave Hola.

## <a name="part3"></a>Parte 3: Agregar clave compartida de Hola y crear la conexión de Hola
1. En hello **Agregar conexión** hoja, Agregar clave compartida de Hola que desea toouse toocreate la conexión. Puede obtener una clave compartida Hola desde su dispositivo VPN, o crear uno aquí y, a continuación, configurar su Hola de toouse del dispositivo VPN misma clave compartida. Hola importante que es que las claves de hello son exactamente Hola igual.
   
    ![Clave compartida](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Clave compartida")<br>
2. En la parte inferior de Hola de hoja de hello, haga clic en **Aceptar** conexión de hello toocreate.

## <a name="part4"></a>Parte 4: comprobar la conexión de VPN de Hola


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Ver máquinas virtuales de hello [ruta de acceso de aprendizaje](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) para obtener más información.
