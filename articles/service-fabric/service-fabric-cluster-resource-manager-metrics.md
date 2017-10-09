---
title: "carga de Azure microservicio aaaManage con métricas | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las métricas de tooconfigure y el uso de Service Fabric toomanage el consumo de recursos del servicio."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Administración de consumo y carga de recursos en Service Fabric con métricas
*Las métricas* son recursos de Hola que su ocuparse de servicios y que se proporcionan con nodos de hello en clúster de Hola. Una métrica es todo lo que desea que toomanage en rendimiento de Hola de orden tooimprove o el monitor de los servicios. Por ejemplo, podría observar tooknow de consumo de memoria si el servicio está sobrecargado. Otro uso es toofigure out podría mover servicio hello en otro lugar que la memoria es que menos restringida a un mejor rendimiento de orden tooget.

Las métricas son, por ejemplo, memoria, disco y uso de CPU. Estas métricas son métricas físicas, recursos que corresponden toophysical recursos en el nodo de Hola que necesitan toobe administrado. Las métricas también pueden ser (y normalmente son) métricas lógicas. Las métricas lógicas son, por ejemplo, "MyWorkQueueDepth", "MessagesToProcess" o "TotalRecords". Métricas lógicas son definidos por la aplicación e indirectamente corresponden toosome el consumo de recursos físicos. Las métricas lógicas son comunes porque puede ser toomeasure de disco duro y de informes la utilización de recursos físicos por servicio. complejidad de Hola de valorar e informar sobre sus propias métricas físicos también es ¿por qué Service Fabric proporciona algunas métricas de forma predeterminada.

## <a name="default-metrics"></a>Métricas predeterminadas
Supongamos que desea tooget iniciado escribir e implementar su servicio. En este momento no sabe qué recursos físicos o lógicos consume. ¡Eso está bien! Hola, Administrador de recursos de clúster de tejido de servicio utiliza algunas métricas de forma predeterminada cuando no se especifican ningún otras métricas. Son las siguientes:

  - PrimaryCount - recuento de las réplicas principales en el nodo de Hola 
  - ReplicaCount - número de réplicas con estado total en el nodo de Hola
  - Recuento: recuento de todos los objetos de servicio (con y sin estado) en el nodo de Hola

| Métrica | Carga de instancia sin estado | Carga secundaria con estado | Carga principal con estado |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Recuento |1 |1 |1 |

Para las cargas de trabajo básicos, Hola predeterminado que proporcionan una distribución decente de trabajo en clúster de Hola. En el siguiente ejemplo de Hola, veamos qué sucede cuando se crea dos servicios y se basan en las métricas de predeterminado de hello para el equilibrio. Hola primer servicio es un servicio con estado con tres particiones y una réplica de destino establece tamaño de tres. segundo servicio de Hello es un servicio sin estado con una partición y un recuento de instancias de tres.

Esto es lo que obtiene:

<center>
![Diseño de clúster con métricas predeterminadas][Image1]
</center>

Algunos toonote cosas:
  - Las réplicas principales de servicio con estado Hola se distribuyen entre varios nodos
  - Réplicas de la misma partición que se encuentran en distintos nodos de Hola
  - número total de Hola de entidades principales y secundarias se distribuye en clúster de Hola
  - número total de Hola de objetos de servicio se asigna uniformemente en cada nodo

¡Bien!

las métricas de Hello predeterminada funcionan correctamente como un tutorial de inicio. Sin embargo, las métricas de hello predeterminada sólo transmitirá se hasta ahora. Por ejemplo: ¿qué es la probabilidad de Hola Hola particiones esquema que se ha seleccionado resultados perfectamente incluso uso de todas las particiones? ¿Qué es la posibilidad de Hola que Hola carga para un servicio determinado es constante con el tiempo, o incluso simplemente Hola igual en varias particiones ahora?

Puede ejecutar con solo las métricas de Hola de forma predeterminada. De todas forma, si lo hace, normalmente significa que la utilización del clúster será inferior y más desigual de lo deseable. Esto es porque las métricas de Hola predeterminado no están adaptables y suponen que todo lo que es equivalente. Por ejemplo, un elemento principal que está ocupado y otra que no es both contribuyen "1" toohello PrimaryCount métrica. En hello peor de los casos, también puede producir usar solo las métricas de hello predeterminado en nodos overscheduled lo que da lugar a problemas de rendimiento. Si está interesado en obtener Hola mayoría fuera de su clúster y evitar problemas de rendimiento, debe toouse de métricas personalizadas y los informes de carga dinámica.

