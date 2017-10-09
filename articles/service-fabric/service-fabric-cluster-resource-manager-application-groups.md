---
title: "aaaService Administrador de recursos de clúster de tejido - grupos de aplicaciones | Documentos de Microsoft"
description: "Información general sobre la funcionalidad de grupo de aplicaciones en el servicio Administrador de recursos del clúster de tejido de Hola Hola"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Introducción tooApplication grupos
Administrador de recursos del clúster de Service Fabric normalmente administra los recursos del clúster al repartir la carga de hello (representar mediante [métricas](service-fabric-cluster-resource-manager-metrics.md)) uniformemente a lo largo de clúster de Hola. Service Fabric administra la capacidad de Hola de nodos Hola Hola y Hola clúster como un todo a través de [capacidad](service-fabric-cluster-resource-manager-cluster-description.md). Las métricas y la capacidad funcionan muy bien con muchas cargas de trabajo diferentes, pero patrones que hacen un uso intensivo de diferentes instancias de aplicación de Service Fabric en ocasiones introducen requisitos adicionales. Por ejemplo, puede que desee:

- Reservar cierta capacidad en nodos de hello en clúster de Hola para los servicios de hello en alguna instancia de aplicación con nombre
- Limitar Hola número total de nodos que se ejecutan servicios de hello dentro de una instancia con nombre de aplicación en (en lugar de distribuirlos de forma horizontal en clúster completo hello)
- Definir las capacidades en la propia instancia de aplicación con nombre hello número de Hola de toolimit servicios o total del consumo de recursos de servicios de hello en él

toomeet estos requisitos, Hola, Administrador de recursos de clúster de tejido de servicio admite una característica denominada grupos de aplicaciones.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Limitar el número máximo de Hola de nodos
caso de uso más simple de Hola de capacidad de la aplicación es cuando una instancia de la aplicación necesita toobe limitado tooa cierto número máximo de nodos. Todos los servicios dentro de esa instancia de aplicación se consolidan en un número establecido de máquinas. Consolidación es útil cuando está tratando de toopredict o limitar el uso de los recursos físicos por servicios de hello en esa instancia con nombre de aplicación. 

Hello siguiente imagen muestra una instancia de la aplicación con y sin un número máximo de nodos definidos:

<center>
![Definición del número máximo de nodos para la instancia de aplicación][Image1]
</center>

En el ejemplo de Hola a izquierda, aplicación hello no tiene un número máximo de nodos definidos y tiene tres servicios. Hola, Administrador de recursos del clúster se reparten todas las réplicas a través de seis nodos disponibles tooachieve Hola mejor equilibrio en clúster de hello (comportamiento predeterminado de Hola). En el ejemplo de Hola a derecha, vemos Hola misma aplicación limitada toothree nodos.

parámetro de Hola que controla este comportamiento se denomina MaximumNodes. Este parámetro se puede establecer durante la creación de la aplicación, o actualizarse con una instancia de la aplicación que ya se estaba ejecutando.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

En el conjunto de Hola de nodos, Hola, Administrador de recursos del clúster no garantiza qué objetos de servicio se asignarán juntos o qué nodos se usan.

## <a name="application-metrics-load-and-capacity"></a>Métrica, carga y capacidad de aplicación
Grupos de aplicaciones le permiten métricas de toodefine asociadas a una instancia de aplicación con nombre determinada y la capacidad de la instancia de esa aplicación para esas métricas. Las métricas de aplicación permiten tootrack, reserva y limitar el consumo de recursos de servicios de hello dentro de esa instancia de la aplicación hello.

En cada métrica de la aplicación, hay dos valores que se pueden establecer:

- **Total de capacidad de la aplicación** : esta opción representa la capacidad total de Hola de aplicación hello para una métrica concreta. Hola, Administrador de recursos del clúster no permite la creación de hello de los nuevos servicios en la instancia de aplicación que puede provocar que la carga total tooexceed este valor. Por ejemplo, supongamos que tuviera una capacidad de 10 de instancia de la aplicación hello y ya tenía la carga de cinco. creación de Hello de un servicio con una carga total predeterminado de 10 circunstancias no está permitida.
- **Capacidad máxima de nodo** : esta configuración especifica la carga total máxima de hello para la aplicación hello en un único nodo. Si carga supera esta capacidad, Hola, Administrador de recursos de clúster mueve nodos de tooother de réplicas para que reduzca la hello carga.


Powershell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Reserva de capacidad
Otro uso común para los grupos de aplicaciones es tooensure que recursos dentro de Hola clúster están reservados para una instancia de aplicación determinada. Cuando se crea la instancia de la aplicación hello, se reserva siempre Hola espacio.

La reserva de espacio en el clúster de hello para la aplicación hello ocurre inmediatamente, incluso cuando:
- instancia de la aplicación Hello se ha creado pero aún no tiene ningún servicio dentro de él
- número de Hello de servicios dentro de la instancia de la aplicación hello cambia cada vez 
- Servicios de Hello existen pero no están consumiendo recursos Hola 

Para reservar recursos para una instancia de aplicación, es necesario especificar dos parámetros adicionales: *MinimumNodes* y *NodeReservationCapacity* .

- **MinimumNodes** -define el número mínimo de Hola de nodos que Hola aplicación instancia debe ejecutarse.  
- **NodeReservationCapacity** -esta configuración es por métrica para la aplicación hello. valor de Hello es la cantidad de Hola de esa métrica reservada para la aplicación hello en cualquier nodo en los que se Hola servicios en ejecución de la aplicación.

Combinar **MinimumNodes** y **NodeReservationCapacity** garantiza una reserva de carga mínima para la aplicación hello en clúster de Hola. Si hay menos restantes capacidad en Hola de clúster que reserva total Hola necesaria, se produce un error en la creación de la aplicación hello. 

