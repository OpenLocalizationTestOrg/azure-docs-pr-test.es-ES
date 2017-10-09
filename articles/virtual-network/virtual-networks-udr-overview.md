---
title: "rutas definidas por el aaaUser y el reenvío IP en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las rutas definidas por el usuario de tooconfigure (UDR) y el reenvío IP tooforward tráfico toonetwork aparatos virtuales en Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Rutas definidas por el usuario y reenvío IP

Cuando se agrega la red virtual de máquinas virtuales (VM) tooa (VNet) en Azure, observará que hello las máquinas virtuales son capaz de toocommunicate entre sí a través de la red hello, automáticamente. No es necesario toospecify una puerta de enlace, incluso aunque hello las máquinas virtuales están en subredes diferentes. Hello mismo sirve para la comunicación de hello las máquinas virtuales toohello Internet pública y la red local de tooyour incluso cuando el propietario de una conexión híbrida de Azure tooyour centro de datos está presente.

Este flujo de comunicación es posible porque Azure utiliza una serie de sistema rutas toodefine cómo fluye el tráfico IP. Las rutas del sistema controlan el flujo de Hola de comunicación en hello los escenarios siguientes:

* Desde Hola misma subred.
* Desde un tooanother de subred dentro de una red virtual.
* Desde máquinas virtuales toohello Internet.
* Desde una red virtual tooanother red virtual a través de una puerta de enlace VPN.
* Desde una red virtual a través de intercambio de tráfico de red virtual (encadenamiento de servicio) de red virtual tooanother.
* Desde una red de en entornos de red virtual tooyour a través de una puerta de enlace VPN.

Hola siguiente ilustración muestra una configuración simple con una red virtual y dos subredes, algunas máquinas virtuales, junto con hello las rutas de sistema que permiten tooflow de tráfico IP.

![Rutas del sistema de Azure](./media/virtual-networks-udr-overview/Figure1.png)

Aunque el uso de Hola de rutas del sistema facilita tráfico automáticamente para su implementación, hay casos en que desea toocontrol Hola enrutamiento de paquetes a través de un dispositivo virtual. Puede por lo tanto mediante la creación de rutas definidas por el usuario especificar próximo salto Hola para los paquetes que fluyen tooa dispositivo virtual de subred específica toogo tooyour en su lugar, y habilitar IP Hola el reenvío de máquina virtual que ejecuta como dispositivo virtual Hola.

Hola figura siguiente muestra un ejemplo de rutas definidas por el usuario y reenvío tooforce paquetes IP enviados tooone subred desde otro toogo a través de un dispositivo virtual en una subred terceros.

