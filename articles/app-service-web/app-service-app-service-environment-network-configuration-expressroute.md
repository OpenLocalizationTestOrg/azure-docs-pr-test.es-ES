---
title: "aaaNetwork detalles de configuración para trabajar con Express Route"
description: "Detalles de configuración de red para ejecutar entornos del servicio de aplicación en una red Virtual conectado tooan circuito de ExpressRoute."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>Detalles de configuración de red para entornos del Servicio de aplicaciones con ExpressRoute
## <a name="overview"></a>Información general
Los clientes pueden conectarse un [ExpressRoute de Azure] [ ExpressRoute] infraestructura de red virtual de circuito tootheir, lo que extender su tooAzure de red local.  Se puede crear una instancia de App Service Environment en una subred de la infraestructura de esta [red virtual][virtualnetwork].  Aplicaciones que se ejecutan en el entorno del servicio de aplicación Hola, a continuación, pueden establecer conexiones seguras tooback los recursos de servidor puede tener acceso sólo a través de hello conexión ExpressRoute.  

Un entorno del Servicio de aplicaciones se puede crear **en** una red virtual de Azure Resource Manager **o en** una del modelo de implementación clásica.  Tras el cambio reciente realizado en junio de 2016, los entornos ASE también se pueden implementar ahora en redes virtuales que usen intervalos de direcciones públicas o espacios de direcciones de RFC1918 (es decir, direcciones privadas). 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>Conectividad de red necesaria
Hay requisitos de conectividad de red para los entornos del servicio de aplicación que no puede cumplirse inicialmente en un tooan de red virtual conectado ExpressRoute.  Los entornos del servicio de aplicación requieren todas siguiente de hello en orden toofunction correctamente:

* Red saliente conectividad tooAzure extremos de almacenamiento en todo el mundo en los puertos 80 y 443.  Esto incluye los puntos de conexión que se encuentra en hello misma región que Hola entorno del servicio de aplicaciones, así como los extremos de almacenamiento que se encuentra en **otros** regiones de Azure.  Extremos de almacenamiento de Azure resolver en hello siguiendo los dominios DNS: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net* y *file.core.windows.net*.  
* Toohello de conectividad de red saliente servicio de archivos de Azure en el puerto 445.
* Los puntos de conexión de red saliente conectividad tooSql DB ubicado en hello misma región como lo Hola entorno del servicio de aplicaciones.  Resolver los puntos de conexión de base de datos SQL en hello después de dominio: *database.windows.net*.  Esto requiere abrir acceso tooports 1433, 11000 a 11999 y 14000 a 14999.  Para obtener más información, consulte [este artículo sobre el uso de puertos en la versión 12 de Base de datos SQL](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).
* Salida conectividad toohello administración de Azure plano extremos de la red (extremos ASM y ARM).  Esto incluye conectividad saliente tooboth *management.core.windows.net* y *management.azure.com*. 
* Salida conectividad de red demasiado*ocsp.msocsp.com*, *mscrl.microsoft.com* y *crl.microsoft.com*.  Se trata de funcionalidad SSL de toosupport necesarios.
* configuración de DNS de Hola de red virtual de hello debe ser capaz de resolver todos los puntos de conexión de Hola y dominios que se menciona en Hola puntos anteriores.  Si estos puntos de conexión no se pueden resolver, se producirá un error en los intentos de creación del entorno del Servicio de aplicaciones y los entornos del Servicio de aplicaciones existentes se marcarán como incorrectos.
* Se requiere acceso saliente en el puerto 53 para establecer la comunicación con los servidores DNS.
* Si existe un servidor DNS personalizado en hello otro extremo de una puerta de enlace VPN, servidor DNS de hello debe ser accesible desde la subred de Hola que contiene Hola entorno del servicio de aplicaciones. 
* ruta de acceso de red saliente de Hello no se puede atravesar servidores proxy corporativo interno, ni puede ser force túnel tooon local.  Si lo hace, cambios Hola efectivo dirección NAT del tráfico de red saliente de hello entorno del servicio de aplicaciones.  Cambiar dirección NAT de Hola de tráfico de red saliente de un entorno servicio de aplicaciones, se producirá conectividad toomany de errores de los puntos de conexión de hello mencionado anteriormente.  Lo que da como resultado un error al intentar la creación del entorno del Servicio de aplicaciones, y además, los entornos del Servicio de aplicaciones previamente correctos estarán marcados como incorrectos.  
* Puertos de toorequired de acceso de red de entrada para entornos del servicio de aplicación debe poder tal como se describe en este [artículo][requiredports].

