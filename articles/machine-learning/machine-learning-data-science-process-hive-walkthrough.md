---
title: "Exploración de datos en un clúster de Hadoop y creación de modelos en Azure Machine Learning | Microsoft Docs"
description: "Uso del proceso de ciencia de datos en equipos para un escenario completo que emplea un clúster de Hadoop de HDInsight con el objetivo de compilar e implementar un modelo con un conjunto de datos disponible públicamente"
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
ms.openlocfilehash: e48d59ca467e3e7fd772389e6e48a2d81726f859
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="e7a97-103">Proceso de ciencia de datos en equipos en acción: uso de clústeres de Hadoop de Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7a97-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="e7a97-104">En este tutorial se describe cómo utilizar el [proceso de ciencia de datos en equipos (TDSP)](data-science-process-overview.md) en un escenario completo con un clúster de [Hadoop de HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/) para almacenar, explorar y diseñar características de los datos del conjunto de datos de [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) disponible públicamente, así como para reducir el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span></span> <span data-ttu-id="e7a97-105">Los modelos de datos se generan mediante Aprendizaje automático de Azure para controlar las tareas predictivas de clasificación binaria y de clases múltiples, y de regresión.</span><span class="sxs-lookup"><span data-stu-id="e7a97-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="e7a97-106">Para acceder a un tutorial que muestra cómo controlar un conjunto de datos de mayor tamaño (1 terabyte) para un escenario similar con clústeres de Hadoop de HDInsight para el procesamiento de datos, consulte [Proceso de ciencia de datos en equipos en acción: uso de clústeres de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e7a97-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="e7a97-107">También es posible utilizar un cuaderno de iPython para realizar las tareas que se presentan en este tutorial con el conjunto de datos de 1 TB.</span><span class="sxs-lookup"><span data-stu-id="e7a97-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span></span> <span data-ttu-id="e7a97-108">Los usuarios que deseen probar este método deben consultar el tema sobre el [tutorial de Criteo con una conexión de ODBC de Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) .</span><span class="sxs-lookup"><span data-stu-id="e7a97-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="e7a97-109"><a name="dataset"></a>Descripción del conjunto de datos NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="e7a97-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="e7a97-110">Los datos de carreras de taxi de Nueva York son aproximadamente 20 GB de archivos comprimidos de valores separados por comas (CSV) (~48 GB sin comprimir), que incluyen más de 173 millones de carreras individuales y las tarifas pagadas por cada carrera.</span><span class="sxs-lookup"><span data-stu-id="e7a97-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="e7a97-111">Cada registro de carrera incluye la hora y la ubicación de recogida y de entrega, el número de licencia de (del conductor) anónimo y el número de ida y vuelta incluye la ubicación de entrega y recogida y el tiempo, la número de licencia y el número de identificador único del taxi.</span><span class="sxs-lookup"><span data-stu-id="e7a97-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="e7a97-112">Los datos cubren todos los viajes del año 2013 y se proporcionan en los dos conjuntos de datos siguientes para cada mes:</span><span class="sxs-lookup"><span data-stu-id="e7a97-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="e7a97-113">Los archivos CSV 'trip_data' contienen información detallada de las carreras, como el número de pasajeros, los puntos de recogida y destino, la duración de las carreras y la longitud del recorrido.</span><span class="sxs-lookup"><span data-stu-id="e7a97-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e7a97-114">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7a97-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="e7a97-115">Los archivos CSV 'trip_fare' contienen información detallada de la tarifa que se paga en cada carrera, como el tipo de pago, el importe de la tarifa, los suplementos e impuestos, las propinas y peajes, y el importe total pagado.</span><span class="sxs-lookup"><span data-stu-id="e7a97-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="e7a97-116">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7a97-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e7a97-117">La clave única para unir trip\_data and trip\_fare se compone de los campos: medallion, hack\_licence and pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="e7a97-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="e7a97-118">Para obtener todos los detalles correspondientes a una carrera concreta, es suficiente combinar tres claves: "medallion", "hack\_license" and "pickup\_datetime".</span><span class="sxs-lookup"><span data-stu-id="e7a97-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="e7a97-119">Se describen detalles adicionales de los datos al almacenarlos en tablas de Hive un poco más adelante.</span><span class="sxs-lookup"><span data-stu-id="e7a97-119">We describe some more details of the data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="e7a97-120"><a name="mltasks"></a>Ejemplos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="e7a97-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="e7a97-121">Al trabajar con datos, determinar el tipo de predicciones que desea realizar en función de su análisis ayuda a aclarar las tareas que necesitará incluir en el proceso.</span><span class="sxs-lookup"><span data-stu-id="e7a97-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span></span>
<span data-ttu-id="e7a97-122">A continuación presentamos tres ejemplos de problemas de predicción que abordaremos en este tutorial cuya formulación se basa en el importe de la propina, *tip\_amount*:</span><span class="sxs-lookup"><span data-stu-id="e7a97-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span></span>

1. <span data-ttu-id="e7a97-123">**Clasificación binaria**: permite predecir si se pagó una propina tras una carrera, o no; es decir, un valor de *tip\_amount* mayor que 0 $ es un ejemplo positivo, mientras que un valor de *tip\_amount* de 0 $ es un ejemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="e7a97-124">**Clasificación con múltiples clases**: permite predecir el rango de importes de propina pagados por la carrera.</span><span class="sxs-lookup"><span data-stu-id="e7a97-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="e7a97-125">Dividimos *tip\_amount* en cinco ubicaciones o clases:</span><span class="sxs-lookup"><span data-stu-id="e7a97-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="e7a97-126">**Tarea de regresión**: permite predecir el importe pagado como propina en una carrera.</span><span class="sxs-lookup"><span data-stu-id="e7a97-126">**Regression task**: To predict the amount of the tip paid for a trip.</span></span>  

