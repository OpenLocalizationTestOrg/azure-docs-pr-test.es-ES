---
title: "conexión aaaHybrid con aplicación de capa 2 | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy aparatos virtuales y UDR toocreate un entorno de aplicación de varios niveles en Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>Escenario de aplicación virtual
Un escenario común entre mayor al cliente de Azure es Hola necesidad tooprovide una toohello de aplicación de dos niveles expuesto Internet, permitiendo toohello back-nivel de acceso de un centro de datos local. Este documento le guiará a través de un escenario de usuario define las rutas (UDR), una puerta de enlace VPN y toodeploy de dispositivos virtuales de red un entorno de dos niveles que cumpla Hola según los requisitos:

* Aplicación Web debe ser accesible desde Hola sólo Internet pública.
* Aplicación Hola hospedaje del servidor Web debe ser capaz de tooaccess un servidor de aplicaciones back-end.
* Todo el tráfico de la aplicación web de Internet toohello Hola debe pasar por un dispositivo virtual de firewall. Esta aplicación virtual se usará solo para el tráfico de Internet.
* Todo el tráfico encaminado toohello servidor de aplicaciones debe pasar por un dispositivo virtual de firewall. Este dispositivo virtual se usará para el servidor de acceso toohello back-end end y proceden de la red local de Hola a través de una puerta de enlace de VPN de acceso.
* Los administradores deben ser capaz de toomanage Hola firewall los accesorios virtuales desde sus equipos locales, mediante el uso de un tercer firewall dispositivo virtual que se usa exclusivamente para fines de administración.

Este es un escenario de red perimetral estándar con una red perimetral y una red protegida. Dicho escenario se puede construir en Azure con NSG, aplicaciones virtuales de firewall o una combinación de ambos elementos. tabla de Hello siguiente muestra algunas de hello pros y los contras entre los NSG y aparatos virtuales de firewall.

|  | Ventajas | Desventajas |
| --- | --- | --- |
| Grupo de seguridad de red |No tienen costo. <br/>Están integrados en Azure RBAC. <br/>Las reglas se pueden crear en plantillas ARM. |La complejidad podría variar en entornos de mayor tamaño. |
| Firewall |Control total sobre el plano de datos. <br/>Administración central a través de la consola de firewall. |El costo de la aplicación de firewall. <br/>No está integrado con Azure RBAC. |

solución de Hello siguiente utiliza firewall aparatos virtuales tooimplement un escenario de red DMZ/protegido.

## <a name="considerations"></a>Consideraciones
Puede implementar el entorno Hola explicado con anterioridad en Azure con diferentes características disponibles hoy en día, como se indica a continuación.

* **Red virtual**. Una red virtual de Azure actúa en red de local de tooan de forma similar y se puede dividir en uno o más aislamiento del tráfico de subredes tooprovide y separación de intereses.
* **Aplicación virtual**. Varios socios proporcionan dispositivos virtuales en hello Azure Marketplace que puede usarse para los tres firewalls Hola que se ha descrito anteriormente. 
* **Rutas definidas por el usuario (UDR)**. Tablas de rutas pueden contener UDRs usa Azure red toocontrol Hola el flujo de paquetes dentro de una red virtual. Estas tablas de rutas pueden ser toosubnets aplicada. Una de las características más recientes de hello en Azure es Hola capacidad tooapply un toohello de tabla de ruta GatewaySubnet, proporcionando Hola capacidad tooforward todo el tráfico que entran en hello red virtual de Azure desde un dispositivo virtual de la tooa de conexión híbrida.
* **Reenvío IP**. De forma predeterminada, hello Azure motor red reenviarán los paquetes toovirtual tarjetas de interfaz de red (NIC) solo si dirección IP de destino de paquetes de saludo coincide con direcciones IP de NIC de Hola. Por lo tanto, si un UDR define que se debe enviar un paquete tooa dado el dispositivo virtual, hello Azure motor red entraban ese paquete. paquete de saludo tooensure se entrega tooa máquina virtual (en este caso, un dispositivo virtual) que no sea el destino real de hello para el paquete de saludo, deberá tooenable el reenvío IP para dispositivo virtual Hola.
* **Grupos de seguridad de red (NSG)**. ejemplo de Hola siguiente no sirven de los NSG, pero puede usar NSG aplicados toohello subredes o NIC en esta solución toofurther filtro Hola tráfico dentro y fuera de esas subredes y la NIC.

