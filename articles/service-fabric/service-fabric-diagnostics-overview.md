---
title: "aaaAzure información general sobre diagnóstico y supervisión del servicio de Fabric | Documentos de Microsoft"
description: "Obtenga información sobre la supervisión y el diagnóstico para los clústeres, las aplicaciones y los servicios de Azure Service Fabric."
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Supervisión y diagnóstico para Azure Service Fabric

Supervisión y diagnóstico está toodeveloping crítico, probar e implementar aplicaciones y servicios en cualquier entorno. Las soluciones de Service Fabric funcionan mejor cuando diseña e implementa la supervisión y el diagnóstico que ayudan a asegurarse de que las aplicaciones y los servicios funcionen según lo previsto en un entorno de desarrollo local o en producción.

Hola objetivos principales de supervisión y diagnóstico es para:
* Detectar y diagnosticar problemas de hardware y de infraestructura
* Detectar problemas de software y aplicaciones, y reducir el tiempo de inactividad del servicio
* Conocer el consumo de recursos y facilitar la toma de decisiones de operaciones
* Optimizar el rendimiento de la aplicación, el servicio y la infraestructura
* Generar información de la empresa e identificar áreas de mejora


Hola de flujo de trabajo general de supervisión y diagnóstico consta de tres pasos:

1. **Generación de eventos**: Esto incluye los eventos (registros, seguimientos de eventos personalizados) en la infraestructura de hello (clúster), la plataforma y el nivel de aplicación / servicio
2. **Agregación de eventos**: eventos generados necesitan toobe recopilan y se agregan antes de que se pueden mostrar
3. **Análisis**: eventos necesitan toobe visualizado y esté accesible en algún formato, tooallow para su análisis y visualización según sea necesario

Varios productos están disponibles que abarcan estas tres áreas y son toochoose libre tecnologías diferentes para cada uno. Es importante toomake seguro de que Hola toodeliver conjunto de trabajo una solución de supervisión de extremo a extremo para el clúster distintos de piezas.

## <a name="event-generation"></a>Generación de eventos

Hola primer paso en el flujo de trabajo de supervisión y diagnósticos de hello es Hola creación y generación de eventos y registros. Estos eventos, los registros y los seguimientos se generan en dos niveles: Hola a nivel de plataforma (incluidas clúster hello, máquinas de Hola o acciones de Service Fabric) u Hola a nivel de aplicación (ningún Instrumental agregado toohello clúster se implementó servicios y tooapps). Los eventos de cada uno de estos niveles son personalizables, aunque Service Fabric proporciona instrumentación de forma predeterminada.

Obtenga más información sobre [eventos de nivel de plataforma](service-fabric-diagnostics-event-generation-infra.md) y [eventos de nivel de aplicación](service-fabric-diagnostics-event-generation-app.md) toounderstand lo que se proporciona y cómo tooadd más Instrumental.

Después de tomar una decisión sobre Hola le gustaría toouse de proveedor de registro, debe toomake seguro de los registros se están agregan y almacenan correctamente.

## <a name="event-aggregation"></a>Agregación de datos

