---
title: "aaaHow tooControl el tráfico entrante tooan entorno del servicio de aplicaciones"
description: "Obtenga información acerca de cómo toocontrol de reglas de seguridad de red tooconfigure entrada tráfico tooan entorno del servicio de aplicaciones."
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Cómo tooControl el tráfico entrante tooan entorno del servicio de aplicaciones
## <a name="overview"></a>Información general
Un entorno de App Service se puede crear **en** una red virtual de Azure Resource Manager **o en** una [red virtual][virtualnetwork] del modelo de implementación clásica.  Una nueva red virtual y la nueva subred pueden definirse en tiempo de Hola que se crea un entorno de servicio de aplicación.  También puede crearse un entorno del Servicio de aplicaciones en una red virtual y subred preexistentes.  Tras el cambio realizado en junio de 2016, los entornos ASE también se pueden implementar en redes virtuales que usen intervalos de direcciones públicas o espacios de direcciones de RFC1918 (es decir, direcciones privadas).  Para obtener más información acerca de cómo crear un entorno de servicio de aplicaciones, consulte [cómo tooCreate un entorno de servicio de aplicaciones][HowToCreateAnAppServiceEnvironment].

Un entorno de servicio de aplicaciones debe siempre se pueden crear dentro de una subred porque una subred proporciona un límite de red que puede ser usado toolock hacia abajo el tráfico entrante detrás de dispositivos de nivel superior y los servicios de modo que solo se acepta el tráfico HTTP y HTTPS de específico ascendente Direcciones IP.

El tráfico de red entrante y saliente de una subred se controla mediante un [grupo de seguridad de red][NetworkSecurityGroups]. Controlar el tráfico entrante requiere la creación de reglas de seguridad de red en un grupo de seguridad de red y, a continuación, asignar Hola red seguridad grupo Hola subred contenedor Hola entorno del servicio de aplicaciones.

Una vez que se asigna a un grupo de seguridad de red tooa subred, el tráfico entrante tooapps Hola que entono es permitidos y bloqueados en función de Hola permitir y denegar las reglas definidas en el grupo de seguridad de red de Hola.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Puertos de red usados en un entorno de App Service
Antes de bloquear el tráfico de red entrante a un grupo de seguridad de red, es importante tooknow Hola conjunto de puertos de red necesarios y opcionales utilizados por un entorno de servicio de aplicaciones.  Cierra accidentalmente desactivar tráfico toosome puertos puede dar lugar a pérdida de funcionalidad en un entorno de servicio de aplicaciones.

Hola mostramos una lista de puertos utilizados por un entorno de servicio de aplicaciones. Todos los puertos son **TCP**, a menos que indique claramente:

* 454:  **puerto obligatorio** utilizado por la infraestructura de Azure para administrar y mantener App Service Environment a través de SSL.  No se bloquee el puerto de toothis de tráfico.  Este puerto es siempre toohello enlazado VIP pública de un ASE.
* 455:  **puerto obligatorio** utilizado por la infraestructura de Azure para administrar y mantener App Service Environment a través de SSL.  No se bloquee el puerto de toothis de tráfico.  Este puerto es siempre toohello enlazado VIP pública de un ASE.
* 80: el puerto de entrada tooapps de tráfico HTTP se ejecuta en los planes de servicio de aplicación en un entorno de servicio de aplicaciones predeterminado.  En un ASE habilitado ILB, este puerto es la dirección ILB de toohello enlazado de hello ASE.
* 443: el puerto de entrada tooapps de tráfico SSL ejecutando en los planes de servicio de aplicación en un entorno de servicio de aplicaciones predeterminado.  En un ASE habilitado ILB, este puerto es la dirección ILB de toohello enlazado de hello ASE.
* 21: canal de control para FTP.  Este puerto se puede bloquear de forma segura si no se utiliza FTP.  En un ASE habilitado ILB, este puerto puede ser la dirección ILB de toohello enlazado para un ASE.
* 990: canal de control para FTPS.  Este puerto se puede bloquear de forma segura si no se utiliza FTPS.  En un ASE habilitado ILB, este puerto puede ser la dirección ILB de toohello enlazado para un ASE.
* 10001-10020: canales de datos para FTP.  Como con canal de control de hello, estos puertos pueden ser sin ningún riesgo bloqueados si no se utiliza FTP.  En un ASE habilitado ILB, este puerto puede ser la dirección ILB de toohello dependiente del ASE.
* 4016: usado para la depuración remota con Visual Studio 2012.  Este puerto se puede bloquear de forma segura si no se utiliza la característica de Hola.  En un ASE habilitado ILB, este puerto es la dirección ILB de toohello enlazado de hello ASE.
* 4018: usado para la depuración remota con Visual Studio 2013.  Este puerto se puede bloquear de forma segura si no se utiliza la característica de Hola.  En un ASE habilitado ILB, este puerto es la dirección ILB de toohello enlazado de hello ASE.
* 4020: usado para la depuración remota con Visual Studio 2015.  Este puerto se puede bloquear de forma segura si no se utiliza la característica de Hola.  En un ASE habilitado ILB, este puerto es la dirección ILB de toohello enlazado de hello ASE.

