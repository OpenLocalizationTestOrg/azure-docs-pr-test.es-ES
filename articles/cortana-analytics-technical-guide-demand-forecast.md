---
title: "Previsión de guía técnica de energía aaaDemand | Documentos de Microsoft"
description: "Una guía técnica toohello plantilla de solución con inteligencia de Cortana de Microsoft para la previsión de demanda en energía."
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>Guía técnica toohello plantilla de solución de inteligencia de Cortana de previsión de demanda en energía
## <a name="overview"></a>**Información general**
Plantillas de solución se han diseñado tooaccelerate proceso de hello de la creación de una demostración de E2E sobre el conjunto de inteligencia de Cortana. Una plantilla de implementada se aprovisionar la suscripción con el componente necesario de inteligencia de Cortana y crear relaciones de hello entre. También se propaga canalización de datos de hello con datos de ejemplo que se estén generados desde una aplicación de simulación de datos. Descargar simulador de datos de Hola de vínculo de hello proporcionado e instalar en el equipo local, consulte el archivo readme.txt de toohello para obtener instrucciones sobre cómo usar el simulador de Hola. Datos generados a partir de simulador de Hola se hacer uso de canalización de datos de Hola y empezar a generar la predicción de aprendizaje de máquina que, a continuación, se puede visualizar en el panel de Power BI Hola.

