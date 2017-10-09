---
title: "aaaCapacity planificación de aplicaciones de Service Fabric | Documentos de Microsoft"
description: "Describe cómo tooidentify Hola número de nodos de proceso necesarios para una aplicación de Service Fabric"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Planeación de la capacidad para las aplicaciones de Service Fabric
Este documento enseña cómo tooestimate Hola cantidad de recursos (CPU, RAM, almacenamiento en disco), debe toorun de las aplicaciones de Azure Service Fabric. Es habitual que los toochange de requisitos de recursos con el tiempo. Normalmente necesitará menos recursos mientras desarrolla o prueba su servicio y luego una cantidad mayor cuando pase a producción y su aplicación se vuelva cada vez más popular. Al diseñar la aplicación, barajar requisitos a largo plazo de Hola y tomar decisiones que permiten la demanda de los clientes alta de servicio tooscale toomeet.

 Cuando se crea un clúster de Service Fabric, decide qué tipos de máquinas virtuales (VM) forman el clúster de Hola. Cada máquina virtual incluye una cantidad limitada de recursos en forma de Hola de CPU (núcleos y velocidad), el ancho de banda de red, RAM y almacenamiento en disco. A medida que aumenta su servicio con el tiempo, puede actualizar tooVMs que ofrecen la mayor cantidad de recursos o agregar más máquinas virtuales tooyour clúster. Hola toodo este último debe diseñar su servicio inicialmente por lo que puede beneficiarse de nuevas máquinas virtuales que se agregan dinámicamente toohello clúster.

Algunos servicios administran pocos datos toono en hello las propias máquinas virtuales. Por lo tanto, capacidad para estos servicios deben centrarse principalmente en el rendimiento, lo que significa seleccionar Hola adecuados CPU (núcleos y velocidad) de máquinas virtuales de Hola. Además, debe tener en cuenta el ancho de banda de red y, incluso con qué frecuencia se producen transferencias de red y la cantidad de datos que se transfieren. Si el servicio necesita tooperform así como también aumenta el uso del servicio, puede agregar más máquinas virtuales toohello clúster y equilibrar las solicitudes de red de Hola la carga entre todas las máquinas virtuales de Hola.

Para los servicios que administran grandes cantidades de datos en las máquinas virtuales de hello, planificación de capacidad debe centrarse principalmente en tamaño. Por lo tanto, debe considerar detenidamente capacidad de hello de la máquina virtual de hello RAM y almacenamiento en disco. sistema de administración de memoria virtual Hola de Windows hace espacio en disco RAM tooapplication código el aspecto. Además, el tiempo de ejecución de hello Service Fabric proporciona la paginación inteligente conservando los datos activos sólo en memoria y toodisk de los datos inactivos de hello móvil. Las aplicaciones, por tanto, pueden usar más memoria que está físicamente disponible en hello máquina virtual. Basta con tener más memoria RAM mejora el rendimiento, ya que Hola VM puede mantener más almacenamiento en disco en la memoria RAM. Hola VM que seleccione debe tiene un disco toostore lo suficientemente grande como Hola de datos que desee en hello VM. De forma similar, Hola VM debe tener suficiente tooprovide de RAM a Hola de rendimiento que desee. Si los datos de su servicio aumentan con el tiempo, puede agregar más máquinas virtuales toohello clúster y crear particiones Hola datos a través de todas las máquinas virtuales de Hola.

## <a name="determine-how-many-nodes-you-need"></a>Determinación del número de nodos que necesita
El servicio de creación de particiones permite tooscale los datos de su servicio. Para más información sobre las particiones, consulte [Creación de particiones de Service Fabric](service-fabric-concepts-partitioning.md). Cada partición debe ajustarse a una sola máquina virtual, pero se pueden colocar varias particiones (pequeñas) en una sola máquina virtual. Por lo tanto, tener más particiones pequeñas le proporciona mayor flexibilidad que tener pocas particiones más grandes. ventajas y desventajas de Hello son que tener una gran cantidad de particiones aumenta la carga de trabajo de Service Fabric y no se puede realizar operaciones de transacción entre las particiones. También es más tráfico de red posibles si el código de servicio con frecuencia necesita tooaccess elementos de datos que residen en diferentes particiones. Al diseñar su servicio, debe considerar detenidamente estas tooarrive ventajas y desventajas en una estrategia de partición eficaz.