![Rutas del sistema de Azure](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Las rutas definidas por el usuario son aplicado tootraffic salir de una subred de cualquier recurso (como interfaces de red conexión tooVMs) en la subred de Hola. No se puede crear rutas toospecify cómo el tráfico entra en una subred de hello Internet, por ejemplo. dispositivo de Hola que va a reenviar tráfico toocannot estar Hola misma subred donde se origina el tráfico de Hola. Recuerde siempre crear una subred independiente para sus aplicaciones. 
> 
> 

## <a name="route-resource"></a>Recurso de ruta
Los paquetes se enrutan a través de una red TCP/IP basada en una tabla de ruta definida en cada nodo de red física de Hola. Una tabla de ruta es que una colección de rutas individuales utilizados toodecide donde tooforward paquetes basan en el destino de hello dirección IP. Una ruta consta de siguientes hello:

| Propiedad | Description | Restricciones | Consideraciones |
| --- | --- | --- | --- |
| Prefijo de dirección |ruta de Hello destino CIDR toowhich Hola se aplica, como 10.1.0.0/16. |Debe ser un intervalo válido de CIDR que representa las direcciones en hello red pública de Internet, red virtual de Azure o centro de datos local. |Asegúrese de hello seguro **prefijo de dirección** no contiene la dirección de Hola para hello **de próximo salto**, en caso contrario, deberá especificar los paquetes en un bucle que se va de próximo salto de hello origen toohello sin que se alcance nunca destino de Hola. |
| Tipo de próximo salto |tipo Hello de paquete de saludo de salto de Azure se enviarán a. |Debe ser uno de hello siguientes valores: <br/> **Red virtual**. Representa la red virtual local de Hola. Por ejemplo, si tiene dos subredes, 10.1.0.0/16 y 10.2.0.0/16 en Hola misma red virtual, ruta de Hola para cada subred de la tabla de rutas de hello tendrá un valor de salto siguiente de *red Virtual*. <br/> **Puerta de enlace de red virtual**. Representa una puerta de enlace de VPN S2S de Azure. <br/> **Internet**. Representa Hola Internet puerta de enlace proporcionado por hello infraestructura de Azure. <br/> **Dispositivo virtual**. Representa un dispositivo virtual que se ha agregado tooyour red virtual de Azure. <br/> **Ninguna**. Representa un agujero negro. Paquetes reenviados tooa negras no se reenviarán en absoluto. |Considere el uso de **dispositivo Virtual** toodirect tráfico tooa máquina virtual o equilibrador de carga Azure dirección IP interna.  Este tipo permite la especificación de Hola de una dirección IP, tal y como se describe a continuación. Considere el uso de un **ninguno** escriba toostop paquetes de flujo tooa dado de destino. |
| Siguiente dirección de salto |dirección del próximo salto Hello contiene la dirección IP de Hola se deberían reenviar paquetes. Los valores de salto siguientes solo se permiten en rutas donde es el tipo de próximo salto hello *dispositivo Virtual*. |Debe ser una dirección IP que sea accesible dentro de hello red Virtual que se aplica Hola ruta definida por el usuario, sin tener que pasar a través de un **puerta de enlace de red Virtual**. dirección IP de Hello tiene toobe en hello mismo Virtual de red donde se aplica, o en una red Virtual peered. |Si la dirección IP de hello representa una máquina virtual, asegúrese de habilitar [reenvío IP](#IP-forwarding) en Azure para hello máquina virtual. Si hello representa Hola interno dirección IP del equilibrador de carga de Azure, asegúrese de que tiene una regla para cada puerto de equilibrio de carga correspondiente que se va a equilibrar tooload.|

En Azure PowerShell algunos de los valores de "NextHopType" hello tienen nombres diferentes:

* Red virtual es VnetLocal
* Puerta de enlace de red virtual es VirtualNetworkGateway
* Aplicación virtual es VirtualAppliance
* Internet es Internet
* No es None

### <a name="system-routes"></a>Rutas del sistema
Cada subred que se crea en una red virtual se asocia automáticamente con una tabla de ruta que contiene Hola siguiendo las reglas de ruta del sistema:

* **Regla de red virtual local**: esta regla se crea automáticamente para cada subred de una red virtual. Especifica que no hay un vínculo directo entre máquinas virtuales de Hola Hola red virtual y no hay ningún salto siguiente intermedio.
* **Regla local**: esta regla se aplica el intervalo de direcciones de tooall tráfico destinado toohello local y utiliza la puerta de enlace VPN como destino de salto siguiente Hola.
* **Regla de Internet**: esta regla controla todos los toohello de tráfico destinado a Internet pública (prefijo de dirección 0.0.0.0/0) y usos de puerta de enlace de internet de infraestructura hello como Hola del próximo salto para todo el tráfico destinado toohello Internet.

### <a name="user-defined-routes"></a>Rutas definidas por el usuario
Para la mayoría de los entornos solo tendrá que las rutas de sistema de hello ya están definidas por Azure. Sin embargo, puede necesita toocreate una tabla de rutas y agregar una o más rutas en casos concretos, como:

* Forzar túnel toohello Internet a través de la red local.
* Uso de dispositivos virtuales en el entorno de Azure.

En escenarios de hello anteriores, tendrá toocreate una tabla de rutas y agregar tooit de rutas definidas por el usuario. Puede tener varias tablas de rutas y hello misma tabla de ruta puede ser tooone asociado o más subredes. Y cada subred sólo puede ser una tabla de rutas solo tooa asociado. Todas las máquinas virtuales y servicios en la nube en una subred usan Hola ruta las tablas asociadas toothat subred.

Subredes se basan en las rutas del sistema hasta que una tabla de rutas se subred toohello asociado. Una vez creada una asociación, el enrutamiento se realiza según la coincidencia de prefijo más larga (LPM) entre las rutas definidas por el usuario y las rutas predeterminadas. Si hay más de una ruta con hello coincide con el mismo LPM, a continuación, se selecciona una ruta se basa en su origen en hello siguiente orden:

1. Ruta definida por el usuario
2. Ruta BGP (cuando se utiliza ExpressRoute)
3. Ruta del sistema

toolearn toocreate usuario definición de rutas, vea [cómo tooCreate enruta y habilitar el reenvío IP en Azure](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> Las rutas definidas por el usuario son solo aplicada tooAzure máquinas virtuales y servicios en la nube. Por ejemplo, si desea que tooadd un dispositivo virtual de firewall entre la red local y Azure, tendrá toocreate una ruta definida por el usuario para las tablas de enrutamiento de Azure que reenvía todo el tráfico encaminado toohello de espacio de direcciones de toohello local virtual dispositivo. También puede agregar definida por el usuario ruta (UDR) toohello GatewaySubnet tooforward todo el tráfico de tooAzure de local a través del dispositivo virtual Hola. Esta es una incorporación reciente.
> 
> 

### <a name="bgp-routes"></a>Rutas BGP
Si tiene una conexión de ExpressRoute entre la red local y Azure, puede habilitar las rutas BGP toopropagate desde su tooAzure de red local. Estas rutas BGP se usan en hello igual que las rutas del sistema y el usuario define las rutas en cada subred de Azure. Para obtener más información, consulte [Introducción a ExpressRoute](../expressroute/expressroute-introduction.md).

> [!IMPORTANT]
> Puede configurar su entorno de Azure toouse aplicar el túnel forzado a través de la red local mediante la creación de una ruta definida por el usuario para 0.0.0.0/0 de subred que utiliza la puerta de enlace VPN de hello como próximo salto de Hola. Sin embargo, esto solo funciona si se utiliza una puerta de enlace de VPN, no ExpressRoute. Para ExpressRoute, la tunelización forzada se configura a través de BGP.
> 
> 

## <a name="ip-forwarding"></a>Reenvío IP
Como se describió anteriormente, uno de hello razones principales toocreate una ruta definida por el usuario es dispositivo virtual de tooforward tráfico tooa. Un dispositivo virtual es nada más que una máquina virtual que se ejecuta un aplicación que se usa el tráfico de red toohandle de alguna manera, como un firewall o un dispositivo NAT.

Este dispositivo virtual de que VM debe ser capaz de tooreceive el tráfico entrante que está dirigido no tooitself. tooallow un tráfico de tooreceive VM direccionado tooother destinos, debe habilitar el reenvío IP para hello máquina virtual. Se trata de una configuración, no es una configuración de sistema operativo de Hola de Azure.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[crear rutas en el modelo de implementación del Administrador de recursos de hello](virtual-network-create-udr-arm-template.md) y asociarlos toosubnets. 
* Obtenga información acerca de cómo demasiado[crear rutas en el modelo de implementación clásica de hello](virtual-network-create-udr-classic-ps.md) y asociarlos toosubnets.

