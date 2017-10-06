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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="9b706-103">Análisis de datos de retraso de vuelos mediante Hive en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="9b706-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="9b706-104">Obtenga información acerca de cómo los datos de retrasos de vuelos tooanalyze con Hive en HDInsight basados en Linux, a continuación, exportación Hola datos tooAzure base de datos SQL mediante Sqoop.</span><span class="sxs-lookup"><span data-stu-id="9b706-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b706-105">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="9b706-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="9b706-106">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="9b706-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9b706-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9b706-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9b706-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b706-108">Prerequisites</span></span>

* <span data-ttu-id="9b706-109">**Un clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9b706-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="9b706-110">Vea [Introducción al uso de Hadoop con Hive en HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md) para conocer los pasos sobre la creación de un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="9b706-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="9b706-111">**Base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="9b706-111">**Azure SQL Database**.</span></span> <span data-ttu-id="9b706-112">Use una instancia de Azure SQL Database como almacén de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="9b706-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="9b706-113">Si no dispone todavía de una Base de datos SQL, consulte [Tutorial de Base de datos SQL: creación de una Base de datos SQL en cuestión de minutos](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9b706-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="9b706-114">**CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="9b706-114">**Azure CLI**.</span></span> <span data-ttu-id="9b706-115">Si no ha instalado Hola CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) para conocer los pasos más.</span><span class="sxs-lookup"><span data-stu-id="9b706-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="9b706-116">Descargar datos del vuelo Hola</span><span class="sxs-lookup"><span data-stu-id="9b706-116">Download hello flight data</span></span>

1. <span data-ttu-id="9b706-117">Examinar demasiado[investigación y administración de tecnología innovadora, centro de transporte estadísticas][rita-website].</span><span class="sxs-lookup"><span data-stu-id="9b706-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="9b706-118">En página de hello, seleccione Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="9b706-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="9b706-119">Nombre</span><span class="sxs-lookup"><span data-stu-id="9b706-119">Name</span></span> | <span data-ttu-id="9b706-120">Valor</span><span class="sxs-lookup"><span data-stu-id="9b706-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="9b706-121">Filter Year</span><span class="sxs-lookup"><span data-stu-id="9b706-121">Filter Year</span></span> |<span data-ttu-id="9b706-122">2013</span><span class="sxs-lookup"><span data-stu-id="9b706-122">2013</span></span> |
   | <span data-ttu-id="9b706-123">Filter Period</span><span class="sxs-lookup"><span data-stu-id="9b706-123">Filter Period</span></span> |<span data-ttu-id="9b706-124">January</span><span class="sxs-lookup"><span data-stu-id="9b706-124">January</span></span> |
   | <span data-ttu-id="9b706-125">Fields</span><span class="sxs-lookup"><span data-stu-id="9b706-125">Fields</span></span> |<span data-ttu-id="9b706-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="9b706-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="9b706-127">Borrado de los demás campos</span><span class="sxs-lookup"><span data-stu-id="9b706-127">Clear all other fields</span></span> |

3. <span data-ttu-id="9b706-128">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="9b706-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="9b706-129">Cargar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="9b706-129">Upload hello data</span></span>

1. <span data-ttu-id="9b706-130">Usar hello después comando tooupload Hola zip archivo toohello HDInsight nodo principal del clúster:</span><span class="sxs-lookup"><span data-stu-id="9b706-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="9b706-131">Reemplace **FILENAME** por nombre de hello del archivo zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="9b706-132">Reemplace **nombre de usuario** con inicio de sesión SSH de hello para el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="9b706-133">Reemplace el nombre del clúster por nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b706-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9b706-134">Si utiliza una contraseña tooauthenticate su inicio de sesión SSH, le pediremos contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="9b706-135">Si utiliza una clave pública, puede que necesite toouse hello `-i` parámetro y especificar hello toohello de ruta de acceso que coinciden con la clave privada.</span><span class="sxs-lookup"><span data-stu-id="9b706-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="9b706-136">Por ejemplo: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="9b706-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="9b706-137">Cuando haya completado la carga de hello, conectar clúster toohello mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="9b706-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="9b706-138">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9b706-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="9b706-139">Una vez conectado, use hello toounzip Hola .zip archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9b706-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="9b706-140">Este comando extrae un archivo .csv que tiene un tamaño aproximado de 60 MB.</span><span class="sxs-lookup"><span data-stu-id="9b706-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="9b706-141">Usar hello siguiente comando toocreate un directorio de almacenamiento de HDInsight y, a continuación, copie el directorio del archivo toohello de hello:</span><span class="sxs-lookup"><span data-stu-id="9b706-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="9b706-142">Crear y ejecutar hello HiveQL</span><span class="sxs-lookup"><span data-stu-id="9b706-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="9b706-143">Use Hola siguientes pasos le indican tooimport datos desde un archivo CSV hello en una tabla de Hive denominada **retrasos**.</span><span class="sxs-lookup"><span data-stu-id="9b706-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="9b706-144">Comando toocreate siguiente de Hola de uso y editar un nuevo archivo denominado **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="9b706-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="9b706-145">Usar hello después de texto como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="9b706-145">Use hello following text as hello contents of this file:</span></span>

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

