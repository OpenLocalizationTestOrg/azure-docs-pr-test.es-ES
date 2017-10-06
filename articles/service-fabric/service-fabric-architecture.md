---
title: aaaArchitecture de Azure Service Fabric | Documentos de Microsoft
description: "Service Fabric es que una plataforma de sistemas distribuidos utiliza toobuild escalable, confiable y administrar con facilidad aplicaciones de nube Hola. Este artículo muestra la arquitectura de Hola de Service Fabric."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Arquitectura de Service Fabric
Service Fabric está construido con subsistemas en capas. Estos subsistemas le permiten aplicaciones toowrite que son:

* Alta disponibilidad
* Escalable
* Capacidad de administración
* De prueba

Hola siguiente diagrama muestra los principales subsistemas de Hola de Service Fabric.

![Diagrama de la arquitectura de Service Fabric](media/service-fabric-architecture/service-fabric-architecture.png)

En un sistema distribuido, Hola capacidad toosecurely comunicarse entre los nodos de un clúster es fundamental. En hello base de pila de hello es subsistema de transporte de hello, que proporciona una comunicación segura entre los nodos. Por encima de transporte de hello subsistema encuentra subsistema de federación de hello, cuáles clústeres Hola nodos diferentes en una única entidad (denominada clústeres) para que pueda detectar errores, realizar elecciones de relleno y proporcionar enrutamiento coherente Service Fabric. subsistema de confiabilidad de Hello, superpuesta subsistema de federación de hello, es responsable de la confiabilidad de hello de servicios de Service Fabric a través de mecanismos como la replicación y administración de recursos, conmutación por error. subsistema de federación de Hello también subyace a subsistema alojamiento y activación de hello, que administra el ciclo de vida de Hola de una aplicación en un único nodo. subsistema de administración de Hello administra Hola del ciclo de vida de aplicaciones y servicios. subsistema de capacidad de prueba de Hello ayuda a los desarrolladores de aplicaciones a probar sus servicios a través de errores simulados antes y después de implementar entornos tooproduction aplicaciones y servicios. Service Fabric proporciona capacidad de hello tooresolve ubicaciones de servicio a través de su subsistema de comunicaciones. Hola modelos de programación de la aplicación toodevelopers expuestos se superpone a estos subsistemas junto con herramientas de tooenable de modelo de aplicación Hola.

## <a name="transport-subsystem"></a>Subsistema de transporte
subsistema de transporte de Hello implementa un canal de comunicación de datagramas punto a punto. Este canal se usa para la comunicación dentro de los clústeres de tejido de servicio y la comunicación entre clientes y el clúster de hello service fabric. Admite unidireccional y patrones de comunicación de solicitud y respuesta, que proporciona la base de hello para la implementación de difusión y multidifusión en Hola capa de federación. subsistema de transporte de Hello protege la comunicación mediante X509 certificados o la seguridad de Windows. Este subsistema utilizado internamente por Service Fabric y no es accesible directamente toodevelopers de programación de aplicaciones.

## <a name="federation-subsystem"></a>Subsistema de federación
En orden tooreason sobre un conjunto de nodos en un sistema distribuido, debe toohave una vista coherente de sistema de Hola. subsistema de federación de Hello usa a las primitivas de comunicación de hello proporcionadas por el subsistema de transporte de Hola y las pega Hola varios nodos en un clúster único y unificado que puede analizar. Proporciona primitivas de sistemas distribuido de hello necesitan por Hola otros subsistemas: detección de errores, la elección de relleno y el enrutamiento coherente. subsistema de federación de Hola se basa en las tablas hash distribuida con un espacio de símbolo (token) de 128 bits. subsistema de Hello crea una topología en anillo en nodos de hello, donde cada nodo en anillo de hello está asignando un subconjunto del espacio de símbolo (token) de hello para la propiedad. Para la detección de errores, capa de hello usa un mecanismo de concesiones en función de latido del corazón y arbitraje. subsistema de federación de Hello también garantiza a través de una combinación compleja y protocolos de salida que solo un único propietario de un símbolo (token) existe en cualquier momento. Esto nos permite elegir al líder y ofrece garantías de enrutamiento coherentes.

## <a name="reliability-subsystem"></a>Subsistema de confiabilidad
Hello subsistema de confiabilidad proporciona el Hola mecanismo toomake Hola estado de un servicio de Service Fabric alta disponibilidad mediante el uso de Hola de hello *replicador*, *el Administrador de conmutación por error*, y  *Equilibrador de recursos*.

