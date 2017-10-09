---
title: "las aplicaciones de Service Fabric con el uso de análisis de registros aaaAssess Hola portal de Azure | Documentos de Microsoft"
description: "Puede usar soluciones de Service Fabric hello en análisis de registros con el riesgo de hello tooassess portal Azure de Hola y el estado de las aplicaciones de Service Fabric, micro-services, nodos y clústeres."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Evaluar las aplicaciones de Service Fabric y microservicios con hello portal de Azure

> [!div class="op_single_selector"]
> * [Resource Manager](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Símbolo de Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

Este artículo describe cómo toouse Hola solución de Service Fabric en análisis de registros toohelp identificar y solucionar problemas en el clúster de Service Fabric.

Hola soluciones de Service Fabric utiliza datos de diagnósticos de Azure de las máquinas virtuales tejido de servicio, mediante la recopilación de estos datos de las tablas de WAD de Azure. Posteriormente, Log Analytics lee los eventos del marco de Service Fabric, incluidos los **eventos de servicios de confianza**, los **eventos de actor**, los **eventos operativos** y los **eventos ETW personalizados**. Con el panel de la solución de hello, son problemas importantes capaz de tooview y los eventos relevantes en su entorno de Service Fabric.

tooget a trabajar con soluciones de hello, deberá tooconnect el área de trabajo de análisis de registros de Service Fabric clúster tooa. A continuación, presentamos tres tooconsider de escenarios:

1. Si no ha implementado el clúster de Service Fabric, siga los pasos de hello en ***implementar un área de trabajo de análisis de registros de servicio de Cluster Server tejido conectado tooa*** toodeploy un nuevo clúster y configuró tooreport tooLog análisis.
2. Si necesita toocollect los contadores de rendimiento de su toouse hosts otras soluciones OMS como la seguridad en su clúster de Service Fabric, siga los pasos de hello en ***implementar un área de trabajo de análisis de registros de tooa de clúster de Service Fabric conectado con la extensión de máquina virtual instalado.***
3. Si ya ha implementado el clúster de Service Fabric y desea tooconnect se tooLog análisis, siga los pasos de hello en ***agregando un tooLog de cuenta de almacenamiento existente análisis.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Implementar un área de trabajo de análisis de registros de tooa conectado el clúster de Service Fabric.
Esta plantilla Hola siguientes:

1. Implementa un área de trabajo de análisis de registros de Azure Service Fabric ya está conectado el clúster tooa. Tener Hola opción toocreate una nueva área de trabajo durante la implementación de plantilla de Hola o nombre de entrada Hola de un área de trabajo de análisis de registros ya existente.
2. Agrega el área de trabajo de análisis de registro de toohello de cuenta de hello el almacenamiento de diagnóstico.
3. Habilita la solución de Service Fabric de hello en el área de trabajo de análisis de registros.

[![Implementar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

Una vez que selecciona Hola implementar el botón de más arriba, hello Azure abre portal con parámetros para tooedit. Ser seguro toocreate un nuevo grupo de recursos si se escribe un nuevo nombre de área de trabajo de análisis de registros:

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Acepte los términos legales de Hola y haga clic en **crear** implementación de hello toostart. Una vez completada la implementación de hello, debería ver área de trabajo nueva hello y clúster creado y Hola WADServiceFabric * WADWindowsEventLogs de eventos y WADETWEvent tablas agregadas:

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Implementar un área de trabajo de análisis de registros de tooa de clúster de Service Fabric conectado con la extensión de VM instalado.

Esta plantilla Hola siguientes:

1. Implementa un área de trabajo de análisis de registros de Azure Service Fabric ya está conectado el clúster tooa. Puede crear una tabla o usar una existente.
2. Agrega el área de trabajo de análisis de registro de toohello de cuentas de hello el almacenamiento de diagnóstico.
3. Habilita la solución de Service Fabric hello en el área de trabajo de análisis de registros de Hola.
4. Instala la extensión del agente MMA hello en cada conjunto en el clúster de Service Fabric de escalas de máquina virtual. Con instalado el agente MMA hello, está tooview capaz de métricas de rendimiento acerca de los nodos.

[![Implementar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

A continuación Hola los mismos pasos anteriormente, los parámetros necesarios de entrada hello y comenzar una implementación. Una vez más verá nueva área de trabajo de hello, el clúster y creadas todas las tablas WAD:

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Visualización de datos de rendimiento

tooview datos de rendimiento de los nodos:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Inicie el área de trabajo de análisis de registros de Hola de hello portal de Azure.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- Vaya tooSettings en el panel izquierdo de Hola y seleccionar los datos >> contadores de rendimiento de Windows >> "hello complemento seleccionado los contadores de rendimiento": ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- En búsqueda de registros, utilice Hola después toodelve de las consultas en las métricas clave sobre los nodos:

    a. Comparar Hola uso promedio de CPU en todos los nodos de hello último una hora toosee qué nodos están experimentando problemas al y en el intervalo de tiempo que un nodo tenía un pico:

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Vea gráficos de líneas similares para la memoria disponible en cada nodo con esta consulta:

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview una lista de todos los nodos, donde se muestran un valor promedio exacto Hola de MBytes disponibles para cada nodo, use esta consulta:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. En caso de Hola que quiera toodrill hacia abajo en un nodo específico mediante el examen de media hora de hello, uso de CPU mínimo, máximo y percentil 75, le toodo puede confirmarlo mediante esta consulta (sustituya el campo de equipo):

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

Leer más información acerca de las métricas de rendimiento de análisis de registros en hello [blog de Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Agregar un tooLog de cuenta de almacenamiento existente análisis

Esta plantilla simplemente agrega su almacenamiento cuentas tooa nuevo o existente análisis de registros área de trabajo existente.

[![Implementar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> En la selección de un grupo de recursos, si está trabajando con un área de trabajo de análisis de registros ya existente, seleccione "Usar existente" y busque el grupo de recursos de Hola que contiene el área de trabajo de análisis de registros de Hola. En caso contrario, cree uno nuevo.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

Una vez se ha implementado esta plantilla, es posible que el área de trabajo de toosee capaz de hello almacenamiento cuenta conectada tooyour análisis de registros. En este caso, agregué una más almacenamiento cuenta toohello Exchange área de trabajo que creó anteriormente.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Visualización de eventos de Service Fabric

Una vez que se completen las implementaciones de Hola y Hola soluciones de tejido de servicio se ha habilitado en el área de trabajo, seleccione hello **Service Fabric** el icono Panel de hello análisis de registros toolaunch portal Hola Service Fabric. panel de Hello incluye columnas de hello en hello en la tabla siguiente. Cada columna muestra top 10 eventos de hello mediante la correspondencia de recuento que han especificado criterios de la columna para hello intervalo de tiempo. Puede ejecutar una búsqueda de registros que proporciona la lista completa de hello haciendo clic en **ver todas** en hello derecha, abajo de cada columna, o haciendo clic en el encabezado de columna de Hola.

| **Evento de Service Fabric** | **descripción** |
| --- | --- |
| Problemas importantes |Una pantalla con problemas como RunAsyncFailures RunAsynCancellations y nodos inactivos. |
| Eventos operativos |Eventos operativos importantes como implementaciones y actualizaciones de aplicaciones. |
| Eventos de servicios de confianza |Eventos de servicios de confianza importantes como Runasyncinvocations. |
| Eventos de actor |Eventos de actor importantes generados por los microservicios, como las excepciones que inician un método de actor, activaciones y desactivaciones de actor, etc. |
| Eventos de aplicación |Todos los eventos ETW personalizados generados por las aplicaciones. |

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Panel de Service Fabric](./media/log-analytics-service-fabric/sf4.png)

Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de Service Fabric.

| plataforma | Agente directo | Agente de Operations Manager | Almacenamiento de Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 minutos |

> [!NOTE]
> También puede cambiar el ámbito de Hola de estos eventos en hello soluciones de Service Fabric haciendo clic en **datos basándose en los últimos 7 días** en parte superior de hello del panel de Hola. También puede mostrar los eventos generados en hello últimos siete días, un día o seis horas. O bien, puede seleccionar **personalizado** toospecify un intervalo de fechas personalizado.
>
>

## <a name="next-steps"></a>Pasos siguientes

* Use [búsquedas de registros de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de eventos de Service Fabric.
