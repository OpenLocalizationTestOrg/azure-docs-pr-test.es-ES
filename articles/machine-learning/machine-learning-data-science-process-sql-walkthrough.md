---
title: "Creación e implementación de un modelo de aprendizaje automático mediante SQL Server en una VM de Azure | Microsoft Docs"
description: "Tecnología y procesos de análisis avanzado en acción"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 6c5361c7e47209c8eb4d5630b44b3dcfeedeaf01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="3abb5-103">Proceso de ciencia de datos en equipos en acción: uso de SQL Server</span><span class="sxs-lookup"><span data-stu-id="3abb5-103">The Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="3abb5-104">En este tutorial, se describe el proceso de creación e implementación de un modelo de Machine Learning con SQL Server y un conjunto de datos disponible públicamente: [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) .</span><span class="sxs-lookup"><span data-stu-id="3abb5-104">In this tutorial, you walk through the process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="3abb5-105">El procedimiento sigue un flujo de trabajo de ciencia de datos estándar: introducir y explorar los datos, diseñar características para facilitar el aprendizaje y, después, crear e implementar un modelo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-105">The procedure follows a standard data science workflow: ingest and explore the data, engineer features to facilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="3abb5-106"><a name="dataset"></a>Descripción del conjunto de datos NYC Taxi Trip</span><span class="sxs-lookup"><span data-stu-id="3abb5-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="3abb5-107">El conjunto de datos NYC Taxi Trips consiste en aproximadamente 20 GB de archivos de valores separados por comas (CSV) comprimidos (aproximadamente, 48 GB sin comprimir), que incluyen más de 173 millones de carreras individuales y las tarifas pagadas por cada carrera.</span><span class="sxs-lookup"><span data-stu-id="3abb5-107">The NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="3abb5-108">Cada registro de carrera incluye la hora y la ubicación de recogida y de entrega, el número de licencia de (del conductor) anónimo y el número de ida y vuelta incluye la ubicación de entrega y recogida y el tiempo, la número de licencia y el número de identificador único del taxi.</span><span class="sxs-lookup"><span data-stu-id="3abb5-108">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="3abb5-109">Los datos cubren todos los viajes del año 2013 y se proporcionan en los dos conjuntos de datos siguientes para cada mes:</span><span class="sxs-lookup"><span data-stu-id="3abb5-109">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="3abb5-110">El archivo CSV 'trip_data' contiene información detallada de las carreras, como el número de pasajeros, los puntos de recogida y destino, la duración de las carreras y la longitud del recorrido.</span><span class="sxs-lookup"><span data-stu-id="3abb5-110">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="3abb5-111">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3abb5-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="3abb5-112">El archivo CSV 'trip_fare' contiene información detallada de la tarifa que se paga en cada carrera, como el tipo de pago, el importe de la tarifa, los suplementos e impuestos, las propinas y peajes, y el importe total pagado.</span><span class="sxs-lookup"><span data-stu-id="3abb5-112">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="3abb5-113">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3abb5-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="3abb5-114">La clave única para unir trip\_data and trip\_fare se compone de los campos: medallion, hack\_licence and pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="3abb5-114">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="3abb5-115"><a name="mltasks"></a>Ejemplos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="3abb5-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="3abb5-116">Se formularán tres problemas de predicción basados en *tip\_amount*, a saber:</span><span class="sxs-lookup"><span data-stu-id="3abb5-116">We will formulate three prediction problems based on the *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="3abb5-117">Clasificación binaria: permite predecir si se pagó una propina tras una carrera, o no; es decir, un valor de *tip\_amount* mayor que 0 $ es un ejemplo positivo, mientras que un valor de *tip\_amount* de 0 $ es un ejemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="3abb5-118">Clasificación con múltiples clases: para predecir el intervalo de la propina de la carrera.</span><span class="sxs-lookup"><span data-stu-id="3abb5-118">Multiclass classification: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="3abb5-119">Dividimos *tip\_amount* en cinco ubicaciones o clases:</span><span class="sxs-lookup"><span data-stu-id="3abb5-119">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="3abb5-120">Tarea de regresión: para predecir la cantidad de propina pagada en una carrera.</span><span class="sxs-lookup"><span data-stu-id="3abb5-120">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="3abb5-121"><a name="setup"></a>Configuración del entorno de ciencia de datos de Azure para análisis avanzado</span><span class="sxs-lookup"><span data-stu-id="3abb5-121"><a name="setup"></a>Setting Up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="3abb5-122">Como puede ver en la guía [Planear su entorno de ciencia de datos de aprendizaje automático de Azure](machine-learning-data-science-plan-your-environment.md) , existen varias opciones para trabajar con el conjunto de datos NYC Taxi Trips en Azure:</span><span class="sxs-lookup"><span data-stu-id="3abb5-122">As you can see from the [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options to work with the NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="3abb5-123">Trabajar con los datos en blobs de Azure y, a continuación, modelar en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3abb5-123">Work with the data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="3abb5-124">Cargar los datos en una base de datos de SQL Server y, a continuación, modelar en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3abb5-124">Load the data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="3abb5-125">En este tutorial se mostrará la importación paralela en bloque de los datos en SQL Server, la exploración de los datos, el diseño de características y la reducción de la muestra con SQL Server Management Studio, así como con un Bloc de notas de IPython.</span><span class="sxs-lookup"><span data-stu-id="3abb5-125">In this tutorial we will demonstrate parallel bulk import of the data to a SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="3abb5-126">Los [scripts de ejemplo](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) y [blocs de notas de IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) se comparten en GitHub.</span><span class="sxs-lookup"><span data-stu-id="3abb5-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="3abb5-127">Hay un Bloc de notas de IPython de ejemplo disponible para trabajar con los datos de blobs de Azure en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="3abb5-127">A sample IPython notebook to work with the data in Azure blobs is also available in the same location.</span></span>