## <a name="custom-metrics"></a>Métricas personalizadas
Las métricas se configuran en por-denominado-service-instancia al crear el servicio de Hola.

Todas las métricas tienen algunas propiedades que las describen: un nombre, un peso y una carga predeterminada.

* : Métrica Hola nombre de métrica de Hola. nombre de la métrica Hello es un identificador único para la métrica de hello en clúster de Hola desde la perspectiva del Administrador de recursos de Hola.
* Peso: Peso métrico define la importancia relativa toohello esta medida es otras métricas para este servicio.
* Carga de forma predeterminada: carga de forma predeterminada de hello representado de forma diferente dependiendo de si el servicio de hello es con o sin estado.
  * Para los servicios sin estado, cada métrica tiene una propiedad única llamada DefaultLoad.
  * Para servicios con estado, se define lo siguiente:
    * PrimaryDefaultLoad: cantidad Hola predeterminada de esta métrica que este servicio se utiliza cuando es un elemento principal
    * SecondaryDefaultLoad: cantidad Hola predeterminada de esta métrica que este servicio se utiliza cuando es un elemento secundario

> [!NOTE]
> Si definir métricas personalizadas y desea que las métricas de too_also_ uso Hola predeterminado, deberá too_explicitly_ agregar métricas predeterminadas de hello hacer copia y definen pesos y los valores para ellos. Esto es porque debe definir relación Hola entre las métricas de forma predeterminada de Hola y de la métrica personalizada. Por ejemplo, puede que le preocupen más las métricas ConnectionCount o WorkQueueDepth que las de distribución principal. Peso de saludo predeterminado de hello PrimaryCount métrica es alta, por lo que desee tooreduce se tooMedium al agregar los otro tooensure métricas tienen prioridad.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Definición de las métricas del servicio: ejemplo
Supongamos que desea Hola siguiente configuración:

  - El servicio notifica una métrica denominada "ConnectionCount"
  - También puede métricas de toouse Hola predeterminadas 
  - Ha realizado algunas mediciones y sabe que, normalmente, una réplica principal de ese servicio ocupa hasta 20 unidades de "ConnectionCount"
  - Por su parte las secundarias usan 5 unidades de "ConnectionCount"
  - Sepa que "Recuento de conexión" es la métrica más importante de hello en cuanto a la administración del rendimiento de Hola de este servicio en particular
  - Pero también desea que las réplicas principales estén equilibradas. Mantener el equilibrio de las réplicas principales suele ser siempre una buena idea. Esto ayuda a evitar la pérdida de Hola de algún nodo o error de dominio no afecten a la mayoría de las réplicas principales junto con ella. 
  - De lo contrario, son válidas las métricas de saludo predeterminado

Aquí es que habría que escribir toocreate un servicio con el que la configuración de métrica de código de hello:

Código:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> Hola por encima de los ejemplos y hello resto de este documento se describen las métricas de administración de forma por con el nombre de servicio. También es posible toodefine métricas para los servicios en el servicio de hello _tipo_ nivel. Esto se consigue especificándolos en los manifiestos de servicio. No se recomienda definir las métricas de nivel de tipo por varias razones. primer motivo de Hola es que los nombres de métrica son con frecuencia específica del entorno. A menos que haya un contrato firme en su lugar, no puede ser seguro que esa métrica Hola "Núcleos" en un entorno no es "MiliCores" o "Núcleos" en otros. Si las métricas se definen en el manifiesto debe toocreate nuevos manifiestos por cada entorno. Normalmente, esto lleva tooa proliferación de manifiestos diferentes con sólo pequeñas diferencias, lo que pueden provocar problemas de toomanagement.  
>
> Las cargas de métricas normalmente se asignan en base a cada instancia de servicio denominado. Por ejemplo, supongamos que se crea una instancia de hello atenderla para clientea que planes toouse apenas. Supongamos también que crea otra instancia para el ClienteB que tiene una mayor carga de trabajo. En este caso, seguramente desearía incluir predeterminado de hello tootweak carga para esos servicios. Si dispone de las métricas y cargas definidas a través de los manifiestos y desea toosupport este escenario, requiere diferentes aplicaciones y tipos de servicio para cada cliente. valores de Hello definidos en el momento de creación de servicio reemplazan a las definidas en el manifiesto de hello, por lo que podría utilizar esa tooset Hola determinados valores predeterminados. Sin embargo, haciendo produce valores de hello declarados en coincidencia de hello manifiestos toonot con que esos Hola realmente se ejecuta. Esto puede provocar tooconfusion. 
>

