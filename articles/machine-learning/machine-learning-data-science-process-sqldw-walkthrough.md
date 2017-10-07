---
title: "Hola proceso de ciencia de datos de equipo en acción: con almacenamiento de datos SQL | Documentos de Microsoft"
description: "Tecnología y procesos de análisis avanzado en acción"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="81340-103">Hola proceso de ciencia de datos de equipo en acción: con almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="81340-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="81340-104">En este tutorial, se le guían en la creación e implementación de un modelo de aprendizaje automático con almacenamiento de datos de SQL (SQL DW) para un conjunto de datos disponible públicamente--hello [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="81340-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="81340-105">modelo de clasificación binaria de Hello construido predice si no se le paga una sugerencia para un recorrido, y los modelos de regresión y de clasificación multiclase también se tratan que predicen distribución Hola para hello cantidades de sugerencia de pago.</span><span class="sxs-lookup"><span data-stu-id="81340-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="81340-106">procedimiento de Hello sigue hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="81340-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="81340-107">Le mostramos cómo toosetup un entorno de ciencia de datos, cómo tooload Hola datos en almacenamiento de datos de SQL y cómo usar el almacenamiento de datos de SQL o un bloc de notas de IPython tooexplore Hola datos e ingeniero características toomodel.</span><span class="sxs-lookup"><span data-stu-id="81340-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="81340-108">A continuación, mostramos cómo toobuild e implementar un modelo de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="81340-109"><a name="dataset"></a>el conjunto de datos de Hello NYC Taxi viajes</span><span class="sxs-lookup"><span data-stu-id="81340-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="81340-110">Hola datos NYC Taxi recorridos consta de unos 20GB de archivos comprimidos de CSV (sin comprimir de ~ 48GB), más de 173 millones de grabación hello y viajes individuales puntuación de pago para cada recorrido.</span><span class="sxs-lookup"><span data-stu-id="81340-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="81340-111">Cada registro de ida y vuelta incluye ubicaciones de recogida y entrega de Hola y tiempos, anónimos hack número de licencia (del controlador) y Hola número medallion (identificador único del taxi).</span><span class="sxs-lookup"><span data-stu-id="81340-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="81340-112">datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:</span><span class="sxs-lookup"><span data-stu-id="81340-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="81340-113">Hola **trip_data.csv** archivo contiene los detalles de ida y vuelta, como el número de los pasajeros, puntos de recogida y caída, duración de ida y vuelta y duración del viaje.</span><span class="sxs-lookup"><span data-stu-id="81340-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="81340-114">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="81340-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="81340-115">Hola **trip_fare.csv** archivo contiene detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago.</span><span class="sxs-lookup"><span data-stu-id="81340-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="81340-116">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="81340-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="81340-117">Hola **clave única** utilizan recorridos toojoin\_datos y recorridos\_tarifa se compone de hello después de tres campos:</span><span class="sxs-lookup"><span data-stu-id="81340-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="81340-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="81340-118">medallion,</span></span>
* <span data-ttu-id="81340-119">hack\_license y</span><span class="sxs-lookup"><span data-stu-id="81340-119">hack\_license and</span></span>
* <span data-ttu-id="81340-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="81340-120">pickup\_datetime.</span></span>

## <span data-ttu-id="81340-121"><a name="mltasks"></a>Realicemos tres tipos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="81340-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="81340-122">Se formular tres problemas de predicción basándose en hello *sugerencia\_cantidad* tooillustrate tres tipos de tareas de modelado:</span><span class="sxs-lookup"><span data-stu-id="81340-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="81340-123">**Clasificación binaria**: toopredict o no se pagó una sugerencia para un recorrido, es decir, un *sugerencia\_cantidad* que es mayor que $0 es un ejemplo positivo, mientras un *sugerencia\_cantidad* $ 0 es un ejemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="81340-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="81340-124">**Clasificación multiclase**: intervalo de hello toopredict de sugerencia de pago para recorridos de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="81340-125">Se divide hello *sugerencia\_cantidad* en cinco bandejas o clases:</span><span class="sxs-lookup"><span data-stu-id="81340-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="81340-126">**Tarea de regresión**: cantidad de hello toopredict de sugerencia de pago para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="81340-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="81340-127"><a name="setup"></a>Configurar el entorno de ciencia de datos de Azure de Hola para análisis avanzado</span><span class="sxs-lookup"><span data-stu-id="81340-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="81340-128">tooset del entorno de ciencia de datos de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="81340-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="81340-129">**Cree su propia cuenta de Almacenamiento de blobs de Azure.**</span><span class="sxs-lookup"><span data-stu-id="81340-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="81340-130">Al proporcionar su propio almacenamiento de blobs de Azure, elija una ubicación geográfica del almacenamiento de blobs de Azure en o tan cerca como sea posible demasiado**Ee.uu. Central sur**, que es donde se almacena los datos de Nueva York Taxi Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="81340-131">datos de Hola se copiarán con AzCopy de contenedor de tooa de contenedor de almacenamiento de blobs públicos de hello en su propia cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="81340-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="81340-132">Hello cuando se acerque el almacenamiento de blobs de Azure es tooSouth Central US, hello más rápido (paso 4) se puede realizar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="81340-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="81340-133">cuenta de su propio almacenamiento de Azure toocreate, Hola seguir pasos que se describen en [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="81340-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="81340-134">Estar seguro de notas de toomake valores de hello para las siguientes credenciales de cuenta de almacenamiento que se necesitarán más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="81340-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="81340-135">**Nombre de cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="81340-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="81340-136">**Clave de cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="81340-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="81340-137">**Nombre del contenedor** (que quiere hello toobe de datos almacenado en hello almacenamiento de blobs de Azure)</span><span class="sxs-lookup"><span data-stu-id="81340-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="81340-138">**Aprovisione la instancia de Almacenamiento de datos SQL de Azure.**</span><span class="sxs-lookup"><span data-stu-id="81340-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="81340-139">Seguir la documentación de hello en [crear un almacén de datos de SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision una instancia de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="81340-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="81340-140">Asegúrese de que realiza las notaciones en hello siguiendo las credenciales de almacén de datos de SQL que se utilizarán en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="81340-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="81340-141">**Nombre del servidor**: <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="81340-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="81340-142">**Nombre de SQLDW (base de datos)**</span><span class="sxs-lookup"><span data-stu-id="81340-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="81340-143">**Nombre de usuario**</span><span class="sxs-lookup"><span data-stu-id="81340-143">**Username**</span></span>
* <span data-ttu-id="81340-144">**Password**</span><span class="sxs-lookup"><span data-stu-id="81340-144">**Password**</span></span>

