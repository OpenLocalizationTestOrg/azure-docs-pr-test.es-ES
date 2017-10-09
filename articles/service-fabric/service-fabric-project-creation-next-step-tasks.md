---
title: "pasos siguientes de la creación del proyecto de aaaService tejido | Documentos de Microsoft"
description: "Este artículo contiene vínculos tooa formado por tareas de desarrollo principal de Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>Su aplicación de Service Fabric y próximos pasos
La aplicación Azure Service Fabric se ha creado. Este artículo describe la composición de Hola de su proyecto y algunos pasos posibles.

## <a name="your-application"></a>Su aplicación
Cada nueva aplicación incluye un proyecto de aplicación. Puede haber uno o dos proyectos adicionales, según tipo hello del servicio elegido.

### <a name="hello-application-project"></a>proyecto de aplicación Hola
proyecto de aplicación Hola consta de:

* Un conjunto de servicios de toohello de referencias que conforman la aplicación.
* Tres publican perfiles (nodo 1 Local, 5 nodos locales así como en la nube) que se pueden usar toomaintain preferencias para trabajar con entornos diferentes: como punto de conexión de clúster de preferencias tooa relacionados y si tooperform actualizar las implementaciones de forma predeterminada.
* Tres archivos parámetro de aplicación (igual que arriba) que puede utilizar configuraciones de aplicación específica del entorno de toomaintain, como el número de Hola de toocreate de particiones para un servicio.
* Un script de implementación que puede utilizar toodeploy la aplicación de línea de comandos de Hola o como parte de una canalización de integraciones e implementaciones continua automatizada.
* manifiesto de aplicación Hello, que describe la aplicación hello. Puede encontrar Hola manifiesto en la carpeta de ApplicationPackageRoot Hola.

### <a name="stateless-service"></a>Servicio sin estado
Cuando se agrega un nuevo servicio sin estado, Visual Studio agrega una solución de tooyour de proyecto de servicio que incluye un tipo desciende de `StatelessService`. servicio de Hello incrementa una variable local en un contador.

### <a name="stateful-service"></a>Servicio con estado
Cuando se agrega un nuevo servicio con estado, Visual Studio agrega una solución de tooyour de proyecto de servicio que incluye un tipo desciende de `StatefulService`. servicio Hello incrementa un contador en su `RunAsync` (método) y almacena el resultado de hello en un `ReliableDictionary`.

### <a name="actor-service"></a>Servicio de actor
Cuando se agrega un nuevo actor confiable, Visual Studio agrega dos soluciones de tooyour de proyectos: un proyecto de actor y un proyecto de interfaz.

proyecto de actor Hola proporciona métodos para la configuración y obtener valor de Hola de un contador que se conserva de forma confiable dentro estado del actor Hola. Hello proyecto interfaz proporciona una interfaz que otros servicios pueden usar actor de hello tooinvoke.

### <a name="stateless-web-api"></a>API web sin estado
proyecto de API Web sin estado Hola proporciona básico que puede usar tooopen los clientes de tooexternal de aplicación de servicio web. Para obtener más información acerca de cómo se estructura proyecto hello, consulte [servicios de API Web del servicio tejido con OWIN hospeda a sí mismo](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>ASP.NET Core
Hola SDK del servicio de Fabric proporciona Hola al mismo conjunto de plantillas de ASP.NET Core que están disponibles para los proyectos ASP.NET Core de independiente: vacía, [API Web][aspnet-webapi], y [aplicación Web][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Ejecutables y contenedores de invitado

Un tejido de servicio 'guest' es un servicio que no se compila con modelos de programación de la plataforma de Hola. Puede empaquetar los archivos binarios de Hola o para un invitado [directamente en paquete de aplicación Hola](service-fabric-deploy-existing-app.md) o [a través de una imagen de contenedor](service-fabric-deploy-container.md). En ambos casos, Visual Studio crea Hola artefactos necesarios en hello **ApplicationPackageRoot** carpeta de proyecto de aplicación Hola. Visual Studio no creará un nuevo proyecto de servicio porque el código de hello ya existe en otra parte. Si desea que toomanage invitado proyectos junto con el proyecto de aplicación de Service Fabric hello, puede agregarlos toohello misma solución de Visual Studio.

## <a name="next-steps"></a>Pasos siguientes
### <a name="create-an-azure-cluster"></a>Creación de un clúster de Azure
Hola SDK del servicio tejido proporciona un clúster local para desarrollo y pruebas. toocreate un clúster de Azure, consulte [configuración de un clúster de Service Fabric de hello portal de Azure][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Publicar su aplicación tooAzure
Puede publicar su aplicación directamente desde Visual Studio tooan clúster de Azure. cómo hacerlo, consulte toolearn [publicar su aplicación tooAzure][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Utilizar el Explorador de Service Fabric toovisualize su clúster
Explorador de Service Fabric ofrece una manera sencilla de toovisualize su clúster, incluidas las aplicaciones implementadas y el diseño físico. más información, consulte toolearn [visualizar el clúster mediante el uso de Service Fabric Explorer][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Control de versiones y actualización de los servicios
Service Fabric permite el control de versiones independiente y la actualización de servicios independientes en una aplicación. más información, consulte toolearn [control de versiones y actualizar los servicios][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Configuración de la integración continua con Visual Studio Team Services
toolearn cómo puede configurar un proceso de integración continua para la aplicación de Service Fabric, vea [configurar la integración continua con Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
