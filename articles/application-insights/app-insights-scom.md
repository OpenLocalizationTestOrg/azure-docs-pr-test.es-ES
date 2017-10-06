---
title: "integración de aaaSCOM con Application Insights | Documentos de Microsoft"
description: "Si es usuario de SCOM, supervise el rendimiento y diagnostique problemas con Application Insights. Paneles integrales, alertas inteligentes, eficaces herramientas de diagnóstico y consultas de análisis."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Supervisión del rendimiento de la aplicación con Application Insights para SCOM
Si usa System Center Operations Manager (SCOM) toomanage los servidores, puede supervisar el rendimiento y diagnosticar problemas de rendimiento con la Ayuda de Hola de [Azure Application Insights](app-insights-asp-net.md). Application Insights supervisa solicitudes entrantes de la aplicación web, llamadas SQL y REST salientes, excepciones y seguimientos de registros. Proporciona paneles con gráficos de métricas y alertas inteligentes, así como una eficaz búsqueda de diagnóstico y consultas analíticas sobre esta telemetría. 

Puede activar la supervisión de Application Insights mediante un módulo de administración de SCOM.

## <a name="before-you-start"></a>Antes de comenzar
Condiciones:

* Está familiarizado con SCOM y uso de SCOM 2012 R2 o toomanage 2016 IIS servidores web.
* Ya ha instalado en los servidores de una aplicación web que desea que toomonitor con Application Insights.
* La versión de framework de la aplicación es .NET 4.5 o posterior.
* Tener acceso tooa suscripción en [Microsoft Azure](https://azure.com) y puede iniciar sesión en toohello [portal de Azure](https://portal.azure.com). Su organización puede tener una suscripción y puede agregar su tooit de cuenta de Microsoft.

(equipo de desarrollo de hello podría aumentar hello [Application Insights SDK](app-insights-asp-net.md) en la aplicación web de hello. Esta instrumentación en tiempo de compilación les proporciona mayor flexibilidad al escribir una telemetría personalizada. Sin embargo, no importa: puede seguir los pasos de hello descritos aquí con o sin Hola SDK integrado.)

## <a name="one-time-install-application-insights-management-pack"></a>(Una vez) Instalación del módulo de administración de Application Insights
En el equipo de Hola donde se ejecuta Operations Manager:

1. Desinstale cualquier versión anterior del módulo de administración de hello:
   1. En Operations Manager, abra Administración, Módulos de administración. 
   2. Eliminar la versión anterior de Hola.
2. Descargue e instale el módulo de administración de Hola desde el catálogo de Hola.
3. Reinicie Operations Manager.

## <a name="create-a-management-pack"></a>Creación de un módulo de administración
1. En Operations Manager, abra **Creación**, **.NET... con Application Insights**, **Asistente para agregar monitores** y vuelva a elegir **.NET... con Application Insights**.
   
    ![](./media/app-insights-scom/020.png)
2. Configuración de hello nombre después de la aplicación. (Tiene tooinstrument una aplicación en un momento.)
   
    ![](./media/app-insights-scom/030.png)
3. En Hola misma página del asistente, cree una nueva administración de módulo, o seleccione un paquete que creó anteriormente para Application Insights.
   
     (Hola Application Insights [módulo de administración](https://technet.microsoft.com/library/cc974491.aspx) es una plantilla, desde el que se crea una instancia. Puede reutilizar Hola misma instancia posteriormente.)

    ![En la ficha Propiedades generales de hello, escriba el nombre de Hola de aplicación hello. Haga clic en Nuevo y escriba un nombre para un módulo de administración. Haga clic en Aceptar y, luego, en Crear.](./media/app-insights-scom/040.png)

1. Elija una aplicación que desea toomonitor. característica de búsqueda de Hello busca entre aplicaciones instaladas en los servidores.
   
    ![En la ficha tooMonitor, haga clic en Agregar, escriba parte del nombre de la aplicación hello, haga clic en Buscar, elija aplicación hello y, a continuación, agregar, en Aceptar.](./media/app-insights-scom/050.png)
   
    campo de ámbito de supervisión opcional Hola puede ser usado toospecify un subconjunto de los servidores, si no desea toomonitor Hola aplicación en todos los servidores.
2. En la siguiente página del asistente hello, primero debe proporcionar su toosign de credenciales en tooMicrosoft Azure.
   
    En esta página, elija recursos de Application Insights Hola donde desea toobe de datos de telemetría de hello analiza y muestra. 
   
   * Si la aplicación hello se configuró para Application Insights durante el desarrollo, seleccione el recurso existente.
   * En caso contrario, cree un nuevo recurso con el nombre de la aplicación hello. Si no hay otras aplicaciones que son componentes de hello mismo sistema, colóquelos en hello mismo grupo de recursos, toomake acceso toohello telemetría más fácil toomanage.
     
     Puede cambiar estas opciones aquí.
     
     ![En la pestaña de configuración de Application Insights, haga clic en 'Iniciar sesión' y proporcione las credenciales de la cuenta de Microsoft para Azure. A continuación, elija una suscripción, el grupo de recursos y el recurso.](./media/app-insights-scom/060.png)
3. Asistente de hello completa.
   
    ![Click Create](./media/app-insights-scom/070.png)

Repita este procedimiento para cada aplicación que desea que se toomonitor.

Si necesita una configuración toochange más adelante, vuelva a abrir propiedades de Hola de hello supervisar desde la ventana de creación de hello.

![En Creación, seleccione .NET Application Performance Monitoring (Supervisión del rendimiento de la aplicación de .NET) con Application Insights, seleccione al monitor y haga clic en Propiedades.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Comprobación de la supervisión
monitor de Hola que ha instalado busca la aplicación en todos los servidores. Donde encuentra la aplicación hello, que configura la aplicación hello de Monitor de estado de aplicación visión toomonitor. Si es necesario, instala primero el Monitor de estado en el servidor de Hola.

También puede comprobar qué instancias de aplicación hello que ha encontrado:

![En Supervisión, abra Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Visualización de la telemetría en Application Insights
Hola [portal de Azure](https://portal.azure.com), examinar toohello recursos de la aplicación. [Verá gráficos que muestran la telemetría](app-insights-dashboards.md) de su aplicación. (Si lo no ha aparecido en la página principal de hello todavía, haga clic en secuencia en directo de métricas).

## <a name="next-steps"></a>Pasos siguientes
* [Configurar un panel](app-insights-dashboards.md) gráficos más importantes de toobring Hola juntos esta y otras aplicaciones de supervisión.
* [Más información sobre las métricas](app-insights-metrics-explorer.md)
* [Configuración de alertas](app-insights-alerts.md)
* [Diagnóstico de problemas de rendimiento](app-insights-detect-triage-diagnose.md)
* [Consultas de Analytics eficaces](app-insights-analytics.md)
* [Pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md)

