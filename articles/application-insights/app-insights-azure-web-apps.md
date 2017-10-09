---
title: "aaaMonitor rendimiento de la aplicación web de Azure | Documentos de Microsoft"
description: "Supervisión del rendimiento de Azure Web Apps. Carga y tiempo de respuesta de gráfico, información de dependencia y establecer alertas en el rendimiento."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Supervisión del rendimiento de Azure Web Apps
Hola [Portal de Azure](https://portal.azure.com) puede configurar la supervisión de rendimiento de aplicaciones para su [aplicaciones web de Azure](../app-service-web/app-service-web-overview.md). [Azure Application Insights](app-insights-overview.md) instrumenta la telemetría de aplicación toosend acerca de su servicio de Application Insights, donde se almacena y analiza toohello de actividades. Allí, los gráficos de métricas y herramientas de búsqueda se pueden usar toohelp diagnosticar problemas, mejorar el rendimiento y evaluar el uso.

## <a name="run-time-or-build-time"></a>Tiempo de ejecución o de compilación
Puede configurar la supervisión mediante la instrumentación de la aplicación hello en cualquiera de estas dos maneras:

* **Tiempo de ejecución**: puede seleccionar una extensión de supervisión de rendimiento cuando la aplicación web ya esté activa. No es necesario toorebuild o volver a instalar la aplicación. Tendrá a disposición un conjunto estándar de paquetes que supervisan tiempos de respuesta, tasas de éxito, excepciones, dependencias, etc. 
* **Tiempo de compilación** : puede instalar un paquete en la aplicación que esté en desarrollo. Esta opción es más versátil. En suma toohello mismos paquetes estándares, puede escribir telemetría de código toocustomize Hola o toosend su propia telemetría. Puede registrar eventos de registro según la semántica de toohello de su dominio de aplicación o actividades específicas. 

## <a name="run-time-instrumentation-with-application-insights"></a>Instrumentación del tiempo de ejecución con Application Insights
Si ya está ejecutando una aplicación web en Azure, ya goza de cierta supervisión: tasas de solicitudes y errores. Agregar Application Insights tooget más, como tiempos de respuesta, supervisión toodependencies de llamadas, detección inteligente y eficaz lenguaje de consulta de análisis de registros Hola. 

1. **Seleccionar Application Insights** hello Azure panel de control de la aplicación web.
   
    ![En Supervisión, elija Application Insights.](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Elija toocreate un nuevo recurso, a menos que ya ha configurado un recurso de Application Insights para esta aplicación por otra ruta.
2. **Instrumente la aplicación web** después de haber instalado Application Insights. 
   
    ![Instrumentación de la aplicación web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   **Habilite la supervisión de cliente** para la vista de página y la telemetría de usuario.

   * Seleccione Configuración > Configuración de la aplicación.
   * En Configuración de la aplicación, agregue un nuevo par clave-valor: 
   
    Clave: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valor: `true`
   * **Guardar** Hola configuración y **reiniciar** la aplicación.
3. **Supervise la aplicación**.  [Datos de hello Expore](#explore-the-data).

Más adelante, si lo desea puede incorporar aplicación hello con Application Insights.

*¿Cómo quitar Application Insights, o cambiar toosending tooanother recursos?*

* En Azure, hoja de control de la aplicación de web Hola abierto y en las herramientas de desarrollo, abra **extensiones**. Eliminar la extensión de Application Insights de Hola. A continuación, en supervisión, elija Application Insights y cree o seleccione recurso Hola que desee.

## <a name="build-hello-app-with-application-insights"></a>Compilar la aplicación hello con Application Insights
Application Insights puede proporcionar una telemetría más detallada instalando un SDK en la aplicación. En concreto, puede recopilar registros de seguimiento, [escribir telemetría personalizada](app-insights-api-custom-events-metrics.md), y obtener informes de excepción más detallados.

1. **En Visual Studio** (2013 Update 2 o posterior), configure Application Insights para el proyecto.

    Haga clic en proyecto de web de Hola y seleccione **Agregar > Application Insights** o **configurar Application Insights**.
   
    ![Haga clic en proyecto de web de Hola y elija Agregar o configurar Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    Si se le pregunta toosign en, usar credenciales de Hola para su cuenta de Azure.
   
    operación de Hello tiene dos efectos:
   
   1. Crea un recurso de Application Insights en Azure, donde se almacenan, analizan y muestran los datos de telemetría.
   2. Hola código del tooyour del paquete de NuGet de visión de aplicación (si no está allí ya), se agrega y configura toosend telemetría toohello recursos de Azure.
2. **Probar la telemetría de hello** por aplicación hello en ejecución en el equipo de desarrollo (F5).
3. **Publicar la aplicación hello** tooAzure Hola forma habitual. 

*¿Cómo se puede cambiar el recurso de Application Insights toosending tooa diferente?*

* En Visual Studio, proyecto de hello del menú contextual, elija **configurar Application Insights** y elija el recurso de Hola que desee. Obtener Hola opción toocreate un nuevo recurso. Vuelva a compilar e implementar.

## <a name="explore-hello-data"></a>Explorar datos Hola
1. En la hoja de Application Insights Hola de su panel de control de aplicación web, vea las métricas en vivo, que muestra las solicitudes y errores dentro de un segundo o dos de ellos que se producen. Esta información es muy útil cuando se vuelve a publicar la aplicación ya que permite ver inmediatamente cualquier problema.
2. Desplazarse por los recursos de Application Insights completo toohello.

    ![Hacer clic en las distintas opciones](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    También puede ir allí directamente desde la exploración de recursos de Azure.

1. Haga clic en cualquier tooget gráfico más detalle:
   
    ![En la hoja de información general de Application Insights de hello, haga clic en un gráfico](./media/app-insights-azure-web-apps/07-dependency.png)
   
    También puede [personalizar las hojas de métricas](app-insights-metrics-explorer.md).
2. Haga clic en más toosee los eventos individuales y sus propiedades:
   
    ![Haga clic en un tooopen del tipo de evento filtra una búsqueda en ese tipo](./media/app-insights-azure-web-apps/08-requests.png)
   
    Tenga en cuenta Hola "..." vínculo tooopen todas las propiedades.
   
    También puede [personalizar las búsquedas](app-insights-diagnostic-search.md).

Para realizar búsquedas más eficaces a través de la telemetría, usar hello [lenguaje de consulta de análisis de registros](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Más telemetría

* [Datos de carga de página web](app-insights-javascript.md)
* [Telemetría personalizada](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Pasos siguientes
* [Ejecutar el analizador de hello en la aplicación activa](app-insights-profiler.md).
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample): supervisar Azure Functions con Application Insights
* [Habilitar diagnósticos de Azure](app-insights-azure-diagnostics.md) tooApplication toobe enviado información.
* [Supervisar las métricas de mantenimiento de servicio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.
* [Reciba notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) cada vez que se produzcan eventos de operaciones o las métricas traspasen un umbral.
* Use [Application Insights para las aplicaciones de JavaScript y páginas web](app-insights-javascript.md) tooget telemetría de cliente de exploradores de Hola que visite una página web.
* [Configurar las pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md) toobe una alerta si el sitio está inactivo.

