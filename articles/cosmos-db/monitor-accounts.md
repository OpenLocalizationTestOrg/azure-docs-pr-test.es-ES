---
title: base de datos de Azure Cosmos aaaMonitor solicitudes y almacenamiento | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor cuenta de la base de datos de Azure Cosmos para las métricas de rendimiento, como las solicitudes y errores de servidor y las métricas de uso, como el consumo de almacenamiento."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Supervisión de las solicitudes, uso y almacenamiento de Azure Cosmos DB
Puede supervisar sus cuentas de base de datos de Azure Cosmos en hello [portal de Azure](https://portal.azure.com/). Para cada cuenta de Azure Cosmos DB, existen métricas de rendimiento, como solicitudes y errores de servidor, y métricas de uso, como consumo de almacenamiento.

Las métricas pueden revisarse en la hoja de cuenta de hello, hoja de métricas nueva hello, o en el Monitor de Azure.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Visualice las métricas de rendimiento en la hoja de métricas de Hola
1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **más servicios**, desplácese demasiado**bases de datos**, haga clic en **base de datos de Azure Cosmos**y, a continuación, haga clic en nombre de Hola Hola Cuenta de Azure DB Cosmos para el que desea que las métricas de rendimiento de tooview.
2. En el menú de recursos de hello, en **supervisión**, haga clic en **métricas**.

se abre la hoja de métricas de Hola y puede seleccionar Hola colección tooreview. Puede revisar las métricas de disponibilidad, las solicitudes, el rendimiento y almacenamiento y compararlas toohello Azure Cosmos DB SLA.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Visualice las métricas de rendimiento mediante el uso de supervisión de Azure
1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **Monitor** en hello Jumpbar.
2. En el menú de recursos de hello, haga clic en **métricas**.
3. Hola **Monitor - métricas** ventana, en hello **ecurso grupo** menú desplegable, el grupo de recursos de hello seleccione asociado con la cuenta de base de datos de Azure Cosmos Hola que desearía toomonitor. 
4. Hola **recursos** menú desplegable, toomonitor de cuenta de base de datos de hello select.
5. En la lista de Hola de **métricas disponibles**, seleccione Hola métricas toodisplay. Utilice Hola CTRL botón selección de toomulti. 

    Las métricas se muestran en Hola **trazar** ventana. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Visualice las métricas de rendimiento en la hoja de la cuenta de hello
1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **más servicios**, desplácese demasiado**bases de datos**, haga clic en **base de datos de Azure Cosmos**y, a continuación, haga clic en nombre de Hola Hola Cuenta de Azure DB Cosmos para el que desea que las métricas de rendimiento de tooview.
2. Hola **supervisión** lente muestra hello siguiendo los iconos de forma predeterminada:
   
   * Número total de solicitudes Hola día actual.
   * Almacenamiento utilizado.
   
   Si la tabla se muestran **no hay datos disponibles** y cree que hay datos en la base de datos, vea hello [solución de problemas](#troubleshooting) sección.
   
   ![Captura de pantalla de la lente de supervisión de Hola que muestra las solicitudes de Hola y el uso de almacenamiento Hola](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Al hacer clic en hello **solicitudes** o **cuota de uso** icono abre una detallada **métrica** hoja.
4. Hola **métrica** hoja muestra los detalles acerca de las métricas de Hola que seleccionó.  En hello parte superior de la hoja de hello es un gráfico de solicitudes representan gráficamente cada hora y a continuación que es la tabla que muestra los valores de agregación para las solicitudes limitadas y total.  Hello hoja de métricas también muestra hello lista de alertas que han sido toohello definido y filtrado métricas que aparecen en la hoja de métricas de hello actual (de este modo, si tiene un número de alertas, sólo verá hello las relevantes proporcionadas en esta guía).   
   
   ![Captura de pantalla de hoja de métricas de Hola que incluye limitar las solicitudes](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Personalizar vistas de métrica de rendimiento en el portal de Hola
1. métricas de hello toocustomize que mostrar en un gráfico en concreto, haga clic en tooopen de gráfico de hello en hello **métrica** hoja y, a continuación, haga clic en **Editar gráfico**.  
   ![Captura de pantalla de controles de hoja de métricas de hello, con Editar gráfico resaltado](./media/monitor-accounts/madocdb3.png)
2. En hello **Editar gráfico** hoja, hay opciones toomodify Hola métricas que se muestran en el gráfico de hello, así como su intervalo de tiempo.  
   ![Captura de pantalla de hoja de hello Editar gráfico](./media/monitor-accounts/madocdb4.png)
3. métricas de hello toochange mostradas en la parte de hello, simplemente seleccione o desactive las métricas de rendimiento disponibles de hello y, a continuación, haga clic en **Aceptar** final Hola de hoja de Hola.  
4. Hola toochange el intervalo de tiempo, elija un intervalo diferente (por ejemplo, **personalizado**) y, a continuación, haga clic en **Aceptar** final Hola de hoja de Hola.  
   
   ![Captura de pantalla de parte del intervalo de tiempo de Hola de muestra de Hola Editar gráfico hoja cómo tooenter un intervalo de tiempo personalizado](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Crear gráficos en paralelo en el portal de Hola
Hola Portal de Azure permite gráficos de métricas de toocreate en paralelo.  

1. En primer lugar, haga doble clic en el gráfico de Hola que desee toocopy y seleccione **personalizar**.
   
   ![Captura de pantalla de gráfico de hello Nº Total de solicitudes con la opción de personalizar Hola resaltado](./media/monitor-accounts/madocdb6.png)
2. Haga clic en **clon** Hola parte de hello toocopy de menú y, a continuación, haga clic en **realiza personalizar**.
   
   ![Pantalla captura del gráfico de número Total de solicitudes de hello con hello clon y terminado personalizar las opciones de resaltado](./media/monitor-accounts/madocdb7.png)  

Ahora puede tratar esta parte como cualquier otra parte métrica, personalizar el rango de métricas y la hora de hello mostrado en la parte de Hola.  Al hacerlo, puede ver dos métricas diferentes gráfico side-by-side en hello mismo tiempo.  
    ![Captura de pantalla de gráfico del número Total de solicitudes de Hola y Hola nuevo nº Total de solicitudes más allá del gráfico de hora](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Configurar alertas en el portal de Hola
1. Hola [portal de Azure](https://portal.azure.com/), haga clic en **más servicios**, haga clic en **base de datos de Azure Cosmos**y, a continuación, haga clic en hello nombre de cuenta de base de datos de Azure Cosmos hello para el que le gustaría toosetup alertas de métrica de rendimiento.
2. En el menú de recursos de hello, haga clic en **reglas de alerta** hoja de tooopen hello las reglas de alerta.  
   ![Una parte seleccionada de reglas de captura de pantalla de hello alerta](./media/monitor-accounts/madocdb10.5.png)
3. Hola **reglas de alerta** hoja, haga clic en **Agregar alerta**.  
   ![Captura de pantalla de hoja de las reglas de alerta de hello, con el botón Agregar alerta Hola resaltado](./media/monitor-accounts/madocdb11.png)
4. Hola **agregar una regla de alerta** hoja, especifique:
   
   * nombre de Hola de regla de alerta de saludo que está configurando.
   * Una descripción de la nueva regla de alerta de Hola.
   * Hola métrica para la regla de alerta de Hola.
   * condición de Hello, umbral y el período que determinan si activa la alerta Hola. Por ejemplo, un error del servidor número superior a 5 sobre Hola últimos 15 minutos.
   * Si el administrador del servicio de Hola y coadministrators reciben un correo electrónico cuando se desencadene la alerta de Hola.
   * Direcciones de correo electrónico adicionales para las notificaciones de alerta.  
     ![Captura de pantalla de hello agrega una hoja de regla de alerta](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Supervisión de Azure Cosmos DB mediante programación
Hola métricas de nivel de cuenta disponibles en el portal de hello, como el uso de almacenamiento de información de cuenta y Nº total de solicitudes, no están disponibles a través de hello DocumentDB APIs. Sin embargo, puede recuperar datos de uso en el nivel de colección de hello mediante hello DocumentDB APIs. datos de nivel de colección tooretrieve Hola siguientes:

* Hola toouse API de REST, [realiza una operación GET en la colección de hello](https://msdn.microsoft.com/library/mt489073.aspx). se devuelve información de cuota y uso de Hello para la recopilación de hello en los encabezados x-ms-resource-quota y x-ms-resource-usage Hola en respuesta de Hola.
* Hola toouse .NET SDK, use hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) método, que devuelve un [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) que contiene un número de propiedades de uso como  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**y mucho más.

tooaccess otras métricas, usar hello [Azure SDK del Monitor](https://www.nuget.org/packages/Microsoft.Azure.Insights). Se pueden recuperar definiciones de métricas mediante la llamada a:

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Las consultas tooretrieve métricas individuales uso Hola siguiendo el formato:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Para obtener más información, consulte [recuperar las métricas de recursos a través de la API de REST de Azure Monitor hello](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Tenga en cuenta que se ha cambiado el nombre "Azure Inights" a "Azure Monitor".  Esta entrada de blog refiere toohello anterior nombre.

## <a name="troubleshooting"></a>Solución de problemas
Si la supervisión iconos mostrar hello **no hay datos disponibles** mensaje y recientemente enviado solicitudes o agregar base de datos de toohello de datos, puede editar Hola mosaico tooreflect Hola el uso reciente.

### <a name="edit-a-tile-toorefresh-current-data"></a>Editar los datos mosaico toorefresh actual
1. métricas de hello toocustomize que mostrarán en un elemento determinado, haga clic en Hola de hello gráfico tooopen **métrica** hoja y, a continuación, haga clic en **Editar gráfico**.  
   ![Captura de pantalla de controles de hoja de métricas de hello, con Editar gráfico resaltado](./media/monitor-accounts/madocdb3.png)
2. En hello **Editar gráfico** hoja en hello **intervalo de tiempo** sección, haga clic en **pasada hora**y, a continuación, haga clic en **Aceptar**.  
   ![Captura de pantalla de hoja de hello Editar gráfico con la última hora seleccionada](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. El icono debería actualizarse y mostrar los datos y el uso actuales.  
   ![Captura de pantalla de hello actualizado Total de solicitudes más allá de mosaico de hora](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la base de datos de Azure Cosmos planear la capacidad, vea hello [Calculadora de planificador de capacidad de base de datos de Azure Cosmos](https://www.documentdb.com/capacityplanner).