## <span data-ttu-id="e7a97-127"><a name="setup"></a>Configuración de un clúster de Hadoop de HDInsight para el análisis avanzado</span><span class="sxs-lookup"><span data-stu-id="e7a97-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-128">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-129">Puede configurar un entorno de Azure para análisis avanzado que emplee un clúster de HDInsight en tres pasos:</span><span class="sxs-lookup"><span data-stu-id="e7a97-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="e7a97-130">[Cree una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md): esta cuenta de almacenamiento se utiliza para almacenar datos en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a97-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="e7a97-131">Los datos utilizados en los clústeres de HDInsight también se encuentran aquí.</span><span class="sxs-lookup"><span data-stu-id="e7a97-131">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="e7a97-132">[Personalice los clústeres de Hadoop de HDInsight de Azure para la tecnología y procesos de análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e7a97-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="e7a97-133">Este paso crea un clúster de Hadoop de HDInsight de Azure con Anaconda Python 2.7 de 64 bits instalado en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="e7a97-134">Hay dos pasos importantes que debe recordar al personalizar el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7a97-134">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="e7a97-135">Recuerde vincular la cuenta de almacenamiento que creó en el paso 1 con el clúster de HDInsight en el momento de crearlo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="e7a97-136">Esta cuenta de almacenamiento se utiliza para tener acceso a datos que se procesan en el clúster.</span><span class="sxs-lookup"><span data-stu-id="e7a97-136">This storage account is used to access data that is processed within the cluster.</span></span>
   * <span data-ttu-id="e7a97-137">Después de crear el clúster, debe habilitar el acceso remoto a su nodo principal.</span><span class="sxs-lookup"><span data-stu-id="e7a97-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="e7a97-138">Navegue hasta la pestaña **Configuración** y haga clic en **Habilitar de forma remota**.</span><span class="sxs-lookup"><span data-stu-id="e7a97-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="e7a97-139">Este paso especifica las credenciales de usuario usadas para el inicio de sesión remoto.</span><span class="sxs-lookup"><span data-stu-id="e7a97-139">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="e7a97-140">[Cree un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md): esta área de trabajo se usa para crear modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="e7a97-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span></span> <span data-ttu-id="e7a97-141">Esta tarea se lleva a cabo después de completar una exploración inicial de los datos y de reducir su tamaño con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7a97-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span></span>

## <span data-ttu-id="e7a97-142"><a name="getdata"></a>Obtención de los datos desde un origen público</span><span class="sxs-lookup"><span data-stu-id="e7a97-142"><a name="getdata"></a>Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-143">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-144">Para obtener el conjunto de datos [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) de su ubicación pública, puede usar cualquiera de los métodos descritos en [Mover datos hacia y desde el almacenamiento de blobs de Azure](machine-learning-data-science-move-azure-blob.md) para copiar los datos en su máquina.</span><span class="sxs-lookup"><span data-stu-id="e7a97-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span></span>

<span data-ttu-id="e7a97-145">Aquí se describe cómo utilizar AzCopy para transferir los archivos que contienen datos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-145">Here we describe how use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="e7a97-146">Para descargar e instalar AzCopy, siga las indicaciones de [Introducción a la utilidad de línea de comandos AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="e7a97-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="e7a97-147">Desde una ventana de símbolo del sistema, emita los siguientes comandos de AzCopy, reemplazando *<ruta_a_carpeta_datos>* con el destino deseado:</span><span class="sxs-lookup"><span data-stu-id="e7a97-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="e7a97-148">Cuando se completa la copia, la carpeta de datos elegida contiene un total de 24 archivos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span></span> <span data-ttu-id="e7a97-149">Descomprima los archivos descargados en el mismo directorio del equipo local.</span><span class="sxs-lookup"><span data-stu-id="e7a97-149">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="e7a97-150">Tome nota de la carpeta donde se encuentran los archivos sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="e7a97-150">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="e7a97-151">Se hará referencia a esta carpeta como *<path\_to\_unzipped_data\_files\>* en lo que sigue.</span><span class="sxs-lookup"><span data-stu-id="e7a97-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="e7a97-152"><a name="upload"></a>Carga de los datos en el contenedor predeterminado del clúster de Hadoop de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e7a97-152"><a name="upload"></a>Upload the data to the default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-153">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-154">En los siguientes comandos de AzCopy, reemplace los siguientes parámetros con los valores reales que se especificó al crear el clúster de Hadoop y descomprimir los archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="e7a97-155">***&#60;path_to_data_folder>***: el directorio (junto con la ruta de acceso) del equipo que contiene los archivos de datos sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="e7a97-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span></span>  
* <span data-ttu-id="e7a97-156">***&#60;storage account name of Hadoop cluster>***: la cuenta de almacenamiento asociada con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7a97-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="e7a97-157">***&#60;default container of Hadoop cluster>***: el contenedor predeterminado que usa el clúster.</span><span class="sxs-lookup"><span data-stu-id="e7a97-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span></span> <span data-ttu-id="e7a97-158">Tenga en cuenta que el nombre del contenedor predeterminado suele ser el mismo que el del propio clúster.</span><span class="sxs-lookup"><span data-stu-id="e7a97-158">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="e7a97-159">Por ejemplo, si el clúster se llama "abc123.azurehdinsight.net", el contenedor predeterminado es abc123.</span><span class="sxs-lookup"><span data-stu-id="e7a97-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="e7a97-160">***&#60;storage account key>***: clave para la cuenta de almacenamiento usada por el clúster.</span><span class="sxs-lookup"><span data-stu-id="e7a97-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span></span>

<span data-ttu-id="e7a97-161">Desde un símbolo del sistema o una ventana de Windows PowerShell en el equipo, ejecute los dos comandos siguientes de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e7a97-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span></span>

<span data-ttu-id="e7a97-162">Este comando permite cargar los datos de carrera en el directorio ***nyctaxitripraw*** del contenedor predeterminado del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e7a97-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="e7a97-163">Este comando permite cargar los datos de tarifa en el directorio ***nyctaxifareraw*** del contenedor predeterminado del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e7a97-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="e7a97-164">Los datos deben estar ahora en el almacenamiento de blobs de Azure, listos para usarse dentro del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7a97-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span></span>

