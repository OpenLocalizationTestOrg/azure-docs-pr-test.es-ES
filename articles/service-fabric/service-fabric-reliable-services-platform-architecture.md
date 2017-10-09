---
title: arquitectura del servicio aaaReliable | Documentos de Microsoft
description: "Información general de arquitectura de servicio confiable de Hola para los servicios con estado y sin estado"
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Arquitectura para servicios de Reliable Services con y sin estado
Los servicios de Reliable Services de Azure Service Fabric pueden ser con estado o sin estado. Cada tipo de servicio se ejecuta dentro de una arquitectura específica. Estas arquitecturas se describen en este artículo.
Vea hello [Introducción al servicio confiable](service-fabric-reliable-services-introduction.md) para obtener más información acerca de las diferencias de hello entre los servicios con estado y sin estado.

## <a name="stateful-reliable-services"></a>Servicios fiables con estado
### <a name="architecture-of-a-stateful-service"></a>Arquitectura de un servicio con estado
![Diagrama de arquitectura de un servicio con estado](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Servicio fiable con estado
Un servicio confiable con estado pueden derivar de hello StatefulService o clase StatefulServiceBase. Ambas clases base las proporciona Service Fabric Ofrecen diferentes niveles de abstracción para hello toointerface de servicio con estado con Service Fabric--y tooparticipate como un servicio en clúster de Service Fabric hello y soporte técnico.

StatefulService se deriva de StatefulServiceBase. StatefulServiceBase ofrece servicios de más flexibilidad, pero requiere más conocimientos de funcionamiento interno de Hola de Service Fabric.
Vea hello [Introducción al servicio confiable](service-fabric-reliable-services-introduction.md) y [servicio confiable uso avanzado de](service-fabric-reliable-services-advanced-usage.md) para obtener más información sobre los detalles de Hola de escribir servicios mediante las clases de StatefulService y StatefulServiceBase Hola .

Ambas clases base administran la duración de Hola y el rol de implementación del servicio Hola. implementación del servicio Hola puede invalidar métodos virtuales de cualquier clase base si implementación del servicio hello tiene toodo de trabajo en esos puntos del ciclo de vida de la implementación del servicio de hello, o si desea toocreate un objeto de agente de escucha de comunicación. Tenga en cuenta que aunque una implementación de servicio puede implementar su propio objeto de agente de escucha de comunicación exponer ICommunicationListener, en el diagrama de hello anterior, el agente de escucha de hello comunicación se implementa con Service Fabric--como Hola implementación del servicio utiliza un agente de escucha de comunicación que se implementa mediante Service Fabric.

Un servicio confiable con estado utiliza Hola estado confiable manager tootake aprovechar colecciones confiables. Colecciones confiables son estructuras de datos locales que son toohello alta disponibilidad del servicio, que es, siempre están disponibles, independientemente de las conmutaciones por error de servicio. Cada tipo de colección fiable es implementada mediante un proveedor de estado fiable.
Para obtener más información sobre colecciones confiables, vea hello [información general sobre colecciones confiable](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Proveedores de estado y administrador de estado fiable
el Administrador de estado confiable Hello es objeto de Hola que administra los proveedores de estado confiable. Tiene Hola funcionalidad toocreate, eliminar, enumerar y asegúrese de que los proveedores de estado confiable Hola son persistentes y alta disponibilidad. Una instancia de proveedor de estado confiable representa una instancia de una estructura de datos persistente y de alta disponibilidad, como un diccionario o una cola.

Cada proveedor de estado de confianza expone una interfaz que usa un toointeract de servicio con estado con el proveedor de estado confiable de Hola. Por ejemplo, IReliableDictionary es toointerface usado con diccionario confiable de hello, mientras IReliableQueue es toointerface usado con cola confiable de Hola. Todos los proveedores de estado confiable Implementar interfaz IReliableState de Hola.

el Administrador de estado confiable Hello tiene una interfaz denominada IReliableStateManager, lo que permite tooit de acceso de un servicio con estado. Se devuelven los proveedores de estado de interfaces tooreliable a través de IReliableStateManager.

el Administrador de estado confiable Hola utiliza una arquitectura de complemento para que los nuevos tipos de colecciones confiables se pueden conectar dinámicamente.

diccionario confiable de Hola y cola confiable se basan en la implementación de Hola de un almacén de diferencial de alto rendimiento, con control de versiones.

### <a name="transactional-replicator"></a>Replicador de transacciones
componente del replicador transaccional de Hello es responsable de garantizar que el estado de Hola de un servicio (es decir, el estado de hello en Administrador de estado confiable de Hola y colecciones confiable hello) sea coherente en todas las réplicas que se ejecuta el servicio de Hola. También se asegura de que el estado de Hola se mantiene en el registro de hello. Hola interfaces de administrador de estado confiable con replicador transaccional de Hola a través de un mecanismo privado.

Replicador transaccional de Hello usa un estado de toocommunicate de protocolo de red con otras réplicas de instancia de servicio de Hola para que todas las réplicas tienen información de estado actualizada.

Replicador transaccional de Hello usa una información de estado de registro toopersist para que la información de estado de hello sobrevive proceso o nodo se bloquea. registro de Hello interfaz toohello es a través de un mecanismo privado.

### <a name="log"></a>Registro
componente de registro de Hello proporciona un almacén persistente de alto rendimiento que se puede optimizar para escribir toospinning o discos de estado sólido.  diseño de Hola de registro de hello es para el almacenamiento persistente de hello (es decir, discos duros) toobe toohello local nodos que ejecutan el servicio con estado Hola. Esto permite latencias de bajas y alto rendimiento, como tooremote en comparación con el almacenamiento persistente, que no es el nodo de toohello local.

componente de registro de Hello usa varios archivos de registro. Hay un archivo de registro compartido de todo el nodo que todas las réplicas que se usan como puede proporcionar mayor rendimiento y latencia más baja de Hola para almacenar los datos de estado. De forma predeterminada registro compartido Hola se coloca en el directorio de trabajo de nodo de Service Fabric Hola pero también puede ser configurado toobe colocada en otra ubicación, lo ideal es que en un disco reservado para sólo registro compartido Hola. Cada réplica para el servicio de hello también tiene un archivo de registro dedicado y registro dedicado Hola se coloca en el directorio de trabajo del servicio de Hola. No hay ningún toobe de registro de hello dedicado de tooconfigure mecanismo colocada en una ubicación diferente.

registro compartido Hello es un área de transición para obtener información de estado de la réplica de hello, mientras Hola archivo de registro dedicado es el destino final Hola donde se conservan. En este diseño, información de estado de hello es el primer archivo de registro compartido toohello escrito y, a continuación, mover de forma diferida toohello archivos de registro dedicado en segundo plano de Hola. De esta manera, hello toohello escribir el registro compartido tendría latencia más baja de Hola y mayor rendimiento que permite toomake progreso del servicio de hello con mayor rapidez.

Lecturas y escrituras de registro compartido toohello se realiza a través de directa espacio de toopreallocated de E/S en disco de Hola Hola compartido archivo de registro. tooallow un uso óptimo del espacio en disco en la unidad de hello con registros dedicados, archivos de registro dedicado Hola se crean como un archivo disperso de NTFS. Tenga en cuenta que esto le permitirá exceso de espacio en disco y Hola SO mostrará los archivos de registro de hello dedicado mediante mucho más espacio en disco que se usa realmente.

Además de un registro de toohello de interfaz mínima de modo de usuario, el registro de hello se escribe como un controlador de modo kernel. Al ejecutarse como un controlador de modo kernel, registro de hello puede proporcionar mayor rendimiento de hello servicios tooall que lo usan.

Para obtener más información acerca de cómo configurar el registro de hello, consulte [configurar servicios de confianza con estado](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Servicio fiable sin estado
### <a name="architecture-of-a-stateless-service"></a>Arquitectura de un servicio sin estado
![Diagrama de arquitectura de un servicio sin estado](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Servicio fiable sin estado
Las implementaciones de servicios sin estado se derivan de Hola StatelessService o clase StatelessServiceBase. Hola StatelessServiceBase clase permite más flexibilidad que hello StatelessService clase.
Ambas clases base administran la vigencia de Hola y el rol de un servicio.

implementación del servicio Hola puede invalidar métodos virtuales de cualquier clase base si servicio hello tiene toodo de trabajo en esos puntos del ciclo de vida de servicio de hello--o si desea toocreate un objeto de agente de escucha de comunicación. Tenga en cuenta que aunque el servicio de hello puede implementar su propio objeto de agente de escucha de comunicación exponer ICommunicationListener, en el diagrama de hello anterior, el agente de escucha de hello comunicación se implementa con Service Fabric, como esa implementación del servicio utiliza una comunicación agente de escucha que se implementa mediante Service Fabric.

Vea hello [Introducción al servicio confiable](service-fabric-reliable-services-introduction.md) y [servicio confiable uso avanzado de](service-fabric-reliable-services-advanced-usage.md) para obtener más información sobre los detalles de Hola de escribir servicios mediante las clases de StatelessService y StatelessServiceBase Hola .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de Service Fabric, consulte:

[Información general del servicio confiable](service-fabric-reliable-services-introduction.md)

[Inicio rápido](service-fabric-reliable-services-quick-start.md)

[Información general sobre colecciones confiables](service-fabric-reliable-services-reliable-collections.md)

[Uso avanzado de un servicio confiable](service-fabric-reliable-services-advanced-usage.md)

[Configuración de un servicio confiable](service-fabric-reliable-services-configuration.md)  

