---
title: aaaOverview de Service Fabric en Azure | Documentos de Microsoft
description: "Introducción a Service Fabric, donde las aplicaciones se componen de muchos microservicios tooprovide escala y resistencia. Service Fabric es una plataforma de sistemas distribuidos utiliza toobuild escalable, confiable y administra fácilmente aplicaciones de nube de Hola."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Información general de Azure Service Fabric
Azure Service Fabric es una plataforma de sistemas distribuidos que resulta fácil toopackage, implementar y administrar contenedores y microservicios escalables y confiables. Service Fabric también aborda retos significativos de hello en desarrollar y administrar aplicaciones nativas de nube. Los desarrolladores y administradores pueden evitar problemas complejos de infraestructura y centrarse en su lugar en las cargas de trabajo más exigentes y críticas que son escalables, confiables y fáciles de administrar. Service Fabric representa la plataforma de próxima generación de Hola para generar y administrar estos empresariales, nivel 1, aplicaciones de escala de nube que se ejecutan en contenedores.

En este breve vídeo se presentan Service Fabric y los microservicios: <center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Aplicaciones compuestas por microservicios 
Service Fabric permite toobuild y administrar aplicaciones escalables y confiables que se compone de microservicios que la ejecución de alta densidad en un grupo compartido de máquinas, que se denomina tooas un clúster de. Proporciona un toobuild en tiempo de ejecución sofisticados y ligera distribuido, microservicios escalables, sin estado y con estado ejecutar en contenedores. También proporciona tooprovision de capacidades de administración de aplicación completa, implementar, supervisar, actualización o revisión y eliminar las aplicaciones implementadas, incluidos los servicios en contenedores.

En la actualidad, Service Fabric se utiliza en muchos servicios Microsoft, como Azure SQL Database, Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Azure IoT Hub, Dynamics 365, Skype Empresarial y muchos servicios principales de Azure.

Service Fabric es toocreate adaptada nativo servicios en la nube que pueden empezar siendo pequeños, según sea necesario y aumentar la escala de toomassive con cientos o miles de equipos.

Actualmente, los servicios de escala de Internet se crean a partir de microservicios. Entre los ejemplos de microservicios se encuentran las puertas de enlace de protocolo, perfiles de usuario, carros de la compra, procesamiento de inventario, colas y memorias caché. Service Fabric es una plataforma de microservicios que da a cada microservicio (o contenedor) un nombre único con o sin estado.

Service Fabric proporciona completa en tiempo de ejecución y el ciclo de vida de administración capacidades tooapplications que se componen de estos microservicios. Hospeda microservicios dentro de contenedores que se han implementado y activado en el clúster de Service Fabric Hola. Un movimiento de máquinas virtuales toocontainers permite un aumento de orden de magnitud en la densidad. De forma similar, otra orden de magnitud en la densidad es posible cuando se mueve de toomicroservices de contenedores en estos contenedores. Por ejemplo, un único clúster de Azure SQL Database se compone de cientos de máquinas que ejecutan decenas de miles de contenedores que hospedan un total de cientos de miles de bases de datos. Cada base de datos es un microservicio con estado de Service Fabric. 