## <span data-ttu-id="e7a97-165"><a name="#download-hql-files"></a>Inicio de sesión en el nodo principal del clúster de Hadoop y preparación para el análisis de exploración de datos</span><span class="sxs-lookup"><span data-stu-id="e7a97-165"><a name="#download-hql-files"></a>Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-166">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-167">Para tener acceso al nodo principal del clúster para el análisis de exploración de datos y la reducción de estos, siga el procedimiento descrito en [Acceso al nodo principal del clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="e7a97-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="e7a97-168">En este tutorial se usan principalmente las consultas escritas en [Hive](https://hive.apache.org/), un lenguaje de consultas de tipo SQL, para realizar exploraciones preliminares de los datos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="e7a97-169">Las consultas de Hive se almacenan en archivos .hql.</span><span class="sxs-lookup"><span data-stu-id="e7a97-169">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="e7a97-170">A continuación, se reducen estos datos para su uso en Aprendizaje automático de Azure con el fin de generar modelos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-170">We then down sample this data to be used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="e7a97-171">Para preparar el clúster para el análisis de exploración de datos, se descargan los archivos .hql que contienen los scripts de Hive pertinentes de [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) en un directorio local (C:\temp) en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="e7a97-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="e7a97-172">Para ello, abra el **símbolo del sistema** desde dentro del nodo principal del clúster y emita los dos comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e7a97-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="e7a97-173">Estos dos comandos descargarán todos los archivos .hql necesarios en este tutorial en el directorio local ***C:\temp&#92;*** del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="e7a97-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <span data-ttu-id="e7a97-174"><a name="#hive-db-tables"></a>Creación de base de datos y tablas de Hive con particiones por mes</span><span class="sxs-lookup"><span data-stu-id="e7a97-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-175">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-176">Ahora estamos listos para crear tablas de Hive para nuestro conjunto de datos de taxis de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="e7a97-176">We are now ready to create Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="e7a97-177">En el nodo principal del clúster de Hadoop, abra la ***línea de comandos de Hadoop*** en el escritorio del nodo principal y especifique el directorio de Hive mediante este comando:</span><span class="sxs-lookup"><span data-stu-id="e7a97-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="e7a97-178">**Ejecute todos los comandos de Hive que aparecen en este tutorial desde el símbolo del sistema del directorio bin/ de Hive que aparece anteriormente. De esta manera, cualquier problema con la ruta de acceso se solucionará automáticamente. En este tutorial se utilizan indistintamente los términos "símbolo del sistema del directorio de Hive", "símbolo del sistema del directorio bin/ de Hive" y "línea de comandos de Hadoop".**</span><span class="sxs-lookup"><span data-stu-id="e7a97-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="e7a97-179">Desde el símbolo del sistema del directorio de Hive, escriba el siguiente comando en la línea de comandos de Hadoop del nodo principal para enviar la consulta de Hive de creación de la base de datos y las tablas de Hive:</span><span class="sxs-lookup"><span data-stu-id="e7a97-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="e7a97-180">Este es el contenido del archivo ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** que crea la base de datos de Hive ***nyctaxidb*** y las tablas ***trip*** y ***fare***.</span><span class="sxs-lookup"><span data-stu-id="e7a97-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="e7a97-181">Este script de Hive crea dos tablas:</span><span class="sxs-lookup"><span data-stu-id="e7a97-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="e7a97-182">La tabla "trip" contiene detalles del recorrido de cada carrera (detalles del conductor, hora de recogida, distancia de viaje y horas)</span><span class="sxs-lookup"><span data-stu-id="e7a97-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="e7a97-183">La tabla "fare" contiene los detalles de tarifa (importe de tarifa, propina, peajes y suplementos).</span><span class="sxs-lookup"><span data-stu-id="e7a97-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="e7a97-184">Si necesita ayuda adicional con estos procedimientos o bien si desea investigar otros alternativos, consulte la sección [Enviar consultas de Hive directamente desde la línea de comandos de Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="e7a97-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="e7a97-185"><a name="#load-data"></a>Carga de datos en tablas de Hive por particiones</span><span class="sxs-lookup"><span data-stu-id="e7a97-185"><a name="#load-data"></a>Load Data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-186">Esta tarea la suelen hacer los **administradores** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-187">El conjunto de datos de taxis de Nueva York tiene una partición natural por mes, que usamos para conseguir tiempos de procesamiento y consulta más rápidos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="e7a97-188">Los siguientes comandos de PowerShell (emitidos desde el directorio de Hive mediante la **línea de comandos de Hadoop**) cargan datos en las tablas de Hive "trip" y "fare" particionadas por mes.</span><span class="sxs-lookup"><span data-stu-id="e7a97-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="e7a97-189">El archivo *sample\_hive\_load\_data\_by\_partitions.hql* contiene los siguientes comandos **LOAD**.</span><span class="sxs-lookup"><span data-stu-id="e7a97-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="e7a97-190">Tenga en cuenta que un número de consultas de Hive que usamos aquí en el proceso de exploración implica la búsqueda en una sola partición o en un par de particiones.</span><span class="sxs-lookup"><span data-stu-id="e7a97-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="e7a97-191">Sin embargo, estas consultas se pueden ejecutar para todos los datos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-191">But these queries could be run across the entire data.</span></span>

### <span data-ttu-id="e7a97-192"><a name="#show-db"></a>Visualización de bases de datos en el clúster de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7a97-192"><a name="#show-db"></a>Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="e7a97-193">Para mostrar las bases de datos creadas en el clúster de Hadoop de HDInsight dentro de la ventana de la línea de comandos de Hadoop, ejecute el siguiente comando en la línea de comandos de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="e7a97-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="e7a97-194"><a name="#show-tables"></a>Visualización de las tablas de Hive en la base de datos nyctaxidb</span><span class="sxs-lookup"><span data-stu-id="e7a97-194"><a name="#show-tables"></a>Show the Hive tables in the nyctaxidb database</span></span>
<span data-ttu-id="e7a97-195">Para mostrar las tablas de la base de datos nyctaxidb, ejecute el siguiente comando en la línea de comandos de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="e7a97-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="e7a97-196">Para confirmar que las tabla trip tiene particiones se puede emitir el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7a97-196">We can confirm that the tables are partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="e7a97-197">A continuación se muestra el resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e7a97-197">The expected output is shown below:</span></span>

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

<span data-ttu-id="e7a97-198">Del mismo modo, para confirmar que las tabla fare tiene particiones se puede emitir el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7a97-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="e7a97-199">A continuación se muestra el resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e7a97-199">The expected output is shown below:</span></span>

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

