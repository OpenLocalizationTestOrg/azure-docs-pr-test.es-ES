---
title: "información general de arquitectura de aplicación servicio entornos aaaNetwork"
description: "Introducción a la arquitectura de la topología de red de los entornos del Servicio de aplicaciones."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>Información general sobre la arquitectura de red de los entornos del Servicio de aplicaciones
## <a name="introduction"></a>Introducción
Entornos del servicio de aplicación siempre se crean dentro de una subred de un [red virtual] [ virtualnetwork] -aplicaciones que se ejecutan en un entorno de servicio de aplicaciones pueden comunicarse con privada extremos ubicados en hello mismo virtual topología de red.  Puesto que los clientes pueden bloquear partes de su infraestructura de red virtual, es importante toounderstand tipos de Hola de flujos de comunicación de red que se producen con un entorno de servicio de aplicaciones.

## <a name="general-network-flow"></a>Flujo de red general
Cuando un entorno del Servicio de aplicaciones (ASE) utiliza una dirección IP virtual pública (VIP) para las aplicaciones, todo el tráfico entrante llega a esa VIP pública,  incluido el tráfico HTTP y HTTPS para las aplicaciones, así como otro tráfico de FTP, la funcionalidad de depuración remota y las operaciones de administración de Azure.  Para obtener una lista completa de hello puertos específicos (necesarios y opcionales) que están disponibles en la VIP pública Hola consulte artículo de hello en [controlar el tráfico entrante] [ controllinginboundtraffic] tooan entorno del servicio de aplicaciones. 

Entornos del servicio de aplicación también permiten la ejecución aplicaciones que se enlazan solo tooa virtual red dirección interna, también denominado tooas una dirección ILB (equilibrador de carga interno).  En un ILB tráfico ASE, HTTP y HTTPS habilitado para aplicaciones, así como llamadas de depuración remotas, llegan en hello dirección ILB.  Para configuraciones de ILB ASE más habituales, el tráfico FTP o FTPS también llegarán a Hola dirección ILB.  Sin embargo las operaciones de administración de Azure sigue fluirá tooports 454 y 455 en hello VIP pública de un ILB habilita ASE.

diagrama de Hello siguiente muestra un resumen de hello distintos flujos de red entrantes y salientes para un entorno de servicio de aplicación donde hello aplicaciones están enlazadas tooa: dirección IP virtual pública:

![Flujos de red generales][GeneralNetworkFlows]

Un entorno del Servicio de aplicaciones puede comunicarse con una variedad de extremos privados del cliente.  Por ejemplo, aplicaciones que se ejecutan en hello en que entorno del servicio de aplicaciones puede conectarse a servidores de toodatabase que se ejecutan en máquinas virtuales de IaaS Hola misma topología de red virtual.

> [!IMPORTANT]
> Examinando el diagrama de red de hello, Hola "otros proceso recursos" se implementan en una subred diferente de hello entorno del servicio de aplicaciones. Implementar recursos en hello misma subred con hello ASE bloqueará la conectividad de los recursos de toothose ASE (a excepción de enrutamiento específico intra-ASE). Implementar tooa subred diferente en su lugar (en Hola misma red virtual). Hola entono será capaz de tooconnect. No se necesita ninguna configuración adicional.
> 
> 

Los entornos del Servicio de aplicaciones también se comunican con la base de datos SQL y los recursos del Almacenamiento de Azure necesarios para administrar y operar un entorno del Servicio de aplicaciones.  Algunos de los recursos de Sql y el almacenamiento de Hola que un entorno de servicio de aplicaciones se comunica con se encuentran en hello misma región que Hola entorno de servicio de aplicaciones, mientras que otras personas se encuentran en regiones de Azure remotas.  Como resultado, conectividad saliente toohello Internet siempre se requiere para un entorno de servicio de aplicaciones toofunction correctamente. 

Dado que un entorno de servicio de aplicación se implementa en una subred, grupos de seguridad de red pueden ser usado toocontrol subred toohello de tráfico entrante.  Para obtener detalles sobre cómo toocontrol entrada tráfico tooan entorno del servicio de aplicaciones, vea el siguiente hello [artículo][controllinginboundtraffic].

Para obtener más información acerca de cómo tooallow conectividad a Internet saliente desde un entorno de servicio de aplicaciones, vea Hola artículo sobre cómo trabajar con siguiente [Expressroute][ExpressRoute].  Hola mismo enfoque descrita en el artículo Hola se aplica cuando se trabaja con conectividad de sitio a sitio y que estás usando la tunelización forzada.

## <a name="outbound-network-addresses"></a>Direcciones de red de salida
Cuando un entorno de servicio de aplicaciones realiza las llamadas salientes, siempre se asocia con llamadas salientes de hello una dirección IP.  dirección IP específica Hola que se usa depende de si se llama a un punto de conexión de Hola se encuentra dentro de la topología de red virtual de Hola o fuera de la topología de red virtual de Hola.