requisitos de DNS de Hello pueden cumplirse asegurándose de una infraestructura DNS válida se configuran y se mantienen para la red virtual de Hola.  Si para cualquier hello motivo se cambia la configuración de DNS después de crear un entorno de servicio de aplicaciones, los desarrolladores pueden forzar una toopick entono la nueva configuración de DNS Hola.  Desencadenar un reinicio gradual de entorno usando Hola "Reiniciar" icono encuentra final Hola de hoja de administración de entorno de servicio de aplicación Hola Hola [portal de Azure] [ NewPortal] provocará Hola entorno toopick la nueva configuración de DNS Hola.

Hello requisitos de acceso de red de entrada pueden cumplirse mediante la configuración de un [grupo de seguridad de red] [ NetworkSecurityGroups] en subred tooallow Hola requerido acceso del entorno del servicio de aplicación Hola tal como se describe en este [artículo][requiredports].

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>Habilitar la conectividad de red saliente para un entorno del Servicio de aplicaciones
De forma predeterminada, un circuito de ExpressRoute recién creado anuncia una ruta predeterminada que permite la conectividad saliente de Internet.  Con esta configuración de un entorno de servicio de aplicaciones será capaz de tooconnect tooother extremos de Azure.

Sin embargo, una configuración de cliente común es toodefine su propia ruta predeterminada (0.0.0.0/0), lo que obliga al flujo de tooinstead de tráfico de Internet saliente local.  Este flujo de tráfico invariable, interrumpe entornos del servicio de aplicación porque el tráfico saliente Hola está bloqueado de forma local o NAT con el conjunto irreconocible tooan de direcciones que ya no funcionan con varios extremos de Azure.

solución de Hello es rutas de toodefine uno (o más) definidos por el usuario (UDRs) de subred de Hola que contiene Hola entorno del servicio de aplicaciones.  Un UDR define las rutas de subred específica que se respetará en lugar de la ruta predeterminada de Hola.

Si es posible, se recomienda hello toouse siguiente configuración:

* configuración de ExpressRoute de Hello anuncia 0.0.0.0/0 y de forma predeterminada force túneles todo el tráfico saliente en local.
* Hola UDR aplica toohello subred que contiene Hola entono define 0.0.0.0/0 con un tipo de próximo salto de Internet (un ejemplo de esto es situados más abajo en este artículo).

Hola efecto combinado de estos pasos es que nivel de subred de hello UDR tendrá prioridad sobre hello ExpressRoute forzado túnel, lo que garantiza el acceso a Internet saliente desde Hola entorno del servicio de aplicaciones.

> [!IMPORTANT]
> Hola rutas definidas en un UDR **debe** ser lo suficientemente específica demasiado tienen prioridad sobre las rutas que anuncia Hola configuración de ExpressRoute.  ejemplo de Hola siguiente utiliza el intervalo de direcciones de hello amplia 0.0.0.0/0 y así puede potencialmente accidentalmente reemplazarse por anuncios de rutas con intervalos de direcciones más específicos.
> 
> Entornos del servicio de aplicación no son compatibles con las configuraciones de ExpressRoute que **entre-anunciar rutas de hello pública emparejamiento toohello privada emparejamiento ruta de acceso**.  Las configuraciones de ExpressRoute con el emparejamiento público configurado recibirán anuncios de ruta de Microsoft para un amplio conjunto de intervalos de direcciones IP de Microsoft Azure.  Si estos intervalos de direcciones entre anunciados en la ruta de intercambio de tráfico privado hello, obteniéndose hello es que todos los paquetes de red saliente de la subred del entorno del servicio de aplicación Hola será la infraestructura de red local del cliente de túnel forzado tooa.  Actualmente, este flujo de red no es compatible con las instancias de App Service Environment.  Un problema de toothis de solución es rutas de toostop entre anuncios de Hola pública emparejamiento toohello privada emparejamiento ruta de acceso.
> 
> 

Se puede encontrar información de contexto sobre las rutas definidas por el usuario en esta [información general][UDROverview].  

Obtener más información sobre cómo crear y configurar las rutas definidas por el usuario está disponible en este [cómo tooGuide][UDRHowTo].