<span data-ttu-id="3abb5-128">Para configurar el entorno de ciencia de datos de Azure:</span><span class="sxs-lookup"><span data-stu-id="3abb5-128">To set up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="3abb5-129">Cree una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3abb5-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="3abb5-130">Creación de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3abb5-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="3abb5-131">[Aprovisione una máquina virtual de ciencia de datos](machine-learning-data-science-setup-sql-server-virtual-machine.md), que proporcionará un servidor de SQL Server y un servidor de Notebook de IPython.</span><span class="sxs-lookup"><span data-stu-id="3abb5-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3abb5-132">Los scripts y Blocs de notas de IPython de ejemplo se descargarán en la máquina virtual de ciencia de datos durante el proceso de instalación.</span><span class="sxs-lookup"><span data-stu-id="3abb5-132">The sample scripts and IPython notebooks will be downloaded to your Data Science virtual machine during the setup process.</span></span> <span data-ttu-id="3abb5-133">Cuando se complete el script posterior a la instalación de máquina virtual, los ejemplos estarán en la biblioteca de documentos de su máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="3abb5-133">When the VM post-installation script completes, the samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="3abb5-134">Scripts de ejemplo: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="3abb5-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="3abb5-135">Blocs de notas de IPython de ejemplo: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="3abb5-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="3abb5-136">where `<user_name>` es el nombre de inicio de sesión de Windows de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3abb5-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="3abb5-137">Se hará referencia a las carpetas de ejemplo como **Scripts de ejemplo** y **Blocs de notas de IPython de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-137">We will refer to the sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="3abb5-138">Teniendo en cuenta el tamaño del conjunto de datos, la ubicación del origen de datos y el entorno de destino de Azure seleccionado, este escenario es similar a [Escenario \#5: Conjunto de datos grande de archivos locales, con SQL Server en una máquina virtual de Azure como destino](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="3abb5-138">Based on the dataset size, data source location, and the selected Azure target environment, this scenario is similar to [Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="3abb5-139"><a name="getdata"></a>Obtener los datos del origen público</span><span class="sxs-lookup"><span data-stu-id="3abb5-139"><a name="getdata"></a>Get the Data from Public Source</span></span>
<span data-ttu-id="3abb5-140">Para obtener el conjunto de datos [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) de su ubicación pública, puede usar cualquiera de los métodos descritos en [Mover datos hacia y desde Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) para copiar los datos en su nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3abb5-140">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your new virtual machine.</span></span>

<span data-ttu-id="3abb5-141">Para copiar los datos mediante AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3abb5-141">To copy the data using AzCopy:</span></span>

1. <span data-ttu-id="3abb5-142">Inicie sesión en la máquina virtual (VM)</span><span class="sxs-lookup"><span data-stu-id="3abb5-142">Log in to your virtual machine (VM)</span></span>
2. <span data-ttu-id="3abb5-143">Cree un nuevo directorio en disco de datos de la máquina virtual (Nota: no use el disco temporal que se incluye con la máquina virtual como disco de datos).</span><span class="sxs-lookup"><span data-stu-id="3abb5-143">Create a new directory in the VM's data disk (Note: Do not use the Temporary Disk which comes with the VM as a Data Disk).</span></span>
3. <span data-ttu-id="3abb5-144">En una ventana de símbolo del sistema, ejecute la siguiente línea de comandos de Azcopy, reemplazando <ruta_a_carpeta_datos> por la carpeta de datos que se creó en (2):</span><span class="sxs-lookup"><span data-stu-id="3abb5-144">In a Command Prompt window, run the following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="3abb5-145">Cuando se complete la operación AzCopy, debe haber un total de 24 archivos CSV comprimidos (12 para trip\_data y 12 para trip\_fare) en la carpeta de datos.</span><span class="sxs-lookup"><span data-stu-id="3abb5-145">When the AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in the data folder.</span></span>
4. <span data-ttu-id="3abb5-146">Descomprima los archivos descargados.</span><span class="sxs-lookup"><span data-stu-id="3abb5-146">Unzip the downloaded files.</span></span> <span data-ttu-id="3abb5-147">Observe la carpeta donde se encuentran los archivos sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="3abb5-147">Note the folder where the uncompressed files reside.</span></span> <span data-ttu-id="3abb5-148">Se hará referencia a esta carpeta como <path\_to\_data\_files\>.</span><span class="sxs-lookup"><span data-stu-id="3abb5-148">This folder will be referred to as the <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="3abb5-149"><a name="dbload"></a>Importación masiva de datos en una base de datos de SQL Server</span><span class="sxs-lookup"><span data-stu-id="3abb5-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="3abb5-150">Para mejorar tanto el rendimiento de la carga y transferencia de grandes cantidades de datos a una base de datos SQL como las consultas posteriores, utilice *tablas y vistas con particiones*.</span><span class="sxs-lookup"><span data-stu-id="3abb5-150">The performance of loading/transferring large amounts of data to an SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="3abb5-151">En esta sección, se seguirán las instrucciones que se describen en [Importación paralela de conjuntos masivos de datos mediante tablas de partición de SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) para crear una nueva base de datos y cargar los datos en tablas con particiones en paralelo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-151">In this section, we will follow the instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) to create a new database and load the data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="3abb5-152">Con la sesión iniciada en la máquina virtual, inicie **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-152">While logged in to your VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="3abb5-153">Conéctese con la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="3abb5-153">Connect using Windows Authentication.</span></span>
   
    ![Conexión SSMS][12]
3. <span data-ttu-id="3abb5-155">Si aún no ha cambiado el modo de autenticación de SQL Server ni ha creado un nuevo usuario de inicio de sesión de SQL, abra el archivo de script **change\_auth.sql** de la carpeta **Scripts de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-155">If you have not yet changed the SQL Server authentication mode and created a new SQL login user, open the script file named **change\_auth.sql** in the **Sample Scripts** folder.</span></span> <span data-ttu-id="3abb5-156">Cambie el nombre de usuario y la contraseña predeterminados.</span><span class="sxs-lookup"><span data-stu-id="3abb5-156">Change the  default user name and password.</span></span> <span data-ttu-id="3abb5-157">Haga clic en **!Ejecutar** en la barra de herramientas para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="3abb5-157">Click **!Execute** in the toolbar to run the script.</span></span>
   
    ![Ejecutar script][13]
4. <span data-ttu-id="3abb5-159">Compruebe o cambie las carpetas de registro y las bases de datos de SQL Server predeterminadas para asegurarse de que las bases de datos recién creadas se almacenarán en un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="3abb5-159">Verify and/or change the SQL Server default database and log folders to ensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="3abb5-160">La imagen de la máquina virtual de SQL Server que está optimizada para cargas de almacén de datos está configurada previamente con discos de registros y datos.</span><span class="sxs-lookup"><span data-stu-id="3abb5-160">The SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="3abb5-161">Si la máquina virtual no incluía un disco de datos y agregó nuevos discos duros virtuales durante el proceso de instalación de la máquina virtual, cambie las carpetas predeterminadas de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="3abb5-161">If your VM did not include a Data Disk and you added new virtual hard disks during the VM setup process, change the default folders as follows:</span></span>
   
   * <span data-ttu-id="3abb5-162">Haga clic con el botón derecho en el nombre del servidor SQL Server en el panel izquierdo y haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-162">Right-click the SQL Server name in the left panel and click **Properties**.</span></span>
     
       ![Propiedades de SQL Server][14]
   * <span data-ttu-id="3abb5-164">Seleccione **Configuración de base de datos** en la lista **Seleccionar una página** de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="3abb5-164">Select **Database Settings** from the **Select a page** list to the left.</span></span>
   * <span data-ttu-id="3abb5-165">Compruebe o cambie los datos del apartado **Ubicaciones predeterminadas de la base de datos** por las ubicaciones del **Disco de datos** que prefiera.</span><span class="sxs-lookup"><span data-stu-id="3abb5-165">Verify and/or change the **Database default locations** to the **Data Disk** locations of your choice.</span></span> <span data-ttu-id="3abb5-166">Aquí es donde se almacenarán las nuevas bases de datos si se crean con la configuración de ubicación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3abb5-166">This is where new databases reside if created with the default location settings.</span></span>
     
       ![Valores predeterminados de Base de datos SQL][15]  
