---
title: "aaaBuild e implementar un modelo de aprendizaje automático mediante SQL Server en una máquina virtual de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="bcc03-103">Hola proceso de ciencia de datos de equipo en acción: uso de SQL Server</span><span class="sxs-lookup"><span data-stu-id="bcc03-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="bcc03-104">En este tutorial, guían en proceso de Hola de creación e implementación de un modelo de aprendizaje automático mediante SQL Server y un conjunto de datos disponible públicamente--hello [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="bcc03-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="bcc03-105">procedimiento de Hello sigue un flujo de trabajo de ciencia de datos estándar: introducir y explorar los datos de hello, ingeniero de aprendizaje de toofacilitate de características, a continuación, generar e implementar un modelo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="bcc03-106"><a name="dataset"></a>Descripción del conjunto de datos NYC Taxi Trip</span><span class="sxs-lookup"><span data-stu-id="bcc03-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="bcc03-107">Hola datos NYC Taxi recorridos es aproximadamente 20GB de archivos comprimidos de CSV (sin comprimir de ~ 48GB), que incluye más de 173 millones hello y viajes individuales puntuación de pago para cada recorrido.</span><span class="sxs-lookup"><span data-stu-id="bcc03-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="bcc03-108">Cada registro de ida y vuelta incluye ubicación de entrega y recogida de Hola y tiempo, hack anonimizado (controlador) número de licencia y número medallion (identificador único del taxi).</span><span class="sxs-lookup"><span data-stu-id="bcc03-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="bcc03-109">datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:</span><span class="sxs-lookup"><span data-stu-id="bcc03-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="bcc03-110">Hola 'trip_data' CSV contiene los detalles de ida y vuelta, como el número de los pasajeros, recogida y puntos de caída, duración de ida y vuelta y duración del viaje.</span><span class="sxs-lookup"><span data-stu-id="bcc03-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="bcc03-111">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bcc03-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="bcc03-112">Hello 'trip_fare' CSV contiene detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago.</span><span class="sxs-lookup"><span data-stu-id="bcc03-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="bcc03-113">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bcc03-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="bcc03-114">recorridos de toojoin de clave única de Hello\_datos y recorridos\_tarifa se compone de campos de hello: medallion, prueba\_licencia y recogida\_fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="bcc03-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="bcc03-115"><a name="mltasks"></a>Ejemplos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="bcc03-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="bcc03-116">Se formulará tres problemas de predicción basándose en hello *sugerencia\_cantidad*, a saber:</span><span class="sxs-lookup"><span data-stu-id="bcc03-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="bcc03-117">Clasificación binaria: permite predecir si se pagó una propina tras una carrera, o no; es decir, un valor de *tip\_amount* mayor que 0 $ es un ejemplo positivo, mientras que un valor de *tip\_amount* de 0 $ es un ejemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="bcc03-118">Clasificación multiclase: intervalo de hello toopredict de sugerencia de pago para recorridos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="bcc03-119">Se divide hello *sugerencia\_cantidad* en cinco bandejas o clases:</span><span class="sxs-lookup"><span data-stu-id="bcc03-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="bcc03-120">Tarea de regresión: cantidad de hello toopredict de sugerencia de pago para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="bcc03-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="bcc03-121"><a name="setup"></a>Configurar el entorno de ciencia de análisis avanzado de hello datos de Azure</span><span class="sxs-lookup"><span data-stu-id="bcc03-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="bcc03-122">Como puede ver en hello [el entorno de su Plan](machine-learning-data-science-plan-your-environment.md) guía, hay varios toowork de opciones con conjunto de datos de Nueva York Taxi viajes de hello en Azure:</span><span class="sxs-lookup"><span data-stu-id="bcc03-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="bcc03-123">Trabajar con datos de hello en blobs de Azure, a continuación, modelo de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="bcc03-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="bcc03-124">Cargar datos de hello en una base de datos de SQL Server, a continuación, modelo de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="bcc03-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="bcc03-125">En este tutorial se indicará la importación masiva paralelas de hello tooa de datos SQL Server, exploración de datos, la característica de ingeniería y hacia abajo de muestreo utilizando SQL Server Management Studio, así como usar el Bloc de notas de IPython.</span><span class="sxs-lookup"><span data-stu-id="bcc03-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="bcc03-126">Los [scripts de ejemplo](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) y [blocs de notas de IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) se comparten en GitHub.</span><span class="sxs-lookup"><span data-stu-id="bcc03-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="bcc03-127">Un toowork de Bloc de notas de IPython de ejemplo con datos de hello en blobs de Azure también está disponible en hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="bcc03-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="bcc03-128">tooset del entorno de ciencia de datos de Azure:</span><span class="sxs-lookup"><span data-stu-id="bcc03-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="bcc03-129">crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bcc03-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="bcc03-130">Creación de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="bcc03-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="bcc03-131">[Aprovisione una máquina virtual de ciencia de datos](machine-learning-data-science-setup-sql-server-virtual-machine.md), que proporcionará un servidor de SQL Server y un servidor de Notebook de IPython.</span><span class="sxs-lookup"><span data-stu-id="bcc03-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bcc03-132">las secuencias de comandos de ejemplo de Hola y notas de IPython será tooyour descargado ciencia de datos virtual machine durante el proceso de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="bcc03-133">Cuando finalice el Hola script posterior a la instalación de VM, ejemplos de hello estarán en la biblioteca de documentos de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="bcc03-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="bcc03-134">Scripts de ejemplo: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="bcc03-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="bcc03-135">Blocs de notas de IPython de ejemplo: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="bcc03-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="bcc03-136">where `<user_name>` es el nombre de inicio de sesión de Windows de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bcc03-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="bcc03-137">Nos referiremos a carpetas de ejemplo de toohello como **secuencias de comandos de ejemplo** y **ejemplo blocs de notas de IPython**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="bcc03-138">En función de tamaño del conjunto de datos de hello, ubicación de origen de datos y entorno de destino de Azure seleccionado hello, este escenario es similar demasiado[escenario \#5: SQL Server en VM de Azure de destino de conjunto de datos grande en un archivos locales,](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="bcc03-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="bcc03-139"><a name="getdata"></a>Obtener Hola datos de origen pública</span><span class="sxs-lookup"><span data-stu-id="bcc03-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="bcc03-140">Hola tooget [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos desde su ubicación pública, puede usar cualquiera de los métodos de hello descritos en [tooand de mover los datos desde el almacenamiento de blobs de Azure](machine-learning-data-science-move-azure-blob.md) toocopy Hola datos tooyour nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bcc03-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="bcc03-141">datos de hello toocopy con AzCopy:</span><span class="sxs-lookup"><span data-stu-id="bcc03-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="bcc03-142">Inicie sesión en la máquina virtual (VM) de tooyour</span><span class="sxs-lookup"><span data-stu-id="bcc03-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="bcc03-143">Crear un nuevo directorio en el disco de datos de la máquina virtual de hello (Nota: no use Hola disco temporal que se incluye con hello máquina virtual como un disco de datos).</span><span class="sxs-lookup"><span data-stu-id="bcc03-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="bcc03-144">En una ventana del símbolo del sistema, ejecute hello después de la línea de comandos de Azcopy, reemplazando < path_to_data_folder > con la carpeta de datos creada en (2):</span><span class="sxs-lookup"><span data-stu-id="bcc03-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="bcc03-145">Cuando se completa el Hola AzCopy, un total de 24 zip archivos CSV (12 de ida y vuelta\_datos y 12 para recorridos\_tarifa) debe estar en la carpeta de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="bcc03-146">Descomprimir archivos de hello descargado.</span><span class="sxs-lookup"><span data-stu-id="bcc03-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="bcc03-147">Tenga en cuenta carpeta Hola donde residen los archivos de hello sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="bcc03-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="bcc03-148">Esta carpeta será la que se hace referencia tooas Hola < ruta de acceso\_a\_datos\_archivos\>.</span><span class="sxs-lookup"><span data-stu-id="bcc03-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="bcc03-149"><a name="dbload"></a>Importación masiva de datos en una base de datos de SQL Server</span><span class="sxs-lookup"><span data-stu-id="bcc03-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="bcc03-150">Hello rendimiento de carga/transferir grandes cantidades de base de datos SQL de tooan de datos y las consultas posteriores se puede mejorar mediante el uso de *Partitioned Tables and vistas*.</span><span class="sxs-lookup"><span data-stu-id="bcc03-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="bcc03-151">En esta sección, se sigue las instrucciones de hello descritas en [paralelo masiva datos utilizando SQL partición de tablas de importación](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate un nueva base de datos y cargar Hola datos en tablas con particiones en paralelo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="bcc03-152">Iniciar una sesión en tooyour VM, **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="bcc03-153">Conéctese con la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="bcc03-153">Connect using Windows Authentication.</span></span>
   
    ![Conexión SSMS][12]
3. <span data-ttu-id="bcc03-155">Si todavía no ha cambiado el modo de autenticación de SQL Server de hello ni crea un nuevo usuario de inicio de sesión SQL, abra el archivo de script de Hola denominado **cambiar\_auth.sql** en hello **secuencias de comandos de ejemplo** carpeta.</span><span class="sxs-lookup"><span data-stu-id="bcc03-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="bcc03-156">Cambiar el nombre de usuario predeterminado de Hola y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="bcc03-156">Change hello  default user name and password.</span></span> <span data-ttu-id="bcc03-157">Haga clic en **! Ejecutar** en secuencia de comandos de hello barra de herramientas toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Ejecutar script][13]
4. <span data-ttu-id="bcc03-159">Comprobar o cambiar Hola se almacenará la base de datos y registro tooensure carpetas predeterminado que recién creado bases de datos en un disco de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bcc03-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="bcc03-160">imagen de VM de SQL Server de Hola que está optimizado para cargas de almacén de datos está preconfigurado con discos de datos y de registro.</span><span class="sxs-lookup"><span data-stu-id="bcc03-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="bcc03-161">Si la máquina virtual no incluía un disco de datos y agregar nuevos discos duros virtuales durante Hola proceso de configuración de máquina virtual, cambie las carpetas predeterminadas hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="bcc03-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="bcc03-162">Nombre de SQL Server contextual Hola Hola dejado el panel y haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Propiedades de SQL Server][14]
   * <span data-ttu-id="bcc03-164">Seleccione **configuración de base de datos** de hello **seleccionar una página** lista toohello izquierda.</span><span class="sxs-lookup"><span data-stu-id="bcc03-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="bcc03-165">Comprobar o cambiar hello **ubicaciones predeterminadas de la base de datos** toohello **disco de datos** ubicaciones de su elección.</span><span class="sxs-lookup"><span data-stu-id="bcc03-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="bcc03-166">Esto es donde nuevas bases de datos residen si creado con la configuración de ubicación predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![Valores predeterminados de Base de datos SQL][15]  
5. <span data-ttu-id="bcc03-168">toocreate una nueva base de datos y un conjunto de grupos de archivos toohold Hola tablas con particiones, abra el script de ejemplo de Hola **crear\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="bcc03-169">script de Hola creará una nueva base de datos denominada **TaxiNYC** y 12 grupos de archivos en la ubicación de datos predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="bcc03-170">Cada uno de los grupos de archivos contendrá un mes de datos de trip\_data y trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="bcc03-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="bcc03-171">Modifique el nombre de la base de datos de hello, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="bcc03-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="bcc03-172">Haga clic en **! Ejecutar** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="bcc03-173">A continuación, cree dos tablas de partición, uno para el recorrido de hello\_datos y otro para el recorrido de hello\_tarifa.</span><span class="sxs-lookup"><span data-stu-id="bcc03-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="bcc03-174">Abra el script de ejemplo de Hola **crear\_con particiones\_table.sql**, que:</span><span class="sxs-lookup"><span data-stu-id="bcc03-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="bcc03-175">Crear una partición función toosplit Hola de datos por mes.</span><span class="sxs-lookup"><span data-stu-id="bcc03-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="bcc03-176">Crear un toomap de esquema de partición datos tooa otro grupo de archivos de cada mes.</span><span class="sxs-lookup"><span data-stu-id="bcc03-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="bcc03-177">Crear el esquema de partición de dos tablas con particiones toohello asignada: **nyctaxi\_recorridos** contendrá recorridos hello\_datos y **nyctaxi\_tarifa** contendrá recorridos Hola \_resultados son los datos.</span><span class="sxs-lookup"><span data-stu-id="bcc03-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="bcc03-178">Haga clic en **! Ejecutar** toorun Hola script y crear tablas con particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="bcc03-179">Hola **secuencias de comandos de ejemplo** carpeta, hay dos scripts de PowerShell de ejemplo proporcionan toodemonstrate importaciones por lotes paralela tooSQL servidor de tablas de datos.</span><span class="sxs-lookup"><span data-stu-id="bcc03-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="bcc03-180">**BCP\_paralelo\_generic.ps1** es una secuencia de comandos genérica tooparallel importación masiva de datos en una tabla.</span><span class="sxs-lookup"><span data-stu-id="bcc03-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="bcc03-181">Modificar variables de entrada y de destino a esta Hola de tooset de secuencia de comandos como se indica en las líneas de comentario de hello en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="bcc03-182">**BCP\_paralelo\_nyctaxi.ps1** es una versión preconfigurada de script genérico de Hola y puede ser tootooload usa ambas tablas para los datos de Nueva York Taxi viajes Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="bcc03-183">Menú contextual hello **bcp\_paralelo\_nyctaxi.ps1** nombre del script y haga clic en **editar** tooopen en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcc03-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="bcc03-184">Hola de revisión preestablecido variables y modificar el nombre de base de datos seleccionada tooyour correspondiente, carpeta de datos de entrada, carpeta de registro de destino y archivos de formato de ejemplo de las rutas de acceso toohello **nyctaxi_trip.xml** y **nyctaxi\_ Fare.XML** (proporcionadas en hello **secuencias de comandos de ejemplo** carpeta).</span><span class="sxs-lookup"><span data-stu-id="bcc03-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Datos de importación en bloque][16]
   
    <span data-ttu-id="bcc03-186">También puede seleccionar el modo de autenticación de hello, el valor predeterminado es autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="bcc03-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="bcc03-187">Haga clic en la flecha verde de Hola en hello toorun de barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="bcc03-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="bcc03-188">script de Hola iniciará 24 operaciones de importación masiva en paralelo, 12 para cada tabla con particiones.</span><span class="sxs-lookup"><span data-stu-id="bcc03-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="bcc03-189">Puede supervisar Hola progreso de la importación de datos, abra la carpeta de datos predeterminada de hello SQL Server como conjunto anterior.</span><span class="sxs-lookup"><span data-stu-id="bcc03-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="bcc03-190">informes de script de PowerShell de Hola Hola horas inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="bcc03-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="bcc03-191">Cuando todas las importaciones que completar de forma masiva, se registrará Hola hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="bcc03-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="bcc03-192">Compruebe Hola destino registro carpeta tooverify importaciones masivas de hello tuvieron éxito, es decir, errores no notifican en la carpeta de registro de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="bcc03-193">La base de datos ya está preparada para la exploración, diseño de características y otras operaciones que desee.</span><span class="sxs-lookup"><span data-stu-id="bcc03-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="bcc03-194">Puesto que las tablas de hello tienen particiones según toohello **recogida\_datetime** campo, las consultas que incluyen **recogida\_datetime** condiciones en hello  **DONDE** cláusula se beneficiará de esquema de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="bcc03-195">En **SQL Server Management Studio**, explorar el script de ejemplo de Hola proporciona **ejemplo\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="bcc03-196">toorun cualquiera de las consultas de ejemplo de Hola, resaltado Hola líneas de consulta, a continuación, haga clic en **! Ejecutar** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="bcc03-197">Hola datos NYC Taxi viajes se carga en dos tablas independientes.</span><span class="sxs-lookup"><span data-stu-id="bcc03-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="bcc03-198">operaciones de combinación de tooimprove, se recomienda encarecidamente tablas de hello tooindex.</span><span class="sxs-lookup"><span data-stu-id="bcc03-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="bcc03-199">script de ejemplo de Hola **crear\_con particiones\_index.sql** crea índices con particiones en la clave de combinación compuesto de hello **medallion, prueba\_licencia y recogida\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="bcc03-200"><a name="dbexplore"></a>Exploración de datos e ingeniería de características en SQL Server</span><span class="sxs-lookup"><span data-stu-id="bcc03-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="bcc03-201">En esta sección, se llevará a cabo generación de exploración y la característica de datos mediante la ejecución de consultas SQL directamente en hello **SQL Server Management Studio** usando la base de datos de SQL Server de hello creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bcc03-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="bcc03-202">Un script de ejemplo denominado **ejemplo\_queries.sql** se proporciona en hello **secuencias de comandos de ejemplo** carpeta.</span><span class="sxs-lookup"><span data-stu-id="bcc03-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="bcc03-203">Modificar el nombre de base de datos de hello script toochange hello, si es diferente del valor predeterminado de hello: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="bcc03-204">En este ejercicio, se hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bcc03-204">In this exercise, we will:</span></span>

