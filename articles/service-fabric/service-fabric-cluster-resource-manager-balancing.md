---
title: "aaaBalance el clúster de Azure Service Fabric | Documentos de Microsoft"
description: "Un toobalancing de introducción del clúster con el servicio Administrador de recursos del clúster de tejido de Hola."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a>Equilibrio del clúster de Service Fabric
Hola, Administrador de recursos de clúster de tejido de servicio admite cambios de carga dinámico, tooadditions reaccionando o las eliminaciones de nodos o servicios. También corrige automáticamente las infracciones de restricción y vuelve a equilibrar clúster Hola de forma proactiva. ¿Pero con qué frecuencia se realizan estas acciones y qué las activa?

Hay tres categorías diferentes de trabajo que realiza el Administrador de recursos del clúster de Hola. Son las siguientes:

1. Ubicación: esta fase tiene que ver con la colocación de las réplicas con estado o las instancias sin estado que faltan. Abarca los nuevos servicios y la administración de réplicas con estado o instancias sin estado incorrectas. Aquí también se administra la eliminación de réplicas o instancias.
2. Se comprueba la restricción: esta fase se comprueba y corrige las infracciones de restricciones de posición diferente de hello (reglas) en el sistema de Hola. Algunos ejemplos de reglas son asegurarse de que los nodos no sobrepasan la capacidad y que las restricciones de selección de ubicación de un servicio se cumplen.
3. Equilibrio de esta fase se comprueba toosee si reequilibrio es necesario basándose en hello configurado nivel deseado de saldo de métricas diferentes. Si lo intenta toofind una disposición en hello del clúster que es más equilibrada.

## <a name="configuring-cluster-resource-manager-timers"></a>Configuración de temporizadores de Cluster Resource Manager
Hola primer conjunto de controles de equilibrio son un conjunto de temporizadores. Estos temporizadores controlan la frecuencia con hello Administrador de recursos del clúster examina clúster hello y toma medidas correctivas.

Cada uno de estos tipos diferentes de hello correcciones puede hacer el Administrador de recursos del clúster se controla mediante un temporizador diferentes que rige su frecuencia. Cuando se activa cada temporizador, se programa la tarea hello. De forma predeterminada Hola Administrador de recursos:

* Examina su estado y aplica las actualizaciones (por ejemplo, la grabación de que un nodo está inactivo) cada 1/10 de segundo.
* establece la marca de verificación de selección de ubicación de Hola 
* establece la marca de verificación de restricción de hello cada segundo
* establece Hola equilibrio marca cada cinco segundos.

Ejemplos de configuración de Hola que rigen estos temporizadores son los siguientes:

ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

Hoy en día Hola, Administrador de recursos del clúster sólo realiza una de estas acciones a la vez, secuencialmente. Se trata de por qué se hacen referencia los temporizadores de toothese como "intervalos mínimos" y Hola medidas que obtengan tomar al temporizadores Hola apagarán "marcadores de configuración". Por ejemplo, Hola, Administrador de recursos del clúster se encarga de pendiente solicita toocreate services antes de hello clúster de equilibrio. Como puede ver por intervalos de tiempo predeterminado de hello especificados, Hola, Administrador de recursos del clúster analiza para cualquier elemento necesidades toodo con frecuencia. Normalmente esto significa que el conjunto de Hola de los cambios realizados durante cada paso es pequeño. Realizar pequeños cambios con frecuencia permite hello toobe del Administrador de recursos de clúster responda cuando ocurren cosas en clúster de Hola. Hello temporizadores predeterminados proporcionan algún procesamiento por lotes desde muchos Hola mismo tipos de eventos suelen toooccur al mismo tiempo. 

Por ejemplo, cuando los nodos no funcionan pueden provocar que todos los dominios dejen de funcionar a la vez. Todos estos errores se capturan durante el siguiente estado de hello actualización después de hello *PLBRefreshGap*. correcciones de Hola se determinan durante Hola después de selección de ubicación, comprobación de restricción y el equilibrio de ejecuciones. Hola predeterminado Administrador de recursos del clúster no está analizando horas de cambios en el clúster de Hola e intentar tooaddress todos los cambios a la vez. Si lo hace, provocaría toobursts de renovación.

Hola, Administrador de recursos del clúster también necesita algunos toodetermine información adicional si hello en clúster equilibrado. Para ello se cuenta con dos elementos de configuración: *BalancingThresholds* y *ActivityThresholds*.