Supongamos que la aplicación tiene un único servicio con estado que tiene un tamaño de almacén que esperar toogrow tooDB_Size GB en un año. Está dispuesto tooadd más aplicaciones (y particiones) que experimenta un crecimiento más allá de ese año.  Hola factor de replicación (RF), que determina el número de Hola de réplicas para el impacto en el servicio Hola DB_Size total. Hola que db_size total en todas las réplicas es hello multiplicado por DB_Size de Factor de replicación.  Node_Size representa el espacio de disco de Hola/memoria RAM por nodo necesite toouse para el servicio. Para obtener el mejor rendimiento, hello DB_Size debe caber en la memoria en clúster de Hola y un Node_Size que hay alrededor de hello RAM de hello que debe elegirse la máquina virtual. Asignando un Node_Size que es mayor que la capacidad de RAM hello, depende de la paginación de hello proporcionada por el tiempo de ejecución de hello Service Fabric. Por lo tanto, el rendimiento puede no ser óptimo si los datos completos se consideran que toobe activa (desde Hola, a continuación, los datos se paginan los in/out). Sin embargo, para muchos servicios donde está activa solo una parte de datos de hello, es más rentable.

número de Hola de nodos necesarios para obtener el máximo rendimiento se puede calcular como sigue:

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Consideración sobre el crecimiento
Puede que desee toocompute Hola número de nodos según hello DB_Size que esperan su toogrow de servicio, además toohello DB_Size con el que empezó. A continuación, aumentar número Hola de nodos a medida que el servicio aumenta para que se sobreaprovisionar número Hola de nodos no. Pero el número de Hola de particiones debe basarse en el número de Hola de nodos que son necesarios cuando se está ejecutando el servicio en crecimiento máximo.

Es buena toohave algunas máquinas adicionales disponibles en cualquier momento para que pueda controlar los picos inesperados o no (por ejemplo, si algunas máquinas virtuales dejan de funcionar).  Aunque Hola capacidad adicional debe determinarse mediante el uso de los picos esperados, un punto de partida es tooreserve algunas máquinas virtuales adicionales (5-10 por ciento adicional).

Hola anterior se da por supuesto un único servicio con estado. Si tiene más de un servicio con estado, tendrá tooadd hello DB_Size asociada Hola otros servicios en la ecuación de Hola. Como alternativa, puede calcular el número de Hola de nodos por separado para cada servicio con estado.  El servicio puede tener réplicas o particiones que no están equilibradas. Tenga en cuenta que hay particiones que pueden tener más datos que otras. Para más información sobre la creación de particiones, consulte el [artículo sobre la creación de particiones en los procedimientos recomendados](service-fabric-concepts-partitioning.md). Sin embargo, hello ecuación anterior es partición y réplica independiente, porque Service Fabric garantiza que las réplicas de Hola se reparten entre los nodos de Hola de forma optimizada.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Uso de una hoja de cálculo para calcular costos
Ahora vamos a poner algunos números reales en la fórmula de saludo. Un [hoja de cálculo de ejemplo](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) muestra cómo tooplan Hola capacidad para una aplicación que contenga tres tipos de objetos de datos. Para cada objeto, se aproximación su tamaño y número de objetos, esperamos toohave. También hemos seleccionado el número de réplicas que queremos de cada tipo de objeto. hoja de cálculo de Hello calcula la cantidad total de Hola de toobe de memoria que se almacena en el clúster de Hola.

A continuación, escribimos un tamaño de máquina virtual y un costo mensual. En función de hello tamaño de máquina virtual, hoja de cálculo de hello indica que Hola número mínimo de particiones que debe usar toosplit su toophysically datos caben en nodos de Hola. Desea un mayor número de tooaccommodate particiones que necesidades del tráfico de red y de cálculo de específicos de su aplicación. hoja de cálculo de Hello muestra hello número de particiones que administran objetos de perfil de usuario de hello también ha aumentado de una toosix.

Ahora, en función de toda esta información, hoja de cálculo de hello muestra que físicamente se pudieron obtener todos los datos de hello con hello deseado particiones y réplicas en un clúster de nodo de 26. Sin embargo, este clúster podría ser densamente empaquetada, por lo que puede algunas actualizaciones y los errores de nodo tooaccommodate nodos adicionales. hoja de cálculo de Hello también muestra que tiene más de 57 nodos no proporciona ningún valor adicional ya que tendría nodos vacíos. De nuevo, puede que desee toogo anteriormente 57 nodos todas formas las actualizaciones y los errores de nodo tooaccommodate. Puede retocar toomatch de hoja de cálculo de hello las necesidades específicas de su aplicación.   

![Hoja de cálculo para calcular costos][Image1]

## <a name="next-steps"></a>Pasos siguientes
Extraer del repositorio [servicios de creación de particiones Service Fabric] [ 10] toolearn más información sobre el servicio de creación de particiones.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
