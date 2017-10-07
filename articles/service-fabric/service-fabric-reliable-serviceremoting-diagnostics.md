---
title: "aaaAzure ServiceFabric diagnósticos y supervisión | Documentos de Microsoft"
description: "Este artículo describen características de supervisión de rendimiento de hello en hello ServiceRemoting confiable de tejido de servicio en tiempo de ejecución, como los contadores de rendimiento emite."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Supervisión de diagnósticos y rendimiento de Reliable ServiceRemoting
tiempo de ejecución de Hello ServiceRemoting confiable emite [contadores de rendimiento](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Estos proporcionan información sobre cómo funciona hello ServiceRemoting y ayudarán con la solución de problemas y supervisión de rendimiento.


## <a name="performance-counters"></a>Contadores de rendimiento
en tiempo de ejecución de Hello ServiceRemoting confiable define Hola siguientes categorías de contador de rendimiento:

| Categoría | Descripción |
| --- | --- |
| Servicio de Service Fabric |Contadores específico tooAzure comunicación remota de servicio de Fabric de servicio, por ejemplo, solicitar tiempo promedio necesario tooprocess |
| Método del servicio Service Fabric |Contadores específicos toomethods implementada por servicio Fabric Remoting Service, por ejemplo, la frecuencia con la que se invoca un método de servicio |

Cada uno de hello anteriores categorías tiene uno o varios contadores.

Hola [Monitor de rendimiento de Windows](https://technet.microsoft.com/library/cc749249.aspx) aplicación que está disponible de forma predeterminada en el sistema operativo de Windows hello puede ser usados datos del contador de rendimiento toocollect y vista. [Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) es otra opción para recopilar los datos del contador de rendimiento y cargarlos tooAzure tablas.

### <a name="performance-counter-instance-names"></a>Nombres de instancias de contador de rendimiento
Un clúster con un gran número de servicios o particiones de ServiceRemoting tendrá una gran cantidad de instancias de contador de rendimiento. instancia de contador de rendimiento de Hello nombres pueden ayudar a identificar la partición específica de Hola y el método de servicio (si procede) que está asociada esa instancia de contador de rendimiento de Hola.

#### <a name="service-fabric-service-category"></a>Categoría del servicio de Service Fabric
De categoría de hello `Service Fabric Service`, son nombres de instancia de contador de Hola Hola siguiendo el formato:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* es Hola representación de cadena de hello está asociado con Id. de partición de Service Fabric que Hola instancia del contador de rendimiento. Id. de partición de Hello es un GUID y su representación de cadena se genera a través de hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método con el especificador de formato "D".

*ServiceReplicaOrInstanceId* es Hola representación de cadena de hello Id. de réplica/instancia de servicio de tejido que Hola instancia del contador de rendimiento está asociado.

*ServiceRuntimeInternalID* es Hola representación de cadena de un entero de 64 bits que se genera en tiempo de ejecución del servicio de Fabric de Hola para su uso interno. Esto se incluye en la instancia de contador de rendimiento de hello, asigne un nombre tooensure su unicidad y evitar el conflicto con otros nombres de instancia de contador de rendimiento. Los usuarios no deben intentar toointerpret esta parte del nombre de instancia de contador de rendimiento de Hola.

Hello aquí te mostramos un ejemplo de un nombre de instancia de contador de un contador que pertenece toohello `Service Fabric Service` categoría:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Hola anterior ejemplo, `2740af29-78aa-44bc-a20b-7e60fb783264` es Hola representación de cadena de Id. de partición de Service Fabric de hello, `635650083799324046` es la representación de cadena de réplica/InstanceId y `5008379932` es Id. de 64 bits de hello generada para hello en tiempo de ejecución interno Use.

#### <a name="service-fabric-service-method-category"></a>Categoría del método del servicio Service Fabric
De categoría de hello `Service Fabric Service Method`, son nombres de instancia de contador de Hola Hola siguiendo el formato:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* es Hola nombre del método de servicio de hello que Hola instancia del contador de rendimiento asociado. formato de Hello del nombre de método de Hola se determina en función de alguna lógica en tiempo de ejecución de servicio de Fabric de Hola que equilibre la legibilidad de hello del nombre de hello con restricciones en la longitud máxima de Hola de nombres de instancia de contador de rendimiento de hello en Windows.

*ServiceRuntimeMethodId* es Hola representación de cadena de un entero de 32 bits que se genera en tiempo de ejecución del servicio de Fabric de Hola para su uso interno. Esto se incluye en la instancia de contador de rendimiento de hello, asigne un nombre tooensure su unicidad y evitar el conflicto con otros nombres de instancia de contador de rendimiento. Los usuarios no deben intentar toointerpret esta parte del nombre de instancia de contador de rendimiento de Hola.

*ServiceFabricPartitionID* es Hola representación de cadena de hello está asociado con Id. de partición de Service Fabric que Hola instancia del contador de rendimiento. Id. de partición de Hello es un GUID y su representación de cadena se genera a través de hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método con el especificador de formato "D".

*ServiceReplicaOrInstanceId* es Hola representación de cadena de hello Id. de réplica/instancia de servicio de tejido que Hola instancia del contador de rendimiento está asociado.

*ServiceRuntimeInternalID* es Hola representación de cadena de un entero de 64 bits que se genera en tiempo de ejecución del servicio de Fabric de Hola para su uso interno. Esto se incluye en la instancia de contador de rendimiento de hello, asigne un nombre tooensure su unicidad y evitar el conflicto con otros nombres de instancia de contador de rendimiento. Los usuarios no deben intentar toointerpret esta parte del nombre de instancia de contador de rendimiento de Hola.

Hello aquí te mostramos un ejemplo de un nombre de instancia de contador de un contador que pertenece toohello `Service Fabric Service Method` categoría:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Hola anterior ejemplo, `ivoicemailboxservice.leavemessageasync` es el nombre del método hello, `2` es hello usa el Id. de 32 bits generado para interno en tiempo de ejecución de hello, `89383d32-e57e-4a9b-a6ad-57c6792aa521` es Hola representación de cadena de Id. de partición de Service Fabric de hello,`635650083804480486` es cadena Hola representación en forma de hello Id. de réplica/instancia de tejido de servicio y `5008380` es utilizar el Id. de 64 bits de hello generado para hello en tiempo de ejecución interno.

## <a name="list-of-performance-counters"></a>Lista de contadores de rendimiento
### <a name="service-method-performance-counters"></a>Contadores de rendimiento del método de servicio

en tiempo de ejecución de un servicio confiable de Hello publica Hola después de la ejecución de toohello relacionados de contadores de rendimiento de métodos de servicio.

| Nombre de la categoría | Nombre del contador | Descripción |
| --- | --- | --- |
| Método del servicio Service Fabric |Invocaciones/seg. |Número de veces que se invoca el método de servicio de Hola por segundo |
| Método del servicio Service Fabric |Promedio de milisegundos por invocación |Tiempo que tarda el método de servicio de tooexecute hello en milisegundos |
| Método del servicio Service Fabric |Excepciones generadas/seg. |Número de veces que el método de servicio de Hola produjo una excepción por segundo |

### <a name="service-request-processing-performance-counters"></a>Contadores de rendimiento del procesamiento de solicitudes de servicio
Cuando un cliente invoca un método a través de un objeto de proxy de servicio, se produce un mensaje de solicitud que se envían a través del servicio de acceso remoto de hello red toohello. servicio de Hello procesa el mensaje de solicitud de saludo y envía a un cliente de toohello de espera de respuesta. en tiempo de ejecución de Hello ServiceRemoting confiable publica Hola después de procesamiento de solicitudes de tooservice relacionados de contadores de rendimiento.

| Nombre de la categoría | Nombre del contador | Descripción |
| --- | --- | --- |
| Servicio de Service Fabric |Número de solicitudes pendientes |Número de solicitudes que se procesan en el servicio de Hola |
| Servicio de Service Fabric |Promedio de milisegundos por solicitud |Tiempo que demora (en milisegundos) Hola servicio tooprocess una solicitud |
| Servicio de Service Fabric |Promedio de milisegundos para la deserialización de una solicitud |Mensaje de solicitud de servicio de tiempo toodeserialize tomada (en milisegundos) cuando se recibe en el servicio de Hola |
| Servicio de Service Fabric |Promedio de milisegundos para la deserialización de una respuesta |Mensaje de respuesta de tiempo tooserialize tomada (en milisegundos) Hola servicio a servicio de hello antes de enviar respuesta hello toohello cliente |

## <a name="next-steps"></a>Pasos siguientes
* [Código de ejemplo](https://github.com/Azure/servicefabric-samples)
* [Proveedores de EventSource en PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