Como recordatorio: si desea que las métricas de toouse Hola de forma predeterminada, no necesita la colección de métricas de hello tootouch en absoluto o hacer nada especial al crear el servicio. métricas de Hello predeterminadas hacía automáticamente cuando no hay otras se definen. 

Ahora, vamos a analizar cada uno de estos valores con más detalle y hablar acerca del comportamiento de Hola que influye en.

## <a name="load"></a>Carga
Hola todo punto de definición de métricas es toorepresent cierta carga. *Carga* es la cantidad de una determinada métrica que alguna instancia del servicio o réplica consume en un nodo específico. El valor Carga puede configurarse prácticamente en cualquier momento. Por ejemplo:

  - Carga se puede definir cuando se crea un servicio. Esto se denomina _carga predeterminada_.
  - carga información de métrica de Hello, incluido de forma predeterminada, para un servicio puede actualizar después de crear el servicio de Hola. Esto se denomina _actualizar un servicio_. 
  - Hola cargas para una partición determinada pueden ser valores de predeterminado toohello de restablecimiento para ese servicio. Esto se llama _restablecer la carga de partición_.
  - La carga se puede notificar en base a cada objeto de servicio de forma dinámica durante el tiempo de ejecución. Esto se denomina _notificar la carga_. 
  
Todas estas estrategias pueden usarse en hello mismo servicios a través de su duración. 

## <a name="default-load"></a>Carga predeterminada
*Carga predeterminada* es la cantidad de métrica de hello consume cada objeto de servicio (instancia sin estado o réplica con estado) de este servicio. Hola, Administrador de recursos del clúster utiliza este número para la carga de Hola Hola de objeto de servicio hasta que recibe otra información, como un informe dinámico de carga. Para los servicios más sencillos, carga predeterminada de hello es una definición estática. carga de forma predeterminada de Hello nunca se actualiza y se utiliza para vida Hola Hola. Valor predeterminado carga funciona bien para planear escenarios donde determinadas cantidades de recursos son cargas de trabajo de toodifferent dedicado y no cambian la capacidad simple.

