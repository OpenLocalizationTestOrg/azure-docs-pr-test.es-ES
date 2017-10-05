---
title: "Análisis de datos de retraso de vuelos con Hive en HDInsight: Azure | Microsoft Docs"
description: Aprenda a usar Hive para analizar datos de vuelos en HDInsight basado en Linux y luego exporte los datos a la Base de datos SQL con Sqoop.
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
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="85f56-103">Análisis de datos de retraso de vuelos mediante Hive en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="85f56-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="85f56-104">Aprenda a analizar datos de retrasos de vuelos con Hive en HDInsight basado en Linux y luego exportar los datos a Azure SQL Database mediante Sqoop.</span><span class="sxs-lookup"><span data-stu-id="85f56-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85f56-105">Los pasos descritos en este documento requieren un clúster de HDInsight que use Linux.</span><span class="sxs-lookup"><span data-stu-id="85f56-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="85f56-106">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="85f56-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="85f56-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="85f56-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="85f56-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="85f56-108">Prerequisites</span></span>

* <span data-ttu-id="85f56-109">**Un clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="85f56-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="85f56-110">Vea [Introducción al uso de Hadoop con Hive en HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md) para conocer los pasos sobre la creación de un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="85f56-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="85f56-111">**Base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="85f56-111">**Azure SQL Database**.</span></span> <span data-ttu-id="85f56-112">Use una instancia de Azure SQL Database como almacén de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="85f56-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="85f56-113">Si no dispone todavía de una Base de datos SQL, consulte [Tutorial de Base de datos SQL: creación de una Base de datos SQL en cuestión de minutos](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="85f56-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="85f56-114">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="85f56-114">**Azure CLI**.</span></span> <span data-ttu-id="85f56-115">Si no ha instalado la CLI de Azure, vea [Instalación y configuración de la interfaz de la línea de comandos (CLI) de Azure](../cli-install-nodejs.md) para conocer más pasos.</span><span class="sxs-lookup"><span data-stu-id="85f56-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="85f56-116">Descarga de los datos de vuelo</span><span class="sxs-lookup"><span data-stu-id="85f56-116">Download the flight data</span></span>