5. <span data-ttu-id="3abb5-168">Para crear una nueva base de datos y un conjunto de grupos de archivos para almacenar las tablas con particiones, abra el script de ejemplo **create\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-168">To create a new database and a set of filegroups to hold the partitioned tables, open the sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="3abb5-169">El script creará una nueva base de datos llamada **TaxiNYC** y doce grupos de archivos en la ubicación de datos predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3abb5-169">The script will create a new database named **TaxiNYC** and 12 filegroups in the default data location.</span></span> <span data-ttu-id="3abb5-170">Cada uno de los grupos de archivos contendrá un mes de datos de trip\_data y trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="3abb5-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="3abb5-171">Modifique el nombre de la base de datos, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="3abb5-171">Modify the database name, if desired.</span></span> <span data-ttu-id="3abb5-172">Haga clic en **!Ejecutar** para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="3abb5-172">Click **!Execute** to run the script.</span></span>
6. <span data-ttu-id="3abb5-173">A continuación, cree dos tablas de particiones, una para trip\_data y otra para trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="3abb5-173">Next, create two partition tables, one for the trip\_data and another for the trip\_fare.</span></span> <span data-ttu-id="3abb5-174">Abra el script de ejemplo **create\_partitioned\_table.sql**, que:</span><span class="sxs-lookup"><span data-stu-id="3abb5-174">Open the sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="3abb5-175">Creará una función de partición para dividir los datos por mes.</span><span class="sxs-lookup"><span data-stu-id="3abb5-175">Create a partition function to split the data by month.</span></span>
   * <span data-ttu-id="3abb5-176">Creará un esquema de partición para asignar los datos de cada mes a un grupo de archivos distinto.</span><span class="sxs-lookup"><span data-stu-id="3abb5-176">Create a partition scheme to map each month's data to a different filegroup.</span></span>
   * <span data-ttu-id="3abb5-177">Creará dos tablas con particiones asignadas al esquema de partición: **nyctaxi\_trip** contendrá los datos de trip\_data y **nyctaxi\_fare** los de trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="3abb5-177">Create two partitioned tables mapped to the partition scheme: **nyctaxi\_trip** will hold the trip\_data and **nyctaxi\_fare** will hold the trip\_fare data.</span></span>
     
     <span data-ttu-id="3abb5-178">Haga clic en **!Ejecutar** para ejecutar el script y crear las tablas con particiones.</span><span class="sxs-lookup"><span data-stu-id="3abb5-178">Click **!Execute** to run the script and create the partitioned tables.</span></span>
7. <span data-ttu-id="3abb5-179">En la carpeta **Scripts de ejemplo** , hay dos scripts de PowerShell de ejemplo para mostrar las importaciones en bloque paralelas de datos en tablas de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3abb5-179">In the **Sample Scripts** folder, there are two sample PowerShell scripts provided to demonstrate parallel bulk imports of data to SQL Server tables.</span></span>
   
   * <span data-ttu-id="3abb5-180">**bcp\_parallel\_generic.ps1** es un script genérico para importar datos en bloque y de forma paralela en una tabla.</span><span class="sxs-lookup"><span data-stu-id="3abb5-180">**bcp\_parallel\_generic.ps1** is a generic script to parallel bulk import data into a table.</span></span> <span data-ttu-id="3abb5-181">Modifique este script para establecer las variables de entrada y de destino, como se indica en las líneas de comentario del script.</span><span class="sxs-lookup"><span data-stu-id="3abb5-181">Modify this script to set the input and target variables as indicated in the comment lines in the script.</span></span>
   * <span data-ttu-id="3abb5-182">**bcp\_parallel\_nyctaxi.ps1** es una versión preconfigurada del script genérico y se puede usar para cargar ambas tablas para los datos de NYC Taxi Trips.</span><span class="sxs-lookup"><span data-stu-id="3abb5-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of the generic script and can be used to to load both tables for the NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="3abb5-183">Haga clic con el botón derecho en el nombre de script **bcp\_parallel\_nyctaxi.ps1** y haga clic en **Editar** para abrirlo en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3abb5-183">Right-click the **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** to open it in PowerShell.</span></span> <span data-ttu-id="3abb5-184">Revise las variables preestablecidas y modifíquelas según el nombre de la base de datos seleccionada, la carpeta de datos de entrada, la carpeta de registro de destino y las rutas de acceso a los archivos de formato de ejemplo **nyctaxi_trip.xml** y **nyctaxi\_fare.xml** (que se incluyen en la carpeta **Scripts de ejemplo**).</span><span class="sxs-lookup"><span data-stu-id="3abb5-184">Review the preset variables and modify according to your selected database name, input data folder, target log folder, and paths to the  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in the **Sample Scripts** folder).</span></span>
   
    ![Datos de importación en bloque][16]
   
    <span data-ttu-id="3abb5-186">También puede seleccionar el modo de autenticación, cuyo valor predeterminado es Autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="3abb5-186">You may also select the authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="3abb5-187">Haga clic en la flecha verde de la barra de herramientas para iniciar la ejecución.</span><span class="sxs-lookup"><span data-stu-id="3abb5-187">Click the green arrow in the toolbar to run.</span></span> <span data-ttu-id="3abb5-188">El script ejecutará 24 operaciones de importación masiva en paralelo, 12 para cada tabla con particiones.</span><span class="sxs-lookup"><span data-stu-id="3abb5-188">The script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="3abb5-189">Puede supervisar el progreso de la importación de datos si abre la carpeta de datos predeterminada de SQL Server como el conjunto anterior.</span><span class="sxs-lookup"><span data-stu-id="3abb5-189">You may monitor the data import progress by opening the SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="3abb5-190">El script de PowerShell informa de las horas de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="3abb5-190">The PowerShell script reports the starting and ending times.</span></span> <span data-ttu-id="3abb5-191">Cuando se completan todas las importaciones masivas, se notifica la hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="3abb5-191">When all bulk imports complete, the ending time is reported.</span></span> <span data-ttu-id="3abb5-192">Revise la carpeta de registro de destino para comprobar que las importaciones masivas se realizaron correctamente, es decir, que no se informó de errores en la carpeta de registro de destino.</span><span class="sxs-lookup"><span data-stu-id="3abb5-192">Check the target log folder to verify that the bulk imports were successful, i.e., no errors reported in the target log folder.</span></span>