2. <span data-ttu-id="9b706-146">archivo de hello toosave, use **Ctrl + X**, a continuación, **Y** .</span><span class="sxs-lookup"><span data-stu-id="9b706-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="9b706-147">toostart Hive y ejecución hello **flightdelays.hql** de archivos, use el siguiente comando de Hola:</span><span class="sxs-lookup"><span data-stu-id="9b706-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="9b706-148">En este ejemplo, `localhost` se usa ya está conectado toohello del nodo principal del clúster de HDInsight de hello, que es donde se está ejecutando HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="9b706-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="9b706-149">Una vez Hola __flightdelays.hql__ termine la ejecución, tooopen una sesión interactiva de Beeline de comando siguiente de Hola de uso de la secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="9b706-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="9b706-150">Cuando aparezca el Hola `jdbc:hive2://localhost:10001/>` símbolo del sistema, use Hola siguientes tooretrieve consultar los datos de los datos de retrasos de vuelos Hola importado.</span><span class="sxs-lookup"><span data-stu-id="9b706-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="9b706-151">Esta consulta recupera una lista de ciudades que retrasos de tiempo con experiencia, junto con el promedio de hello Retrasar hora y la guarda demasiado`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="9b706-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="9b706-152">Posteriormente, Sqoop lee los datos de Hola desde esta ubicación y exportarlo tooAzure base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9b706-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="9b706-153">tooexit Beeline, escriba `!quit` en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="9b706-154">una Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="9b706-154">Create a SQL Database</span></span>

<span data-ttu-id="9b706-155">Si ya tiene una base de datos de SQL, debe obtener el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="9b706-156">Puede encontrar el nombre del servidor de Hola Hola [portal de Azure](https://portal.azure.com) seleccionando **bases de datos SQL**, y, a continuación, el filtrado en nombre de Hola de hello de base de datos desea toouse.</span><span class="sxs-lookup"><span data-stu-id="9b706-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="9b706-157">aparece el nombre del servidor de Hello en hello **SERVER** columna.</span><span class="sxs-lookup"><span data-stu-id="9b706-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="9b706-158">Si no dispone de una base de datos de SQL, utilice la información de hello en [tutorial de base de datos SQL: crear una base de datos SQL en minutos](../sql-database/sql-database-get-started.md) toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="9b706-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="9b706-159">Guardar el nombre del servidor hello usado para la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="9b706-160">Creación de una tabla de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="9b706-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="9b706-161">Hay muchas maneras tooconnect tooSQL base de datos y crear una tabla.</span><span class="sxs-lookup"><span data-stu-id="9b706-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="9b706-162">Hola a consecuencia del uso de pasos [uso](http://www.freetds.org/) de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="9b706-163">Usar clústeres de HDInsight basados en Linux SSH tooconnect toohello y ejecución Hola siguiendo los pasos de la sesión de SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="9b706-164">Usar hello siguiendo el uso del comando tooinstall:</span><span class="sxs-lookup"><span data-stu-id="9b706-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="9b706-165">Una vez que se haya completado la instalación de hello, utilice Hola después el servidor de base de datos SQL de comandos tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="9b706-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="9b706-166">Reemplace **serverName** con el nombre del servidor de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="9b706-167">Reemplace **adminLogin** y **adminPassword** con inicio de sesión de hello para la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9b706-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="9b706-168">Reemplace **databaseName** con el nombre de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="9b706-169">Recibir toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="9b706-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="9b706-170">En hello `1>` símbolo del sistema, escriba Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="9b706-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="9b706-171">Cuando Hola `GO` instrucción se haya especificado, se evalúan en las instrucciones anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="9b706-172">Se crea una tabla denominada **delays** con un índice agrupado.</span><span class="sxs-lookup"><span data-stu-id="9b706-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="9b706-173">Hola de uso después de tooverify de consulta que Hola tabla se ha creado:</span><span class="sxs-lookup"><span data-stu-id="9b706-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="9b706-174">Hola de salida es toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="9b706-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="9b706-175">Escriba `exit` en hello `1>` solicitar utilidad de tooexit Hola tsql.</span><span class="sxs-lookup"><span data-stu-id="9b706-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="9b706-176">Exportación de datos con Sqoop</span><span class="sxs-lookup"><span data-stu-id="9b706-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="9b706-177">Usar hello después tooverify de comando que Sqoop puede ver la base de datos de SQL:</span><span class="sxs-lookup"><span data-stu-id="9b706-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="9b706-178">Este comando devuelve una lista de bases de datos, incluida la base de datos de Hola que creó anteriormente tabla de retrasos de hello en.</span><span class="sxs-lookup"><span data-stu-id="9b706-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="9b706-179">Usar hello siguientes comando tooexport datos de tabla de hivesampletable toohello mobiledata:</span><span class="sxs-lookup"><span data-stu-id="9b706-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="9b706-180">Sqoop se conecta toohello base de datos que contiene la tabla de retrasos de Hola y exporta los datos de hello `/tutorials/flightdelays/output` tabla de directorios toohello retrasos.</span><span class="sxs-lookup"><span data-stu-id="9b706-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="9b706-181">Una vez completado el comando de hello, utilice Hola después de la base de datos de tooconnect toohello mediante TSQL:</span><span class="sxs-lookup"><span data-stu-id="9b706-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="9b706-182">Una vez conectado, use Hola después tooverify de instrucciones que los datos de hello estaban toohello exportado mobiledata tabla:</span><span class="sxs-lookup"><span data-stu-id="9b706-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="9b706-183">Debería ver una lista de datos de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b706-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="9b706-184">Tipo `exit` utilidad de tooexit Hola tsql.</span><span class="sxs-lookup"><span data-stu-id="9b706-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="9b706-185"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b706-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="9b706-186">toolearn más toowork de formas con los datos de HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="9b706-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="9b706-187">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9b706-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9b706-188">[Uso de Oozie con HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="9b706-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="9b706-189">[Uso de Sqoop con HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="9b706-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="9b706-190">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9b706-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9b706-191">[Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9b706-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="9b706-192">[Desarrollo de programas de Hadoop con Python en HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="9b706-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