## <span data-ttu-id="e7a97-200"><a name="#explore-hive"></a>Exploración de datos e ingeniería de características en Hive</span><span class="sxs-lookup"><span data-stu-id="e7a97-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-201">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-202">Las tareas de exploración de datos e ingeniería de características para los datos cargados en las tablas de subárbol se pueden lograr mediante consultas de subárbol.</span><span class="sxs-lookup"><span data-stu-id="e7a97-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="e7a97-203">Estos son ejemplos de dichas tareas por que las que le guiaremos en esta sección:</span><span class="sxs-lookup"><span data-stu-id="e7a97-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="e7a97-204">Ver los diez registros principales en ambas tablas.</span><span class="sxs-lookup"><span data-stu-id="e7a97-204">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="e7a97-205">Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="e7a97-206">Investigar la calidad de los datos de los campos de longitud y latitud.</span><span class="sxs-lookup"><span data-stu-id="e7a97-206">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="e7a97-207">Generar etiquetas de clasificación binaria y multiclase según **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="e7a97-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="e7a97-208">Generar características calculando las distancias de las carreras directas.</span><span class="sxs-lookup"><span data-stu-id="e7a97-208">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="e7a97-209">Exploración: Consulta de los 10 principales registros de la tabla trip</span><span class="sxs-lookup"><span data-stu-id="e7a97-209">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-210">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-211">Para ver el aspecto de los datos, examinamos 10 registros de cada tabla.</span><span class="sxs-lookup"><span data-stu-id="e7a97-211">To see what the data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="e7a97-212">Ejecute las dos consultas siguientes por separado desde el símbolo de sistema del directorio de Hadoop en la consola de línea de comandos de Hadoop para inspeccionar los registros.</span><span class="sxs-lookup"><span data-stu-id="e7a97-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span></span>

<span data-ttu-id="e7a97-213">Para obtener los 10 principales registros de la tabla "trip" correspondientes al primer mes:</span><span class="sxs-lookup"><span data-stu-id="e7a97-213">To get the top 10 records in the table "trip" from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="e7a97-214">Para obtener los 10 principales registros de la tabla "fare" correspondientes al primer mes:</span><span class="sxs-lookup"><span data-stu-id="e7a97-214">To get the top 10 records in the table "fare" from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="e7a97-215">A menudo resulta útil guardar los registros en un archivo para una visualización cómoda.</span><span class="sxs-lookup"><span data-stu-id="e7a97-215">It is often useful to save the records to a file for convenient viewing.</span></span> <span data-ttu-id="e7a97-216">Esto se consigue mediante un pequeño cambio en la consulta anterior:</span><span class="sxs-lookup"><span data-stu-id="e7a97-216">A small change to the above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="e7a97-217">Exploración: Consulta del número de registros en cada una de las 12 particiones</span><span class="sxs-lookup"><span data-stu-id="e7a97-217">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-218">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-219">Resulta interesante comprobar cómo varía el número de carreras durante el año natural.</span><span class="sxs-lookup"><span data-stu-id="e7a97-219">Of interest is the how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="e7a97-220">La agrupación por mes permite ver el aspecto de esta distribución de carreras.</span><span class="sxs-lookup"><span data-stu-id="e7a97-220">Grouping by month allows us to see what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="e7a97-221">Esto nos da el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="e7a97-221">This gives us the output :</span></span>

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

<span data-ttu-id="e7a97-222">En este caso, la primera columna es el mes y la segunda el número de carreras de ese mes.</span><span class="sxs-lookup"><span data-stu-id="e7a97-222">Here, the first column is the month and the second is the number of trips for that month.</span></span>

<span data-ttu-id="e7a97-223">También se puede contar el número total de registros del conjunto de datos de carreras emitiendo el comando siguiente en el símbolo del sistema del directorio de Hive.</span><span class="sxs-lookup"><span data-stu-id="e7a97-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="e7a97-224">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="e7a97-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="e7a97-225">Mediante el uso de comandos similares a los que se mostraron para el conjunto de datos de carreras se pueden emitir consultas de Hive desde el símbolo del sistema del directorio de Hive para el conjunto de datos de tarifas, con el fin de validar el número de registros.</span><span class="sxs-lookup"><span data-stu-id="e7a97-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="e7a97-226">Esto nos da el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="e7a97-226">This gives us the output:</span></span>

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