10. <span data-ttu-id="3abb5-193">La base de datos ya está preparada para la exploración, diseño de características y otras operaciones que desee.</span><span class="sxs-lookup"><span data-stu-id="3abb5-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="3abb5-194">Dado que las particiones de las tablas se crean según el campo **pickup\_datetime**, las consultas que incluyan condiciones **pickup\_datetime** en la cláusula **WHERE** se beneficiarán del esquema de partición.</span><span class="sxs-lookup"><span data-stu-id="3abb5-194">Since the tables are partitioned according to the **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in the **WHERE** clause will benefit from the partition scheme.</span></span>
11. <span data-ttu-id="3abb5-195">En **SQL Server Management Studio**, explore el script de ejemplo proporcionado, **sample\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-195">In **SQL Server Management Studio**, explore the provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="3abb5-196">Para ejecutar cualquiera de las consultas de ejemplo, resalte las líneas de la consulta y haga clic en **!Ejecutar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="3abb5-196">To run any of the sample queries, highlight the query lines then click **!Execute** in the toolbar.</span></span>
12. <span data-ttu-id="3abb5-197">Los datos de NYC Taxi Trips se cargan en dos tablas distintas.</span><span class="sxs-lookup"><span data-stu-id="3abb5-197">The NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="3abb5-198">Para mejorar las operaciones de combinación, se recomienda la indexación de las tablas.</span><span class="sxs-lookup"><span data-stu-id="3abb5-198">To improve join operations, it is highly recommended to index the tables.</span></span> <span data-ttu-id="3abb5-199">El script de ejemplo **create\_partitioned\_index.sql** crea índices con particiones en la clave de combinación compuesta **medallion, hack\_license y pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-199">The sample script **create\_partitioned\_index.sql** creates partitioned indexes on the composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="3abb5-200"><a name="dbexplore"></a>Exploración de datos e ingeniería de características en SQL Server</span><span class="sxs-lookup"><span data-stu-id="3abb5-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="3abb5-201">En esta sección, se llevará a cabo la exploración de datos y la generación de características mediante la ejecución de consultas SQL directamente en **SQL Server Management Studio** con la base de datos de SQL Server creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3abb5-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in the **SQL Server Management Studio** using the SQL Server database created earlier.</span></span> <span data-ttu-id="3abb5-202">Se proporciona un script de ejemplo llamado **sample\_queries.sql** en la carpeta **Scripts de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-202">A sample script named **sample\_queries.sql** is provided in the **Sample Scripts** folder.</span></span> <span data-ttu-id="3abb5-203">Modifique el script para cambiar el nombre de la base de datos, en caso de que no sea el predeterminado: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-203">Modify the script to change the database name, if it is different from the default: **TaxiNYC**.</span></span>

<span data-ttu-id="3abb5-204">En este ejercicio, se hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3abb5-204">In this exercise, we will:</span></span>

* <span data-ttu-id="3abb5-205">Conectarse a **SQL Server Management Studio** mediante Autenticación de Windows o con Autenticación de SQL y el nombre de inicio de sesión y la contraseña de SQL.</span><span class="sxs-lookup"><span data-stu-id="3abb5-205">Connect to **SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and the SQL login name and password.</span></span>
* <span data-ttu-id="3abb5-206">Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="3abb5-207">Investigar la calidad de los datos de los campos de longitud y latitud.</span><span class="sxs-lookup"><span data-stu-id="3abb5-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="3abb5-208">Generar etiquetas de clasificación binaria y multiclase según **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="3abb5-209">Generar características y calcular o comparar distancias de carreras.</span><span class="sxs-lookup"><span data-stu-id="3abb5-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="3abb5-210">Combinar las dos tablas y extraer una muestra aleatoria que se usará para generar modelos.</span><span class="sxs-lookup"><span data-stu-id="3abb5-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

