---
title: aaaDifferences entre servicios en la nube y el tejido de servicio | Documentos de Microsoft
description: "Información general y conceptual para migrar las aplicaciones de servicios en la nube tooService tejido."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>Obtenga información acerca de las diferencias de hello entre servicios en la nube y el tejido de servicio antes de migrar las aplicaciones.
Microsoft Azure Service Fabric es la plataforma de aplicaciones de nube de próxima generación de Hola para las aplicaciones distribuidas altamente escalables, altamente confiables. Presenta muchas características nuevas para empaquetar, implementar, actualizar y administrar aplicaciones distribuidas en la nube. 

Se trata de una aplicación de toomigrating de guía de introducción de servicios en la nube tooService tejido. Se centra principalmente en las diferencias de diseño y arquitectura entre Servicios en la nube y Service Fabric.

## <a name="applications-and-infrastructure"></a>Infraestructura y aplicaciones
Una diferencia fundamental entre los servicios en la nube y el tejido de servicio es la relación de hello entre las máquinas virtuales, las cargas de trabajo y aplicaciones. A continuación una carga de trabajo se define como código de hello escribir tooperform una tarea específica o proporcionar un servicio.

* **Servicios en la nube tiene que ver con la implementación de aplicaciones como máquinas virtuales.** código de Hello que escribe es instancia de máquina virtual de tooa estrechamente acopladas, por ejemplo, un rol Web o trabajo. toodeploy una carga de trabajo de servicios en la nube es toodeploy uno o más VM instancias esa carga de trabajo de ejecución Hola. No hay ninguna separación de las aplicaciones y las máquinas virtuales, por lo que no hay ninguna definición formal de una aplicación. Una aplicación puede considerarse un conjunto de instancias de rol de trabajo o web dentro de una implementación de Servicios en la nube o como una implementación completa de Servicios en la nube. En este ejemplo, se muestra una aplicación como un conjunto de instancias de rol.

![Aplicaciones y topología de Servicios en la nube][1]

* **Service Fabric es sobre la implementación de aplicaciones tooexisting máquinas virtuales o máquinas que se ejecutan Service Fabric en Windows o Linux.** Servicios de Hello que escribe están completamente desacoplados de hello subyacente de la infraestructura, que se abstrae mediante la plataforma de aplicaciones de Service Fabric hello, por lo que una aplicación puede ser implementado toomultiple entornos. Una carga de trabajo de Service Fabric se conoce como un "servicio"; uno o más servicios se agrupan en una aplicación formalmente definidos por el que se ejecuta en la plataforma de aplicaciones de Service Fabric Hola. Varias aplicaciones pueden ser implementado tooa único clúster de Service Fabric.

![Aplicaciones y topología de Service Fabric][2]

Service Fabric en sí es una capa de la plataforma de aplicaciones que se ejecuta en Windows o Linux, mientras que Servicios en la nube es un sistema para la implementación de máquinas virtuales administradas de Azure con cargas de trabajo asociadas.
modelo de aplicaciones de Service Fabric Hello tiene una serie de ventajas:

* Tiempos de implementación rápidos. La creación de instancias de máquina virtual puede llevar mucho tiempo. En el tejido de servicio, las máquinas virtuales se implementan solo una vez tooform un clúster que hospeda Hola plataforma de aplicaciones de Service Fabric. Desde ese momento, los paquetes de aplicación pueden ser implementado toohello clúster muy rápidamente.
* Hospedaje de alta densidad. En Servicios en la nube, una máquina virtual de rol de trabajo hospeda una carga de trabajo. En el tejido de servicio, las aplicaciones son independientes de hello las máquinas virtuales que se ejecutan, lo que significa que puede implementar un gran número de aplicaciones tooa pocas máquinas virtuales, que pueden reducir el costo total para implementaciones más grandes.
* Hola Service Fabric plataforma puede ejecutarse en cualquier lugar que tiene equipos de Windows Server o Linux, ya sea local o Azure. plataforma de Hello proporciona una capa de abstracción a través de la infraestructura subyacente de Hola para que la aplicación pueda ejecutarse en distintos entornos. 
* Administración de aplicaciones distribuidas. Service Fabric es una plataforma que no solo hospeda las aplicaciones distribuidas, pero también le ayuda a administrar su ciclo de vida independientemente Hola hospeda la máquina virtual o del ciclo de vida de la máquina.

## <a name="application-architecture"></a>Arquitectura de la aplicación
Hello arquitectura de una aplicación de servicios en la nube normalmente incluye numerosas dependencias externas, como Service Bus, tabla de Azure y almacenamiento de blobs, SQL, Redis y otros toomanage Hola estado y los datos de una aplicación y la comunicación entre Web y los Roles de trabajo en una implementación de servicios en la nube. Un ejemplo de una aplicación de Servicios en la nube completa podría tener este aspecto:  