## <a name="example-udr-configuration-for-an-app-service-environment"></a>Ejemplo de configuración de rutas definidas por el usuario para un entorno del Servicio de aplicaciones
**Requisitos previos**

1. Instalar Azure Powershell de hello [página de descargas de Azure] [ AzureDownloads] (con fecha de junio de 2015 o versiones posterior).  En "Herramientas de línea de comandos" hay un vínculo de "Instalar" en "Windows Powershell" que va a instalar los cmdlets de Powershell más recientes de Hola.
2. Se recomienda crear una única subred para que el entorno del Servicio de aplicaciones lo utilice de manera exclusiva.  Esto garantiza que esa subred de hello UDRs aplicadas toohello solo abrirá el tráfico saliente para el entorno del servicio de aplicación Hola.
3. **Importante**: no implemente Hola entono hasta **después** se siguen los siguientes pasos de configuración de Hola.  Esto garantiza que la conectividad de red saliente está disponible antes de intentar toodeploy un entorno de servicio de aplicaciones.

**Paso 1: Crear una tabla de rutas con nombre**

Hello fragmento de código siguiente crea una tabla de ruta denominada "DirectInternetRouteTable" en la región del Oeste nos Azure hello:

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**Paso 2: Crear una o más rutas en la tabla de rutas de Hola**

Necesitará tooadd uno o más rutas toohello ruta tabla en orden tooenable acceso saliente a Internet.  

Hola recomienda enfoque para configurar toohello de acceso de salida a que Internet es toodefine una ruta para 0.0.0.0/0 como se muestra a continuación.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

Recuerde que 0.0.0.0/0 es un intervalo de direcciones amplia y como tales serán reemplazadas por intervalos de direcciones más específicos anunciados hello ExpressRoute.  toore-iterar Hola recomendación anterior, un UDR con una ruta 0.0.0.0/0 debe usarse junto con una configuración de ExressRoute que solamente se publicita 0.0.0.0/0 también. 

Como alternativa, puede descargar una lista completa y actualizada de intervalos CIDR usados por Azure.  Hello archivo Xml que contiene todos los intervalos de direcciones IP Azure Hola está disponible en hello [Microsoft Download Center][DownloadCenterAddressRanges].  

Tenga en cuenta sin embargo que estos intervalos se cambian con el tiempo, por lo que hace actualizaciones manuales periódicas toohello definido por el usuario tookeep rutas sincronizados.  Además, dado que no hay valor predeterminado es superior toofit dentro de límite de la ruta de hello 100 intervalos de límite de 100 rutas en un único UDR, necesita demasiado "resumirá" dirección de IP de Azure de hello, teniendo en cuenta que UDR rutas definidas necesitan toobe más específico que las rutas de Hola que anuncia su ExpressRoute.  

**Paso 3: Asociar Hola ruta tabla toohello subred contenedor Hola entorno del servicio de aplicaciones**

Hola último paso de configuración es subred toohello de tooassociate Hola ruta tabla donde se implementará Hola entorno del servicio de aplicaciones.  Hello siguiente comando asocia toohello de "DirectInternetRouteTable" hello "ASESubnet" que finalmente contendrá un entorno de servicio de aplicaciones.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**Paso 4: Pasos finales**

Una vez que una tabla de rutas Hola subred toohello enlazado, se recomienda toofirst prueba y confirmar Hola pensado efecto.  Por ejemplo, implementar una máquina virtual en la subred de Hola y confirme que:

* El tráfico saliente tooboth Azure y extremos de Azure no se ha mencionado anteriormente en este artículo es **no** que fluyen hacia abajo Hola circuito de ExpressRoute.  Es muy importante tooverify este comportamiento, ya que si el tráfico saliente de la subred de hello es todavía verse obligado túnel local, la creación del entorno de servicio de aplicación le siempre producirá un error. 
* Las búsquedas DNS para los extremos de hello mencionadas anteriormente son todos resolver correctamente. 

Una vez que se confirman Hola por encima de los pasos, deberá toodelete Hola virtual machine porque subred Hola necesita toobe "vacío" en Hola Hola de tiempo que se crea el entorno del servicio de aplicaciones.

Ahora, ya puede continuar con la creación de un entorno del Servicio de aplicaciones.

## <a name="getting-started"></a>Introducción
Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

tooget iniciado con el entorno de servicio de aplicación, consulte [Introducción tooApp entorno del servicio][IntroToAppServiceEnvironment]

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