Veamos un ejemplo de la reserva de capacidad:

<center>
![Definición de la capacidad reservada para la instancia de aplicación][Image2]
</center>

En el ejemplo de Hola a izquierda, las aplicaciones no tiene ninguna capacidad de aplicación definida. Hola, Administrador de recursos del clúster equilibra todos los elementos según las reglas de toonormal.

En el ejemplo de Hola en hello derecho, supongamos que Application1 se creó con hello después de configuración:

- MinimumNodes establecer tootwo
- Una aplicación métrica definida con
  - NodeReservationCapacity de 20

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Service Fabric reserva capacidad en dos nodos para Application1 y no permite los servicios de Application2 tooconsume esa capacidad incluso si no hay que ninguna carga utilizada por servicios de hello dentro Application1 en tiempo de presentación. Se considera que esta capacidad reservada aplicación consumido y se descuenta de hello capacidad en ese nodo y en clúster de hello restante.  reserva de Hola se deduce de hello restantes capacidad clúster inmediatamente, pero Hola reservado consumo se deduce del capacidad Hola de un nodo específico solo cuando al menos un servicio se ponen en él. Esta reserva posterior permite flexibilidad y una mejor utilización de recursos, ya que solo se reservan recursos en nodos cuando resulta necesario.

## <a name="obtaining-hello-application-load-information"></a>Obtener información de carga de la aplicación hello
Para cada aplicación que tiene una capacidad de aplicación definidos para una o varias métricas puede obtener información de hello acerca de la carga global Hola notificado por las réplicas de sus servicios.

Powershell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

consulta de Hello ApplicationLoad devuelve información básica de hello acerca de la capacidad de las aplicaciones que se especificó para la aplicación hello. Esta información incluye información de nodos de mínimo y máximo de Hola y número de Hola que actualmente está ocupando aplicación hello. También incluye información de cada métrica de carga de la aplicación, por ejemplo:

* Nombre de la métrica: El nombre de métrica de Hola.
* Capacidad de reserva: Capacidad de clúster que está reservada en clúster de Hola para esta aplicación.
* Carga de la aplicación: carga total de las réplicas secundarias de esta aplicación.
* Capacidad de aplicación: valor máximo permitido de la carga de la aplicación.

## <a name="removing-application-capacity"></a>Eliminación de la capacidad de aplicación
Una vez que los parámetros de la capacidad de las aplicaciones de Hola se establecen para una aplicación, puede quitar mediante cmdlets de PowerShell o las API de aplicación de actualización. Por ejemplo:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

Este comando quita todos los parámetros de administración de capacidad de aplicación de la instancia de la aplicación hello. Esto incluye MinimumNodes, MaximumNodes y métricas de la aplicación hello, si lo hay. efecto de Hola de comando hello es inmediata. Una vez completado este comando, Hola, Administrador de recursos del clúster usa un comportamiento de hello predeterminado para administrar aplicaciones. Los parámetros de la capacidad de aplicación se pueden especificar de nuevo mediante `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Restricciones en la capacidad de aplicación
Existen varias restricciones en los parámetros de capacidad de aplicación que se deben respetar. Si hay errores de validación, no se producirá ningún cambio.

- Todos los parámetros de número entero deben ser números no negativos.
- MinimumNodes nunca debe ser mayor que MaximumNodes.
- Si se definen capacidades para una métrica de carga, deben seguir estas reglas:
  - La capacidad de reserva del nodo no debe ser superior a la capacidad máxima del nodo. Por ejemplo, no puede limitar la capacidad de Hola de métrica de Hola "CPU" en las unidades de tootwo del nodo de Hola e intente tooreserve tres unidades en cada nodo.
  - Si se especifica MaximumNodes, producto Hola de MaximumNodes y la capacidad máxima de nodo no debe ser mayor que la capacidad Total de la aplicación. Por ejemplo, supongamos que la capacidad máxima de nodo de métrica de carga "CPU" se establece tooeight Hola. Supongamos también que establece hello too10 de nodos máximos. En este caso, la capacidad total de aplicación debe ser mayor que 80 en esta métrica de carga.

se aplican restricciones de Hello tanto durante la creación de aplicaciones y actualizaciones.

## <a name="how-not-toouse-application-capacity"></a>Cómo no toouse capacidad de aplicación
- No intente toouse Hola grupo de aplicaciones características tooconstrain Hola aplicación tooa _específico_ subconjunto de nodos. En otras palabras, puede especificar que la aplicación hello se ejecuta en al menos cinco nodos, pero no qué cinco nodos específicos en clúster de Hola. Restringir una aplicación toospecific nodos pueden lograrse mediante las restricciones de posición para los servicios.
- No intente tooensure de capacidad de la aplicación hello toouse que dos servicios de hello misma aplicación se colocan en Hola los mismos nodos. En su lugar use la [afinidad](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) o las [restricciones de colocación](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Pasos siguientes
- Para más información sobre la configuración de servicios, vaya a [este vínculo](service-fabric-cluster-resource-manager-configure-services.md).
- toofind out acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, desproteger artículo hello en [equilibrio de carga](service-fabric-cluster-resource-manager-balancing.md)
- Desde el principio de Hola y [obtener un servicio Administrador de recursos del clúster de tejido de toohello de introducción](service-fabric-cluster-resource-manager-introduction.md)
- Para más información sobre cómo funcionan las métricas en general, lea el artículo [Administración de consumo y carga de recursos en Service Fabric con métricas](service-fabric-cluster-resource-manager-metrics.md)
- Hola, Administrador de recursos del clúster tiene muchas opciones para describir el clúster de Hola. toofind más información acerca de ellos, consulte este artículo en [que describe un clúster de Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
