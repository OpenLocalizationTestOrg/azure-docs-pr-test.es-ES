---
title: "Análisis de eventos de tejido de servicio con Application Insights aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre cómo visualizar y analizar eventos con Application Insights para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Análisis y visualización de eventos con Application Insights

Azure Application Insights es una plataforma extensible para la supervisión y el diagnóstico de aplicaciones. Incluye una sólida herramienta de análisis y consulta, visualizaciones y paneles personalizables y otras opciones, como las alertas automáticas. Es Hola recomendada plataforma para la supervisión y diagnóstico para servicios y aplicaciones de Service Fabric.

## <a name="setting-up-application-insights"></a>Configuración de Application Insights

### <a name="creating-an-ai-resource"></a>Creación de un recurso de AI

recurso de toocreate una AI, principal sobre toohello Azure Marketplace y busque "Application Insights". Debería ser primera solución de hello (no en la categoría "Web + Mobile"). Haga clic en **crear** cuando se encuentre en recursos derecho hello (confirme que la ruta de acceso coincide con imagen Hola siguiente).

![Nuevo recurso de Application Insights](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Deberá toofill a algunos recursos de información tooprovision Hola correctamente. Hola *tipo de aplicación* campo, use "Aplicación web ASP.NET" Si va a usar cualquiera de Service Fabric del modelos de programación o un clúster de toohello de aplicaciones .NET de publicación. Use "General" si va a implementar contenedores y ejecutables de invitado. En general, predeterminado toousing "Aplicación web ASP.NET" tookeep las opciones de abren en hello futuras. Hola se denomina una preferencia de tooyour y grupo de recursos de Hola y suscripción son modificable posterior a la implementación de recursos de Hola. Se recomienda que el recurso de AI sea Hola mismo grupo de recursos que su clúster. Si necesita más información, vea [Creación de recursos en Application Insights](../application-insights/app-insights-create-new-resource.md).

Necesitará Hola clave de instrumentación AI tooconfigure AI con la herramienta de la agregación de eventos. Una vez que se ha configurado el recurso AI (tarda unos minutos después de valida la implementación de hello), navegue tooit y busque hello **propiedades** sección en la barra de navegación izquierda de Hola. Se abre una hoja nueva en la que aparece una *CLAVE DE INSTRUMENTACIÓN*. Si necesita toochange suscripción de Hola o grupo de recursos del recurso de hello, que es posible aquí también.

### <a name="configuring-ai-with-wad"></a>Configuración de AI con WAD

Hay dos métodos principales para datos de toosend de WAD tooAzure AI, que se consigue mediante la adición de una configuración de WAD AI receptor toohello, como se detalla en [este artículo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Agregar una clave de instrumentación de AI al crear un clúster en Azure Portal

![Adición de una clave de AI](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

Al crear un clúster, si se activa el diagnóstico "On", se mostrará un campo opcional tooenter una clave de instrumentación de la visión de aplicación. Si pega el IKey AI aquí, receptor Hola AI será automáticamente configuran automáticamente en plantilla de administrador de recursos de hello es toodeploy usa el clúster.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Agregar Hola plantilla de administrador de recursos de toohello de receptor de AI

Hola "WadCfg" de la plantilla de administrador de recursos de hello, agregue un "receptor" mediante la inclusión de hello siguiendo dos cambios:

1. Agregar configuración de receptor de hello:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Incluir Hola receptor en hello DiagnosticMonitorConfiguration agregando Hola línea siguiente en "DiagnosticMonitorConfiguration" Hola "WadCfg":

    ```json
    "sinks": "applicationInsights"
    ```

En ambos fragmentos de código de hello anteriormente, Hola nombre "applicationInsights" era receptor de hello toodescribe usado. Esto no es un requisito y siempre que se incluye el nombre de Hola de receptor de hello en "receptores", puede establecer la cadena de tooany de nombre de Hola.

Actualmente, los registros del clúster de Hola se mostrarán como seguimientos en el Visor de registro de AI. Puesto que la mayoría de los seguimientos de hello procedentes de la plataforma de Hola es de nivel de "Informativo", también puede considerar cambiar Hola receptor configuración tooonly enviar registros de tipo "Crítico" o "Error". Esto puede hacerse mediante la adición de receptor de tooyour de "Canales", como se muestra en [este artículo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Si usas un IKey AI incorrecto en el portal o en la plantilla de administrador de recursos, tendrá toomanually cambiar clave de Hola y actualizar clúster hello y volver a implementarla. 

### <a name="configuring-ai-with-eventflow"></a>Configuración de AI con EventFlow

Si usas EventFlow tooaggregate eventos, que seguro Hola de tooimport `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`paquete NuGet. Hello siguiente tiene toobe incluido en hello *genera* sección de hello *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Modificar en los filtros de hello necesario toomake seguro, así como incluir cualquier otras entradas (junto con sus respectivos paquetes de NuGet).

## <a name="aisdk"></a>AI.SDK

En general se recomienda toouse EventFlow y WAD como soluciones de agregación, ya que permiten que un toodiagnostics enfoque más modular y no supervisión, es decir, si desea que toochange los resultados de EventFlow, requiere ningún tooyour cambio real instrumentación, solo un archivo de configuración de tooyour modificación sencilla. Si, sin embargo, sólo decide tooinvest en el uso de visión de la aplicación y no es probable que toochange tooa otra plataforma, debería considerar la utilización nuevo SDK de AI para agregar eventos y los envía tooAI. Esto significa que ya no tendrá tooconfigure EventFlow toosend su tooAI de datos, pero en su lugar, se instalará el paquete de NuGet de tejido de servicio de hello ApplicationInsight. Encontrará detalles sobre el paquete de hello [aquí](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Compatibilidad con Application Insights de Microservicios y contenedores](https://azure.microsoft.com/app-insights-microservices/) muestra algunas de hello nuevas características que se está trabajando (todavía actualmente en versión beta), que le permiten toohave más completa del cuadro Opciones de supervisión con AI. Puede tratarse de seguimiento de dependencias (que se usaron para generar un AppMap de todos los servicios y aplicaciones en un clúster y Hola la comunicación entre ellos) y mejor correlación de seguimientos procedentes de los servicios (Ayuda en mejor indicar un problema en hello flujo de trabajo de una aplicación o servicio).

Si está desarrollando en .NET y lo probable es que se usan algunos de los modelos de programación de Service Fabric y están dispuesto toouse AI como la plataforma para visualizar y analizar datos de eventos y registros, le recomendamos que vaya a través de hello ruta AI SDK como la supervisión y flujo de trabajo de diagnóstico. Lectura [esto](../application-insights/app-insights-asp-net-more.md) y [esto](../application-insights/app-insights-asp-net-trace-logs.md) tooget Introducción al uso de AI toocollect y mostrar sus registros.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Navegar por los recursos de AI hello en el portal de Azure

Una vez haya configurado AI como una salida para los eventos y registros, información debe iniciarse tooshow en el recurso de AI dentro de unos minutos. Navegue del recurso AI toohello, que tendrá toohello AI panel recursos. Haga clic en **búsqueda** en hello AI barra de tareas toosee hello más reciente de seguimiento que ha recibido y toobe toofilter capaz de iteración.

El *Explorador de métricas* es una herramienta útil para crear paneles personalizados basados en métricas sobre las que las aplicaciones, los servicios y el clúster pueden informar. Vea [explorar las métricas en Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset seguridad unos gráficos por sí mismo en función de los datos de hello va a recopilar.

Haga clic en **análisis** le permitirán toohello portal de análisis de visión de aplicaciones, donde puede consultar eventos y seguimientos con mayor ámbito y definir la opcionalidad como. Lea más información en [Analytics en Application Insights](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Pasos siguientes

* [Configurar alertas en AI](../application-insights/app-insights-alerts.md) toobe notificado los cambios realizados en uso o rendimiento
* [Detección de Application Insights de Smart](../application-insights/app-insights-proactive-diagnostics.md) realiza un análisis automático de telemetría de hello enviarse tooAI toowarn de posibles problemas de rendimiento