puede encontrar la plantilla de solución de Hello [aquí](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

proceso de implementación de Hello le guiará a través de varias tooset pasos sus credenciales de la solución. Asegúrese de que registrar estas credenciales como nombre de la solución, nombre de usuario y contraseña que proporcione durante la implementación de Hola.

objetivo de Hola de este documento es tooexplain arquitectura de referencia de Hola y diferentes componentes aprovisionados en su suscripción como parte de esta plantilla de solución. documento de Hello también habla de cómo tooreplace Hola datos de ejemplo, con datos reales de sus propio toosee pueda toobe visión/predicciones de usted won datos. Además, Hola documento trata sobre los elementos de Hola de hello plantilla de solución que necesitaría toobe modificado si desea que solución de hello toocustomize con sus propios datos. Se proporcionan instrucciones sobre cómo toobuild Hola panel de Power BI para esta plantilla de solución final Hola.

## <a name="big-picture"></a>**Idea general**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Arquitectura explicada
Cuando se implementa la solución de hello, se activan varios servicios de Azure en conjunto de análisis de Cortana (*, es decir,* Event Hubs, Stream Analytics, HDInsight, Data Factory, Machine Learning, *etc.*). diagrama de arquitectura de Hello anterior muestra, en un nivel alto, cómo se construye Hola previsión de demanda para la plantilla de solución de energía de principio a fin. Es posible que pueda tooinvestigate estos servicios haciendo clic en ellos en Hola diagrama de plantilla de solución creado con la implementación de Hola de solución de Hola. Hola siguientes secciones describe cada parte.

## <a name="data-source-and-ingestion"></a>**Origen e ingesta de datos**
### <a name="synthetic-data-source"></a>Origen de datos sintéticos
Para estos datos de Hola de plantilla se genera código fuente que se utiliza desde una aplicación de escritorio que se descarga y ejecuta de forma local tras una implementación correcta. Encontrará toodownload de instrucciones de Hola e instalar esta aplicación en la barra de hello propiedades cuando selecciona primer nodo de hello llamado simulador de datos de previsión de energía en el diagrama de plantilla de solución de Hola. Esta aplicación fuentes hello [concentrador de eventos de Azure](#azure-event-hub) con puntos de datos o eventos, que se utilizarán en el resto de Hola de flujo de solución de Hola.

aplicación de generación de eventos de Hello rellenará Hola concentrador de eventos de Azure solo mientras se ejecuta en el equipo.

### <a name="azure-event-hub"></a>Centro de eventos de Azure
Hola [concentrador de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) servicio es destinatario de Hola de entrada de hello proporcionada por hello sintética origen de datos se ha descrito anteriormente.

## <a name="data-preparation-and-analysis"></a>**Preparación y análisis de datos**
### <a name="azure-stream-analytics"></a>Análisis de transmisiones de Azure
Hola [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) servicio es usado tooprovide cerca de análisis en tiempo real en el flujo de entrada de Hola de hello [concentrador de eventos de Azure](#azure-event-hub) de servicio y publicar los resultados en un [Power BI](https://powerbi.microsoft.com) panel así como archivo sin formato de todas las toohello eventos entrantes [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) servicio para su posterior procesamiento por hello [Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/) servicio.

### <a name="hd-insights-custom-aggregation"></a>Agregación personalizada de HD Insights
Hola servicio Hdinsight de Azure es usado toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts (organizadas la factoría de datos de Azure) tooprovide agregaciones en eventos sin procesar de Hola que se han archivado con el servicio de análisis de transmisiones de Azure Hola.

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Hola [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) se usa el servicio (organiza la factoría de datos de Azure) toomake previsiones en consumo de energía futuras de una región determinada tiene entradas de hello recibidos.

## <a name="data-publishing"></a>**Publicación de datos**
### <a name="azure-sql-database-service"></a>Servicio Base de datos SQL de Azure.
Hola [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/) servicio es predicciones de hello toostore usa (administrada por factoría de datos de Azure) recibidas por el servicio de aprendizaje automático de Azure que se consumirán Hola Hola [Power BI](https://powerbi.microsoft.com) panel.

## <a name="data-consumption"></a>**Consumo de datos**
### <a name="power-bi"></a>Power BI
Hola [Power BI](https://powerbi.microsoft.com) servicio es tooshow usa un panel que contiene agregaciones proporcionadas por hello [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) los resultados almacenados en previsión de servicio, así como a petición [SQL Azure Base de datos](https://azure.microsoft.com/services/sql-database/) que se generó con hello [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) servicio. Para obtener instrucciones sobre cómo toobuild Hola panel de Power BI para esta plantilla de solución, consulte toohello sección más adelante.

## <a name="how-toobring-in-your-own-data"></a>**¿Cómo toobring en sus propios datos**
En esta sección se describe cómo toobring su propio tooAzure de datos y lo que requeriría áreas cambia para datos de Hola poner en esta arquitectura.

No es probable que cualquier conjunto de datos que coincidiría con el conjunto de datos de hello usado para esta plantilla de solución. Descripción de los datos y los requisitos será fundamental en cómo modificar esta plantilla toowork con sus propios datos. Si se trata de la primera toohello de exposición servicio de aprendizaje automático de Azure, puede obtener una introducción tooit mediante el uso de ejemplo de Hola en [cómo toocreate su primer experimento](machine-learning/machine-learning-create-experiment.md).

Hola siguientes secciones describe secciones Hola de plantilla de Hola que requerirán modificaciones cuando se introduce un nuevo conjunto de datos.

### <a name="azure-event-hub"></a>Centro de eventos de Azure
Hola [concentrador de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) servicio es muy genérico, de forma que los datos se pueden enviar toohello concentrador en formato CSV o JSON. Se produce ningún procesamiento especial Hola concentrador de eventos de Azure, pero es importante que comprenda datos Hola que se introduce en él.

Este documento describe cómo tooingest los datos, pero uno puede enviar fácilmente eventos o datos tooan concentrador de eventos de Azure, mediante hello [API del concentrador de eventos](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Análisis de transmisiones de Azure
Hola [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) servicio es usado tooprovide cerca de análisis en tiempo real mediante la lectura de flujos de datos y generar el número de tooany de datos de orígenes de.

Para hello previsión de demanda para la plantilla de solución de energía, consultas de análisis de transmisiones de Azure Hola consta de dos subconsultas, cada cómo consumir eventos de hello servicio del concentrador de eventos de Azure como entradas y salidas tootwo distintas ubicaciones de tener. Estas salidas constan de un conjunto de datos de Power BI y una ubicación de Almacenamiento de Azure.

Hola [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) consulta puede encontrarse por:

* Iniciar sesión en hello [portal de administración de Azure](https://manage.windowsazure.com/)
* Buscar trabajos de análisis de transmisiones de hello ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) que se genera cuando se implementó la solución de Hola. Uno es para insertar el almacenamiento de datos tooblob (p. ej., mytest1streaming432822asablob) y Hola sí lo para insertar datos tooPower BI (p. ej. mytest1streaming432822asapbi).
* Seleccionar

  * ***ENTRADAS*** entrada de consulta de hello tooview
  * ***CONSULTA*** propia consulta de hello tooview
  * ***GENERA*** tooview Hola diferentes salidas

Encontrará información acerca de la construcción de consultas de análisis de transmisiones de Azure en hello [referencia de consulta de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn834998.aspx) en MSDN.

En esta solución, Hola trabajo de análisis de transmisiones de Azure que genera el conjunto de datos con información de análisis en tiempo real sobre el panel de Hola entrante datos flujo tooa Power BI casi se proporciona como parte de esta plantilla de solución. Porque no hay conocimiento implícito acerca del formato de datos entrantes de hello, estas consultas necesitaría toobe modifica tomando como base el formato de datos.

Hello otro trabajo de análisis de transmisiones de Azure genera todos los [concentrador de eventos](https://azure.microsoft.com/services/event-hubs/) eventos a [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) y, por tanto, no requiere ninguna modificación, independientemente de su formato de datos tal y como se transmite información de eventos completa Hola toostorage.

### <a name="azure-data-factory"></a>Azure Data Factory
Hola [Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/) servicio orquesta movimiento de Hola y el procesamiento de datos. Hola previsión de demanda para datos de saludo de la plantilla de solución de energía generador se compone de doce [canalizaciones](data-factory/data-factory-create-pipelines.md) que mover y procesar los datos de hello con varias tecnologías.

  Puede tener acceso a su factoría de datos, abra el nodo de la factoría de datos de hello final Hola de diagrama de la plantilla de solución Hola creado con la implementación de Hola de solución de Hola. Esto le llevará se toohello factoría de datos en el portal de administración de Azure. Si ve errores en los conjuntos de datos, puede omitirlos tal como están debido generador toodata implementarse antes de que se inició el generador de datos de Hola. Estos errores no impiden que la Factoría de datos funcione.

Esta sección describen Hola necesarios [canalizaciones](data-factory/data-factory-create-pipelines.md) y [actividades](data-factory/data-factory-create-pipelines.md) contenidos en hello [Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/). A continuación se muestra en vista de diagrama de Hola de solución de Hola.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Cinco de las canalizaciones de Hola de este generador contienen [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) secuencias de comandos que son utilizado toopartition y datos de hello agregado. Cuando se indique, las secuencias de comandos de Hola se ubicará en hello [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) cuenta creada durante la instalación. Su ubicación será: demandforecasting\\\\script\\\\hive\\\\ (or https://[Your solution name].blob.core.windows.net/demandforecasting).

Toohello similar [análisis de transmisiones de Azure](#azure-stream-analytics-1) de las consultas, el [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts tienen conocimiento implícito acerca del formato de datos entrantes de hello, estas consultas necesitaría toobe modifica tomando como base el formato de datos y [característica ingeniería](machine-learning/machine-learning-feature-selection-and-engineering.md) requisitos.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
Esto [canalización](data-factory/data-factory-create-pipelines.md) canalización contiene una sola actividad - un [HDInsightHive](data-factory/data-factory-hive-activity.md) actividad mediante una [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que se ejecuta un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)hello de la secuencia de comandos tooaggregate cada 10 segundos transmitan datos petición en el nivel de la región de subestación toohourly nivel y copie en [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) a través de trabajo de análisis de transmisiones de Azure Hola.

El script de [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) para esta tarea de creación de particiones es ***AggregateDemandRegion1Hr.hql***

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
Esta [canalización](data-factory/data-factory-create-pipelines.md) contiene dos actividades:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) actividad mediante una [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que se ejecuta un subárbol tooaggregate Hola por hora petición datos del historial en el nivel de la región de subestación toohourly de nivel de script y coloque en el almacenamiento de Azure durante hello Azure Trabajo de análisis de transmisiones
* [Copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) actividad que mueve Hola datos agregados desde el almacenamiento de Azure blob toohello la base de datos de SQL de Azure que se haya proporcionado como parte de la instalación de la plantilla de hello solución.

Hola [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) secuencia de comandos para esta tarea es ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Estos [canalizaciones](data-factory/data-factory-create-pipelines.md) contienen varias actividades y cuyo resultado final se Hola puntúa predicciones de hello experimento de aprendizaje automático de Azure asociado a esta plantilla de solución. Son casi idénticas excepto cada uno de ellos solo administra región diferente de Hola que está llevando a cabo diferentes RegionID pasada de canalización ADF de Hola y de script de hive de Hola para cada región.  
actividades de Hello contenidas en esta instancia son:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) actividad mediante una [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que ejecute un subárbol script tooperform agregaciones y características necesarios para hello experimento de aprendizaje automático de Azure de ingeniería. Hello scripts de Hive para esta tarea son respectivos ***PrepareMLInputRegionX.hql***.
* [Copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) actividad que mueve los resultados de Hola de hello [HDInsightHive](data-factory/data-factory-hive-activity.md) actividad tooa único almacenamiento de Azure blob que puede acceder hello [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) actividad.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) actividad que llama el experimento de aprendizaje automático de Azure de Hola que da lugar a Hola da como resultado que se va a colocar en un único blob de almacenamiento de Azure.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Estos [canalizaciones](data-factory/data-factory-create-pipelines.md) contenga una única actividad - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) actividad que mueve los resultados de Hola de hello experimento de aprendizaje automático de Azure de hello respectivo ***MLScoringRegionXPipeline *** toohello la base de datos de SQL de Azure que se haya proporcionado como parte de la instalación de la plantilla de hello solución.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
Esto [canalizaciones](data-factory/data-factory-create-pipelines.md) contenga una única actividad - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) datos de petición en curso de agregados de actividad que mueve hello ***LoadHistoryDemandDataPipeline*** toohello Azure Base de datos de SQL que se haya proporcionado como parte de la instalación de la plantilla de hello solución.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
Estos [canalizaciones](data-factory/data-factory-create-pipelines.md) contenga una única actividad - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) actividad que mueve los datos de referencia de Hola de región/subestación/Topologygeo que están cargados tooAzure blob de almacenamiento como parte de la solución de Hola toohello de instalación de la plantilla base de datos SQL de Azure que se haya proporcionado como parte de la instalación de la plantilla de hello solución.

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Hola [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) experimentar utilizado para esta plantilla de solución proporciona predicción Hola de petición de región. experimento Hello es conjunto de datos específico toohello consumido y por lo tanto, requieren datos de toohello específico de modificación o reemplazo que se ponen en.

## <a name="monitor-progress"></a>**Supervisión de progreso**
Una vez que se inicia el generador de datos de hello, canalización hello comienza tooget hidratado y hello diferentes componentes de la solución inician lo en los siguientes comandos de hello emitidos por hello factoría de datos de acción. Hay dos maneras para supervisar canalización Hola.

1. Comprobar los datos de Hola desde el almacenamiento de blobs de Azure.

    Uno de los trabajos de análisis de transmisiones de hello escribe Hola sin formato entrante tooblob almacenamiento de datos. Si hace clic en **almacenamiento de blobs de Azure** componente de la solución de hello pantalla solución Hola se implementó correctamente y, a continuación, haga clic en **abiertos** en el panel derecho de hello, le permitirán toohello [Portal de administración de azure](https://portal.azure.com). Una vez allí, haga clic en **Blobs**. En el panel siguiente hello, verá una lista de contenedores. Haga clic en **"energysadata"**. En el panel siguiente hello, verá hello **"demandongoing"** carpeta. Dentro de la carpeta de rawdata hello, verá las carpetas con nombres como fecha = 2016-01-28 etcetera. Si ve estas carpetas, indica que los datos sin procesar de hello están correctamente se genera en el equipo y se almacena en almacenamiento de blobs. Verá archivos que deben tener tamaños finitos en MB en esas carpetas.
2. Comprobar los datos de Hola de base de datos de SQL Azure.

    Hola último paso de la canalización de hello es toowrite datos (por ejemplo, las predicciones de aprendizaje automático) en la base de datos SQL. Podría tener un máximo de 2 horas para hello datos tooappear de toowait en base de datos SQL. Una manera de toomonitor la cantidad de datos está disponible en la base de datos de SQL es a través de [portal de administración de Azure](https://manage.windowsazure.com/). En el panel izquierdo de hello, busque las bases de datos de SQL![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) y haga clic en él. A continuación, busque su base de datos (es decir, demo123456db) y haga clic en ella. En la página siguiente de hello en **"Conectar tooyour database"** sección, haga clic en **"Consultas de ejecución Transact-SQL en la base de datos SQL"**.

    En este caso, puede hacer clic en nueva consulta y buscar Hola número de filas (por ejemplo, "select Count de DemandRealHourly)" a medida que crece la base de datos, Hola número de filas de tabla de hello debe aumentar.)
3. Comprobar los datos de Hola desde el panel de Power BI.

    Puede configurar la ruta de acceso activa panel toomonitor Hola sin formato entrantes datos de Power BI. Siga las instrucciones de hello en la sección "Panel de Power BI" Hola.

## <a name="power-bi-dashboard"></a>**Panel de Power BI**
### <a name="overview"></a>Información general
Esta sección describe cómo tooset una toovisualize de panel de Power BI los datos en tiempo real de Azure transmitir analytics (ruta de acceso activa) como previsión así como resultados de aprendizaje automático de Azure (ruta de acceso frío).

### <a name="setup-hot-path-dashboard"></a>Configuración del panel de análisis en caliente
Hola pasos le ayudará cómo toovisualize datos en tiempo real de salida de análisis de transmisiones de trabajos que se generaron en tiempo de Hola de implementación de la solución. A [Power BI en línea](http://www.powerbi.com/) cuenta es hello tooperform necesarios pasos. Si no tiene una cuenta, puede [crear una](https://powerbi.microsoft.com/pricing).

1. Agregue una salida de Power BI en el Análisis de transmisiones de Azure (ASA).

   * Necesitará toofollow instrucciones hello [análisis de transmisiones de Azure y Power BI: un panel de análisis en tiempo real para obtener visibilidad en tiempo real de datos de transmisión](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset la salida de hello de su trabajo de análisis de transmisiones de Azure como la energía Panel BI.
   * Busque el trabajo de análisis de transmisiones de hello en su [portal de administración de Azure](https://manage.windowsazure.com). Hola nombre del trabajo de hello debe ser: nombreDeSolución + "streamingjob" + número aleatorio + "asapbi" (es decir, demostreamingjob123456asapbi).
   * Agregar una salida de Power BI para trabajo ASA de Hola. Conjunto hello **Alias de salida** como **'PBIoutput'**. Configure **Nombre de conjunto de datos** y **Nombre de tabla** como **"EnergyStreamData"**. Cuando haya agregado la salida de hello, haga clic en **"Start"** final Hola de trabajo de análisis de transmisiones de hello página toostart Hola. Recibirá un mensaje de confirmación (*por ejemplo*, "Se ha iniciado correctamente el trabajo de análisis de transmisiones myteststreamingjob12345asablob").
2. Inicie sesión demasiado[Power BI en línea](http://www.powerbi.com)

   * En hello dejado la sección de conjuntos de datos del panel en Mi área de trabajo, debe ser capaz de toosee muestra una conjunto de datos nuevo en el panel izquierdo de Hola de Power BI. Se trata de hello datos insertados de análisis de transmisiones de Azure en el paso anterior de Hola de transmisión por secuencias.
   * Asegúrese de hello seguro ***visualizaciones*** panel está abierto y se muestra en el lado derecho de la pantalla de bienvenida.
3. Crear Hola que icono "Demanda por marca de tiempo":

   * Haga clic en el conjunto de datos **'EnergyStreamData'** en hello dejado la sección de conjuntos de datos del panel.
   * Haga clic en el icono **"Gráfico de líneas"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * Haga clic en "EnergyStreamData" en el panel **Campos** .
   * Haga clic en **"Marca de hora"** y asegúrese de que se muestra en "Eje". Haga clic en **"Carga"** y asegúrese de que se muestra en "Valores".
   * Haga clic en **guardar** en Hola superior y el nombre de informe de hello como "EnergyStreamDataReport". informe de Hello denominado "EnergyStreamDataReport" se mostrará en la sección de informes en el panel de navegación de Hola de izquierda.
   * Haga clic en **"Pin Visual"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) icono en la esquina superior derecha de este gráfico de líneas, una ventana de "Pin tooDashboard" puede aparecer para toochoose un panel. Seleccione "EnergyStreamDataReport" y luego haga clic en "Anclar".
   * Al mantener el puntero del mouse de hello sobre este icono en el panel de hello, haga clic en "Editar" icono en la esquina superior derecha toochange su título como "Demanda por fecha y hora"
4. Cree otros iconos de panel basados en conjuntos de datos adecuados. a continuación se muestra la vista de panel final de Hola.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Configuración del panel de análisis en frío
En la canalización de datos inactivos de la ruta de acceso, objetivo fundamental de hello es previsión de la demanda de Hola de tooget de cada región. Power BI conecta a base de datos de SQL Azure tooan como origen de datos, donde se almacenan los resultados de la predicción de Hola.

> [!NOTE]
> 1) Toma algunas toocollect horas resultados suficientemente previsión para el panel de Hola. Se recomienda que iniciar este proceso de 2 a 3 horas después de comer el generador de datos de Hola. (2) en este paso, requisito previo de hello es toodownload e instalar software gratuito de hello [Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Obtiene las credenciales de base de datos de Hola.

   Necesitará **nombre del servidor, nombre de base de datos, nombre de usuario y contraseña de la base de datos** antes de seguir los pasos de toonext. Presentamos Hola pasos tooguide también cómo toofind ellos.

   * Una vez que **"Azure SQL Database"** se muestre en color verde en el diagrama de la plantilla de solución, haga clic en este icono y, después, haga clic en **"Abrir"**. Usted será el portal de administración de tooAzure guiada y así se abrirá la página de información de la base de datos.
   * En la página de hello, encontrará una sección "Database". Contiene una lista base de datos de Hola que haya creado. nombre de saludo de la base de datos debe ser **"El nombre de la solución + número aleatorio + 'db'"** (por ejemplo, "mytest12345db").
   * Haga clic en la base de datos nueva, que despliegue el panel, puede encontrar el nombre del servidor de base de datos en la parte superior de Hola Hola. El nombre del servidor de base de datos debería ser **"Su nombre de solución + Número aleatorio + 'database.windows.net,1433'"** (por ejemplo, "mytest12345.database.windows.net,1433").
   * La base de datos **nombre de usuario** y **contraseña** son Hola igual Hola nombre de usuario y contraseña almacenada anteriormente durante la implementación de soluciones de Hola.
2. Actualizar el origen de datos de Hola de ruta de acceso de hello frío archivo de Power BI

   * Asegúrese de que ha instalado la versión más reciente de Hola de [Power BI desktop](https://powerbi.microsoft.com/desktop).
   * Hola **"DemandForecastingDataGeneratorv1.0"** carpeta descargó, haga doble clic en hello **'Power BI Template\DemandForecastPowerBI.pbix'** archivo. visualizaciones de saludo inicial se basan en datos ficticios. **Nota:** si ve un error de masaje, asegúrese de que ha instalado la versión más reciente de Hola de Power BI Desktop.

     Una vez abierto, en la parte superior de Hola de archivo hello, haga clic en **'Editar consultas'**. Hola despliegue de ventana, haga doble clic en **'Source'** en el panel derecho Hola.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * Hola despliegue de ventana, reemplace **"Server"** y **"Database"** con sus propios nombres de servidor y base de datos y, a continuación, haga clic en **"Aceptar"**. Para nombre del servidor, asegúrese de especificar el puerto 1433 de hello (**YourSolutionName.database.windows.net, 1433**). Pasar por alto los mensajes de advertencia de Hola que aparecen en pantalla de bienvenida.
   * Hola siguiente emergente ventana, verá dos opciones en el panel izquierdo de hello (**Windows** y **base de datos**). Haga clic en **"Database"**, rellene su **"Username"** y **"Contraseña"** (se trata de hello nombre de usuario y contraseña que ha escrito la primera vez que implementa la solución de Hola y crea un Base de datos SQL Azure). En ***seleccione que nivel tooapply esta configuración se***, compruebe la opción de nivel de base de datos. Después, haga clic en **"Conectar"**.
   * Cuando se encuentre toohello atrás guiada de página anterior, cierre la ventana de Hola. Aparecerá un mensaje. Haga clic en **Aplicar**. Por último, haga clic en hello **guardar** botón toosave Hola cambiará. El archivo de Power BI ahora ha establecido toohello de conexión del servidor. Si las visualizaciones están vacías, asegúrese de que borrar las selecciones de hello en hello visualizaciones toovisualize todos los datos de Hola haciendo clic en el icono de borrador de hello en hello superior derecha de las leyendas de Hola. Usar nuevos datos tooreflect del botón de actualización de hello en visualizaciones de Hola. Inicialmente, solo verá datos de valor de inicialización de hello en las visualizaciones como factoría de datos de hello es toorefresh programada cada tres horas. Después de 3 horas, verá nuevas predicciones reflejadas en las visualizaciones al actualizar datos Hola.
3. (Opcional) Publicar panel inactivos de la ruta de acceso de hello demasiado[Power BI en línea](http://www.powerbi.com/). Tenga en cuenta que este paso necesita una cuenta de Power BI (o la cuenta de Office 365).

   * Haga clic en **"Publicar"** y pocos segundos después aparece una ventana Mostrar "Publicar tooPower BI correcto!" y con una marca de verificación verde. Haga clic en el vínculo de Hola "Demoprediction.pbix abrir en Power BI". toofind obtener instrucciones, consulte [publicar desde Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate un nuevo panel: haga clic en hello  **+**  firmar siguiente toothe **paneles** sección en el panel izquierdo de Hola. Escriba el nombre de Hola "Demostración de previsión de demanda" para este nuevo panel.
   * Una vez abierto el informe de hello, haga clic en ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin el panel de tooyour de visualizaciones. toofind obtener instrucciones, consulte [anclar un icono o panel de Power BI tooa desde un informe](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Ir a página de panel toohello y ajustar el tamaño de Hola y la ubicación de las visualizaciones y editar sus títulos. toofind instrucciones detalladas sobre cómo tooedit los iconos, consulte [editar un icono: cambio de tamaño, mover, cambiar el nombre, pin, eliminar, Agregar hipervínculo](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Este es un panel de ejemplo con algunos tooit de visualizaciones ancladas inactivos de la ruta de acceso.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (Opcional) Programar la actualización del origen de datos de Hola.

   * actualización de tooschedule de los datos de hello, mantenga el mouse sobre hello **EnergyBPI Final** conjunto de datos, haga clic en ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) y, a continuación, elija **Programar actualización**.
     **Nota:** si ve un mensaje de advertencia, haga clic en **modificar credenciales** y asegúrese de que las credenciales de la base de datos se Hola igual como los descritos en el paso 1.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Expanda hello **Programar actualización** sección. Active "Mantener los datos actualizados".
   * Programar la actualización de hello según sus necesidades. toofind obtener más información, consulte [actualizar datos en Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**¿Cómo toodelete la solución**
Asegúrese de detener generador de datos de hello no activamente con soluciones de hello tal y como se ejecuta el generador de datos de hello incurrirá en costos superior. Elimine solución Hola si no lo está usando. Si elimina la solución, se eliminarán todos los componentes de hello aprovisionados en su suscripción al implementar soluciones de Hola. solución de hello toodelete haga clic en el nombre de la solución en el panel izquierdo de la plantilla de solución de Hola de Hola y haga clic en eliminar.

## <a name="cost-estimation-tools"></a>**Herramientas de estimación de costos**
Hello dos herramientas siguientes son toohelp disponible se comprenden mejor los costos totales implicados en la ejecución Hola previsión de demanda para la plantilla de solución de energía en su suscripción:

* [Herramienta de estimación de costos de Microsoft Azure (en línea)](https://azure.microsoft.com/pricing/calculator/)
* [Herramienta de estimación de costos de Microsoft Azure (escritorio)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Agradecimientos**
Este artículo fue creado por el científico de datos Yijing Chen y el ingeniero de software Qiu Min de Microsoft.
