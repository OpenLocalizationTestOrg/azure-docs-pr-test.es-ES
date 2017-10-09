---
title: "las aplicaciones de Docker de aaaMonitor de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Excepciones, eventos y contadores de rendimiento de docker se pueden mostrar en la información de la aplicación, junto con la telemetría de Hola desde aplicaciones de hello en contenedores."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Supervisar aplicaciones Docker en Application Insights
Los eventos de ciclo de vida y los contadores de rendimiento de los contenedores [Docker](https://www.docker.com/) pueden mostrarse en gráficos en Application Insights. Instalar hello [Application Insights](app-insights-overview.md) imagen en un contenedor en el host y mostrará los contadores de rendimiento para el host de hello, como así como para Hola otras imágenes.

Con Docker, distribuye sus aplicaciones en contenedores ligeros junto con todas las dependencias. Estos contenedores se ejecutan en cualquier equipo host que ejecute un motor Docker.

Cuando ejecute hello [imagen de Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) en el host Docker, obtener estas ventajas:

* Ciclo de vida telemetría acerca de todos los contenedores de Hola que se ejecutan en el host de hello - iniciar, detener y así sucesivamente.
* Contadores de rendimiento para todos los contenedores de Hola. CPU, memoria, uso de red y mucho más.
* Si se [instalado Application Insights SDK para Java](app-insights-java-live.md) en hello aplicaciones que se ejecutan en contenedores de hello, todos los telemetría Hola de esas aplicaciones tendrán propiedades adicionales que identifica el contenedor de Hola y el equipo host. De esta forma, si tiene, por ejemplo, instancias de una aplicación que se ejecuta en más de un host, podrá filtrar fácilmente los datos de telemetría de la aplicación en función del host.

![ejemplo](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Configurar el recurso de Application Insights
1. Iniciar sesión en [portal de Microsoft Azure](https://azure.com) y abra el recurso de Application Insights de hello para la aplicación; o [crear una nueva](app-insights-create-new-resource.md). 
   
    *¿Qué recurso debería usar?* Si se desarrollaron hello las aplicaciones que se ejecutan en el host por otra persona, deberá demasiado[crear un nuevo recurso de Application Insights](app-insights-create-new-resource.md). Esto es donde ver y analizar la telemetría de Hola. (Seleccione "General" para el tipo de aplicación Hola).
   
    Pero si es desarrollador de Hola de las aplicaciones de hello, a continuación, esperamos [agrega Application Insights SDK](app-insights-java-live.md) tooeach de ellos. Si son todos los componentes realmente de una aplicación de negocio individual, a continuación, puede configurar todas ellas toosend telemetría tooone recurso y usará ese mismo recursos toodisplay hello Docker ciclo de vida de datos y rendimiento. 
   
    En un tercer escenario es que se ha desarrollado la mayoría de las aplicaciones de hello, pero que usa recursos separados toodisplay su telemetría. En ese caso, probablemente también desee toocreate recursos independientes para hello datos de Docker. 
2. Agregar icono de Docker de hello: elija **agregar icono**, arrastre el icono de Docker de Hola de galería de Hola y, a continuación, haga clic en **realiza**. 
   
    ![ejemplo](./media/app-insights-docker/03.png)
3. Haga clic en hello **Essentials** desplegable y copie Hola clave de instrumentación. Utilice este hello tootell SDK donde toosend su telemetría.

    ![ejemplo](./media/app-insights-docker/02-props.png)

Mantener esa ventana del explorador práctica, tal y como le vuelva tooit pronto toolook en la telemetría.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Ejecutar el monitor de Application Insights de hello en el host
Ahora que tienes en algún lugar telemetría de hello toodisplay, puede configurar aplicación en contenedores de hello que recopilará y enviará.

1. Conectar el host de Docker de tooyour. 
2. Edite la clave de instrumentación de este comando y después ejecútelo:
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Solo es necesaria una imagen de Application Insights por cada host de Docker. Si la aplicación se implementa en varios hosts de Docker, a continuación, repita el comando de hello en todos los hosts.

## <a name="update-your-app"></a>Actualización de la aplicación
Si la aplicación se ha instrumentado con hello [Application Insights SDK para Java](app-insights-java-get-started.md), agregar Hola siguen en archivo de ApplicationInsights.xml hello en el proyecto, bajo hello `<TelemetryInitializers>` elemento:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Esto agrega información de Docker como contenedor y el host identificador tooevery telemetría item enviado desde su aplicación.

## <a name="view-your-telemetry"></a>Visualización de la telemetría
Volver atrás tooyour recursos de Application Insights en hello portal de Azure.

Haga clic en icono de Docker Hola.

En breve, verá los datos que llegan desde la aplicación de Docker de hello, especialmente si tiene otros contenedores que se ejecutan en el motor de Docker.

Estas son algunas de las vistas de Hola que puedas.

### <a name="perf-counters-by-host-activity-by-image"></a>Contadores de rendimiento por host, actividad por imagen
![ejemplo](./media/app-insights-docker/10.png)

![ejemplo](./media/app-insights-docker/11.png)

Haga clic en cualquier host o imagen para obtener más detalles.

vista de hello toocustomize, haga clic en cualquier gráfico, el encabezado de cuadrícula de Hola o utilizar Agregar gráfico. 

[Más información sobre el explorador de métricas](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>Eventos de contenedor Docker
![ejemplo](./media/app-insights-docker/13.png)

tooinvestigate eventos individuales, haga clic en [búsqueda](app-insights-diagnostic-search.md). Buscar y filtrar los eventos de hello toofind que desee. Haga clic en cualquier evento tooget más detalle.

### <a name="exceptions-by-container-name"></a>Excepciones por el nombre del contenedor
![ejemplo](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>El contexto del docker agrega tooapp telemetría
Telemetría de solicitud enviado desde la aplicación hello instrumentado con SDK AI, enriquecido con contexto de Docker:

![ejemplo](./media/app-insights-docker/16.png)

Contadores de rendimiento de tiempo de procesador y memoria disponible, enriquecidos y agrupados según el nombre del contenedor de Docker:

![ejemplo](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Preguntas y respuestas
*¿Qué me da Application Insights que no me dé Docker?*

* Desglose detallado de los contadores de rendimiento por contenedor e imagen.
* Integración de datos de contenedores y aplicaciones en un panel.
* [Exportar telemetría](app-insights-export-telemetry.md) para otra base de datos de analysis tooa, Power BI u otro panel.

*¿Cómo consigo telemetría de la propia aplicación Hola?*

* Instalar Hola Application Insights SDK en la aplicación hello. Más información sobre: [aplicaciones web de Java](app-insights-java-get-started.md) y [aplicaciones web de Windows](app-insights-asp-net.md).

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Pasos siguientes

* [Application Insights para Java](app-insights-java-get-started.md)
* [Application Insights para Node.js](app-insights-nodejs.md)
* [Application Insights para ASP.NET](app-insights-asp-net.md)