![Conectividad de IPv6](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

En este ejemplo hay una suscripción que contiene Hola siguiente:

* 2 grupos de recursos, que no se muestra en el diagrama de Hola. 
  * **ONPREMRG**. Contiene todos los recursos toosimulate es necesario una red local.
  * **AZURERG**. Contiene todos los recursos necesarios para el entorno de red virtual de Azure Hola. 
* Una red virtual denominada **onpremvnet** utiliza toomimic segmentada de un centro de datos local como se muestra a continuación.
  * **onpremsn1**. Subred que contiene una máquina virtual (VM) que se ejecutan Ubuntu toomimic un servidor local.
  * **onpremsn2**. Subred que contiene una máquina virtual con Ubuntu toomimic en un equipo local utilizado por un administrador.
* Hay un dispositivo virtual de firewall denominado **OPFW** en **onpremvnet** utiliza toomaintain un túnel demasiado**azurevnet**.
* Una red virtual llamada **azurevnet** segmentada como se muestra a continuación.
  * **azsn1**. Subred de firewall externo utilizada exclusivamente para el servidor de seguridad externo Hola. Todo el tráfico de Internet entrará a través de esta subred. Esta subred solo contiene un servidor de seguridad NIC vinculado toohello externo.
  * **azsn2**. Subred de front-end que hospede una máquina virtual que se ejecuta como un servidor web que se obtendrá acceso desde Internet Hola.
  * **azsn3**. Subred de back-end que hospede una máquina virtual con un servidor de aplicaciones back-end que tendrán acceso al servidor de hello front-end web.
  * **azsn4**. Subred de administración utiliza exclusivamente tooprovide administración acceso tooall firewall aparatos virtuales. Esta subred contiene sólo una NIC para cada dispositivo virtual firewall utilizado en la solución de Hola.
  * **GatewaySubnet**. Subred de conexión híbrida de Azure requerida para la conectividad de tooprovide ExpressRoute y puerta de enlace VPN entre redes virtuales de Azure y otras redes. 
* Hay 3 aparatos virtuales firewall Hola **azurevnet** red. 
  * **AZF1**. Firewall externo expuesta toohello Internet pública mediante el uso de un recurso de dirección IP público de Azure. Necesita tooensure tiene una plantilla desde Hola Marketplace, o directamente desde el fabricante del dispositivo, que aprovisiona un dispositivo virtual 3 NIC.
  * **AZF2**. Firewall interno usa toocontrol tráfico entre **azsn2** y **azsn3**. También es una aplicación virtual de 3 NIC.
  * **AZF3**. Tooadministrators accesible de firewall de administración de hello centro de datos local y conectado tooa administración subred usa toomanage todos los dispositivos de firewall. Puede buscar plantillas de dispositivo virtual de 2 NIC en hello Marketplace o solicitarlo directamente desde el proveedor del dispositivo.

## <a name="user-defined-routing-udr"></a>Enrutamiento definido por el usuario (UDR)
Cada subred de Azure puede ser vinculado tooa UDR tabla utilizada toodefine cómo se enruta el tráfico iniciado en esa subred. Si no se han definido ningún UDRs, Azure usa de forma predeterminada las rutas tooallow tráfico tooflow de tooanother de una subred. toobetter comprender UDRs, visite [¿qué son rutas definidas por el usuario y el reenvío IP](virtual-networks-udr-overview.md#ip-forwarding).

tooensure comunicación se realiza a través de dispositivo de firewall derecho hello, basado en hello último requisito anterior, necesita toocreate Hola siguiente que contiene UDRs en una tabla de rutas **azurevnet**.

### <a name="azgwudr"></a>azgwudr
En este escenario, Hola solo tráfico que fluye desde tooAzure local se usa toomanage Hola firewalls conectándose demasiado**AZF3**, y que el tráfico debe pasar a través del firewall interno de hello, **AZF2**. Por lo tanto, es necesaria en hello solo una ruta **GatewaySubnet** tal y como se muestra a continuación.

| Destino | Próximo salto | Explicación |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |Permite a firewall de administración de tooreach de tráfico local **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| Destino | Próximo salto | Explicación |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |Permite la subred back-end de tráfico toohello de hospedaje de servidor de aplicación Hola a través de **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |Permite que todos los otro toobe de tráfico que se enrutan a través de **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| Destino | Próximo salto | Explicación |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |Permite el tráfico demasiado**azsn2** tooflow de servidor Web de toohello del servidor de aplicación a través de **AZF2** |

También necesita toocreate tablas de rutas para las subredes de hello en **onpremvnet** toomimic Hola centro de datos local.

### <a name="onpremsn1udr"></a>onpremsn1udr
| Destino | Próximo salto | Explicación |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |Permite el tráfico demasiado**onpremsn2** a través de **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| Destino | Próximo salto | Explicación |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |Permite la subred de tráfico toohello de seguridad en Azure a través de **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |Permite el tráfico demasiado**onpremsn1** a través de **OPFW** |

## <a name="ip-forwarding"></a>reenvío de IP
UDR y el reenvío IP son características que puede usar en el flujo del tráfico de toocontrol de combinación tooallow aparatos virtuales toobe utilizado en una red virtual de Azure.  Un dispositivo virtual es nada más que una máquina virtual que se ejecuta un aplicación que se usa el tráfico de red toohandle de alguna manera, como un firewall o un dispositivo NAT.

Este dispositivo virtual de que VM debe ser capaz de tooreceive el tráfico entrante que está dirigido no tooitself. tooallow un tráfico de tooreceive VM direccionado tooother destinos, debe habilitar el reenvío IP para hello máquina virtual. Se trata de una configuración, no es una configuración de sistema operativo de Hola de Azure. Su toorun necesidades todavía del dispositivo virtual cierta de tipo de aplicación toohandle Hola el tráfico entrante y enrutar de forma adecuada.

toolearn más información sobre el reenvío IP, visite [¿qué son rutas definidas por el usuario y el reenvío IP](virtual-networks-udr-overview.md#ip-forwarding).

Por ejemplo, imagine que tiene Hola después de la instalación en una red virtual de Azure:

* La subred **onpremsn1** contiene una máquina virtual llamada **onpremvm1**.
* La subred **onpremsn2** contiene una máquina virtual llamada **onpremvm2**.
* Un dispositivo virtual denominado **OPFW** está conectado demasiado**onpremsn1** y **onpremsn2**.
* Una ruta definida por el usuario vinculado demasiado**onpremsn1** especifica que todo el tráfico demasiado**onpremsn2** deben enviarse demasiado**OPFW**.

En este punto, si **onpremvm1** intenta tooestablish una conexión con **onpremvm2**, hello UDR se usará y el tráfico se enviará demasiado**OPFW** salto siguiente Hola. Tenga en cuenta que Hola destino paquete real no se está cambiando, sigue indicando **onpremvm2** constituye el destino de Hola. 

Sin habilitado para el reenvío de IP **OPFW**, hello Azure lógica de red virtual quitará los paquetes de saludo, ya que sólo permite paquetes toobe envía tooa VM si hello dirección IP de la máquina virtual es el destino de hello para el paquete de saludo.

Con el reenvío IP, Hola lógica de la red virtual de Azure reenviará tooOPFW de paquetes de saludo, sin cambiar su dirección de destino original. **OPFW** debe controlar los paquetes de saludo y determinar qué toodo con ellos.

Para el escenario de hello anteriormente toowork, debe habilitar el reenvío IP en hello NIC para **OPFW**, **AZF1**, **AZF2**, y **AZF3** que se utilizan para enrutamiento (todas las NIC excepto hello las toohello vinculado administración subred). 

## <a name="firewall-rules"></a>Reglas de firewall
Como se describió anteriormente, solo el reenvío IP garantiza los paquetes se envían aparatos virtuales toohello. El dispositivo sigue necesitando toodecide qué toodo con esos paquetes. En el escenario de hello anterior, necesitará hello toocreate siguiendo reglas de los dispositivos:

### <a name="opfw"></a>OPFW
OPFW representa un dispositivo local que contiene Hola siguiendo reglas:

* **Ruta**: todo el tráfico too10.0.0.0/16 (**azurevnet**) se deben enviar a través de túnel **ONPREMAZURE**.
* **Directiva**: permita todo el tráfico bidireccional entre **port2** y **ONPREMAZURE**.

### <a name="azf1"></a>AZF1
AZF1 representa una aplicación virtual de Azure que contiene Hola siguiendo reglas:

* **Directiva**: permita todo el tráfico bidireccional entre **port1** y **port2**.

### <a name="azf2"></a>AZF2
AZF2 representa una aplicación virtual de Azure que contiene Hola siguiendo reglas:

* **Ruta**: todo el tráfico too10.0.0.0/16 (**onpremvnet**) se deben enviar dirección IP de puerta de enlace de Azure toohello (es decir, 10.0.0.1) a través de **port1**.
* **Directiva**: permita todo el tráfico bidireccional entre **port1** y **port2**.

## <a name="network-security-groups-nsgs"></a>Grupos de seguridad de red (NSG)
En este escenario, no se usan los NSG. Sin embargo, podría aplicar NSG tooeach subred toorestrict tráfico entrante y saliente. Por ejemplo, podría aplicar Hola después de la subred de FW externa de toohello de reglas NSG.

**Entrante**

* Permitir todo el tráfico TCP de hello Internet tooport 80 en cualquier máquina virtual en la subred de Hola.
* Denegar todo el tráfico desde Internet Hola.

**Saliente**

* Denegar todo el tráfico toohello Internet.

## <a name="high-level-steps"></a>Pasos de alto nivel
toodeploy este escenario, seguimiento Hola pasos de alto nivel siguiente.

1. Inicio de sesión tooyour suscripción de Azure.
2. Si desea un Hola de red virtual toomimic toodeploy red local, aprovisionar recursos de Hola que forman parte de **ONPREMRG**.
3. Aprovisionar recursos de Hola que forman parte de **AZURERG**.
4. Túnel de Hola de aprovisionamiento de **onpremvnet** demasiado**azurevnet**.
5. Una vez que todos los recursos se aprovisionan, inicie sesión demasiado**onpremvm2** y la conectividad de ping 10.0.3.101 tootest entre **onpremsn2** y **azsn3**.

