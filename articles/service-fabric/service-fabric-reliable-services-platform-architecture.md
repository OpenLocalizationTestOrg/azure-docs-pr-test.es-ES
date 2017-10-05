---
title: Arquitectura de Reliable Services | Microsoft Docs
description: "Información general de la arquitectura de Reliable Services para servicios con y sin estado"
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
ms.openlocfilehash: a00a16945356b9731485554e06df46528b5c7bb2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Arquitectura para servicios de Reliable Services con y sin estado
Los servicios de Reliable Services de Azure Service Fabric pueden ser con estado o sin estado. Cada tipo de servicio se ejecuta dentro de una arquitectura específica. Estas arquitecturas se describen en este artículo.
Consulte [Información general de Reliable Services](service-fabric-reliable-services-introduction.md) para obtener más información sobre las diferencias entre los servicios con y sin estado.

## <a name="stateful-reliable-services"></a>Servicios fiables con estado
### <a name="architecture-of-a-stateful-service"></a>Arquitectura de un servicio con estado
![Diagrama de arquitectura de un servicio con estado](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Servicio fiable con estado
Los servicios de Reliable Services con estado pueden derivar de la clase StatefulService o StatefulServiceBase. Ambas clases base las proporciona Service Fabric y ofrecen diversos niveles de asistencia y abstracción para el servicio con estado para interactuar con Service Fabric y participar como un servicio en el clúster de Service Fabric.

StatefulService se deriva de StatefulServiceBase. StatefulServiceBase ofrece a los servicios una mayor flexibilidad, pero requiere más conocimiento de las interioridades de Service Fabric.
Consulte [Información general de Reliable Services](service-fabric-reliable-services-introduction.md) y [Uso avanzado de Reliable Services](service-fabric-reliable-services-advanced-usage.md) para obtener más información sobre las características específicas de escribir servicios mediante las clases StatefulService y StatefulServiceBase.

Ambas clases base administran la duración y la función de la implementación del servicio. La implementación del servicio puede invalidar los métodos virtuales de cualquier clase base si la implementación del servicio tiene trabajo que hacer en esos puntos del ciclo de vida de implementación del servicio o si desea crear un objeto de agente de escucha de comunicación. Tenga en cuenta que aunque una implementación de servicio puede implementar su propio objeto de agente de escucha de comunicación exponiendo ICommunicationListener, en el diagrama anterior, el agente de escucha de comunicación es implementado por Service Fabric mientras la implementación del servicio utiliza un agente de escucha de comunicación implementado por Service Fabric.

Los servicios de Reliable Services con estado usan Reliable State Manager para aprovechar las colecciones confiables. Las colecciones confiables son estructuras de datos locales que tienen una alta disponibilidad para su servicio, es decir, están siempre disponibles sin tener en cuenta las conmutaciones por error del servicio. Cada tipo de colección fiable es implementada mediante un proveedor de estado fiable.
Para obtener más información sobre colecciones confiables, consulte [la introducción a las colecciones confiables](service-fabric-reliable-services-reliable-collections.md)

### <a name="reliable-state-manager-and-state-providers"></a>Proveedores de estado y administrador de estado fiable
El administrador de estado confiable es el objeto que administra los proveedores de estado confiables. Tiene la funcionalidad para crear, eliminar, enumerar y asegurarse de que los proveedores de estado confiables sean persistentes y de alta disponibilidad. Una instancia de proveedor de estado confiable representa una instancia de una estructura de datos persistente y de alta disponibilidad, como un diccionario o una cola.

Cada proveedor de estado confiable expone una interfaz que es utilizada por el servicio con estado para interactuar con el proveedor de estado confiable. Por ejemplo IReliableDictionary se utiliza para interactuar con el diccionario confiable mientras que IReliableQueue se utiliza para interactuar con la cola confiable. Todos los proveedores de estado fiables implementan la interfaz IReliableState.

El administrador de estado confiable tiene una interfaz denominada IReliableStateManager, que permite acceder a ella mediante la implementación del servicio con estado. Mediante IReliableStateManager se devuelven interfaces a proveedores de estado fiables.

El administrador de estado fiable está diseñado con una arquitectura de complemento dinámica para que se puedan conectar dinámicamente nuevos tipos de colecciones fiables.

El diccionario y la cola confiables se basan en la implementación de un almacén diferencial con versiones de alto rendimiento.

### <a name="transactional-replicator"></a>Replicador de transacciones
El componente replicador de transacciones es responsable de garantizar que el estado de su servicio (que es el estado del administrador de estado confiable y las colecciones confiables) es coherente en todas las réplicas que se ejecutan en su servicio. También garantiza que ese estado también persiste en el registro. El administrador de estado fiable interactúa con el replicador de transacciones a través de un mecanismo privado.

El replicador de transacciones usa un protocolo de red para comunicar el estado con otras réplicas de la instancia de servicio para que todas las réplicas dispongan de información de estado actualizada.

El replicador de transacciones usa un registro para conservar información de estado para que la información de estado sobreviva a bloqueos del proceso o el nodo. La interacción con el registro se efectúa a través de un mecanismo privado.

### <a name="log"></a>Registro
El componente de registro proporciona un almacén persistente de alto rendimiento que se puede optimizar para escribir en discos de estado giratorio o sólidos.  El diseño del registro es para que el almacenamiento persistente (es decir, discos duros) sea local en los nodos que ejecutan el servicio con estado. Esto permite bajas latencias y un alto rendimiento en comparación con el almacenamiento persistente remoto, que no es local en el nodo.

El componente de registro usa varios tipos de archivos de registro. Hay un archivo de registro compartido de todo el nodo que usan todas las réplicas porque puede proporcionar la menor latencia y el rendimiento máximo para almacenar los datos de estado. De forma predeterminada, el registro compartido se coloca en el directorio de trabajo del nodo de Service Fabric, pero también puede configurarse para que se ponga en otra ubicación (lo ideal sería que se pusiese en un disco reservado solo para el registro compartido). Cada réplica del servicio también tiene un archivo de registro dedicado, y el registro dedicado se coloca en el directorio de trabajo del servicio. No hay ningún mecanismo para configurar el registro dedicado de modo que se coloque en una ubicación diferente.

El registro compartido es un área de transición para la información de estado de la réplica y el archivo de registro dedicado es el destino final, donde se almacena. En este diseño la información de estado se escribe, en primer lugar, en el archivo de registro compartido y después se mueve de forma diferida al archivo de registro dedicado en segundo plano. De esta manera, la escritura en el registro compartido tendría la latencia más baja y el máximo rendimiento, lo que permite que el servicio progrese con mayor rapidez.

Las lecturas y escrituras en el registro compartido se realizan a través de E/S directas en el espacio preasignado en el disco para el archivo de registro compartido. Para permitir un uso óptimo del espacio en disco en la unidad con registros dedicados, se crea el archivo de registro dedicado como un archivo disperso de NTFS. Tenga en cuenta que esto permitirá un aprovisionamiento en exceso del espacio en disco y el sistema operativo mostrará los archivos de registro dedicados con mucho más espacio en disco del que se usa realmente.

Además de una interfaz de modo de usuario mínima en el registro, el registro se escribe como un controlador en modo kernel. Mediante la ejecución como un controlador de modo kernel, el registro puede proporcionar el máximo rendimiento a todos los servicios que lo utilizan.

Para obtener más información sobre cómo configurar el registro, consulte [Configuración de Reliable Services con estado](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Servicio fiable sin estado
### <a name="architecture-of-a-stateless-service"></a>Arquitectura de un servicio sin estado
![Diagrama de arquitectura de un servicio sin estado](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Servicio fiable sin estado
Las implementaciones de servicios sin estado se derivan de la clase StatelessService o StatelessServiceBase. La clase StatelessServiceBase permite más flexibilidad que la clase StatelessService.
Ambas clases base administran la duración y el rol del servicio.

La implementación del servicio puede invalidar los métodos virtuales de cualquier clase base si el servicio tiene trabajo que hacer en esos puntos del ciclo de vida de servicio o si desea crear un objeto de agente de escucha de comunicación. Tenga en cuenta que aunque es posible que el servicio puede implementar su propio objeto de agente de escucha de comunicación exponiendo ICommunicationListener, en el diagrama anterior, el agente de escucha de comunicación es implementado por Service Fabric mientras la implementación del servicio utiliza un agente de escucha de comunicación implementado por Service Fabric.

Consulte [Información general de Reliable Services](service-fabric-reliable-services-introduction.md) y [Uso avanzado de Reliable Services](service-fabric-reliable-services-advanced-usage.md) para obtener más información sobre las características específicas de escribir servicios mediante las clases StatelessService y StatelessServiceBase.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de Service Fabric, consulte:

[Información general del servicio confiable](service-fabric-reliable-services-introduction.md)

[Inicio rápido](service-fabric-reliable-services-quick-start.md)

[Información general sobre colecciones confiables](service-fabric-reliable-services-reliable-collections.md)

[Uso avanzado de un servicio confiable](service-fabric-reliable-services-advanced-usage.md)

[Configuración de un servicio confiable](service-fabric-reliable-services-configuration.md)  