> [!NOTE]
> Para obtener más información sobre la administración de capacidad y definir las capacidades para nodos de hello en el clúster, vea [este artículo](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Hola, Administrador de recursos de clúster permite toospecify de servicios con estado una carga predeterminados diferentes para sus entidades principales y secundarias. Servicios sin estado solo pueden especificar un valor que se aplica a instancias de tooall. Para los servicios con estado, carga de hello predeterminado para las réplicas principal y secundaria son normalmente diferentes dado que las réplicas realizar diferentes tipos de trabajo en cada rol. Por ejemplo, los elementos normalmente servir lecturas y escrituras y satisfacer la mayoría de carga de cálculo de hello, pero no elementos secundarios. Carga de hello predeterminado para una réplica principal suele ser mayor que la carga de hello predeterminado para las réplicas secundarias. números reales de Hello debe depender de sus propias medidas.

## <a name="dynamic-load"></a>Carga dinámica
Supongamos que lleva un tiempo ejecutando el servicio. Con cierta supervisión, habrá observado lo siguiente:

1. Algunas particiones o instancias de un servicio determinado consumen más recursos que otras.
2. Algunos servicios tienen cargas que varían con el tiempo.

Hay una gran cantidad de cosas que podrían causar estos tipos de fluctuaciones de la carga. Por ejemplo, diferentes servicios o particiones están asociadas con diferentes clientes con requisitos diferentes. También podría cambiar la carga porque cantidad de hello del servicio de trabajo Hola varía con el transcurso de Hola de día de Hola. Independientemente del motivo de hello, no suele haber ningún número único que puede usar de forma predeterminada. Esto es especialmente cierto si desea tooget Hola mayoría uso fuera del clúster de Hola. Cualquier valor que se toma para carga de forma predeterminada es incorrecto algunos de tiempo de presentación. Predeterminada incorrecta carga resultados Hola Administrador de recursos de clúster superior o inferior a asignación de recursos. Como resultado, tiene nodos superior o inferior a su capacidad aunque Hola, Administrador de recursos del clúster se considera clúster Hola está equilibrada. Las cargas predeterminadas siguen siendo buenas porque proporcionan cierta información para la ubicación inicial, pero no cuentan la historia completa de las cargas de trabajo reales. captura de tooaccurately cambiantes requerimientos de recursos, Hola, Administrador de recursos del clúster permite a cada tooupdate de objeto de servicio su propia carga en tiempo de ejecución. Esto se llama informes de carga dinámica.

Los informes de dinámico de carga permiten tooadjust réplicas o instancias de su carga de las métricas de asignación/notifica largo de su vida. Normalmente, una instancia o una réplica del servicio que estaba inactiva y sin realizar ningún trabajo informará de que usó poca cantidad de una métrica determinada. Una réplica o instancia ocupadas indicarían que están usando más.

Reporting cargar por instancia o la réplica permite hello tooreorganize del Administrador de recursos del clúster de objetos de servicio individuales de Hola Hola clúster. La reorganización de los servicios de hello le ayuda a asegurarse de que obtienen los recursos de Hola que requieran. Servicios ocupados eficazmente obtener demasiado "reclamar" los recursos de otras réplicas o las instancias que están actualmente frío o menos trabajando.

Dentro de los servicios de confianza, carga de tooreport de código de hello dinámicamente este aspecto:

Código:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Un servicio puede informar sobre cualquiera de las métricas de hello definidas para él en tiempo de creación. Si una carga de informes de servicio para una medida que no está configurado toouse, Service Fabric omite ese informe. Si hay otras métricas notifican en hello igual que son válidos, se aceptan los informes. Código de servicio puede medir e informar todos Hola métricas que sepa cómo, y los operadores pueden especificar toouse de configuración de métrica de hello sin necesidad de código del servicio toochange Hola. 

### <a name="updating-a-services-metric-configuration"></a>Actualización de la configuración de métrica de un servicio
asociada la lista de Hola de métricas con el servicio de Hola y Hola propiedades de esas métricas se pueden actualizar dinámicamente mientras el servicio de hello está activo. Esto permite experimentación y flexibilidad. Algunos ejemplos de cuándo esto resulta útil son:

  - deshabilitación de una métrica con un informe con errores para un servicio determinado
  - volver a configurar pesos Hola de métricas adicionales basadas en el comportamiento deseado
  - Si se habilita una nueva métrica solo código de hello ya se hayan implementado y se ha validado a través de otros mecanismos de
  - cambiar la carga de hello predeterminado para un servicio basado en el consumo y el comportamiento observado

Hello principales API para cambiar la configuración de métrica son `FabricClient.ServiceManagementClient.UpdateServiceAsync` en C# y `Update-ServiceFabricService` en PowerShell. Cualquier información que se especifique con estas API reemplaza información existente de métrica hello para el servicio de hello inmediatamente. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>Combinación de valores de carga predeterminados e informes de carga dinámica
Carga de forma predeterminada y carga dinámica puede utilizarse para hello mismo servicio. Cuando un servicio utiliza los informes tanto de carga predeterminada como de carga dinámica, la carga predeterminada actúa como una estimación hasta que aparecen los informes dinámicos. Carga de forma predeterminada es bueno, porque proporciona Hola, Administrador de recursos del clúster algo toowork con. Hola de carga de predeterminado permite hello tooplace del Administrador de recursos del clúster de objetos de servicio de hello en ubicaciones buena cuando se crean. Si no se proporciona ninguna información de carga predeterminada, la ubicación de los servicios es aleatoria. Cuando llegan los informes de carga más adelante una colocación aleatoria inicial Hola a menudo es incorrecta y Hola, Administrador de recursos del clúster tiene servicios de toomove.

Vamos a tomar nuestro ejemplo anterior y vemos qué sucede cuando se agregan algunas métricas personalizadas e informes de carga dinámicos. En este ejemplo, utilizamos "MemoryInMb" como una métrica de ejemplo.

> [!NOTE]
> Memoria es una de las métricas del sistema Hola que puede Service Fabric [recursos rigen](service-fabric-resource-governance.md), y notificar que suele ser difícil. No realmente esperamos se tooreport consumo de memoria; La memoria se utiliza aquí como un toolearning ayuda acerca de las capacidades de Hola Hola, Administrador de recursos del clúster.
>

Vamos a suponer que se creó inicialmente servicio con estado Hola con hello siguiente comando:

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Como recordatorio, esta sintaxis es ("MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad").

El aspecto de un diseño del clúster podría ser similar a este:

<center>
![Clúster equilibrado con métricas predeterminadas y personalizadas][Image2]
</center>

Algunas cosas que debe tener en cuenta:

* Las réplicas secundarias dentro de una partición pueden tener su propia carga cada una
* En general las métricas de hello buscar equilibradas. Para la memoria, Hola proporción entre Hola máximo y mínimo carga es 1,75 (nodo Hola con hello carga mayoría es N3, hello es menos N2 y 28/16 = 1,75).

Hay algunas cosas que todavía necesitamos tooexplain:

* ¿Qué determinó si una relación de 1,75 era razonable o no? ¿Cómo sabe Hola, Administrador de recursos del clúster si es suficientemente bueno, o si no hay más toodo de trabajo?
* ¿Cuándo se produce el equilibrio?
* ¿Qué significa que la ponderación de Memoria es alta?

## <a name="metric-weights"></a>Pesos de métrica
Seguimiento Hola mismo las métricas entre servicios diferentes son importante. Que la vista global es lo que permite Hola consumo de tootrack de administrador de recursos de clúster en el clúster de hello, equilibrar el consumo en todos los nodos y asegurarse de que los nodos no abuse de capacidad. Sin embargo, los servicios pueden tener vistas diferentes como toohello importancia de hello misma métrica. Además, en un clúster con muchas métricas y una gran cantidad de servicios, puede que no existan soluciones perfectamente equilibradas para todas las métricas. ¿Cómo debe controlar estas situaciones Hola, Administrador de recursos del clúster?

Pesos de métricos permiten hello toodecide de administrador de recursos del clúster cómo toobalance Hola clúster cuando no hay ninguna respuesta perfecta. Pesos métricos también permiten hello toobalance del Administrador de recursos del clúster de servicios específicos diferente. Las métricas pueden tener cuatro niveles diferentes de ponderación: cero, baja, media o alta. Una métrica con un peso de cero no aporta nada a la hora de considerar si todo está equilibrado o no. Sin embargo, su carga aún contribuyen toocapacity administración. Las métricas con un peso cero siguen siendo útiles y se utilizan con frecuencia como parte la supervisión del comportamiento y el rendimiento del servicio. [En este artículo](service-fabric-diagnostics-event-generation-infra.md) proporciona más información sobre el uso de Hola de métricas de supervisión y diagnóstico de los servicios. 

impacto de Hola de diferentes pesos métricos en el clúster de hello es que ese Hola, Administrador de recursos del clúster genera diferentes soluciones. Pesos métricos indican Hola, Administrador de recursos del clúster que ciertas métricas son más importantes que otros usuarios. Cuando no hay ningún Hola solución perfecta Administrador de recursos del clúster puede preferir soluciones que equilibrar Hola superior ponderada las métricas mejor. Si un servicio considera que una métrica no es importante, puede encontrar que su uso de esa métrica está desequilibrado. Esto permite que una distribución uniforme de algunos métrica que es importante tooit tooget de otro servicio.

Echemos un vistazo a un ejemplo de algunos informes de carga y la métrica diferente Pondere los resultados de las diferentes asignaciones de clúster Hola. En este ejemplo, vemos que intercambiar peso relativo de Hola de métricas de hello, hello toocreate del Administrador de recursos del clúster diferentes organizaciones de servicios.

<center>
![Ejemplo de ponderación de métricas y su impacto en soluciones de equilibrio][Image3]
</center>

En este ejemplo, hay cuatro servicios diferentes, todos informando sobre valores diferentes para dos métricas diferentes, MetricA y MetricB. En un caso, todos los servicios de hello definen MetricA es más importante de hello (peso = alta) y MetricB como no importantes (peso = bajos). Como resultado, vemos que Administrador de recursos del clúster de Hola coloca servicios Hola para que MetricA es más equilibrada que MetricB. "Mejor equilibrada" significa que MetricA tiene una desviación estándar menor que MetricB. En segundo caso hello, se invierte la dirección pesos de métrica de Hola. Como resultado, Hola, Administrador de recursos del clúster intercambia servicios A y B toocome seguridad con una asignación donde MetricB mejor es equilibrada que MetricA.

> [!NOTE]
> Pesos métricos determinan cómo debe equilibrar Hola, Administrador de recursos del clúster, pero no cuando equilibrio debería ocurrir. Para más información sobre el equilibrio, consulte [este artículo](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>Ponderaciones de métricas globales
Supongamos que Services como define MetricA como alta de peso y ServiceB establece el peso de Hola para MetricA tooLow o cero. ¿Qué es el peso real Hola que terminan acostumbrarse?

En realidad, para cada métrica se realiza el seguimiento con varios pesos. primer grosor de Hello es hello uno definido para la métrica de hello cuando se crea el servicio de Hola. Hola otro peso es un peso global, que se calcula automáticamente. Hola, Administrador de recursos del clúster utiliza ambos estos pesos cuando realice la puntuación soluciones. Es importante tener ambos pesos en cuenta. Esto permite hello toobalance del Administrador de recursos del clúster de cada servicio tooits correspondiente posee las prioridades y asegúrese también de ese clúster Hola como un todo se asignó correctamente.

¿Qué ocurriría si Hola, Administrador de recursos del clúster no se preocupa de saldo global y local? Bueno, es fácil tooconstruct soluciones que están equilibrados global, pero lo que ocasionará saldo deficiente de los recursos para los servicios individuales. En el siguiente ejemplo de Hola, veamos un servicio configurado con solo las métricas de Hola de forma predeterminada y vea Qué sucede cuando se considera solo global saldo:

<center>
![Hola impacto de una solución solo Global][Image4]
</center>

En hello ejemplo superior basándose sólo en equilibrio global, realmente está equilibrada clúster Hola como un todo. Todos los nodos tienen Hola mismo recuento de los elementos y Hola mismo número de réplicas totales. Sin embargo, si observa impacto real de Hola de esta asignación no es tan buena: pérdida de Hola de cualquier nodo afecta a una carga de trabajo determinada desproporcionadamente, porque toma todos sus elementos. Por ejemplo, si se produce un error en primer nodo de hello tres primarios Hola para las diferentes particiones de tres de Hola de hello servicio círculo todos no se pierde. Por el contrario, el Hola triángulo y servicios de hexágonos tienen sus particiones pierde una réplica. Esto no hace que interrupción, que no sea de tener hello toorecover hacia abajo de la réplica.

En el ejemplo de la parte inferior de hello, Hola, Administrador de recursos del clúster distribuyó réplicas Hola basándose en ambos equilibrio hello, globales y por servicio. Al calcular la puntuación de Hola de solución de hello ofrece la mayoría de solución global de hello peso toohello y un servicio de tooindividual parte (configurable). Equilibrar global para una métrica se calcula según promedio de Hola de pesos de métrica de Hola de cada servicio. Cada servicio se equilibra tooits de pesos métrica definida propio correspondiente. Esto garantiza que los servicios de Hola están equilibrados entre ellas según tootheir propias necesidades. Como resultado, si hello mismo primer nodo tiene un error error Hola se distribuye entre todas las particiones de todos los servicios. Hola impacto tooeach es Hola igual.

## <a name="next-steps"></a>Pasos siguientes
- Para más información acerca de cómo configurar servicios, [lea sobre la configuración de servicios](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Definir métricas de desfragmentación es tooconsolidate una manera de carga en los nodos en lugar de propagarse. toolearn cómo tooconfigure la desfragmentación, consulte demasiado[este artículo](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind out acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, desproteger artículo hello en [equilibrio de carga](service-fabric-cluster-resource-manager-balancing.md)
- Desde el principio de Hola y [obtener un servicio Administrador de recursos del clúster de tejido de toohello de introducción](service-fabric-cluster-resource-manager-introduction.md)
- Coste del movimiento es una manera de señalización toohello Administrador de recursos del clúster que determinados servicios estén toomove más cara que otras. toolearn más información acerca del coste del movimiento, consulte demasiado[este artículo](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