<span data-ttu-id="81340-145">**Instale Visual Studio y SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="81340-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="81340-146">Para ver instrucciones, consulte [Instalación de Visual Studio 2015 y SSDT para Almacenamiento de datos SQL](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="81340-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="81340-147">**Conectar tooyour almacenamiento de datos de SQL Azure con Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="81340-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="81340-148">Para obtener instrucciones, consulte los pasos 1 y 2 en [conectar tooAzure almacenamiento de datos de SQL con Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81340-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="81340-149">Ejecución hello consulta SQL en la base de datos de Hola que creó en el almacenamiento de datos de SQL siguiente (en lugar de consulta de hello proporcionada en el paso 3 de hello conectar tema) demasiado**crear una clave maestra de**.</span><span class="sxs-lookup"><span data-stu-id="81340-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="81340-150">**Cree un área de trabajo de Azure Machine Learning en su suscripción de Azure.**</span><span class="sxs-lookup"><span data-stu-id="81340-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="81340-151">Para ver instrucciones, consulte [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="81340-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="81340-152"><a name="getdata"></a>Cargar datos de hello en almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="81340-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="81340-153">Abra una consola de comandos de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81340-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="81340-154">Ejecute hello siguiente comandos de PowerShell toodownload Hola ejemplo archivos de script SQL que se comparten con usted en GitHub tooa directorio local que se especifica con el parámetro hello *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="81340-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="81340-155">Puede cambiar Hola valor del parámetro *- DestDir* tooany de directorio local.</span><span class="sxs-lookup"><span data-stu-id="81340-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="81340-156">Si *- DestDir* no existe, se creará Hola script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81340-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="81340-157">Es posible que tenga demasiado**ejecutar como administrador** al ejecutar Hola siguiente script de PowerShell si su *DestDir* directorio debe tooit de toocreate o toowrite de privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="81340-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="81340-158">Tras la ejecución correcta, el directorio de trabajo actual cambia demasiado*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="81340-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="81340-159">Debería poder toosee pantalla como a continuación:</span><span class="sxs-lookup"><span data-stu-id="81340-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="81340-160">En su *- DestDir*, ejecute hello siguiente script de PowerShell en modo de administrador:</span><span class="sxs-lookup"><span data-stu-id="81340-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="81340-161">Cuando Hola script de PowerShell se ejecuta para hello primera vez, se le pedirá información de hello tooinput desde el almacenamiento de datos de SQL Azure y la cuenta de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="81340-162">Cuando se completa este script de PowerShell ejecuta para hello primera vez, las credenciales de hello proporcionados por el habrá se han escrito archivo de configuración de tooa SQLDW.conf en el directorio de trabajo presente Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="81340-163">Hello ejecución futuras de este archivo de script de PowerShell tiene Hola opción tooread necesarios todos los parámetros de este archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="81340-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="81340-164">Si necesita toochange algunos parámetros, puede elegir parámetros hello en pantalla de bienvenida al símbolo del sistema si elimina este archivo de configuración y especificar valores de parámetros de hello cuando se le solicite o con valores de parámetro de hello toochange tooinput editando el archivo de hello SQLDW.conf en su *- DestDir* directory.</span><span class="sxs-lookup"><span data-stu-id="81340-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="81340-165">En orden tooavoid esquema nombre entra en conflicto con los que ya existen en el almacenamiento de datos de SQL Azure, al leer parámetros directamente desde el archivo de SQLDW.conf hello, un número aleatorio de 3 dígitos se agrega toohello nombre del esquema de archivo de hello SQLDW.conf como nombre de esquema predeterminado de Hola para cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="81340-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="81340-166">Hola script de PowerShell puede pedirle un nombre de esquema: se puede especificar el nombre de Hola a discreción del usuario.</span><span class="sxs-lookup"><span data-stu-id="81340-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="81340-167">Esto **script de PowerShell** archivo completa Hola siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="81340-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="81340-168">**Descarga e instala AzCopy**, si AzCopy no se ha instalado aún</span><span class="sxs-lookup"><span data-stu-id="81340-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="81340-169">**Copia de la cuenta de almacenamiento de blobs privado de datos tooyour** de blob públicos de hello con AzCopy</span><span class="sxs-lookup"><span data-stu-id="81340-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="81340-170">**Carga datos mediante Polybase (mediante la ejecución de LoadDataToSQLDW.sql) tooyour Azure SQL DW** de la cuenta de almacenamiento de blobs privado con hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="81340-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="81340-171">Creación de un esquema</span><span class="sxs-lookup"><span data-stu-id="81340-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="81340-172">Creación de una credencial con ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="81340-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="81340-173">Creación de un origen de datos externo para un blob de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="81340-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="81340-174">Cree un formato de archivo externo para un archivo .csv.</span><span class="sxs-lookup"><span data-stu-id="81340-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="81340-175">Datos sin comprimir y los campos están separados con carácter de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="81340-176">Cree tablas externas de tarifas y propinas para el conjunto de datos de NYC Taxi en el Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="81340-177">Cargar datos de tablas externas de almacenamiento de blobs de Azure tooSQL almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="81340-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="81340-178">Crear una tabla de datos de ejemplo (NYCTaxi_Sample) e insertar tooit de datos de la selección de consultas SQL en tablas de tarifas y recorridos de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="81340-179">(Algunos pasos de este tutorial debe toouse esta tabla de ejemplo.)</span><span class="sxs-lookup"><span data-stu-id="81340-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="81340-180">ubicación geográfica de Hola de sus cuentas de almacenamiento afecta a los tiempos de carga.</span><span class="sxs-lookup"><span data-stu-id="81340-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="81340-181">Según la ubicación geográfica de saludo de la cuenta de almacenamiento de blobs privado, proceso Hola de copiar datos de una cuenta de almacenamiento privado tooyour blob público puede tardar unos 15 minutos o incluso ya y hello del proceso de carga de datos de la cuenta de almacenamiento tooyour almacenamiento de datos de SQL Azure puede tardar 20 minutos o más.</span><span class="sxs-lookup"><span data-stu-id="81340-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="81340-182">Deberá toodecide ¿qué hacer si tiene un origen duplicado y archivos de destino.</span><span class="sxs-lookup"><span data-stu-id="81340-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="81340-183">Si toobe de archivos .csv Hola copiado de cuenta de almacenamiento de blobs privado de hello blob público almacenamiento tooyour ya existe en la cuenta de almacenamiento de blobs privado, AzCopy le preguntará si desea toooverwrite ellos.</span><span class="sxs-lookup"><span data-stu-id="81340-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="81340-184">Si no desea toooverwrite éstos, entrada  **n**  cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="81340-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="81340-185">Si desea que toooverwrite **todos los** de ellos, de entrada **un** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="81340-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="81340-186">También puede introducir **y** toooverwrite .csv archivos individualmente.</span><span class="sxs-lookup"><span data-stu-id="81340-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![Diagrama 21][21]