¿Para obtener más información sobre el enfoque de microservicios hello, lea [por qué un microservicios enfoque toobuilding las aplicaciones?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Organización e implementación de contenedores
Service Fabric es el [orquestador de contenedores](service-fabric-cluster-resource-manager-introduction.md) de Microsoft que implementa microservicios en un clúster de máquinas. Se pueden desarrollar Microservicios de muchas maneras de usar Hola [modelos de programación de Service Fabric](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [cualquier código de su elección](service-fabric-deploy-existing-app.md). Lo que es importante, puede mezclar los servicios de procesos y servicios en contenedores en hello misma aplicación. Si su intención es demasiado[implementar y administrar contenedores](service-fabric-containers-overview.md), Service Fabric es una opción perfecta como un orquestador del contenedor.

## <a name="any-os-any-cloud"></a>Cualquier sistema operativo, cualquier nube
Service Fabric se ejecuta en todas partes. Puede crear clústeres de Service Fabric en muchos entornos, incluido Azure o en entornos locales, en Windows Server o en Linux. Incluso puede crear clústeres en otras nubes públicas. Además, es el entorno de desarrollo de Hola Hola SDK **idénticos** toohello entorno de producción, con ningún emuladores implicados. En otras palabras, lo que se ejecuta en el clúster de desarrollo local, implementa toohello clústeres en otros entornos.

![Plataforma de Service Fabric][Image1]

Para obtener más información sobre la creación de clústeres local, leer [creación de un clúster en Windows Server o Linux](service-fabric-deploy-anywhere.md) o para crear un clúster de Azure [a través del portal de Azure hello](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microservicios de Service Fabric con estado y sin estado
Service Fabric también permite que las aplicaciones de toobuild que constan de microservicios o contenedores. Microservicios sin estado (por ejemplo, las puertas de enlace de protocolo y servidores proxy web) no mantienen un estado mutable fuera de una solicitud y su respuesta de servicio de Hola. Los roles de trabajo de los servicios en la nube de Azure son un ejemplo de servicio sin estado. Microservicios con estado (por ejemplo, las cuentas de usuario, las bases de datos, dispositivos, compra Amazon y colas) mantienen un estado mutable, autorizado más allá de la solicitud de Hola y su respuesta. Actualmente, las aplicaciones de escala de Internet se componen de una combinación de microservicios con estado y sin estado. 

Una clave differentation con Service Fabric es la gran importancia en la creación de servicios con estado, ya sea con hello [modelos de programación integrados ](service-fabric-choose-framework.md) o con los servicios con estado en contenedores. Hola [escenarios de aplicación](service-fabric-application-scenarios.md) describen escenarios de Hola donde se usan los servicios con estado.


## <a name="application-lifecycle-management"></a>Administración del ciclo de vida de aplicación
Service Fabric proporciona compatibilidad para ciclo de vida completo de la aplicación de Hola y CI/CD de aplicaciones en la nube incluidos contenedores. Este ciclo de vida incluye el desarrollo a través de la implementación, la administración diaria y la retirada de tooeventual de mantenimiento.

Capacidades de administración de ciclo de vida de aplicación de Service Fabric permiten que los administradores de aplicación y TI operadores toouse flujos de trabajo simple y de bajo nivel interactivo tooprovision, implementación, revisiones y supervisión aplicaciones. Estos flujos de trabajo integrados reducen considerablemente la carga de hello en aplicaciones de tookeep de TI operadores disponibles continuamente.

La mayoría de las aplicaciones se componen de una combinación de microservicios con estado y sin estado, contenedores y otros ejecutables que se implementan juntos. Si tiene tipos seguros en las aplicaciones de hello, Service Fabric permite la implementación de Hola de varias instancias de aplicación. Cada instancia se administra y actualiza de manera independiente. Lo importante es que Service Fabric puede implementar contenedores o cualquier ejecutable y hacer que sean confiables. Por ejemplo, Service Fabric puede implementar .NET, ASP.NET Core, node.js, contenedores de Windows, contenedores de Linux, máquinas virtuales Java, scripts, Angular o literalmente todo lo que compone la aplicación.

Service Fabric se integra con herramientas de CI/CD como [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html) y [Octopus Deploy](https://octopus.com/), y puede utilizarse con cualquier otra herramienta de CI/CD popular.

Para más información sobre la administración del ciclo de vida de las aplicaciones, lea [Ciclo de vida de la aplicación de Service Fabric](service-fabric-application-lifecycle.md). Para obtener más información acerca de cómo toodeploy cualquier código, consulte [implementar un archivo ejecutable de invitado](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Principales capacidades
Usando Service Fabric, puede:

* Implemente los centros de datos de tooAzure o tooon locales que ejecutan Windows o Linux con cero cambios en el código. Escribir una vez y, a continuación, implementar en cualquier lugar tooany clúster de Service Fabric.
* Desarrollar aplicaciones escalables que constan de microservicios mediante el uso de modelos de programación de Service Fabric hello, contenedores o cualquier código.
* Desarrollar microservicios con estado y sin estado que desean de alta confianza. Simplificar el diseño de saludo de la aplicación mediante el uso de microservicios con estado. 
* Utilice Hola novel Reliable Actors programación modelo toocreate objetos de nube con estado y código autocontenidas.
* Implementar y orquestar contenedores que incluyen contenedores de Windows y de Linux. Service Fabric es un orquestador de contenedores, con estado y reconocimiento de datos.
* Implementar aplicaciones en segundos, con una elevada densidad de cientos o miles de aplicaciones o contenedores por máquina.
* Implementar distintas versiones de hello misma aplicación en paralelo y actualizar cada aplicación de forma independiente.
* Administrar el ciclo de vida de Hola de las aplicaciones sin tiempo de inactividad, incluidas las actualizaciones de última hora y sin interrupción.
* Escalar horizontalmente o escalar en número de Hola de nodos de un clúster. Según se escalan los nodos, las aplicaciones se escalan automáticamente.
* Supervisar y diagnosticar el estado de Hola de las aplicaciones y establecer directivas para llevar a cabo reparaciones automáticas.
* Ver equilibrador de recursos de hello orquestar la redistribución de Hola de aplicaciones en el clúster de Hola. Tejido de servicio se recupera de los errores y optimiza la distribución de Hola de carga en función de los recursos disponibles.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información:
  * [¿Por qué un microservicios enfocar toobuilding aplicaciones?](service-fabric-overview-microservices.md)
  * [Información general sobre la terminología](service-fabric-technical-overview.md)
* Configuración del [entorno de desarrollo](service-fabric-get-started.md)  
* Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
