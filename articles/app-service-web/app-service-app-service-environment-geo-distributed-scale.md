---
title: "aaaGeo distribuido escala con entornos del servicio de aplicación"
description: "Obtenga información acerca de cómo toohorizontally escalar aplicaciones con la distribución geográfica con el Administrador de tráfico y entornos del servicio de aplicación."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>Escala distribuida geográficamente con entornos de Servicio de aplicaciones
## <a name="overview"></a>Información general
Escenarios de aplicaciones que requieren alta escala pueden superar Hola recursos capacidad disponible tooa única implementación de procesos de una aplicación.  Algunos ejemplos de los escenarios que requieren una escala extremadamente alta son las aplicaciones de votación, los acontecimientos deportivos y los espectáculos televisados. Requisitos de gran escala pueden cumplirse mediante el escalado horizontal de las aplicaciones, con varias implementaciones de aplicación que se va a realizar en una única región, así como entre las regiones, requisitos de carga extrema toohandle en.

Los entornos de Servicio de aplicaciones son una plataforma ideal para el escalado horizontal.  Una vez que se ha seleccionado una configuración de entorno del servicio de aplicaciones que puede admitir una tasa de solicitud conocidos, los desarrolladores pueden implementar entornos del servicio de aplicación adicionales en "molde" modo tooattain una capacidad de carga pico deseado.

Por ejemplo, imagine una aplicación que se ejecuta en una configuración de entorno del servicio de aplicaciones ha sido probado toohandle 20 KB solicitudes por segundo (RPS).  Si se carga pico deseado Hola capacidad es 100K RPS, se pueden crear entornos del servicio de aplicación de cinco (5) y tooensure configurado Hola aplicación puede controlar la carga máxima proyectada de Hola.

Puesto que los clientes normalmente tienen acceso a aplicaciones que usan un dominio personalizado (o personal), los desarrolladores que necesitan una aplicación de manera toodistribute solicita a través de todas las instancias del entorno del servicio de aplicaciones de Hola de.  Un tooaccomplish excelente manera es tooresolve Hola dominio personalizado utilizando un [perfil de Traffic Manager de Azure][AzureTrafficManagerProfile].  Hola Traffic Manager perfil puede ser toopoint configurado en absoluto de Hola entornos del servicio de aplicación individuales.  El Administrador de tráfico controlará automáticamente la distribución de los clientes en todos los que entornos del servicio de aplicación en función de la configuración de perfil de Traffic Manager Hola de equilibrio de carga de Hola de Hola.  Este enfoque funciona independientemente de si todos los entornos del servicio aplicación Hola se implementa en una sola región de Azure o implementadas en todo el mundo a través de varias regiones de Azure.

Además, puesto que los clientes acceder a las aplicaciones a través de dominio personal de hello, los clientes no son conscientes del número de Hola de entornos del servicio de aplicación al ejecutar una aplicación.  Como resultado, los desarrolladores pueden agregar y quitar rápida y fácilmente entornos de Servicio de aplicaciones según la carga de tráfico observada.

diagrama conceptual de Hello siguiente muestra una aplicación escalada horizontalmente a través de tres entornos de servicio de aplicación en una única región.

![Arquitectura conceptual][ConceptualArchitecture] 

resto de Hola de este tema recorre Hola pasos con la configuración de una topología distribuida para la aplicación de ejemplo de Hola con varios entornos de servicio de aplicación.

## <a name="planning-hello-topology"></a>Planear la topología de Hola
Antes de crear una superficie de la aplicación distribuida, es útil toohave algunas partes información con antelación.