<span data-ttu-id="3abb5-211">Cuando esté listo para continuar con Aprendizaje automático de Azure, puede:</span><span class="sxs-lookup"><span data-stu-id="3abb5-211">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="3abb5-212">Guardar la consulta SQL final para extraer y muestrear los datos, y copiar y pegar la consulta directamente en un módulo [Importar datos][import-data] de Azure Machine Learning; o bien</span><span class="sxs-lookup"><span data-stu-id="3abb5-212">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="3abb5-213">Conservar los datos muestreados y de ingeniería que planea usar para la generación de modelos en una nueva tabla de bases de datos y usar la nueva tabla en el módulo [Importar datos][import-data] de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3abb5-213">Persist the sampled and engineered data you plan to use for model building in a new database table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="3abb5-214">En esta sección se guardará la consulta final para extraer y muestrear los datos.</span><span class="sxs-lookup"><span data-stu-id="3abb5-214">In this section we will save the final query to extract and sample the data.</span></span> <span data-ttu-id="3abb5-215">El segundo método se muestra en la sección [Exploración de datos e ingeniería de características en el Bloc de notas de IPython](#ipnb) .</span><span class="sxs-lookup"><span data-stu-id="3abb5-215">The second method is demonstrated in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="3abb5-216">Para una comprobación rápida del número de filas y columnas en las tablas que se rellenaron anteriormente mediante la importación masiva paralela,</span><span class="sxs-lookup"><span data-stu-id="3abb5-216">For a quick verification of the number of rows and columns in the tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="3abb5-217">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="3abb5-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="3abb5-218">Este ejemplo identifica las licencias (números de taxi) con más de 100 carreras dentro de un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-218">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="3abb5-219">La consulta se beneficiaría del acceso de la tabla con particiones, ya que está condicionada por el esquema de partición de **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-219">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="3abb5-220">La consulta el conjunto de datos completo también hará uso de la tabla con particiones o del recorrido de índice.</span><span class="sxs-lookup"><span data-stu-id="3abb5-220">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="3abb5-221">Exploración: distribución de carreras por medallion y hack_license</span><span class="sxs-lookup"><span data-stu-id="3abb5-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="3abb5-222">Evaluación de la calidad de los datos: comprobar los registros con longitud o latitud incorrectas</span><span class="sxs-lookup"><span data-stu-id="3abb5-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="3abb5-223">En este ejemplo se investiga si alguno de los campos de longitud y latitud contiene un valor no válido (los grados radianes deben encontrarse entre -90 y 90) o tienen coordenadas (0, 0).</span><span class="sxs-lookup"><span data-stu-id="3abb5-223">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="3abb5-224">Exploración: distribución de carreras con propinas frente a sin propinas</span><span class="sxs-lookup"><span data-stu-id="3abb5-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="3abb5-225">En este ejemplo se busca el número de carreras en las que se han dado propinas frente a aquellas en las que no se han dado, en un período de tiempo determinado (o en el conjunto de datos completo si se abarca todo el año).</span><span class="sxs-lookup"><span data-stu-id="3abb5-225">This example finds the number of trips that were tipped vs. not tipped in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="3abb5-226">Esta distribución refleja la distribución de etiquetas binarias que se usará más adelante para el modelado de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="3abb5-226">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="3abb5-227">Exploración: distribución por intervalos y clases de propinas</span><span class="sxs-lookup"><span data-stu-id="3abb5-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="3abb5-228">Este ejemplo calcula la distribución de los intervalos de propinas de un período de tiempo determinado (o en el conjunto de datos completo si abarca todo el año).</span><span class="sxs-lookup"><span data-stu-id="3abb5-228">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="3abb5-229">Esta es la distribución de las clases de etiquetas que se usarán posteriormente para el modelado de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="3abb5-229">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="3abb5-230">Exploración: calcular y comparar la distancia de la carrera</span><span class="sxs-lookup"><span data-stu-id="3abb5-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="3abb5-231">En este ejemplo se convierte la longitud y latitud de los puntos de recogida y destino a puntos geográficos de SQL, se calcula la distancia de la carrera mediante la diferencia de puntos geográficos de SQL y se devuelve una muestra aleatoria de los resultados de la comparación.</span><span class="sxs-lookup"><span data-stu-id="3abb5-231">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="3abb5-232">En el ejemplo se limitan los resultados a coordenadas válidas usando solo la consulta de evaluación de calidad de datos tratada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3abb5-232">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="3abb5-233">Diseño de características en consultas SQL</span><span class="sxs-lookup"><span data-stu-id="3abb5-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="3abb5-234">Las consultas de exploración de conversión geográfica y la generación de etiquetas pueden usarse también para generar etiquetas y características mediante la eliminación de la parte de recuento.</span><span class="sxs-lookup"><span data-stu-id="3abb5-234">The label generation and geography conversion exploration queries can also be used to generate labels/features by removing the counting part.</span></span> <span data-ttu-id="3abb5-235">En la sección [Exploración de datos e ingeniería de características en el Bloc de notas de IPython](#ipnb) se ofrecen ejemplos SQL de ingeniería de características adicionales.</span><span class="sxs-lookup"><span data-stu-id="3abb5-235">Additional feature engineering SQL examples are provided in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="3abb5-236">Resulta más eficaz ejecutar consultas de generación de características sobre el conjunto de datos completo o un subconjunto grande mediante consultas SQL que se ejecuten directamente en la instancia de base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3abb5-236">It is more efficient to run the feature generation queries on the full dataset or a large subset of it using SQL queries which run directly on the SQL Server database instance.</span></span> <span data-ttu-id="3abb5-237">Las consultas se pueden ejecutar en **SQL Server Management Studio**, el Bloc de notas de IPython o cualquier herramienta o entorno de desarrollo que tenga acceso local o remoto a la base de datos local.</span><span class="sxs-lookup"><span data-stu-id="3abb5-237">The queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access the database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="3abb5-238">Preparación de los datos para la creación del modelo</span><span class="sxs-lookup"><span data-stu-id="3abb5-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="3abb5-239">La siguiente consulta combina las tablas **nyctaxi\_trip** y **nyctaxi\_fare**, genera una etiqueta de clasificación binaria **tipped**, una etiqueta de clasificación multiclase **tip\_class** y extrae una muestra aleatoria de un 1 % del conjunto de datos combinado completo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-239">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from the full joined dataset.</span></span> <span data-ttu-id="3abb5-240">Esta consulta se puede copiar y pegar directamente en el módulo [Importar datos](https://studio.azureml.net) de [Azure Machine Learning Studio][import-data] para la ingesta directa de datos de la instancia de base de datos SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="3abb5-240">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL Server database instance in Azure.</span></span> <span data-ttu-id="3abb5-241">La consulta excluye los registros con coordenadas (0, 0) incorrectas.</span><span class="sxs-lookup"><span data-stu-id="3abb5-241">The query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="3abb5-242"><a name="ipnb"></a>Exploración de datos e ingeniería de características en el Bloc de notas de IPython</span><span class="sxs-lookup"><span data-stu-id="3abb5-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="3abb5-243">En esta sección, se llevará a cabo la exploración de datos y la generación de características con consultas Pyhton y SQL en la base de datos de SQL Server creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3abb5-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL Server database created earlier.</span></span> <span data-ttu-id="3abb5-244">Se proporciona un bloc de notas de IPython de ejemplo llamado **machine-Learning-data-science-process-sql-story.ipynb** en la carpeta **Blocs de notas de IPython de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in the **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="3abb5-245">Este bloc de notas también está disponible en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="3abb5-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="3abb5-246">La secuencia recomendada al trabajar con big data es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3abb5-246">The recommended sequence when working with big data is the following:</span></span>

* <span data-ttu-id="3abb5-247">Leer una pequeña muestra de los datos en una trama de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="3abb5-247">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="3abb5-248">Realizar algunas visualizaciones y exploraciones con los datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-248">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="3abb5-249">Experimentar con el diseño de características con los datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-249">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="3abb5-250">Para el diseño de características, la exploración y la manipulación de datos más grandes, usar Python para emitir consultas SQL directamente sobre la base de datos de SQL Server en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="3abb5-250">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL Server database in the Azure VM.</span></span>
* <span data-ttu-id="3abb5-251">Decidir el tamaño de muestra que se usará para la creación del modelo de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3abb5-251">Decide the sample size to use for Azure Machine Learning model building.</span></span>

<span data-ttu-id="3abb5-252">Cuando esté listo para continuar con Aprendizaje automático de Azure, puede:</span><span class="sxs-lookup"><span data-stu-id="3abb5-252">When ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="3abb5-253">Guardar la consulta SQL final para extraer y muestrear los datos, y copiar y pegar la consulta directamente en un módulo [Importar datos][import-data] de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3abb5-253">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="3abb5-254">Este método se muestra en la sección [Generación de modelos en Aprendizaje automático de Azure](#mlmodel) .</span><span class="sxs-lookup"><span data-stu-id="3abb5-254">This method is demonstrated in the [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="3abb5-255">Conservar los datos muestreados y de ingeniería que planea usar para la generación de modelos en una nueva tabla de base de datos y usar la nueva tabla en el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="3abb5-255">Persist the sampled and engineered data you plan to use for model building in a new database table, then use the new table in the [Import Data][import-data] module.</span></span>

<span data-ttu-id="3abb5-256">A continuación, se muestran algunas exploraciones de datos, visualizaciones de datos y ejemplos de diseño de características.</span><span class="sxs-lookup"><span data-stu-id="3abb5-256">The following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="3abb5-257">Para obtener más ejemplos, vea el Bloc de notas de IPython de SQL de ejemplo en la carpeta **Blocs de notas de IPython** de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-257">For more examples, see the sample SQL IPython notebook in the **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="3abb5-258">Inicializar las credenciales de la base de datos</span><span class="sxs-lookup"><span data-stu-id="3abb5-258">Initialize Database Credentials</span></span>
<span data-ttu-id="3abb5-259">Inicialice la configuración de conexión de base de datos en las variables siguientes:</span><span class="sxs-lookup"><span data-stu-id="3abb5-259">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="3abb5-260">Crear conexiones de base de datos</span><span class="sxs-lookup"><span data-stu-id="3abb5-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="3abb5-261">Informe con el número de filas y columnas en la tabla nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="3abb5-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="3abb5-262">Número total de filas = 173179759</span><span class="sxs-lookup"><span data-stu-id="3abb5-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="3abb5-263">Número total de columnas = 14</span><span class="sxs-lookup"><span data-stu-id="3abb5-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-the-sql-server-database"></a><span data-ttu-id="3abb5-264">Lectura de una muestra de datos pequeña de la base de datos de SQL Server</span><span class="sxs-lookup"><span data-stu-id="3abb5-264">Read-in a small data sample from the SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="3abb5-265">El tiempo empleado en leer la tabla de ejemplo es 6,492000 segundos</span><span class="sxs-lookup"><span data-stu-id="3abb5-265">Time to read the sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="3abb5-266">Número de filas y columnas recuperadas = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="3abb5-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="3abb5-267">Estadísticas descriptivas</span><span class="sxs-lookup"><span data-stu-id="3abb5-267">Descriptive Statistics</span></span>
<span data-ttu-id="3abb5-268">Ya se pueden explorar los datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-268">Now are ready to explore the sampled data.</span></span> <span data-ttu-id="3abb5-269">Comenzamos echando un vistazo a las estadísticas descriptivas del campo **trip\_distance** (o cualquier otro):</span><span class="sxs-lookup"><span data-stu-id="3abb5-269">We start with looking at descriptive statistics for the **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="3abb5-270">Visualización: ejemplo de diagrama de caja</span><span class="sxs-lookup"><span data-stu-id="3abb5-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="3abb5-271">A continuación, observaremos el diagrama de caja de la distancia de la carrera para ver los cuantiles</span><span class="sxs-lookup"><span data-stu-id="3abb5-271">Next we look at the box plot for the trip distance to visualize the quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagrama 1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="3abb5-273">Visualización: ejemplo de diagrama de distribución</span><span class="sxs-lookup"><span data-stu-id="3abb5-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagrama 2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="3abb5-275">Visualización: diagramas de barras y líneas</span><span class="sxs-lookup"><span data-stu-id="3abb5-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="3abb5-276">En este ejemplo, se discretiza la distancia de la carrera en cinco discretizaciones y se visualizan los resultados de la discretización.</span><span class="sxs-lookup"><span data-stu-id="3abb5-276">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="3abb5-277">Podemos trazar la distribución de discretización anterior en un gráfico de barras o líneas, como se indica a continuación</span><span class="sxs-lookup"><span data-stu-id="3abb5-277">We can plot the above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagrama 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagrama 4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="3abb5-280">Visualización: ejemplo de gráfico de dispersión</span><span class="sxs-lookup"><span data-stu-id="3abb5-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="3abb5-281">Se muestra el gráfico de dispersión entre **trip\_time\_in\_secs** y **trip\_distance** para ver si existe algún tipo de correlación</span><span class="sxs-lookup"><span data-stu-id="3abb5-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagrama 6][6]

