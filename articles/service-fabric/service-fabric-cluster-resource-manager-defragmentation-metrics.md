---
title: "aaaDefragmentation de métricas en Azure Service Fabric | Documentos de Microsoft"
description: "Información general del uso de la desfragmentación o el empaquetado como estrategia para métricas en Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Desfragmentación de métricas y carga en Service Fabric
estrategia predeterminada de Hello tejido clúster recursos de Service Manager para administrar las métricas de carga en el clúster de hello es carga de hello toodistribute. Asegurarse de que los nodos se utilizan uniformemente evita las zonas activas e inactivos que mejoren la contención de tooboth y recursos desperdiciados. Distribuir las cargas de trabajo en clúster de hello también es hello más segura en términos de supervivientes errores, ya que garantiza que un error no retire un porcentaje elevado de una carga de trabajo determinado. 

Hola, Administrador de recursos de clúster de tejido de servicio admite una estrategia diferente para administrar la carga, que es la desfragmentación. Desfragmentación significa que en lugar de tratar de utilización de hello toodistribute de una métrica en el clúster de hello, se ha consolidado. La consolidación es simplemente una inversión de valor predeterminado de hello estrategia: en lugar de minimizar Hola de desviación estándar promedio de métrica de carga de equilibrio, Hola, Administrador de recursos del clúster intenta tooincrease lo.

## <a name="when-toouse-defragmentation"></a>Cuando la desfragmentación toouse
Distribución de carga en el clúster de hello consume algunos de los recursos de hello en cada nodo. Algunas cargas de trabajo crean servicios que son excepcionalmente grandes y consumen la mayoría del nodo o el nodo entero. En estos casos, es posible que cuando hay grandes cargas de trabajo creados que no hay suficiente espacio en cualquier nodo toorun ellos. Grandes cargas de trabajo no están un problema de Service Fabric; en estos Hola casos Administrador de recursos del clúster determina que necesita espacio de toomake de tooreorganize Hola clúster para esta carga de trabajo grande. Sin embargo, en hello mientras tanto esa carga de trabajo tiene toobe toowait programado en clúster de Hola.

Si hay muchos servicios y estado toomove alrededor, puede tardar mucho tiempo para toobe de grandes cargas de trabajo de hello colocado en el clúster de Hola. Esto es más probable si otras cargas de trabajo en clúster de hello también son grandes y eche un vistazo más tooreorganize. equipo de Service Fabric Hola mide los tiempos de creación en las simulaciones de este escenario. Se encontró que la creación de servicios grandes tardaba mucho más tiempo en cuanto la utilización del clúster se situaba entre el 30 % y el 50 %. toohandle este escenario, se introdujo como una estrategia de equilibrio de la desfragmentación. Se encontró que para grandes cargas de trabajo, especialmente los que era importante, desfragmentación realmente ayudó a las cargas de trabajo nueva hora de creación se programan en clúster de Hola.

Puede configurar la desfragmentación métricas toohave Hola carga de tooproactively del Administrador de recursos de clúster intente toocondense hello de servicios de hello en menos nodos. Esto ayuda a garantizar que casi siempre hay espacio para servicios grandes sin reorganizar clúster Hola. No tener clúster de hello tooreorganize permite crear rápidamente grandes cargas de trabajo.

La mayoría de los usuarios no requiere desfragmentación. Los servicios se suele ser pequeño, por lo que no es el espacio de disco duro toofind para ellos en clúster de Hola. Cuando la reorganización es posible, funciona rápidamente, de nuevo porque la mayoría de los servicios son pequeños y se pueden mover fácilmente y en paralelo. Sin embargo, si tiene servicios grandes y necesiten crear rápidamente y Hola estrategia de desfragmentación es para usted. Trataremos compensaciones Hola de usar a continuación la desfragmentación. 

## <a name="defragmentation-tradeoffs"></a>Inconvenientes de la desfragmentación
La desfragmentación puede aumentar los errores de forma impactante, dado que hay más servicios en ejecución en los nodos que dan error. La desfragmentación puede aumentar los costos, como recursos de clúster de hello deben se mantiene en reserva, esperando la creación de hello grandes cargas de trabajo.

Hello siguiente diagrama proporciona una representación visual de dos clústeres, uno que está desfragmentado y otro que no sea. 

<center>
![Comparación de clústeres equilibrados y desfragmentados][Image1]
</center>

En caso de hello equilibrada, considere la posibilidad de número Hola movimientos que sería necesario tooplace uno hello más grandes de objetos de servicio. Hola clúster desfragmentado, carga de trabajo grande de hello podría colocarse en nodos de cuatro o cinco sin necesidad de toowait para otro toomove de servicios.

## <a name="defragmentation-pros-and-cons"></a>Ventajas y desventajas de la desfragmentación
¿Cuáles son esas otras soluciones intermedias conceptuales? Aquí es una tabla rápida de cosas toothink sobre:

| Ventajas de la desfragmentación | Inconvenientes de la desfragmentación |
| --- | --- |
| Permite la creación rápida de servicios de gran tamaño. |Concentra la carga en menos nodos, de modo que aumenta la contención. |
| Permite reducir el movimiento de datos durante la creación. |Los errores pueden afectar a más servicios y provocar más renovaciones. |
| Permite la descripción enriquecida de requisitos y la reclamación de espacio. |La configuración general de administración de recursos es más compleja. |

Es posible mezclar desfragmentado y métricas normales en Hola mismo clúster. Hola Administrador de recursos de clúster intentos tooconsolidate Hola desfragmentación métricas tanto como sea posible mientras extiende las Hola a otros usuarios. resultados de Hola de mezcla de desfragmentación y equilibrio estrategias depende de varios factores, incluyendo:
  - número de Hola de equilibrio métricas frente a número de Hola de métricas de desfragmentación
  - Si algún servicio usa ambos tipos de métricas 
  - pesos de métrica de Hola
  - Las cargas de métrica actuales
  
Experimentación es necesario toodetermine Hola exacta configuración necesaria. Se recomienda medir de forma exhaustiva sus cargas de trabajo antes de permitir métricas de desfragmentación en producción. Esto es especialmente cierto cuando se mezclan equilibrada métrica dentro de Hola y desfragmentación del mismo servicio. 

## <a name="configuring-defragmentation-metrics"></a>Configuración de métricas de desfragmentación
La configuración de métricas de desfragmentación es una decisión global en clúster de Hola y métricas individuales pueden seleccionarse para desfragmentación. Hola siguientes fragmentos de código de configuración muestra cómo tooconfigure métricas para la desfragmentación. En este caso, "Metric1" se configura como una métrica de desfragmentación, mientras que "Metric2" continuará toobe equilibrada normalmente. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Pasos siguientes
- Hola, Administrador de recursos del clúster tiene opciones de man para describir el clúster de Hola. toofind más información acerca de ellos, consulte este artículo en [que describe un clúster de Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Las métricas son cómo Hola, Administrador de recursos de clúster de tejido de servicio administra capacidad en clúster de Hola y consumo. toolearn más información acerca de las métricas y cómo tooconfigure, visite [este artículo](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