## <a name="balancing-thresholds"></a>Umbrales de equilibrio
Un umbral de equilibrio es control principal de hello para la activación de reequilibrio. Hola equilibrio de umbral de una métrica es un _proporción_. Si carga Hola para una métrica en hello más carga nodo dividido por volumen Hola de carga Hola menos cargado nodo supera esa métrica *BalancingThreshold*, clúster de hello es desequilibrado. Como resultado equilibrio es Hola Hola desencadenadas de tiempo siguiente comprueba el Administrador de recursos del clúster. Hola *MinLoadBalancingInterval* temporizador define la frecuencia con hello Administrador de recursos del clúster debe comprobar si el nuevo equilibrio es necesario. La comprobación no significa que suceda nada. 

Se han definido umbrales de equilibrio de forma por métrica como parte de la definición del clúster de Hola. Para más información sobre las métricas, consulte [este artículo](service-fabric-cluster-resource-manager-metrics.md).

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<center>
![Ejemplo de umbral de equilibrio][Image1]
</center>

En este ejemplo, cada servicio solo consume una unidad de alguna métrica. En el ejemplo de Hola superior, carga máxima de hello en un nodo es cinco y mínimo de hello es dos. Supongamos que Hola equilibrio umbral para esta métrica es tres. Puesto que la proporción de hello en clúster de hello es 5/2 = 2.5 y que es menor que la especificada de hello equilibrio umbral de tres, clúster de hello está equilibrada. Equilibrio no se desencadena cuando comprueba Hola, Administrador de recursos del clúster.

En el ejemplo de la parte inferior de hello, carga máxima de hello en un nodo es 10, mientras mínimo hello es dos, como resultado una relación de cinco. Cinco es mayor que el umbral de equilibrio designado de Hola de tres para esa métrica. Como resultado, una ejecución de reequilibrio será programada Hola tiempo siguiente equilibrio se activa de temporizador. En una situación como ésta cierta carga es tooNode3 normalmente distribuida. Porque Hola, Administrador de recursos de clúster de tejido de servicio no usa un enfoque expansivo, cierta carga también podría ser tooNode2 distribuida. 

<center>
![Acciones de ejemplo de umbral de equilibrio][Image2]
</center>

> [!NOTE]
> "Equilibrio" controla dos estrategias distintas para administrar la carga del clúster. estrategia de predeterminada Hola Hola usos del Administrador de recursos de clúster es toodistribute carga en todos los nodos de hello en clúster de Hola. Hola otra estrategia es [desfragmentación](service-fabric-cluster-resource-manager-defragmentation-metrics.md). La desfragmentación se realiza durante Hola equilibrio mismo ejecutar. Hello las estrategias de desfragmentación y equilibrio pueden utilizarse para diferentes métricas dentro de hello mismo clúster. Un servicio puede tener métricas de equilibrio y desfragmentación. Para las métricas de desfragmentación, carga proporción de Hola de hello en los desencadenadores de clúster de hello reequilibrio cuando sea _a continuación_ Hola equilibrio umbral. 
>

