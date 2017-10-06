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
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="b24c1-103">Hola proceso de ciencia de datos de equipo en acción: clústeres de Hadoop de HDInsight de Azure de uso</span><span class="sxs-lookup"><span data-stu-id="b24c1-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="b24c1-104">En este tutorial, usamos hello [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md) en un escenario de extremo a extremo mediante un [clúster de HDInsight Hadoop de Azure](https://azure.microsoft.com/services/hdinsight/) toostore, explorar y las características de datos de ingeniería de hello públicamente disponible [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) datos Hola de ejemplo del conjunto de datos y toodown.</span><span class="sxs-lookup"><span data-stu-id="b24c1-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="b24c1-105">Se generan los modelos de datos de hello con aprendizaje automático de Azure toohandle multiclase y binarias clasificación y regresión tareas de predicción.</span><span class="sxs-lookup"><span data-stu-id="b24c1-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="b24c1-106">Para ver un tutorial que muestra cómo toohandle clústeres de un conjunto de datos mayor (1 terabyte) para un escenario similar con Hadoop de HDInsight para el procesamiento de datos, vea [proceso de ciencia de datos de equipo - con clústeres de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="b24c1-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="b24c1-107">También es posible toouse un hello tooaccomplish de Bloc de notas de IPython tareas Tutorial Hola presentado con conjunto de datos de 1 TB de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="b24c1-108">Los usuarios que serían como tootry debe consultar este enfoque Hola [tutorial Criteo mediante una conexión ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tema.</span><span class="sxs-lookup"><span data-stu-id="b24c1-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="b24c1-109"><a name="dataset"></a>Descripción del conjunto de datos NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="b24c1-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="b24c1-110">Hola datos NYC Taxi recorridos es de aproximadamente 20GB comprimido valores separados por comas (CSV) de archivos de (~ 48GB sin comprimir), que incluye más de 173 millones hello y viajes individuales puntuación de pago para cada recorrido.</span><span class="sxs-lookup"><span data-stu-id="b24c1-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="b24c1-111">Cada registro de ida y vuelta incluye ubicación de entrega y recogida de Hola y tiempo, hack anonimizado (controlador) número de licencia y número medallion (identificador único del taxi).</span><span class="sxs-lookup"><span data-stu-id="b24c1-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="b24c1-112">datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:</span><span class="sxs-lookup"><span data-stu-id="b24c1-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="b24c1-113">archivos CSV de Hello 'trip_data' contienen detalles de ida y vuelta, como el número de los pasajeros, recogida y puntos de caída, duración de ida y vuelta y duración del viaje.</span><span class="sxs-lookup"><span data-stu-id="b24c1-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="b24c1-114">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b24c1-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="b24c1-115">archivos CSV de Hello 'trip_fare' contienen detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago.</span><span class="sxs-lookup"><span data-stu-id="b24c1-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="b24c1-116">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b24c1-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="b24c1-117">recorridos de toojoin de clave única de Hello\_datos y recorridos\_tarifa se compone de campos de hello: medallion, prueba\_licencia y recogida\_fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="b24c1-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="b24c1-118">tooget todas las de ida y vuelta determinado Hola detalles tooa relevante, es suficiente toojoin con tres claves: Hola "medallion", "hack\_licencia" y "recogida\_datetime".</span><span class="sxs-lookup"><span data-stu-id="b24c1-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="b24c1-119">Se describen algunos detalles más de los datos de hello cuando se almacenarlos en tablas de Hive en breve.</span><span class="sxs-lookup"><span data-stu-id="b24c1-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="b24c1-120"><a name="mltasks"></a>Ejemplos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="b24c1-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="b24c1-121">Cuando planee los datos, determinar tipo hello de predicciones que desee toomake en función de su análisis ayuda a aclarar las tareas de Hola que necesitará tooinclude en el proceso.</span><span class="sxs-lookup"><span data-stu-id="b24c1-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="b24c1-122">Presentamos tres ejemplos de problemas de predicción que se abordan en este tutorial cuyo formulación se basa en hello *sugerencia\_cantidad*:</span><span class="sxs-lookup"><span data-stu-id="b24c1-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="b24c1-123">**Clasificación binaria**: permite predecir si se pagó una propina tras una carrera, o no; es decir, un valor de *tip\_amount* mayor que 0 $ es un ejemplo positivo, mientras que un valor de *tip\_amount* de 0 $ es un ejemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="b24c1-124">**Clasificación multiclase**: intervalo de hello toopredict de cantidades de sugerencia de pago para recorridos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="b24c1-125">Se divide hello *sugerencia\_cantidad* en cinco bandejas o clases:</span><span class="sxs-lookup"><span data-stu-id="b24c1-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="b24c1-126">**Tarea de regresión**: cantidad de hello toopredict de sugerencia de Hola de pago para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="b24c1-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="b24c1-127"><a name="setup"></a>Configuración de un clúster de Hadoop de HDInsight para el análisis avanzado</span><span class="sxs-lookup"><span data-stu-id="b24c1-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-128">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-129">Puede configurar un entorno de Azure para análisis avanzado que emplee un clúster de HDInsight en tres pasos:</span><span class="sxs-lookup"><span data-stu-id="b24c1-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="b24c1-130">[Cree una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md): esta cuenta de almacenamiento se utiliza para almacenar datos en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="b24c1-131">datos de Hello usados en clústeres de HDInsight también se encuentran aquí.</span><span class="sxs-lookup"><span data-stu-id="b24c1-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="b24c1-132">[Personalizar Hadoop de HDInsight de Azure para hello de clústeres de proceso de análisis avanzado y la tecnología](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b24c1-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="b24c1-133">Este paso crea un clúster de Hadoop de HDInsight de Azure con Anaconda Python 2.7 de 64 bits instalado en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="b24c1-134">Hay dos tooremember pasos importantes al personalizar su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b24c1-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="b24c1-135">Recordar cuenta de almacenamiento de hello toolink creada en el paso 1 con el clúster de HDInsight al crearla.</span><span class="sxs-lookup"><span data-stu-id="b24c1-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="b24c1-136">Esta cuenta de almacenamiento es tooaccess usa datos que se procesan en los clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="b24c1-137">Después de crea el clúster de hello, habilitar el nodo principal de acceso remoto toohello de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="b24c1-138">Navegue toohello **configuración** ficha y haga clic en **habilitar de forma remota**.</span><span class="sxs-lookup"><span data-stu-id="b24c1-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="b24c1-139">Este paso especifica las credenciales de usuario de Hola utilizadas para inicio de sesión remoto.</span><span class="sxs-lookup"><span data-stu-id="b24c1-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="b24c1-140">[Crear un área de trabajo de aprendizaje automático de Azure](machine-learning-create-workspace.md): aprendizaje automático de Azure esta área de trabajo es los modelos de aprendizaje automático de toobuild usado.</span><span class="sxs-lookup"><span data-stu-id="b24c1-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="b24c1-141">Esta tarea se dirige después de completar una exploración de datos iniciales y hacia abajo de muestreo con clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="b24c1-142"><a name="getdata"></a>Obtener datos de Hola desde un origen público</span><span class="sxs-lookup"><span data-stu-id="b24c1-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-143">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-144">Hola tooget [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos desde su ubicación pública, puede usar cualquiera de los métodos de hello descritos en [tooand de mover los datos desde el almacenamiento de blobs de Azure](machine-learning-data-science-move-azure-blob.md) máquina tooyour de toocopy Hola datos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="b24c1-145">Aquí se describe cómo los archivos que contiene los datos de uso AzCopy tootransfer Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="b24c1-146">toodownload e instale AzCopy siguen las instrucciones de hello en [Introducción a la utilidad de línea de comandos de AzCopy hello](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b24c1-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="b24c1-147">Desde una ventana del símbolo del sistema, emitir Hola siguientes comandos de AzCopy, reemplazar *< path_to_data_folder >* con destino deseado de hello:</span><span class="sxs-lookup"><span data-stu-id="b24c1-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="b24c1-148">Cuando se completa la copia de hello, son un total de 24 archivos comprimidos en la carpeta de datos de hello seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b24c1-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="b24c1-149">Descomprima Hola descargan archivos toohello mismo directorio en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="b24c1-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="b24c1-150">Tome nota de carpeta Hola donde residen los archivos de hello sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="b24c1-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="b24c1-151">Esta carpeta será la que se hace referencia tooas Hola *< ruta de acceso\_a\_unzipped_data\_archivos\>*  es lo que sigue.</span><span class="sxs-lookup"><span data-stu-id="b24c1-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="b24c1-152"><a name="upload"></a>Cargar el contenedor de hello datos toohello predeterminado del clúster de Hadoop de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="b24c1-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-153">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-154">Hola siguientes comandos de AzCopy, reemplace Hola siguientes parámetros con valores reales de Hola que especificó al crear el clúster de Hadoop de Hola y descomprimir archivos de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="b24c1-155">***&#60; path_to_data_folder >*** directory hello (junto con la ruta de acceso) en el equipo que contienen archivos de datos de hello descomprimió</span><span class="sxs-lookup"><span data-stu-id="b24c1-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="b24c1-156">***&#60; nombre de cuenta de almacenamiento de clúster de Hadoop >*** Hola cuenta de almacenamiento asociada al clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="b24c1-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="b24c1-157">***&#60; contenedor predeterminado del clúster de Hadoop >*** contenedor de hello predeterminado utilizado por el clúster.</span><span class="sxs-lookup"><span data-stu-id="b24c1-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="b24c1-158">Tenga en cuenta que nombre hello predeterminado Hola contenedor suele ser Hola mismo nombre como el propio clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="b24c1-159">Por ejemplo, si el clúster de Hola se llama "abc123.azurehdinsight.net", contenedor predeterminado de hello es abc123.</span><span class="sxs-lookup"><span data-stu-id="b24c1-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="b24c1-160">***&#60; clave de la cuenta de almacenamiento >*** Hola clave Hola cuenta de almacenamiento utilizado por el clúster</span><span class="sxs-lookup"><span data-stu-id="b24c1-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="b24c1-161">Desde un símbolo del sistema o una ventana de Windows PowerShell en el equipo, ejecute hello siguiendo dos comandos de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b24c1-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="b24c1-162">Este comando carga los datos de ida y vuelta de hello demasiado***nyctaxitripraw*** directorio en el contenedor de predeterminado de hello del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="b24c1-163">Este comando carga los datos de la tarifa de hello demasiado***nyctaxifareraw*** directorio en el contenedor de predeterminado de hello del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="b24c1-164">datos de Hello ahora deberían en almacenamiento de blobs de Azure y listo toobe consumida en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="b24c1-165"><a name="#download-hql-files"></a>Inicie sesión en el nodo principal de Hola de clúster de Hadoop y y preparar para el análisis de exploración de datos</span><span class="sxs-lookup"><span data-stu-id="b24c1-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-166">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-167">tooaccess Hola del nodo principal del clúster de hello para el análisis de exploración de datos y hacia abajo de muestreo de datos de hello, siga procedimiento Hola descrito en [Hola de acceso principal del nodo de clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="b24c1-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="b24c1-168">En este tutorial, se usan principalmente las consultas escritas [Hive](https://hive.apache.org/), un lenguaje de consulta similar a SQL, exploraciones de datos preliminares de tooperform.</span><span class="sxs-lookup"><span data-stu-id="b24c1-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="b24c1-169">consultas de Hive Hola se almacenan en archivos de .hql.</span><span class="sxs-lookup"><span data-stu-id="b24c1-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="b24c1-170">A continuación, se abajo ejemplo este toobe de datos que se usan en aprendizaje automático de Azure para generar modelos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="b24c1-171">tooprepare el clúster de hello para el análisis de exploración de datos, se descargar archivos de .hql de Hola que contengan scripts de Hive relevantes de Hola de [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa directorio local (C:\temp) en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="b24c1-172">toodo, abra hello **símbolo** desde Hola nodo principal de Hola Hola de clúster y el problema siguiendo dos comandos:</span><span class="sxs-lookup"><span data-stu-id="b24c1-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="b24c1-173">Estos dos comandos descargarán todos los archivos de .hql necesarios en este directorio local de tutorial toohello ***C:\temp &#92;*** en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="b24c1-174"><a name="#hive-db-tables"></a>Creación de base de datos y tablas de Hive con particiones por mes</span><span class="sxs-lookup"><span data-stu-id="b24c1-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-175">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-176">Ahora estamos listos toocreate Hive tablas para el conjunto de datos de Nueva York taxi.</span><span class="sxs-lookup"><span data-stu-id="b24c1-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="b24c1-177">En el nodo principal de Hola de clúster de Hadoop de hello, abra hello ***línea de comandos de Hadoop*** en Hola escritorio del nodo principal de Hola y escriba el directorio del subárbol de hello escribiendo el comando de Hola</span><span class="sxs-lookup"><span data-stu-id="b24c1-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="b24c1-178">**Ejecutar todos los comandos de Hive en este tutorial de Hola por encima de la Papelera de Hive / símbolo del sistema de directorio. De esta manera, cualquier problema con la ruta de acceso se solucionará automáticamente. Usamos Hola términos "Prompt de directorio de Hive", "Hive bin / símbolo del sistema de directorio" y "línea de comandos de Hadoop" indistintamente en este tutorial.**</span><span class="sxs-lookup"><span data-stu-id="b24c1-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="b24c1-179">En el símbolo del sistema de hello subárbol de directorio, escriba Hola siguiente comando de línea de comandos de Hadoop de tablas y Hola nodo principal toosubmit Hola Hive consultar toocreate Hive base de datos:</span><span class="sxs-lookup"><span data-stu-id="b24c1-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="b24c1-180">Aquí es contenido de Hola de hello ***C:\temp\sample\_hive\_crear\_db\_y\_tables.hql*** archivos que crea la base de datos de Hive ***nyctaxidb *** y tablas ***recorridos*** y ***tarifa***.</span><span class="sxs-lookup"><span data-stu-id="b24c1-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="b24c1-181">Este script de Hive crea dos tablas:</span><span class="sxs-lookup"><span data-stu-id="b24c1-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="b24c1-182">tabla de "recorrido" Hello contiene detalles de ida y vuelta de cada carrera (detalles del controlador, hora de recopilación, distancia de viaje y veces)</span><span class="sxs-lookup"><span data-stu-id="b24c1-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="b24c1-183">tabla de "tarifa" Hello contiene los detalles de tarifa (cantidad de tarifa, cantidad de sugerencia, peajes y suplementos).</span><span class="sxs-lookup"><span data-stu-id="b24c1-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="b24c1-184">Si necesita ayuda adicional con estos procedimientos o quiere tooinvestigate otras alternativas, vea la sección de hello [consultas de Hive enviar directamente desde Hola línea de comandos de Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="b24c1-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="b24c1-185"><a name="#load-data"></a>Cargar las tablas de tooHive de datos con particiones</span><span class="sxs-lookup"><span data-stu-id="b24c1-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-186">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-187">el conjunto de datos de Hello NYC taxi tiene una partición natural por mes, lo que usamos tooenable tiempos de procesamiento y consulta más rápidos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="b24c1-188">Hola los siguientes comandos de PowerShell (emitidas desde el directorio de Hive de hello mediante hello **línea de comandos de Hadoop**) cargar datos toohello "recorrido" y "tarifa" Hive las tablas con particiones por mes.</span><span class="sxs-lookup"><span data-stu-id="b24c1-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="b24c1-189">Hola *ejemplo\_hive\_cargar\_datos\_por\_partitions.hql* archivo contiene siguiente hello **cargar** comandos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="b24c1-190">Tenga en cuenta que un número de consultas de Hive que aquí utilizamos en proceso de exploración de hello implica la búsqueda en una sola partición o en solo un par de particiones.</span><span class="sxs-lookup"><span data-stu-id="b24c1-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="b24c1-191">Pero estas consultas se pudieron ejecutar a través de los datos completos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="b24c1-192"><a name="#show-db"></a>Mostrar bases de datos en clúster de Hadoop de HDInsight de Hola</span><span class="sxs-lookup"><span data-stu-id="b24c1-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="b24c1-193">tooshow Hola bases de datos creadas en clúster de Hadoop de HDInsight dentro de la ventana de línea de comandos de Hadoop de hello, ejecute el siguiente comando de línea de comandos de Hadoop de Hola:</span><span class="sxs-lookup"><span data-stu-id="b24c1-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="b24c1-194"><a name="#show-tables"></a>Mostrar tablas de Hive de hello en la base de datos de hello nyctaxidb</span><span class="sxs-lookup"><span data-stu-id="b24c1-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="b24c1-195">tooshow Hola tablas hello nyctaxidb base de datos, ejecute el siguiente comando de línea de comandos de Hadoop de Hola:</span><span class="sxs-lookup"><span data-stu-id="b24c1-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="b24c1-196">Esto se puede confirmar que las tablas de hello tienen particiones emitiendo el comando de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="b24c1-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="b24c1-197">Hola espera el resultado se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="b24c1-197">hello expected output is shown below:</span></span>

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

<span data-ttu-id="b24c1-198">De igual forma, es posible asegurarse de que esa tabla de tarifa hello tiene particiones emitiendo el comando de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="b24c1-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="b24c1-199">Hola espera el resultado se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="b24c1-199">hello expected output is shown below:</span></span>

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

## <span data-ttu-id="b24c1-200"><a name="#explore-hive"></a>Exploración de datos e ingeniería de características en Hive</span><span class="sxs-lookup"><span data-stu-id="b24c1-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-201">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-202">Hola exploración de datos y la característica de tareas de ingeniería para hello datos cargados en tablas de Hive Hola pueden realizarse mediante consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="b24c1-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="b24c1-203">Estos son ejemplos de dichas tareas por que las que le guiaremos en esta sección:</span><span class="sxs-lookup"><span data-stu-id="b24c1-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="b24c1-204">Ver los registros de 10 principales de hello en ambas tablas.</span><span class="sxs-lookup"><span data-stu-id="b24c1-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="b24c1-205">Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="b24c1-206">Investigue la calidad de los datos de los campos de longitud y latitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="b24c1-207">Generar etiquetas de clasificación multiclase y binaria basándose en hello **sugerencia\_cantidad**.</span><span class="sxs-lookup"><span data-stu-id="b24c1-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="b24c1-208">Generar características y calcula las distancias Hola directa de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="b24c1-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="b24c1-209">Exploración: Vista Hola top 10 registros en el recorrido de tabla</span><span class="sxs-lookup"><span data-stu-id="b24c1-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-210">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-211">toosee aspecto qué datos hello, examinamos 10 registros de cada tabla.</span><span class="sxs-lookup"><span data-stu-id="b24c1-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="b24c1-212">Ejecute hello siguientes dos consultas por separado de símbolo del sistema de hello subárbol de directorio en los registros de hello línea de comandos de Hadoop consola tooinspect Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="b24c1-213">tooget Hola top 10 registros en la tabla de Hola "recorrido" de Hola y primer mes:</span><span class="sxs-lookup"><span data-stu-id="b24c1-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="b24c1-214">tooget Hola top 10 registros de hello tabla "tarifa" de hello primer mes:</span><span class="sxs-lookup"><span data-stu-id="b24c1-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="b24c1-215">A menudo es útil toosave Hola el archivo de tooa de registros para su visualización adecuada.</span><span class="sxs-lookup"><span data-stu-id="b24c1-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="b24c1-216">Un toohello pequeño cambio por encima de la consulta para hacerlo:</span><span class="sxs-lookup"><span data-stu-id="b24c1-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="b24c1-217">Exploración: Número de Hola vista de registros en cada uno de los 12 particiones de Hola</span><span class="sxs-lookup"><span data-stu-id="b24c1-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-218">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-219">Hola cómo varía el número de Hola de viajes de durante el año natural de hello es interesante.</span><span class="sxs-lookup"><span data-stu-id="b24c1-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="b24c1-220">Agrupar por mes nos permite toosee el aspecto de esta distribución de viajes.</span><span class="sxs-lookup"><span data-stu-id="b24c1-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="b24c1-221">Esto nos da salida de hello:</span><span class="sxs-lookup"><span data-stu-id="b24c1-221">This gives us hello output :</span></span>

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

<span data-ttu-id="b24c1-222">En este caso, Hola primera columna es el mes de Hola y Hola en segundo lugar es número Hola de viajes de durante ese mes.</span><span class="sxs-lookup"><span data-stu-id="b24c1-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="b24c1-223">Se podemos contar Hola número total de registros en nuestro conjunto de datos de ida y vuelta mediante la emisión de hello siguiente comando en el símbolo del sistema de hello subárbol de directorio.</span><span class="sxs-lookup"><span data-stu-id="b24c1-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="b24c1-224">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="b24c1-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="b24c1-225">Comandos toothose similar que se muestra para el conjunto de datos de ida y vuelta de hello, podemos emitir consultas de Hive de hello Hive directory pedir Hola tarifa datos toovalidate Hola número establecido de registros.</span><span class="sxs-lookup"><span data-stu-id="b24c1-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="b24c1-226">Esto nos da salida de hello:</span><span class="sxs-lookup"><span data-stu-id="b24c1-226">This gives us hello output:</span></span>

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

<span data-ttu-id="b24c1-227">Tenga en cuenta que Hola exacta mismo número de viajes por mes se devuelve para los dos conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="b24c1-228">Esto proporciona la validación primera Hola ese Hola datos se han cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="b24c1-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="b24c1-229">Contando Hola número total de registros en el conjunto de datos de tarifa de hello puede realizarse con el comando de Hola a continuación del símbolo del sistema de hello subárbol de directorio:</span><span class="sxs-lookup"><span data-stu-id="b24c1-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="b24c1-230">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="b24c1-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="b24c1-231">número total de Hola de registros en ambas tablas también se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="b24c1-232">Esto proporciona una validación segundo ese Hola datos se han cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="b24c1-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="b24c1-233">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="b24c1-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-234">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-235">Este ejemplo identifica medallion Hola (números de taxi) con más de 100 viajes dentro de un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="b24c1-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="b24c1-236">ventajas de la consulta de Hola de hello partición acceso a la tabla porque está condicionado por la variable de la partición de hello **mes**.</span><span class="sxs-lookup"><span data-stu-id="b24c1-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="b24c1-237">resultados de la consulta de Hola se escriben tooa archivo local queryoutput.tsv `C:\temp` en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="b24c1-238">Aquí es contenido de Hola de *ejemplo\_hive\_recorridos\_recuento\_por\_medallion.hql* archivo para su inspección.</span><span class="sxs-lookup"><span data-stu-id="b24c1-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="b24c1-239">medallion Hola Hola NYC taxi conjunto de datos identifica un único archivo cab.</span><span class="sxs-lookup"><span data-stu-id="b24c1-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="b24c1-240">Se puede identificar qué taxis trabajan más preguntando cuáles realizaron más de un determinado número de carreras en un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="b24c1-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="b24c1-241">Hello en el ejemplo siguiente se identifica archivos CAB que realizan viajes de más de cien en hello primeros tres meses y guarda Hola resultados tooa local archivo de consulta C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="b24c1-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="b24c1-242">Aquí es contenido de Hola de *ejemplo\_hive\_recorridos\_recuento\_por\_medallion.hql* archivo para su inspección.</span><span class="sxs-lookup"><span data-stu-id="b24c1-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="b24c1-243">De hello subárbol símbolo del sistema de directorio, problema Hola comando a continuación:</span><span class="sxs-lookup"><span data-stu-id="b24c1-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="b24c1-244">Exploración: distribución de carreras por medallion y hack_license</span><span class="sxs-lookup"><span data-stu-id="b24c1-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-245">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-246">Al explorar un conjunto de datos, con frecuencia se requiere número de hello tooexamine de co-repeticiones de grupos de valores.</span><span class="sxs-lookup"><span data-stu-id="b24c1-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="b24c1-247">En esta sección se proporcionan un ejemplo de cómo toodo esto en archivos .cab y controladores.</span><span class="sxs-lookup"><span data-stu-id="b24c1-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="b24c1-248">Hola *ejemplo\_hive\_recorridos\_recuento\_por\_medallion\_license.hql* archivo agrupa los datos de la tarifa de hello establecida en "medallion" y "hack_license" y devuelve recuentos de cada combinación.</span><span class="sxs-lookup"><span data-stu-id="b24c1-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="b24c1-249">A continuación se muestra su contenido.</span><span class="sxs-lookup"><span data-stu-id="b24c1-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="b24c1-250">Esta consulta devuelve combinaciones de taxi y conductor determinado ordenadas por número descendente de carreras.</span><span class="sxs-lookup"><span data-stu-id="b24c1-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="b24c1-251">De hello Hive indicador del directorio, ejecute:</span><span class="sxs-lookup"><span data-stu-id="b24c1-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="b24c1-252">resultados de la consulta de Hola se escriben archivo local tooa C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="b24c1-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="b24c1-253">Exploración: Evaluación de la calidad de los datos mediante la comprobación de registros con latitud/longitud no válida</span><span class="sxs-lookup"><span data-stu-id="b24c1-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-254">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-255">Un objetivo comunes de análisis de exploración de datos es tooweed los registros no válidos o es incorrectos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="b24c1-256">Hello ejemplo de esta sección determina si bien hello campos de longitud o latitud contienen un valor fuera del área de Nueva York Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="b24c1-257">Puesto que es probable que estos registros tengan los valores de longitud y latitud erróneos, queremos tooeliminate de cualquier dato que sea toobe utilizados para el modelado.</span><span class="sxs-lookup"><span data-stu-id="b24c1-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="b24c1-258">Este es el contenido de Hola de *ejemplo\_hive\_calidad\_assessment.hql* archivo para su inspección.</span><span class="sxs-lookup"><span data-stu-id="b24c1-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="b24c1-259">De hello Hive indicador del directorio, ejecute:</span><span class="sxs-lookup"><span data-stu-id="b24c1-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="b24c1-260">Hola *-S* argumento incluido en este comando suprime la copia impresa de pantalla del estado de Hola de trabajos de Hive asignación y reducción de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="b24c1-261">Esto es útil porque dificulta la impresión de la pantalla de Hola de hello Hive resultado de la consulta sea más legible.</span><span class="sxs-lookup"><span data-stu-id="b24c1-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="b24c1-262">Exploración: Distribuciones de clase binaria de las propinas de las carreras</span><span class="sxs-lookup"><span data-stu-id="b24c1-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-263">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-264">Problema de clasificación binaria de hello descrito en hello [ejemplos de tareas de predicción](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sección, resulta útil tooknow si se proporcionó una sugerencia o no.</span><span class="sxs-lookup"><span data-stu-id="b24c1-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="b24c1-265">Esta distribución de las propinas es binaria:</span><span class="sxs-lookup"><span data-stu-id="b24c1-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="b24c1-266">Propina dada (clase 1, tip\_amount > 0 $).</span><span class="sxs-lookup"><span data-stu-id="b24c1-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="b24c1-267">Sin propina (clase 0, tip\_amount = 0 $).</span><span class="sxs-lookup"><span data-stu-id="b24c1-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="b24c1-268">Hola *ejemplo\_hive\_superpuesto\_frequencies.hql* archivo se muestra a continuación para ello.</span><span class="sxs-lookup"><span data-stu-id="b24c1-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="b24c1-269">De hello Hive indicador del directorio, ejecute:</span><span class="sxs-lookup"><span data-stu-id="b24c1-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="b24c1-270">Exploración: Clase distribuciones en configuración de hello multiclase</span><span class="sxs-lookup"><span data-stu-id="b24c1-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-271">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-272">Problema de clasificación multiclase Hola descrito en hello [ejemplos de tareas de predicción](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sección este conjunto de datos también se presta tooa clasificación natural que nos gustaría toopredict cantidad de Hola de sugerencias de hello dada.</span><span class="sxs-lookup"><span data-stu-id="b24c1-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="b24c1-273">Podemos usar ubicaciones toodefine sugerencia intervalos de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="b24c1-274">tooget Hola distribuciones de clase de hello distintos intervalos de sugerencia, usaremos hello *ejemplo\_hive\_sugerencia\_intervalo\_frequencies.hql* archivo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="b24c1-275">A continuación se muestra su contenido.</span><span class="sxs-lookup"><span data-stu-id="b24c1-275">Below are its contents.</span></span>

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

<span data-ttu-id="b24c1-276">Ejecute el siguiente comando desde la consola de línea de comandos de Hadoop de hello:</span><span class="sxs-lookup"><span data-stu-id="b24c1-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="b24c1-277">Exploración: Cálculo de la distancia directa entre dos ubicaciones de longitud y latitud de proceso</span><span class="sxs-lookup"><span data-stu-id="b24c1-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-278">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-279">Tener una medida de distancia directa Hola nos permite toofind out discrepancia de hello entre él y Hola real distancia de viaje.</span><span class="sxs-lookup"><span data-stu-id="b24c1-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="b24c1-280">Esta característica se promoverá, señale que pasajeros pueden ser menor probable información sobre herramientas si pueda determinar dicho controlador Hola intencionadamente las ha tomado por una ruta más larga.</span><span class="sxs-lookup"><span data-stu-id="b24c1-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="b24c1-281">comparación de hello toosee entre hello y distancia de viaje real [distancia Haversine](http://en.wikipedia.org/wiki/Haversine_formula) entre dos puntos longitud-latitud (distancia de Hola "great círculo"), usamos funciones trigonométricas de hello disponibles dentro de Hive, por lo tanto:</span><span class="sxs-lookup"><span data-stu-id="b24c1-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="b24c1-282">En la consulta de hello anterior, R es el radio Hola Hola tierra en millas y pi es tooradians convertido.</span><span class="sxs-lookup"><span data-stu-id="b24c1-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="b24c1-283">Tenga en cuenta que puntos longitud-latitud de hello tooremove "filtrado" valores que están lejos de área de Nueva York Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="b24c1-284">En este caso, escribimos nuestro directorio de tooa de resultados llamado "queryoutputdir".</span><span class="sxs-lookup"><span data-stu-id="b24c1-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="b24c1-285">Hello secuencia de comandos que se muestra a continuación, primero crea este directorio de salida y, a continuación, ejecuta el comando de Hive de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="b24c1-286">De hello Hive indicador del directorio, ejecute:</span><span class="sxs-lookup"><span data-stu-id="b24c1-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="b24c1-287">Hello resultados de la consulta se escriben los blobs de Azure too9 ***queryoutputdir/000000\_0*** demasiado ***queryoutputdir/000008\_0*** en contenedor de hello predeterminado del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="b24c1-288">tamaño de hello toosee de blobs individuales de hello, ejecutamos Hola siguiente comando desde el símbolo del sistema de hello subárbol de directorio:</span><span class="sxs-lookup"><span data-stu-id="b24c1-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="b24c1-289">contenido de hello toosee de un archivo determinado, diga 000000\_0, usamos de Hadoop `copyToLocal` comando, por lo tanto.</span><span class="sxs-lookup"><span data-stu-id="b24c1-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="b24c1-290">`copyToLocal` puede ser muy lento para archivos de gran tamaño y no se recomienda para su uso con ellos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="b24c1-291">Una ventaja clave de tener estos datos residen en un blob de Azure es que podemos exploramos datos hello en aprendizaje automático de Azure con hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="b24c1-292"><a name="#downsample"></a>Reducción de datos y creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b24c1-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="b24c1-293">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="b24c1-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="b24c1-294">Después de la fase de análisis de datos de exploración de hello, ahora estamos listos toodown datos de Hola de ejemplo para generar modelos de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="b24c1-295">En esta sección, se muestra cómo consultar los datos de toodown ejemplo hello, que, a continuación, se obtiene acceso desde hello toouse un subárbol [importar datos] [ import-data] módulo aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="b24c1-296">Profundidad de muestreo de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="b24c1-296">Down sampling hello data</span></span>
<span data-ttu-id="b24c1-297">Este procedimiento incluye dos pasos.</span><span class="sxs-lookup"><span data-stu-id="b24c1-297">There are two steps in this procedure.</span></span> <span data-ttu-id="b24c1-298">En primer lugar se unir hello **nyctaxidb.trip** y **nyctaxidb.fare** tablas en tres claves que están presentes en todos los registros: "medallion", "hack\_licencia", y "recogida\_datetime".</span><span class="sxs-lookup"><span data-stu-id="b24c1-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="b24c1-299">Después se genera una etiqueta de clasificación binaria **tipped** y una etiqueta de clasificación de múltiples clases **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="b24c1-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="b24c1-300">toobe toouse capaz de hello hacia abajo de los datos muestreados directamente desde hello [importar datos] [ import-data] módulo aprendizaje automático de Azure, es necesario toostore resultados de Hola de hello por encima de la tabla de Hive interno de consulta tooan.</span><span class="sxs-lookup"><span data-stu-id="b24c1-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="b24c1-301">En la información siguiente, se crea una tabla interna de Hive y rellena su contenido con hello Unido y hacia abajo de los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="b24c1-302">consulta Hello aplica funciones de Hive estándares directamente toogenerate hora Hola del día, semana del año, semana (el lunes es 1 y 7 es el domingo) de Hola "recogida\_datetime" campo y Hola distancia directa entre la recogida de Hola y caída ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="b24c1-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="b24c1-303">Los usuarios pueden consultar demasiado[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) para obtener una lista completa de dichas funciones.</span><span class="sxs-lookup"><span data-stu-id="b24c1-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="b24c1-304">Hola consulta, a continuación, el detalle de datos de saludo de ejemplos para que los resultados de la consulta de hello pueden caber en hello estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="b24c1-305">Se importa solo 1% del conjunto de datos original de Hola Hola Studio.</span><span class="sxs-lookup"><span data-stu-id="b24c1-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="b24c1-306">A continuación se muestran contenido Hola de *ejemplo\_hive\_preparar\_para\_aml\_full.hql* archivo que prepara los datos para el modelo de creación de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

<span data-ttu-id="b24c1-307">Esta consulta, del directorio del subárbol de hello solicitar al toorun:</span><span class="sxs-lookup"><span data-stu-id="b24c1-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="b24c1-308">Ahora tenemos una tabla interna "nyctaxidb.nyctaxi_downsampled_dataset", que se puede acceder mediante hello [importar datos] [ import-data] módulo de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="b24c1-309">También se puede utilizar este conjunto de datos para generar modelos de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="b24c1-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="b24c1-310">Usar módulo de importar datos de Hola Hola de aprendizaje automático de Azure tooaccess hacia abajo de los datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b24c1-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="b24c1-311">Como requisitos previos para emitir consultas de Hive en hello [importar datos] [ import-data] módulo de aprendizaje automático de Azure, se necesita acceso de área de trabajo de aprendizaje automático de Azure tooan y tener acceso a las credenciales de toohello de hello clúster y su cuenta de almacenamiento asociada.</span><span class="sxs-lookup"><span data-stu-id="b24c1-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="b24c1-312">Algunos detalles de hello [importar datos] [ import-data] hello y módulo tooinput de parámetros:</span><span class="sxs-lookup"><span data-stu-id="b24c1-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="b24c1-313">**URI del servidor de HCatalog**: si el nombre del clúster de hello es abc123, esto es simplemente: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="b24c1-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="b24c1-314">**Nombre de cuenta de usuario de Hadoop** : nombre de usuario de hello elegido para el clúster de hello (**no** nombre de usuario de acceso remoto de hello)</span><span class="sxs-lookup"><span data-stu-id="b24c1-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="b24c1-315">**Contraseña de cuenta de usuario de Hadoop** : contraseña de hello elegido para el clúster de hello (**no** contraseña de acceso remoto de hello)</span><span class="sxs-lookup"><span data-stu-id="b24c1-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="b24c1-316">**Ubicación de los datos de salida** : Esto se elige toobe Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="b24c1-317">**Nombre de la cuenta de almacenamiento de Azure** : nombre de cuenta de almacenamiento predeterminada de hello asociada Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="b24c1-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="b24c1-318">**Nombre de contenedor de Azure** : Esto es nombre de contenedor predeterminado de Hola para clúster hello y normalmente es Hola mismo como el nombre del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="b24c1-319">En un clúster denominado "abc123", es abc123.</span><span class="sxs-lookup"><span data-stu-id="b24c1-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b24c1-320">**Cualquier tabla deseamos tooquery con hello [importar datos] [ import-data] módulo aprendizaje automático de Azure debe ser una tabla interna.**</span><span class="sxs-lookup"><span data-stu-id="b24c1-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="b24c1-321">Una manera de determinar si una tabla T en una base de datos D.db es una tabla interna es la siguiente.</span><span class="sxs-lookup"><span data-stu-id="b24c1-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="b24c1-322">De hello subárbol símbolo del sistema de directorio, problema Hola comando:</span><span class="sxs-lookup"><span data-stu-id="b24c1-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="b24c1-323">Si la tabla de hello es una tabla interna y se rellena, su contenido debe mostrar aquí.</span><span class="sxs-lookup"><span data-stu-id="b24c1-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="b24c1-324">Otro toodetermine de manera que si una tabla es una tabla interna es toouse Hola Explorador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="b24c1-325">Usar nombre del contenedor predeterminado toonavigate toohello de clúster de Hola y, a continuación, filtrar por nombre de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="b24c1-326">Si la tabla de Hola y su contenido se muestra, Esto confirma que es una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="b24c1-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="b24c1-327">Ésta es una instantánea de la consulta de Hive de Hola y Hola [importar datos] [ import-data] módulo:</span><span class="sxs-lookup"><span data-stu-id="b24c1-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Consulta de Hive para el módulo de importación de datos](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="b24c1-329">Tenga en cuenta que desde nuestro abajo los datos muestreados residen en el contenedor predeterminado de hello, consulta de Hive resultante Hola de aprendizaje automático de Azure es muy simple y es un "seleccionar * de nyctaxidb.nyctaxi\_reduce\_datos".</span><span class="sxs-lookup"><span data-stu-id="b24c1-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="b24c1-330">conjunto de datos de Hello ahora puede utilizarse como punto de partida para generar modelos de aprendizaje automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="b24c1-331"><a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b24c1-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="b24c1-332">Ahora estamos tooproceed capaz de toomodel creación e implementación de modelo en [aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="b24c1-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="b24c1-333">Hola datos están listos para que podamos toouse para resolver problemas de predicción de hello arriba indicados:</span><span class="sxs-lookup"><span data-stu-id="b24c1-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="b24c1-334">**1. Clasificación binaria**: toopredict o no se pagó una sugerencia para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="b24c1-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="b24c1-335">**Lector usado** : regresión logística de dos clases</span><span class="sxs-lookup"><span data-stu-id="b24c1-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="b24c1-336">a.</span><span class="sxs-lookup"><span data-stu-id="b24c1-336">a.</span></span> <span data-ttu-id="b24c1-337">En este problema la etiqueta de destino (o clase) es "tipped".</span><span class="sxs-lookup"><span data-stu-id="b24c1-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="b24c1-338">El conjunto de datos reducido original incluye algunas columnas que no contienen datos para el experimento de clasificación.</span><span class="sxs-lookup"><span data-stu-id="b24c1-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="b24c1-339">En concreto: sugerencia\_de clases, sugerencia\_cantidad y total\_importe revelar información acerca de la etiqueta de destino de Hola que no está disponible en el tiempo de prueba.</span><span class="sxs-lookup"><span data-stu-id="b24c1-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="b24c1-340">Se quite estas columnas de cuenta con hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="b24c1-341">en la instantánea de Hola a continuación se muestra nuestra toopredict experimento o no se pagó una sugerencia para un recorrido dado.</span><span class="sxs-lookup"><span data-stu-id="b24c1-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="b24c1-343">b.</span><span class="sxs-lookup"><span data-stu-id="b24c1-343">b.</span></span> <span data-ttu-id="b24c1-344">En este experimento las distribuciones de la etiqueta de destino eran aproximadamente 1:1.</span><span class="sxs-lookup"><span data-stu-id="b24c1-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="b24c1-345">instantánea de Hello siguiente muestra la distribución de Hola de las etiquetas de clase de sugerencia de problema de clasificación binaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![Distribución de las etiquetas de clase de sugerencia](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="b24c1-347">Como resultado, obtenemos un AUC de 0.987 tal y como se muestra en la siguiente ilustración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![Valor de AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="b24c1-349">**2. Clasificación multiclase**: las clases definidas por el intervalo de hello toopredict de cantidades de sugerencia de pago de ida y vuelta hello, utilizaba anteriormente Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="b24c1-350">**Lector usado** : regresión logística de múltiples clases</span><span class="sxs-lookup"><span data-stu-id="b24c1-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="b24c1-351">a.</span><span class="sxs-lookup"><span data-stu-id="b24c1-351">a.</span></span> <span data-ttu-id="b24c1-352">En este problema, la etiqueta de destino (o clase) es "tip\_class", que puede adoptar uno de cinco valores (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="b24c1-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="b24c1-353">Como en el caso de clasificación binaria de hello, tenemos unas pocas columnas que son las pérdidas de destino para este experimento.</span><span class="sxs-lookup"><span data-stu-id="b24c1-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="b24c1-354">En concreto: superpuesto, sugerencia\_importe total\_importe revelar información acerca de la etiqueta de destino de Hola que no está disponible en el tiempo de prueba.</span><span class="sxs-lookup"><span data-stu-id="b24c1-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="b24c1-355">Quitamos estas columnas con hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="b24c1-356">Hola instantánea siguiente muestra nuestra toopredict experimento en qué bin una sugerencia es probable toofall (clase 0: sugerencia = $0, 1 de la clase: Sugerencia > $0 y sugerencia < = $5, clase 2: Sugerencia > $5 y en la sugerencia < = $10, 3 de la clase: Sugerencia > $10 y en la sugerencia < = 20 $ Clase 4: Sugerencia > $20)</span><span class="sxs-lookup"><span data-stu-id="b24c1-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="b24c1-358">Ahora vemos qué aspecto tiene nuestra distribución de clases de prueba real.</span><span class="sxs-lookup"><span data-stu-id="b24c1-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="b24c1-359">Vemos que aunque clase 0 y 1 de la clase son muy extendido, hello otras clases son poco frecuentes.</span><span class="sxs-lookup"><span data-stu-id="b24c1-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Distribución de la clase de prueba](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="b24c1-361">b.</span><span class="sxs-lookup"><span data-stu-id="b24c1-361">b.</span></span> <span data-ttu-id="b24c1-362">Para este experimento, usamos un toolook de matriz de confusión en nuestro precisiones de predicción.</span><span class="sxs-lookup"><span data-stu-id="b24c1-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="b24c1-363">Esto se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b24c1-363">This is shown below.</span></span>

![Matriz de confusión](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="b24c1-365">Tenga en cuenta que mientras nuestro precisiones de clase en clases de hello frecuente es bastante bueno, modelo hello no hacer un buen trabajo de "aprendizaje" en las clases de hello poco frecuentes.</span><span class="sxs-lookup"><span data-stu-id="b24c1-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="b24c1-366">**3. Tarea de regresión**: cantidad de hello toopredict de sugerencia de pago para un recorrido.</span><span class="sxs-lookup"><span data-stu-id="b24c1-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="b24c1-367">**Lector usado** : árbol de decisión incrementado</span><span class="sxs-lookup"><span data-stu-id="b24c1-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="b24c1-368">a.</span><span class="sxs-lookup"><span data-stu-id="b24c1-368">a.</span></span> <span data-ttu-id="b24c1-369">En este problema la etiqueta de destino (o clase) es "tip\_amount".</span><span class="sxs-lookup"><span data-stu-id="b24c1-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="b24c1-370">En este caso son nuestra pérdidas de destino: superpuesto, sugerencia\_(clase), total\_cantidad; todas estas variables revelar información acerca de la cantidad de sugerencia de Hola que no está disponible normalmente en el tiempo de prueba.</span><span class="sxs-lookup"><span data-stu-id="b24c1-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="b24c1-371">Quitamos estas columnas con hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="b24c1-372">Hola instantánea belows muestra nuestra cantidad de Hola de toopredict de experimento de hello dada la sugerencia.</span><span class="sxs-lookup"><span data-stu-id="b24c1-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="b24c1-374">b.</span><span class="sxs-lookup"><span data-stu-id="b24c1-374">b.</span></span> <span data-ttu-id="b24c1-375">Para los problemas de regresión, se medir precisiones Hola de nuestro predicción examinando error Hola cuadrado en predicciones hello, Hola coeficiente de determinación y Hola como.</span><span class="sxs-lookup"><span data-stu-id="b24c1-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="b24c1-376">Lo mostramos a continuación.</span><span class="sxs-lookup"><span data-stu-id="b24c1-376">We show these below.</span></span>

![Estadísticas de predicción](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="b24c1-378">Vemos que sobre Hola coeficiente de determinación es 0.709, lo que implica aproximadamente el 71% de variación de Hola se explica por nuestro coeficientes de modelo.</span><span class="sxs-lookup"><span data-stu-id="b24c1-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b24c1-379">toolearn más información acerca de aprendizaje automático de Azure y cómo tooaccess y usarla, consulte demasiado[¿qué es aprendizaje automático?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="b24c1-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="b24c1-380">Un recurso muy útil para reproducir con un montón de experimentos de aprendizaje automático en aprendizaje automático de Azure es hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="b24c1-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="b24c1-381">Galería de Hello cubre una gama de experimentos y proporciona una introducción completa a intervalo de Hola de capacidades de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="b24c1-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="b24c1-382">Información de licencia</span><span class="sxs-lookup"><span data-stu-id="b24c1-382">License Information</span></span>
<span data-ttu-id="b24c1-383">En este tutorial de ejemplo y sus secuencias de comandos que lo acompaña se comparten entre Microsoft bajo licencia MIT de Hola.</span><span class="sxs-lookup"><span data-stu-id="b24c1-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="b24c1-384">Compruebe archivo LICENSE.txt de hello directorio de hello del código de ejemplo de Hola en GitHub para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="b24c1-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="b24c1-385">Referencias</span><span class="sxs-lookup"><span data-stu-id="b24c1-385">References</span></span>
<span data-ttu-id="b24c1-386">•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="b24c1-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="b24c1-387">•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="b24c1-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="b24c1-388">•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="b24c1-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