<span data-ttu-id="3abb5-283">También podemos comprobar la relación entre **rate\_code** y **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-283">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagrama 8][8]

### <a name="sub-sampling-the-data-in-sql"></a><span data-ttu-id="3abb5-285">Submuestreo de los datos en SQL</span><span class="sxs-lookup"><span data-stu-id="3abb5-285">Sub-Sampling the Data in SQL</span></span>
<span data-ttu-id="3abb5-286">Al preparar los datos para la creación del modelo en [Azure Machine Learning Studio](https://studio.azureml.net), puede decidir **usar consultas SQL directamente en el módulo Importar datos** o conservar los datos de ingeniería y de muestreo en una tabla nueva, que puede utilizar en el módulo [Importar datos][import-data] con una única instrucción **SELECT * FROM <nuevo\_nombre\_de\_tabla>**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on the **SQL query to use directly in the Import Data module** or persist the engineered and sampled data in a new table, which you could use in the [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="3abb5-287">En esta sección se creará una nueva tabla para almacenar los datos de ingeniería y muestreados.</span><span class="sxs-lookup"><span data-stu-id="3abb5-287">In this section we will create a new table to hold the sampled and engineered data.</span></span> <span data-ttu-id="3abb5-288">En la sección [Exploración de datos e ingeniería de características en SQL Server](#dbexplore) se proporciona un ejemplo de una consulta SQL directa para la creación del modelo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-288">An example of a direct SQL query for model building is provided in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-the-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="3abb5-289">Cree una tabla de ejemplo y rellénela con el 1 % de las tablas combinadas.</span><span class="sxs-lookup"><span data-stu-id="3abb5-289">Create a Sample Table and Populate with 1% of the Joined Tables.</span></span> <span data-ttu-id="3abb5-290">Quite la tabla primero si existe.</span><span class="sxs-lookup"><span data-stu-id="3abb5-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="3abb5-291">En esta sección, se combinan las tablas **nyctaxi\_trip** y **nyctaxi\_fare**, se extrae una muestra aleatoria de un 1 % y se conservan los datos del muestreo en un nuevo nombre de tabla **nyctaxi\_one\_percent**:</span><span class="sxs-lookup"><span data-stu-id="3abb5-291">In this section, we join the tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist the sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="3abb5-292">Exploración de datos mediante consultas SQL en Blocs de notas de IPython</span><span class="sxs-lookup"><span data-stu-id="3abb5-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="3abb5-293">En esta sección, se explorarán las distribuciones de datos con los datos de 1 % de muestreo que se conservan en la nueva tabla que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3abb5-293">In this section, we explore data distributions using the 1% sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="3abb5-294">Tenga en cuenta que se pueden realizar exploraciones similares mediante las tablas originales, con el uso opcional de **TABLESAMPLE** para limitar el ejemplo de exploración o mediante la limitación de los resultados a un período de tiempo determinado con las particiones **pickup\_datetime**, como se muestra en la sección [Exploración de datos e ingeniería de características en SQL Server](#dbexplore).</span><span class="sxs-lookup"><span data-stu-id="3abb5-294">Note that similar explorations can be performed using the original tables, optionally using **TABLESAMPLE** to limit the exploration sample or by limiting the results to a given time period using the **pickup\_datetime** partitions, as illustrated in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="3abb5-295">Exploración: distribución diaria de carreras</span><span class="sxs-lookup"><span data-stu-id="3abb5-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="3abb5-296">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="3abb5-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="3abb5-297">Generación de características mediante consultas SQL en Blocs de notas de IPython</span><span class="sxs-lookup"><span data-stu-id="3abb5-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="3abb5-298">En esta sección, se generarán nuevas etiquetas y características directamente mediante consultas SQL, que funcionarán con la muestra de 1 % que se creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="3abb5-298">In this section we will generate new labels and features directly using SQL queries, operating on the 1% sample table we created in the previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="3abb5-299">Generación de etiquetas: generar etiquetas de clase</span><span class="sxs-lookup"><span data-stu-id="3abb5-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="3abb5-300">En el ejemplo siguiente, se generan dos conjuntos de etiquetas que se usan para el modelado:</span><span class="sxs-lookup"><span data-stu-id="3abb5-300">In the following example, we generate two sets of labels to use for modeling:</span></span>

1. <span data-ttu-id="3abb5-301">Etiquetas de clase binaria **tipped** (que predecirán si se dará propina)</span><span class="sxs-lookup"><span data-stu-id="3abb5-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="3abb5-302">Etiquetas multiclase **tip\_class** (que predecirán el intervalo o la discretización de la propina)</span><span class="sxs-lookup"><span data-stu-id="3abb5-302">Multiclass Labels **tip\_class** (predicting the tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="3abb5-303">Ingeniería de características: características de recuento de columnas de categorías</span><span class="sxs-lookup"><span data-stu-id="3abb5-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="3abb5-304">En este ejemplo se transforma un campo de categoría en un campo numérico mediante el reemplazo de cada categoría por el recuento de sus apariciones en los datos.</span><span class="sxs-lookup"><span data-stu-id="3abb5-304">This example transforms a categorical field into a numeric field by replacing each category with the count of its occurrences in the data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="3abb5-305">Ingeniería de características: características de discretización de columnas numéricas</span><span class="sxs-lookup"><span data-stu-id="3abb5-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="3abb5-306">En este ejemplo se transforma un campo numérico continuo en intervalos de categoría preestablecidos; por ejemplo, la transformación de un campo numérico en un campo de categoría.</span><span class="sxs-lookup"><span data-stu-id="3abb5-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="3abb5-307">Ingeniería de características: extraer las características de ubicación a partir de una latitud o longitud decimal</span><span class="sxs-lookup"><span data-stu-id="3abb5-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="3abb5-308">En este ejemplo se desglosa la representación decimal de un campo de longitud o latitud en varios campos de región de granularidad diferente, como país, provincia, localidad, bloque, etc.  Tenga en cuenta que los nuevos campos geográficos no están asignados a ubicaciones reales.</span><span class="sxs-lookup"><span data-stu-id="3abb5-308">This example breaks down the decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that the new geo-fields are not mapped to actual locations.</span></span> <span data-ttu-id="3abb5-309">Para obtener información sobre la asignación de ubicaciones de códigos geográficos, consulte [Servicios REST de Mapas de Bing](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="3abb5-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="3abb5-310">Comprobar el formulario final de la tabla con características</span><span class="sxs-lookup"><span data-stu-id="3abb5-310">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="3abb5-311">Ya está todo listo para pasar a la creación del modelo y la implementación del mismo en [Aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="3abb5-311">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="3abb5-312">Los datos están listos para cualquiera de los problemas de predicción identificados anteriormente, a saber:</span><span class="sxs-lookup"><span data-stu-id="3abb5-312">The data is ready for any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="3abb5-313">Clasificación binaria: para predecir si se dio propina en una carrera, o no.</span><span class="sxs-lookup"><span data-stu-id="3abb5-313">Binary classification: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="3abb5-314">Clasificación multiclase: para predecir el intervalo de la propina dada, según las clases definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3abb5-314">Multiclass classification: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="3abb5-315">Tarea de regresión: para predecir la cantidad de propina pagada en una carrera.</span><span class="sxs-lookup"><span data-stu-id="3abb5-315">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="3abb5-316"><a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3abb5-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="3abb5-317">Para iniciar el ejercicio de modelado, inicie sesión en el área de trabajo de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3abb5-317">To begin the modeling exercise, log in to your Azure Machine Learning workspace.</span></span> <span data-ttu-id="3abb5-318">Si aún no ha creado un área de trabajo de aprendizaje automático, consulte [Creación y uso compartido de un área de trabajo de Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3abb5-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="3abb5-319">Para empezar a usar el Aprendizaje automático de Azure, consulte [¿Qué es Estudio de aprendizaje automático de Microsoft Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="3abb5-319">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="3abb5-320">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="3abb5-320">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="3abb5-321">La página principal del Estudio ofrece una gran cantidad de información, vídeos, tutoriales, vínculos a referencias de módulos y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="3abb5-321">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="3abb5-322">Para obtener más información acerca de Aprendizaje automático de Azure, consulte el [Centro de documentación de Aprendizaje automático de Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="3abb5-322">Fore more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="3abb5-323">Un experimento de entrenamiento típico consta de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="3abb5-323">A typical training experiment consists of the following:</span></span>

1. <span data-ttu-id="3abb5-324">Crear un experimento **+NUEVO** .</span><span class="sxs-lookup"><span data-stu-id="3abb5-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="3abb5-325">Obtener los datos para Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3abb5-325">Get the data to Azure Machine Learning.</span></span>
3. <span data-ttu-id="3abb5-326">Preprocesar, transformar y manipular los datos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3abb5-326">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="3abb5-327">Generar características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3abb5-327">Generate features as needed.</span></span>
5. <span data-ttu-id="3abb5-328">Dividir los datos en conjuntos de datos de entrenamiento, validación y pruebas (o disponer de conjuntos de datos independientes para cada uno).</span><span class="sxs-lookup"><span data-stu-id="3abb5-328">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="3abb5-329">Seleccionar uno o varios algoritmos de aprendizaje automático, según el problema de aprendizaje que se quiera resolver.</span><span class="sxs-lookup"><span data-stu-id="3abb5-329">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="3abb5-330">Por ejemplo: clasificación binaria, clasificación multiclase, regresión.</span><span class="sxs-lookup"><span data-stu-id="3abb5-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="3abb5-331">Entrenar uno o varios modelos utilizando el conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="3abb5-331">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="3abb5-332">Puntuar el conjunto de datos de validación con los modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="3abb5-332">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="3abb5-333">Evaluar los modelos para calcular las métricas relevantes para el problema de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="3abb5-333">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="3abb5-334">Ajustar los modelos y seleccionar el mejor para su implementación.</span><span class="sxs-lookup"><span data-stu-id="3abb5-334">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="3abb5-335">En este ejercicio, ya se han explorado y diseñado los datos en SQL Server, y también se ha decidido el tamaño de la muestra para la ingesta en Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3abb5-335">In this exercise, we have already explored and engineered the data in SQL Server, and decided on the sample size to ingest in Azure Machine Learning.</span></span> <span data-ttu-id="3abb5-336">Para crear uno o varios de los modelos de predicción, se decidió:</span><span class="sxs-lookup"><span data-stu-id="3abb5-336">To build one or more of the prediction models we decided:</span></span>

1. <span data-ttu-id="3abb5-337">Proporcionar los datos a Azure Machine Learning con el módulo [Importar datos][import-data], disponible en la sección **Data Input and Output** (Entrada y salida de datos).</span><span class="sxs-lookup"><span data-stu-id="3abb5-337">Get the data to Azure Machine Learning using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="3abb5-338">Para obtener más información, consulte la página de referencia del módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="3abb5-338">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Importar datos de Azure Machine Learning][17]
2. <span data-ttu-id="3abb5-340">Seleccionar **Azure SQL Database** como **Origen de datos** en el panel **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-340">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="3abb5-341">Escribir el nombre DNS de la base de datos en el campo **Nombre del servidor de la base de datos** .</span><span class="sxs-lookup"><span data-stu-id="3abb5-341">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="3abb5-342">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="3abb5-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="3abb5-343">Escribir el **nombre de la base de datos** en el campo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="3abb5-343">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="3abb5-344">Escribir el **nombre de usuario de SQL** en **Server user account name y la contraseña en **Server user account password**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-344">Enter the **SQL user name** in the **Server user aqccount name, and the password in the **Server user account password**.</span></span>
6. <span data-ttu-id="3abb5-345">Activar la opción **Aceptar cualquier certificado de servidor** .</span><span class="sxs-lookup"><span data-stu-id="3abb5-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="3abb5-346">En el área de texto editable **Consulta de base de datos** , pegar la consulta que extrae los campos de la base de datos necesarios (incluidos los campos calculados, como las etiquetas) y reducir la muestra al tamaño de muestra deseado.</span><span class="sxs-lookup"><span data-stu-id="3abb5-346">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="3abb5-347">En la ilustración siguiente se muestra un ejemplo de un experimento de clasificación binaria que lee datos directamente de la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3abb5-347">An example of a binary classification experiment reading data directly from the SQL Server database is in the figure below.</span></span> <span data-ttu-id="3abb5-348">Se pueden construir experimentos similares para problemas de clasificación multiclase y de regresión.</span><span class="sxs-lookup"><span data-stu-id="3abb5-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Entrenar Azure Machine Learning][10]

> [!IMPORTANT]
> <span data-ttu-id="3abb5-350">En los ejemplos de consultas de extracción y muestreo de datos de modelado de las secciones anteriores, **las etiquetas de los tres ejercicios de modelado se incluyen en la consulta**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-350">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="3abb5-351">Un paso importante (requerido) en cada uno de los ejercicios de modelado consiste en **excluir** las etiquetas innecesarias de los otros dos problemas y cualquier otra **fuga de destino**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-351">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="3abb5-352">Por ejemplo, cuando use clasificación binaria, utilice la etiqueta **tipped** y excluya los campos **tip\_class**, **tip\_amount** y **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="3abb5-352">For e.g., when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="3abb5-353">Estos últimos son fugas de destino ya que implican que se pagó propina.</span><span class="sxs-lookup"><span data-stu-id="3abb5-353">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="3abb5-354">Para excluir columnas innecesarias o fugas de destino, puede usar los módulos [Seleccionar columnas de conjunto de datos][select-columns] o [Editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3abb5-354">To exclude unnecessary columns and/or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="3abb5-355">Para obtener más información, consulte las páginas de referencia de [Seleccionar columnas de conjunto de datos][select-columns] y [Editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3abb5-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="3abb5-356"><a name="mldeploy"></a>Implementación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3abb5-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="3abb5-357">Cuando el modelo esté listo, podrá implementarlo fácilmente como un servicio web directamente desde el experimento.</span><span class="sxs-lookup"><span data-stu-id="3abb5-357">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="3abb5-358">Para más información sobre la implementación de servicios web Azure Machine Learning, vea [Implementar un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="3abb5-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="3abb5-359">Para implementar un nuevo servicio web, deberá:</span><span class="sxs-lookup"><span data-stu-id="3abb5-359">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="3abb5-360">Crear un experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="3abb5-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="3abb5-361">Implemente el servicio web.</span><span class="sxs-lookup"><span data-stu-id="3abb5-361">Deploy the web service.</span></span>

<span data-ttu-id="3abb5-362">Para crear un experimento de puntuación a partir de un experimento de entrenamiento **Finalizado**, haga clic en **CREAR EXPERIMENTO DE PUNTUACIÓN** en la barra de acciones inferior.</span><span class="sxs-lookup"><span data-stu-id="3abb5-362">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Puntuación de Azure][18]

<span data-ttu-id="3abb5-364">Aprendizaje automático de Azure intentará crear un experimento de puntuación en función de los componentes del experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="3abb5-364">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="3abb5-365">En concreto, hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3abb5-365">In particular, it will:</span></span>

1. <span data-ttu-id="3abb5-366">Guardar el modelo entrenado y quitar los módulos de entrenamiento del modelo.</span><span class="sxs-lookup"><span data-stu-id="3abb5-366">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="3abb5-367">Identificar un **puerto de entrada** lógico que represente el esquema de datos de entrada esperado.</span><span class="sxs-lookup"><span data-stu-id="3abb5-367">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="3abb5-368">Identificar un **puerto de salida** lógico que represente el esquema de salida del servicio web.</span><span class="sxs-lookup"><span data-stu-id="3abb5-368">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="3abb5-369">Cuando se crea el experimento de puntuación, revíselo y ajústelo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3abb5-369">When the scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="3abb5-370">Un ajuste común consiste en reemplazar la consulta o el conjunto de datos de entrada por uno que excluya los campos de etiqueta, ya que estos no estarán disponibles cuando se llame al servicio.</span><span class="sxs-lookup"><span data-stu-id="3abb5-370">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="3abb5-371">También es una buena práctica reducir el tamaño de la consulta o del conjunto de datos de entrada a unos pocos registros, los necesarios para indicar el esquema de entrada.</span><span class="sxs-lookup"><span data-stu-id="3abb5-371">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="3abb5-372">En el caso del puerto de salida, es habitual excluir todos los campos de entrada e incluir solo las **etiquetas puntuadas** y las **probabilidades puntuada**s en la salida mediante el módulo [Seleccionar columnas de conjunto de datos][select-columns].</span><span class="sxs-lookup"><span data-stu-id="3abb5-372">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="3abb5-373">En la ilustración siguiente se muestra un ejemplo de experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="3abb5-373">A sample scoring experiment is in the figure below.</span></span> <span data-ttu-id="3abb5-374">Cuando todo esté listo para implementar, haga clic en el botón **PUBLICAR SERVICIO WEB** de la barra de acciones inferior.</span><span class="sxs-lookup"><span data-stu-id="3abb5-374">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Publicar Azure Machine Learning][11]

<span data-ttu-id="3abb5-376">Para recapitular, en este tutorial paso a paso se ha creado un entorno de ciencia de datos de Azure, se ha trabajado con un conjunto grande de datos público de principio a fin, desde la adquisición de los datos al entrenamiento del modelo, y la implementación de un servicio web de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3abb5-376">To recap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all the way from data acquisition to model training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="3abb5-377">Información de licencia</span><span class="sxs-lookup"><span data-stu-id="3abb5-377">License Information</span></span>
<span data-ttu-id="3abb5-378">Microsoft comparte este tutorial de ejemplo y sus scripts adjuntos y Blocs de notas de IPython bajo la licencia MIT.</span><span class="sxs-lookup"><span data-stu-id="3abb5-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="3abb5-379">Consulte el archivo LICENSE.txt que se encuentra en el directorio del código de ejemplo en GitHub para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="3abb5-379">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="3abb5-380">Referencias</span><span class="sxs-lookup"><span data-stu-id="3abb5-380">References</span></span>
<span data-ttu-id="3abb5-381">•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="3abb5-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="3abb5-382">•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="3abb5-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="3abb5-383">•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="3abb5-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
