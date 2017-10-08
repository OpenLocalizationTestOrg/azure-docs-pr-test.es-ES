---
title: "aaaLayered arquitectura de seguridad con el entorno de servicio de aplicación"
description: "Implementación de una arquitectura de seguridad por capas con entornos del Servicio de aplicaciones"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Implementación de una arquitectura de seguridad por capas con entornos del Servicio de aplicaciones
## <a name="overview"></a>Información general
Como los entornos del Servicio de aplicaciones proporcionan un entorno de tiempo de ejecución aislado que está implementado en una red virtual, los desarrolladores pueden crear una arquitectura de seguridad por capas que proporcione diferentes niveles de acceso a la red para cada capa de aplicación física.

Un deseo común es toohide API back-end de acceso general a Internet y solo se permiten toobe API llama a las aplicaciones web de nivel superior.  [Grupos de seguridad (NSG) de red] [ NetworkSecurityGroups] puede utilizarse en las subredes que contiene aplicaciones de tooAPI de acceso público de toorestrict entornos del servicio de aplicación.

diagrama de Hello siguiente muestra una arquitectura de ejemplo con una aplicación de WebAPI según implementada en un entorno de servicio de aplicaciones.  Tres instancias de aplicación web independiente, implementadas en tres entornos de servicio de aplicación independientes, realizar llamadas de back-end toohello misma aplicación WebAPI.

![Arquitectura conceptual][ConceptualArchitecture] 

Hello verde signos de más indicar ese Hola grupo de seguridad de red en la subred de Hola que contiene "apiase" permite llamadas entrantes de hello las aplicaciones web de nivel superior, como bien llamadas de sí misma.  Sin embargo, Hola deniega explícitamente el mismo grupo de seguridad de red acceder a toogeneral el tráfico entrante desde Internet Hola. 

resto de Hola de este tema le guía a través del grupo de seguridad de red de Hola Hola pasos tooconfigure necesarios de subred de Hola que contiene "apiase".

## <a name="determining-hello-network-behavior"></a>Determinar Hola comportamiento de la red
En orden tooknow la seguridad de la red son necesarias las reglas, debe toodetermine se permitirá que los clientes de red aplicación tooreach Hola entono contenedor hello API y qué clientes se bloquearán.

Puesto que [grupos de seguridad (NSG) de red] [ NetworkSecurityGroups] son toosubnets aplicado, y entornos del servicio de aplicación se implementan en subredes, Hola contenidas en un NSG se aplican reglas demasiado**todos los** aplicaciones que se ejecutan en un entorno de servicio de aplicaciones.  Mediante la arquitectura de ejemplo de Hola para este artículo, una vez que un grupo de seguridad de red se subred toohello aplicados que contiene "apiase", todas las aplicaciones que se ejecutan en hello "apiase" entorno del servicio de aplicación se protegerán Hola mismo conjunto de reglas de seguridad. 

* **Determinar la dirección IP saliente Hola de llamadores de nivel superior:** ¿qué es Hola dirección o direcciones IP de los llamadores de nivel superior de hello?  Estas direcciones deberá toobe permitidos explícitamente acceso en hello NSG.  Dado que las llamadas entre entornos del servicio de aplicación se consideran llamadas "Internet", esto significa Hola salida IP dirección asignada tooeach de hello tres ascendente entornos del servicio de aplicación necesidades toobe puede tener acceso en hello NSG para la subred de "apiase" Hola.   Para obtener más información acerca de cómo determinar la dirección IP de la salida Hola para aplicaciones que se ejecutan en un entorno de servicio de aplicaciones, consulte hello [arquitectura de red] [ NetworkArchitecture] artículo de información general.
* **¿Será necesario aplicaciones de API de back-end de hello toocall propio?**  Un punto en ocasiones, se pasa por alto y sutil es escenario Hola donde la aplicación de back-end de hello necesita toocall propio.  Si una aplicación de API de back-end en un entorno de servicio de aplicaciones necesita toocall propio, también se trata como una llamada de "Internet".  En la arquitectura de ejemplo de Hola Esto requiere que permite el acceso de la dirección IP saliente Hola Hola "apiase" entono así.

## <a name="setting-up-hello-network-security-group"></a>Configuración de grupo de seguridad de red de Hola
Una vez Hola conjunto de direcciones IP salientes se conocen, Hola siguiente paso es tooconstruct un grupo de seguridad de red.  Se pueden crear grupos de seguridad de red para las redes virtuales basadas en Resource Manager, así como para las redes virtuales clásicas.  ejemplos de Hello siguientes muestran la creación y configuración de un NSG en una red virtual clásica mediante Powershell.

De arquitectura de ejemplo de Hola, entornos de Hola se encuentran en el Ee.uu. Central sur, por lo que se crea un NSG vacío en dicha región:

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

En primer lugar explícito Permitir que se agrega la regla para la infraestructura de administración de Azure de hello como se indica en el artículo de hello en [el tráfico entrante] [ InboundTraffic] para entornos del servicio de aplicación.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

A continuación, dos reglas se agregan tooallow HTTP y HTTPS llamadas de Hola primer entorno del servicio de aplicación de nivel superior ("fe1ase").

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Enjuagar y repita la operación para Hola segunda y tercera ascendente aplicación entornos del servicio ("fe2ase" y "fe3ase").

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Por último, conceder acceso toohello saliente dirección IP del entorno de servicio de aplicaciones de la API de back-end de Hola de manera que puede devolver la llamada a sí misma.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Ninguna otra regla de seguridad de red necesita toobe configurado porque cada NSG tiene un conjunto de reglas predeterminadas que bloqueen el acceso entrante de hello Internet de forma predeterminada.

lista completa de Hola de reglas en el grupo de seguridad de red de Hola se muestran a continuación.  Tenga en cuenta cómo regla última hello, que está resaltado, bloquea el acceso entrante desde todos los llamadores distintos de los que ha concedido acceso explícitamente.

![Configuración NSG][NSGConfiguration] 

Hola último paso es tooapply hello NSG toohello máscara de subred que contiene Hola "apiase" entorno del servicio de aplicaciones.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Con hello NSG aplica toohello subred, sólo hello tres entornos del servicio de aplicación de nivel superior y Hola Hola de contenedor de entorno del servicio de aplicaciones back-end de API, se permiten toocall en entorno de "apiase" Hola.

## <a name="additional-links-and-information"></a>Información y vínculos adicionales
Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

Información acerca de los [grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md). 

Descripción de las [direcciones IP saliente][NetworkArchitecture] y entornos de App Service.

[Puertos de red][InboundTraffic] usados en un entorno de App Service

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
