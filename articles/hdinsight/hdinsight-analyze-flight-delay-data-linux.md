---
title: datos de retrasos de vuelos aaaAnalyze con Hive en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hive datos del vuelo tooanalyze en HDInsight basados en Linux, a continuación, exportar Hola datos tooSQL con Sqoop de la base de datos."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Análisis de datos de retraso de vuelos mediante Hive en HDInsight basado en Linux

Obtenga información acerca de cómo los datos de retrasos de vuelos tooanalyze con Hive en HDInsight basados en Linux, a continuación, exportación Hola datos tooAzure base de datos SQL mediante Sqoop.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="prerequisites"></a>Requisitos previos

* **Un clúster de HDInsight**. Vea [Introducción al uso de Hadoop con Hive en HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md) para conocer los pasos sobre la creación de un clúster de HDInsight basado en Linux.

* **Base de datos de SQL Azure**. Use una instancia de Azure SQL Database como almacén de datos de destino. Si no dispone todavía de una Base de datos SQL, consulte [Tutorial de Base de datos SQL: creación de una Base de datos SQL en cuestión de minutos](../sql-database/sql-database-get-started.md).

* **CLI de Azure** Si no ha instalado Hola CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) para conocer los pasos más.

## <a name="download-hello-flight-data"></a>Descargar datos del vuelo Hola

1. Examinar demasiado[investigación y administración de tecnología innovadora, centro de transporte estadísticas][rita-website].

2. En página de hello, seleccione Hola siguientes valores:

   | Nombre | Valor |
   | --- | --- |
   | Filter Year |2013 |
   | Filter Period |January |
   | Fields |Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Borrado de los demás campos |

3. Haga clic en **Descargar**.

## <a name="upload-hello-data"></a>Cargar datos de Hola

1. Usar hello después comando tooupload Hola zip archivo toohello HDInsight nodo principal del clúster:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Reemplace **FILENAME** por nombre de hello del archivo zip de Hola. Reemplace **nombre de usuario** con inicio de sesión SSH de hello para el clúster de HDInsight Hola. Reemplace el nombre del clúster por nombre de Hola Hola del clúster de HDInsight.

   > [!NOTE]
   > Si utiliza una contraseña tooauthenticate su inicio de sesión SSH, le pediremos contraseña Hola. Si utiliza una clave pública, puede que necesite toouse hello `-i` parámetro y especificar hello toohello de ruta de acceso que coinciden con la clave privada. Por ejemplo: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Cuando haya completado la carga de hello, conectar clúster toohello mediante SSH:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Una vez conectado, use hello toounzip Hola .zip archivo siguiente:

    ```
    unzip FILENAME.zip
    ```

    Este comando extrae un archivo .csv que tiene un tamaño aproximado de 60 MB.

4. Usar hello siguiente comando toocreate un directorio de almacenamiento de HDInsight y, a continuación, copie el directorio del archivo toohello de hello:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Crear y ejecutar hello HiveQL

Use Hola siguientes pasos le indican tooimport datos desde un archivo CSV hello en una tabla de Hive denominada **retrasos**.

1. Comando toocreate siguiente de Hola de uso y editar un nuevo archivo denominado **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Usar hello después de texto como contenido de Hola de este archivo:

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. archivo de hello toosave, use **Ctrl + X**, a continuación, **Y** .

3. toostart Hive y ejecución hello **flightdelays.hql** de archivos, use el siguiente comando de Hola:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > En este ejemplo, `localhost` se usa ya está conectado toohello del nodo principal del clúster de HDInsight de hello, que es donde se está ejecutando HiveServer2.

4. Una vez Hola __flightdelays.hql__ termine la ejecución, tooopen una sesión interactiva de Beeline de comando siguiente de Hola de uso de la secuencia de comandos:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Cuando aparezca el Hola `jdbc:hive2://localhost:10001/>` símbolo del sistema, use Hola siguientes tooretrieve consultar los datos de los datos de retrasos de vuelos Hola importado.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    Esta consulta recupera una lista de ciudades que retrasos de tiempo con experiencia, junto con el promedio de hello Retrasar hora y la guarda demasiado`/tutorials/flightdelays/output`. Posteriormente, Sqoop lee los datos de Hola desde esta ubicación y exportarlo tooAzure base de datos SQL.

