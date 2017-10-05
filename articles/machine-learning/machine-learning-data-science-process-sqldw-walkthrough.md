---
title: "Proceso de ciencia de datos en equipos en acción: uso de SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: ce7de48af0f2f21576c66a962b88635a0f9f8333
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="390d0-103">Proceso de ciencia de datos en equipos en acción: uso de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="390d0-103">The Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="390d0-104">En este tutorial le guiaremos a través de la creación e implementación de un modelo de aprendizaje automático mediante Almacenamiento de datos SQL (SQL DW) para un conjunto de datos disponible públicamente: el conjunto de datos [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) .</span><span class="sxs-lookup"><span data-stu-id="390d0-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="390d0-105">El modelo de clasificación binaria construido predice si se va a pagar o no una propina para la carrera, y también se describen los modelos de clasificación y regresión multiclase que predicen la distribución de los importes pagados en concepto de propina.</span><span class="sxs-lookup"><span data-stu-id="390d0-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span></span>

<span data-ttu-id="390d0-106">El procedimiento sigue el flujo de trabajo del [proceso de ciencia de datos en equipos (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) .</span><span class="sxs-lookup"><span data-stu-id="390d0-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="390d0-107">Se muestra cómo configurar un entorno de ciencia de datos, cómo cargar los datos en Almacenamiento de datos SQL y cómo usar Almacenamiento de datos SQL o un IPython Notebook para explorar las características de datos y de diseño para modelar.</span><span class="sxs-lookup"><span data-stu-id="390d0-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span></span> <span data-ttu-id="390d0-108">Luego se muestra cómo compilar e implementar un modelo con Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-108">We then show how to build and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="390d0-109"><a name="dataset"></a>Conjunto de datos NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="390d0-109"><a name="dataset"></a>The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="390d0-110">El conjunto de datos NYC Taxi Trips consta de aproximadamente 20 GB de archivos de valores separados por comas (CSV) comprimidos (aproximadamente, 48 GB sin comprimir), que registran más de 173 millones de carreras individuales y las tarifas pagadas por cada carrera.</span><span class="sxs-lookup"><span data-stu-id="390d0-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="390d0-111">Cada registro de carrera incluye la hora y el lugar de recogida y llegada, el número de licencia del taxista anonimizado y el número de placa (número de identificación único del taxi).</span><span class="sxs-lookup"><span data-stu-id="390d0-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="390d0-112">Los datos cubren todos los viajes del año 2013 y se proporcionan en los dos conjuntos de datos siguientes para cada mes:</span><span class="sxs-lookup"><span data-stu-id="390d0-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="390d0-113">El archivo **trip_data.csv** contiene información detallada de las carreras, como el número de pasajeros, los puntos de recogida y destino, la duración de las carreras y la longitud del recorrido.</span><span class="sxs-lookup"><span data-stu-id="390d0-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="390d0-114">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="390d0-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="390d0-115">El archivo **trip_fare.csv** contiene información detallada de la tarifa que se paga en cada carrera, como el tipo de pago, el importe de la tarifa, los suplementos e impuestos, las propinas y los peajes, y el importe total pagado.</span><span class="sxs-lookup"><span data-stu-id="390d0-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="390d0-116">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="390d0-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="390d0-117">La **clave única** para unir trip\_data y trip\_fare se compone de los tres campos siguientes:</span><span class="sxs-lookup"><span data-stu-id="390d0-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span></span>

* <span data-ttu-id="390d0-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="390d0-118">medallion,</span></span>
* <span data-ttu-id="390d0-119">hack\_license y</span><span class="sxs-lookup"><span data-stu-id="390d0-119">hack\_license and</span></span>
* <span data-ttu-id="390d0-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="390d0-120">pickup\_datetime.</span></span>

## <span data-ttu-id="390d0-121"><a name="mltasks"></a>Realicemos tres tipos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="390d0-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="390d0-122">Se formulan tres problemas de predicción basados en el valor *tip\_amount* para mostrar tres tipos de tareas de modelado:</span><span class="sxs-lookup"><span data-stu-id="390d0-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="390d0-123">**Clasificación binaria**: permite predecir si se pagó una propina tras una carrera, o no; es decir, un valor de *tip\_amount* mayor que 0 $ es un ejemplo positivo, mientras que un valor de *tip\_amount* de 0 $ es un ejemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="390d0-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="390d0-124">**Clasificación con múltiples clases**: para predecir el intervalo de la propina de la carrera.</span><span class="sxs-lookup"><span data-stu-id="390d0-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="390d0-125">Dividimos *tip\_amount* en cinco ubicaciones o clases:</span><span class="sxs-lookup"><span data-stu-id="390d0-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="390d0-126">**Tarea de regresión**: para predecir la cantidad de propina pagada en una carrera.</span><span class="sxs-lookup"><span data-stu-id="390d0-126">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="390d0-127"><a name="setup"></a>Configuración del entorno de ciencia de datos de Azure para análisis avanzado</span><span class="sxs-lookup"><span data-stu-id="390d0-127"><a name="setup"></a>Set up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="390d0-128">Para configurar el entorno de ciencia de datos de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="390d0-128">To set up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="390d0-129">**Cree su propia cuenta de Almacenamiento de blobs de Azure.**</span><span class="sxs-lookup"><span data-stu-id="390d0-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="390d0-130">Cuando aprovisione su propia instancia de Azure Blob Storage, elija una ubicación geográfica para esta en la región **centro-sur de EE.UU.**, o lo más cerca posible de esta región, ya que es donde se almacenan los datos de NYC Taxi.</span><span class="sxs-lookup"><span data-stu-id="390d0-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span></span> <span data-ttu-id="390d0-131">Los datos se copian con AzCopy desde el contenedor de Almacenamiento de blobs público a un contenedor de su propia cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="390d0-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span></span> <span data-ttu-id="390d0-132">Cuanto más se acerque el Almacenamiento de blobs de Azure a la región centro-sur de EE. UU., más rápida se completará esta tarea (paso 4).</span><span class="sxs-lookup"><span data-stu-id="390d0-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="390d0-133">Para crear una cuenta propia de almacenamiento de Azure, siga los pasos descritos en [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="390d0-134">Asegúrese de hacer anotaciones en los valores de las credenciales de la cuenta de almacenamiento siguientes, que necesitará más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="390d0-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="390d0-135">**Nombre de cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="390d0-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="390d0-136">**Clave de cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="390d0-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="390d0-137">**Nombre de contenedor** (en donde los datos se van a almacenar en el Almacenamiento de blobs de Azure)</span><span class="sxs-lookup"><span data-stu-id="390d0-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span></span>

<span data-ttu-id="390d0-138">**Aprovisione la instancia de Almacenamiento de datos SQL de Azure.**</span><span class="sxs-lookup"><span data-stu-id="390d0-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="390d0-139">Siga la documentación de [Creación de Almacenamiento de datos SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para aprovisionar una instancia de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="390d0-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="390d0-140">Asegúrese de que hacer anotaciones en las credenciales de Almacenamiento de datos SQL siguientes que se usarán en los pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="390d0-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="390d0-141">**Nombre del servidor**: <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="390d0-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="390d0-142">**Nombre de SQLDW (base de datos)**</span><span class="sxs-lookup"><span data-stu-id="390d0-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="390d0-143">**Nombre de usuario**</span><span class="sxs-lookup"><span data-stu-id="390d0-143">**Username**</span></span>
* <span data-ttu-id="390d0-144">**Password**</span><span class="sxs-lookup"><span data-stu-id="390d0-144">**Password**</span></span>

<span data-ttu-id="390d0-145">**Instale Visual Studio y SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="390d0-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="390d0-146">Para ver instrucciones, consulte [Instalación de Visual Studio 2015 y SSDT para Almacenamiento de datos SQL](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="390d0-147">**Conéctese a Almacenamiento de datos SQL de Azure con Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="390d0-147">**Connect to your Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="390d0-148">Para obtener instrucciones, consulte los pasos 1 y 2 de [Conexión a Azure SQL Data Warehouse con Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="390d0-149">Ejecute la siguiente consulta SQL en la base de datos que creó en SQL Data Warehouse (en lugar de la consulta proporcionada en el paso 3 del tema sobre la conexión) para **crear una clave maestra**.</span><span class="sxs-lookup"><span data-stu-id="390d0-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try to create the master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If the master key exists, do nothing
    END CATCH;

<span data-ttu-id="390d0-150">**Cree un área de trabajo de Azure Machine Learning en su suscripción de Azure.**</span><span class="sxs-lookup"><span data-stu-id="390d0-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="390d0-151">Para ver instrucciones, consulte [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="390d0-152"><a name="getdata"></a>Carga de datos en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="390d0-152"><a name="getdata"></a>Load the data into SQL Data Warehouse</span></span>
<span data-ttu-id="390d0-153">Abra una consola de comandos de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="390d0-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="390d0-154">Ejecute los comandos de PowerShell siguientes para descargar los archivos de script SQL de ejemplo que compartimos en GitHub en un directorio local especificado con el parámetro *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="390d0-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span></span> <span data-ttu-id="390d0-155">Puede cambiar el valor del parámetro *-DestDir* en cualquier directorio local.</span><span class="sxs-lookup"><span data-stu-id="390d0-155">You can change the value of parameter *-DestDir* to any local directory.</span></span> <span data-ttu-id="390d0-156">Si *-DestDir* no existe, lo creará el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="390d0-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="390d0-157">Es posible que necesite **ejecutar como administrador** el siguiente script de PowerShell si su directorio *DestDir* necesita privilegios de administrador para crearlo o escribir en él.</span><span class="sxs-lookup"><span data-stu-id="390d0-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="390d0-158">Cuando se haya ejecutado correctamente, el directorio de trabajo actual cambia a *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="390d0-158">After successful execution, your current working directory changes to *-DestDir*.</span></span> <span data-ttu-id="390d0-159">Debe ver una pantalla similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="390d0-159">You should be able to see screen like below:</span></span>

![][19]

<span data-ttu-id="390d0-160">En su *-DestDir*, ejecute el siguiente script de PowerShell en modo de administrador:</span><span class="sxs-lookup"><span data-stu-id="390d0-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="390d0-161">Cuando se ejecuta el script de PowerShell por primera vez, se le pedirá que introduzca información desde Almacenamiento de datos SQL de Azure y la cuenta de Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="390d0-162">Cuando este script de PowerShell termine de ejecutarse por primera vez, las credenciales indicadas se habrán escrito en un archivo de configuración SQLDW.conf del directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="390d0-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span></span> <span data-ttu-id="390d0-163">La ejecución futura de este archivo de script de PowerShell puede leer todos los parámetros necesarios de este archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="390d0-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span></span> <span data-ttu-id="390d0-164">Si necesita cambiar algunos parámetros, puede elegir escribir los parámetros en la pantalla después del aviso mediante la eliminación de este archivo de configuración y de escribir los valores de parámetros cuando se le solicite o cambiar los valores de parámetros mediante la edición del archivo SQLDW.conf en el directorio *-DestDir* .</span><span class="sxs-lookup"><span data-stu-id="390d0-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="390d0-165">Para evitar conflictos de nombres de esquema con los que ya existen en Almacenamiento de datos SQL de Azure, al leer los parámetros directamente desde el archivo SQLDW.conf, se agrega un número aleatorio de tres dígitos al nombre del esquema desde el archivo SQLDW.conf como el nombre de esquema predeterminado para cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="390d0-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span></span> <span data-ttu-id="390d0-166">El script de PowerShell puede pedirle un nombre de esquema: se puede especificar el nombre a discreción del usuario.</span><span class="sxs-lookup"><span data-stu-id="390d0-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="390d0-167">Este archivo de **script de PowerShell** realiza las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="390d0-167">This **PowerShell script** file completes the following tasks:</span></span>

* <span data-ttu-id="390d0-168">**Descarga e instala AzCopy**, si AzCopy no se ha instalado aún</span><span class="sxs-lookup"><span data-stu-id="390d0-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
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
* <span data-ttu-id="390d0-169">**Copia datos en la cuenta de Almacenamiento de blobs privada** desde el blob público con AzCopy</span><span class="sxs-lookup"><span data-stu-id="390d0-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob to yo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account to verify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob to your storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="390d0-170">**Carga datos mediante Polybase (mediante la ejecución de LoadDataToSQLDW.sql) para el Almacenamiento de datos SQL de Azure** de la cuenta de almacenamiento de blobs privada con los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="390d0-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span></span>
  
  * <span data-ttu-id="390d0-171">Creación de un esquema</span><span class="sxs-lookup"><span data-stu-id="390d0-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="390d0-172">Creación de una credencial con ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="390d0-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="390d0-173">Creación de un origen de datos externo para un blob de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="390d0-173">Create an external data source for an Azure storage blob</span></span>
    
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
  * <span data-ttu-id="390d0-174">Cree un formato de archivo externo para un archivo .csv.</span><span class="sxs-lookup"><span data-stu-id="390d0-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="390d0-175">Los datos se descomprimen y los campos se separan con el carácter de barra vertical.</span><span class="sxs-lookup"><span data-stu-id="390d0-175">Data is uncompressed and fields are separated with the pipe character.</span></span>
    
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
  * <span data-ttu-id="390d0-176">Cree tablas externas de tarifas y propinas para el conjunto de datos de NYC Taxi en el Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
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

    - <span data-ttu-id="390d0-177">Carga de datos de tablas externas del Almacenamiento de blobs de Azure en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="390d0-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span></span>

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

    - <span data-ttu-id="390d0-178">Cree una tabla de datos de ejemplo (NYCTaxi_Sample) e inserte datos en ella mediante la selección de consultas SQL en las tablas de carreras y tarifas.</span><span class="sxs-lookup"><span data-stu-id="390d0-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span></span> <span data-ttu-id="390d0-179">(Algunos pasos de este tutorial necesitan usar esta tabla de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="390d0-179">(Some steps of this walkthrough needs to use this sample table.)</span></span>

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

<span data-ttu-id="390d0-180">La ubicación geográfica de las cuentas de almacenamiento afecta a los tiempos de carga.</span><span class="sxs-lookup"><span data-stu-id="390d0-180">The geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="390d0-181">Según la ubicación geográfica de la cuenta de almacenamiento de blobs privada, el proceso de copiar datos de un blob público a su cuenta de almacenamiento privada puede tardar unos 15 minutos o incluso más tiempo, y el proceso de carga de datos desde la cuenta de almacenamiento al Almacenamiento de datos SQL de Azure podría tardar 20 minutos o más tiempo.</span><span class="sxs-lookup"><span data-stu-id="390d0-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="390d0-182">Tendrá que decidir qué hacer si tiene archivos de origen y de destino duplicados.</span><span class="sxs-lookup"><span data-stu-id="390d0-182">You will have to decide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="390d0-183">Si los archivos .csv que se van a copiar desde el almacenamiento de blobs público a la cuenta de almacenamiento de blobs privada ya existen en la cuenta de almacenamiento de blobs privada, AzCopy le preguntará si desea sobrescribirlos.</span><span class="sxs-lookup"><span data-stu-id="390d0-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span></span> <span data-ttu-id="390d0-184">Si no desea sobrescribirlos, escriba **n** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="390d0-184">If you do not want to overwrite them, input **n** when prompted.</span></span> <span data-ttu-id="390d0-185">Si desea sobrescribir **todos** ellos, escriba **a** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="390d0-185">If you want to overwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="390d0-186">También puede escribir **y** para sobrescribir los archivos .csv individualmente.</span><span class="sxs-lookup"><span data-stu-id="390d0-186">You can also input **y** to overwrite .csv files individually.</span></span>
> 
> 

![Diagrama 21][21]

<span data-ttu-id="390d0-188">Puede usar sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="390d0-188">You can use your own data.</span></span> <span data-ttu-id="390d0-189">Si los datos están en la máquina local en la aplicación de la vida real, todavía puede usar AzCopy para cargar los datos locales a su área privada de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="390d0-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy to upload on-premises data to your private Azure blob storage.</span></span> <span data-ttu-id="390d0-190">Solo tiene que cambiar la ubicación de **origen**, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, en el comando de AzCopy del archivo de scripts de PowerShell por un directorio local que contiene los datos.</span><span class="sxs-lookup"><span data-stu-id="390d0-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="390d0-191">Si los datos ya están en el Almacenamiento de blobs de Azure privado en la aplicación de la vida real, puede omitir el paso de AzCopy en el script de PowerShell y cargar directamente los datos en Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span></span> <span data-ttu-id="390d0-192">Esto requerirá modificaciones adicionales del script para adaptarlo al formato de los datos.</span><span class="sxs-lookup"><span data-stu-id="390d0-192">This will require additional edits of the script to tailor it to the format of your data.</span></span>
> 
> 

<span data-ttu-id="390d0-193">Este script de Powershell también conecta la información de Almacenamiento de datos SQL de Azure en los archivos de ejemplo de exploración de datos SQLDW_Explorations.sql, SQLDW_Explorations.ipynb y SQLDW_Explorations_Scripts.py para que estos tres archivos están listos para ser probados de inmediato cuando finalice el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="390d0-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span></span>

<span data-ttu-id="390d0-194">Después de una ejecución correcta, verá una pantalla similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="390d0-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="390d0-195"><a name="dbexplore"></a>Exploración de datos y diseño de características en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="390d0-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="390d0-196">En esta sección, realizamos la generación de características y la exploración de datos mediante la ejecución de consultas SQL en Almacenamiento de datos SQL de Azure directamente mediante **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="390d0-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="390d0-197">Todas las consultas SQL que se usan en esta sección se pueden encontrar en el script de ejemplo llamado *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="390d0-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="390d0-198">Este archivo ya lo ha descargado en el directorio local el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="390d0-198">This file has already been downloaded to your local directory by the PowerShell script.</span></span> <span data-ttu-id="390d0-199">También puede recuperarlo desde [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="390d0-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="390d0-200">Pero el archivo de GitHub no tiene la información de Azure SQL DW conectada.</span><span class="sxs-lookup"><span data-stu-id="390d0-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="390d0-201">Conéctese con Almacenamiento de datos SQL de Azure utilizando Visual Studio con el nombre de inicio de sesión de Almacenamiento de datos SQL y la contraseña y abra el **Explorador de objetos SQL** para confirmar que la base de datos y las tablas se han importado.</span><span class="sxs-lookup"><span data-stu-id="390d0-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span></span> <span data-ttu-id="390d0-202">Recupere el archivo *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="390d0-202">Retrieve the *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="390d0-203">Para abrir un editor de consultas de Almacenamiento de datos paralelos (PDW), utilice el comando **Nueva consulta** mientras el PDW está seleccionado en el **Explorador de objetos SQL**.</span><span class="sxs-lookup"><span data-stu-id="390d0-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span></span> <span data-ttu-id="390d0-204">El editor de consultas estándar de SQL no es compatible con PDW.</span><span class="sxs-lookup"><span data-stu-id="390d0-204">The standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="390d0-205">A continuación se muestra el tipo de tareas de exploración de datos y de generación de características realizado en esta sección:</span><span class="sxs-lookup"><span data-stu-id="390d0-205">Here are the type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="390d0-206">Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="390d0-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="390d0-207">Investigar la calidad de los datos de los campos de longitud y latitud.</span><span class="sxs-lookup"><span data-stu-id="390d0-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="390d0-208">Generar etiquetas de clasificación binaria y multiclase según **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="390d0-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="390d0-209">Generar características y calcular o comparar distancias de carreras.</span><span class="sxs-lookup"><span data-stu-id="390d0-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="390d0-210">Combinar las dos tablas y extraer una muestra aleatoria que se usará para generar modelos.</span><span class="sxs-lookup"><span data-stu-id="390d0-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="390d0-211">Comprobación de la importación de datos</span><span class="sxs-lookup"><span data-stu-id="390d0-211">Data import verification</span></span>
<span data-ttu-id="390d0-212">Estas consultas proporcionan una comprobación rápida del número de filas y columnas en las tablas que se rellenaron anteriormente mediante la importación masiva paralela de Polybase.</span><span class="sxs-lookup"><span data-stu-id="390d0-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="390d0-213">**Salida:** debe obtener 173 179 759 filas y 14 columnas.</span><span class="sxs-lookup"><span data-stu-id="390d0-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="390d0-214">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="390d0-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="390d0-215">Esta consulta de ejemplo identifica las licencias (números de taxi) que han completado más de 100 carreras dentro de un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="390d0-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="390d0-216">La consulta se beneficiaría del acceso de la tabla con particiones, ya que está condicionada por el esquema de partición de **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="390d0-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="390d0-217">La consulta el conjunto de datos completo también hará uso de la tabla con particiones o del recorrido de índice.</span><span class="sxs-lookup"><span data-stu-id="390d0-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="390d0-218">**Salida:** la consulta debe devolver una tabla con filas en las que se especifiquen las 13 369 licencias (taxis) y el número de carreras completadas por ellos en 2013.</span><span class="sxs-lookup"><span data-stu-id="390d0-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span></span> <span data-ttu-id="390d0-219">La última columna contiene el recuento del número de carreras realizadas.</span><span class="sxs-lookup"><span data-stu-id="390d0-219">The last column contains the count of the number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="390d0-220">Exploración: distribución de carreras por medallion y hack_license</span><span class="sxs-lookup"><span data-stu-id="390d0-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="390d0-221">Este ejemplo identifica las licencias (números de taxi) y los números de hack_license (conductores) que han completado más de 100 carreras dentro de un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="390d0-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="390d0-222">**Salida:** la consulta debe devolver una tabla con 13 369 filas en las que se especifiquen los 13 369 identificadores de vehículo/conductor que han realizado más de 100 carreras en 2013.</span><span class="sxs-lookup"><span data-stu-id="390d0-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="390d0-223">La última columna contiene el recuento del número de carreras realizadas.</span><span class="sxs-lookup"><span data-stu-id="390d0-223">The last column contains the count of the number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="390d0-224">Evaluación de la calidad de los datos: comprobar los registros con longitud o latitud incorrectas</span><span class="sxs-lookup"><span data-stu-id="390d0-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="390d0-225">En este ejemplo se investiga si alguno de los campos de longitud y latitud contiene un valor no válido (los grados radianes deben encontrarse entre -90 y 90) o tienen coordenadas (0, 0).</span><span class="sxs-lookup"><span data-stu-id="390d0-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="390d0-226">**Salida:** la consulta devuelve 837 467 carreras con campos de latitud o longitud no válidos.</span><span class="sxs-lookup"><span data-stu-id="390d0-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="390d0-227">Exploración: distribución de carreras con propinas frente a sin propinas</span><span class="sxs-lookup"><span data-stu-id="390d0-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="390d0-228">Este ejemplo busca el número de carreras en las que se han dado propinas frente a aquellas en las que no se han dado en un período de tiempo especificado (o en el conjunto de datos completo si se abarca todo el año, como se establece aquí).</span><span class="sxs-lookup"><span data-stu-id="390d0-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span></span> <span data-ttu-id="390d0-229">Esta distribución refleja la distribución de etiquetas binarias que se usará más adelante para el modelado de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="390d0-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="390d0-230">**Salida** : la consulta debe devolver las siguientes frecuencias de propinas para el año 2013: 90 447 622 con propina y 82 264 709 sin propina.</span><span class="sxs-lookup"><span data-stu-id="390d0-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="390d0-231">Exploración: distribución por intervalos y clases de propinas</span><span class="sxs-lookup"><span data-stu-id="390d0-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="390d0-232">Este ejemplo calcula la distribución de los intervalos de propinas de un período de tiempo determinado (o en el conjunto de datos completo si abarca todo el año).</span><span class="sxs-lookup"><span data-stu-id="390d0-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="390d0-233">Esta es la distribución de las clases de etiquetas que se usarán posteriormente para el modelado de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="390d0-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

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

<span data-ttu-id="390d0-234">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="390d0-234">**Output:**</span></span>

| <span data-ttu-id="390d0-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="390d0-235">tip_class</span></span> | <span data-ttu-id="390d0-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="390d0-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="390d0-237">1</span><span class="sxs-lookup"><span data-stu-id="390d0-237">1</span></span> |<span data-ttu-id="390d0-238">82 230 915</span><span class="sxs-lookup"><span data-stu-id="390d0-238">82230915</span></span> |
| <span data-ttu-id="390d0-239">2</span><span class="sxs-lookup"><span data-stu-id="390d0-239">2</span></span> |<span data-ttu-id="390d0-240">6 198 803</span><span class="sxs-lookup"><span data-stu-id="390d0-240">6198803</span></span> |
| <span data-ttu-id="390d0-241">3</span><span class="sxs-lookup"><span data-stu-id="390d0-241">3</span></span> |<span data-ttu-id="390d0-242">1 932 223</span><span class="sxs-lookup"><span data-stu-id="390d0-242">1932223</span></span> |
| <span data-ttu-id="390d0-243">0</span><span class="sxs-lookup"><span data-stu-id="390d0-243">0</span></span> |<span data-ttu-id="390d0-244">82 264 625</span><span class="sxs-lookup"><span data-stu-id="390d0-244">82264625</span></span> |
| <span data-ttu-id="390d0-245">4</span><span class="sxs-lookup"><span data-stu-id="390d0-245">4</span></span> |<span data-ttu-id="390d0-246">85 765</span><span class="sxs-lookup"><span data-stu-id="390d0-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="390d0-247">Exploración: proceso y comparación de la distancia de la carrera</span><span class="sxs-lookup"><span data-stu-id="390d0-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="390d0-248">En este ejemplo se convierte la longitud y latitud de los puntos de recogida y destino a puntos geográficos de SQL, se calcula la distancia de la carrera mediante la diferencia de puntos geográficos de SQL y se devuelve una muestra aleatoria de los resultados de la comparación.</span><span class="sxs-lookup"><span data-stu-id="390d0-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="390d0-249">En el ejemplo se limitan los resultados a coordenadas válidas usando solo la consulta de evaluación de calidad de datos tratada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="390d0-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function to calculate the direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
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

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="390d0-250">Diseño de características con las funciones de SQL</span><span class="sxs-lookup"><span data-stu-id="390d0-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="390d0-251">A veces, las funciones de SQL pueden ser una opción eficiente de diseño de características.</span><span class="sxs-lookup"><span data-stu-id="390d0-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="390d0-252">En este tutorial, hemos definido una función SQL para calcular la distancia directa entre las ubicaciones de recogida y entrega.</span><span class="sxs-lookup"><span data-stu-id="390d0-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="390d0-253">Puede ejecutar los scripts SQL siguientes en **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="390d0-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="390d0-254">Este es el script SQL que define la función de distancia.</span><span class="sxs-lookup"><span data-stu-id="390d0-254">Here is the SQL script that defines the distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate the direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="390d0-255">Este es un ejemplo para llamar a esta función para generar características en la consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="390d0-255">Here is an example to call this function to generate features in your SQL query:</span></span>

    -- Sample query to call the function to create features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="390d0-256">**Salida:** esta consulta genera una tabla (con 2 803 538 filas) con las latitudes y longitud de los puntos de origen y destino y las distancias directas correspondientes en millas.</span><span class="sxs-lookup"><span data-stu-id="390d0-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span></span> <span data-ttu-id="390d0-257">Estos son los resultados de las tres primeras filas:</span><span class="sxs-lookup"><span data-stu-id="390d0-257">Here are the results for first 3 rows:</span></span>

|  | <span data-ttu-id="390d0-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="390d0-258">pickup_latitude</span></span> | <span data-ttu-id="390d0-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="390d0-259">pickup_longitude</span></span> | <span data-ttu-id="390d0-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="390d0-260">dropoff_latitude</span></span> | <span data-ttu-id="390d0-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="390d0-261">dropoff_longitude</span></span> | <span data-ttu-id="390d0-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="390d0-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="390d0-263">1</span><span class="sxs-lookup"><span data-stu-id="390d0-263">1</span></span> |<span data-ttu-id="390d0-264">40,731804</span><span class="sxs-lookup"><span data-stu-id="390d0-264">40.731804</span></span> |<span data-ttu-id="390d0-265">-74,001083</span><span class="sxs-lookup"><span data-stu-id="390d0-265">-74.001083</span></span> |<span data-ttu-id="390d0-266">40,736622</span><span class="sxs-lookup"><span data-stu-id="390d0-266">40.736622</span></span> |<span data-ttu-id="390d0-267">-73,988953</span><span class="sxs-lookup"><span data-stu-id="390d0-267">-73.988953</span></span> |<span data-ttu-id="390d0-268">0,7169601222</span><span class="sxs-lookup"><span data-stu-id="390d0-268">.7169601222</span></span> |
| <span data-ttu-id="390d0-269">2</span><span class="sxs-lookup"><span data-stu-id="390d0-269">2</span></span> |<span data-ttu-id="390d0-270">40,715794</span><span class="sxs-lookup"><span data-stu-id="390d0-270">40.715794</span></span> |<span data-ttu-id="390d0-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="390d0-271">-74,010635</span></span> |<span data-ttu-id="390d0-272">40,725338</span><span class="sxs-lookup"><span data-stu-id="390d0-272">40.725338</span></span> |<span data-ttu-id="390d0-273">-74,00399</span><span class="sxs-lookup"><span data-stu-id="390d0-273">-74.00399</span></span> |<span data-ttu-id="390d0-274">0,7448343721</span><span class="sxs-lookup"><span data-stu-id="390d0-274">.7448343721</span></span> |
| <span data-ttu-id="390d0-275">3</span><span class="sxs-lookup"><span data-stu-id="390d0-275">3</span></span> |<span data-ttu-id="390d0-276">40,761456</span><span class="sxs-lookup"><span data-stu-id="390d0-276">40.761456</span></span> |<span data-ttu-id="390d0-277">-73,999886</span><span class="sxs-lookup"><span data-stu-id="390d0-277">-73.999886</span></span> |<span data-ttu-id="390d0-278">40,766544</span><span class="sxs-lookup"><span data-stu-id="390d0-278">40.766544</span></span> |<span data-ttu-id="390d0-279">-73,988228</span><span class="sxs-lookup"><span data-stu-id="390d0-279">-73.988228</span></span> |<span data-ttu-id="390d0-280">0,7037227967</span><span class="sxs-lookup"><span data-stu-id="390d0-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="390d0-281">Preparar datos para la generación de modelos</span><span class="sxs-lookup"><span data-stu-id="390d0-281">Prepare data for model building</span></span>
<span data-ttu-id="390d0-282">La siguiente consulta combina las tablas **nyctaxi\_trip** y **nyctaxi\_fare**, genera una etiqueta de clasificación binaria **tipped**, una etiqueta de clasificación multiclase **tip\_class** y extrae una muestra aleatoria del conjunto de datos combinado completo.</span><span class="sxs-lookup"><span data-stu-id="390d0-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span></span> <span data-ttu-id="390d0-283">El muestreo se realiza mediante la recuperación de un subconjunto de los viajes en función de la hora de recogida.</span><span class="sxs-lookup"><span data-stu-id="390d0-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span></span>  <span data-ttu-id="390d0-284">Esta consulta se puede copiar y pegar directamente en el módulo [Importar datos](https://studio.azureml.net) de [Microsoft Azure Machine Learning Studio][import-data] para la ingesta directa de datos desde la instancia de SQL Database de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span></span> <span data-ttu-id="390d0-285">La consulta excluye los registros con coordenadas (0, 0) incorrectas.</span><span class="sxs-lookup"><span data-stu-id="390d0-285">The query excludes records with incorrect (0, 0) coordinates.</span></span>

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

<span data-ttu-id="390d0-286">Cuando esté listo para continuar con Aprendizaje automático de Azure, puede:</span><span class="sxs-lookup"><span data-stu-id="390d0-286">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="390d0-287">Guardar la consulta SQL final para extraer y muestrear los datos, y copiar y pegar la consulta directamente en un módulo [Importar datos][import-data] de Azure Machine Learning; o bien</span><span class="sxs-lookup"><span data-stu-id="390d0-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="390d0-288">Conservar los datos muestreados y de ingeniería que planea usar para la generación de modelos en una nueva tabla de SQL Data Warehouse y usar la nueva tabla en el módulo [Importar datos][import-data] de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="390d0-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="390d0-289">El script de PowerShell del paso anterior se ha encargado de hacerlo.</span><span class="sxs-lookup"><span data-stu-id="390d0-289">The PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="390d0-290">Puede leer directamente de esta tabla en el módulo Importar datos.</span><span class="sxs-lookup"><span data-stu-id="390d0-290">You can read directly from this table in the Import Data module.</span></span>

## <span data-ttu-id="390d0-291"><a name="ipnb"></a>Exploración de datos e ingeniería de características en IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="390d0-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="390d0-292">En esta sección, se llevará a cabo la exploración de datos y la generación de características con consultas Python y SQL en el Almacenamiento de datos SQL creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="390d0-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span></span> <span data-ttu-id="390d0-293">Se han descargado un cuaderno de IPython Notebook de ejemplo denominado **SQLDW_Explorations.ipynb** y un archivo de script de Python **SQLDW_Explorations_Scripts.py** en el directorio local.</span><span class="sxs-lookup"><span data-stu-id="390d0-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span></span> <span data-ttu-id="390d0-294">También están disponibles en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="390d0-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="390d0-295">Estos dos archivos son idénticos en los scripts de Python.</span><span class="sxs-lookup"><span data-stu-id="390d0-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="390d0-296">El archivo de script de Python se proporciona en caso de que no tenga un servidor de IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="390d0-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="390d0-297">Estos dos archivos de Python de muestra están diseñados en **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="390d0-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="390d0-298">La información necesaria de Almacenamiento de datos SQL de Azure en el cuaderno de IPython Notebook de ejemplo y el archivo de script de Python descargados en el equipo local está conectada por el script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="390d0-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span></span> <span data-ttu-id="390d0-299">Son ejecutables sin ninguna modificación.</span><span class="sxs-lookup"><span data-stu-id="390d0-299">They are executable without any modification.</span></span>

<span data-ttu-id="390d0-300">Si ya ha configurado un área de trabajo de Aprendizaje automático de Azure, puede cargar el cuaderno de IPython Notebook de ejemplo en el servicio IPython Notebook de Aprendizaje automático de Azure y comenzar a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="390d0-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="390d0-301">Estos son los pasos para cargar en el servicio IPython Notebook de Aprendizaje automático de Azure:</span><span class="sxs-lookup"><span data-stu-id="390d0-301">Here are the steps to upload to AzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="390d0-302">Inicie sesión en el área de trabajo de Aprendizaje automático de Azure, haga clic en "Estudio" en la parte superior y después en "CUADERNOS" en el lado izquierdo de la página web.</span><span class="sxs-lookup"><span data-stu-id="390d0-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span></span>
   
    ![Diagrama 22][22]
2. <span data-ttu-id="390d0-304">Haga clic en "NUEVO" en la esquina inferior izquierda de la página web y seleccione "Python 2".</span><span class="sxs-lookup"><span data-stu-id="390d0-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span></span> <span data-ttu-id="390d0-305">A continuación, proporcione un nombre para el cuaderno y haga clic en la marca de verificación para crear el nuevo cuaderno de IPython Notebook en blanco.</span><span class="sxs-lookup"><span data-stu-id="390d0-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span></span>
   
    ![Diagrama 23][23]
3. <span data-ttu-id="390d0-307">Haga clic en el símbolo "Jupyter" en la esquina superior izquierda del nuevo cuaderno de IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="390d0-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span></span>
   
    ![Diagrama 24][24]
4. <span data-ttu-id="390d0-309">Arrastre y coloque el cuaderno de IPython Notebook de ejemplo en la página **árbol** del servicio IPython Notebook de Azure Machine Learning y haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="390d0-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="390d0-310">A continuación, se cargará el cuaderno de IPython Notebook de ejemplo en el servicio IPython Notebook de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span></span>
   
    ![Diagrama 25][25]

<span data-ttu-id="390d0-312">Para ejecutar el cuaderno de IPython Notebook de ejemplo o el archivo de script de Python, son necesarios los siguientes paquetes Python.</span><span class="sxs-lookup"><span data-stu-id="390d0-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="390d0-313">Si usa el servicio IPython Notebook de Aprendizaje automático de Azure, estos paquetes ya están preinstalados.</span><span class="sxs-lookup"><span data-stu-id="390d0-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="390d0-314">Pandas</span><span class="sxs-lookup"><span data-stu-id="390d0-314">pandas</span></span>
    - <span data-ttu-id="390d0-315">numpy</span><span class="sxs-lookup"><span data-stu-id="390d0-315">numpy</span></span>
    - <span data-ttu-id="390d0-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="390d0-316">matplotlib</span></span>
    - <span data-ttu-id="390d0-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="390d0-317">pyodbc</span></span>
    - <span data-ttu-id="390d0-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="390d0-318">PyTables</span></span>

<span data-ttu-id="390d0-319">La secuencia recomendada al crear soluciones analíticas avanzadas en Aprendizaje automático de Azure con gran cantidad de datos es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="390d0-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span></span>

* <span data-ttu-id="390d0-320">Leer una pequeña muestra de los datos en una trama de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="390d0-320">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="390d0-321">Realizar algunas visualizaciones y exploraciones con los datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="390d0-321">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="390d0-322">Experimentar con el diseño de características con los datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="390d0-322">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="390d0-323">Para el diseño de características, la exploración y la manipulación de datos más grandes, usar Python para emitir consultas SQL directamente en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="390d0-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span></span>
* <span data-ttu-id="390d0-324">Decidir el tamaño de muestra que se usará para la creación del modelo de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="390d0-325">A continuación, se muestran algunas exploraciones de datos, visualizaciones de datos y ejemplos de diseño de características.</span><span class="sxs-lookup"><span data-stu-id="390d0-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="390d0-326">Se pueden encontrar más exploraciones de datos en el cuaderno de IPython Notebook de ejemplo y en el archivo de script de Python de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="390d0-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="390d0-327">Inicialización de las credenciales de la base de datos</span><span class="sxs-lookup"><span data-stu-id="390d0-327">Initialize database credentials</span></span>
<span data-ttu-id="390d0-328">Inicialice la configuración de conexión de base de datos en las variables siguientes:</span><span class="sxs-lookup"><span data-stu-id="390d0-328">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="390d0-329">Creación de conexiones de base de datos</span><span class="sxs-lookup"><span data-stu-id="390d0-329">Create database connection</span></span>
<span data-ttu-id="390d0-330">Esta es la cadena de conexión que crea la conexión a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="390d0-330">Here is the connection string that creates the connection to the database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="390d0-331">Informe con el número de filas y columnas de la tabla <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="390d0-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
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

* <span data-ttu-id="390d0-332">Número total de filas = 173179759</span><span class="sxs-lookup"><span data-stu-id="390d0-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="390d0-333">Número total de columnas = 14</span><span class="sxs-lookup"><span data-stu-id="390d0-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="390d0-334">Informe con el número de filas y columnas de la tabla <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="390d0-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
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

* <span data-ttu-id="390d0-335">Número total de filas = 173179759</span><span class="sxs-lookup"><span data-stu-id="390d0-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="390d0-336">Número total de columnas = 11</span><span class="sxs-lookup"><span data-stu-id="390d0-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-the-sql-data-warehouse-database"></a><span data-ttu-id="390d0-337">Lectura de una muestra de datos pequeña de la base de datos de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="390d0-337">Read-in a small data sample from the SQL Data Warehouse Database</span></span>
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
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="390d0-338">El tiempo empleado en leer la tabla de ejemplo es 14,096495 segundos</span><span class="sxs-lookup"><span data-stu-id="390d0-338">Time to read the sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="390d0-339">Número de filas y columnas recuperadas = (1000, 21)</span><span class="sxs-lookup"><span data-stu-id="390d0-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="390d0-340">Estadísticas descriptivas</span><span class="sxs-lookup"><span data-stu-id="390d0-340">Descriptive statistics</span></span>
<span data-ttu-id="390d0-341">Ya puede explorar los datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="390d0-341">Now you are ready to explore the sampled data.</span></span> <span data-ttu-id="390d0-342">Comenzamos echando un vistazo a algunas estadísticas descriptivas del campo **trip\_distance** (o de cualquier otro que elija).</span><span class="sxs-lookup"><span data-stu-id="390d0-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="390d0-343">Visualización: ejemplo de diagrama de caja</span><span class="sxs-lookup"><span data-stu-id="390d0-343">Visualization: Box plot example</span></span>
<span data-ttu-id="390d0-344">A continuación, observaremos el diagrama de caja de la distancia de la carrera para ver los cuantiles.</span><span class="sxs-lookup"><span data-stu-id="390d0-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagrama 1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="390d0-346">Visualización: ejemplo de diagrama de distribución</span><span class="sxs-lookup"><span data-stu-id="390d0-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="390d0-347">Diagramas que visualizan la distribución y un histograma de las distancias de las carreras muestreadas.</span><span class="sxs-lookup"><span data-stu-id="390d0-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagrama 2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="390d0-349">Visualización: diagramas de barras y líneas</span><span class="sxs-lookup"><span data-stu-id="390d0-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="390d0-350">En este ejemplo, se discretiza la distancia de la carrera en cinco discretizaciones y se visualizan los resultados de la discretización.</span><span class="sxs-lookup"><span data-stu-id="390d0-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="390d0-351">Podemos trazar la distribución de discretización anterior en un gráfico de barras o líneas con:</span><span class="sxs-lookup"><span data-stu-id="390d0-351">We can plot the above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagrama 3][3]

<span data-ttu-id="390d0-353">y</span><span class="sxs-lookup"><span data-stu-id="390d0-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagrama 4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="390d0-355">Visualización: ejemplos de gráfico de dispersión</span><span class="sxs-lookup"><span data-stu-id="390d0-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="390d0-356">Se muestra el gráfico de dispersión entre **trip\_time\_in\_secs** y **trip\_distance** para ver si existe algún tipo de correlación</span><span class="sxs-lookup"><span data-stu-id="390d0-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagrama 6][6]

<span data-ttu-id="390d0-358">También podemos comprobar la relación entre **rate\_code** y **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="390d0-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagrama 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="390d0-360">Exploración de datos en datos de muestreo mediante consultas SQL en IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="390d0-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="390d0-361">En esta sección, se explorarán las distribuciones de datos con los datos de muestreo que se conservan en la nueva tabla que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="390d0-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="390d0-362">Tenga en cuenta que se pueden realizar exploraciones similares con las tablas originales.</span><span class="sxs-lookup"><span data-stu-id="390d0-362">Note that similar explorations can be performed using the original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-the-sampled-table"></a><span data-ttu-id="390d0-363">Exploración: notificación del número de filas y columnas de la tabla de muestreo</span><span class="sxs-lookup"><span data-stu-id="390d0-363">Exploration: Report number of rows and columns in the sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="390d0-364">Exploración: distribución con propinas y sin propinas</span><span class="sxs-lookup"><span data-stu-id="390d0-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="390d0-365">Exploración: distribución de clases de propinas</span><span class="sxs-lookup"><span data-stu-id="390d0-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-the-tip-distribution-by-class"></a><span data-ttu-id="390d0-366">Exploración: trazado de la distribución de propinas por clase</span><span class="sxs-lookup"><span data-stu-id="390d0-366">Exploration: Plot the tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Diagrama 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="390d0-368">Exploración: distribución diaria de carreras</span><span class="sxs-lookup"><span data-stu-id="390d0-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="390d0-369">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="390d0-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="390d0-370">Exploración: distribución de carreras por placa y número de licencia</span><span class="sxs-lookup"><span data-stu-id="390d0-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="390d0-371">Exploración: distribución del tiempo de la carrera</span><span class="sxs-lookup"><span data-stu-id="390d0-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="390d0-372">Exploración: distribución de la distancia de la carrera</span><span class="sxs-lookup"><span data-stu-id="390d0-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="390d0-373">Exploración: distribución del tipo de pago</span><span class="sxs-lookup"><span data-stu-id="390d0-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="390d0-374">Comprobar el formulario final de la tabla con características</span><span class="sxs-lookup"><span data-stu-id="390d0-374">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="390d0-375"><a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="390d0-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="390d0-376">Ya está todo listo para pasar a la creación del modelo y la implementación del mismo en [Aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="390d0-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="390d0-377">Los datos están listos para usarse en cualquiera de los problemas de predicción identificados anteriormente, a saber:</span><span class="sxs-lookup"><span data-stu-id="390d0-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="390d0-378">**Clasificación binaria**: para predecir si se dio propina en una carrera o no.</span><span class="sxs-lookup"><span data-stu-id="390d0-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="390d0-379">**Clasificación multiclase**: para predecir el intervalo de la propina dada, según las clases definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="390d0-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="390d0-380">**Tarea de regresión**: para predecir la cantidad de propina pagada en una carrera.</span><span class="sxs-lookup"><span data-stu-id="390d0-380">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

<span data-ttu-id="390d0-381">Para iniciar el ejercicio de modelado, inicie sesión en el área de trabajo de **Aprendizaje automático de Azure** .</span><span class="sxs-lookup"><span data-stu-id="390d0-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="390d0-382">Si aún no ha creado un área de trabajo de aprendizaje automático, consulte [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="390d0-383">Para empezar a usar el Aprendizaje automático de Azure, consulte [¿Qué es Estudio de aprendizaje automático de Microsoft Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="390d0-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="390d0-384">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="390d0-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="390d0-385">La página principal del Estudio ofrece una gran cantidad de información, vídeos, tutoriales, vínculos a referencias de módulos y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="390d0-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="390d0-386">Para obtener más información sobre Aprendizaje automático de Azure, visite el [Centro de documentación de aprendizaje automático de Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="390d0-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="390d0-387">Un experimento de entrenamiento típico consta de los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="390d0-387">A typical training experiment consists of the following steps:</span></span>

1. <span data-ttu-id="390d0-388">Crear un experimento **+NUEVO** .</span><span class="sxs-lookup"><span data-stu-id="390d0-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="390d0-389">Proporcionar los datos a Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-389">Get the data into Azure ML.</span></span>
3. <span data-ttu-id="390d0-390">Preprocesar, transformar y manipular los datos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="390d0-390">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="390d0-391">Generar características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="390d0-391">Generate features as needed.</span></span>
5. <span data-ttu-id="390d0-392">Dividir los datos en conjuntos de datos de entrenamiento, validación y pruebas (o disponer de conjuntos de datos independientes para cada uno).</span><span class="sxs-lookup"><span data-stu-id="390d0-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="390d0-393">Seleccionar uno o varios algoritmos de aprendizaje automático, según el problema de aprendizaje que se quiera resolver.</span><span class="sxs-lookup"><span data-stu-id="390d0-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="390d0-394">Por ejemplo: clasificación binaria, clasificación multiclase, regresión.</span><span class="sxs-lookup"><span data-stu-id="390d0-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="390d0-395">Entrenar uno o varios modelos utilizando el conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="390d0-395">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="390d0-396">Puntuar el conjunto de datos de validación con los modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="390d0-396">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="390d0-397">Evaluar los modelos para calcular las métricas relevantes para el problema de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="390d0-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="390d0-398">Ajustar los modelos y seleccionar el mejor para su implementación.</span><span class="sxs-lookup"><span data-stu-id="390d0-398">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="390d0-399">En este ejercicio, ya se han explorado y diseñado los datos en Almacenamiento de datos SQL, y también se ha decidido el tamaño de la muestra para la ingesta en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span></span> <span data-ttu-id="390d0-400">Este es el procedimiento para crear uno o varios de los modelos de predicción:</span><span class="sxs-lookup"><span data-stu-id="390d0-400">Here is the procedure to build one or more of the prediction models:</span></span>

1. <span data-ttu-id="390d0-401">Obtenga los datos e introdúzcalos en Azure ML mediante el módulo [Importar datos][import-data], que se encuentra disponible en la sección **Entrada y salida de datos**.</span><span class="sxs-lookup"><span data-stu-id="390d0-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="390d0-402">Para obtener más información, consulte la página de referencia sobre el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="390d0-402">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Datos de importación de Aprendizaje automático de Azure][17]
2. <span data-ttu-id="390d0-404">Seleccionar **Azure SQL Database** como **Origen de datos** en el panel **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="390d0-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="390d0-405">Escribir el nombre DNS de la base de datos en el campo **Nombre del servidor de la base de datos** .</span><span class="sxs-lookup"><span data-stu-id="390d0-405">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="390d0-406">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="390d0-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="390d0-407">Escribir el **nombre de la base de datos** en el campo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="390d0-407">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="390d0-408">Escribir el *nombre de usuario de SQL* en **Nombre de la cuenta de usuario del servidor** y la *contraseña* en **Contraseña de la cuenta de usuario del servidor**.</span><span class="sxs-lookup"><span data-stu-id="390d0-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span></span>
6. <span data-ttu-id="390d0-409">Activar la opción **Aceptar cualquier certificado de servidor** .</span><span class="sxs-lookup"><span data-stu-id="390d0-409">Check the **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="390d0-410">En el área de texto editable **Consulta de base de datos** , pegar la consulta que extrae los campos de la base de datos necesarios (incluidos los campos calculados, como las etiquetas) y reducir la muestra al tamaño de muestra deseado.</span><span class="sxs-lookup"><span data-stu-id="390d0-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="390d0-411">En la ilustración siguiente se muestra un ejemplo de un experimento de clasificación binaria que lee datos directamente desde la base de datos de Almacenamiento de datos SQL (no olvide reemplazar los nombres de tabla nyctaxi_trip y nyctaxi_fare por el nombre de esquema y los nombres de tabla que utilizó en el tutorial).</span><span class="sxs-lookup"><span data-stu-id="390d0-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span></span> <span data-ttu-id="390d0-412">Se pueden construir experimentos similares para problemas de clasificación multiclase y de regresión.</span><span class="sxs-lookup"><span data-stu-id="390d0-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Entrenamiento de Aprendizaje automático de Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="390d0-414">En los ejemplos de consultas de extracción y muestreo de datos de modelado de las secciones anteriores, **las etiquetas de los tres ejercicios de modelado se incluyen en la consulta**.</span><span class="sxs-lookup"><span data-stu-id="390d0-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="390d0-415">Un paso importante (requerido) en cada uno de los ejercicios de modelado consiste en **excluir** las etiquetas innecesarias de los otros dos problemas y cualquier otra **fuga de destino**.</span><span class="sxs-lookup"><span data-stu-id="390d0-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="390d0-416">Por ejemplo, cuando use clasificación binaria, utilice la etiqueta **tipped** y excluya los campos **tip\_class**, **tip\_amount** y **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="390d0-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="390d0-417">Estos últimos son fugas de destino ya que implican que se pagó propina.</span><span class="sxs-lookup"><span data-stu-id="390d0-417">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="390d0-418">Para excluir cualquier columna innecesaria o fugas de destino, puede usar el módulo [Seleccionar columnas de conjunto de datos][select-columns] o [Editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="390d0-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="390d0-419">Para obtener más información, consulte las páginas de referencia de [Seleccionar columnas de conjunto de datos][select-columns] y [Editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="390d0-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="390d0-420"><a name="mldeploy"></a>Implementación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="390d0-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="390d0-421">Cuando el modelo esté listo, podrá implementarlo fácilmente como un servicio web directamente desde el experimento.</span><span class="sxs-lookup"><span data-stu-id="390d0-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="390d0-422">Para obtener más información sobre la implementación de servicios web de Aprendizaje automático de Azure, vea [Implementación de un servicio web de Aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="390d0-423">Para implementar un nuevo servicio web, deberá:</span><span class="sxs-lookup"><span data-stu-id="390d0-423">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="390d0-424">Crear un experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="390d0-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="390d0-425">Implemente el servicio web.</span><span class="sxs-lookup"><span data-stu-id="390d0-425">Deploy the web service.</span></span>

<span data-ttu-id="390d0-426">Para crear un experimento de puntuación a partir de un experimento de entrenamiento **Finalizado**, haga clic en **CREAR EXPERIMENTO DE PUNTUACIÓN** en la barra de acciones inferior.</span><span class="sxs-lookup"><span data-stu-id="390d0-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Puntuación de Azure][18]

<span data-ttu-id="390d0-428">Aprendizaje automático de Azure intentará crear un experimento de puntuación en función de los componentes del experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="390d0-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="390d0-429">En concreto, hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="390d0-429">In particular, it will:</span></span>

1. <span data-ttu-id="390d0-430">Guardar el modelo entrenado y quitar los módulos de entrenamiento del modelo.</span><span class="sxs-lookup"><span data-stu-id="390d0-430">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="390d0-431">Identificar un **puerto de entrada** lógico que represente el esquema de datos de entrada esperado.</span><span class="sxs-lookup"><span data-stu-id="390d0-431">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="390d0-432">Identificar un **puerto de salida** lógico que represente el esquema de salida del servicio web.</span><span class="sxs-lookup"><span data-stu-id="390d0-432">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="390d0-433">Cuando se crea el experimento de puntuación, revíselo y ajústelo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="390d0-433">When the scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="390d0-434">Un ajuste común consiste en reemplazar la consulta o el conjunto de datos de entrada por uno que excluya los campos de etiqueta, ya que estos no estarán disponibles cuando se llame al servicio.</span><span class="sxs-lookup"><span data-stu-id="390d0-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="390d0-435">También es una buena práctica reducir el tamaño de la consulta o del conjunto de datos de entrada a unos pocos registros, los necesarios para indicar el esquema de entrada.</span><span class="sxs-lookup"><span data-stu-id="390d0-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="390d0-436">En el caso del puerto de salida, es habitual excluir todos los campos de entrada e incluir solo las **etiquetas puntuadas** y las **probabilidades puntuadas** en la salida mediante el módulo [Seleccionar columnas de conjunto de datos][select-columns].</span><span class="sxs-lookup"><span data-stu-id="390d0-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="390d0-437">En la ilustración siguiente se muestra un ejemplo de experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="390d0-437">A sample scoring experiment is provided in the figure below.</span></span> <span data-ttu-id="390d0-438">Cuando todo esté listo para implementar, haga clic en el botón **PUBLICAR SERVICIO WEB** de la barra de acciones inferior.</span><span class="sxs-lookup"><span data-stu-id="390d0-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Publicación de Aprendizaje automático de Azure][11]

## <a name="summary"></a><span data-ttu-id="390d0-440">Resumen</span><span class="sxs-lookup"><span data-stu-id="390d0-440">Summary</span></span>
<span data-ttu-id="390d0-441">A modo de recapitulación, en este tutorial paso a paso se ha creado un entorno de ciencia de datos de Azure, se ha trabajado con un conjunto de datos público grande de principio a fin, llevándolo a través del proceso de ciencia de datos en equipos, desde la adquisición de los datos al entrenamiento del modelo, para finalizar con la implementación de un servicio web de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="390d0-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="390d0-442">Información de licencia</span><span class="sxs-lookup"><span data-stu-id="390d0-442">License information</span></span>
<span data-ttu-id="390d0-443">Microsoft comparte este tutorial de ejemplo y sus scripts adjuntos y Blocs de notas de IPython bajo la licencia MIT.</span><span class="sxs-lookup"><span data-stu-id="390d0-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="390d0-444">Consulte el archivo LICENSE.txt que se encuentra en el directorio del código de ejemplo en GitHub para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="390d0-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="390d0-445">Referencias</span><span class="sxs-lookup"><span data-stu-id="390d0-445">References</span></span>
<span data-ttu-id="390d0-446">•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="390d0-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="390d0-447">•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="390d0-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="390d0-448">•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="390d0-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
