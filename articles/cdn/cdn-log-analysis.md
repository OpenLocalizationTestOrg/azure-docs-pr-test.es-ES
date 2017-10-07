---
title: "análisis de aaaLog para red CDN de Azure | Documentos de Microsoft"
description: "Los clientes pueden habilitar el análisis de registros para la red CDN de Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Registros de diagnóstico de red CDN de Azure

Después de habilitar CDN para la aplicación, es probable que se desea el uso CDN Hola toomonitor, comprobará el estado de saludo de la entrega y solucionar posibles problemas. La red CDN de Azure proporciona estas funcionalidades con [Análisis Básico de la red CDN](cdn-analyze-usage-patterns.md) y [Registros de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>Análisis Básico de la red CDN
Como un usuario de red CDN de Azure actual con Verizon estándar o el perfil de premium, se le asignará ya tooview capaz de análisis de núcleo portal complementario de hello accesible a través de la opción de "Administrar" hello de hello portal de Azure. 

## <a name="azure-diagnostic-logs"></a>Registros de diagnóstico de Azure

Con esta nueva característica de Azure, ahora puede ver el análisis básico y guardarlo en uno o más destinos, entre los que se incluyen:

 - Cuenta de almacenamiento de Azure
 - Azure Event Hubs
 - [Repositorio de Log Analytics de OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Esta característica está disponible para todos los puntos de conexión de red CDN que pertenecen tooVerizon (Standard y Premium) y perfiles de red CDN de Akamai (estándar).

Registros de diagnóstico le permiten tooexport métricas de uso básico de la red CDN extremo tooa de diversos orígenes, por lo que se puede utilizar de una manera personalizada. Por ejemplo, puede hacer Hola tipos de exportación de datos siguientes:

- Exportar el almacenamiento de datos tooblob, exportar tooCSV y generar gráficos en excel.
- Exporte los centros de datos tooevent y correlacionar con los datos de otros servicios de azure.
- Exportar datos toolog análisis y ver los datos en su propio espacio de trabajo OMS

Hello en la ilustración siguiente se muestra una vista de análisis de núcleo de CDN habitual en los datos.

![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Figura 1: vista de Análisis Básico de la red CDN*

Hola tutorial pasa por esquema Hola de datos de análisis de núcleo de hello, pasos necesarios para habilitar la característica de Hola y entregarlos toovarious destinos y consumir a partir de estos destinos.

## <a name="enable-logging-with-azure-portal"></a>Habilitación del registro con Azure Portal

> [!NOTE]
> Hello registros de diagnóstico se activan **desactivar** de forma predeterminada. 

Siga los pasos de hello debajo de registro tooenable con análisis de núcleo de red CDN:

Inicie sesión en toohello [portal de Azure](http://portal.azure.com). Si no se ha habilitado ya la red CDN para el flujo de trabajo, [habilítela](cdn-create-new-endpoint.md) antes de continuar.

1. En el portal de hello, navegue demasiado**perfil de CDN**.
2. Seleccione un perfil de CDN, a continuación, seleccione el extremo de red CDN Hola que desea tooenable **registros de diagnóstico**.

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Vaya demasiado**registros de diagnóstico** hoja bajo **supervisión** sección, a continuación, cambiar el estado de hello demasiado**en**.

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Habilitación del registro con Azure Storage
    
toouse almacenamiento de Azure toostore Hola registros, seleccione **tooa cuenta de almacenamiento de archivo**, seleccione los días de retención y haga clic en **CoreAnalytics** en **registro**.

![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Figura 2: registro con Azure Storage*

### <a name="logging-with-oms-log-analytics"></a>Registro con Log Analytics de OMS

registros de toouse análisis de registros de OMS toostore hello, siga estos pasos:

1. De hello **registros de diagnóstico** hoja bajo **supervisión**, seleccione **enviar tooLog análisis** desde 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Configurar el registro de análisis de registros de hello haciendo clic en configurar. Esto le llevará tooa el cuadro de diálogo donde puede seleccionar un área de trabajo anterior o cree uno nuevo.

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Haga clic en **Crear nueva área de trabajo**.

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. A continuación debe seleccionar un nuevo nombre de área de trabajo, una suscripción existente, un grupo de recursos (nuevo o existente), la ubicación y el plan de tarifa. Tiene la opción de hello Anclar este panel de tooyour de configuración de. Haga clic en configuración de hello toocomplete Aceptar.

    A continuación debería ver el área de trabajo con los nombres del grupo de recursos y del área de trabajo de OMS. Los nombres deben ser únicos y solo se pueden usar letras, números y guiones. No se permiten espacios ni caracteres de subrayado. 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. A continuación, obtendrá un mensaje breve que indica que se ha creado el área de trabajo y se devuelven tooyour la pantalla de configuración de registro. Puede confirmar nombre hello del área de trabajo de análisis de registros.

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Una vez haya configurado la configuración de análisis de registros de hello, asegúrese de que también casilla hello CoreAnalytics para el registro de la red CDN.

6. Si todo está tooyour gusto, haga clic en hello **guardar** situado en la parte superior de hello del cuadro de diálogo de configuración de Hola.

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    Hola **guardar** botón ya no está activa y que hello en/botón ahora es ON, pero azul en lugar de púrpura.

7. Si desea que toosee la nueva área de trabajo OMS, vaya tooyour portal de Azure panel, haga clic en nombre de hello del área de trabajo de análisis de registros. A continuación, verá el área de trabajo (asegúrese de que el área de trabajo de OMS se resalta en hello izquierda). Haga clic en toosee de icono de Portal de OMS Hola el área de trabajo en el repositorio OMS Hola. 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    El repositorio OMS ahora está listo toolog datos. En orden tooconsume esos datos, debe usar un [solución de OMS](#consuming-oms-log-analytics-data), cubierto más adelante en este artículo.

Para más información sobre los retardos en el registro de datos, vaya [aquí](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Habilitación del registro con PowerShell

A continuación se muestra un ejemplo sobre cómo tooenable y obtener registros de diagnóstico a través de Hola Cmdlets de PowerShell de Azure.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Habilitación de registros de diagnóstico en una cuenta de Storage

Inicio de sesión y selección de una suscripción:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable registros de diagnóstico de una cuenta de almacenamiento, use este comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable registros de diagnóstico en un área de trabajo OMS, use este comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Consumo de registros de diagnósticos desde Azure Storage
Esta sección describe los esquemas de Hola de análisis de núcleo CDN Hola, cómo éstos se organizan dentro de una cuenta de almacenamiento de Azure y proporciona Hola de toodownload de código de ejemplo se registra en el archivo CSV de tooa.

### <a name="using-microsoft-azure-storage-explorer"></a>Uso del Explorador de Microsoft Azure Storage
Antes de poder acceder a datos de análisis de núcleo de Hola de hello cuenta de almacenamiento de Azure, debe primero un contenido de herramienta tooaccess hello en una cuenta de almacenamiento. Aunque hay varias herramientas disponibles en el mercado de hello, Hola uno que se recomienda es hello Explorador de almacenamiento de Microsoft Azure. Puede descargar la herramienta de Hola desde [aquí](http://storageexplorer.com/). Después de descargar e instalar software de hello, configurarlo toouse Hola misma cuenta de almacenamiento de Azure que se configuró como un toohello registros de diagnósticos de red CDN de destino.

1.  Abra el **Explorador de Microsoft Azure Storage**
2.  Busque la cuenta de almacenamiento de Hola
3.  Vaya toohello **"Contenedores de blobs"** nodo bajo este almacenamiento cuenta y expanda el nodo de Hola
4.  Contenedor de hello seleccione denominado **"coreanalytics de registros de visión"** y haga doble clic en él
5.  Mostrar los resultados de una en hello panel derecho a partir de hello primero nivel, qué aspecto **"resourceId ="**. Siga haciendo clic en forma de hello todos los hasta que vea el archivo hello **PT1H.json**. Vea Hola después Nota para ver una explicación de la ruta de acceso de Hola.
6.  Cada blob **PT1H.json** representa Hola registros de análisis durante una hora para un punto de conexión de red CDN concreto o de su dominio personalizado.
7.  esquema de Hola de contenido de Hola de este archivo JSON se describe en la sección de hello esquema de hello registros de análisis de núcleo


> [!NOTE]
> **Formato de ruta de acceso de blob**
> 
> Los registros de análisis básico se generan cada hora. Todos los datos de una hora se recopilan y almacenan dentro de un único blob de Azure como una carga JSON. ruta de acceso de Hello toothis blobs de Azure aparece como si hay una estructura jerárquica. Esto es porque interpreta la herramienta Explorador de almacenamiento de hello '/' como separador de directorios y muestra la jerarquía de Hola para su comodidad. En realidad, ruta de acceso completa de hello representa solo el nombre del blob de Hola. Este nombre de blob de hello sigue Hola sigue la convención de nomenclatura 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Descripción de los campos:**

|value|Descripción|
|-------|---------|
|Id. de suscripción    |Id. de suscripción de Azure Hola. Está en formato de Guid de Hola.|
|Recurso |Nombre de grupo de recursos de red CDN Hola recursos grupo toowhich Hola pertenecen.|
|Nombre del perfil |Nombre del perfil de CDN Hola|
|Nombre del punto de conexión |Nombre del extremo de red CDN Hola|
|Year|  representación en forma de 4 dígitos del año de hello, por ejemplo, de 2017|
|Mes| representación de 2 dígitos del número del mes Hola. 01=enero ... 12=diciembre|
|Día|   representación de 2 dígitos del día de hello del mes de Hola|
|PT1H.json| Archivo JSON real donde se almacenan los datos de análisis de Hola|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Exportar datos de análisis de núcleo de hello tooa archivo CSV

toomake TI tooaccess fácil Hola análisis Core, proporcionamos un código de ejemplo para una herramienta que permite descargar los archivos JSON de hello en un formato de archivo sin formato separados por comas, que puede ser usado tooeasily crear gráficos u otras agregaciones.

Le mostramos cómo puede usar la herramienta de hello:

1.  Visite el vínculo de Hola github: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Descargar código de hello
3.  Siga las instrucciones toocompile y configurar
4.  Ejecutar la herramienta de Hola
5.  Archivo CSV resultante muestra datos de análisis de hello en una jerarquía plana simple.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Consumo de registros de diagnóstico desde un repositorio de Log Analytics de OMS
Análisis de registros es un servicio en Operations Management Suite (OMS) que supervisa su toomaintain de entornos de nube y locales su disponibilidad y el rendimiento. Recopila los datos generados por los recursos en los entornos de nube y locales y de otros análisis de tooprovide herramientas supervisión a través de varios orígenes. 

toouse análisis de registros, debe [habilitar el registro](#enable-logging-with-azure-storage) repositorio de análisis de registros de OMS de Azure toohello, que se describe anteriormente en este artículo.

### <a name="using-hello-oms-repository"></a>Uso de hello repositorio de OMS

 Hola siguiente diagrama muestra la arquitectura de Hola de entradas de Hola y salidas del repositorio de hello:

![Repositorio de Log Analytics de OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Figura 3: repositorio de Log Analytics*

Puede mostrar datos de hello en una variedad de maneras con las soluciones de administración. Puede obtener soluciones de administración de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Puede instalar soluciones de administración de Azure marketplace, haga clic en hello **obtenerlo ahora** vínculo Hola final de cada solución.

### <a name="adding-an-oms-cdn-management-solution"></a>Agregación de una solución de administración de la red CDN de OMS

Siga estas tooadd una solución de administración de pasos:

1.   Si aún no lo ha hecho, inicie sesión en toohello portal de Azure con su suscripción de Azure y vaya tooyour panel.
    ![Panel de Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. Hola **New** hoja bajo **Marketplace**, seleccione **supervisión + administración**.

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. Hola **supervisión + administración** hoja, haga clic en **ver todas**.

    ![Ver todos](./media/cdn-diagnostics-log/15_See-all.png)

4.  Búsqueda de CDN en el cuadro de búsqueda de Hola.

    ![Ver todos](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Seleccione **Análisis Básico de la red CDN de Azure**. 

    ![Ver todos](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Después de hacer clic **crear**, estará más toocreate una nueva área de trabajo OMS o utilizar uno existente. 

    ![Ver todos](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Seleccione el área de trabajo de Hola que creó antes. A continuación, deberá tooadd una cuenta de automatización.

    ![Ver todos](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Hola de pantalla siguiente muestra formulario de la cuenta de automatización Hola que se debe rellenar. 

    ![Ver todos](./media/cdn-diagnostics-log/20_Automation.png)

9. Una vez haya creado la cuenta de automatización de hello, está listo tooadd la solución. Haga clic en hello **crear** botón.

    ![Ver todos](./media/cdn-diagnostics-log/21_Ready.png)

10. La solución se ha agregado tooyour área de trabajo. Volver atrás tooyour panel de portal de Azure.

    ![Ver todos](./media/cdn-diagnostics-log/22_Dashboard.png)

    Haga clic en el área de trabajo de análisis de registros de hello creó el área de trabajo de toogo tooyour. 

11. Haga clic en hello **Portal de OMS** icono toosee la nueva solución de portal de OMS Hola.

    ![Ver todos](./media/cdn-diagnostics-log/23_workspace.png)

12. El portal OMS debe parecerse Hola después de pantalla:

    ![Ver todos](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Haga clic en uno de hello iconos toosee varias vistas en los datos.

    ![Ver todos](./media/cdn-diagnostics-log/25_Interior-view.png)

    Puede desplazarse a la izquierda o derecha toosee más iconos que representan vistas individuales en datos Hola. 

    Haga clic en uno de los iconos de hello ofrece más detalles sobre los datos.

     ![Ver todos](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Ofertas y planes de tarifa

Puede ver ofertas y planes de tarifa de las soluciones de administración de OMS [aquí](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Personalización de las vistas

Puede personalizar vista hello en los datos mediante el uso de hello **Diseñador de vistas**. Vaya tooyour área de trabajo OMS y comienza a diseñar haciendo clic en hello **Diseñador de vistas** icono.

![Ver diseñador](./media/cdn-diagnostics-log/27_Designer.png)

Puede arrastra y coloca tipos de gráficos desde la izquierda de Hola y rellene Hola detalles de datos que desee tooanalyze en hello izquierda.

![Ver diseñador](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Retrasos en el registro de datos

Retrasos en el registro de datos de Verizon | Retrasos en el registro de datos de Akamai
--- | ---
Datos de registro de Verizon se retrasan de 1 hora y ocupan too2 horas toostart que aparecen después de la finalización de la propagación de punto de conexión. | Datos de registro de Akamai son de 24 horas retrasados y ocupa too2 horas toostart que aparece si se ha creado hace más de 24 horas. Si se ha creado recientemente, pueden tardar horas too25 Hola registros toostart que aparecen.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Tipos de registro de diagnósticos para el Análisis Básico de la red CDN

Ofrecemos actualmente solo registros de análisis de núcleo, que contienen las métricas que muestra estadísticas de respuesta HTTP y salida tal como se muestra de Hola POP CDN/bordes.

### <a name="core-analytics-metrics-details"></a>Detalles de las métricas de análisis básico
Hello en la tabla siguiente muestra una lista de métricas disponibles en hello que registros de análisis de núcleo. No todas las métricas están disponibles en todos los proveedores, si bien tales diferencias son mínimas. Hello en la tabla siguiente también se muestra si hay una métrica determinada de un proveedor. Tenga en cuenta que las métricas de hello están disponibles para únicamente los extremos de red CDN que tienen el tráfico.


|Métrica                     | Descripción   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Número total de solicitudes durante este periodo| Sí  |Sí   |
| RequestCountHttpStatus2xx |Recuento de todas las solicitudes que dieron lugar a un código HTTP 2xx (por ejemplo, 200, 202)              | Sí  |Sí   |
| RequestCountHttpStatus3xx | Recuento de todas las solicitudes que dieron lugar a un código HTTP 3xx (por ejemplo, 300, 302)              | Sí  |Sí   |
| RequestCountHttpStatus4xx |Recuento de todas las solicitudes que dieron lugar a un código HTTP 4xx (por ejemplo, 400, 404)               | Sí   |Sí   |
| RequestCountHttpStatus5xx | Recuento de todas las solicitudes que dieron lugar a un código HTTP 5xx (por ejemplo, 500, 504)              | Sí  |Sí   |
| RequestCountHttpStatusOthers |  Recuento de todos los demás códigos HTTP (fuera del intervalo 2xx-5xx) | Sí  |Sí   |
| RequestCountHttpStatus200 | Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 200              |No   |Sí   |
| RequestCountHttpStatus206 | Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 206              |No   |Sí   |
| RequestCountHttpStatus302 | Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 302              |No   |Sí   |
| RequestCountHttpStatus304 |  Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 304             |No   |Sí   |
| RequestCountHttpStatus404 | Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 404              |No   |Sí   |
| RequestCountCacheHit |Recuento de todas las solicitudes que dieron lugar a un acierto de caché. Esto significa que se realizó el servicio activo Hola directamente desde Hola POP toohello cliente.               | Sí  |No   |
| RequestCountCacheMiss | Recuento de todas las solicitudes que dieron lugar a un error de caché. Esto significa Hola activo no se encontró en el cliente de toohello más cercano de hello POP y, por tanto, se recuperó de hello origen.              |Sí   | No  |
| RequestCountCacheNoCache | Recuento de todas las solicitudes activo tooan que se evita que se almacenen en caché debido tooa configuración de usuario en el borde de Hola.              |Sí   | No  |
| RequestCountCacheUncacheable | Recuento de todas las solicitudes tooassets que se impide que se almacena en memoria caché Cache-Control del recurso de hello y expira encabezados, que indican que no se debe guardar en un POP o cliente hello HTTP                |Sí   |No   |
| RequestCountCacheOthers | Recuento de todas las solicitudes con un estado de caché no cubierto por lo anterior.              |Sí   | No  |
| EgressTotal | Transferencia de datos salientes en GB              |Sí   |Sí   |
| EgressHttpStatus2xx | Transferencia de datos salientes* para respuestas con códigos de estado HTTP 2xx en GB            |Sí   |No   |
| EgressHttpStatus3xx | Transferencia de datos salientes para respuestas con códigos de estado HTTP 3xx en GB              |Sí   |No   |
| EgressHttpStatus4xx | Transferencia de datos de salida para respuestas con códigos de estado HTTP 4xx en GB               |Sí   | No  |
| EgressHttpStatus5xx | Transferencia de datos de salida para respuestas con códigos de estado HTTP 5xx en GB               |Sí   |  No |
| EgressHttpStatusOthers | Transferencia de datos de salida para respuestas con otros códigos de estado HTTP en GB                |Sí   |No   |
| EgressCacheHit |  Transferencia de datos de salida para las respuestas que se enviaron directamente desde la caché de la red CDN Hola en hello POP de CDN/bordes  |Sí   |  No |
| EgressCacheMiss | Transferencia de datos de salida para las respuestas que no se encuentra en hello más próximo servidor POP y recuperar desde el servidor de origen de Hola              |Sí   |  No |
| EgressCacheNoCache | Transferencia de datos de salida para los activos que se evita que se almacenen en caché debido tooa configuración de usuario en el borde de Hola.                |Sí   |No   |
| EgressCacheUncacheable | Transferencia de datos de salida para los activos que se impidieron que se almacena en memoria caché del recurso de hello Cache-Control o Expires encabezados, que indican que no se debe guardar en un POP o cliente hello HTTP                    |Sí   | No  |
| EgressCacheOthers |  Transferencias de datos de salida para otros escenarios de caché.             |Sí   | No  |

* Transferencia de datos saliente hace referencia tootraffic entregado de cliente de toohello de servidores de POP de CDN.


### <a name="schema-of-hello-core-analytics-logs"></a>Esquema de hello registros de análisis de núcleo 

Todos los registros se almacenan en formato JSON y cada entrada tiene campos de cadena siguientes Hola siguiente esquema:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Donde hello 'tiempo' representa el tiempo de inicio de Hola de límite de hora de hello para el que se notifican las estadísticas de Hola. Cuando un proveedor de CDN no admite una métrica, en lugar de un valor doble o entero, habrá un valor nulo. Este valor nulo indica la ausencia de Hola de una métrica, y esto es diferente de un valor de 0. Tenga en cuenta que habrá un conjunto de estas métricas por dominio configurado en el punto de conexión de Hola.

Propiedades de ejemplo:

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Recursos adicionales

* [Registros de diagnóstico de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Análisis básico mediante el portal complementario de la red CDN](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Log Analytics de OMS de Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [API de REST de Azure Log Analytics](https://docs.microsoft.com/en-us/rest/api/loganalytics)