![Arquitectura de Servicios en la nube][9]

Aplicaciones de Service Fabric también pueden elegir toouse Hola mismo servicios externos en una aplicación completa. Con este ejemplo de arquitectura de servicios en la nube, Hola la ruta de acceso de migración más sencilla de servicios en la nube tooService tejido es tooreplace implementación solo para hello servicios en la nube con una aplicación de Service Fabric, mantener Hola arquitectura global Hola igual. Hola Web y Roles de trabajo pueden ser servicios sin estado de Fabric tooService migrado con cambios mínimos en el código.

![Arquitectura de Service Fabric después de una migración simple][10]

En esta fase, debe continuar sistema hello toowork Hola igual que antes. Aprovechando las características con estado de Service Fabric, los almacenes de estado externos se pueden internalizar como servicios con estado, cuando corresponda. Esto es más complicado que una migración simple de servicios Web y Roles de trabajo tooService tejido sin estado, ya que requiere servicios personalizados que proporcionan aplicaciones de tooyour una funcionalidad equivalente como servicios externos Hola hacían antes de escribir. Hola ventajas de hacerlo se incluyen: 

* Eliminación de dependencias externas 
* Implementación de Hola y unificador, administración y modelos de actualización. 

Una arquitectura de ejemplo resultante de internalizar estos servicios podría tener este aspecto:

![Arquitectura de Service Fabric después de una migración completa][11]

## <a name="communication-and-workflow"></a>Comunicación y flujo de trabajo
La mayoría de las aplicaciones del Servicio en la nube constan de más de un nivel. De forma similar, una aplicación de Service Fabric consta de más de un servicio (normalmente muchos servicios). Dos modelos de comunicación comunes son la comunicación directa y a través de un almacenamiento externo duradero.

### <a name="direct-communication"></a>Comunicación directa
Con la comunicación directa, los niveles pueden comunicarse directamente a través del punto de conexión expuesto por cada nivel. En entornos sin estado como servicios en la nube, este significa que al seleccionar una instancia de un rol de VM, ya sea al azar o carga de round robin toobalance y conecta tooits endpoint directamente.

![Comunicación directa de Servicios en la nube][5]

 La comunicación directa es un modelo de comunicación común en Service Fabric. Hola principal diferencia entre Service Fabric y servicios en la nube es que servicios en la nube conectarse tooa máquina virtual, mientras que en el tejido de servicio se conecta el servicio de tooa. Esta distinción es importante por dos motivos:

* Servicios de Service Fabric no son máquinas virtuales de toohello enlazado que hospedan; servicios puede moverse por clúster de Hola y de hecho, son toomove esperado alrededor por varias razones: equilibrio de recursos, conmutación por error, las actualizaciones de aplicaciones y la infraestructura y las restricciones de posición o de carga. Esto significa que la dirección de una instancia de servicio se puede cambiar en cualquier momento. 
* En Service Fabric, una máquina virtual puede hospedar varios servicios, cada uno con puntos de conexión únicos.

Service Fabric proporciona un mecanismo de detección de servicio, llamado hello servicio de nombres, que puede ser usado tooresolve direcciones de extremo de servicios. 

![Comunicación directa de Service Fabric][6]

### <a name="queues"></a>Colas
Un mecanismo de comunicación común entre las capas de entornos sin estado como servicios en la nube es toouse un toodurably de cola de almacenamiento externo almacenar las tareas de trabajo de un nivel tooanother. Un escenario común es un nivel de web que envía trabajos tooan cola de Azure o Bus de servicio donde pueden quitar de la cola y procese los trabajos de hello instancias de rol de trabajo.

![Comunicación mediante la cola de Servicios en la nube][7]

Hola puede utilizarse el mismo modelo de comunicación de Service Fabric. Esto puede ser útil cuando se migra un tooService de aplicación de servicios en la nube tejido existente. 

![Comunicación directa de Service Fabric][8]

## <a name="next-steps"></a>Pasos siguientes
Hello ruta de migración más sencilla de tooService de servicios en la nube Fabric es tooreplace solo hello implementación de servicios en la nube con una aplicación de Service Fabric, mantener Hola arquitectura global de la aplicación aproximadamente Hola igual. Hola artículo siguiente proporciona a una guía toohelp convert un tooa de rol de trabajo Web o de servicio sin estado de Service Fabric.

* [Migración simple: convertir un tooa de rol de trabajo Web o de servicio sin estado de Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