* **Dominio personalizado para su aplicación hello:** ¿qué es el nombre de dominio personalizado de Hola que los clientes usarán tooaccess Hola aplicación?  Dominio personalizado de hello ejemplo aplicación Hola nombre es *www.scalableasedemo.com*
* **Dominio de Traffic Manager:** toobe elegida al crear un nombre de dominio es necesario un [perfil de Traffic Manager de Azure][AzureTrafficManagerProfile].  Este nombre se combinarán con hello *trafficmanager.net* sufijo tooregister una entrada de dominio que está administrada por el Administrador de tráfico.  Para la aplicación de ejemplo de Hola, elegida de nombre de hello es *escalable de demostración de ase*.  Como resultado es el nombre de dominio completo de Hola que es administrado por el Administrador de tráfico *demo.trafficmanager.net escalable de ase*.
* **¿Estrategia para el escalado de la superficie de la aplicación de hello:** se distribuirán superficie de aplicación Hola a través de varios entornos de servicio de aplicación en una sola región?  ¿Varias regiones?  ¿Una combinación de ambos enfoques?  Hola decisión debe basarse en las expectativas de donde se originará a tráfico de cliente, así como la puede escalar el resto de Hola y de una aplicación de la compatibilidad de la infraestructura de back-end.  Por ejemplo, con una aplicación totalmente sin estado, se puede escalar una aplicación de forma masiva mediante una combinación de varias instancias de App Service Environment por región de Azure, multiplicados por más instancias de App Service Environment implementadas en varias regiones de Azure.  Con 15 + regiones de Azure pública toochoose disponibles desde, los clientes pueden crear realmente una superficie de la aplicación de gran escala de todo el mundo.  Para la aplicación de ejemplo Hola se usa para este artículo, se crearon tres entornos del servicio de aplicación en una sola región de Azure (Ee.uu. Central sur).
* **Convención de nomenclatura para los entornos del servicio de aplicación Hola:** cada entorno de servicio de aplicaciones requiere un nombre único.  Más allá de uno o dos entornos del servicio de aplicación resulta útil toohave una convención de nomenclatura toohelp identificar cada entorno de servicio de aplicaciones.  Aplicación de ejemplo de Hola se usó una convención de nomenclatura simple.  Hello nombres de hello tres entornos del servicio de aplicación son *fe1ase*, *fe2ase*, y *fe3ase*.
* **Convención de nomenclatura para las aplicaciones de hello:** desde que se implementarán varias instancias de la aplicación hello, se requiere un nombre para cada instancia de la aplicación hello implementado.  Una característica de poco conocidos, pero muy cómoda de entornos del servicio de aplicación es ese hello mismo nombre de aplicación puede utilizarse en varios entornos de servicio de aplicación.  Puesto que cada entorno de servicio de aplicación tiene un sufijo de dominio único, a los desarrolladores pueden elegir usar toore Hola exacta mismo nombre de aplicación en cada entorno.  Por ejemplo, un desarrollador podría asignar los siguientes nombres a las aplicaciones:*myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net, etc*.  Para la aplicación de ejemplo de Hola aunque cada instancia de la aplicación también tiene un nombre único.  Hello aplicación instancia nombres utilizados son *webfrontend1*, *webfrontend2*, y *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Configurar perfil de Traffic Manager Hola
Una vez que se implementan varias instancias de una aplicación en varios entornos de servicio de aplicación, se pueden registrar instancias de aplicaciones individuales de hello con Traffic Manager.  Aplicación de ejemplo de Hola un administrador de tráfico de perfil es necesaria para *demo.trafficmanager.net escalable de ase* que puede enrutar con instancias de aplicación tooany de hello después de implementar los clientes:

* **webfrontend1.fe1ase.p.azurewebsites.NET:** Hola a una instancia de la aplicación de ejemplo de Hola implementada en el primer entorno de servicio de aplicación.
* **webfrontend2.fe2ase.p.azurewebsites.NET:** Hola a una instancia de la aplicación de ejemplo de Hola implementada en el segundo entorno de servicio de aplicación.
* **webfrontend3.fe3ase.p.azurewebsites.NET:** Hola a una instancia de la aplicación de ejemplo de Hola implementada en el tercer entorno de servicio de aplicaciones.

Hola tooregister de manera más fácil varios extremos de servicio de aplicaciones de Azure, ejecutan todos en hello **mismo** región de Azure, está con hello Powershell [soporte técnico de Azure Resource Manager Traffic Manager] [ ARMTrafficManager].  

Hola primer paso es toocreate un perfil de Traffic Manager de Azure.  código de Hello siguiente muestra cómo se creó el perfil de hello para la aplicación de ejemplo de Hola:

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Tenga en cuenta cómo Hola *RelativeDnsName* parámetro se establece demasiado*escalable de demostración de ase*.  Esto es cómo Hola nombre de dominio *demo.trafficmanager.net escalable de ase* está creado y asociado con un perfil de Traffic Manager.

Hola *TrafficRoutingMethod* parámetro define la directiva de Traffic Manager usará toodetermine cómo cargar toospread cliente en todos los extremos disponibles de Hola de equilibrio de carga de Hola.  En este Hola ejemplo *Weighted* método se ha elegido.  Esto provocará en las solicitudes de cliente que se va a distribuir en todos los de los extremos de la aplicación hello registrado en función de los pesos relativos Hola asociados a cada punto de conexión. 

