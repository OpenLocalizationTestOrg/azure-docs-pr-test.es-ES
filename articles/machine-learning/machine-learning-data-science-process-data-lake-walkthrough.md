---
title: 'Ciencia de datos escalables con Azure Data Lake: tutorial completo | Microsoft Docs'
description: "¿Cómo toouse Azure Data Lake toodo datos exploración binario la clasificación y tareas en un conjunto de datos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Ciencia de datos escalables con Azure Data Lake: tutorial completo
Este tutorial muestra cómo toouse la exploración de datos de Azure Data Lake toodo y tareas de clasificación binaria de una muestra de Hola NYC taxi tarifas y recorridos toopredict de conjunto de datos o no una sugerencia que se va a pagar por una tarifa. Le guiará por los pasos de Hola de hello [proceso de ciencia de datos de equipo](http://aka.ms/datascienceprocess)-to- end, de entrenamiento de toomodel de adquisición de datos y, a continuación, la implementación de toohello de un servicio web que publica el modelo de Hola.

### <a name="azure-data-lake-analytics"></a>Análisis con Azure Data Lake
Hola [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) tiene todos los Hola capacidades necesario toomake más sencilla para datos científicos toostore cualquier tamaño, forma y velocidad y tooconduct de procesamiento de datos, análisis y modelado de aprendizaje de máquina avanzados con alta escalabilidad de una manera rentable.   Se paga por trabajo, solo cuando se procesan los datos. Análisis de Azure Data Lake incluye U-SQL, un lenguaje que mezclas Hola naturaleza declarativa de SQL con expresivo de Hola de C# tooprovide escalable distribuye la capacidad de consulta. Le permite tooprocess datos no estructurados mediante la aplicación de esquema en lectura, insertar lógica personalizada y definida por el usuario (UDF) las funciones e incluye extensibilidad tooenable específica un control exhaustivo sobre cómo tooexecute a escala. toolearn más información acerca de la filosofía de diseño de hello detrás de T-SQL, consulte [entrada de blog de Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Análisis de Data Lake es también una parte fundamental del conjunto de aplicaciones Cortana Analytics y funciona con Almacenamiento de datos SQL de Azure, Power BI y Data Factory. Esto proporciona una plataforma completa de análisis avanzado y macrodatos en la nube.

Este tutorial comienza con la descripción de los requisitos previos de Hola y recursos que son necesarios toocomplete Hola tareas con análisis de Data Lake que forman el proceso de ciencia de datos de Hola y cómo tooinstall ellos. A continuación, se describen los pasos de procesamiento de datos de hello con U-SQL y concluye mostrándole cómo toouse Python y Hive con toobuild de estudio de aprendizaje automático de Azure e implementar modelos predictivos Hola. 

### <a name="u-sql-and-visual-studio"></a>U-SQL y Visual Studio
En este tutorial se recomienda el uso conjunto de datos de Visual Studio tooedit U-SQL scripts tooprocess Hola. las secuencias de comandos de U-SQL de Hola están descritos aquí y proporcionan en un archivo independiente. proceso de Hello incluye ingesta en bloque, explorar y Hola datos de muestreo. También muestra cómo toorun U T-SQL incluir en un script de trabajo de hello portal de Azure. Se crean tablas de subárbol para los datos de hello en una generación de Hola de toofacilitate de clúster de HDInsight asociado y la implementación de un modelo de clasificación binaria en estudio de aprendizaje automático de Azure.  

### <a name="python"></a>Python
En este tutorial también contiene una sección que muestra cómo toobuild e implementar un modelo de predicción mediante Python con estudio de aprendizaje automático de Azure.  Proporcionamos Jupyter notebook con scripts de Python de Hola para estos pasos de este proceso. Bloc de notas de Hello incluye código para algunos pasos de ingeniería de características adicionales y la construcción de modelos, como clasificación multiclase y regresión además modelado toohello modelo de clasificación binaria que se describen aquí. tarea de regresión de Hello es la cantidad de Hola de toopredict de sugerencia de hello en función de otras características de sugerencia. 

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Estudio de aprendizaje automático de Azure es toobuild usado e implementar los modelos de predicción de Hola. Para esto se aplican dos enfoques: primero con scripts Python y después con tablas de Hive en un clúster de HDInsight (Hadoop).

### <a name="scripts"></a>Scripts
Solo los pasos principales Hola se describen en este tutorial. Puede descargar Hola completa **script U-SQL** y **Jupyter Notebook** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar estos temas, debe tener el siguiente hello:

* Una suscripción de Azure. Si aún no tiene una, consulte [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)(Obtener una evaluación gratuita de Azure).
* [Recomendado] Visual Studio 2013 o posterior. Si aún no tiene ninguna de estas versiones instaladas, puede descargar una versión gratuita de Community desde [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> En lugar de Visual Studio, también puede usar las consultas de hello Azure Portal toosubmit Azure Data Lake. Se proporcionarán instrucciones acerca de cómo toodo así con Visual Studio y en el portal de hello en la sección de hello titulada **procesar datos con SQL U**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Preparación del entorno de la ciencia de datos para Azure Data Lake
entorno de ciencia de datos tooprepare hello en este tutorial, cree Hola recursos siguientes:

* Almacén de Azure Data Lake (ADLS) 
* Análisis de Azure Data Lake (ADLA)
* Cuenta de Almacenamiento de blobs de Azure
* Cuenta de Estudio de aprendizaje automático de Azure
* Herramientas de Azure Data Lake para Visual Studio (se recomienda)

Esta sección proporciona instrucciones sobre cómo toocreate de estos recursos. Si elige toouse tablas de Hive con aprendizaje automático de Azure, en lugar de Python, toobuild un modelo, también necesitará tooprovision un clúster de HDInsight (Hadoop). Este procedimiento alternativo en descrito en hello sección apropiada.


> [!NOTE]
> Hola **almacén de Azure Data Lake** se pueden crear por separado o bien cuando cree hello **análisis de Azure Data Lake** como almacenamiento predeterminado de Hola. Se hace referencia a las instrucciones para crear cada uno de estos recursos por separado a continuación, pero Hola cuenta de almacenamiento de Data Lake no es necesario crear por separado.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Creación de un Almacén de Azure Data Lake


Crear un ADLS de hello [Portal de Azure](http://portal.azure.com). Para más información, consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Ser seguro tooset seguridad Hola identidad de AAD de clúster en hello **origen de datos** hoja de hello **configuración opcional** hoja descritos no existe. 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Creación de una cuenta de Análisis de Azure Data Lake
Crear una cuenta ADLA de hello [Portal de Azure](http://portal.azure.com). Para más información, consulte [Tutorial: Introducción a Análisis de Azure Data Lake mediante el Portal de Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Creación de una cuenta de Almacenamiento de blobs de Azure
Crear una cuenta de almacenamiento de blobs de Azure de hello [Portal de Azure](http://portal.azure.com). Para obtener más información, vea Hola crear una cuenta de almacenamiento sección [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md).

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Configuración de una cuenta de Estudio de aprendizaje automático de Azure
Iniciar en estudio de aprendizaje automático de Azure de hello [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) página. Haga clic en hello **empezar ahora** botón y, a continuación, elija un "Área de trabajo estándar" o "Área de trabajo gratuita". Después de esto será capaz de toocreate experimentos en estudio de aprendizaje automático.  

### <a name="install-azure-data-lake-tools-recommended"></a>Instalación de las herramientas de Azure Data Lake [recomendación]
Instale las herramientas de Azure Data Lake para su versión de Visual Studio desde [Azure Data Lake Tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)(Herramientas de Azure Data Lake para Visual Studio).

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

Una vez finalizada correctamente la instalación de hello, abra Visual Studio. Debería ver el menú de Hola Hola Data Lake ficha en la parte superior de Hola. Los recursos de Azure deben aparecer en el panel izquierdo de hello cuando inicia sesión en su cuenta de Azure.

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a>el conjunto de datos de Hello NYC Taxi viajes
Hello conjunto de datos se usa aquí es un conjunto de datos disponible públicamente--hello [conjunto de datos de Nueva York Taxi viajes](http://www.andresmh.com/nyctaxitrips/). Hola datos NYC Taxi recorridos consta de unos 20GB de archivos comprimidos de CSV (sin comprimir de ~ 48GB), más de 173 millones de grabación hello y viajes individuales puntuación de pago para cada recorrido. Cada registro de ida y vuelta incluye ubicaciones de recogida y entrega de Hola y tiempos, anónimos hack número de licencia (del controlador) y Hola número medallion (identificador único del taxi). datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:

* Hola 'trip_data' CSV contiene los detalles de ida y vuelta, como el número de los pasajeros, recogida y puntos de caída, duración de ida y vuelta y duración del viaje. Estos son algunos registros de ejemplo:
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* Hello 'trip_fare' CSV contiene detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago. Estos son algunos registros de ejemplo:
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

recorridos de toojoin de clave única de Hello\_datos y recorridos\_tarifa se compone de hello después de tres campos: medallion, prueba\_licencia y recogida\_fecha y hora. archivos CSV raw de Hello pueden tener acceso desde un blob de almacenamiento de Azure pública. Hola script U-SQL para esta combinación es Hola [unir tablas de ida y vuelta y tarifa](#join) sección.

## <a name="process-data-with-u-sql"></a>Procesamiento de datos con U-SQL
las tareas de procesamiento de datos de Hello mostradas en esta sección incluyen ingesta en bloque, comprobar la calidad, explorar y Hola datos de muestreo. También se muestran cómo toojoin de ida y vuelta y tarifa tablas. sección final Hello muestra ejecución un trabajo de script U-SQL desde Hola portal de Azure. Estos son vínculos tooeach subsección:

* [Ingesta de datos: leer datos de un blob público](#ingest)
* [Comprobaciones de la calidad de los datos](#quality)
* [Exploración de datos](#explore)
* [Combinación de las tablas de carreras y tarifas](#join)
* [Muestreo de datos](#sample)
* [Ejecución de trabajos U-SQL](#run)

las secuencias de comandos de U-SQL de Hola están descritos aquí y proporcionan en un archivo independiente. Puede descargar Hola completa **secuencias de comandos SQL U** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

tooexecute T-SQL, abra Visual Studio, haga clic en **archivo--> Nuevo--> proyecto**, elija **U-SQL proyecto**, nombre y guardar tooa carpeta.

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> Es posible toouse hello Azure Portal tooexecute U-SQL en lugar de Visual Studio. Puede navegar por los recursos de análisis de Azure Data Lake toohello en el portal de Hola y enviar consultas directamente, como se ilustra en la figura siguiente de Hola.
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Ingesta de datos: leer datos de un blob público
ubicación de Hola de datos de Hola Hola blobs de Azure se hace referencia como  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  y puede extraerse mediante **Extractors.Csv()**. Sustituir su propio nombre del contenedor y el nombre de cuenta de almacenamiento en los siguientes scripts para container_name@blob_storage_account_name en la dirección de wasb Hola. Puesto que son nombres de archivo de hello en el mismo formato, podemos usar **recorridos\_data_ {\*\}.csv** tooread en todos los archivos de 12 de ida y vuelta. 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

Dado que hay encabezados en la primera fila de hello, se necesitan encabezados de hello tooremove y cambiar los tipos de columna en las columnas adecuadas. Se puede guardar Hola procesa datos tooAzure datos Lake almacenamiento usando **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**cuenta de almacenamiento de blobs _ o tooAzure mediante  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** . 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

De igual forma podemos leer Hola tarifa en conjuntos de datos. Haga clic con el almacén de Azure Data Lake, puede elegir toolook de los datos **Portal de Azure--> Explorador de datos** o **Explorador de archivos** dentro de Visual Studio. 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Comprobaciones de la calidad de los datos
Después de que se han leído tarifas y recorridos de tablas, comprobaciones de calidad de datos pueden realizarse en hello siguiente forma. Hola resultante archivos CSV puede ser almacenamiento de blobs de salida tooAzure o almacén de Azure Data Lake. 

Buscar el número de Hola de medallions y número único de medallions:

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

Busque las placas de licencia que tenían más de 100 carreras:

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

Busque los registros no válidos en términos de pickup_longitude:

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

Busque los valores que faltan en algunas variables:

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Exploración de datos
Podemos hacer una mejor comprensión de los datos de hello algunos tooget de exploración de datos.

Buscar distribución Hola de viajes superpuestos y no superpuesto de:

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

Buscar distribución Hola de cantidad de sugerencia con valores de corte: 0,5,10 y 20 dólares.

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

Busque las estadísticas básicas de la distancia de las carreras:

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Buscar percentiles Hola de distancia de ida y vuelta:

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a>Combinación de las tablas de carreras y tarifas
Las tablas de carreras y tarifas pueden combinarse por placa de licencia, hack_license y pickup_time.

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Para cada nivel de recuento de pasajeros, calcule el número de Hola de registros, sugerencia promedio, la varianza de la cantidad de información sobre, porcentaje de viajes superpuestos de.

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Muestreo de datos
En primer lugar se selecciona de forma aleatoria 0,1% de los datos de Hola Hola de tabla combinada:

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

A continuación, se realiza un muestreo estratificado por la variable binaria tip_class:

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>Ejecución de trabajos U-SQL
Cuando termine de editar scripts SQL U, puede enviarlos a server toohello con su cuenta de análisis de Data Lake de Azure. Haga clic en **Data Lake**, **Enviar trabajo**, seleccione su **cuenta de Analytics**, elija **Paralelismo** y haga clic en el botón **Enviar**.  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

Cuando el trabajo de hello es considerado correctamente, estado de Hola de su trabajo se mostrará en Visual Studio para la supervisión. Cuando finalice el trabajo de hello, puede que el proceso de ejecución reproducción Hola trabajo incluso y obtenga más información sobre Hola crear cuellos de botella pasos tooimprove la eficacia de su proceso de trabajo. También puede ir tooAzure estado de hello toocheck de Portal de los trabajos de SQL U.

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

Ahora puede comprobar los archivos de salida de hello en almacenamiento de blobs de Azure o Portal de Azure. Datos de ejemplo de Hola estratificado se usará para el modelado en el paso siguiente Hola.

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Generación e implementación de modelos en Aprendizaje automático de Azure
Se muestran dos opciones disponibles para que los datos de toopull en toobuild de aprendizaje automático de Azure y 

* En la primera opción hello, usa los datos de hello muestreada que se ha escrito tooan blobs de Azure (Hola **muestreo de datos** paso anterior) y usar Python toobuild e implementar modelos de aprendizaje automático de Azure. 
* En la segunda opción hello, consultar datos hello en Azure Data Lake directamente mediante una consulta de Hive. Esta opción requiere que cree un nuevo clúster de HDInsight o use un clúster de HDInsight existente donde hello Hive tablas toohello de punto de datos de Nueva York Taxi datos Lake en almacenamiento de Azure.  Las dos opciones se explican a continuación. 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a>Opción 1: Uso de Python toobuild e implementar modelos de aprendizaje automático
toobuild e implementar modelos de aprendizaje automático con Python, crear Jupyter Notebook en el equipo local o en estudio de aprendizaje automático de Azure. Hello Jupyter Notebook proporcionada en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contiene Hola tooexplore de código completo, visualizar datos, ingeniería de característica, modelado y la implementación. En este artículo, se muestran solo modelado Hola e implementación. 

### <a name="import-python-libraries"></a>Importación de bibliotecas de Python
Hola toorun de pedido de ejemplo Jupyter Notebook u Hola archivo de script de Python, hello siguientes Python paquetes son necesarios. Si usas Hola servicio Bloc de notas de aprendizaje automático de Azure, estos paquetes se han instalado previamente.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a>Leer datos de Hola de blob
* Cadena de conexión   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* Leer como texto
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* Agregar nombres de columna y separar las columnas
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Cambiar algunos toonumeric de columnas
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Generación de modelos de aprendizaje automático
Este artículo se crea un toopredict de modelo de clasificación binaria si está superpuesto un viaje o no. Hola Jupyter Notebook puede encontrar otros dos modelos: clasificación multiclase y los modelos de regresión.

* Primero necesitamos toocreate variables ficticia que se pueden usar en scikit-Obtenga información acerca de los modelos
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Crear la trama de datos para el modelado de Hola
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* División 60 - 40 de entrenamiento y pruebas
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* Regresión logística en conjunto de pruebas
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* Puntuar conjunto de datos de pruebas
  
        Y_test_pred = logit_fit.predict(X_test)
* Calcular métricas de evaluación
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>Generación de API de servicio web y su consumo en Python
Queremos que la máquina de hello toooperationalize modelo de aprendizaje después de que se ha creado. Aquí usamos modelo logística binaria de hello como ejemplo. Asegúrese de que scikit Hola-Obtenga información acerca de la versión en el equipo local es 0.15.1. Tooworry sobre esto no es necesario si utiliza el servicio de Azure ML studio.

* Busque las credenciales del área de trabajo en la configuración de Estudio de aprendizaje automático de Azure. En Azure Machine Learning Studio, haga clic en **Configuración** --> **Nombre** --> **Tokens de autorización**. 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* Cree un servicio web
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* Obtenga las credenciales del servicio web
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* Llame a una API de servicio web. Tener toowait entre 5 y 10 segundos después del paso anterior Hola.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Opción 2: Crear e implementar modelos directamente en Aprendizaje automático de Azure
Estudio de aprendizaje automático de Azure puede leer los datos directamente desde el almacén de Azure Data Lake y, a continuación, puede toocreate usado e implementar modelos. Este enfoque utiliza una tabla de Hive que apunta al almacén de Azure Data Lake Hola. Esto requiere que se aprovisiona un clúster de HDInsight de Azure diferente, en qué Hola subárbol se crea la tabla. Hola siguientes secciones muestran cómo toodo esto. 

### <a name="create-an-hdinsight-linux-cluster"></a>Creación de un clúster de HDInsight Linux
Crear un clúster de HDInsight (Linux) de hello [Portal de Azure](http://portal.azure.com). Para obtener más información, vea hello **crear un clúster de HDInsight con acceso tooAzure almacén de Data Lake** sección [crear un clúster de HDInsight con el almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Creación de una tabla de Hive en HDInsight
Ahora creamos Hive tablas toobe usar en el estudio de aprendizaje automático de Azure en clúster de HDInsight de hello mediante datos de hello almacenados en el almacén de Azure Data Lake en el paso anterior de Hola. Vaya toohello acaba de crear el clúster de HDInsight. Haga clic en **configuración** --> **propiedades** --> **clúster identidad AAD** --> **acceso a ADLS**, Asegúrese de que se agrega la cuenta de almacén de Azure Data Lake en lista de hello con lectura, escritura y ejecución derechos. 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

A continuación, haga clic en **panel** toohello siguiente **configuración** botón y una ventana se abrirá. Haga clic en **vista Hive** Hola esquina superior derecha de la página de Hola y se verán hello **Editor de consultas**.

 ![20 |](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Pegar en hello después toocreate de scripts de Hive una tabla. Hola de origen de datos se encuentra en la referencia de almacén de Azure Data Lake de esta manera: **adl://data_lake_store_name.azuredatalakestore.net:443/nombreCarpeta/nombre_archivo**.

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


Cuando finaliza la ejecución de consultas de hello, verá resultados de hello similar al siguiente:

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Generación e implementación de modelos en Estudio de aprendizaje automático de Azure
Se está ahora listo toobuild e implementa un modelo que predice si no se le paga una sugerencia con aprendizaje automático de Azure. datos de ejemplo estratificado Hello están listo toobe utilizado en esta clasificación binaria (sugerencia o no) problema. Hola modelos predictivos con clasificación multiclase (tip_class) y regresión (tip_amount) también se generó e implantó estudio de aprendizaje automático de Azure, pero sólo le mostramos cómo usar casos de toohandle Hola Hola modelo de clasificación binaria.

1. Obtener datos de hello en aprendizaje automático de Azure con hello **importar datos** módulo, disponibles en hello **datos de entrada y salida** sección. Para obtener más información, vea hello [módulo importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) página de referencia.
2. Seleccione **consulta de Hive** como hello **origen de datos** en hello **propiedades** panel.
3. Hola pegar después de script de Hive en hello **consulta de base de datos de Hive** editor
   
        select * from nyc_stratified_sample;
4. Escriba el clúster de URI de HDInsight de hello (Esto puede encontrarse en el Portal de Azure), las credenciales de Hadoop, ubicación de datos de salida y el nombre de contenedor/nombre/clave de cuenta de almacenamiento de Azure.
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

En la figura de Hola a continuación se muestra un ejemplo de un experimento de clasificación binaria leer los datos de tabla de Hive.

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

Una vez creado el experimento de hello, haga clic en **configurar el servicio de Web** --> **predictivo servicio Web**

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

La puntuación del experimento, cuando termine, haga clic en ejecución Hola crea automáticamente **implementar el servicio de Web**

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

panel del servicio web Hola aparecerá en breve:

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Resumen
Al completar este tutorial, ha creado un entorno de ciencia de datos para generar soluciones completas escalables en Azure Data Lake. Este entorno fue tooanalyze usa un conjunto de datos público grande, vamos a través de pasos canónica Hola Hola proceso de ciencia de datos, de adquisición de datos a través de entrenamiento del modelo, y, a continuación, modelo de implementación toohello de hello como un servicio web. U-SQL era tooprocess usado, explorar y Hola datos de ejemplo. Python y Hive usan con toobuild de estudio de aprendizaje automático de Azure e implementación modelos de predicción.

## <a name="whats-next"></a>Pasos siguientes
ruta de acceso de aprendizaje de Hola la [proceso de ciencia de datos de equipo (TDSP)](http://aka.ms/datascienceprocess) proporciona tootopics de vínculos que describen cada uno paso a paso Hola avanzada de proceso de análisis. Hay una serie de tutoriales que se detallan en hello [tutoriales de proceso de ciencia de datos de equipo](data-science-process-walkthroughs.md) página ese showcase cómo toouse recursos y servicios en varios escenarios de análisis predictivos:

* [Hola proceso de ciencia de datos de equipo en acción: con almacenamiento de datos SQL](machine-learning-data-science-process-sqldw-walkthrough.md)
* [Hola proceso de ciencia de datos de equipo en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md)
* [Hola proceso de ciencia de datos de equipo: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Información general del uso de proceso de ciencia de datos de hello inspirará en HDInsight de Azure](machine-learning-data-science-spark-overview.md)