1. <span data-ttu-id="85f56-117">Diríjase a[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span><span class="sxs-lookup"><span data-stu-id="85f56-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="85f56-118">En la página, seleccione los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="85f56-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="85f56-119">Nombre</span><span class="sxs-lookup"><span data-stu-id="85f56-119">Name</span></span> | <span data-ttu-id="85f56-120">Valor</span><span class="sxs-lookup"><span data-stu-id="85f56-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="85f56-121">Filter Year</span><span class="sxs-lookup"><span data-stu-id="85f56-121">Filter Year</span></span> |<span data-ttu-id="85f56-122">2013</span><span class="sxs-lookup"><span data-stu-id="85f56-122">2013</span></span> |
   | <span data-ttu-id="85f56-123">Filter Period</span><span class="sxs-lookup"><span data-stu-id="85f56-123">Filter Period</span></span> |<span data-ttu-id="85f56-124">January</span><span class="sxs-lookup"><span data-stu-id="85f56-124">January</span></span> |
   | <span data-ttu-id="85f56-125">Fields</span><span class="sxs-lookup"><span data-stu-id="85f56-125">Fields</span></span> |<span data-ttu-id="85f56-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="85f56-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="85f56-127">Borrado de los demás campos</span><span class="sxs-lookup"><span data-stu-id="85f56-127">Clear all other fields</span></span> |

3. <span data-ttu-id="85f56-128">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="85f56-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="85f56-129">Carga de los datos</span><span class="sxs-lookup"><span data-stu-id="85f56-129">Upload the data</span></span>

1. <span data-ttu-id="85f56-130">Use el siguiente comando para cargar el archivo .zip en el nodo principal del clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="85f56-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="85f56-131">Reemplace **FILENAME** por el nombre del archivo .zip.</span><span class="sxs-lookup"><span data-stu-id="85f56-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="85f56-132">Reemplace **USERNAME** por el inicio de sesión SSH para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85f56-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="85f56-133">Reemplace CLUSTERNAME por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85f56-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="85f56-134">Si usa una contraseña para autenticar el inicio de sesión SSH, se le pedirá la contraseña.</span><span class="sxs-lookup"><span data-stu-id="85f56-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="85f56-135">Si utiliza una clave pública, puede que tenga que usar el parámetro `-i` y especificar la ruta de acceso a la correspondiente clave privada.</span><span class="sxs-lookup"><span data-stu-id="85f56-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="85f56-136">Por ejemplo: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="85f56-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="85f56-137">Tras completar la carga, conéctese al clúster mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="85f56-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="85f56-138">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="85f56-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="85f56-139">Una vez conectado, use lo siguiente para descomprimir el archivo .zip:</span><span class="sxs-lookup"><span data-stu-id="85f56-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="85f56-140">Este comando extrae un archivo .csv que tiene un tamaño aproximado de 60 MB.</span><span class="sxs-lookup"><span data-stu-id="85f56-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="85f56-141">Use el siguiente comando para crear un directorio en el almacenamiento para HDInsight y luego copie el archivo en el directorio:</span><span class="sxs-lookup"><span data-stu-id="85f56-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="85f56-142">Creación y ejecución de HiveQL</span><span class="sxs-lookup"><span data-stu-id="85f56-142">Create and run the HiveQL</span></span>

<span data-ttu-id="85f56-143">Siga estos pasos para importar datos desde el archivo CSV en una tabla de Hive denominada **Delays**.</span><span class="sxs-lookup"><span data-stu-id="85f56-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="85f56-144">Use el comando siguiente para crear y editar un nuevo archivo denominado **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="85f56-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="85f56-145">Use el texto siguiente como contenido de este archivo:</span><span class="sxs-lookup"><span data-stu-id="85f56-145">Use the following text as the contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
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
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
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

2. <span data-ttu-id="85f56-146">Para guardar el archivo, use **Ctrl+X** y luego **Y**.</span><span class="sxs-lookup"><span data-stu-id="85f56-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="85f56-147">Para iniciar Hive y ejecutar el archivo **flightdelays.hql**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="85f56-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="85f56-148">En este ejemplo, se utiliza `localhost`, ya que está conectado al nodo principal del clúster de HDInsight, que es donde se está ejecutando HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="85f56-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="85f56-149">Una vez que el script __flightdelays.hql__ termine de ejecutarse, use el siguiente comando para abrir una sesión interactiva de Beeline:</span><span class="sxs-lookup"><span data-stu-id="85f56-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="85f56-150">Cuando reciba el símbolo del sistema `jdbc:hive2://localhost:10001/>`, use la consulta siguiente para recuperar datos de los datos de retrasos de vuelos importados.</span><span class="sxs-lookup"><span data-stu-id="85f56-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="85f56-151">Esta consulta recupera una lista de ciudades que experimentaron demoras debidas a inclemencias del tiempo, junto con el tiempo medio de retraso, y la guarda en `/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="85f56-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="85f56-152">Más adelante, Sqoop leerá los datos desde esta ubicación y los exportará a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="85f56-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="85f56-153">Para salir de Beeline, escriba `!quit` en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="85f56-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="85f56-154">una Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="85f56-154">Create a SQL Database</span></span>

<span data-ttu-id="85f56-155">Si ya tiene una base de datos SQL, debe obtener el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="85f56-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="85f56-156">Puede encontrar el nombre del servidor en [Azure Portal](https://portal.azure.com) seleccionando **SQL Database** y, después, filtrando por el nombre de la base de datos que desee usar.</span><span class="sxs-lookup"><span data-stu-id="85f56-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="85f56-157">El nombre del servidor aparece en la columna **SERVIDOR** .</span><span class="sxs-lookup"><span data-stu-id="85f56-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="85f56-158">Si no dispone todavía de una base de datos SQL, consulte [Tutorial de Base de datos SQL: creación de una Base de datos SQL en cuestión de minutos](../sql-database/sql-database-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="85f56-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="85f56-159">Guarde el nombre del servidor usado para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="85f56-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="85f56-160">Creación de una tabla de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="85f56-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="85f56-161">Hay muchas maneras de conectarse a SQL Database y crear una tabla.</span><span class="sxs-lookup"><span data-stu-id="85f56-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="85f56-162">En los siguientes pasos se utiliza [FreeTDS](http://www.freetds.org/) desde el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85f56-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="85f56-163">Use SSH para conectarse al clúster de HDInsight basado en Linux y ejecute los siguientes pasos en la sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="85f56-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="85f56-164">Use el siguiente comando para instalar FreeTDS:</span><span class="sxs-lookup"><span data-stu-id="85f56-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="85f56-165">Una vez finalizada la instalación, use el comando siguiente para conectarse al servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="85f56-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="85f56-166">Reemplace **serverName** por el nombre del servidor de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="85f56-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="85f56-167">Reemplace **adminLogin** y **adminPassword** por el inicio de sesión de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="85f56-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="85f56-168">Reemplace **databaseName** por el nombre de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="85f56-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="85f56-169">Recibirá una salida similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="85f56-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="85f56-170">En el símbolo del sistema `1>` , introduzca las líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="85f56-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="85f56-171">Cuando se haya especificado la instrucción `GO`, se evaluarán las instrucciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="85f56-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="85f56-172">Se crea una tabla denominada **delays** con un índice agrupado.</span><span class="sxs-lookup"><span data-stu-id="85f56-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="85f56-173">Use la siguiente consulta para comprobar que se ha creado la tabla:</span><span class="sxs-lookup"><span data-stu-id="85f56-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="85f56-174">La salida será similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="85f56-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="85f56-175">Entrar `exit` at the `1>` .</span><span class="sxs-lookup"><span data-stu-id="85f56-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="85f56-176">Exportación de datos con Sqoop</span><span class="sxs-lookup"><span data-stu-id="85f56-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="85f56-177">Utilice el siguiente comando para comprobar que Sqoop puede ver la base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="85f56-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="85f56-178">Este comando devuelve una lista de bases de datos, incluida la que creó anteriormente en la tabla delays.</span><span class="sxs-lookup"><span data-stu-id="85f56-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="85f56-179">Use el comando siguiente para exportar los datos de hivesampletable a la tabla mobiledata:</span><span class="sxs-lookup"><span data-stu-id="85f56-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="85f56-180">Sqoop se conecta a la base de datos que contiene la tabla delays y exporta datos del directorio `/tutorials/flightdelays/output` a dicha tabla.</span><span class="sxs-lookup"><span data-stu-id="85f56-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="85f56-181">Una vez completado el comando, utilice lo siguiente para conectarse a la base de datos mediante TSQL:</span><span class="sxs-lookup"><span data-stu-id="85f56-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="85f56-182">Una vez conectada, use las instrucciones siguientes para comprobar que los datos se exportaron a la tabla mobiledata:</span><span class="sxs-lookup"><span data-stu-id="85f56-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="85f56-183">Debería ver una lista de los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="85f56-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="85f56-184">Escriba `exit` para salir de la utilidad de tsql.</span><span class="sxs-lookup"><span data-stu-id="85f56-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="85f56-185"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85f56-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="85f56-186">Para conocer más formas para trabajar con datos en Hive en HDInsight, consulte los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="85f56-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="85f56-187">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="85f56-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="85f56-188">[Uso de Oozie con HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="85f56-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="85f56-189">[Uso de Sqoop con HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="85f56-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="85f56-190">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="85f56-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="85f56-191">[Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="85f56-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="85f56-192">[Desarrollo de programas de Hadoop con Python en HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="85f56-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
