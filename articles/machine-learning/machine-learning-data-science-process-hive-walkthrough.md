---
title: "aaaExplore datos en un Hadoop de clúster y crear modelos de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Con hello proceso de ciencia de datos de equipo para un escenario de extremo a emplear un Hadoop de HDInsight toobuild de clúster e implementar un modelo mediante un conjunto de datos disponible públicamente."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>Hola proceso de ciencia de datos de equipo en acción: clústeres de Hadoop de HDInsight de Azure de uso
En este tutorial, usamos hello [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md) en un escenario de extremo a extremo mediante un [clúster de HDInsight Hadoop de Azure](https://azure.microsoft.com/services/hdinsight/) toostore, explorar y las características de datos de ingeniería de hello públicamente disponible [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) datos Hola de ejemplo del conjunto de datos y toodown. Se generan los modelos de datos de hello con aprendizaje automático de Azure toohandle multiclase y binarias clasificación y regresión tareas de predicción.

Para ver un tutorial que muestra cómo toohandle clústeres de un conjunto de datos mayor (1 terabyte) para un escenario similar con Hadoop de HDInsight para el procesamiento de datos, vea [proceso de ciencia de datos de equipo - con clústeres de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).

También es posible toouse un hello tooaccomplish de Bloc de notas de IPython tareas Tutorial Hola presentado con conjunto de datos de 1 TB de Hola. Los usuarios que serían como tootry debe consultar este enfoque Hola [tutorial Criteo mediante una conexión ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tema.

## <a name="dataset"></a>Descripción del conjunto de datos NYC Taxi Trips
Hola datos NYC Taxi recorridos es de aproximadamente 20GB comprimido valores separados por comas (CSV) de archivos de (~ 48GB sin comprimir), que incluye más de 173 millones hello y viajes individuales puntuación de pago para cada recorrido. Cada registro de ida y vuelta incluye ubicación de entrega y recogida de Hola y tiempo, hack anonimizado (controlador) número de licencia y número medallion (identificador único del taxi). datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:

1. archivos CSV de Hello 'trip_data' contienen detalles de ida y vuelta, como el número de los pasajeros, recogida y puntos de caída, duración de ida y vuelta y duración del viaje. Estos son algunos registros de ejemplo:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. archivos CSV de Hello 'trip_fare' contienen detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago. Estos son algunos registros de ejemplo:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

recorridos de toojoin de clave única de Hello\_datos y recorridos\_tarifa se compone de campos de hello: medallion, prueba\_licencia y recogida\_fecha y hora.

tooget todas las de ida y vuelta determinado Hola detalles tooa relevante, es suficiente toojoin con tres claves: Hola "medallion", "hack\_licencia" y "recogida\_datetime".

Se describen algunos detalles más de los datos de hello cuando se almacenarlos en tablas de Hive en breve.

## <a name="mltasks"></a>Ejemplos de tareas de predicción
Cuando planee los datos, determinar tipo hello de predicciones que desee toomake en función de su análisis ayuda a aclarar las tareas de Hola que necesitará tooinclude en el proceso.
Presentamos tres ejemplos de problemas de predicción que se abordan en este tutorial cuyo formulación se basa en hello *sugerencia\_cantidad*:

1. **Clasificación binaria**: permite predecir si se pagó una propina tras una carrera, o no; es decir, un valor de *tip\_amount* mayor que 0 $ es un ejemplo positivo, mientras que un valor de *tip\_amount* de 0 $ es un ejemplo negativo.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Clasificación multiclase**: intervalo de hello toopredict de cantidades de sugerencia de pago para recorridos de Hola. Se divide hello *sugerencia\_cantidad* en cinco bandejas o clases:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Tarea de regresión**: cantidad de hello toopredict de sugerencia de Hola de pago para un recorrido.  

## <a name="setup"></a>Configuración de un clúster de Hadoop de HDInsight para el análisis avanzado
> [!NOTE]
> Esta tarea la suelen hacer los **administradores** .
> 
> 

Puede configurar un entorno de Azure para análisis avanzado que emplee un clúster de HDInsight en tres pasos:

1. [Cree una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md): esta cuenta de almacenamiento se utiliza para almacenar datos en el almacenamiento de blobs de Azure. datos de Hello usados en clústeres de HDInsight también se encuentran aquí.
2. [Personalizar Hadoop de HDInsight de Azure para hello de clústeres de proceso de análisis avanzado y la tecnología](machine-learning-data-science-customize-hadoop-cluster.md). Este paso crea un clúster de Hadoop de HDInsight de Azure con Anaconda Python 2.7 de 64 bits instalado en todos los nodos. Hay dos tooremember pasos importantes al personalizar su clúster de HDInsight.
   
   * Recordar cuenta de almacenamiento de hello toolink creada en el paso 1 con el clúster de HDInsight al crearla. Esta cuenta de almacenamiento es tooaccess usa datos que se procesan en los clústeres de Hola.
   * Después de crea el clúster de hello, habilitar el nodo principal de acceso remoto toohello de clúster de Hola. Navegue toohello **configuración** ficha y haga clic en **habilitar de forma remota**. Este paso especifica las credenciales de usuario de Hola utilizadas para inicio de sesión remoto.
3. [Crear un área de trabajo de aprendizaje automático de Azure](machine-learning-create-workspace.md): aprendizaje automático de Azure esta área de trabajo es los modelos de aprendizaje automático de toobuild usado. Esta tarea se dirige después de completar una exploración de datos iniciales y hacia abajo de muestreo con clúster de HDInsight Hola.

## <a name="getdata"></a>Obtener datos de Hola desde un origen público
> [!NOTE]
> Esta tarea la suelen hacer los **administradores** .
> 
> 

Hola tooget [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos desde su ubicación pública, puede usar cualquiera de los métodos de hello descritos en [tooand de mover los datos desde el almacenamiento de blobs de Azure](machine-learning-data-science-move-azure-blob.md) máquina tooyour de toocopy Hola datos.

Aquí se describe cómo los archivos que contiene los datos de uso AzCopy tootransfer Hola. toodownload e instale AzCopy siguen las instrucciones de hello en [Introducción a la utilidad de línea de comandos de AzCopy hello](../storage/common/storage-use-azcopy.md).

1. Desde una ventana del símbolo del sistema, emitir Hola siguientes comandos de AzCopy, reemplazar *< path_to_data_folder >* con destino deseado de hello:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Cuando se completa la copia de hello, son un total de 24 archivos comprimidos en la carpeta de datos de hello seleccionada. Descomprima Hola descargan archivos toohello mismo directorio en el equipo local. Tome nota de carpeta Hola donde residen los archivos de hello sin comprimir. Esta carpeta será la que se hace referencia tooas Hola *< ruta de acceso\_a\_unzipped_data\_archivos\>*  es lo que sigue.

## <a name="upload"></a>Cargar el contenedor de hello datos toohello predeterminado del clúster de Hadoop de HDInsight de Azure
> [!NOTE]
> Esta tarea la suelen hacer los **administradores** .
> 
> 

Hola siguientes comandos de AzCopy, reemplace Hola siguientes parámetros con valores reales de Hola que especificó al crear el clúster de Hadoop de Hola y descomprimir archivos de datos de Hola.

* ***&#60; path_to_data_folder >*** directory hello (junto con la ruta de acceso) en el equipo que contienen archivos de datos de hello descomprimió  
* ***&#60; nombre de cuenta de almacenamiento de clúster de Hadoop >*** Hola cuenta de almacenamiento asociada al clúster de HDInsight
* ***&#60; contenedor predeterminado del clúster de Hadoop >*** contenedor de hello predeterminado utilizado por el clúster. Tenga en cuenta que nombre hello predeterminado Hola contenedor suele ser Hola mismo nombre como el propio clúster Hola. Por ejemplo, si el clúster de Hola se llama "abc123.azurehdinsight.net", contenedor predeterminado de hello es abc123.
* ***&#60; clave de la cuenta de almacenamiento >*** Hola clave Hola cuenta de almacenamiento utilizado por el clúster

Desde un símbolo del sistema o una ventana de Windows PowerShell en el equipo, ejecute hello siguiendo dos comandos de AzCopy.

Este comando carga los datos de ida y vuelta de hello demasiado***nyctaxitripraw*** directorio en el contenedor de predeterminado de hello del clúster de Hadoop de Hola.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

Este comando carga los datos de la tarifa de hello demasiado***nyctaxifareraw*** directorio en el contenedor de predeterminado de hello del clúster de Hadoop de Hola.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

datos de Hello ahora deberían en almacenamiento de blobs de Azure y listo toobe consumida en clúster de HDInsight Hola.

## <a name="#download-hql-files"></a>Inicie sesión en el nodo principal de Hola de clúster de Hadoop y y preparar para el análisis de exploración de datos
> [!NOTE]
> Esta tarea la suelen hacer los **administradores** .
> 
> 

tooaccess Hola del nodo principal del clúster de hello para el análisis de exploración de datos y hacia abajo de muestreo de datos de hello, siga procedimiento Hola descrito en [Hola de acceso principal del nodo de clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

En este tutorial, se usan principalmente las consultas escritas [Hive](https://hive.apache.org/), un lenguaje de consulta similar a SQL, exploraciones de datos preliminares de tooperform. consultas de Hive Hola se almacenan en archivos de .hql. A continuación, se abajo ejemplo este toobe de datos que se usan en aprendizaje automático de Azure para generar modelos.

tooprepare el clúster de hello para el análisis de exploración de datos, se descargar archivos de .hql de Hola que contengan scripts de Hive relevantes de Hola de [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa directorio local (C:\temp) en el nodo principal de Hola. toodo, abra hello **símbolo** desde Hola nodo principal de Hola Hola de clúster y el problema siguiendo dos comandos:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Estos dos comandos descargarán todos los archivos de .hql necesarios en este directorio local de tutorial toohello ***C:\temp &#92;*** en el nodo principal de Hola.

## <a name="#hive-db-tables"></a>Creación de base de datos y tablas de Hive con particiones por mes
> [!NOTE]
> Esta tarea la suelen hacer los **administradores** .
> 
> 

Ahora estamos listos toocreate Hive tablas para el conjunto de datos de Nueva York taxi.
En el nodo principal de Hola de clúster de Hadoop de hello, abra hello ***línea de comandos de Hadoop*** en Hola escritorio del nodo principal de Hola y escriba el directorio del subárbol de hello escribiendo el comando de Hola

    cd %hive_home%\bin

> [!NOTE]
> **Ejecutar todos los comandos de Hive en este tutorial de Hola por encima de la Papelera de Hive / símbolo del sistema de directorio. De esta manera, cualquier problema con la ruta de acceso se solucionará automáticamente. Usamos Hola términos "Prompt de directorio de Hive", "Hive bin / símbolo del sistema de directorio" y "línea de comandos de Hadoop" indistintamente en este tutorial.**
> 
> 

En el símbolo del sistema de hello subárbol de directorio, escriba Hola siguiente comando de línea de comandos de Hadoop de tablas y Hola nodo principal toosubmit Hola Hive consultar toocreate Hive base de datos:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Aquí es contenido de Hola de hello ***C:\temp\sample\_hive\_crear\_db\_y\_tables.hql*** archivos que crea la base de datos de Hive ***nyctaxidb *** y tablas ***recorridos*** y ***tarifa***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Este script de Hive crea dos tablas:

* tabla de "recorrido" Hello contiene detalles de ida y vuelta de cada carrera (detalles del controlador, hora de recopilación, distancia de viaje y veces)
* tabla de "tarifa" Hello contiene los detalles de tarifa (cantidad de tarifa, cantidad de sugerencia, peajes y suplementos).

Si necesita ayuda adicional con estos procedimientos o quiere tooinvestigate otras alternativas, vea la sección de hello [consultas de Hive enviar directamente desde Hola línea de comandos de Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Cargar las tablas de tooHive de datos con particiones
> [!NOTE]
> Esta tarea la suelen hacer los **administradores** .
> 
> 

el conjunto de datos de Hello NYC taxi tiene una partición natural por mes, lo que usamos tooenable tiempos de procesamiento y consulta más rápidos. Hola los siguientes comandos de PowerShell (emitidas desde el directorio de Hive de hello mediante hello **línea de comandos de Hadoop**) cargar datos toohello "recorrido" y "tarifa" Hive las tablas con particiones por mes.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Hola *ejemplo\_hive\_cargar\_datos\_por\_partitions.hql* archivo contiene siguiente hello **cargar** comandos.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Tenga en cuenta que un número de consultas de Hive que aquí utilizamos en proceso de exploración de hello implica la búsqueda en una sola partición o en solo un par de particiones. Pero estas consultas se pudieron ejecutar a través de los datos completos de Hola.

### <a name="#show-db"></a>Mostrar bases de datos en clúster de Hadoop de HDInsight de Hola
tooshow Hola bases de datos creadas en clúster de Hadoop de HDInsight dentro de la ventana de línea de comandos de Hadoop de hello, ejecute el siguiente comando de línea de comandos de Hadoop de Hola:

    hive -e "show databases;"

### <a name="#show-tables"></a>Mostrar tablas de Hive de hello en la base de datos de hello nyctaxidb
tooshow Hola tablas hello nyctaxidb base de datos, ejecute el siguiente comando de línea de comandos de Hadoop de Hola:

    hive -e "show tables in nyctaxidb;"

Esto se puede confirmar que las tablas de hello tienen particiones emitiendo el comando de Hola a continuación:

    hive -e "show partitions nyctaxidb.trip;"

Hola espera el resultado se muestra a continuación:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

De igual forma, es posible asegurarse de que esa tabla de tarifa hello tiene particiones emitiendo el comando de Hola a continuación:

    hive -e "show partitions nyctaxidb.fare;"

Hola espera el resultado se muestra a continuación:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Exploración de datos e ingeniería de características en Hive
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Hola exploración de datos y la característica de tareas de ingeniería para hello datos cargados en tablas de Hive Hola pueden realizarse mediante consultas de Hive. Estos son ejemplos de dichas tareas por que las que le guiaremos en esta sección:

* Ver los registros de 10 principales de hello en ambas tablas.
* Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.
* Investigue la calidad de los datos de los campos de longitud y latitud de Hola.
* Generar etiquetas de clasificación multiclase y binaria basándose en hello **sugerencia\_cantidad**.
* Generar características y calcula las distancias Hola directa de ida y vuelta.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Exploración: Vista Hola top 10 registros en el recorrido de tabla
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

toosee aspecto qué datos hello, examinamos 10 registros de cada tabla. Ejecute hello siguientes dos consultas por separado de símbolo del sistema de hello subárbol de directorio en los registros de hello línea de comandos de Hadoop consola tooinspect Hola.

tooget Hola top 10 registros en la tabla de Hola "recorrido" de Hola y primer mes:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget Hola top 10 registros de hello tabla "tarifa" de hello primer mes:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

A menudo es útil toosave Hola el archivo de tooa de registros para su visualización adecuada. Un toohello pequeño cambio por encima de la consulta para hacerlo:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Exploración: Número de Hola vista de registros en cada uno de los 12 particiones de Hola
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Hola cómo varía el número de Hola de viajes de durante el año natural de hello es interesante. Agrupar por mes nos permite toosee el aspecto de esta distribución de viajes.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Esto nos da salida de hello:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

En este caso, Hola primera columna es el mes de Hola y Hola en segundo lugar es número Hola de viajes de durante ese mes.

Se podemos contar Hola número total de registros en nuestro conjunto de datos de ida y vuelta mediante la emisión de hello siguiente comando en el símbolo del sistema de hello subárbol de directorio.

    hive -e "select count(*) from nyctaxidb.trip;"

El resultado es:

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

Comandos toothose similar que se muestra para el conjunto de datos de ida y vuelta de hello, podemos emitir consultas de Hive de hello Hive directory pedir Hola tarifa datos toovalidate Hola número establecido de registros.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Esto nos da salida de hello:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Tenga en cuenta que Hola exacta mismo número de viajes por mes se devuelve para los dos conjuntos de datos. Esto proporciona la validación primera Hola ese Hola datos se han cargado correctamente.

Contando Hola número total de registros en el conjunto de datos de tarifa de hello puede realizarse con el comando de Hola a continuación del símbolo del sistema de hello subárbol de directorio:

    hive -e "select count(*) from nyctaxidb.fare;"

El resultado es:

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

número total de Hola de registros en ambas tablas también se Hola mismo. Esto proporciona una validación segundo ese Hola datos se han cargado correctamente.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploración: distribución de carreras por licencia
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Este ejemplo identifica medallion Hola (números de taxi) con más de 100 viajes dentro de un período de tiempo determinado. ventajas de la consulta de Hola de hello partición acceso a la tabla porque está condicionado por la variable de la partición de hello **mes**. resultados de la consulta de Hola se escriben tooa archivo local queryoutput.tsv `C:\temp` en el nodo principal de Hola.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Aquí es contenido de Hola de *ejemplo\_hive\_recorridos\_recuento\_por\_medallion.hql* archivo para su inspección.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

medallion Hola Hola NYC taxi conjunto de datos identifica un único archivo cab. Se puede identificar qué taxis trabajan más preguntando cuáles realizaron más de un determinado número de carreras en un período de tiempo determinado. Hello en el ejemplo siguiente se identifica archivos CAB que realizan viajes de más de cien en hello primeros tres meses y guarda Hola resultados tooa local archivo de consulta C:\temp\queryoutput.tsv.

Aquí es contenido de Hola de *ejemplo\_hive\_recorridos\_recuento\_por\_medallion.hql* archivo para su inspección.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

De hello subárbol símbolo del sistema de directorio, problema Hola comando a continuación:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploración: distribución de carreras por medallion y hack_license
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Al explorar un conjunto de datos, con frecuencia se requiere número de hello tooexamine de co-repeticiones de grupos de valores. En esta sección se proporcionan un ejemplo de cómo toodo esto en archivos .cab y controladores.

Hola *ejemplo\_hive\_recorridos\_recuento\_por\_medallion\_license.hql* archivo agrupa los datos de la tarifa de hello establecida en "medallion" y "hack_license" y devuelve recuentos de cada combinación. A continuación se muestra su contenido.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Esta consulta devuelve combinaciones de taxi y conductor determinado ordenadas por número descendente de carreras.

De hello Hive indicador del directorio, ejecute:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

resultados de la consulta de Hola se escriben archivo local tooa C:\temp\queryoutput.tsv.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Exploración: Evaluación de la calidad de los datos mediante la comprobación de registros con latitud/longitud no válida
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Un objetivo comunes de análisis de exploración de datos es tooweed los registros no válidos o es incorrectos. Hello ejemplo de esta sección determina si bien hello campos de longitud o latitud contienen un valor fuera del área de Nueva York Hola. Puesto que es probable que estos registros tengan los valores de longitud y latitud erróneos, queremos tooeliminate de cualquier dato que sea toobe utilizados para el modelado.

Este es el contenido de Hola de *ejemplo\_hive\_calidad\_assessment.hql* archivo para su inspección.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


De hello Hive indicador del directorio, ejecute:

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Hola *-S* argumento incluido en este comando suprime la copia impresa de pantalla del estado de Hola de trabajos de Hive asignación y reducción de Hola. Esto es útil porque dificulta la impresión de la pantalla de Hola de hello Hive resultado de la consulta sea más legible.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Exploración: Distribuciones de clase binaria de las propinas de las carreras
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Problema de clasificación binaria de hello descrito en hello [ejemplos de tareas de predicción](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sección, resulta útil tooknow si se proporcionó una sugerencia o no. Esta distribución de las propinas es binaria:

* Propina dada (clase 1, tip\_amount > 0 $).  
* Sin propina (clase 0, tip\_amount = 0 $).

Hola *ejemplo\_hive\_superpuesto\_frequencies.hql* archivo se muestra a continuación para ello.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

De hello Hive indicador del directorio, ejecute:

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>Exploración: Clase distribuciones en configuración de hello multiclase
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Problema de clasificación multiclase Hola descrito en hello [ejemplos de tareas de predicción](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sección este conjunto de datos también se presta tooa clasificación natural que nos gustaría toopredict cantidad de Hola de sugerencias de hello dada. Podemos usar ubicaciones toodefine sugerencia intervalos de consulta de Hola. tooget Hola distribuciones de clase de hello distintos intervalos de sugerencia, usaremos hello *ejemplo\_hive\_sugerencia\_intervalo\_frequencies.hql* archivo. A continuación se muestra su contenido.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Ejecute el siguiente comando desde la consola de línea de comandos de Hadoop de hello:

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Exploración: Cálculo de la distancia directa entre dos ubicaciones de longitud y latitud de proceso
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Tener una medida de distancia directa Hola nos permite toofind out discrepancia de hello entre él y Hola real distancia de viaje. Esta característica se promoverá, señale que pasajeros pueden ser menor probable información sobre herramientas si pueda determinar dicho controlador Hola intencionadamente las ha tomado por una ruta más larga.

comparación de hello toosee entre hello y distancia de viaje real [distancia Haversine](http://en.wikipedia.org/wiki/Haversine_formula) entre dos puntos longitud-latitud (distancia de Hola "great círculo"), usamos funciones trigonométricas de hello disponibles dentro de Hive, por lo tanto:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

En la consulta de hello anterior, R es el radio Hola Hola tierra en millas y pi es tooradians convertido. Tenga en cuenta que puntos longitud-latitud de hello tooremove "filtrado" valores que están lejos de área de Nueva York Hola.

En este caso, escribimos nuestro directorio de tooa de resultados llamado "queryoutputdir". Hello secuencia de comandos que se muestra a continuación, primero crea este directorio de salida y, a continuación, ejecuta el comando de Hive de Hola.

De hello Hive indicador del directorio, ejecute:

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Hello resultados de la consulta se escriben los blobs de Azure too9 ***queryoutputdir/000000\_0*** demasiado ***queryoutputdir/000008\_0*** en contenedor de hello predeterminado del clúster de Hadoop de Hola.

tamaño de hello toosee de blobs individuales de hello, ejecutamos Hola siguiente comando desde el símbolo del sistema de hello subárbol de directorio:

    hdfs dfs -ls wasb:///queryoutputdir

contenido de hello toosee de un archivo determinado, diga 000000\_0, usamos de Hadoop `copyToLocal` comando, por lo tanto.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> `copyToLocal` puede ser muy lento para archivos de gran tamaño y no se recomienda para su uso con ellos.  
> 
> 

Una ventaja clave de tener estos datos residen en un blob de Azure es que podemos exploramos datos hello en aprendizaje automático de Azure con hello [importar datos] [ import-data] módulo.

## <a name="#downsample"></a>Reducción de datos y creación de modelos en Aprendizaje automático de Azure
> [!NOTE]
> Esta tarea la suelen hacer los **científicos de datos** .
> 
> 

Después de la fase de análisis de datos de exploración de hello, ahora estamos listos toodown datos de Hola de ejemplo para generar modelos de aprendizaje automático de Azure. En esta sección, se muestra cómo consultar los datos de toodown ejemplo hello, que, a continuación, se obtiene acceso desde hello toouse un subárbol [importar datos] [ import-data] módulo aprendizaje automático de Azure.

### <a name="down-sampling-hello-data"></a>Profundidad de muestreo de datos de Hola
Este procedimiento incluye dos pasos. En primer lugar se unir hello **nyctaxidb.trip** y **nyctaxidb.fare** tablas en tres claves que están presentes en todos los registros: "medallion", "hack\_licencia", y "recogida\_datetime". Después se genera una etiqueta de clasificación binaria **tipped** y una etiqueta de clasificación de múltiples clases **tip\_class**.

toobe toouse capaz de hello hacia abajo de los datos muestreados directamente desde hello [importar datos] [ import-data] módulo aprendizaje automático de Azure, es necesario toostore resultados de Hola de hello por encima de la tabla de Hive interno de consulta tooan. En la información siguiente, se crea una tabla interna de Hive y rellena su contenido con hello Unido y hacia abajo de los datos de ejemplo.

consulta Hello aplica funciones de Hive estándares directamente toogenerate hora Hola del día, semana del año, semana (el lunes es 1 y 7 es el domingo) de Hola "recogida\_datetime" campo y Hola distancia directa entre la recogida de Hola y caída ubicaciones. Los usuarios pueden consultar demasiado[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) para obtener una lista completa de dichas funciones.

Hola consulta, a continuación, el detalle de datos de saludo de ejemplos para que los resultados de la consulta de hello pueden caber en hello estudio de aprendizaje automático de Azure. Se importa solo 1% del conjunto de datos original de Hola Hola Studio.

A continuación se muestran contenido Hola de *ejemplo\_hive\_preparar\_para\_aml\_full.hql* archivo que prepara los datos para el modelo de creación de aprendizaje automático de Azure.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

Esta consulta, del directorio del subárbol de hello solicitar al toorun:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Ahora tenemos una tabla interna "nyctaxidb.nyctaxi_downsampled_dataset", que se puede acceder mediante hello [importar datos] [ import-data] módulo de aprendizaje automático de Azure. También se puede utilizar este conjunto de datos para generar modelos de Aprendizaje automático.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Usar módulo de importar datos de Hola Hola de aprendizaje automático de Azure tooaccess hacia abajo de los datos de ejemplo
Como requisitos previos para emitir consultas de Hive en hello [importar datos] [ import-data] módulo de aprendizaje automático de Azure, se necesita acceso de área de trabajo de aprendizaje automático de Azure tooan y tener acceso a las credenciales de toohello de hello clúster y su cuenta de almacenamiento asociada.

Algunos detalles de hello [importar datos] [ import-data] hello y módulo tooinput de parámetros:

**URI del servidor de HCatalog**: si el nombre del clúster de hello es abc123, esto es simplemente: https://abc123.azurehdinsight.net

**Nombre de cuenta de usuario de Hadoop** : nombre de usuario de hello elegido para el clúster de hello (**no** nombre de usuario de acceso remoto de hello)

**Contraseña de cuenta de usuario de Hadoop** : contraseña de hello elegido para el clúster de hello (**no** contraseña de acceso remoto de hello)

**Ubicación de los datos de salida** : Esto se elige toobe Azure.

**Nombre de la cuenta de almacenamiento de Azure** : nombre de cuenta de almacenamiento predeterminada de hello asociada Hola clúster.

**Nombre de contenedor de Azure** : Esto es nombre de contenedor predeterminado de Hola para clúster hello y normalmente es Hola mismo como el nombre del clúster de Hola. En un clúster denominado "abc123", es abc123.

> [!IMPORTANT]
> **Cualquier tabla deseamos tooquery con hello [importar datos] [ import-data] módulo aprendizaje automático de Azure debe ser una tabla interna.** Una manera de determinar si una tabla T en una base de datos D.db es una tabla interna es la siguiente.
> 
> 

De hello subárbol símbolo del sistema de directorio, problema Hola comando:

    hdfs dfs -ls wasb:///D.db/T

Si la tabla de hello es una tabla interna y se rellena, su contenido debe mostrar aquí. Otro toodetermine de manera que si una tabla es una tabla interna es toouse Hola Explorador de almacenamiento de Azure. Usar nombre del contenedor predeterminado toonavigate toohello de clúster de Hola y, a continuación, filtrar por nombre de la tabla de Hola. Si la tabla de Hola y su contenido se muestra, Esto confirma que es una tabla interna.

Ésta es una instantánea de la consulta de Hive de Hola y Hola [importar datos] [ import-data] módulo:

![Consulta de Hive para el módulo de importación de datos](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Tenga en cuenta que desde nuestro abajo los datos muestreados residen en el contenedor predeterminado de hello, consulta de Hive resultante Hola de aprendizaje automático de Azure es muy simple y es un "seleccionar * de nyctaxidb.nyctaxi\_reduce\_datos".

conjunto de datos de Hello ahora puede utilizarse como punto de partida para generar modelos de aprendizaje automático de Hola.

### <a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure
Ahora estamos tooproceed capaz de toomodel creación e implementación de modelo en [aprendizaje automático de Azure](https://studio.azureml.net). Hola datos están listos para que podamos toouse para resolver problemas de predicción de hello arriba indicados:

**1. Clasificación binaria**: toopredict o no se pagó una sugerencia para un recorrido.

**Lector usado** : regresión logística de dos clases

a. En este problema la etiqueta de destino (o clase) es "tipped". El conjunto de datos reducido original incluye algunas columnas que no contienen datos para el experimento de clasificación. En concreto: sugerencia\_de clases, sugerencia\_cantidad y total\_importe revelar información acerca de la etiqueta de destino de Hola que no está disponible en el tiempo de prueba. Se quite estas columnas de cuenta con hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.

en la instantánea de Hola a continuación se muestra nuestra toopredict experimento o no se pagó una sugerencia para un recorrido dado.

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. En este experimento las distribuciones de la etiqueta de destino eran aproximadamente 1:1.

instantánea de Hello siguiente muestra la distribución de Hola de las etiquetas de clase de sugerencia de problema de clasificación binaria de Hola.

![Distribución de las etiquetas de clase de sugerencia](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

Como resultado, obtenemos un AUC de 0.987 tal y como se muestra en la siguiente ilustración de Hola.

![Valor de AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Clasificación multiclase**: las clases definidas por el intervalo de hello toopredict de cantidades de sugerencia de pago de ida y vuelta hello, utilizaba anteriormente Hola.

**Lector usado** : regresión logística de múltiples clases

a. En este problema, la etiqueta de destino (o clase) es "tip\_class", que puede adoptar uno de cinco valores (0,1,2,3,4). Como en el caso de clasificación binaria de hello, tenemos unas pocas columnas que son las pérdidas de destino para este experimento. En concreto: superpuesto, sugerencia\_importe total\_importe revelar información acerca de la etiqueta de destino de Hola que no está disponible en el tiempo de prueba. Quitamos estas columnas con hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.

Hola instantánea siguiente muestra nuestra toopredict experimento en qué bin una sugerencia es probable toofall (clase 0: sugerencia = $0, 1 de la clase: Sugerencia > $0 y sugerencia < = $5, clase 2: Sugerencia > $5 y en la sugerencia < = $10, 3 de la clase: Sugerencia > $10 y en la sugerencia < = 20 $ Clase 4: Sugerencia > $20)

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Ahora vemos qué aspecto tiene nuestra distribución de clases de prueba real. Vemos que aunque clase 0 y 1 de la clase son muy extendido, hello otras clases son poco frecuentes.

![Distribución de la clase de prueba](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. Para este experimento, usamos un toolook de matriz de confusión en nuestro precisiones de predicción. Esto se muestra a continuación.

![Matriz de confusión](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Tenga en cuenta que mientras nuestro precisiones de clase en clases de hello frecuente es bastante bueno, modelo hello no hacer un buen trabajo de "aprendizaje" en las clases de hello poco frecuentes.

**3. Tarea de regresión**: cantidad de hello toopredict de sugerencia de pago para un recorrido.

**Lector usado** : árbol de decisión incrementado

a. En este problema la etiqueta de destino (o clase) es "tip\_amount". En este caso son nuestra pérdidas de destino: superpuesto, sugerencia\_(clase), total\_cantidad; todas estas variables revelar información acerca de la cantidad de sugerencia de Hola que no está disponible normalmente en el tiempo de prueba. Quitamos estas columnas con hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.

Hola instantánea belows muestra nuestra cantidad de Hola de toopredict de experimento de hello dada la sugerencia.

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. Para los problemas de regresión, se medir precisiones Hola de nuestro predicción examinando error Hola cuadrado en predicciones hello, Hola coeficiente de determinación y Hola como. Lo mostramos a continuación.

![Estadísticas de predicción](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Vemos que sobre Hola coeficiente de determinación es 0.709, lo que implica aproximadamente el 71% de variación de Hola se explica por nuestro coeficientes de modelo.

> [!IMPORTANT]
> toolearn más información acerca de aprendizaje automático de Azure y cómo tooaccess y usarla, consulte demasiado[¿qué es aprendizaje automático?](machine-learning-what-is-machine-learning.md). Un recurso muy útil para reproducir con un montón de experimentos de aprendizaje automático en aprendizaje automático de Azure es hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/). Galería de Hello cubre una gama de experimentos y proporciona una introducción completa a intervalo de Hola de capacidades de aprendizaje automático de Azure.
> 
> 

## <a name="license-information"></a>Información de licencia
En este tutorial de ejemplo y sus secuencias de comandos que lo acompaña se comparten entre Microsoft bajo licencia MIT de Hola. Compruebe archivo LICENSE.txt de hello directorio de hello del código de ejemplo de Hola en GitHub para obtener más detalles.

## <a name="references"></a>Referencias
•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)  
•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
