---
title: aaaAzure Application Insights compatibilidad con varios componentes, microservicios y contenedores | Documentos de Microsoft
description: "Supervisión de aplicaciones que constan de varios componentes o roles para uso y rendimiento."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Supervisión de aplicaciones de varios componentes con Application Insights (versión preliminar)

Puede supervisar aplicaciones que consten de varios componentes, roles o servicios de servidor con [Azure Application Insights](app-insights-overview.md). estado de Hola de componentes de Hola y relaciones de hello entre ellos se muestran en una sola asignación de aplicación. Puede realizar el seguimiento de ciertas operaciones por medio de varios componentes con correlación HTTP automática. El diagnóstico de contenedor se puede integrar y correlacionar con telemetría de la aplicación. Utilice un único recurso de Application Insights para todos los componentes de saludo de la aplicación. 

![Asignación de aplicaciones de varios componentes](./media/app-insights-monitor-multi-role-apps/app-map.png)

Usamos 'componente' toomean aquí cualquier parte en funcionamiento de una aplicación grande. Por ejemplo, una aplicación empresarial típico puede constar de código de cliente que se ejecuta en los exploradores web, hablando tooone o más servicios de aplicaciones web, que a su vez utilizan volver terminar los servicios. Componentes de servidor pueden hospedarse de forma local en la nube de hello, o pueden ser roles web y trabajador de Azure o se pueden ejecutar en contenedores, como Docker o Service Fabric. 

### <a name="sharing-a-single-application-insights-resource"></a>Uso compartido de un único recurso de Application Insights 

Hello técnica clave aquí es toosend telemetría de todos los componentes de la aplicación toohello mismo recurso de Application Insights, pero use hello `cloud_RoleName` componentes toodistinguish de propiedad cuando sea necesario. Hola Application Insights SDK agrega hello `cloud_RoleName` emiten componentes de telemetría de toohello de propiedad. Por ejemplo, hello SDK agregará un nombre del sitio web o toohello de nombre de rol de servicio `cloud_RoleName` propiedad. Puede invalidar este valor con un valor de telemetryinitializer. Hola asignación de la aplicación usa hello `cloud_RoleName` componentes de propiedad tooidentify hello en el mapa de Hola.

Para obtener más información acerca de cómo invalidar hello `cloud_RoleName` propiedad vea [agregar propiedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

En algunos casos, esto puede no ser adecuado y, quizás prefiera toouse recursos independientes para distintos grupos de componentes. Por ejemplo, podría necesitar toouse distintos recursos para administración o con fines de facturación. Uso de recursos independientes significa que no vea todos los componentes de hello mostrados en una sola asignación de aplicación; y que no se pueden consultar a través de los componentes de [análisis](app-insights-analytics.md). También tiene tooset recursos independientes Hola.

Con dicha advertencia, supondremos en rest Hola de este documento que desea que los datos de toosend de varios componentes tooone recursos de Application Insights.

## <a name="configure-multi-component-applications"></a>Configuración de aplicaciones de varios componentes

asignar una aplicación de varios componente de tooget, deberá tooachieve estos objetivos:

* **Instalar la versión preliminar más reciente de hello** paquete de Application Insights en cada componente de aplicación Hola. 
* **Compartir un único recurso de Application Insights** de Hola a todos los componentes de la aplicación.
* **Habilitar asignación de la aplicación de varios roles** en la hoja de las vistas previas de Hola.

Configure cada componente de la aplicación utilizando el método adecuado de Hola para su tipo. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) o [JavaScript](app-insights-javascript.md)).

### <a name="1-install-hello-latest-pre-release-package"></a>1. Instalar paquete de versión preliminar más reciente de Hola

Actualizar o instalar paquetes de saludo visión correspondientes en el proyecto de Hola para cada componente del servidor. Si usa Visual Studio:

1. Haga clic con el botón derecho en un proyecto y seleccione **Administrar paquetes NuGet**. 
2. Seleccione **Incluir versión preliminar**.
3. Si los paquetes de Application Insights aparecen en Actualizaciones, selecciónelos. 

    En caso contrario, buscar e instalar el paquete adecuado de hello:
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric: para aquellos componentes que se ejecutan como archivos ejecutables invitados y contenedores de Docker que se ejecutan en una aplicación de Service Fabric
    * Microsoft.ApplicationInsights.ServiceFabric.Native: para instancias de Reliable Services en las aplicaciones de Service Fabric
    * Microsoft.ApplicationInsights.Kubernetes: para componentes que se ejecutan en Docker en Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Uso compartido de un único recurso de Application Insights

* En Visual Studio, haga clic con el botón derecho en un proyecto y elija **Configurar Application Insights** o **Application Insights > Configurar**. Para el primer proyecto hello, utilice Hola Asistente toocreate un recurso de Application Insights. Para los proyectos posteriores, seleccione Hola mismo recurso.
* Si no hay ningún menú Application Insights, configúrelo manualmente:

   1. En [portal de Azure](https://portal,azure.com), abra el recurso de Application Insights de Hola que ya creado para otro componente.
   2. En hoja de información general de hello, pestaña abierta Hola desplegable Essentials y Hola copia **clave de instrumentación.**
   3. En el proyecto, abra ApplicationInsights.config e inserte: `<InstrumentationKey>your copied key</InstrumentationKey>`

![Copiar el archivo .config de hello Instrumental toohello clave](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Habilitación de Asignación de aplicaciones de varios roles

Hola portal de Azure, abra el recurso de hello para la aplicación. En la hoja de las vistas previas de hello, habilitar *asignación de la aplicación de varios roles*.

### <a name="4-enable-docker-metrics-optional"></a>4. Habilitación de las métricas de Docker (opcional) 

Si un componente se ejecuta en una Docker hospedada en una VM de Windows Azure, puede recopilar métricas adicionales de contenedor de Hola. Inserte esto en el archivo de configuración de [Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md):

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Usar cloud_RoleName tooseparate componentes

Hola `cloud_RoleName` propiedad es telemetría tooall adjunto. Identifica el componente de hello - Hola rol o servicio - que se origina la telemetría de Hola. (Es no Hola igual como cloud_RoleInstance, que separa idénticos roles que se ejecutan en paralelo en varios procesos de servidor o equipos).

En el portal de hello, puede filtrar o segmentar la telemetría de uso de esta propiedad. En este ejemplo, hoja de errores de hello es tooshow filtrado sólo la información del servicio de front-end web de hello, filtrando los errores de back-end de hello API de CRM:

![Gráfico de métricas segmentadas por Nombre del rol en la nube](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Seguimiento de operaciones entre componentes

Puede realizar un seguimiento de un componente tooanother, llamadas de hello realizadas durante el procesamiento de una operación individual.


![Mostrar telemetría para la operación](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Haga clic en tooa lista correlacionados de telemetría para realizar esta operación en el servidor de web front-end de Hola y Hola API de back-end:

![Búsqueda entre componentes](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Pasos siguientes

* [Separación de telemetría de desarrollo, prueba y producción](app-insights-separate-resources.md)