<span data-ttu-id="e7a97-227">Tenga en cuenta que se devuelve el mismo número exacto de carreras por mes para ambos conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-227">Note that the exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="e7a97-228">Esto supone la primera validación de que los datos se han cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="e7a97-228">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="e7a97-229">El recuento del número total de registros del conjunto de datos de tarifas puede realizarse mediante el comando siguiente desde el símbolo del sistema del directorio de Hive:</span><span class="sxs-lookup"><span data-stu-id="e7a97-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="e7a97-230">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="e7a97-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="e7a97-231">El número total de registros de ambas tablas es también el mismo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-231">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="e7a97-232">Esto supone la segunda validación de que los datos se han cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="e7a97-232">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="e7a97-233">Exploración: distribución de carreras por licencia</span><span class="sxs-lookup"><span data-stu-id="e7a97-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-234">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-235">Este ejemplo identifica las licencias (números de taxi) con más de 100 carreras dentro de un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="e7a97-236">La consulta se beneficia del acceso a la tabla con particiones puesto que está condicionada por la variable de partición **month**.</span><span class="sxs-lookup"><span data-stu-id="e7a97-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="e7a97-237">Los resultados de la consulta se escriben en un archivo local queryoutput.tsv en `C:\temp` en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="e7a97-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="e7a97-238">Aquí se muestra el contenido del archivo *sample\_hive\_trip\_count\_by\_medallion.hql* para su inspección.</span><span class="sxs-lookup"><span data-stu-id="e7a97-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="e7a97-239">La licencia del conjunto de datos de taxis de NYC identifica a cada taxi de forma única.</span><span class="sxs-lookup"><span data-stu-id="e7a97-239">The medallion in the NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="e7a97-240">Se puede identificar qué taxis trabajan más preguntando cuáles realizaron más de un determinado número de carreras en un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="e7a97-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="e7a97-241">El ejemplo siguiente identifica los taxis que realizaron más de cien carreras en los tres primeros meses y guarda los resultados de la consulta en un archivo local, C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="e7a97-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="e7a97-242">Aquí se muestra el contenido del archivo *sample\_hive\_trip\_count\_by\_medallion.hql* para su inspección.</span><span class="sxs-lookup"><span data-stu-id="e7a97-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="e7a97-243">Desde el símbolo de sistema del directorio de Hive, emita el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e7a97-243">From the Hive directory prompt, issue the command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="e7a97-244">Exploración: distribución de carreras por medallion y hack_license</span><span class="sxs-lookup"><span data-stu-id="e7a97-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-245">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-246">Al explorar un conjunto de datos, con frecuencia deseamos examinar el número de repeticiones de grupos de valores.</span><span class="sxs-lookup"><span data-stu-id="e7a97-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="e7a97-247">En esta sección se ofrece un ejemplo de cómo llevar esto a cabo para los taxis y los conductores.</span><span class="sxs-lookup"><span data-stu-id="e7a97-247">This section provide an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="e7a97-248">El archivo *sample\_hive\_trip\_count\_by\_medallion\_license.hql* agrupa el conjunto de datos de tarifas en función de los valores de "medallion" y "hack_license", y devuelve los recuentos de cada combinación.</span><span class="sxs-lookup"><span data-stu-id="e7a97-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="e7a97-249">A continuación se muestra su contenido.</span><span class="sxs-lookup"><span data-stu-id="e7a97-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="e7a97-250">Esta consulta devuelve combinaciones de taxi y conductor determinado ordenadas por número descendente de carreras.</span><span class="sxs-lookup"><span data-stu-id="e7a97-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="e7a97-251">Desde el símbolo del sistema del directorio de Hive, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e7a97-251">From the Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="e7a97-252">Los resultados de la consulta se escriben en un archivo local C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="e7a97-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="e7a97-253">Exploración: Evaluación de la calidad de los datos mediante la comprobación de registros con latitud/longitud no válida</span><span class="sxs-lookup"><span data-stu-id="e7a97-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-254">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-255">Un objetivo común del análisis de exploración de datos consiste en descartar registros no válidos o incorrectos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="e7a97-256">En el ejemplo de esta sección se determina si los campos de longitud o latitud contienen un valor fuera del área de la ciudad de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="e7a97-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="e7a97-257">Es probable que estos registros tengan valores de longitud o latitud incorrectos, por lo que queremos eliminarlos de todos los datos que se van a usar para el modelado.</span><span class="sxs-lookup"><span data-stu-id="e7a97-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="e7a97-258">Aquí se muestra el contenido del archivo *sample\_hive\_quality\_assessment.hql* para su inspección.</span><span class="sxs-lookup"><span data-stu-id="e7a97-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="e7a97-259">Desde el símbolo del sistema del directorio de Hive, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e7a97-259">From the Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="e7a97-260">El argumento *-S* incluido en este comando suprime la impresión de la pantalla de estado de los trabajos de asignación/reducción de Hive.</span><span class="sxs-lookup"><span data-stu-id="e7a97-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="e7a97-261">Esto es útil porque hace que la impresión de la pantalla de la salida de la consulta de subárbol sea más legible.</span><span class="sxs-lookup"><span data-stu-id="e7a97-261">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="e7a97-262">Exploración: Distribuciones de clase binaria de las propinas de las carreras</span><span class="sxs-lookup"><span data-stu-id="e7a97-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-263">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-264">Para el problema de clasificación binaria descrito en la sección [Ejemplos de tareas de predicción](machine-learning-data-science-process-hive-walkthrough.md#mltasks) , es útil saber si se recibió una propina o no.</span><span class="sxs-lookup"><span data-stu-id="e7a97-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="e7a97-265">Esta distribución de las propinas es binaria:</span><span class="sxs-lookup"><span data-stu-id="e7a97-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="e7a97-266">Propina dada (clase 1, tip\_amount > 0 $).</span><span class="sxs-lookup"><span data-stu-id="e7a97-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="e7a97-267">Sin propina (clase 0, tip\_amount = 0 $).</span><span class="sxs-lookup"><span data-stu-id="e7a97-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="e7a97-268">El archivo *sample\_hive\_tipped\_frequencies.hql* que se muestra a continuación lo lleva a cabo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="e7a97-269">Desde el símbolo del sistema del directorio de Hive, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e7a97-269">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="e7a97-270">Exploración: Distribuciones de clase en la configuración de clases múltiples</span><span class="sxs-lookup"><span data-stu-id="e7a97-270">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-271">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-272">Para el problema de clasificación de clases múltiples descrito en la sección [Ejemplos de tareas de predicción](machine-learning-data-science-process-hive-walkthrough.md#mltasks) este conjunto de datos también se presta a una clasificación natural donde nos gustaría predecir el importe de las propinas dadas.</span><span class="sxs-lookup"><span data-stu-id="e7a97-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span></span> <span data-ttu-id="e7a97-273">Podemos usar ubicaciones para definir intervalos de propinas en la consulta.</span><span class="sxs-lookup"><span data-stu-id="e7a97-273">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="e7a97-274">Para obtener las distribuciones de clase para los distintos intervalos de propina, usamos el archivo *sample\_hive\_tip\_range\_frequencies.hql*.</span><span class="sxs-lookup"><span data-stu-id="e7a97-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="e7a97-275">A continuación se muestra su contenido.</span><span class="sxs-lookup"><span data-stu-id="e7a97-275">Below are its contents.</span></span>

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

<span data-ttu-id="e7a97-276">Ejecute el siguiente comando desde la consola de la línea de comandos de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="e7a97-276">Run the following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="e7a97-277">Exploración: Cálculo de la distancia directa entre dos ubicaciones de longitud y latitud de proceso</span><span class="sxs-lookup"><span data-stu-id="e7a97-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-278">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-279">Tener una medida de la distancia directa nos permite averiguar la discrepancia entre ella y la distancia real de la carrera.</span><span class="sxs-lookup"><span data-stu-id="e7a97-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span></span> <span data-ttu-id="e7a97-280">Esta característica se justifica por el hecho de que es probable que un pasajero sea más remiso a dar propina si sospecha que el conductor le lleva intencionadamente por un recorrido mucho más largo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="e7a97-281">Para ver la comparación entre la distancia real de la carrera y la [distancia Haversine](http://en.wikipedia.org/wiki/Haversine_formula) entre dos puntos de longitud-latitud (la distancia del "círculo máximo"), usamos las funciones trigonométricas disponibles dentro de Hive, así:</span><span class="sxs-lookup"><span data-stu-id="e7a97-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="e7a97-282">En la consulta anterior, R es el radio de la Tierra en millas y pi se ha convertido a radianes.</span><span class="sxs-lookup"><span data-stu-id="e7a97-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="e7a97-283">Tenga en cuenta que los puntos de longitud-latitud se han "filtrado" para quitar los valores que están lejos del área metropolitana de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="e7a97-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="e7a97-284">En este caso, escribimos los resultados en un directorio llamado "queryoutputdir".</span><span class="sxs-lookup"><span data-stu-id="e7a97-284">In this case, we write our results to a directory called "queryoutputdir".</span></span> <span data-ttu-id="e7a97-285">La secuencia de comandos que se muestra a continuación crea primero este directorio de salida y después ejecuta el comando de Hive.</span><span class="sxs-lookup"><span data-stu-id="e7a97-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="e7a97-286">Desde el símbolo del sistema del directorio de Hive, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e7a97-286">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="e7a97-287">Los resultados de la consulta se escriben en 9 blobs de Azure de ***queryoutputdir/000000\_0*** a ***queryoutputdir/000008\_0*** bajo el contenedor predeterminado del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e7a97-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="e7a97-288">Para ver el tamaño de los blobs individuales, se ejecuta el siguiente comando desde el símbolo del sistema del directorio de Hive:</span><span class="sxs-lookup"><span data-stu-id="e7a97-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="e7a97-289">Para ver el contenido de un archivo determinado, por ejemplo, 000000\_0, se usa el comando `copyToLocal` de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e7a97-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="e7a97-290">`copyToLocal` puede ser muy lento para archivos de gran tamaño y no se recomienda para su uso con ellos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="e7a97-291">Una ventaja clave de tener estos datos en un blob de Azure es que se pueden explorar dentro de Azure Machine Learning mediante el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="e7a97-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span></span>

## <span data-ttu-id="e7a97-292"><a name="#downsample"></a>Reducción de datos y creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e7a97-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="e7a97-293">Esta tarea la suelen hacer los **científicos de datos** .</span><span class="sxs-lookup"><span data-stu-id="e7a97-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e7a97-294">Después de la fase de análisis de exploración de datos, estamos preparados para reducir los datos y crear modelos en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a97-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="e7a97-295">En esta sección veremos cómo se usa una consulta de Hive para reducir los datos, a los que después se accede desde el módulo [Importar datos][import-data] de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7a97-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="e7a97-296">Reducción de los datos</span><span class="sxs-lookup"><span data-stu-id="e7a97-296">Down sampling the data</span></span>
<span data-ttu-id="e7a97-297">Este procedimiento incluye dos pasos.</span><span class="sxs-lookup"><span data-stu-id="e7a97-297">There are two steps in this procedure.</span></span> <span data-ttu-id="e7a97-298">En primer lugar, se unen las tablas **nyctaxidb.trip** y **nyctaxidb.fare** en función de tres claves incluidas en todos los registros: "medallion", "hack\_license" y "pickup\_datetime".</span><span class="sxs-lookup"><span data-stu-id="e7a97-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="e7a97-299">Después se genera una etiqueta de clasificación binaria **tipped** y una etiqueta de clasificación de múltiples clases **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="e7a97-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="e7a97-300">Para usar los datos muestreados directamente desde el módulo [Importar datos][import-data] de Azure Machine Learning, se deben almacenar los resultados de la consulta anterior en una tabla interna de Hive.</span><span class="sxs-lookup"><span data-stu-id="e7a97-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span></span> <span data-ttu-id="e7a97-301">En lo que sigue, se crea una tabla interna de Hive y se rellena su contenido con los datos reducidos y combinados.</span><span class="sxs-lookup"><span data-stu-id="e7a97-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span></span>

<span data-ttu-id="e7a97-302">La consulta aplica funciones estándar de Hive directamente para generar la hora del día, la semana del año, el día de la semana (1 representa el lunes y 7 el domingo) a partir del campo "pickup\_datetime", y la distancia directa entre las ubicaciones de recogida y destino.</span><span class="sxs-lookup"><span data-stu-id="e7a97-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="e7a97-303">Los usuarios pueden consultar [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) (Manual de lenguaje: campos definidos por el usuario) para obtener una lista completa de estas funciones.</span><span class="sxs-lookup"><span data-stu-id="e7a97-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="e7a97-304">Después esta consulta reduce los datos para que los resultados quepan en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a97-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span></span> <span data-ttu-id="e7a97-305">Aproximadamente solo el 1% del conjunto de datos original se importa en Estudio.</span><span class="sxs-lookup"><span data-stu-id="e7a97-305">Only about 1% of the original dataset is imported into the Studio.</span></span>

<span data-ttu-id="e7a97-306">A continuación se muestra el contenido del archivo *sample\_hive\_prepare\_for\_aml\_full.hql* que prepara los datos para la creación de modelos en Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7a97-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

        --- now insert contents of the join into the above internal table

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

<span data-ttu-id="e7a97-307">Para ejecutar esta consulta, escriba en el símbolo del sistema del directorio de Hive:</span><span class="sxs-lookup"><span data-stu-id="e7a97-307">To run this query, from the Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="e7a97-308">Ahora tenemos una tabla interna nyctaxidb.nyctaxi_downsampled_dataset, a la que se puede acceder mediante el módulo [Importar datos][import-data] de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7a97-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="e7a97-309">También se puede utilizar este conjunto de datos para generar modelos de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="e7a97-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-azure-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="e7a97-310">Uso del módulo Importar datos de Aprendizaje automático de Azure para acceder a los datos muestreados</span><span class="sxs-lookup"><span data-stu-id="e7a97-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span></span>
<span data-ttu-id="e7a97-311">Como requisitos previos para la emisión de consultas de Hive en el módulo [Importar datos][import-data] de Azure Machine Learning, se necesita acceso a un área de trabajo de Azure Machine Learning y a las credenciales del clúster y su cuenta de almacenamiento asociada.</span><span class="sxs-lookup"><span data-stu-id="e7a97-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="e7a97-312">A continuación se indican algunos detalles del módulo [Importar datos][import-data] y los parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="e7a97-312">Some details on the [Import Data][import-data] module and the parameters to input :</span></span>

<span data-ttu-id="e7a97-313">**URI del servidor de HCatalog**: si el nombre del clúster es abc123, sería: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="e7a97-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="e7a97-314">**Nombre de la cuenta de usuario de Hadoop**: el nombre de usuario elegido para el clúster (**no** es el nombre de usuario de acceso remoto)</span><span class="sxs-lookup"><span data-stu-id="e7a97-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span></span>

<span data-ttu-id="e7a97-315">**Contraseña de la cuenta de usuario de Hadoop**: la contraseña elegida para el clúster (**no** es la contraseña de acceso remoto)</span><span class="sxs-lookup"><span data-stu-id="e7a97-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span></span>

<span data-ttu-id="e7a97-316">**Ubicación de datos de salida** : este valor se elige como Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a97-316">**Location of output data** : This is chosen to be Azure.</span></span>

<span data-ttu-id="e7a97-317">**Nombre de la cuenta de almacenamiento de Azure** : nombre de la cuenta de almacenamiento predeterminada asociada al clúster.</span><span class="sxs-lookup"><span data-stu-id="e7a97-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="e7a97-318">**Nombre de contenedor de Azure** : este es el nombre del contenedor predeterminado para el clúster y suele ser el mismo que el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="e7a97-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="e7a97-319">En un clúster denominado "abc123", es abc123.</span><span class="sxs-lookup"><span data-stu-id="e7a97-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7a97-320">**Cualquier tabla que desee consultar mediante el módulo [Importar datos][import-data] de Azure Machine Learning debe ser una tabla interna.**</span><span class="sxs-lookup"><span data-stu-id="e7a97-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="e7a97-321">Una manera de determinar si una tabla T en una base de datos D.db es una tabla interna es la siguiente.</span><span class="sxs-lookup"><span data-stu-id="e7a97-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="e7a97-322">Desde el símbolo de sistema del directorio de Hive, emita el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e7a97-322">From the Hive directory prompt, issue the command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="e7a97-323">Si la tabla es una tabla interna y está rellena, su contenido se debe mostrar aquí.</span><span class="sxs-lookup"><span data-stu-id="e7a97-323">If the table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="e7a97-324">Otro modo de determinar si una tabla es una tabla interna es utilizar Explorador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a97-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span></span> <span data-ttu-id="e7a97-325">Úselo para navegar al nombre del contenedor predeterminado del clúster y, después, filtre por el nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="e7a97-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="e7a97-326">Si se muestran la tabla y su contenido, se confirma que es una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="e7a97-326">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="e7a97-327">A continuación, se muestra una instantánea de la consulta de Hive y el módulo [Importar datos][import-data]:</span><span class="sxs-lookup"><span data-stu-id="e7a97-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span></span>

![Consulta de Hive para el módulo de importación de datos](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="e7a97-329">Tenga en cuenta que, dado que los datos reducidos se encuentran en el contenedor predeterminado, la consulta de Hive resultante de Azure Machine Learning es muy sencilla, simplemente "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span><span class="sxs-lookup"><span data-stu-id="e7a97-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="e7a97-330">Ahora el conjunto de datos se puede usar como punto de partida para la creación de modelos de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="e7a97-330">The dataset may now be used as the starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="e7a97-331"><a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e7a97-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="e7a97-332">Ya se puede pasar a la creación del modelo y la implementación del mismo en [Aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e7a97-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="e7a97-333">Ahora los datos están preparados para usarlos con el fin de abordar los problemas de predicción identificados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="e7a97-333">The data is ready for us to use in addressing the prediction problems identified above:</span></span>

<span data-ttu-id="e7a97-334">**1. Clasificación binaria**: permite predecir si se dio propina en una carrera, o no.</span><span class="sxs-lookup"><span data-stu-id="e7a97-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="e7a97-335">**Lector usado** : regresión logística de dos clases</span><span class="sxs-lookup"><span data-stu-id="e7a97-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="e7a97-336">a.</span><span class="sxs-lookup"><span data-stu-id="e7a97-336">a.</span></span> <span data-ttu-id="e7a97-337">En este problema la etiqueta de destino (o clase) es "tipped".</span><span class="sxs-lookup"><span data-stu-id="e7a97-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="e7a97-338">El conjunto de datos reducido original incluye algunas columnas que no contienen datos para el experimento de clasificación.</span><span class="sxs-lookup"><span data-stu-id="e7a97-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="e7a97-339">Se trata, en concreto, de tip\_class, tip\_amount, and total\_amount, que dan información sobre la etiqueta de destino que no está disponible en el momento de la prueba.</span><span class="sxs-lookup"><span data-stu-id="e7a97-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="e7a97-340">Quitaremos estas columnas mediante el módulo [Seleccionar columnas de conjunto de datos][select-columns].</span><span class="sxs-lookup"><span data-stu-id="e7a97-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e7a97-341">La siguiente instantánea muestra nuestro experimento para predecir si se pagó o no una propina por una carrera determinada.</span><span class="sxs-lookup"><span data-stu-id="e7a97-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span></span>

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="e7a97-343">b.</span><span class="sxs-lookup"><span data-stu-id="e7a97-343">b.</span></span> <span data-ttu-id="e7a97-344">En este experimento las distribuciones de la etiqueta de destino eran aproximadamente 1:1.</span><span class="sxs-lookup"><span data-stu-id="e7a97-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="e7a97-345">La siguiente instantánea muestra la distribución de las etiquetas de clase de propina para el problema de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="e7a97-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span></span>

![Distribución de las etiquetas de clase de sugerencia](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="e7a97-347">Como resultado, obtenemos un área bajo la curva de 0,987 tal como se muestra en la figura siguiente.</span><span class="sxs-lookup"><span data-stu-id="e7a97-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span></span>

![Valor de AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="e7a97-349">**2. Clasificación con múltiples clases**: permite predecir el intervalo de importes de propinas para la carrera mediante las clases definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e7a97-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span></span>

<span data-ttu-id="e7a97-350">**Lector usado** : regresión logística de múltiples clases</span><span class="sxs-lookup"><span data-stu-id="e7a97-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="e7a97-351">a.</span><span class="sxs-lookup"><span data-stu-id="e7a97-351">a.</span></span> <span data-ttu-id="e7a97-352">En este problema, la etiqueta de destino (o clase) es "tip\_class", que puede adoptar uno de cinco valores (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="e7a97-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="e7a97-353">Como en el caso de clasificación binaria, tenemos algunas columnas que son pérdidas de destino para este experimento.</span><span class="sxs-lookup"><span data-stu-id="e7a97-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="e7a97-354">Se trata, en concreto, de: tipped, tip\_amount y total\_amount, que dan información sobre la etiqueta de destino que no está disponible en el momento de la prueba.</span><span class="sxs-lookup"><span data-stu-id="e7a97-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="e7a97-355">Quitaremos estas columnas mediante el módulo [Seleccionar columnas de conjunto de datos][select-columns].</span><span class="sxs-lookup"><span data-stu-id="e7a97-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e7a97-356">La siguiente instantánea muestra nuestro experimento para predecir en qué ubicación es probable que se incluya una propina (clase 0: propina = 0 $, clase 1: propina > 0 $ y < = 5 $, clase 2: propina > 5 $ y < = 10 $, clase 3: propina > 10 $ y < = 20 $, clase 4: propina > 20 $)</span><span class="sxs-lookup"><span data-stu-id="e7a97-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="e7a97-358">Ahora vemos qué aspecto tiene nuestra distribución de clases de prueba real.</span><span class="sxs-lookup"><span data-stu-id="e7a97-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="e7a97-359">Se puede ver que, mientras que las clase 0 y 1 son frecuentes, las demás no lo son.</span><span class="sxs-lookup"><span data-stu-id="e7a97-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span></span>

![Distribución de la clase de prueba](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="e7a97-361">b.</span><span class="sxs-lookup"><span data-stu-id="e7a97-361">b.</span></span> <span data-ttu-id="e7a97-362">En este experimento utilizamos una matriz de confusión para analizar la precisión de las predicciones.</span><span class="sxs-lookup"><span data-stu-id="e7a97-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span></span> <span data-ttu-id="e7a97-363">Esto se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7a97-363">This is shown below.</span></span>

![Matriz de confusión](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="e7a97-365">Observe que, aunque la precisión para las clases frecuentes es bastante buena, el modelo no hace un buen trabajo de "aprendizaje" en las clases menos frecuentes.</span><span class="sxs-lookup"><span data-stu-id="e7a97-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

<span data-ttu-id="e7a97-366">**3. Tarea de regresión**: permite predecir el importe de la propina pagada por una carrera.</span><span class="sxs-lookup"><span data-stu-id="e7a97-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span></span>

<span data-ttu-id="e7a97-367">**Lector usado** : árbol de decisión incrementado</span><span class="sxs-lookup"><span data-stu-id="e7a97-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="e7a97-368">a.</span><span class="sxs-lookup"><span data-stu-id="e7a97-368">a.</span></span> <span data-ttu-id="e7a97-369">En este problema la etiqueta de destino (o clase) es "tip\_amount".</span><span class="sxs-lookup"><span data-stu-id="e7a97-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="e7a97-370">En este caso las pérdidas de destino son: tipped, tip\_class, total\_amount; todas estas variables ofrecen información sobre el importe de la propina, que no suele estar disponible en el momento de la prueba.</span><span class="sxs-lookup"><span data-stu-id="e7a97-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="e7a97-371">Quitaremos estas columnas mediante el módulo [Seleccionar columnas de conjunto de datos][select-columns].</span><span class="sxs-lookup"><span data-stu-id="e7a97-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e7a97-372">La instantánea siguiente muestra nuestro experimento para predecir el importe de una propina determinada.</span><span class="sxs-lookup"><span data-stu-id="e7a97-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span></span>

![Instantánea del experimento](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="e7a97-374">b.</span><span class="sxs-lookup"><span data-stu-id="e7a97-374">b.</span></span> <span data-ttu-id="e7a97-375">En los problemas de regresión se mide la precisión de nuestra predicción mediante la observación del error cuadrático en las predicciones, el coeficiente de determinación y similares.</span><span class="sxs-lookup"><span data-stu-id="e7a97-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span></span> <span data-ttu-id="e7a97-376">Lo mostramos a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7a97-376">We show these below.</span></span>

![Estadísticas de predicción](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="e7a97-378">Vemos que el coeficiente de determinación es 0,709, lo que implica que aproximadamente el 71% de la varianza se explica por nuestros coeficientes de modelo.</span><span class="sxs-lookup"><span data-stu-id="e7a97-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7a97-379">Para obtener más información sobre Azure Machine Learning y cómo acceder a él y usarlo, consulte [¿Qué es el Aprendizaje automático de Microsoft Azure?](machine-learning-what-is-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="e7a97-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="e7a97-380">Un recurso muy útil para realizar una serie de experimentos con Azure Machine Learning es la [Galería de Cortana Intelligence](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="e7a97-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="e7a97-381">La Galería cubre una gama de experimentos y da una introducción exhaustiva sobre la variedad de capacidades de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a97-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="e7a97-382">Información de licencia</span><span class="sxs-lookup"><span data-stu-id="e7a97-382">License Information</span></span>
<span data-ttu-id="e7a97-383">Microsoft comparte este tutorial de ejemplo y sus scripts adjuntos bajo la licencia MIT.</span><span class="sxs-lookup"><span data-stu-id="e7a97-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="e7a97-384">Consulte el archivo LICENSE.txt que se encuentra en el directorio del código de ejemplo en GitHub para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="e7a97-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="e7a97-385">Referencias</span><span class="sxs-lookup"><span data-stu-id="e7a97-385">References</span></span>
<span data-ttu-id="e7a97-386">•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="e7a97-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="e7a97-387">•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="e7a97-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="e7a97-388">•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="e7a97-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