6. tooexit Beeline, escriba `!quit` en el símbolo del sistema de Hola.

## <a name="create-a-sql-database"></a>una Base de datos SQL

Si ya tiene una base de datos de SQL, debe obtener el nombre del servidor de Hola. Puede encontrar el nombre del servidor de Hola Hola [portal de Azure](https://portal.azure.com) seleccionando **bases de datos SQL**, y, a continuación, el filtrado en nombre de Hola de hello de base de datos desea toouse. aparece el nombre del servidor de Hello en hello **SERVER** columna.

Si no dispone de una base de datos de SQL, utilice la información de hello en [tutorial de base de datos SQL: crear una base de datos SQL en minutos](../sql-database/sql-database-get-started.md) toocreate uno. Guardar el nombre del servidor hello usado para la base de datos de Hola.

## <a name="create-a-sql-database-table"></a>Creación de una tabla de Base de datos SQL

> [!NOTE]
> Hay muchas maneras tooconnect tooSQL base de datos y crear una tabla. Hola a consecuencia del uso de pasos [uso](http://www.freetds.org/) de clúster de HDInsight Hola.


1. Usar clústeres de HDInsight basados en Linux SSH tooconnect toohello y ejecución Hola siguiendo los pasos de la sesión de SSH de Hola.

2. Usar hello siguiendo el uso del comando tooinstall:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Una vez que se haya completado la instalación de hello, utilice Hola después el servidor de base de datos SQL de comandos tooconnect toohello. Reemplace **serverName** con el nombre del servidor de base de datos SQL de Hola. Reemplace **adminLogin** y **adminPassword** con inicio de sesión de hello para la base de datos SQL. Reemplace **databaseName** con el nombre de la base de datos de Hola.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Recibir toohello similar de salida siguiente texto:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. En hello `1>` símbolo del sistema, escriba Hola siguientes líneas:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Cuando Hola `GO` instrucción se haya especificado, se evalúan en las instrucciones anteriores Hola. Se crea una tabla denominada **delays** con un índice agrupado.

    Hola de uso después de tooverify de consulta que Hola tabla se ha creado:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Hola de salida es toohello similar siguiente texto:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Escriba `exit` en hello `1>` solicitar utilidad de tooexit Hola tsql.

## <a name="export-data-with-sqoop"></a>Exportación de datos con Sqoop

1. Usar hello después tooverify de comando que Sqoop puede ver la base de datos de SQL:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    Este comando devuelve una lista de bases de datos, incluida la base de datos de Hola que creó anteriormente tabla de retrasos de hello en.

2. Usar hello siguientes comando tooexport datos de tabla de hivesampletable toohello mobiledata:

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop se conecta toohello base de datos que contiene la tabla de retrasos de Hola y exporta los datos de hello `/tutorials/flightdelays/output` tabla de directorios toohello retrasos.

3. Una vez completado el comando de hello, utilice Hola después de la base de datos de tooconnect toohello mediante TSQL:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Una vez conectado, use Hola después tooverify de instrucciones que los datos de hello estaban toohello exportado mobiledata tabla:

    ```
    SELECT * FROM delays
    GO
    ```

    Debería ver una lista de datos de tabla de Hola. Tipo `exit` utilidad de tooexit Hola tsql.

## <a id="nextsteps"></a> Pasos siguientes

toolearn más toowork de formas con los datos de HDInsight, vea Hola siguientes documentos:

* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Oozie con HDInsight][hdinsight-use-oozie]
* [Uso de Sqoop con HDInsight][hdinsight-use-sqoop]
* [Uso de Pig con HDInsight][hdinsight-use-pig]
* [Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]
* [Desarrollo de programas de Hadoop con Python en HDInsight][hdinsight-develop-streaming]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
