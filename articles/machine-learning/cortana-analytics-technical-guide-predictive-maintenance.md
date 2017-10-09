---
title: "Mantenimiento de aaaPredictive en aeroespacial con Azure - guía técnica de la solución de inteligencia de Cortana | Documentos de Microsoft"
description: "Una guía técnica toohello plantilla de solución con inteligencia de Cortana de Microsoft para un mantenimiento predictivo en aeroespacial, utilidades y el transporte."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Guía técnica toohello plantilla de solución de inteligencia de Cortana para un mantenimiento predictivo en aeroespacial y otras empresas

## <a name="important"></a>**Importante**
Este artículo está en desuso. información de Hello es toohello siendo pertinente problema esté realizando, es decir, un mantenimiento predictivo en aeroespacial, pero puede encontrar el último artículo de hello con hello más la información de toodate [aquí](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Agradecimientos**
Los autores de este artículo son los científicos de datos Yan Zhang, Gauher Shaheen, Fidan Boylu Uz y el ingeniero de software Dan Grecoe de Microsoft.

## <a name="overview"></a>**Información general**
Plantillas de solución se han diseñado tooaccelerate proceso de hello de la creación de una demostración de E2E sobre el conjunto de inteligencia de Cortana. Una plantilla de implementada se aprovisionar la suscripción con los componentes necesarios de inteligencia de Cortana y generar Hola relaciones entre ellos. También se propaga canalización de datos de hello con datos de ejemplo generados a partir de una aplicación de generador de datos que descargará e instalará en el equipo local después de implementar la plantilla de solución de Hola. datos de Hello generados a partir de generador de hello hacer uso de canalización de datos de Hola y empezar a generar las predicciones de aprendizaje automático que, a continuación, se pueden visualizar en el panel de Power BI Hola. proceso de implementación de Hello le guiará a través de varias tooset pasos sus credenciales de la solución. Asegúrese de que registrar estas credenciales como nombre de la solución, nombre de usuario y contraseña que proporcione durante la implementación de Hola.  

objetivo de Hola de este documento es tooexplain arquitectura de referencia de Hola y diferentes componentes aprovisionados en su suscripción como parte de esta plantilla de solución. documento de Hello también habla de cómo tooreplace los datos de ejemplo con datos reales de su propio toobe toosee capaz de visión y predicciones a partir de sus propios datos. Además, el documento de hello describe las partes del programa Hola a plantilla de solución que necesitaría toobe modificado si deseara solución de hello toocustomize con sus propios datos. Se proporcionan instrucciones sobre cómo toobuild Hola panel de Power BI para esta plantilla de solución final Hola.

> [!TIP]
> Puede descargar e imprimir una [versión en PDF de este documento](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Idea general**
![Arquitectura de mantenimiento predictivo](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Cuando se implementa la solución de hello, se activan varios servicios de Azure en conjunto de análisis de Cortana (*, es decir,* Event Hubs, Stream Analytics, HDInsight, Data Factory, Machine Learning, *etc.*). diagrama de arquitectura de Hello anterior muestra, en un nivel alto, cómo se construye Hola mantenimiento predictivo para aeroespacial plantilla de solución de principio a fin. Podrá tooinvestigate capaz de estos servicios en el portal de hello azure haciendo clic en ellos en el diagrama de la plantilla de solución Hola creado con la implementación de Hola de solución de hello con excepción de Hola de HDInsight en este servicio se aprovisiona a petición cuando Hola relacionados actividades de canalización están toorun necesaria y eliminan después.
Puede descargar una [versión a tamaño completo del diagrama de hello](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Hola siguientes secciones describe cada parte.

## <a name="data-source-and-ingestion"></a>**Origen e ingesta de datos**
### <a name="synthetic-data-source"></a>Origen de datos sintéticos
Para estos datos de Hola de plantilla se genera código fuente que se utiliza desde una aplicación de escritorio que se descarga y ejecuta de forma local tras una implementación correcta. Encontrará toodownload de instrucciones de Hola e instalar esta aplicación en la barra de hello propiedades cuando selecciona primer nodo de hello denominada Generador de datos de mantenimiento predictivo en diagrama de plantilla de solución de Hola. Esta aplicación fuentes hello [concentrador de eventos de Azure](#azure-event-hub) con puntos de datos o eventos, que se utilizarán en el resto de Hola de flujo de solución de Hola. Este origen de datos está formado por o derivado de datos disponibles al público de la [repositorio de datos de NASA](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) con hello [conjunto de datos de simulación de Turbofan motor degradación](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

aplicación de generación de eventos de Hello rellenará Hola concentrador de eventos de Azure solo mientras se ejecuta en el equipo.

### <a name="azure-event-hub"></a>Centro de eventos de Azure
Hola [concentrador de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) servicio es destinatario de Hola de entrada de hello proporcionada por hello sintética origen de datos se ha descrito anteriormente.

## <a name="data-preparation-and-analysis"></a>**Preparación y análisis de datos**
### <a name="azure-stream-analytics"></a>Análisis de transmisiones de Azure
Hola [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) servicio es usado tooprovide cerca de análisis en tiempo real en el flujo de entrada de Hola de hello [concentrador de eventos de Azure](#azure-event-hub) de servicio y publicar los resultados en un [Power BI](https://powerbi.microsoft.com) panel así como archivo sin formato de todas las toohello eventos entrantes [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) servicio para su posterior procesamiento por hello [Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/) servicio.

### <a name="hd-insights-custom-aggregation"></a>Agregación personalizada de HD Insights
Hola servicio Hdinsight de Azure es usado toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts (organizadas la factoría de datos de Azure) tooprovide agregaciones en eventos sin procesar de Hola que se han archivado con el servicio de análisis de transmisiones de Azure Hola.

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Hola [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) se usa el servicio (organiza la factoría de datos de Azure) toomake predicciones en hello restantes (RUL) de vida útil de un motor de avión determinado dado entradas Hola recibidos.

## <a name="data-publishing"></a>**Publicación de datos**
### <a name="azure-sql-database-service"></a>Servicio Base de datos SQL de Azure.
Hola [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/) servicio es predicciones de hello toostore usa (administrada por factoría de datos de Azure) recibidas por el servicio de aprendizaje automático de Azure que se consumirán Hola Hola [Power BI](https://powerbi.microsoft.com) panel.

## <a name="data-consumption"></a>**Consumo de datos**
### <a name="power-bi"></a>Power BI
Hola [Power BI](https://powerbi.microsoft.com) servicio es tooshow usa un panel que contiene las agregaciones y alertas proporcionadas por hello [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) servicio, así como las predicciones de RUL almacenadas en [SQL Azure Base de datos](https://azure.microsoft.com/services/sql-database/) que se generó con hello [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) servicio. Para obtener instrucciones sobre cómo toobuild Hola panel de Power BI para esta plantilla de solución, consulte toohello sección más adelante.

## <a name="how-toobring-in-your-own-data"></a>**¿Cómo toobring en sus propios datos**
En esta sección se describe cómo toobring su propio tooAzure de datos y lo que requeriría áreas cambia para datos de Hola poner en esta arquitectura.

No es probable que cualquier conjunto de datos que coincidiría con el conjunto de datos de hello usado por hello [conjunto de datos de simulación de Turbofan motor degradación](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) utilizados para esta plantilla de solución. Descripción de los datos y los requisitos será fundamental en cómo modificar esta plantilla toowork con sus propios datos. Si se trata de la primera toohello de exposición servicio de aprendizaje automático de Azure, puede obtener una introducción tooit mediante el uso de ejemplo de Hola en [cómo toocreate su primer experimento](machine-learning-create-experiment.md).

Hola siguientes secciones describe secciones Hola de plantilla de Hola que requerirán modificaciones cuando se introduce un nuevo conjunto de datos.

### <a name="azure-event-hub"></a>Centro de eventos de Azure
Hola servicio del concentrador de eventos de Azure es muy genérico, que pueden enviarse a datos toohello concentrador en formato CSV o JSON. No hay ningún procesamiento especial se produce en Hola concentrador de eventos de Azure, pero es importante que comprenda datos Hola que se introduce en él.

Este documento se describe cómo tooingest los datos, pero se pueden enviar fácilmente eventos o datos tooan concentrador de eventos de Azure mediante Hola la API del concentrador de eventos.

### <a name="azure-stream-analytics"></a>Análisis de transmisiones de Azure
Hola servicio de análisis de transmisiones de Azure es usado tooprovide cerca de análisis en tiempo real mediante la lectura de flujos de datos y generar el número de tooany de datos de orígenes de.

La consulta de análisis de transmisiones de Azure para hello mantenimiento predictivo para la plantilla de solución aeroespacial, formada por cuatro subconsultas, cada eventos mucho de hello servicio del concentrador de eventos de Azure y tener resultados a las cuatro ubicaciones distintas. Estas salidas constan de tres conjuntos de datos de Power BI y una ubicación de Almacenamiento de Azure.

consulta de análisis de transmisiones de Azure Hola puede encontrarse por:

* Iniciar sesión en hello portal de Azure
* Buscar trabajos de análisis de transmisiones de hello ![el icono de análisis de transmisiones](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) que se genera cuando se implementó la solución de hello (*p. ej.*, **maintenancesa02asapbi** y **maintenancesa02asablob** para la solución de un mantenimiento predictivo)
* Seleccionar
  
  * ***ENTRADAS*** entrada de consulta de hello tooview
  * ***CONSULTA*** propia consulta de hello tooview
  * ***GENERA*** tooview Hola diferentes salidas

Encontrará información acerca de la construcción de consultas de análisis de transmisiones de Azure en hello [referencia de consulta de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn834998.aspx) en MSDN.

En esta solución, las consultas de hello habían salida tres conjuntos de datos con información de análisis en tiempo real acerca de Hola entrantes datos flujo tooa panel de Power BI que se proporciona como parte de esta plantilla de solución casi. Porque no hay conocimiento implícito acerca del formato de datos entrantes de hello, estas consultas necesitaría toobe modifica tomando como base el formato de datos.

consulta de Hello en el segundo trabajo de análisis de transmisiones de hello **maintenancesa02asablob** simplemente genera todos los [concentrador de eventos](https://azure.microsoft.com/services/event-hubs/) eventos a [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) y por lo tanto, se requiere ninguna modificación información de eventos completa se transmite por secuencias toostorage independientemente de su formato de datos como Hola.

### <a name="azure-data-factory"></a>Azure Data Factory
Hola [Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/) servicio orquesta movimiento de Hola y el procesamiento de datos. En el mantenimiento predictivo para datos de plantilla de solución aeroespacial Hola generador se compone de tres [canalizaciones](../data-factory/data-factory-create-pipelines.md) que mover y procesar los datos de hello con varias tecnologías.  Puede tener acceso a su factoría de datos, abra el nodo de factoría de datos de Hola Hola final Hola de diagrama de la plantilla de solución Hola creado con la implementación de Hola de solución de Hola. Esto le llevará se toohello factoría de datos en el portal de Azure. Si ve errores en los conjuntos de datos, puede omitirlos tal como están debido generador toodata implementarse antes de que se inició el generador de datos de Hola. Estos errores no impiden que la Factoría de datos funcione.

![Errores de conjuntos de datos de Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

Esta sección describen Hola necesarios [canalizaciones](../data-factory/data-factory-create-pipelines.md) y [actividades](../data-factory/data-factory-create-pipelines.md) contenidos en hello [Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/). A continuación se muestra en vista de diagrama de Hola de solución de Hola.

![Azure Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Dos de las canalizaciones de Hola de este generador contienen [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) secuencias de comandos que son utilizado toopartition y datos de hello agregado. Cuando se indique, las secuencias de comandos de Hola se ubicará en hello [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) cuenta creada durante la instalación. Su ubicación será: maintenancesascript\\\\script\\\\hive\\\\ (o https://[Nombre de la solución].blob.core.windows.net/maintenancesascript).

Toohello similar [análisis de transmisiones de Azure](#azure-stream-analytics-1) de las consultas, el [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts tienen conocimiento implícito acerca del formato de datos entrantes de hello, estas consultas necesitaría toobe modifica tomando como base el formato de datos y [característica ingeniería](machine-learning-feature-selection-and-engineering.md) requisitos.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Esto [canalización](../data-factory/data-factory-create-pipelines.md) contiene una sola actividad - un [HDInsightHive](../data-factory/data-factory-hive-activity.md) actividad mediante una [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que se ejecuta un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) colocan datos de secuencia de comandos toopartition hello en [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) durante el [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) trabajo.

El script de [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) para esta tarea de creación de particiones es ***AggregateFlightInfo.hql***.

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Esto [canalización](../data-factory/data-factory-create-pipelines.md) contiene varias actividades y cuyo resultado final es Hola puntuado predicciones de hello [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) experimento asociado a esta plantilla de solución.

actividades de Hello contenidas en esta instancia son:

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) actividad mediante una [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que se ejecuta un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) tooperform agregaciones de secuencias de comandos y las características necesarias para Hola de ingeniería [Azure Aprendizaje automático](https://azure.microsoft.com/services/machine-learning/) experimentar.
  El script de [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) para esta tarea de creación de particiones es ***PrepareMLInput.hql***.
* [Copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) actividad que mueve los resultados de Hola desde el [HDInsightHive](../data-factory/data-factory-hive-activity.md) tooa de actividad único [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) blob que puede acceder los [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) actividad.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) actividad que llama hello [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) experimento que da lugar a resultados de Hola se coloque en un único [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) blob.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Esto [canalización](../data-factory/data-factory-create-pipelines.md) contiene una sola actividad - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) actividad que mueve los resultados de Hola de hello [aprendizaje automático de Azure](#azure-machine-learning) experimentar desde el *** MLScoringPipeline*** toohello [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/) que se haya proporcionado como parte de la instalación de la plantilla de solución.

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Hola [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) experimento utilizado para esta plantilla de solución proporciona Hola restantes útil vida (RUL) de un motor de avión. experimento Hello es conjunto de datos específico toohello consumido y por lo tanto, requieren datos de toohello específico de modificación o reemplazo que se ponen en.

Para obtener información acerca de cómo se creara Hola experimento de aprendizaje automático de Azure, consulte [mantenimiento predictivo: paso 1 de 3, preparación de los datos y la ingeniería de la característica](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**Supervisión de progreso**
 Una vez que se inicia el generador de datos de hello, canalización hello comienza tooget hidratado y hello diferentes componentes de la solución inician lo en los siguientes comandos de hello emitidos por hello factoría de datos de acción. Hay dos maneras para supervisar canalización Hola.

1. Uno de los trabajos de análisis de transmisiones de hello escribe Hola sin formato entrante tooblob almacenamiento de datos. Si hace clic en el componente de almacenamiento de blobs de la solución desde la pantalla de bienvenida, solución de Hola se implementó correctamente y, a continuación, haga clic en Abrir en el panel derecho de hello, le permitirán toohello [portal de administración](https://portal.azure.com/). Una vez allí, haga clic en Blobs. En el panel siguiente hello, verá una lista de contenedores. Haga clic en **maintenancesadata**. En el panel siguiente hello, verá hello **rawdata** carpeta. Dentro de la carpeta de rawdata hello, verá las carpetas con nombres como hora = 17, hora = etcetera 18. Si ve estas carpetas, indica que los datos sin procesar de hello están correctamente se genera en el equipo y se almacena en almacenamiento de blobs. Debería ver archivos csv que deben tener tamaños finitos en MB en esas carpetas.
2. Hola último paso de la canalización de hello es toowrite datos (por ejemplo, las predicciones de aprendizaje automático) en la base de datos SQL. Podría tener un máximo de tres horas para hello datos tooappear de toowait en base de datos SQL. Una manera de toomonitor la cantidad de datos está disponible en la base de datos de SQL es a través de [portal de azure](https://manage.windowsazure.com/). En el panel izquierdo de hello, busque las bases de datos de SQL ![icono SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) y haga clic en él. Después, busque la base de datos **pmaintenancedb** y haga clic en ella. En la página siguiente de hello en parte inferior de hello, haga clic en administrar
   
    ![Icono de Administrar](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    En este caso, puede hacer clic en nueva consulta y buscar Hola número de filas (por ejemplo, select Count de PMResult). A medida que crece la base de datos, debería aumentar el número de Hola de filas de tabla de Hola.

## <a name="power-bi-dashboard"></a>**Panel de Power BI**
### <a name="overview"></a>Información general
Esta sección describe cómo tooset una toovisualize de panel de Power BI resultante de los datos en tiempo real de análisis de transmisiones de Azure (ruta de acceso activa), así como de predicción por lotes de aprendizaje automático de Azure (ruta de acceso frío).

### <a name="setup-cold-path-dashboard"></a>Configuración del panel de ruta de acceso inactiva
En la canalización de datos inactivos de la ruta de acceso de hello, objetivo fundamental de hello es tooget la predicción RUL (vida útil restante) de cada motor de avión una vez que finalice un vuelo (ciclo). resultado de predicción de Hola se actualiza cada tres horas para predecir los motores del avión Hola que han terminado de un vuelo durante Hola últimas 3 horas.

Power BI conecta a base de datos de SQL Azure tooan como origen de datos, donde se almacenan los resultados de predicción. Nota: 1) tras implementar la solución, una predicción real se mostrará en la base de datos de hello en 3 horas.
archivo pbix Hello suministrada con la descarga del generador de hello contiene algunos datos de inicialización para que se pueden crear paneles de Power BI de hello inmediatamente. (2) en este paso, requisito previo de hello es toodownload e instalar software gratuito de hello [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Hello siguientes pasos le guiarán en cómo archivo tooconnect hello pbix a saludos de base de datos de SQL que se active en tiempo de Hola de implementación de la solución que contiene datos (*p. ej.*. resultados de predicción) para su visualización.

1. Obtiene las credenciales de base de datos de Hola.
   
   Necesitará **nombre del servidor, nombre de base de datos, nombre de usuario y contraseña de la base de datos** antes de seguir los pasos de toonext. Presentamos Hola pasos tooguide también cómo toofind ellos.
   
   * Una vez que la opción **Azure SQL Database** se muestre en color verde en el diagrama de la plantilla de solución, haga clic en ella y, después, en **Abrir**.
   * Verá una nueva pestaña/ventana del explorador que muestra hello página del portal de Azure. Haga clic en **'Grupos de recursos'** en el panel izquierdo de Hola.
   * Seleccionar suscripción Hola que use para implementar soluciones de hello y, a continuación, seleccione **' nombreDeSolución\_ResourceGroup'**.
   * En hello nueva emergente panel, haga clic en hello ![icono SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) icono tooaccess la base de datos. El nombre de la base de datos es toohello siguiente este icono (*p. ej.*, **'pmaintenancedb'**), hello y **el nombre del servidor de base de datos** aparece en hello propiedad de nombre de servidor y debe tener un aspecto similar demasiado**YourSoutionName.database.windows.net**.
   * La base de datos **nombre de usuario** y **contraseña** son Hola igual Hola nombre de usuario y contraseña almacenada anteriormente durante la implementación de soluciones de Hola.
2. Actualizar el origen de datos de hello del archivo de informe de hello inactivos de la ruta de acceso con Power BI Desktop.
   
   * En la carpeta hello en su PC que has descargado y descomprimido el archivo de generador, haga doble clic en el **PowerBI\\PredictiveMaintenanceAerospace.pbix** archivo. Si ve los mensajes de advertencia cuando se abre el archivo hello, ignorarlos. En la parte superior de Hola de archivo hello, haga clic en **'Editar consultas'**.
     
     ![Editar consultas](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Verá dos tablas, **RemainingUsefulLife** y **PMResult**. Seleccione la primera tabla de Hola y haga clic en ![icono de configuración de consulta](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) siguiente demasiado**'Source'** en **'Pasos aplicados'** en hello derecho **'Configuración de consulta'**panel. Ignore los mensajes de advertencia que aparezcan.
   * Hola despliegue de ventana, reemplace **"Servidor"** y **'Database'** con sus propios nombres de servidor y base de datos y, a continuación, haga clic en **'Aceptar'**. Para nombre del servidor, asegúrese de especificar el puerto 1433 de hello (**YourSoutionName.database.windows.net, 1433**). Deje el campo de la base de datos de hello como **pmaintenancedb**. Pasar por alto los mensajes de advertencia de Hola que aparecen en pantalla de bienvenida.
   * Hola siguiente emergente ventana, verá dos opciones en el panel izquierdo de hello (**Windows** y **base de datos**). Haga clic en **'Database'**, rellene su **"Username"** y **'Contraseña'** (se trata de hello nombre de usuario y contraseña que ha escrito la primera vez que implementa la solución de Hola y crea un Base de datos SQL Azure). En ***seleccione que nivel tooapply esta configuración se***, compruebe la opción de nivel de base de datos. A continuación, haga clic en **"Conectar"**.
   * Haga clic en la segunda tabla de hello **PMResult** , a continuación, haga clic en ![icono de navegación](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) siguiente demasiado**'Source'** en **'Pasos aplicados'** en hello derecho **'Configuración de consulta'** panel y actualizar Hola nombres de servidor y base de datos como en hello por encima de los pasos y haga clic en Aceptar.
   * Cuando se encuentre toohello atrás guiada de página anterior, cierre la ventana de Hola. Aparecerá un mensaje. Haga clic en **Aplicar**. Por último, haga clic en hello **guardar** botón toosave Hola cambiará. El archivo de Power BI ahora ha establecido toohello de conexión del servidor. Si las visualizaciones están vacías, asegúrese de que borrar las selecciones de hello en hello visualizaciones toovisualize todos los datos de Hola haciendo clic en el icono de borrador de hello en hello superior derecha de las leyendas de Hola. Usar nuevos datos tooreflect del botón de actualización de hello en visualizaciones de Hola. Inicialmente, solo verá datos de valor de inicialización de hello en las visualizaciones como factoría de datos de hello es toorefresh programada cada tres horas. Después de 3 horas, verá nuevas predicciones reflejadas en las visualizaciones al actualizar datos Hola.
3. (Opcional) Publicar panel inactivos de la ruta de acceso de hello demasiado[Power BI en línea](http://www.powerbi.com/). Tenga en cuenta que este paso necesita una cuenta de Power BI (o la cuenta de Office 365).
   
   * Haga clic en **'Publish'** y pocos segundos después aparece una ventana Mostrar "Publicar tooPower BI correcto!" y con una marca de verificación verde. Haga clic en el vínculo de Hola "PredictiveMaintenanceAerospace.pbix abrir en Power BI". toofind obtener instrucciones, consulte [publicar desde Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate un nuevo panel: haga clic en hello  **+**  firmar siguiente toothe **paneles** sección en el panel izquierdo de Hola. Escriba el nombre de Hola "Demostración de mantenimiento predictivo" para este nuevo panel.
   * Una vez abierto el informe de hello, haga clic en ![el icono de ALFILER](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin el panel de tooyour de visualizaciones. toofind obtener instrucciones, consulte [anclar un icono o panel de Power BI tooa desde un informe](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Ir a página de panel toohello y ajustar el tamaño de Hola y la ubicación de las visualizaciones y editar sus títulos. toofind instrucciones detalladas sobre cómo tooedit los iconos, consulte [editar un icono: cambio de tamaño, mover, cambiar el nombre, pin, eliminar, Agregar hipervínculo](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Este es un panel de ejemplo con algunos tooit de visualizaciones ancladas inactivos de la ruta de acceso.  Dependiendo de cuánto tiempo se ejecuta el generador de datos, los números en las visualizaciones de hello pueden ser diferentes.
     <br/>
     ![Vista final](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * actualización de tooschedule de los datos de hello, mantenga el mouse sobre hello **PredictiveMaintenanceAerospace** conjunto de datos, haga clic en ![icono de puntos suspensivos](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) y, a continuación, elija **Programar actualización**.
     <br/>
     **Nota:** si ve un mensaje de advertencia, haga clic en **modificar credenciales** y asegúrese de que las credenciales de la base de datos se Hola igual como los descritos en el paso 1.
     <br/>
     ![Programar la actualización](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Expanda hello **Programar actualización** sección. Active "Mantener los datos actualizados".
     <br/>
   * Programar la actualización de hello según sus necesidades. toofind obtener más información, consulte [actualizar datos en Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Configuración del panel de ruta de acceso activa
Hola pasos le ayudará cómo toovisualize datos en tiempo real de salida de análisis de transmisiones de trabajos que se generaron en tiempo de Hola de implementación de la solución. A [Power BI en línea](http://www.powerbi.com/) cuenta es hello tooperform necesarios pasos. Si no tiene una cuenta, puede [crear una](https://powerbi.microsoft.com/pricing).

1. Agregue una salida de Power BI en el Análisis de transmisiones de Azure (ASA).
   
   * Necesitará toofollow instrucciones hello [análisis de transmisiones de Azure y Power BI: un panel de análisis en tiempo real para obtener visibilidad en tiempo real de datos de transmisión](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset la salida de hello de su trabajo de análisis de transmisiones de Azure como la energía Panel BI.
   * consulta ASA Hello tiene tres salidas que son **aircraftmonitor**, **aircraftalert**, y **flightsbyhour**. Puede ver Hola consulta haciendo clic en la pestaña de consulta. Tooeach correspondiente de estas tablas, deberá tooadd un tooASA de salida. Cuando se agrega la primera salida de hello (*p. ej.* **aircraftmonitor**) que Hola seguro **Alias de salida**, **nombre de conjunto de datos** y  **Nombre de la tabla** se Hola igual (**aircraftmonitor**). Hola repita pasos tooadd salidas para **aircraftalert**, y **flightsbyhour**. Cuando haya agregado todas las tres tablas de salida e inició el trabajo ASA de hello, recibirá un mensaje de confirmación (*p. ej.*, "Análisis de transmisiones de inicio del trabajo maintenancesa02asapbi se realizó correctamente").
2. Inicie sesión demasiado[Power BI en línea](http://www.powerbi.com)
   
   * En hello dejado la sección de conjuntos de datos del panel en Mi área de trabajo, el ***conjunto de datos*** nombres **aircraftmonitor**, **aircraftalert**, y **flightsbyhour**debería aparecer. Se trata de hello transmisión de datos insertan desde el análisis de transmisiones de Azure en el conjunto de datos de hello anterior step.hello **flightsbyhour** no puede aparecer en hello mismo tiempo como Hola otros dos conjuntos de datos debido a toohello naturaleza de la consulta SQL Hola detrás de se. Sin embargo, deben aparecer después de una hora.
   * Asegúrese de hello seguro ***visualizaciones*** panel está abierto y se muestra en el lado derecho de la pantalla de bienvenida.
3. Una vez que tenga datos de Hola que fluyen en Power BI, puede empezar a visualizar Hola transmisión de datos. A continuación se muestra que un panel de ejemplo con algunas visualizaciones de la ruta de acceso activa anclado tooit. Puede crear otros iconos de panel basados en conjuntos de datos adecuados. Dependiendo de cuánto tiempo se ejecuta el generador de datos, los números en las visualizaciones de hello pueden ser diferentes.

    ![Vista de panel](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Estos son algunos toocreate pasos uno de los iconos de hello anterior: Hola ""flota vista de vs de Sensor 11. Threshold 48.26":
   
   * Haga clic en el conjunto de datos **aircraftmonitor** en hello dejado la sección de conjuntos de datos del panel.
   * Haga clic en hello **gráfico de líneas** icono.
   * Haga clic en **procesados** en hello **campos** panel para que muestra en "Eje" Hola **visualizaciones** panel.
   * Haga clic en s11 y s11\_alert para que ambos aparezcan en Valores. Haga clic en flecha pequeña situada Hola siguiente demasiado**s11** y **s11\_alerta**, cambie "Suma" demasiado "medio".
   * Haga clic en **guardar** Hola superior y nombre de informe de Hola "aircraftmonitor". Se mostrará el informe denominado "aircraftmonitor" Hola **informes** sección Hola **navegador** panel de hello izquierda.
   * Haga clic en hello **Pin Visual** icono en la esquina derecha superior de Hola de este gráfico de líneas. Puede aparecer una ventana de "Pin tooDashboard" para que elegir un panel. Seleccione "Demostración de mantenimiento predictivo" y luego haga clic en "Anclar".
   * Al mantener el puntero del mouse Hola sobre este icono en el panel de hello, haga clic en icono de "edit" hello en toochange de la esquina superior derecha de hello su título demasiado "frente a vista de flota de Sensor 11. Umbral 48,26" y el subtítulo demasiado"Media en línea con el tiempo".

## <a name="how-toodelete-your-solution"></a>**¿Cómo toodelete la solución**
Asegúrese de detener generador de datos de hello no activamente con soluciones de hello tal y como se ejecuta el generador de datos de hello incurrirá en costos superior. Elimine solución Hola si no lo está usando. Si elimina la solución, se eliminarán todos los componentes de hello aprovisionados en su suscripción al implementar soluciones de Hola. solución de hello toodelete haga clic en el nombre de la solución en el panel izquierdo de la plantilla de solución de Hola de Hola y haga clic en eliminar.

## <a name="cost-estimation-tools"></a>**Herramientas de estimación de costos**
Hello dos herramientas siguientes son toohelp disponible se comprenden mejor los costos totales implicados en la ejecución Hola mantenimiento predictivo para la plantilla de solución aeroespacial en su suscripción:

* [Herramienta de estimación de costos de Microsoft Azure (en línea)](https://azure.microsoft.com/pricing/calculator/)
* [Herramienta de estimación de costos de Microsoft Azure (escritorio)](http://www.microsoft.com/download/details.aspx?id=43376)