* <span data-ttu-id="bcc03-205">Conectar demasiado**SQL Server Management Studio** mediante autenticación de Windows o con nombre de inicio de sesión SQL hello y autenticación de SQL y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="bcc03-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="bcc03-206">Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="bcc03-207">Investigue la calidad de los datos de los campos de longitud y latitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="bcc03-208">Generar etiquetas de clasificación multiclase y binaria basándose en hello **sugerencia\_cantidad**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="bcc03-209">Generar características y calcular o comparar distancias de carreras.</span><span class="sxs-lookup"><span data-stu-id="bcc03-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="bcc03-210">Combinar Hola dos tablas y extraer una muestra aleatoria que será usado toobuild modelos.</span><span class="sxs-lookup"><span data-stu-id="bcc03-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="bcc03-211">Cuando esté listo tooproceed tooAzure aprendizaje automático, puede:</span><span class="sxs-lookup"><span data-stu-id="bcc03-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="bcc03-212">Guardar Hola final SQL consulta tooextract y ejemplo Hola datos y copiar y pegar Hola consulta directamente en un [importar datos] [ import-data] módulo aprendizaje automático de Azure, o</span><span class="sxs-lookup"><span data-stu-id="bcc03-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="bcc03-213">Hola muestreada se conservan y datos de ingeniería que tiene previsto toouse para crear una nueva base de datos de modelo de tabla y usar nueva tabla de hello en hello [importar datos] [ import-data] módulo aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="bcc03-214">En esta sección se guardará Hola consulta final tooextract y Hola datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="bcc03-215">segundo método de Hola se muestra en hello [exploración de datos y de ingeniería de características en el Bloc de notas de IPython](#ipnb) sección.</span><span class="sxs-lookup"><span data-stu-id="bcc03-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="bcc03-216">Para una comprobación rápida del número de Hola de filas y columnas de hello en tablas se rellenaron anteriormente con la importación masiva paralelas,</span><span class="sxs-lookup"><span data-stu-id="bcc03-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="bcc03-217">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="bcc03-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="bcc03-218">Este ejemplo identifica medallion Hola (números de taxi) con más de 100 viajes dentro de un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="bcc03-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="bcc03-219">consulta de Hola se beneficiaría de acceso a la tabla con particiones de hello porque está condicionado por esquema de partición de Hola de **recogida\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="bcc03-220">Consultar el conjunto de datos completo de hello también hará que el uso de la tabla con particiones de Hola o examen de índice.</span><span class="sxs-lookup"><span data-stu-id="bcc03-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="bcc03-221">Exploración: distribución de carreras por medallion y hack_license</span><span class="sxs-lookup"><span data-stu-id="bcc03-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="bcc03-222">Evaluación de la calidad de los datos: comprobar los registros con longitud o latitud incorrectas</span><span class="sxs-lookup"><span data-stu-id="bcc03-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="bcc03-223">En este ejemplo se investiga si alguno de los campos de longitud o latitud de Hola o contiene un valor no válido (grados Radián deben estar entre -90 y 90), o tener (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="bcc03-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="bcc03-224">Exploración: distribución de carreras con propinas frente a sin propinas</span><span class="sxs-lookup"><span data-stu-id="bcc03-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="bcc03-225">Este ejemplo busca el número de Hola de viajes que se han superpuesto frente a no superpuesto en un momento determinado período (o en el conjunto de datos completo de hello si cubriendo año completo hello) de.</span><span class="sxs-lookup"><span data-stu-id="bcc03-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="bcc03-226">Esta distribución refleja Hola etiqueta binario distribución toobe que más adelante se usa para el modelo de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="bcc03-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="bcc03-227">Exploración: distribución por intervalos y clases de propinas</span><span class="sxs-lookup"><span data-stu-id="bcc03-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="bcc03-228">Este ejemplo calcula distribución Hola de intervalos de sugerencia en un momento determinado período (o en el conjunto de datos completo de hello si relativo Hola completa año).</span><span class="sxs-lookup"><span data-stu-id="bcc03-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="bcc03-229">Se trata de distribución de Hola de clases de etiqueta de Hola que usará más adelante para el modelado de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="bcc03-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

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

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="bcc03-230">Exploración: calcular y comparar la distancia de la carrera</span><span class="sxs-lookup"><span data-stu-id="bcc03-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="bcc03-231">Este ejemplo convierte la longitud de recogida y entrega de Hola y geografía de latitud tooSQL señala, calcula la distancia de viaje hello mediante diferencia de puntos de geography SQL y devuelve una muestra aleatoria de resultados de hello para la comparación.</span><span class="sxs-lookup"><span data-stu-id="bcc03-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="bcc03-232">ejemplo de Hola limita los resultados de hello toovalid coordina únicamente con la consulta de evaluación de calidad Hola datos cubierto anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bcc03-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

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

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="bcc03-233">Diseño de características en consultas SQL</span><span class="sxs-lookup"><span data-stu-id="bcc03-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="bcc03-234">Hola etiqueta geography y generación de conversión exploración también pueden ser consultas toogenerate usa etiquetas/características mediante la eliminación de hello contar parte.</span><span class="sxs-lookup"><span data-stu-id="bcc03-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="bcc03-235">Se proporcionan ejemplos SQL de ingeniería de características adicionales en hello [exploración de datos y de ingeniería de características en el Bloc de notas de IPython](#ipnb) sección.</span><span class="sxs-lookup"><span data-stu-id="bcc03-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="bcc03-236">Resulta más eficaz toorun Hola característica generación las consultas en el conjunto de datos completo de Hola o un gran subconjunto de dicho tipo mediante consultas SQL que se ejecutan directamente en la instancia de base de datos de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="bcc03-237">se pueden ejecutar consultas de Hello en **SQL Server Management Studio**, Bloc de notas de IPython o cualquier herramienta o entorno de desarrollo que pueden tener acceso a Hola base de datos local o remotamente.</span><span class="sxs-lookup"><span data-stu-id="bcc03-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="bcc03-238">Preparación de los datos para la creación del modelo</span><span class="sxs-lookup"><span data-stu-id="bcc03-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="bcc03-239">Hola de combinaciones de consulta siguiente Hello **nyctaxi\_recorridos** y **nyctaxi\_tarifa** tablas, genera una etiqueta de clasificación binaria **superpuesto**, etiqueta de clasificación multiclase **sugerencia\_clase**y extrae una muestra aleatoria de 1% del conjunto de datos combinado Hola completa.</span><span class="sxs-lookup"><span data-stu-id="bcc03-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="bcc03-240">Esta consulta se puede copiar y pegar directamente en hello [estudio de aprendizaje automático de Azure](https://studio.azureml.net) [importar datos] [ import-data] módulo de recopilación de datos directas de base de datos de SQL Server de Hola instancia de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="bcc03-241">consulta de Hello excluye los registros con incorrecto (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="bcc03-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

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


## <span data-ttu-id="bcc03-242"><a name="ipnb"></a>Exploración de datos e ingeniería de características en el Bloc de notas de IPython</span><span class="sxs-lookup"><span data-stu-id="bcc03-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="bcc03-243">En esta sección, se llevará a cabo una exploración de datos y la generación de característica mediante consultas de Python y SQL contra Hola de base de datos de SQL Server creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bcc03-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="bcc03-244">Un bloc de notas de IPython de ejemplo denominado **machine-Learning-data-science-process-sql-story.ipynb** se proporciona en hello **ejemplo blocs de notas de IPython** carpeta.</span><span class="sxs-lookup"><span data-stu-id="bcc03-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="bcc03-245">Este bloc de notas también está disponible en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="bcc03-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="bcc03-246">Hola recomendada secuencia cuando se trabaja con grandes cantidades de datos es la siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="bcc03-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="bcc03-247">Leer en una pequeña muestra de datos de hello en un marco de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="bcc03-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="bcc03-248">Realizar algunas visualizaciones y exploraciones con los datos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="bcc03-249">Experimente con ingeniería de característica con hello los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="bcc03-250">Para la exploración de datos mayor, manipulación de datos y la ingeniería de característica, utilice Python tooissue SQL consultas directamente en la base de datos de SQL Server de Hola Hola VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="bcc03-251">Decidir toouse de tamaño de ejemplo de Hola para una compilación de modelo de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="bcc03-252">Cuando esté listo tooproceed tooAzure aprendizaje automático, es posible que ya sea:</span><span class="sxs-lookup"><span data-stu-id="bcc03-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="bcc03-253">Guardar Hola final SQL consulta tooextract y ejemplo Hola datos y copiar y pegar Hola consulta directamente en un [importar datos] [ import-data] módulo aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="bcc03-254">Este método se muestra en hello [generar modelos de aprendizaje automático de Azure](#mlmodel) sección.</span><span class="sxs-lookup"><span data-stu-id="bcc03-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="bcc03-255">Conservar Hola muestreada y los datos de ingeniería piensa toouse para compilar en una nueva tabla de base de datos de modelo, utilice la nueva tabla de Hola Hola [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="bcc03-256">siguiente Hola es unos exploración de datos, visualización de datos y ejemplos de ingeniería de característica.</span><span class="sxs-lookup"><span data-stu-id="bcc03-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="bcc03-257">Para obtener más ejemplos, vea el Bloc de notas del IPython de SQL de ejemplo de Hola Hola **ejemplo blocs de notas de IPython** carpeta.</span><span class="sxs-lookup"><span data-stu-id="bcc03-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="bcc03-258">Inicializar las credenciales de la base de datos</span><span class="sxs-lookup"><span data-stu-id="bcc03-258">Initialize Database Credentials</span></span>
<span data-ttu-id="bcc03-259">Inicializar la configuración de conexión de base de datos en hello siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="bcc03-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="bcc03-260">Crear conexiones de base de datos</span><span class="sxs-lookup"><span data-stu-id="bcc03-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="bcc03-261">Informe con el número de filas y columnas en la tabla nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="bcc03-261">Report number of rows and columns in table nyctaxi_trip</span></span>
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

* <span data-ttu-id="bcc03-262">Número total de filas = 173179759</span><span class="sxs-lookup"><span data-stu-id="bcc03-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="bcc03-263">Número total de columnas = 14</span><span class="sxs-lookup"><span data-stu-id="bcc03-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="bcc03-264">Lectura de un pequeño datos de ejemplo de Hola base de datos de SQL Server</span><span class="sxs-lookup"><span data-stu-id="bcc03-264">Read-in a small data sample from hello SQL Server Database</span></span>
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
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="bcc03-265">Tabla de ejemplo de Hola de tiempo tooread es 6.492000 segundos</span><span class="sxs-lookup"><span data-stu-id="bcc03-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="bcc03-266">Número de filas y columnas recuperadas = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="bcc03-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="bcc03-267">Estadísticas descriptivas</span><span class="sxs-lookup"><span data-stu-id="bcc03-267">Descriptive Statistics</span></span>
<span data-ttu-id="bcc03-268">Ahora están datos de hello muestreada tooexplore listo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="bcc03-269">Empezaremos con examinando Estadísticas descriptivas para hello **recorridos\_distancia** (o cualquier otro) Field (s):</span><span class="sxs-lookup"><span data-stu-id="bcc03-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="bcc03-270">Visualización: ejemplo de diagrama de caja</span><span class="sxs-lookup"><span data-stu-id="bcc03-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="bcc03-271">A continuación, veremos caja Hola para Hola de ida y vuelta distancia toovisualize hello cuantiles</span><span class="sxs-lookup"><span data-stu-id="bcc03-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagrama 1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="bcc03-273">Visualización: ejemplo de diagrama de distribución</span><span class="sxs-lookup"><span data-stu-id="bcc03-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagrama 2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="bcc03-275">Visualización: diagramas de barras y líneas</span><span class="sxs-lookup"><span data-stu-id="bcc03-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="bcc03-276">En este ejemplo, hemos discretizar distancia de viaje hello en cinco cubos y visualizar Hola discretizar los resultados.</span><span class="sxs-lookup"><span data-stu-id="bcc03-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="bcc03-277">Podemos trazar Hola por encima de la distribución de la Papelera de una barra o trazado como a continuación de línea</span><span class="sxs-lookup"><span data-stu-id="bcc03-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagrama 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagrama 4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="bcc03-280">Visualización: ejemplo de gráfico de dispersión</span><span class="sxs-lookup"><span data-stu-id="bcc03-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="bcc03-281">Se muestra el gráfico de dispersión entre **recorridos\_tiempo\_en\_s** y **recorridos\_distancia** toosee si hay alguna correlación</span><span class="sxs-lookup"><span data-stu-id="bcc03-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagrama 6][6]

<span data-ttu-id="bcc03-283">De igual forma podemos comprobar relación Hola entre **velocidad\_código** y **recorridos\_distancia**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagrama 8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="bcc03-285">Hola Submuestreo datos en SQL</span><span class="sxs-lookup"><span data-stu-id="bcc03-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="bcc03-286">Al preparar los datos de generación modelo [estudio de aprendizaje automático de Azure](https://studio.azureml.net), o bien puede decidir hello **toouse de consultas SQL directamente en el módulo de importación de datos de hello** o conservarlos Hola diseñados y muestrear datos de una tabla nueva, que puede usar en hello [importar datos] [ import-data] módulo con un sencillo **seleccione * FROM < su\_nueva\_tabla\_nombre >**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="bcc03-287">En esta sección que se creará un nuevo hello toohold de tabla muestrea y datos de ingeniería.</span><span class="sxs-lookup"><span data-stu-id="bcc03-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="bcc03-288">Se proporciona un ejemplo de una consulta SQL directo para la compilación del modelo en hello [exploración de datos y de ingeniería de características de SQL Server](#dbexplore) sección.</span><span class="sxs-lookup"><span data-stu-id="bcc03-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="bcc03-289">Crear una tabla de ejemplo y rellenar con % 1 de tablas unidas de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="bcc03-290">Quite la tabla primero si existe.</span><span class="sxs-lookup"><span data-stu-id="bcc03-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="bcc03-291">En esta sección, se combinan tablas de hello **nyctaxi\_recorridos** y **nyctaxi\_tarifa**, extraer una muestra aleatoria de 1% y conservar los datos de hello muestreada en un nuevo nombre de tabla  **nyctaxi\_una\_por ciento**:</span><span class="sxs-lookup"><span data-stu-id="bcc03-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

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

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="bcc03-292">Exploración de datos mediante consultas SQL en Blocs de notas de IPython</span><span class="sxs-lookup"><span data-stu-id="bcc03-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="bcc03-293">En esta sección, exploramos distribuciones de datos utilizando los datos de 1% muestreada Hola que se guardan en la nueva tabla de hello que hemos creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bcc03-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="bcc03-294">Tenga en cuenta que se pueden realizar exploraciones similar mediante tablas originales de hello, utilizando opcionalmente **TABLESAMPLE** toolimit de exploración de hello muestra o limitando Hola da como resultado tooa dado el período de tiempo mediante hello **recogida \_datetime** particiones, como se muestra en hello [exploración de datos y de ingeniería de características de SQL Server](#dbexplore) sección.</span><span class="sxs-lookup"><span data-stu-id="bcc03-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="bcc03-295">Exploración: distribución diaria de carreras</span><span class="sxs-lookup"><span data-stu-id="bcc03-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="bcc03-296">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="bcc03-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="bcc03-297">Generación de características mediante consultas SQL en Blocs de notas de IPython</span><span class="sxs-lookup"><span data-stu-id="bcc03-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="bcc03-298">En esta sección se generará nuevas etiquetas y en funcionamiento en la tabla de ejemplo de 1% de hello características directamente mediante consultas SQL, hemos creado en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="bcc03-299">Generación de etiquetas: generar etiquetas de clase</span><span class="sxs-lookup"><span data-stu-id="bcc03-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="bcc03-300">En el siguiente ejemplo de Hola, se generan dos conjuntos de toouse de etiquetas para el modelado:</span><span class="sxs-lookup"><span data-stu-id="bcc03-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="bcc03-301">Etiquetas de clase binaria **tipped** (que predecirán si se dará propina)</span><span class="sxs-lookup"><span data-stu-id="bcc03-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="bcc03-302">Las etiquetas multiclase **sugerencia\_clase** (predecir bin de sugerencia de Hola o intervalo)</span><span class="sxs-lookup"><span data-stu-id="bcc03-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
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

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="bcc03-303">Ingeniería de características: características de recuento de columnas de categorías</span><span class="sxs-lookup"><span data-stu-id="bcc03-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="bcc03-304">En este ejemplo se transforma un campo de categoría en un campo numérico si se reemplaza cada categoría con el recuento de Hola de sus repeticiones en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

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

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="bcc03-305">Ingeniería de características: características de discretización de columnas numéricas</span><span class="sxs-lookup"><span data-stu-id="bcc03-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="bcc03-306">En este ejemplo se transforma un campo numérico continuo en intervalos de categoría preestablecidos; por ejemplo, la transformación de un campo numérico en un campo de categoría.</span><span class="sxs-lookup"><span data-stu-id="bcc03-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

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

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="bcc03-307">Ingeniería de características: extraer las características de ubicación a partir de una latitud o longitud decimal</span><span class="sxs-lookup"><span data-stu-id="bcc03-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="bcc03-308">Este ejemplo divide representación decimal de Hola de un campo o la latitud en varios campos de región de granularidad diferente, como por ejemplo, país, ciudad, ciudad, bloque, etcetera. Tenga en cuenta que Hola geográfica-campos nuevos no asignados tooactual ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="bcc03-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="bcc03-309">Para obtener información sobre la asignación de ubicaciones de códigos geográficos, consulte [Servicios REST de Mapas de Bing](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="bcc03-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

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

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="bcc03-310">Comprobar el formulario final de Hola de tabla de caracterizará Hola</span><span class="sxs-lookup"><span data-stu-id="bcc03-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="bcc03-311">Ahora estamos listos tooproceed toomodel creación e implementación de modelo en [aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="bcc03-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="bcc03-312">datos de Hello están listos para cualquiera de los problemas de predicción de hello identificados anteriormente, a saber:</span><span class="sxs-lookup"><span data-stu-id="bcc03-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="bcc03-313">Clasificación binaria: toopredict o no se pagó una sugerencia para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="bcc03-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="bcc03-314">Clasificación multiclase: intervalo de hello toopredict de sugerencia de pago, según toohello clases definidas previamente.</span><span class="sxs-lookup"><span data-stu-id="bcc03-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="bcc03-315">Tarea de regresión: cantidad de hello toopredict de sugerencia de pago para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="bcc03-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="bcc03-316"><a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="bcc03-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="bcc03-317">toobegin Hola modelado ejercicio, inicie sesión en el área de trabajo de tooyour aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="bcc03-318">Si aún no ha creado un área de trabajo de aprendizaje automático, consulte [Creación y uso compartido de un área de trabajo de Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="bcc03-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="bcc03-319">tooget a trabajar con aprendizaje automático de Azure, consulte [¿qué es el estudio de aprendizaje automático de Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="bcc03-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="bcc03-320">Inicie sesión demasiado[estudio de aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="bcc03-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="bcc03-321">página de inicio de Studio Hola proporciona una gran cantidad de información, vídeos, tutoriales, vínculos toohello referencia de módulos y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="bcc03-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="bcc03-322">Para obtener más información acerca de aprendizaje automático de Azure, consulte hello [centro de documentación de aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="bcc03-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="bcc03-323">Un experimento de entrenamiento típico consta de siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="bcc03-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="bcc03-324">Crear un experimento **+NUEVO** .</span><span class="sxs-lookup"><span data-stu-id="bcc03-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="bcc03-325">Obtener datos de hello tooAzure aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="bcc03-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="bcc03-326">Preprocesar, transformar y manipular datos Hola según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bcc03-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="bcc03-327">Generar características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bcc03-327">Generate features as needed.</span></span>
5. <span data-ttu-id="bcc03-328">Dividir los datos de hello en conjuntos de datos de entrenamiento / / pruebas de validación (o tiene conjuntos de datos independiente para cada uno).</span><span class="sxs-lookup"><span data-stu-id="bcc03-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="bcc03-329">Seleccionar algoritmos función hello toosolve problema de aprendizaje de aprendizaje automático de uno o más.</span><span class="sxs-lookup"><span data-stu-id="bcc03-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="bcc03-330">Por ejemplo: clasificación binaria, clasificación multiclase, regresión.</span><span class="sxs-lookup"><span data-stu-id="bcc03-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="bcc03-331">Entrenar uno o varios modelos utilizando el conjunto de datos de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="bcc03-332">Puntuación Hola de conjunto de datos de validación utilizando modelos entrenados Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="bcc03-333">Evaluar Hola modelos toocompute Hola métricas pertinente para hello problema de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="bcc03-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="bcc03-334">Ajustar los modelos de Hola y Hola seleccione mejor modelo toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bcc03-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="bcc03-335">En este ejercicio, hemos ya explorar e ingeniería datos hello en SQL Server y decidido tooingest de tamaño de ejemplo de Hola en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="bcc03-336">toobuild uno o varios de los modelos de predicción de hello decidimos:</span><span class="sxs-lookup"><span data-stu-id="bcc03-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="bcc03-337">Obtener datos de hello tooAzure aprendizaje automático con hello [importar datos] [ import-data] módulo, disponibles en hello **datos de entrada y salida** sección.</span><span class="sxs-lookup"><span data-stu-id="bcc03-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="bcc03-338">Para obtener más información, vea hello [importar datos] [ import-data] página de referencia de módulo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Importar datos de Azure Machine Learning][17]
2. <span data-ttu-id="bcc03-340">Seleccione **base de datos de SQL Azure** como hello **origen de datos** en hello **propiedades** panel.</span><span class="sxs-lookup"><span data-stu-id="bcc03-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="bcc03-341">Escriba el nombre DNS de base de datos de Hola Hola **el nombre del servidor de base de datos** campo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="bcc03-342">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="bcc03-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="bcc03-343">Escriba hello **nombre de base de datos** en el campo correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="bcc03-344">Escriba hello **nombre de usuario SQL** Hola ** aqccount nombre de usuario y la contraseña de Hola Hola **contraseña de cuenta de usuario de servidor**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="bcc03-345">Activar la opción **Aceptar cualquier certificado de servidor** .</span><span class="sxs-lookup"><span data-stu-id="bcc03-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="bcc03-346">Hola **consulta de base de datos** editar el área de texto, pegue la consulta de Hola que extrae Hola necesarios campos (incluidos los campos calculados, como las etiquetas de hello) de la base de datos y el detalle de ejemplos de tamaño de la muestra de Hola datos toohello deseado.</span><span class="sxs-lookup"><span data-stu-id="bcc03-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="bcc03-347">Un ejemplo de un experimento de clasificación binaria leer los datos directamente desde la base de datos de SQL Server de hello es en hello siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="bcc03-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="bcc03-348">Se pueden construir experimentos similares para problemas de clasificación multiclase y de regresión.</span><span class="sxs-lookup"><span data-stu-id="bcc03-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Entrenar Azure Machine Learning][10]

> [!IMPORTANT]
> <span data-ttu-id="bcc03-350">Hola, extracción de datos de modelado y realizando un muestreo ejemplos de consultas que se proporcionan en las secciones anteriores, **todas las etiquetas de ejercicios de modelado de hello tres se incluyen en la consulta de hello**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="bcc03-351">Un paso importante (obligatorio) en cada uno de los ejercicios de modelado de hello es demasiado**excluir** Hola etiquetas innecesarias para hello otros problemas de dos y cualquier otro **destino pérdidas**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="bcc03-352">Para p. ej., cuando se usa la clasificación binaria, use etiqueta hello **superpuesto** y excluir los campos de hello **sugerencia\_clase**, **sugerencia\_cantidad**, y **total\_cantidad**.</span><span class="sxs-lookup"><span data-stu-id="bcc03-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="bcc03-353">Hola este último se pagan de pérdidas de destino ya que implican sugerencia Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="bcc03-354">las columnas innecesarias tooexclude o pérdidas de destino, puede usar hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo o hello [editar metadatos] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="bcc03-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="bcc03-355">Para obtener más información, consulte las páginas de referencia de [Seleccionar columnas de conjunto de datos][select-columns] y [Editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="bcc03-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="bcc03-356"><a name="mldeploy"></a>Implementación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="bcc03-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="bcc03-357">Cuando el modelo está listo, puede implementar fácilmente como un servicio web directamente desde el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="bcc03-358">Para más información sobre la implementación de servicios web Azure Machine Learning, vea [Implementar un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bcc03-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="bcc03-359">toodeploy un nuevo servicio web, debe:</span><span class="sxs-lookup"><span data-stu-id="bcc03-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="bcc03-360">Crear un experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="bcc03-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="bcc03-361">Implementar el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-361">Deploy hello web service.</span></span>

<span data-ttu-id="bcc03-362">toocreate una puntuación experimentar de un **finalizado** experimento de entrenamiento, haga clic en **crear EXPERIMENTO de puntuación** en la barra de acción inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Puntuación de Azure][18]

<span data-ttu-id="bcc03-364">Aprendizaje automático de Azure intentará toocreate un experimento de puntuación en función de los componentes de hello del experimento de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="bcc03-365">En concreto, hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bcc03-365">In particular, it will:</span></span>

1. <span data-ttu-id="bcc03-366">Guardar modelo entrenado hello y quite los módulos de entrenamiento del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="bcc03-367">Identificar un valor lógico **puerto de entrada** toorepresent Hola esperaba el esquema de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="bcc03-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="bcc03-368">Identificar un valor lógico **puerto de salida** esquema de salida del servicio de toorepresent hello web esperado.</span><span class="sxs-lookup"><span data-stu-id="bcc03-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="bcc03-369">Cuando se crea el experimento de puntuación de hello, revisarlo y ajustar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bcc03-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="bcc03-370">Un ajuste típico es el conjunto de datos de entrada de hello tooreplace o consulta con uno que excluye los campos de etiqueta, ya estos no estarán disponibles cuando se llama servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="bcc03-371">También es que un tamaño de hello tooreduce buenas prácticas de hello entrada tooa de conjunto de datos o de consultas pocos registros, suficiente esquema de entrada tooindicate Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="bcc03-372">Para el puerto de salida de hello, es común tooexclude entrados todos los campos y solo se incluyen hello **puntuación de etiquetas** y **probabilidades con puntuación** Hola Hola de salida [seleccionar columnas de conjunto de datos ] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="bcc03-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="bcc03-373">Un ejemplo de experimento de puntuación es en hello siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="bcc03-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="bcc03-374">Cuando esté listo toodeploy, haga clic en hello **publicar servicio WEB** botón de barra de acción de hello inferior.</span><span class="sxs-lookup"><span data-stu-id="bcc03-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publicar Azure Machine Learning][11]

<span data-ttu-id="bcc03-376">toorecap, en este tutorial tutorial, ha creado un entorno de ciencia de datos de Azure, ha trabajado con un conjunto de datos público grande todas las forma de Hola de toomodel de adquisición de datos de entrenamiento y la implementación de un servicio web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc03-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="bcc03-377">Información de licencia</span><span class="sxs-lookup"><span data-stu-id="bcc03-377">License Information</span></span>
<span data-ttu-id="bcc03-378">En este tutorial de ejemplo y sus elementos notebook(s) IPython y secuencias de comandos que se comparten por Microsoft bajo licencia MIT de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcc03-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="bcc03-379">Compruebe archivo LICENSE.txt de hello directorio de hello del código de ejemplo de Hola en GitHub para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="bcc03-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="bcc03-380">Referencias</span><span class="sxs-lookup"><span data-stu-id="bcc03-380">References</span></span>
<span data-ttu-id="bcc03-381">•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="bcc03-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="bcc03-382">•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="bcc03-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="bcc03-383">•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="bcc03-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
