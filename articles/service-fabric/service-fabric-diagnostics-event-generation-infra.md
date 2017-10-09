---
title: "aaaAzure supervisión de nivel de servicio Fabric plataforma | Documentos de Microsoft"
description: "Obtenga información acerca de los eventos de nivel de plataforma y registros usan toomonitor y diagnosticar clústeres Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>Generación de eventos y registros de nivel de plataforma

## <a name="monitoring-hello-cluster"></a>Supervisión de clústeres de Hola

Es importante toomonitor en toodetermine nivel en la plataforma de Hola o no el hardware y el clúster se comportan según lo esperado. Aunque Service Fabric puede mantener aplicaciones que se ejecutan durante un error de hardware, pero necesitará toodiagnose si se produce un error en una aplicación o en la infraestructura subyacente de Hola. También debe supervisar su plan de toobetter clústeres la capacidad, lo que ayuda en las decisiones sobre cómo agregar o quitar hardware.

Service Fabric proporciona cinco registros diferentes canales fuera-de-predeterminada que generan Hola después de eventos:

* Canal operativo: las operaciones de alto nivel realizadas por Service Fabric y clúster de hello, incluidos los eventos de un nodo a continuación, una nueva aplicación que se implementa, o un SF actualizar rollback, etcetera.
* Canal operativo: detallado: informes de estado y decisiones para el equilibrio de carga
* Canal de mensajería & datos: registros críticos y los eventos generados en nuestra mensajería (actualmente solo Hola ReverseProxy) y la ruta de acceso de datos (modelos de servicios de confianza)
* Canal de datos y mensajería - detallada: canal detallado que contiene todos los registros no críticos Hola de datos y mensajería en clúster de hello (este canal tiene un volumen elevado de eventos)   
* [Eventos de Reliable Services](service-fabric-reliable-services-diagnostics.md): eventos específicos del modelo de programación
* [Eventos de Reliable Actors](service-fabric-reliable-actors-diagnostics.md): contadores de rendimiento y eventos específicos del modelo de programación
* Compatible con registros: generados por Service Fabric toobe solo usado nos al proporcionar compatibilidad con registros del sistema

Estos canales distintos cubren la mayor parte de hello plataforma registro en el nivel que se recomienda. nivel de la plataforma de tooimprove registro, considere la posibilidad de invertir en una mejor comprensión Hola modelo de estado y agregar informes de estado personalizado y agregar personalizada **contadores de rendimiento** toobuild una comprensión en tiempo real de hello afectar de los servicios y aplicaciones en clúster de Hola.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Informes de carga y mantenimiento de Azure Service Fabric

Service Fabric tiene su propio modelo de mantenimiento, que se describe en detalle en estos artículos:
- [Supervisión de estado del tejido de tooService de introducción](service-fabric-health-introduction.md)
- [Notificación y comprobación del estado del servicio](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Incorporación de informes de mantenimiento de Service Fabric personalizados](service-fabric-report-health.md)
- [Vista de los informes de estado de Service Fabric](service-fabric-view-entities-aggregated-health.md)

Supervisión de estado es crítico toomultiple aspectos de la operación de un servicio. La supervisión del mantenimiento es especialmente importante cuando Service Fabric lleva a cabo una actualización de la aplicación con nombre. Después de cada dominio de actualización del servicio de Hola se actualiza y está disponible tooyour clientes, dominio de actualización de hello debe pasar las comprobaciones de mantenimiento antes de que pase de implementación de hello toohello siguiente dominio de actualización. Si no se puede alcanzar el buen estado, implementación de Hola se revierte, para que la aplicación hello está en un estado bueno conocido. Aunque algunos clientes podrían verse afectados antes de que se revierten servicios hello, la mayoría de los clientes no experimentará un problema. Además, se produce una resolución relativamente rápidamente y sin necesidad de toowait para la acción de un operador humano. Hola más comprobaciones de mantenimiento que se integran en el código, hello más resistente que el servicio es toodeployment problemas.

Otro aspecto del estado del servicio está informando de las métricas de servicio de Hola. Las métricas son importantes en Service Fabric porque son utilizados toobalance uso de recursos. Además, son un indicador del estado del sistema. Por ejemplo, supongamos que tiene una aplicación con muchos servicios y que cada instancia informa sobre una métrica de solicitudes por segundo (RPS). Si un servicio está usando más recursos que otro servicio, Service Fabric mueve instancias de servicio en clúster de hello, uso de recursos incluso toomaintain tootry. Para una explicación más detallada sobre cómo funciona el uso de los recursos, consulte [Administración de consumo y carga de recursos en Service Fabric con métricas](service-fabric-cluster-resource-manager-metrics.md).

Las métricas también pueden ayudarle con una visión general de rendimiento del servicio. Con el tiempo, puede utilizar toocheck de métricas que Hola servicio esté funcionando en parámetros esperados. Por ejemplo, si las tendencias muestran que a las 9 A.M. en hello lunes por la mañana promedio RPS es 1.000, puede configurar un informe de estado que le advierte si hello RPS es inferior a 500 o superior 1.500. Todo lo que podría ser perfectamente correcto, pero podría ser conveniente un toobe vistazo seguro de que los clientes tienen una gran experiencia. El servicio puede definir un conjunto de métricas que se puede notificar para fines de comprobación de mantenimiento, pero que no afectan a Hola equilibrar los recursos de clúster de Hola. toodo, toozero de peso métrico de Hola de conjunto. Se recomienda iniciar todas las métricas con un peso de cero y no aumentar peso Hola hasta que esté seguro de que comprende cómo afecta la ponderación métricas de Hola a recursos para el clúster de equilibrio.