Para recopilar registros de Hola y eventos que va a generar sus aplicaciones y el clúster, se recomienda normalmente utilizar [diagnósticos de Azure](service-fabric-diagnostics-event-aggregation-wad.md) (colección de registro basado en tooagent más similar) o [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(en-proceso de recopilación de registros).

Recopilar registros de aplicación con la extensión de diagnósticos de Azure es una buena opción para los servicios de Service Fabric si Hola conjunto de orígenes de registro y destinos no cambian con frecuencia y hay una asignación directa entre orígenes de Hola y sus destinos. motivo de Hola para esto es la configuración de diagnósticos de Azure se produce en el nivel de administrador de recursos de hello, por lo que la configuración de toohello para realizar cambios significativos requiere actualizar o volver a implementar el clúster de Hola. Además, se utiliza de forma óptima al asegurarse de que los registros se almacenan en algún lugar un poco más permanente, donde puede obtenerse acceso a ellos mediante distintas plataformas de análisis. Esto significa que, en último término, es una opción menos eficiente para la canalización que utilizar una opción como EventFlow.

Usar [EventFlow](https://github.com/Azure/diagnostics-eventflow) permite toohave services envía sus registros directamente tooan análisis y plataforma de visualización o toostorage. Otras bibliotecas (ILogger, Serilog, etc.) podrían usarse para hello mismo propósito, pero EventFlow tiene las ventajas de Hola de ya han sido diseñadas específicamente para los servicios de Service Fabric de recopilación y toosupport del registro en curso. Esto tiende a toohave varias ventajas potenciales:

* Fácil configuración e implementación
    * configuración de Hola de recopilación de datos de diagnóstico es parte de la configuración del servicio Hola. Es mantener tooalways fácil que "sincronizados" con hello resto de la aplicación hello
    * Se puede realizar fácilmente la configuración por aplicación o por servicio.
    * Configurar los destinos de datos a través de EventFlow es cuestión de agregar paquete de NuGet adecuado de Hola y cambiar hello *eventFlowConfig.json* archivo
* Flexibilidad
    * aplicación Hello puede enviar datos de hello dondequiera que necesita toogo, siempre que hay una biblioteca de cliente que admite el sistema de almacenamiento de datos de Hola de destino. Se pueden agregar tantos destinos nuevos como se desee.
    * Se pueden implementar reglas complejas de captura, filtrado y agregación de datos.
* Contexto y obtener acceso a datos de aplicación de toointernal
    * subsistema de diagnóstico de Hello ejecuta en proceso de aplicación o un servicio de hello puede ampliar fácilmente la seguimientos de hello junto con información contextual

Una toonote lo es que estas dos opciones no son mutuamente excluyentes y mientras se tooget posible un trabajo similar con el uso de uno u Hola Sí, que podría también tiene sentido para usted tooset tanto. En la mayoría de los casos, la combinación de un agente con la colección en curso puede provocar tooa más fiable de supervisión de flujo de trabajo. Hola extensión de diagnósticos de Azure (agente) podría ser la ruta de acceso elegida para los registros de nivel de plataforma aunque podría utilizar EventFlow (en proceso colección) para sus registros de nivel de aplicación. Una vez que han descubierto qué funciona mejor para usted, es hora toothink acerca de cómo desea que su toobe de datos, mostrar y analizar.

## <a name="event-analysis"></a>Análisis de eventos

Hay varias plataformas excelentes que existen en el mercado de hello cuando se trata de toohello análisis y la visualización de datos de supervisión y diagnóstico. Hello dos que recomendamos son [OMS](service-fabric-diagnostics-event-analysis-oms.md) y [Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) debido tootheir una mejor integración con Service Fabric, pero se debe buscar en hello [pila elástico](https://www.elastic.co/products) (especialmente si se va a ejecutar un clúster en un entorno sin conexión), [Splunk](https://www.splunk.com/), o cualquier otra plataforma de su preferencia.

Hello puntos clave para cualquier plataforma que seleccione debe incluir el grado de comodidad son con interfaz de usuario de Hola y opciones, una consulta Hola datos toovisualize de capacidad y crean paneles fácilmente legibles y hello herramientas adicionales proporcionan tooenhance su supervisión, por ejemplo, alertar automatizadas.

Además toohello plataforma que elige, al configurar un clúster de Service Fabric como un recurso de Azure, también obtendrá acceso tooAzure de cuadro supervisión para las máquinas, que pueden ser útiles para obtener un rendimiento específico y métricas de supervisión.

### <a name="azure-monitor"></a>Azure Monitor

Puede usar [Monitor Azure](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor muchas de Hola recursos de Azure en el que se crea un clúster de Service Fabric. Un conjunto de métricas para hello [conjunto de escalas de máquina virtual](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) individuales y [máquinas virtuales](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) automáticamente se recopilan y se muestran en hello portal de Azure. Hola tooview información recopilada, en hello portal de Azure, grupo de recursos de hello select que contiene el clúster de Service Fabric Hola. A continuación, escalas de máquina virtual de hello seleccione establezca que desea tooview. Hola **supervisión** sección, seleccione **métricas** tooview un gráfico de valores de hello.

![Vista de Azure Portal con la información de métrica recopilada](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

gráficos de hello toocustomize, siga las instrucciones de hello en [métricas en Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md). También puede crear alertas basadas en estas métricas, como se describe en [Creación de alertas en Azure Monitor para servicios de Azure - Azure Portal](../monitoring-and-diagnostics/insights-alerts-portal.md). Puede enviar alertas de servicio de notificación de tooa mediante enlaces web, tal y como se describe en [configurar un enlace web en una alerta de métrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure Monitor es compatible con una sola suscripción. Si necesita toomonitor varias suscripciones, o si necesita características adicionales, [análisis de registros](https://azure.microsoft.com/documentation/services/log-analytics/), parte de Microsoft Operations Management Suite, proporciona una solución integral de administración de TI local y en la nube infraestructura. Puede enrutar datos desde el Monitor de Azure directamente tooLog análisis, de modo que pueda ver registros y las métricas para todo el entorno en un único lugar.

## <a name="next-steps"></a>Pasos siguientes

### <a name="watchdogs"></a>Guardianes

A continuación se proporciona es un servicio independiente que se puede ver el estado y la carga entre los servicios y el estado del informe para cualquier elemento de jerarquía del modelo de mantenimiento de Hola. Esto puede ayudar a evitar errores que no se detectan basados en la vista de Hola de un único servicio. Watchdogs también son un buena colocar el código toohost que lleva a cabo acciones correctoras sin interacción del usuario (por ejemplo, limpiar los archivos de registro de almacenamiento a determinados intervalos de tiempo). [Aquí](https://github.com/Azure-Samples/service-fabric-watchdog-service) puede encontrar la implementación de un servicio guardián de ejemplo.

Introducción a comprender cómo se generan los eventos y registros en hello [nivel de la plataforma](service-fabric-diagnostics-event-generation-infra.md) hello y [nivel de aplicación](service-fabric-diagnostics-event-generation-app.md).
