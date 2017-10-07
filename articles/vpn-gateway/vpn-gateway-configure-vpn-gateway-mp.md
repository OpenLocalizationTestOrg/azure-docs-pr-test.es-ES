---
title: "Configuración de VPN Gateway: Portal de Azure clásico | Microsoft Docs"
description: "Este artículo le lleva por la configuración de la puerta de enlace de VPN de red virtual y el cambio de un tipo de enrutamiento de VPN de puerta de enlace. Estos pasos aplican toohello implementación clásica hello y modelo portal clásico."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Configurar una puerta de enlace VPN en el portal clásico de Hola 
Si desea que toocreate una conexión segura entre entornos entre Azure y su ubicación local, deberá toocreate una puerta de enlace de red virtual. Una puerta de enlace de VPN es un tipo de puerta de enlace de red virtual. En el modelo de implementación clásica de hello, una puerta de enlace VPN puede ser uno de los dos tipos de enrutamiento de VPN: estática o dinámica. Hola tipo VPN que elija depende de su plan de diseño de red tanto dispositivo VPN Hola local que desea toouse. Para obtener más información sobre dispositivos VPN, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).

**Información acerca de los modelos de implementación de Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Información general sobre la configuración
Hello pasos siguientes le guían a través de la configuración de la puerta de enlace VPN en el portal clásico de Hola. Estos pasos aplican toogateways para redes virtuales que se crearon con el modelo de implementación clásica de Hola. Actualmente, no todos los valores de configuración de Hola para puertas de enlace están disponibles en hello portal de Azure. Cuando están, se creará un nuevo conjunto de instrucciones que se aplican toohello portal de Azure.

### <a name="before-you-begin"></a>Antes de empezar
Antes de configurar la puerta de enlace, primero debe toocreate la red virtual. Para pasos toocreate una red virtual para conectividad entre entornos, consulte [configurar una red virtual con una conexión de VPN de sitio a sitio](vpn-gateway-site-to-site-create.md), o [configurar una red virtual con una conexión de VPN de punto a sitio](vpn-gateway-point-to-site-create.md). A continuación, usar hello después de puerta de enlace VPN de pasos tooconfigure Hola y de recopilar información de hello necesita tooconfigure el dispositivo VPN. 

