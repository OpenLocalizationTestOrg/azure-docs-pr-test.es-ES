---
title: aaaExport tooPower BI de Application Insights | Documentos de Microsoft
description: Las consultas de Analytics se pueden mostrar en Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Alimentación de Power BI desde Application Insights
[Power BI](http://www.powerbi.com/) es un conjunto de herramientas de análisis de negocios que pueden ayudar a analizar datos y compartir conocimientos. Cada dispositivo cuenta con paneles que incluyen gran cantidad de datos. Puede combinar datos de varios orígenes, incluidas las consultas de Analytics en [Azure Application Insights](app-insights-overview.md).

Hay tres métodos recomendados para exportar datos de Application Insights tooPower BI. Se pueden utilizar por separado o conjuntamente.

* [**Adaptador de Power BI**](#power-pi-adapter): configure un panel completo de telemetría desde la aplicación. depende del conjunto de Hola de gráficos, pero puede agregar sus propias consultas de cualquier otro origen.
* [**Exportar las consultas de análisis** ](#export-analytics-queries) -escribir ni una sola consulta que desee usar análisis y exportarlo tooPower BI. Puede colocar esta consulta en un panel junto con otros datos.
* [**Exportación continua y análisis de transmisiones** ](app-insights-export-stream-analytics.md) -esto implica tooset de trabajo más seguridad. Resulta útil si desea que tookeep los datos durante largos períodos. En caso contrario, hello otros métodos son recomendables.

## <a name="power-bi-adapter"></a>Adaptador de Power BI
Este método crea un panel completo de telemetría. depende del conjunto de datos inicial de Hello, pero puede agregar más tooit de datos.

### <a name="get-hello-adapter"></a>Obtiene el adaptador de Hola
1. Inicie sesión en demasiado[Power BI](https://app.powerbi.com/).
2. Abra **Obtener datos**, **Servicios**, **Application Insights**
   
    ![Obtención de un origen de datos de Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Proporcione detalles de Hola de su recurso de Application Insights.
   
    ![Obtención de un origen de datos de Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Espere un minuto o dos para hello toobe de datos importado.
   
    ![Adaptador de Power BI](./media/app-insights-export-power-bi/010.png)

Se puede modificar el panel de hello, combinar gráficos de Application Insights Hola con los de otros orígenes y con las consultas de análisis. Tiene a su disposición una galería de visualización en la que puede obtener más gráficos; y cada gráfico tiene a su vez parámetros que puede configurar.

Después de la importación inicial de hello, panel de Hola y los informes de hello continuar tooupdate diariamente. Puede controlar la programación de actualización de hello en el conjunto de datos de Hola.

## <a name="export-analytics-queries"></a>Exportación de consultas de Analytics
Esta ruta permite toowrite cualquier análisis desea consultar y, a continuación, exportar ese panel de Power BI tooa. (Puede agregar panel toohello creada por el adaptador de hello).

### <a name="one-time-install-power-bi-desktop"></a>Una vez: instalar Power BI Desktop
tooimport su consulta Application Insights, utilice la versión de escritorio de Hola de Power BI. Pero, a continuación, puede publicar web toohello o tooyour el área de trabajo de Power BI en la nube. 

Instale [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Exportación de una consulta de Analytics
1. [Abra Analytics y escriba la consulta](app-insights-analytics-tour.md).
2. Probar y refinar la consulta de hello hasta que esté satisfecho con los resultados de Hola.

   **Asegúrese de que esa consulta Hola se ejecuta correctamente en el análisis antes de exportarla.**
3. En hello **exportar** menú, elija **Power BI (M)**. Guarde el archivo de texto hello.
   
    ![Exportación de la consulta de Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. En Power BI Desktop, seleccione **obtener datos, realice una consulta en blanco** y, a continuación, en hello editor de consultas, en **vista** seleccione **Editor de consultas avanzadas**.

    Script de lenguaje M pegar Hola exportado en Hola Editor de consultas avanzadas.

    ![Editor de consultas avanzadas](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Es posible que tenga tooprovide credenciales tooallow Power BI tooaccess Azure. Use 'cuenta profesional' toosign con su cuenta de Microsoft.
   
    ![Proporcione las credenciales de Azure tooenable Power BI toorun la consulta de Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Si necesita tooverify Hola credenciales, utilice comando de menú de configuración del origen de datos de Hola Hola Editor de consultas. Tenga cuidado las credenciales de hello toospecify que use para Azure, que podría ser diferente de las credenciales de Power BI.)
2. Elija una visualización de la consulta y seleccione campos de hello para el eje x, eje y y segmentación de dimensión.
   
    ![Seleccionar la visualización](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Publicar el área de trabajo de informes tooyour Power BI en la nube. Desde allí, puede incluir una versión sincronizada en otras páginas web.
   
    ![Seleccionar la visualización](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Actualizar informes de hello manualmente a intervalos o configurar una actualización programada en la página de opciones de Hola.

## <a name="troubleshooting"></a>Solución de problemas

### <a name="401-or-403-unauthorized"></a>401 o 403 No autorizado 
Esto puede ocurrir si no se ha actualizado su token de actualización. Pruebe estas tooensure pasos que todavía tiene acceso. Si tiene acceso y las credenciales de hello refershing no funciona, abra una incidencia de soporte técnico.

1. Inicie sesión en el Portal de Azure de Hola y asegúrese de que puede tener acceso a recursos de Hola
2. Ensaye con credenciales de hello toorefresh para hello panel

### <a name="502-bad-gateway"></a>Puerta de enlace incorrecta 502
Esto se debe normalmente a una consulta de Analytics que devuelve demasiados datos. También debe intentar usar un intervalo de tiempo más reducido o mediante el uso de hello [hace](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) o [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) solo funciones [proyecto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Hola campos necesarios.

Si reduce el conjunto de datos de hello procedentes de la consulta de análisis de hello no cumple sus requisitos debe considerar el uso de hello [API](https://dev.applicationinsights.io/documentation/overview) toopull un conjunto de datos mayor. Aquí indicamos cómo tooconvert Hola consulta M exportar toouse Hola API.

1. Cree una [clave de API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).
2. Hola actualización secuencias de comandos de Power BI M que haya exportado desde análisis reemplazando hello ARM URL con la API de AI (vea el ejemplo siguiente)
   * Reemplace **https://management.azure.com/subscriptions/...**
   * por **https://api.applicationinsights.io/beta/apps/...**
3. Por último, actualizar credenciales toobasic y usar su clave de API
  

**Script existente**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Script actualizado**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>Acerca del muestreo
Si la aplicación envía una gran cantidad de datos, característica de muestreo adaptativo de hello puede operar y enviar solamente un porcentaje de la telemetría. Hola que mismo es verdadero si ha configurado manualmente de muestreo en hello SDK o en la recopilación. [Aprenda más sobre el muestreo.](app-insights-sampling.md)


## <a name="next-steps"></a>Pasos siguientes
* [Power BI: más información](http://www.powerbi.com/learning/)
* [Tutorial de Analytics](app-insights-analytics-tour.md)