Con el perfil de hello creado, cada instancia de la aplicación se agrega toohello perfil como un extremo de Azure nativo.  código de Hello siguiente captura una aplicación de referencia tooeach front-end web y, a continuación, agrega cada aplicación como un punto de conexión de administrador de tráfico por medio de hello *elemento TargetResourceId* parámetro.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Observe que hay una llamada demasiado*AzureTrafficManagerEndpointConfig agregar* para cada instancia de aplicación individuales.  Hola *elemento TargetResourceId* parámetro en cada comando de Powershell hace referencia a uno de tres instancias de aplicación implementada Hola.  Hola perfil de Traffic Manager repartirán la carga entre los tres extremos registrados en el perfil de Hola.

Todos Hola tres extremos utilizan Hola mismo valor (10) para hello *peso* parámetro.  Como resultado, el Administrador de tráfico distribuye las solicitudes de los clientes entre las tres instancias de la aplicación de forma relativamente uniforme. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Dominio de la aplicación hello señalador personalizado en hello dominio de Traffic Manager
Hola último paso necesario es dominio personalizado de hello toopoint de aplicación hello en el dominio de Traffic Manager Hola.  Para la aplicación de ejemplo de Hola Esto significa que señala *www.scalableasedemo.com* en *demo.trafficmanager.net escalable de ase*.  Este paso es necesario toobe completado con el registrador de dominios de Hola que administra el dominio personalizado de Hola.  

Con herramientas de administración de dominio de su registrador, un toobe de necesidades de los registros CNAME creado qué dominio personalizado de Hola de puntos en el dominio de Traffic Manager de Hola.  Figura Hola siguiente muestra un ejemplo del aspecto de esta configuración CNAME:

![CNAME para el dominio personalizado][CNAMEforCustomDomain] 

Aunque no se tratan en este tema, recuerde que cada instancia de aplicación individuales necesita toohave Hola personalizado de dominio registrado con ella también.  En caso contrario, si una solicitud de instancia de aplicación tooan facilita y aplicación hello no tiene dominio personalizado de hello registrado con la aplicación hello, solicitud de Hola se producirá un error.  

En este Hola de ejemplo es el dominio personalizado *www.scalableasedemo.com*, y cada instancia de la aplicación tiene el dominio personalizado de hello asociado a él.

![Dominio personalizado][CustomDomain] 

Para un resumen de registrar un dominio personalizado con las aplicaciones de servicio de aplicaciones de Azure, vea Hola artículo siguiente [registrar dominios personalizados][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>Probar Hola topología distribuida
Hola resultado final de la configuración de Traffic Manager y DNS de hello es que las solicitudes para *www.scalableasedemo.com* fluirá a través de hello sigue secuencia:

1. Un dispositivo o explorador realizará una búsqueda DNS de *www.scalableasedemo.com*
2. Hola entrada CNAME en el registrador de dominios de hello hace Hola DNS búsqueda toobe redirigido tooAzure Traffic Manager.
3. Se ha realizado una búsqueda de DNS para *demo.trafficmanager.net escalable de ase* en uno de los servidores de DNS de Traffic Manager de Azure Hola.
4. Según la directiva de equilibrio de carga de hello (hello *TrafficRoutingMethod* parámetro utilizado anteriormente al crear el perfil de Traffic Manager de hello), se de Traffic Manager seleccione uno de hello configura los puntos de conexión y devolver Hola FQDN de ese Explorador de toohello de punto de conexión o el dispositivo.
5. Puesto que Hola FQDN del punto de conexión de Hola Hola Url de una instancia de aplicación que se ejecuta en un entorno de servicio de aplicaciones, hello explorador o dispositivo le pedirá a un servidor DNS de Microsoft Azure hello tooresolve dirección IP de tooan FQDN. 
6. Hola explorador o dispositivo enviará Hola HTTP/solicitud toohello dirección IP.  
7. solicitud de Hello llegarán en una de las instancias de aplicación hello en uno de los entornos del servicio de aplicación Hola.

Hello figura de consola siguiente muestra una búsqueda de DNS para dominio personalizado resolver correctamente tooan aplicación instancia la aplicación de ejemplo de Hola se ejecuta en una muestra de Hola tres entornos del servicio de aplicación (en este caso Hola segundo de hello tres entornos del servicio de aplicación):

![Búsqueda DNS][DNSLookup] 

## <a name="additional-links-and-information"></a>Información y vínculos adicionales
Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

Documentación en hello Powershell [soporte técnico de Azure Resource Manager Traffic Manager][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