Introducción a continuación Hola equilibrio umbral no es un objetivo explícito. Los umbrales de equilibrio son tan solo un *desencadenador*. Cuando equilibrio se ejecuta, Hola, Administrador de recursos del clúster determina qué mejoras puede ralentizar, si lo hay. El inicio de una búsqueda de equilibrio no significa que nada cambie. A veces hello clúster es toocorrect desequilibrado pero demasiado limitada. Como alternativa, mejoras de hello necesitan movimientos que son demasiado [costoso](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>umbrales de actividad
A veces, aunque los nodos son relativamente desequilibrados, Hola *total* cantidad de carga en el clúster de hello es baja. falta de Hola de carga podría ser una dip transitoria, o porque clúster hello ' s new and simplemente Introducción al iniciar. En cualquier caso, no puede tiempo toospend Hola clúster con equilibrio porque hay poca toobe adquirida. Clúster Hola hayan sufrido equilibrio, se invierte en red y proceso recursos toomove cosas sin realizar cualquier grandes *absoluta* diferencia. se mueve tooavoid innecesario, hay otro control que se conoce como umbrales de actividad. Umbrales de actividad le permite toospecify límite algunos inferior absoluta para la actividad. Si ningún nodo se encuentra sobre este umbral, equilibrio no desencadena incluso si hello equilibrio umbral se cumple.

Supongamos que se mantiene el umbral de equilibrio de tres para esta métrica. Supongamos también que se tiene un umbral de actividad de 1536. En el primer caso de hello, mientras está equilibrado por hello clúster Hola equilibrio umbral existe no es ningún nodo cumple ese umbral de actividad, nada por lo que ocurre. En el ejemplo de la parte inferior de hello, Nodo1 está por encima de hello umbral de actividad. Dado que ambos Hola umbral de equilibrio y se superan Hola actividad umbral de métrica de Hola, equilibrio está programado. Por ejemplo, echemos un vistazo a Hola siguiente diagrama: 

<center>
![Ejemplo de umbral de actividad][Image3]
</center>

Igual que los umbrales de equilibrio, umbrales de actividad son definidos por métrica a través de la definición del clúster hello:

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

Umbrales de equilibrio y actividad son ambos métrica específica tooa ligada - equilibrio se activa sólo si ambos Hola umbral de equilibrio y se supera el umbral de actividad para hello misma métrica.

## <a name="balancing-services-together"></a>Equilibrio conjunto de los servicios
Si el clúster de hello es desequilibrado o no es una decisión de todo el clúster. Sin embargo, manera Hola decidimos acerca de la solución refiere a instancias alrededor y réplicas de servicio individuales. Tiene sentido, ¿no? Si la memoria es apilada en un nodo, varias réplicas o instancias podrían contribuir tooit. Corrección desequilibrio Hola podría ser necesario mover cualquiera de las réplicas con estado de Hola o instancias sin estado que utiliza Hola desequilibrado métrica.

Sin embargo, en ocasiones obtiene mueve un servicio que no sea propio desequilibrado (recuerde discusión Hola de local y global pondera anteriormente). ¿Por qué habría de moverse un servicio si todas sus métricas están equilibradas? Veamos un ejemplo:

- Supongamos que hay cuatro servicios, Service1, Service2, Service3 y Service4. 
- Service1 informa de las métricas Metric1 y Metric2. 
- Service2 informa de las métricas Metric2 y Metric3. 
- Service3 informa de las métricas Metric3 y Metric4.
- Service4 informa de la Metric99. 

Seguramente puede ver adónde queremos llegar: hay una cadena. En realidad no tenemos cuatro servicios independientes, sino tres servicios que están relacionados y uno que va por su cuenta.

<center>
![Equilibrio conjunto de los servicios][Image4]
</center>

Debido a esta cadena, es posible que un desequilibrio en las métricas de 1 a 4 puede hacer que las réplicas o instancias que pertenecen tooservices toomove de 1 a 3 alrededor. También sabemos que un desequilibrio en las métricas 1, 2 o 3 no puede ocasionar movimientos en Service4. No habría ningún punto desde mover réplicas de Hola o instancias que pertenecen tooService4 alrededor puede no aportan nada tooimpact Hola equilibrio entre las métricas de 1 a 3.

Hola, Administrador de recursos del clúster imagina automáticamente qué servicios están relacionados. Agregar, quitar o cambian las métricas de Hola para servicios pueden afectar a las relaciones entre ellas. Por ejemplo, entre las dos ejecuciones de equilibrio Service2 se haya actualizado tooremove Metric2. Esto interrumpe la cadena de hello entre Service1 y Service2. Ahora, en lugar de dos grupos de servicios relacionados, hay tres:

<center>
![Equilibrio conjunto de los servicios][Image5]
</center>

## <a name="next-steps"></a>Pasos siguientes
* Las métricas son cómo Hola, Administrador de recursos de clúster de tejido de servicio administra capacidad en clúster de Hola y consumo. toolearn más información acerca de las métricas y cómo tooconfigure, visite [este artículo](service-fabric-cluster-resource-manager-metrics.md)
* Coste del movimiento es una manera de señalización toohello Administrador de recursos del clúster que determinados servicios estén toomove más cara que otras. Para obtener más información sobre el coste del movimiento, consulte demasiado[este artículo](service-fabric-cluster-resource-manager-movement-cost.md)
* Hola, Administrador de recursos del clúster tiene varias limitaciones que se puede configurar tooslow hacia abajo renovación en clúster de Hola. Aunque no son normalmente necesarias, si las necesita, puede encontrar información sobre ellas [aquí](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