Si se llama a un punto de conexión de hello es **fuera** de topología de red virtual de Hola y Hola dirección saliente (también conocido como Hola saliente dirección NAT) que se utiliza es Hola VIP pública de hello entorno del servicio de aplicaciones.  Esta dirección se puede encontrar en la interfaz de usuario del portal de Hola para hello entorno del servicio de aplicaciones en la hoja de propiedades.

![Dirección IP saliente][OutboundIPAddress]

También se puede determinar esta dirección para ASEs que solo tienen una VIP pública, cree una aplicación Hola entorno del servicio de aplicaciones y, a continuación, realizar una *nslookup* en dirección de la aplicación hello. dirección IP resultante de Hello es VIP pública hello, así como dirección NAT de salida del entorno del servicio de aplicación Hola.

Si se llama a un punto de conexión de hello es **en** de topología de red virtual de hello, dirección de salida de hello de aplicación que realiza la llamada de hello será la dirección IP interna de Hola Hola individuales de recurso de proceso ejecutando la aplicación hello.  Sin embargo, no hay una asignación persistente de red virtual interna IP direcciones tooapps.  Aplicaciones pueden moverse a través de recursos de proceso diferente y grupo de Hola de recursos de proceso disponibles en un entorno de servicio de aplicaciones puede cambiar debido a las operaciones de tooscaling.

Sin embargo, puesto que un entorno de servicio de aplicaciones siempre se encuentra dentro de una subred, se garantiza que la dirección IP interna de Hola de un recurso de proceso que se ejecuta una aplicación siempre se quedan dentro del alcance CIDR de Hola de subred de Hola.  Como resultado, cuando se utilizan las ACL específicas o grupos de seguridad de red toosecure tener acceso a los puntos de conexión de tooother dentro de la red virtual de hello, Hola intervalo de subred que contiene Hola entono necesidades toobe concedido acceso.

Hello diagrama siguiente muestra estos conceptos más detalladamente:

![Direcciones de red de salida][OutboundNetworkAddresses]

Hola diagrama anterior:

* Puesto que Hola VIP pública de hello entono es 192.23.1.2, que es Hola saliente dirección IP utilizada cuando se realizan llamadas demasiado los extremos de "Internet".
* Hola intervalo CIDR de Hola que contiene la subred para hello entono es 10.0.1.0/26.  Otros puntos de conexión dentro de hello misma infraestructura de red virtual verá llamadas desde aplicaciones que se originan en algún lugar dentro de este intervalo de direcciones.

## <a name="calls-between-app-service-environments"></a>Llamadas entre entornos del Servicio de aplicaciones
Puede producirse una situación más compleja si implementa varios entornos de servicio de aplicación en Hola misma red virtual y realizar llamadas salientes de un entorno de servicio de aplicaciones tooanother entorno del servicio de aplicaciones.  Estos tipos de llamadas cruzadas entre entornos del Servicio de aplicaciones también se tratarán como llamadas de "Internet".

Hola siguiente diagrama muestra un ejemplo de una arquitectura en capas con aplicaciones en un entorno de servicio de aplicación (p. ej. Aplicaciones web de "Puerta principal") al llamar a las aplicaciones en un segundo entorno de servicio de aplicación (por ejemplo, aplicaciones internas de API de back-end no están diseñados toobe accesible desde Internet hello). 

![Llamadas entre entornos del Servicio de aplicaciones][CallsBetweenAppServiceEnvironments] 

Hola ejemplo anterior Hola entono "ASE uno" tiene una dirección IP saliente de 192.23.1.2.  Si una aplicación que se ejecuta en este entorno de servicio de aplicaciones realiza una aplicación de tooan llamada saliente con un segundo entono ("ASE dos") ubicado en hello mismo virtual de red, hello saliente llamada se tratará como una llamada de "Internet".  Como resultado el tráfico de red de Hola que llegan en hello segundo entorno de servicio de aplicación se mostrará como originaria de 192.23.1.2 (es decir, no Hola subred intervalo de direcciones de Hola primer entorno del servicio de aplicaciones).

Aunque las llamadas entre los distintos entornos de servicio de aplicación se tratan como llamadas de "Internet", cuando ambos entornos del servicio de aplicación se encuentran en hello mismo tráfico de red de Hola de región de Azure, permanecerá en la red de Azure regional hello y no se desplazarán físicamente sobre Hola Internet pública.  Como resultado puede usar un grupo de seguridad de red en la subred de Hola de hello segundo entono tooonly permitir llamadas entrantes de Hola primera entono (cuya dirección IP saliente es 192.23.1.2), lo que garantiza una comunicación segura entre Hola Entornos del servicio de aplicación.

## <a name="additional-links-and-information"></a>Información y vínculos adicionales
Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

Obtener más información sobre puertos utilizados por los entornos del servicio de aplicación de entrada y el tráfico entrante con toocontrol de grupos de seguridad de red está disponible [aquí][controllinginboundtraffic].

Detalles sobre el uso de definidos por el usuario rutas toogrant saliente Internet access tooApp entornos del servicio está disponible en este [artículo][ExpressRoute]. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