* Hola replicador garantiza que los cambios de estado de réplica de servicio principal de hello automáticamente estará toosecondary replicada réplicas, mantener la coherencia entre las réplicas principales y secundarias de hello en un conjunto de réplicas de servicio. Replicador de Hello es responsable de la administración de quórum entre réplicas Hola Hola conjunto. Interactúa con la lista hello tooget de unidad de conmutación por error de Hola de operaciones tooreplicate y agente de reconfiguración de Hola proporciona con la configuración de Hola de conjunto de réplicas de Hola. Dicha configuración indica qué operaciones de hello réplicas deben toobe replicado. Service Fabric proporciona un replicador predeterminado denominado Replicador de tejido, que puede utilizarse por hello programación modelo API toomake Hola estado del servicio altamente disponible y confiable.
* Hola, Administrador de conmutación por error garantiza que, cuando se agregan nodos tooor quitado clúster de hello, Hola carga se redistribuye automáticamente entre los nodos disponibles de Hola. Si se produce un error en un nodo de clúster de hello, clúster de hello automáticamente volverá a configurar la disponibilidad de toomaintain de réplicas del servicio de Hola.
* Hola, Administrador de recursos coloca las réplicas de servicio a través de dominio de error en el clúster de Hola y garantiza que todas las unidades de conmutación por error están operativos. Hola, Administrador de recursos también equilibra los recursos del servicio a través de hello subyacente grupo compartido de distribución de carga uniforme óptimo de tooachieve de nodos de clúster.

## <a name="management-subsystem"></a>Subsistema de administración
subsistema de administración de Hello proporciona service to-end y application lifecycle management. Cmdlets de PowerShell y las API administrativas permiten tooprovision, implementación, revisión, actualización y Desaprovisionamiento de aplicaciones sin pérdida de disponibilidad. subsistema de administración de Hello Esto lleva a cabo a través de hello después servicios.

* **El Administrador de clústeres**: se trata de servicio principal de Hola que interactúa con el Administrador de conmutación por error de hello desde aplicaciones de hello tooplace de confiabilidad en los nodos de hello en función de las restricciones de posición del servicio de Hola. Hola Administrador de recursos en el subsistema de conmutación por error garantiza que las restricciones de hello nunca se interrumpen. el Administrador de clústeres Hola administra Hola del ciclo de vida de las aplicaciones de Hola de aprovisionar el aprovisionamiento toode. Se integra con tooensure de administrador de mantenimiento de Hola que disponibilidad de las aplicaciones no se pierden desde la perspectiva del mantenimiento semántica durante las actualizaciones.
* **Administrador de estado**: este servicio habilita la supervisión del mantenimiento de aplicaciones, servicios y entidades de clúster. Las entidades del clúster (por ejemplo, nodos, las particiones de servicio y las réplicas) pueden notificar información de estado, que, a continuación, se agrega al almacén de estado centralizada Hola. Esta información de estado proporciona una instantánea de mantenimiento general en el momento de servicios de Hola y nodos que se distribuyen en varios nodos de clúster de hello, lo que le tootake las acciones correctivas necesarias. Consulta de estado que API permiten que los eventos de estado de hello tooquery informó de subsistema de mantenimiento de toohello. API de consulta de estado de Hello devolver del almacén de datos de estado sin procesar de hello almacenados en el estado de Hola u Hola agregan, interpreta los datos de estado para una entidad de clúster concreto.
* **Almacén de imágenes**: este servicio proporciona almacenamiento y la distribución de hello archivos binarios de aplicación. Este servicio proporciona un almacén de archivos distribuido simple que las aplicaciones de hello son tooand cargado descargado desde.

## <a name="hosting-subsystem"></a>Subsistema de hospedaje
el Administrador de clústeres de Hello informa Hola hospedaje subsistema (que se ejecuta en cada nodo) y qué servicios necesita toomanage para un nodo determinado. Hola hospedaje subsistema, a continuación, administra Hola del ciclo de vida de la aplicación hello en ese nodo. Interactúa con hello el tooensure de componentes confiabilidad y el estado que las réplicas de Hola estén colocadas correctamente y que están en buen estadas.

## <a name="communication-subsystem"></a>Subsistema de comunicación
Este subsistema proporciona mensajería confiable de detección de clúster y el servicio de Hola a través del servicio de nomenclatura de Hola. Hola Naming service resuelve ubicación tooa nombres del servicio de clúster de Hola y permite propiedades y los nombres de servicio de toomanage de los usuarios. Usar servicio de nomenclatura de hello, los clientes pueden segura comunicarse con cualquier nodo Hola clúster tooresolve un nombre de servicio y recuperar metadatos del servicio. Mediante una API de cliente de escribir el nombre simple, los usuarios de Service Fabric pueden desarrollar servicios y clientes capaces de resolver la ubicación de red actual de Hola a pesar de dinamismo de nodo u Hola volver a ajustar el tamaño de clúster de Hola.

## <a name="testability-subsystem"></a>Subsistema de capacidad de prueba
La capacidad de prueba es un conjunto de herramientas diseñadas de manera específica para probar los servicios de pruebas basados en Service Fabric. Hello herramientas permiten al desarrollador fácilmente inducir a errores significativos y ejecutar tooexercise de escenarios de prueba y validar Hola numerosos Estados y transiciones que experimentará un servicio a lo largo de su duración, en forma segura y controlada. Capacidad de prueba también proporciona un mecanismo toorun pruebas más largas que pueden iterar a través de varios posibles errores sin perder la disponibilidad. Esto le ofrece un entorno de producción en pruebas.