> [!TIP]
> No use demasiadas métricas ponderadas. Puede ser difícil toounderstand ¿por qué instancias de servicio se están moviendo de equilibrio. Algunas pueden moverse muchísimo.

Toda la información que puede indicar el estado de Hola y el rendimiento de la aplicación es un candidato para informes de mantenimiento y las métricas. Un contador de rendimiento de la CPU puede indicar cómo se está usando el nodo, pero no indica si un servicio determinado está en buen estado, ya que pueden estar ejecutándose varios servicios en un solo nodo. Pero, métricas como RPS, elementos procesados, y todos los de latencia de solicitudes puede indican el estado de Hola de un servicio específico.

estado de tooreport, use código similar toothis:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport una métrica, use código similar toothis:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Registros de soporte técnico de Service Fabric

Si necesita toocontact soporte técnico de Microsoft para obtener ayuda con el clúster de Azure Service Fabric, casi siempre se necesitan registros de soporte técnico. Si el clúster se hospeda en Azure, estos registros de soporte técnico se configuran y recopilan automáticamente en el proceso de creación del clúster. Hola registros se almacenan en una cuenta de almacenamiento dedicado en el grupo de recursos de su clúster. cuenta de almacenamiento de Hello no tiene un nombre fijo, pero en la cuenta de hello, vea contenedores de blobs y tablas con nombres que empiezan por *tejido*. Para obtener información acerca de cómo configurar las colecciones de registros para un clúster independiente, consulte el artículo sobre la [creación y la administración de un clúster independiente de Azure Service Fabric](service-fabric-cluster-creation-for-windows-server.md) y [Opciones de configuración clústeres de Windows independientes](service-fabric-cluster-manifest.md). Para instancias de Service Fabric independientes, se deben enviar a registros de hello recurso compartido de archivos local de tooa. Está **requiere** toohave estos registros para soporte técnico, pero no son toobe previsto utilizable por alguien fuera de equipo de soporte técnico de cliente de Microsoft de Hola.

## <a name="enabling-diagnostics-for-a-cluster"></a>Habilitar Diagnostics para un clúster

En orden tootake aprovechar estos registros, se recomienda encarecidamente que, durante la creación del clúster, "Diagnostics" está habilitada. Activando el diagnóstico, cuando se implementa el clúster de hello, diagnósticos de Windows Azure es capaz de tooacknowledge Hola Operational, servicios confiables y canales de confianza actores y almacenar datos de hello como se explica más detalladamente en [agregar eventos a Diagnósticos de Azure](service-fabric-diagnostics-event-aggregation-wad.md).

Tal como se muestra anteriormente, también hay un tooadd campo opcional una clave de instrumentación de visión de la aplicación (AI). Si elige toouse AI para los análisis de eventos (leer más sobre esto en [análisis de eventos con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)), incluimos hello AppInsights recursos instrumentationKey (GUID).


Si va clúster tooyour de toodeploy contenedores, habilitar toopick WAD de estadísticas de docker mediante la adición de este tooyour "WadCfg > DiagnosticMonitorConfiguration":

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Medir el rendimiento

Medir el rendimiento de su clúster le ayudará a entender cómo es capaz de toohandle decisiones de carga y la unidad alrededor de ajuste de escala en el clúster (consulte más información acerca de ajuste de escala en un clúster de [en Azure](service-fabric-cluster-scale-up-down.md), o [local](service-fabric-cluster-windows-server-add-remove-nodes.md)). Los datos de rendimiento también están útil cuando compara tooactions usted o sus aplicaciones y servicios podrán haber tardado, al analizar los registros de hello futuras. 

Para obtener una lista de toocollect de contadores de rendimiento al usar Service Fabric, vea [contadores de rendimiento de Service Fabric](service-fabric-diagnostics-event-generation-perf.md)

A continuación se indican dos formas habituales de configurar la recopilación de datos de rendimiento del clúster:

* Uso de un agente: se trata de manera Hola preferido de recopilación de rendimiento de una máquina, ya que los agentes suelen tienen una lista de las métricas de rendimiento posibles que se pueden recopilar y es una métrica de hello es relativamente fácil de proceso que toochoose desea toocollect o cambiarlos . Obtenga información sobre [cómo tooconfigure Hola OMS para Service Fabric](service-fabric-diagnostics-event-analysis-oms.md) y [configurar agente de OMS Windows hello](../log-analytics/log-analytics-windows-agents.md) artículos toolearn más información acerca del agente de OMS hello, que es un tal agente de supervisión que es capaz de toopick hacia arriba datos de rendimiento para las máquinas virtuales del clúster y los contenedores implementados.

* Configuración de rendimiento de diagnóstico toowrite contadores tabla tooa: para los clústeres en Azure, esto significa cambiar hello toopick de configuración de diagnósticos de Azure los contadores de rendimiento adecuado de Hola de hello las máquinas virtuales en el clúster y habilitar toopick seguridad estadísticas de docker si va a implementar los contenedores. Leer acerca de cómo configurar [contadores de rendimiento de WAD](service-fabric-diagnostics-event-aggregation-wad.md) en tooset Service Fabric una recopilación de contadores de rendimiento.

## <a name="next-steps"></a>Pasos siguientes

Los registros y eventos necesitan toobe agrega antes de que se puede enviar tooany plataforma de análisis. Obtenga información sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) y [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprender algunas de hello opciones recomendada.
