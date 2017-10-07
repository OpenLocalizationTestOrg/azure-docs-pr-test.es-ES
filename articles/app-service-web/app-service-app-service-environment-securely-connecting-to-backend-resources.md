---
title: "aaaSecurely conexión tooBackEnd recursos desde un entorno de servicio de aplicaciones"
description: "Obtenga información sobre cómo se conectan toosecurely toobackend recursos desde un entorno de servicio de aplicaciones."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>TooBackend de conexión segura recursos desde un entorno de servicio de aplicaciones
## <a name="overview"></a>Información general
Puesto que siempre se crea un entorno de servicio de aplicación en **cualquier** una red virtual de Azure Resource Manager, **o** un modelo de implementación clásica [red virtual] [ virtualnetwork], las conexiones salientes desde un recursos de back-end de tooother de entorno de servicio de aplicaciones pueden fluir exclusivamente a través de la red virtual de Hola.  Tras el cambio reciente realizado en junio de 2016, los entornos ASE también se pueden implementar en redes virtuales que usen intervalos de direcciones públicas o espacios de direcciones de RFC1918 (es decir, direcciones privadas).  

Por ejemplo, puede haber un servidor SQL Server que se ejecute en un clúster de máquinas virtuales con el puerto 1433 bloqueado.  punto de conexión de Hello puede ser encuentra tooonly permitir el acceso desde otros recursos en Hola misma red virtual.  

Como otro ejemplo, extremos confidenciales pueden ejecutar de forma local y ser tooAzure conectado a través de cualquiera [sitio a sitio] [ SiteToSite] o [ExpressRoute de Azure] [ ExpressRoute] las conexiones.  Como resultado, sólo los recursos en redes virtuales conectado toohello sitio a sitio o ExpressRoute túneles serán puntos de conexión de tooaccess pueda local.

Para todos estos escenarios, aplicaciones que se ejecutan en un entorno de servicio de aplicaciones se pueda toosecurely conectará toohello varios servidores y recursos.  El tráfico saliente de aplicaciones que se ejecutan en los extremos del tooprivate un entorno de servicio de aplicaciones en hello misma red virtual (o conectado toohello misma red virtual), le flujo sólo a través de la red virtual de Hola.  Los puntos de conexión no fluirá a través de tooprivate de tráfico saliente Hola Internet pública.

Una advertencia aplica toooutbound tráfico de un tooendpoints de entorno de servicio de aplicaciones en una red virtual.  Entornos del servicio de aplicación no pueden tener acceso a los puntos de conexión de máquinas virtuales ubicadas en hello **mismo** subred como Hola entorno del servicio de aplicaciones.  Normalmente no debe ser un problema como entornos del servicio de aplicación se implementan en una subred reservada para uso exclusivo por hello solo entorno de servicio de aplicaciones.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Requisitos de DNS y conectividad saliente
Para un entorno de servicio de aplicaciones toofunction correctamente, requiere acceso de salida toovarious extremos. Una lista completa de extremos externos Hola utilizado por un ASE está en la sección "Requiere conectividad de red" de Hola Hola [configuración de red para ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artículo.

Los entornos del servicio de aplicación requieren una infraestructura DNS válida configurada para la red virtual de Hola.  Si para cualquier hello motivo se cambia la configuración de DNS después de crear un entorno de servicio de aplicaciones, los desarrolladores pueden forzar una toopick entono la nueva configuración de DNS Hola.  Desencadenar un reinicio de entorno gradual utilizando Hola "Reinicio" icono situado en parte superior de Hola de hello entono hoja de administración en el portal de hello provocará Hola entorno toopick la configuración de DNS nueva Hola.

También se recomienda que los servidores DNS personalizados en red virtual de hello sea el programa de instalación antes de tiempo anterior toocreating un entorno de servicio de aplicaciones.  Si se cambia la configuración de DNS de una red virtual mientras se crea un entorno de servicio de aplicaciones, que producirá errores de proceso de creación de hello entorno del servicio de aplicaciones.  En un modo similar, si existe un servidor DNS personalizado en hello otro extremo de una puerta de enlace VPN y el servidor DNS de hello es inaccesible o no está disponible, hello también se producirá un error del proceso de creación del entorno del servicio de aplicación.

## <a name="connecting-tooa-sql-server"></a>Conexión tooa SQL Server
Una configuración común de SQL Server tiene un extremo que escucha en el puerto 1433:

![Extremo de SQL Server][SqlServerEndpoint]

Existen dos enfoques para restringir el punto de conexión de toothis de tráfico:

* [Listas de control de acceso de red][NetworkAccessControlLists] (ACL de red)
* [Grupos de seguridad de red][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Restricción del acceso con una lista de control de acceso de red
El puerto 1433 se puede proteger mediante una lista de control de acceso de red.  ejemplo de Hola siguiente cliente listas blancas las direcciones que se origina desde dentro de una red virtual y bloquea el acceso tooall otros clientes.

![Ejemplo de lista de control de acceso de red][NetworkAccessControlListExample]

Las aplicaciones que se ejecutan en el entorno de servicio de aplicación en Hola misma red virtual como Hola SQL Server será tooconnect capaz de instancia de SQL Server toohello con hello **red virtual interna** dirección IP para la máquina virtual de SQL Server de Hola.  

cadena de conexión de ejemplo de Hola a continuación referencias Hola SQL Server mediante su dirección IP privada.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Aunque la máquina virtual de hello tiene también un punto de conexión público, los intentos de conexión con la dirección IP pública Hola se rechazarán debido a ACL de red Hola. 

## <a name="restricting-access-with-a-network-security-group"></a>Restricción del acceso con un grupo de seguridad de red
Un enfoque alternativo para proteger el acceso consiste en usar un grupo de seguridad de red.  Grupos de seguridad de red pueden ser tooindividual aplicado las máquinas virtuales o subred tooa que contienen máquinas virtuales.

En primer lugar un grupo de seguridad de red necesita toobe creado:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Restringir el acceso tooonly tráfico de red virtual interno es muy simple con un grupo de seguridad de red.  las reglas predeterminadas de Hello en un grupo de seguridad de red sólo permiten el acceso desde otros clientes de red en hello misma red virtual.

Como resultado bloquear el acceso tooSQL Server es tan sencillo como aplicación de un grupo de seguridad de red con sus valor predeterminado reglas tooeither Hola máquinas virtuales que ejecutan SQL Server o la subred de Hola que contienen máquinas virtuales de Hola.

ejemplo de Hola siguiente aplica una seguridad grupo toohello contenedor subred:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

resultado de Hello final es un conjunto de reglas de seguridad que bloquean el acceso externo, al permitir el acceso de red virtual interna:

![Reglas de seguridad de red predeterminadas][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Introducción
Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

tooget iniciado con el entorno de servicio de aplicación, consulte [Introducción tooApp entorno del servicio][IntroToAppServiceEnvironment]

Para obtener detalles alrededor de controlar el tráfico entrante tooyour entorno del servicio de aplicaciones, consulte [controlar el tráfico entrante tooan entorno del servicio de aplicaciones][ControlInboundASE]

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