## <a name="outbound-connectivity-and-dns-requirements"></a>Requisitos de DNS y conectividad saliente
Para un entorno de servicio de aplicaciones toofunction correctamente, también se necesita puntos de conexión de acceso de salida toovarious. Una lista completa de extremos externos Hola utilizado por un ASE está en la sección "Requiere conectividad de red" de Hola Hola [configuración de red para ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artículo.

Los entornos del servicio de aplicación requieren una infraestructura DNS válida configurada para la red virtual de Hola.  Si para cualquier hello motivo se cambia la configuración de DNS después de crear un entorno de servicio de aplicaciones, los desarrolladores pueden forzar una toopick entono la nueva configuración de DNS Hola.  Desencadenar un reinicio gradual de entorno usando Hola "Reiniciar" icono encuentra final Hola de hoja de administración de entorno de servicio de aplicación Hola Hola [portal de Azure] [ NewPortal] provocará Hola entorno toopick la nueva configuración de DNS Hola.

También se recomienda que los servidores DNS personalizados en red virtual de hello sea el programa de instalación antes de tiempo anterior toocreating un entorno de servicio de aplicaciones.  Si se cambia la configuración de DNS de una red virtual mientras se crea un entorno de servicio de aplicaciones, que producirá errores de proceso de creación de hello entorno del servicio de aplicaciones.  En un modo similar, si existe un servidor DNS personalizado en hello otro extremo de una puerta de enlace VPN y el servidor DNS de hello es inaccesible o no está disponible, hello también se producirá un error del proceso de creación del entorno del servicio de aplicación.

## <a name="creating-a-network-security-group"></a>Creación de un grupo de seguridad de red
Para obtener detalles completos sobre cómo funcionan los grupos de seguridad de red, consulte siguiente hello [información][NetworkSecurityGroups].  ejemplo de administración de servicios de Azure de Hello siguiente en los últimos retoques resalta de grupos de seguridad de red, con un enfoque sobre cómo configurar y aplicar una subred de tooa de grupo de seguridad de red que contiene un entorno de servicio de aplicaciones.

**Nota:** grupos de seguridad de red se pueden configurar gráficamente mediante hello [Portal de Azure](https://portal.azure.com) o a través de PowerShell de Azure.

Los grupos de seguridad de red se crean por primera vez como una entidad independiente asociada a una suscripción. Puesto que se crean grupos de seguridad de red en una región de Azure, asegúrese de ese grupo de seguridad de red de hello es creado en hello mismo región como lo Hola entorno del servicio de aplicaciones.

siguiente Hello muestra cómo crear un grupo de seguridad de red:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Una vez que se crea un grupo de seguridad de red, una o varias reglas de seguridad de red se agregan tooit.  Puesto que el conjunto de Hola de reglas puede cambiar con el tiempo, se recomienda toospace out Hola esquema de numeración usado para la regla prioridades toomake reglas adicionales tooinsert fácil con el tiempo.

ejemplo de Hola siguiente muestra una regla que concede los puertos de administración de acceso toohello necesarios toomanage de infraestructura de Azure de hello explícitamente y mantener un entorno de servicio de aplicaciones.  Tenga en cuenta que todo el tráfico de administración fluye a través de SSL y se protege mediante certificados de cliente, por lo que, aunque estén abiertos los puertos de hello son inaccesibles por cualquier entidad que no sea la infraestructura de administración de Azure.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Al bloquear el acceso tooport 80 y 443 demasiado "oculta" un entorno de servicio de aplicación detrás de dispositivos de nivel superior o servicios, necesitará la dirección IP de nivel superior de tooknow Hola.  Por ejemplo, si está utilizando un servidor de aplicaciones web (WAFS), Hola WAFS tendrá su propia dirección IP (o direcciones) que usa cuando un proxy tráfico tooa entorno del servicio de aplicación de nivel inferior.  Necesitará toouse esta dirección IP en hello *SourceAddressPrefix* parámetro de una regla de seguridad de red.

En el siguiente ejemplo de Hola, explícitamente se permite el tráfico entrante procedente de una dirección IP de nivel superior específica.  Hola dirección *1.2.3.4* se utiliza como un marcador de posición para la dirección IP de Hola de un nivel superior WAFS.  Cambiar Hola valor toomatch Hola dirección usada por su servicio o un dispositivo de nivel superior.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Si se desea compatibilidad con FTP, Hola siguiendo reglas puede utilizarse como un puerto de control de plantilla toogrant acceso toohello FTP y los puertos de canal de datos.  Puesto que FTP es un protocolo con estado, es posible no que pueda tooroute FTP el tráfico a través de un dispositivo de firewall o proxy tradicional de HTTP/HTTPS.  En este caso deberá hello tooset *SourceAddressPrefix* tooa valor diferente: por ejemplo Hola IP direcciones intervalo de desarrollador o implementación de máquinas en que FTP, los clientes están ejecutando. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Nota:** puede cambiar el intervalo de puertos de canal de datos de Hola durante el período de vista previa de Hola.)

Si se utiliza la depuración remota con Visual Studio, Hola siguiendo las reglas en el que se muestra cómo tener acceso toogrant.  Puesto que cada versión usa un puerto diferente para la depuración remota, hay una regla distinta para cada versión compatible de Visual Studio.  Al igual que ocurre con el acceso FTP, es posible que el tráfico de depuración remoto no fluya correctamente a través de un dispositivo de proxy o WAF tradicional.  Hola *SourceAddressPrefix* en su lugar, se puede establecer toohello intervalo de direcciones IP de los equipos de desarrollador ejecutando Visual Studio.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>Asignación de una subred tooa de grupo de seguridad de red
Un grupo de seguridad de red tiene una regla de seguridad predeterminada que se deniega el acceso tooall el tráfico externo.  Hola resultado de la combinación de reglas de seguridad de red de Hola se ha descrito anteriormente y Hola regla de seguridad predeterminada que bloquee el tráfico entrante, es que únicamente el tráfico de intervalos de direcciones de origen asociado con un *permitir* podrá realizar acción toosend tooapps de tráfico ejecuta en un entorno de servicio de aplicaciones.

Después de un grupo de seguridad de red se rellena con las reglas de seguridad, debe toobe asignado toohello subred que contiene Hola entorno del servicio de aplicaciones.  comando de asignación de Hello hace referencia tanto el nombre de red virtual de Hola donde reside Hola entorno del servicio de aplicaciones, así como nombre de Hola de subred Hola donde se creó el entorno del servicio de aplicación Hola Hola.  

ejemplo de Hola siguiente muestra un grupo de seguridad de red que se va a asignar tooa subred y red virtual:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Una vez realizada correctamente la asignación de grupo de seguridad de red hello (asignación de hello es una operación de larga duración y puede tardar unos toocomplete minutos), sólo de entrada tráfico que coincide con *permitir* reglas correctamente llegará a aplicaciones en la aplicación hello Entorno del servicio.

Para Hola de integridad en el ejemplo siguiente se muestra cómo tooremove y, por tanto, asociar DIS Hola red grupo de seguridad de la subred de hello:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Consideraciones especiales para IP-SSL explícito
Si una aplicación está configurada con una dirección IP SSL explícita (aplicable *sólo* tooASEs que tienen una VIP pública), en lugar de usar la dirección IP de hello predeterminada de hello entorno del servicio de aplicaciones, HTTP y HTTPS flujos en la subred de Hola de tráfico a través de un conjunto diferente de puertos que no sean los puertos 80 y 443.

par individual de Hola de puertos utilizados por cada dirección IP SSL puede encontrarse en la interfaz de usuario del portal de Hola de hoja UX de detalles del entorno del servicio de aplicación Hola.  Seleccione Toda la configuración > Direcciones IP.  hoja de "direcciones IP" Hello muestra una tabla de todas las direcciones IP SSL configuradas explícitamente Hola entorno del servicio de aplicación, junto con el par de puertos especiales de Hola que es usado tooroute tráfico HTTP y HTTPS asociado a cada dirección IP SSL.  Es este par de puertos que necesita toobe utiliza para los parámetros de DestinationPortRange de hello al configurar las reglas en un grupo de seguridad de red.

Cuando una aplicación en un ASE es toouse configurado SSL de IP, los clientes externos no podrán ver y no necesitan tooworry sobre la asignación de par de hello especial de puerto.  Aplicaciones de toohello tráfico fluirá normalmente toohello configurado SSL de IP dirección.  par de puerto especial de Hello traducción toohello automáticamente ocurre internamente durante la autenticación mutua final de Hola de enrutamiento del tráfico en Hola Hola de contenedor de subred ASE. 

## <a name="getting-started"></a>Introducción
tooget iniciado con el entorno de servicio de aplicación, consulte [Introducción tooApp entorno del servicio][IntroToAppServiceEnvironment]

Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

Para obtener más información en aplicaciones que se conecten de forma segura toobackend recursos desde un entorno de servicio de aplicaciones, consulte [conectarse de forma segura tooBackend recursos desde un entorno de servicio de aplicaciones][SecurelyConnecttoBackend]

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