<span data-ttu-id="81340-188">Puede usar sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="81340-188">You can use your own data.</span></span> <span data-ttu-id="81340-189">Si los datos están en el equipo local en su aplicación en la vida real, todavía puede usar el almacenamiento de blobs de Azure privada de tooyour de datos de AzCopy tooupload local.</span><span class="sxs-lookup"><span data-stu-id="81340-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="81340-190">Solo necesita hello toochange **origen** ubicación, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, Hola comandos de AzCopy de hello PowerShell script archivo toohello directorio local que contiene los datos.</span><span class="sxs-lookup"><span data-stu-id="81340-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="81340-191">Si los datos ya están en el almacenamiento de blobs de Azure privada en la aplicación de la vida real, puede omitir hello AzCopy paso Hola script de PowerShell y cargar directamente hello tooAzure de datos SQL DW.</span><span class="sxs-lookup"><span data-stu-id="81340-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="81340-192">Esto requerirá adicionales edita de hello script tootailor toohello formato de los datos.</span><span class="sxs-lookup"><span data-stu-id="81340-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="81340-193">Este script de Powershell también se conecta en hello información de almacenamiento de datos de SQL Azure en archivos ejemplo de Hola datos exploración SQLDW_Explorations.sql, SQLDW_Explorations.ipynb y SQLDW_Explorations_Scripts.py para que estos tres archivos sean toobe listo probado al instante una vez completada la Hola script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81340-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="81340-194">Después de una ejecución correcta, verá una pantalla similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="81340-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="81340-195"><a name="dbexplore"></a>Exploración de datos y diseño de características en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="81340-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="81340-196">En esta sección, realizamos la generación de características y la exploración de datos mediante la ejecución de consultas SQL en Almacenamiento de datos SQL de Azure directamente mediante **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="81340-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="81340-197">Todas las consultas SQL que se utilizan en esta sección pueden encontrarse en el script de ejemplo de Hola denominado *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="81340-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="81340-198">Este archivo ya ha sido descargado tooyour directorio local por script de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="81340-199">También puede recuperarlo desde [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="81340-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="81340-200">Pero el archivo hello en GitHub no tiene información de almacenamiento de datos de SQL Azure Hola enchufado.</span><span class="sxs-lookup"><span data-stu-id="81340-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="81340-201">Conectar tooyour almacenamiento de datos de SQL de Azure con Visual Studio con el nombre de inicio de sesión de SQL DW hello y una contraseña y se abrirán hello **Explorador de objetos SQL** base de datos de tooconfirm hello y las tablas se han importado.</span><span class="sxs-lookup"><span data-stu-id="81340-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="81340-202">Recuperar hello *SQLDW_Explorations.sql* archivo.</span><span class="sxs-lookup"><span data-stu-id="81340-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="81340-203">tooopen un editor de consultas de almacenamiento de datos paralelo (PDW), usar hello **nueva consulta** comando mientras está seleccionado el PDW en hello **Explorador de objetos SQL**.</span><span class="sxs-lookup"><span data-stu-id="81340-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="81340-204">editor de consultas SQL estándar de Hello no es compatible con PDW.</span><span class="sxs-lookup"><span data-stu-id="81340-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="81340-205">Estos son tipo hello de datos realizan tareas de generación de exploración y la característica de esta sección:</span><span class="sxs-lookup"><span data-stu-id="81340-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="81340-206">Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="81340-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="81340-207">Investigue la calidad de los datos de los campos de longitud y latitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="81340-208">Generar etiquetas de clasificación multiclase y binaria basándose en hello **sugerencia\_cantidad**.</span><span class="sxs-lookup"><span data-stu-id="81340-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="81340-209">Generar características y calcular o comparar distancias de carreras.</span><span class="sxs-lookup"><span data-stu-id="81340-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="81340-210">Combinar Hola dos tablas y extraer una muestra aleatoria que será usado toobuild modelos.</span><span class="sxs-lookup"><span data-stu-id="81340-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="81340-211">Comprobación de la importación de datos</span><span class="sxs-lookup"><span data-stu-id="81340-211">Data import verification</span></span>
<span data-ttu-id="81340-212">Estas consultas proporcionan una comprobación rápida del número de Hola de filas y columnas de hello importan tablas rellenadas anteriormente con masiva paralela de Polybase,</span><span class="sxs-lookup"><span data-stu-id="81340-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="81340-213">**Salida:** debe obtener 173 179 759 filas y 14 columnas.</span><span class="sxs-lookup"><span data-stu-id="81340-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="81340-214">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="81340-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="81340-215">Esta consulta de ejemplo identifica medallions Hola (taxi números) que completar más de 100 viajes dentro de un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="81340-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="81340-216">consulta de Hola se beneficiaría de acceso a la tabla con particiones de hello porque está condicionado por esquema de partición de Hola de **recogida\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="81340-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="81340-217">Consultar el conjunto de datos completo de hello también hará que el uso de la tabla con particiones de Hola o examen de índice.</span><span class="sxs-lookup"><span data-stu-id="81340-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="81340-218">**Salida:** deben devolver una tabla con filas especificando medallions hello 13,369 (taxis) de consultas de Hola y Hola número de recorridos realizarla en 2013.</span><span class="sxs-lookup"><span data-stu-id="81340-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="81340-219">Hola última columna contiene recuento de hello del número de Hola de viajes y completado.</span><span class="sxs-lookup"><span data-stu-id="81340-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="81340-220">Exploración: distribución de carreras por medallion y hack_license</span><span class="sxs-lookup"><span data-stu-id="81340-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="81340-221">Este ejemplo identifica medallions Hola (taxi números) y hack_license números (controladores) que completar más de 100 viajes dentro de un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="81340-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="81340-222">**Salida:** consulta Hola debe devolver una tabla con 13,369 filas especificar hello 13,369 automóvil/controlador identificadores que se han completado más que 100 viajes en 2013.</span><span class="sxs-lookup"><span data-stu-id="81340-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="81340-223">Hola última columna contiene recuento de hello del número de Hola de viajes y completado.</span><span class="sxs-lookup"><span data-stu-id="81340-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="81340-224">Evaluación de la calidad de los datos: comprobar los registros con longitud o latitud incorrectas</span><span class="sxs-lookup"><span data-stu-id="81340-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="81340-225">En este ejemplo se investiga si alguno de los campos de longitud o latitud de Hola o contiene un valor no válido (grados Radián deben estar entre -90 y 90), o tener (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="81340-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="81340-226">**Salida:** consulta Hola devuelve 837,467 viajes y que tiene campos no válidos de longitud o latitud.</span><span class="sxs-lookup"><span data-stu-id="81340-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="81340-227">Exploración: distribución de carreras con propinas frente a sin propinas</span><span class="sxs-lookup"><span data-stu-id="81340-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="81340-228">Este ejemplo busca el número de Hola de viajes que se han superpuesto frente a número de Hola y que no se han superpuesto en un período de tiempo especificado (o conjunto de datos completa de hello si cubriendo año completo Hola tal y como se configura aquí).</span><span class="sxs-lookup"><span data-stu-id="81340-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="81340-229">Esta distribución refleja Hola etiqueta binario distribución toobe que más adelante se usa para el modelo de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="81340-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="81340-230">**Salida:** Hola consulta debe siguiente Hola devuelto sugerencia frecuencias de hello año 2013: 90,447,622 superpuesto y 82,264,709 superpuesto no.</span><span class="sxs-lookup"><span data-stu-id="81340-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="81340-231">Exploración: distribución por intervalos y clases de propinas</span><span class="sxs-lookup"><span data-stu-id="81340-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="81340-232">Este ejemplo calcula distribución Hola de intervalos de sugerencia en un momento determinado período (o en el conjunto de datos completo de hello si relativo Hola completa año).</span><span class="sxs-lookup"><span data-stu-id="81340-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="81340-233">Se trata de distribución de Hola de clases de etiqueta de Hola que usará más adelante para el modelado de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="81340-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="81340-234">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="81340-234">**Output:**</span></span>

| <span data-ttu-id="81340-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="81340-235">tip_class</span></span> | <span data-ttu-id="81340-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="81340-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="81340-237">1</span><span class="sxs-lookup"><span data-stu-id="81340-237">1</span></span> |<span data-ttu-id="81340-238">82 230 915</span><span class="sxs-lookup"><span data-stu-id="81340-238">82230915</span></span> |
| <span data-ttu-id="81340-239">2</span><span class="sxs-lookup"><span data-stu-id="81340-239">2</span></span> |<span data-ttu-id="81340-240">6 198 803</span><span class="sxs-lookup"><span data-stu-id="81340-240">6198803</span></span> |
| <span data-ttu-id="81340-241">3</span><span class="sxs-lookup"><span data-stu-id="81340-241">3</span></span> |<span data-ttu-id="81340-242">1 932 223</span><span class="sxs-lookup"><span data-stu-id="81340-242">1932223</span></span> |
| <span data-ttu-id="81340-243">0</span><span class="sxs-lookup"><span data-stu-id="81340-243">0</span></span> |<span data-ttu-id="81340-244">82 264 625</span><span class="sxs-lookup"><span data-stu-id="81340-244">82264625</span></span> |
| <span data-ttu-id="81340-245">4</span><span class="sxs-lookup"><span data-stu-id="81340-245">4</span></span> |<span data-ttu-id="81340-246">85 765</span><span class="sxs-lookup"><span data-stu-id="81340-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="81340-247">Exploración: proceso y comparación de la distancia de la carrera</span><span class="sxs-lookup"><span data-stu-id="81340-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="81340-248">Este ejemplo convierte la longitud de recogida y entrega de Hola y geografía de latitud tooSQL señala, calcula la distancia de viaje hello mediante diferencia de puntos de geography SQL y devuelve una muestra aleatoria de resultados de hello para la comparación.</span><span class="sxs-lookup"><span data-stu-id="81340-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="81340-249">ejemplo de Hola limita los resultados de hello toovalid coordina únicamente con la consulta de evaluación de calidad Hola datos cubierto anteriormente.</span><span class="sxs-lookup"><span data-stu-id="81340-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="81340-250">Diseño de características con las funciones de SQL</span><span class="sxs-lookup"><span data-stu-id="81340-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="81340-251">A veces, las funciones de SQL pueden ser una opción eficiente de diseño de características.</span><span class="sxs-lookup"><span data-stu-id="81340-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="81340-252">En este tutorial, definimos una SQL función toocalculate Hola distancia directa entre las ubicaciones de recogida y caída de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="81340-253">Puede ejecutar Hola siguientes secuencias de comandos SQL en **herramientas de datos de Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="81340-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="81340-254">Esta es la secuencia de comandos SQL de Hola que define la función de distancia de hello.</span><span class="sxs-lookup"><span data-stu-id="81340-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="81340-255">Este es un toocall de ejemplo esta característica de toogenerate de función en la consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="81340-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="81340-256">**Salida:** esta consulta genera una tabla (con 2,803,538 filas) con recogida y caída latitudes y longitudes y Hola correspondiente dirigen distancias en millas.</span><span class="sxs-lookup"><span data-stu-id="81340-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="81340-257">Estos son los resultados de Hola para primero 3 filas:</span><span class="sxs-lookup"><span data-stu-id="81340-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="81340-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="81340-258">pickup_latitude</span></span> | <span data-ttu-id="81340-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="81340-259">pickup_longitude</span></span> | <span data-ttu-id="81340-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="81340-260">dropoff_latitude</span></span> | <span data-ttu-id="81340-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="81340-261">dropoff_longitude</span></span> | <span data-ttu-id="81340-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="81340-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="81340-263">1</span><span class="sxs-lookup"><span data-stu-id="81340-263">1</span></span> |<span data-ttu-id="81340-264">40,731804</span><span class="sxs-lookup"><span data-stu-id="81340-264">40.731804</span></span> |<span data-ttu-id="81340-265">-74,001083</span><span class="sxs-lookup"><span data-stu-id="81340-265">-74.001083</span></span> |<span data-ttu-id="81340-266">40,736622</span><span class="sxs-lookup"><span data-stu-id="81340-266">40.736622</span></span> |<span data-ttu-id="81340-267">-73,988953</span><span class="sxs-lookup"><span data-stu-id="81340-267">-73.988953</span></span> |<span data-ttu-id="81340-268">0,7169601222</span><span class="sxs-lookup"><span data-stu-id="81340-268">.7169601222</span></span> |
| <span data-ttu-id="81340-269">2</span><span class="sxs-lookup"><span data-stu-id="81340-269">2</span></span> |<span data-ttu-id="81340-270">40,715794</span><span class="sxs-lookup"><span data-stu-id="81340-270">40.715794</span></span> |<span data-ttu-id="81340-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="81340-271">-74,010635</span></span> |<span data-ttu-id="81340-272">40,725338</span><span class="sxs-lookup"><span data-stu-id="81340-272">40.725338</span></span> |<span data-ttu-id="81340-273">-74,00399</span><span class="sxs-lookup"><span data-stu-id="81340-273">-74.00399</span></span> |<span data-ttu-id="81340-274">0,7448343721</span><span class="sxs-lookup"><span data-stu-id="81340-274">.7448343721</span></span> |
| <span data-ttu-id="81340-275">3</span><span class="sxs-lookup"><span data-stu-id="81340-275">3</span></span> |<span data-ttu-id="81340-276">40,761456</span><span class="sxs-lookup"><span data-stu-id="81340-276">40.761456</span></span> |<span data-ttu-id="81340-277">-73,999886</span><span class="sxs-lookup"><span data-stu-id="81340-277">-73.999886</span></span> |<span data-ttu-id="81340-278">40,766544</span><span class="sxs-lookup"><span data-stu-id="81340-278">40.766544</span></span> |<span data-ttu-id="81340-279">-73,988228</span><span class="sxs-lookup"><span data-stu-id="81340-279">-73.988228</span></span> |<span data-ttu-id="81340-280">0,7037227967</span><span class="sxs-lookup"><span data-stu-id="81340-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="81340-281">Preparar datos para la generación de modelos</span><span class="sxs-lookup"><span data-stu-id="81340-281">Prepare data for model building</span></span>
<span data-ttu-id="81340-282">Hola de combinaciones de consulta siguiente Hello **nyctaxi\_recorridos** y **nyctaxi\_tarifa** tablas, genera una etiqueta de clasificación binaria **superpuesto**, etiqueta de clasificación multiclase **sugerencia\_clase**y extrae un ejemplo de Hola completa Unidos a un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="81340-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="81340-283">muestreo de Hola se realiza mediante la recuperación de un subconjunto de viajes de hello en función del tiempo de recogida.</span><span class="sxs-lookup"><span data-stu-id="81340-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="81340-284">Esta consulta se puede copiar y pegar directamente en hello [estudio de aprendizaje automático de Azure](https://studio.azureml.net) [importar datos] [ import-data] módulo de recopilación de datos directa de instancia de base de datos SQL de Hola en Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="81340-285">consulta de Hello excluye los registros con incorrecto (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="81340-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="81340-286">Cuando esté listo tooproceed tooAzure aprendizaje automático, puede:</span><span class="sxs-lookup"><span data-stu-id="81340-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="81340-287">Guardar Hola final SQL consulta tooextract y ejemplo Hola datos y copiar y pegar Hola consulta directamente en un [importar datos] [ import-data] módulo aprendizaje automático de Azure, o</span><span class="sxs-lookup"><span data-stu-id="81340-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="81340-288">Hola muestreada se conservan e ingeniería datos que tiene previsto toouse para el modelo de creación de un nuevo almacenamiento de datos de SQL de la tabla y usar nueva tabla de hello en hello [importar datos] [ import-data] módulo aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="81340-289">Hola script de PowerShell en el paso anterior hace esto automáticamente.</span><span class="sxs-lookup"><span data-stu-id="81340-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="81340-290">Puede leer directamente en esta tabla en el módulo de importación de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="81340-291"><a name="ipnb"></a>Exploración de datos e ingeniería de características en IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="81340-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="81340-292">En esta sección, se llevará a cabo una exploración de datos y la generación de característica con ambas Python y consultas SQL en hello SQL DW crean anteriormente.</span><span class="sxs-lookup"><span data-stu-id="81340-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="81340-293">Un bloc de notas de IPython de ejemplo denominado **SQLDW_Explorations.ipynb** y un archivo de script de Python **SQLDW_Explorations_Scripts.py** se han descargado tooyour directorio local.</span><span class="sxs-lookup"><span data-stu-id="81340-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="81340-294">También están disponibles en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="81340-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="81340-295">Estos dos archivos son idénticos en los scripts de Python.</span><span class="sxs-lookup"><span data-stu-id="81340-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="81340-296">archivo de script de Python Hola se proporciona tooyou en caso de que no tiene un servidor de Bloc de notas de IPython.</span><span class="sxs-lookup"><span data-stu-id="81340-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="81340-297">Estos dos archivos de Python de muestra están diseñados en **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="81340-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="81340-298">Hola información necesaria de almacenamiento de datos de SQL Azure en el Bloc de notas de IPython de ejemplo de Hola y Hola Python máquina local de tooyour descargado de archivos de script se ha conectado por script de PowerShell de hello previamente.</span><span class="sxs-lookup"><span data-stu-id="81340-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="81340-299">Son ejecutables sin ninguna modificación.</span><span class="sxs-lookup"><span data-stu-id="81340-299">They are executable without any modification.</span></span>

<span data-ttu-id="81340-300">Si ya ha configurado un área de trabajo de aprendizaje automático de Azure, puede cargar muestra de Hola a servicio de Bloc de notas de IPython toohello Bloc de notas de IPython de aprendizaje automático de Azure y comenzar a ejecutarla directamente.</span><span class="sxs-lookup"><span data-stu-id="81340-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="81340-301">A continuación, incluimos Hola pasos tooupload tooAzureML servicio Bloc de notas de IPython:</span><span class="sxs-lookup"><span data-stu-id="81340-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="81340-302">Inicie sesión en el área de trabajo de tooyour aprendizaje automático de Azure, haga clic en "Studio" en la parte superior de Hola y haga clic en "Blocs de notas" en el lado izquierdo de Hola de página web de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![Diagrama 22][22]
2. <span data-ttu-id="81340-304">Haga clic en "Nuevo" en la esquina inferior izquierda de Hola de página web de Hola y seleccione "Python 2".</span><span class="sxs-lookup"><span data-stu-id="81340-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="81340-305">A continuación, proporcionar un bloc de notas de toohello de nombre y haga clic en hello marca de verificación toocreate Hola nuevo en blanco Bloc de notas de IPython.</span><span class="sxs-lookup"><span data-stu-id="81340-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![Diagrama 23][23]
3. <span data-ttu-id="81340-307">Haga clic en el símbolo de "Jupyter" hello en la esquina superior izquierda de Hola de hello nuevo bloc de notas de IPython.</span><span class="sxs-lookup"><span data-stu-id="81340-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![Diagrama 24][24]
4. <span data-ttu-id="81340-309">Arrastre y coloque Hola ejemplo Bloc de notas de IPython toohello **árbol** página del servicio de Bloc de notas de IPython de aprendizaje automático de Azure y haga clic en **cargar**.</span><span class="sxs-lookup"><span data-stu-id="81340-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="81340-310">A continuación, muestra de Hola Bloc de notas de IPython será cargado toohello servicio Bloc de notas de IPython de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![Diagrama 25][25]

<span data-ttu-id="81340-312">Hola toorun de pedido de ejemplo Bloc de notas de IPython u Hola archivo de script de Python, hello siguientes Python paquetes son necesarios.</span><span class="sxs-lookup"><span data-stu-id="81340-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="81340-313">Si usas el servicio de hello Bloc de notas de IPython de aprendizaje automático de Azure, estos paquetes se hayan instalado previamente.</span><span class="sxs-lookup"><span data-stu-id="81340-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="81340-314">Pandas</span><span class="sxs-lookup"><span data-stu-id="81340-314">pandas</span></span>
    - <span data-ttu-id="81340-315">numpy</span><span class="sxs-lookup"><span data-stu-id="81340-315">numpy</span></span>
    - <span data-ttu-id="81340-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="81340-316">matplotlib</span></span>
    - <span data-ttu-id="81340-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="81340-317">pyodbc</span></span>
    - <span data-ttu-id="81340-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="81340-318">PyTables</span></span>

<span data-ttu-id="81340-319">Hola recomendada secuencia al compilar las soluciones analíticas avanzadas en aprendizaje automático de Azure con datos de gran tamaño es siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="81340-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="81340-320">Leer en una pequeña muestra de datos de hello en un marco de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="81340-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="81340-321">Realizar algunas visualizaciones y exploraciones con los datos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="81340-322">Experimente con ingeniería de característica con hello los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="81340-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="81340-323">Exploración de datos mayor, manipulación de datos y la ingeniería de característica, utilizar consultas de SQL de tooissue de Python directamente en hello SQL DW.</span><span class="sxs-lookup"><span data-stu-id="81340-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="81340-324">Decidir toobe de tamaño de ejemplo de Hola adecuado para la compilación del modelo de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="81340-325">siguiente Hola es unos exploración de datos, visualización de datos y ejemplos de ingeniería de característica.</span><span class="sxs-lookup"><span data-stu-id="81340-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="81340-326">Más exploraciones de datos pueden encontrarse en el ejemplo hello Bloc de notas de IPython y archivo de script de Python de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="81340-327">Inicialización de las credenciales de la base de datos</span><span class="sxs-lookup"><span data-stu-id="81340-327">Initialize database credentials</span></span>
<span data-ttu-id="81340-328">Inicializar la configuración de conexión de base de datos en hello siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="81340-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="81340-329">Creación de conexiones de base de datos</span><span class="sxs-lookup"><span data-stu-id="81340-329">Create database connection</span></span>
<span data-ttu-id="81340-330">Aquí es cadena de conexión de Hola que crea la base de datos de hello conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="81340-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="81340-331">Informe con el número de filas y columnas de la tabla <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="81340-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="81340-332">Número total de filas = 173179759</span><span class="sxs-lookup"><span data-stu-id="81340-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="81340-333">Número total de columnas = 14</span><span class="sxs-lookup"><span data-stu-id="81340-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="81340-334">Informe con el número de filas y columnas de la tabla <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="81340-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="81340-335">Número total de filas = 173179759</span><span class="sxs-lookup"><span data-stu-id="81340-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="81340-336">Número total de columnas = 11</span><span class="sxs-lookup"><span data-stu-id="81340-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="81340-337">Lectura de un pequeño datos de ejemplo de Hola base de datos de almacenamiento de datos de SQL</span><span class="sxs-lookup"><span data-stu-id="81340-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="81340-338">Tabla de ejemplo de Hola de tiempo tooread es 14.096495 segundos.</span><span class="sxs-lookup"><span data-stu-id="81340-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="81340-339">Número de filas y columnas recuperadas = (1000, 21)</span><span class="sxs-lookup"><span data-stu-id="81340-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="81340-340">Estadísticas descriptivas</span><span class="sxs-lookup"><span data-stu-id="81340-340">Descriptive statistics</span></span>
<span data-ttu-id="81340-341">Ahora está listo tooexplore Hola muestreada datos.</span><span class="sxs-lookup"><span data-stu-id="81340-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="81340-342">Empezaremos con mirando algunas estadísticas descriptivas para hello **recorridos\_distancia** (o cualquier otro campo elija toospecify).</span><span class="sxs-lookup"><span data-stu-id="81340-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="81340-343">Visualización: ejemplo de diagrama de caja</span><span class="sxs-lookup"><span data-stu-id="81340-343">Visualization: Box plot example</span></span>
<span data-ttu-id="81340-344">A continuación, veremos caja Hola para Hola de ida y vuelta distancia toovisualize hello cuantiles.</span><span class="sxs-lookup"><span data-stu-id="81340-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagrama 1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="81340-346">Visualización: ejemplo de diagrama de distribución</span><span class="sxs-lookup"><span data-stu-id="81340-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="81340-347">Los trazados que visualización la distribución de Hola y un histograma para hello muestrearon las distancias de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="81340-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagrama 2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="81340-349">Visualización: diagramas de barras y líneas</span><span class="sxs-lookup"><span data-stu-id="81340-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="81340-350">En este ejemplo, hemos discretizar distancia de viaje hello en cinco cubos y visualizar Hola discretizar los resultados.</span><span class="sxs-lookup"><span data-stu-id="81340-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="81340-351">Podemos trazar Hola por encima de la distribución de la Papelera de una barra o línea trazado con:</span><span class="sxs-lookup"><span data-stu-id="81340-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagrama 3][3]

<span data-ttu-id="81340-353">y</span><span class="sxs-lookup"><span data-stu-id="81340-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagrama 4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="81340-355">Visualización: ejemplos de gráfico de dispersión</span><span class="sxs-lookup"><span data-stu-id="81340-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="81340-356">Se muestra el gráfico de dispersión entre **recorridos\_tiempo\_en\_s** y **recorridos\_distancia** toosee si hay alguna correlación</span><span class="sxs-lookup"><span data-stu-id="81340-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagrama 6][6]

<span data-ttu-id="81340-358">De igual forma podemos comprobar relación Hola entre **velocidad\_código** y **recorridos\_distancia**.</span><span class="sxs-lookup"><span data-stu-id="81340-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagrama 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="81340-360">Exploración de datos en datos de muestreo mediante consultas SQL en IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="81340-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="81340-361">En esta sección, exploramos distribuciones de datos utilizando los datos de hello muestreada que se guardan en la nueva tabla de hello que hemos creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="81340-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="81340-362">Tenga en cuenta que se pueden realizar exploraciones similar mediante tablas originales de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="81340-363">Exploración: Número de informes de filas y columnas de hello muestreadas tabla</span><span class="sxs-lookup"><span data-stu-id="81340-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="81340-364">Exploración: distribución con propinas y sin propinas</span><span class="sxs-lookup"><span data-stu-id="81340-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="81340-365">Exploración: distribución de clases de propinas</span><span class="sxs-lookup"><span data-stu-id="81340-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="81340-366">Exploración: Trazar la distribución de la sugerencia de Hola por clase</span><span class="sxs-lookup"><span data-stu-id="81340-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Diagrama 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="81340-368">Exploración: distribución diaria de carreras</span><span class="sxs-lookup"><span data-stu-id="81340-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="81340-369">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="81340-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="81340-370">Exploración: distribución de carreras por placa y número de licencia</span><span class="sxs-lookup"><span data-stu-id="81340-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="81340-371">Exploración: distribución del tiempo de la carrera</span><span class="sxs-lookup"><span data-stu-id="81340-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="81340-372">Exploración: distribución de la distancia de la carrera</span><span class="sxs-lookup"><span data-stu-id="81340-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="81340-373">Exploración: distribución del tipo de pago</span><span class="sxs-lookup"><span data-stu-id="81340-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="81340-374">Comprobar el formulario final de Hola de tabla de caracterizará Hola</span><span class="sxs-lookup"><span data-stu-id="81340-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="81340-375"><a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="81340-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="81340-376">Ahora estamos listos tooproceed toomodel creación e implementación de modelo en [aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="81340-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="81340-377">datos Hello están listo toobe usado en cualquiera de los problemas de predicción de hello identificados anteriormente, a saber:</span><span class="sxs-lookup"><span data-stu-id="81340-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="81340-378">**Clasificación binaria**: toopredict o no se pagó una sugerencia para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="81340-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="81340-379">**Clasificación multiclase**: intervalo de hello toopredict de sugerencia de pago, según toohello clases definidas previamente.</span><span class="sxs-lookup"><span data-stu-id="81340-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="81340-380">**Tarea de regresión**: cantidad de hello toopredict de sugerencia de pago para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="81340-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="81340-381">toobegin Hola modelado ejercicio, inicie sesión en tooyour **aprendizaje automático de Azure** área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="81340-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="81340-382">Si aún no ha creado un área de trabajo de aprendizaje automático, consulte [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="81340-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="81340-383">tooget a trabajar con aprendizaje automático de Azure, consulte [¿qué es el estudio de aprendizaje automático de Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="81340-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="81340-384">Inicie sesión demasiado[estudio de aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="81340-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="81340-385">página de inicio de Studio Hola proporciona una gran cantidad de información, vídeos, tutoriales, vínculos toohello referencia de módulos y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="81340-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="81340-386">Para obtener más información acerca de aprendizaje automático de Azure, consulte hello [centro de documentación de aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="81340-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="81340-387">Un experimento de entrenamiento típico consta de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="81340-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="81340-388">Crear un experimento **+NUEVO** .</span><span class="sxs-lookup"><span data-stu-id="81340-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="81340-389">Obtener datos de hello en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="81340-390">Preprocesar, transformar y manipular datos Hola según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="81340-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="81340-391">Generar características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="81340-391">Generate features as needed.</span></span>
5. <span data-ttu-id="81340-392">Dividir los datos de hello en conjuntos de datos de entrenamiento / / pruebas de validación (o tiene conjuntos de datos independiente para cada uno).</span><span class="sxs-lookup"><span data-stu-id="81340-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="81340-393">Seleccionar algoritmos función hello toosolve problema de aprendizaje de aprendizaje automático de uno o más.</span><span class="sxs-lookup"><span data-stu-id="81340-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="81340-394">Por ejemplo: clasificación binaria, clasificación multiclase, regresión.</span><span class="sxs-lookup"><span data-stu-id="81340-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="81340-395">Entrenar uno o varios modelos utilizando el conjunto de datos de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="81340-396">Puntuación Hola de conjunto de datos de validación utilizando modelos entrenados Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="81340-397">Evaluar Hola modelos toocompute Hola métricas pertinente para hello problema de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="81340-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="81340-398">Ajustar los modelos de Hola y Hola seleccione mejor modelo toodeploy.</span><span class="sxs-lookup"><span data-stu-id="81340-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="81340-399">En este ejercicio, hemos ya explorar e ingeniería datos hello en el almacén de datos de SQL y decidido tooingest de tamaño de ejemplo de Hola en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="81340-400">Aquí es Hola procedimiento toobuild uno o varios de los modelos de predicción de hello:</span><span class="sxs-lookup"><span data-stu-id="81340-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="81340-401">Obtener datos de hello en aprendizaje automático de Azure con hello [importar datos] [ import-data] módulo, disponibles en hello **datos de entrada y salida** sección.</span><span class="sxs-lookup"><span data-stu-id="81340-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="81340-402">Para obtener más información, vea hello [importar datos] [ import-data] página de referencia de módulo.</span><span class="sxs-lookup"><span data-stu-id="81340-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Datos de importación de Aprendizaje automático de Azure][17]
2. <span data-ttu-id="81340-404">Seleccione **base de datos de SQL Azure** como hello **origen de datos** en hello **propiedades** panel.</span><span class="sxs-lookup"><span data-stu-id="81340-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="81340-405">Escriba el nombre DNS de base de datos de Hola Hola **el nombre del servidor de base de datos** campo.</span><span class="sxs-lookup"><span data-stu-id="81340-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="81340-406">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="81340-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="81340-407">Escriba hello **nombre de base de datos** en el campo correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="81340-408">Escriba hello *nombre de usuario SQL* en hello **nombre de cuenta de usuario de servidor**, hello y *contraseña* en hello **contraseña de cuenta de usuario de servidor**.</span><span class="sxs-lookup"><span data-stu-id="81340-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="81340-409">Comprobar hello **Aceptar cualquier certificado de servidor** opción.</span><span class="sxs-lookup"><span data-stu-id="81340-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="81340-410">Hola **consulta de base de datos** editar el área de texto, pegue la consulta de Hola que extrae Hola necesarios campos (incluidos los campos calculados, como las etiquetas de hello) de la base de datos y el detalle de ejemplos de tamaño de la muestra de Hola datos toohello deseado.</span><span class="sxs-lookup"><span data-stu-id="81340-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="81340-411">Es un ejemplo de un experimento de clasificación binaria leer los datos directamente desde la base de datos de almacenamiento de datos SQL de hello en figura Hola siguiente (recuerde tooreplace Hola nombres de tabla nyctaxi_trip y nyctaxi_fare por esquema Hola hello y nombre de los nombres de tabla que usó en el tutorial).</span><span class="sxs-lookup"><span data-stu-id="81340-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="81340-412">Se pueden construir experimentos similares para problemas de clasificación multiclase y de regresión.</span><span class="sxs-lookup"><span data-stu-id="81340-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Entrenamiento de Aprendizaje automático de Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="81340-414">Hola, extracción de datos de modelado y realizando un muestreo ejemplos de consultas que se proporcionan en las secciones anteriores, **todas las etiquetas de ejercicios de modelado de hello tres se incluyen en la consulta de hello**.</span><span class="sxs-lookup"><span data-stu-id="81340-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="81340-415">Un paso importante (obligatorio) en cada uno de los ejercicios de modelado de hello es demasiado**excluir** Hola etiquetas innecesarias para hello otros problemas de dos y cualquier otro **destino pérdidas**.</span><span class="sxs-lookup"><span data-stu-id="81340-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="81340-416">Por ejemplo, cuando se usa la clasificación binaria, usar etiqueta hello **superpuesto** y excluir los campos de hello **sugerencia\_clase**, **sugerencia\_cantidad**, y **total\_cantidad**.</span><span class="sxs-lookup"><span data-stu-id="81340-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="81340-417">Hola este último se pagan de pérdidas de destino ya que implican sugerencia Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="81340-418">tooexclude las columnas innecesarias o pérdidas de destino, puede usar hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo o hello [editar metadatos] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="81340-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="81340-419">Para obtener más información, consulte las páginas de referencia de [Seleccionar columnas de conjunto de datos][select-columns] y [Editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="81340-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="81340-420"><a name="mldeploy"></a>Implementación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="81340-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="81340-421">Cuando el modelo está listo, puede implementar fácilmente como un servicio web directamente desde el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="81340-422">Para obtener más información sobre la implementación de servicios web de Aprendizaje automático de Azure, vea [Implementación de un servicio web de Aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="81340-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="81340-423">toodeploy un nuevo servicio web, debe:</span><span class="sxs-lookup"><span data-stu-id="81340-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="81340-424">Crear un experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="81340-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="81340-425">Implementar el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-425">Deploy hello web service.</span></span>

<span data-ttu-id="81340-426">toocreate una puntuación experimentar de un **finalizado** experimento de entrenamiento, haga clic en **crear EXPERIMENTO de puntuación** en la barra de acción inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Puntuación de Azure][18]

<span data-ttu-id="81340-428">Aprendizaje automático de Azure intentará toocreate un experimento de puntuación en función de los componentes de hello del experimento de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="81340-429">En concreto, hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="81340-429">In particular, it will:</span></span>

1. <span data-ttu-id="81340-430">Guardar modelo entrenado hello y quite los módulos de entrenamiento del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="81340-431">Identificar un valor lógico **puerto de entrada** toorepresent Hola esperaba el esquema de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="81340-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="81340-432">Identificar un valor lógico **puerto de salida** esquema de salida del servicio de toorepresent hello web esperado.</span><span class="sxs-lookup"><span data-stu-id="81340-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="81340-433">Cuando se crea el experimento de puntuación de hello, revisarlo y asegúrese de ajustar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="81340-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="81340-434">Un ajuste típico es el conjunto de datos de entrada de hello tooreplace o consulta con uno que excluye los campos de etiqueta, ya estos no estarán disponibles cuando se llama servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="81340-435">También es que un tamaño de hello tooreduce buenas prácticas de hello entrada tooa de conjunto de datos o de consultas pocos registros, suficiente esquema de entrada tooindicate Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="81340-436">Para el puerto de salida de hello, es común tooexclude entrados todos los campos y solo se incluyen hello **puntuación de etiquetas** y **probabilidades con puntuación** Hola Hola de salida [seleccionar columnas de conjunto de datos ] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="81340-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="81340-437">Se proporciona un ejemplo experimento de puntuación en hello siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="81340-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="81340-438">Cuando esté listo toodeploy, haga clic en hello **publicar servicio WEB** botón de barra de acción de hello inferior.</span><span class="sxs-lookup"><span data-stu-id="81340-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publicación de Aprendizaje automático de Azure][11]

## <a name="summary"></a><span data-ttu-id="81340-440">Resumen</span><span class="sxs-lookup"><span data-stu-id="81340-440">Summary</span></span>
<span data-ttu-id="81340-441">toorecap lo que hemos realizado en este tutorial del tutorial, ha creado un entorno de ciencia de datos de Azure, ha trabajado con un gran conjunto de datos público, si vamos a través del proceso de ciencia de datos de equipo, todas las forma de Hola de entrenamiento de toomodel de adquisición de datos, de hello y, a continuación, toohello la implementación de un servicio web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="81340-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="81340-442">Información de licencia</span><span class="sxs-lookup"><span data-stu-id="81340-442">License information</span></span>
<span data-ttu-id="81340-443">En este tutorial de ejemplo y sus elementos notebook(s) IPython y secuencias de comandos que se comparten por Microsoft bajo licencia MIT de Hola.</span><span class="sxs-lookup"><span data-stu-id="81340-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="81340-444">Compruebe archivo LICENSE.txt de hello directorio de hello del código de ejemplo de Hola en GitHub para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="81340-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="81340-445">Referencias</span><span class="sxs-lookup"><span data-stu-id="81340-445">References</span></span>
<span data-ttu-id="81340-446">•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="81340-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="81340-447">•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="81340-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="81340-448">•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="81340-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