Si ya tiene una puerta de enlace VPN y desea que el tipo de enrutamiento toochange Hola VPN, consulte [cómo toochange Hola tipo de enrutamiento de VPN para la puerta de enlace](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Creación de una puerta de enlace de VPN
1. Hola [portal de Azure clásico](https://manage.windowsazure.com), en hello **redes** , comprueba esa columna de estado de hello para la red virtual es **creado**.
2. Hola **nombre** columna, haga clic en nombre de saludo de la red virtual.
3. En hello **panel** página, tenga en cuenta que esta red virtual no tiene una puerta de enlace configurado todavía. Verá este estado a medida que avances en hello pasos tooconfigure la puerta de enlace.

![Puerta de enlace no creada](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

A continuación, en parte inferior de Hola de página de hello, haga clic en **crear puerta de enlace**. Puede seleccionar *Enrutamiento estático* o *Enrutamiento dinámico*. Hola tipo VPN de enrutamiento que seleccione depende de algunos factores. Por ejemplo, ¿qué es compatible con el dispositivo VPN y si necesita las conexiones de sitio a punto de toosupport. Comprobar [acerca de los dispositivos VPN para la conectividad de red Virtual](vpn-gateway-about-vpn-devices.md) tooverify Hola tipo de enrutamiento de VPN que necesite. Una vez creada la puerta de enlace de hello, no se puede cambiar entre los tipos de enrutamiento de VPN de puerta de enlace sin tener que eliminar y volver a crear la puerta de enlace de Hola. Cuando el sistema de hello le indique tooconfirm que desee Hola puerta de enlace creada, haga clic en **Sí**.

![Tipo de enrutamiento VPN de puerta de enlace](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Cuando está creando la puerta de enlace, observe gráfico de puerta de enlace de hello en página Hola cambia tooyellow y dice *crear puerta de enlace*. Puede tardar minutos too45 hello toocreate de puerta de enlace. Espere hasta que se complete la puerta de enlace de hello antes de poder avanzar con otras opciones de configuración.

![Creación de una puerta de enlace](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Cuando Hola cambios de puerta de enlace demasiado*conexión*, puede recopilar información de Hola que necesitará para el dispositivo VPN.

![Conexión de una puerta de enlace](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Conexiones de sitio a sitio

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Paso 1. Recopilación de información para la configuración del dispositivo VPN
Si va a crear una conexión de sitio a sitio, una vez creada la puerta de enlace de hello, recopilar información para la configuración del dispositivo VPN. Esta información se encuentra en hello **panel** página de la red virtual:

1. **Dirección IP de puerta de enlace -** dirección IP de hello puede encontrarse en hello **panel** página. No será capaz de toosee hasta después de la puerta de enlace ha terminado de crear.
2. **Clave compartida -** haga clic en **administrar clave** final Hola de pantalla de bienvenida. Haga clic en hello icono siguiente toohello clave toocopy se tooyour Portapapeles y, a continuación, pegar y Guardar clave de Hola. Este botón solo funciona cuando hay un solo túnel VPN S2S. Si tiene varios túneles VPN S2S, usar hello *Get Virtual Network Gateway Shared Key* cmdlet de PowerShell o API.

![Administrar claves](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Paso 2:  Configurar el dispositivo VPN
Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN. Mientras se no proporcionan los pasos de configuración para todos los dispositivos VPN, puede encontrar información de Hola Hola siguientes vínculos útiles:

- Para obtener más información sobre dispositivos VPN compatibles, consulte [Dispositivos VPN](vpn-gateway-about-vpn-devices.md). 
- Para valores de configuración de toodevice de vínculos, consulte [valida los dispositivos VPN](vpn-gateway-about-vpn-devices.md#devicetable). Estos vínculos se proporcionan dentro de lo posible. Siempre es mejor toocheck con el fabricante del dispositivo para obtener información de configuración más reciente Hola.
- Para obtener información sobre cómo modificar los ejemplos de configuración de dispositivo, consulte [Edición de ejemplos](vpn-gateway-about-vpn-devices.md#editing).
- Para los parámetros de IPsec/IKE, vea [Parámetros](vpn-gateway-about-vpn-devices.md#ipsec).
- Antes de configurar el dispositivo VPN, compruebe si existe alguno [los problemas de compatibilidad de dispositivo](vpn-gateway-about-vpn-devices.md#known) para dispositivo VPN de Hola que desea toouse.

Al configurar el dispositivo VPN, necesitará Hola siguientes elementos:

- Hola dirección IP pública de la puerta de enlace de red virtual. Puede buscar por van toohello **Introducción** hoja de la red virtual.
- Una clave compartida. Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio. En nuestros ejemplos, se utiliza una clave compartida muy básica. Debe generar un toouse clave más compleja.

Una vez configurado el dispositivo VPN de hello, puede ver la información de conexión actualizada en la página del panel de hello para la red virtual.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Paso 3: Verificación de los intervalos de red local y la dirección IP de puerta de enlace de VPN
#### <a name="verify-your-vpn-gateway-ip-address"></a>Verificación de la dirección IP de la puerta de enlace de VPN
Para tooconnect de puerta de enlace correctamente, dirección IP de hello para el dispositivo VPN debe configurarse correctamente para hello red Local que especificó para la configuración entre entornos. Normalmente, esto se configura durante el proceso de configuración de sitio a sitio de Hola. Sin embargo, si anteriormente usó esta red local con otro dispositivo o dirección IP de hello ha cambiado para esta red local, modificar la dirección de IP de puerta de enlace correcta de hello configuración toospecify Hola.

1. tooverify la dirección IP de puerta de enlace, haga clic en **redes** en Hola panel izquierdo del portal y, a continuación, seleccione **redes locales** al principio de Hola de página de Hola. Podrá ver Hola dirección de puerta de enlace de VPN para cada red local que ha creado. dirección IP de tooedit hello, seleccione Hola red virtual y haga clic en **editar** final Hola de página Hola.
2. En hello **especificar los detalles de la red local** página, Editar dirección IP de hello y, a continuación, haga clic en siguiente flecha de hello final Hola de página Hola.
3. En hello **especificar el espacio de direcciones de hello** página, haga clic en marca de verificación de hello en hello inferior derecho toosave su configuración.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>Comprobar los intervalos de direcciones de Hola para las redes locales
Para hello tooflow de tráfico correcto a través de la ubicación de hello puerta de enlace tooyour local, deberá tooverify que cada intervalo de direcciones IP se ha especificado. Cada intervalo debe mostrarse en la configuración de **Redes locales** de Azure. Según la configuración de red Hola de su ubicación local, esto puede ser una tarea bastante pesada. Tráfico que está limitado por una dirección IP que se encuentra dentro de los intervalos de hello enumerado se enviará a través de puerta de enlace VPN de red virtual de Hola. Hola intervalos que indique no tienen intervalos privados toobe, aunque es conveniente tooverify que puede recibir la configuración local Hola tráfico entrante.

intervalos de hello tooadd o edición de una red Local, use Hola pasos:

1. intervalos de direcciones IP tooedit de Hola para una red local, haga clic en **redes** en Hola panel izquierdo del portal y, a continuación, seleccione **redes locales** al principio de Hola de página de Hola. En el portal de hello, hello más fácil manera tooview Hola intervalos que ha enumerado es en hello **editar** página. toosee los intervalos, seleccione Hola red virtual y haga clic en **editar** final Hola de página Hola.
2. En hello **especificar los detalles de la red local** página, no realiza ningún cambio. Haga clic en la flecha siguiente de hello en parte inferior de Hola de página Hola.
3. En hello **especificar el espacio de direcciones de hello** página, realice los cambios de espacio de dirección de red. A continuación, haga clic en toosave de marca de verificación de hello, su configuración.

## <a name="how-tooview-gateway-traffic"></a>Cómo el tráfico de puerta de enlace de tooview
Puede ver la puerta de enlace y el tráfico de la puerta de enlace desde la página **Panel** de la red virtual.

En hello **panel** página puede ver Hola siguiente:

* cantidad de Hola de datos que se envíen a través de la puerta de enlace, datos y datos de salida.
* nombres de Hola de servidores DNS de Hola que se especifican para la red virtual.
* conexión de Hello entre la puerta de enlace y el dispositivo VPN.
* Hola comparten clave tooconfigure usa el dispositivo VPN de puerta de enlace conexión tooyour.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>¿Cómo toochange Hola tipo de enrutamiento de VPN para la puerta de enlace
Dado que algunas configuraciones de conectividad solo están disponibles para ciertos tipos de enrutamiento de puerta de enlace, es posible que necesite toochange Hola puerta de enlace VPN tipo de enrutamiento de puerta de enlace VPN existente. Por ejemplo, puede que desee tooadd conectividad punto a sitio tooan ya sitio a sitio conexión existente que tiene una puerta de enlace estática. Las conexiones de punto a sitio requieren una puerta de enlace dinámica. Esto significa que tooconfigure una conexión P2S, tendrá que toochange el tipo de enrutamiento de VPN de puerta de enlace de toodynamic estático.

Si necesita toochange un tipo de enrutamiento de VPN de puerta de enlace, podrá eliminar la puerta de enlace existente de hello y, a continuación, crear una nueva puerta de enlace con el nuevo tipo de enrutamiento Hola. No es necesario toodelete Hola toda la red virtual toochange Hola puerta de enlace tipo de enrutamiento.

Antes de cambiar el tipo de enrutamiento de VPN de puerta de enlace, ser tooverify seguro de que el dispositivo VPN es compatible con tipo de enrutamiento de Hola que desea toouse. ejemplos de configuración de enrutamiento nuevo de toodownload y comprobación de requisitos del dispositivo VPN, consulte [acerca de los dispositivos VPN para la conectividad de red Virtual](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Cuando se elimina una puerta de enlace VPN de red virtual, se libera Hola VIP asignada toohello puerta de enlace. Cuando se vuelve a crear la puerta de enlace de hello, una nueva VIP se asigna tooit.
> 
> 

1. **Elimine la puerta de enlace VPN existente Hola.**
   
    En hello **panel** página de la red virtual, navegue toohello inferior de la página de Hola y haga clic en **eliminar puerta de enlace**. Espere la notificación de Hola Hola puerta de enlace se ha eliminado. Una vez que reciba notificaciones de hello en pantalla de bienvenida que se ha eliminado la puerta de enlace, puede crear una nueva puerta de enlace.
2. **Cree una puerta de enlace de VPN.**
   
    Utilice el procedimiento de hello en parte superior de Hola de hello página toocreate una nueva puerta de enlace: [crear una puerta de enlace VPN](#create-a-vpn-gateway).

## <a name="next-steps"></a>Pasos siguientes
Puede agregar la red virtual de máquinas virtuales tooyour. Vea [cómo toocreate una máquina virtual personalizada](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Si desea que la conexión de tooconfigure un point-to-site VPN, consulte [configurar una conexión VPN punto a sitio](vpn-gateway-point-to-site-create.md).

