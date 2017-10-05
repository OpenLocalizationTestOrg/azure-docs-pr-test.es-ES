---
title: 'Ciencia de datos escalables con Azure Data Lake: tutorial completo | Microsoft Docs'
description: "Uso de Azure Data Lake para realizar tareas de exploración de datos y clasificación binaria en un conjunto de datos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 34fbe99572b4a6cee73de6ae5412a0ec09dd1ccc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="fd337-103">Ciencia de datos escalables con Azure Data Lake: tutorial completo</span><span class="sxs-lookup"><span data-stu-id="fd337-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="fd337-104">En este tutorial se muestra cómo utilizar Azure Data Lake para realizar las tareas de exploración de datos y clasificación binaria en un ejemplo del conjunto de datos de carreras y tarifas de taxi de la ciudad de Nueva York para predecir si se dará una propina por tarifa.</span><span class="sxs-lookup"><span data-stu-id="fd337-104">This walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi trip and fare dataset to predict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="fd337-105">Le guía por los pasos de todo el [proceso de la ciencia de datos en equipos](http://aka.ms/datascienceprocess), desde la adquisición de los datos al entrenamiento del modelo y, a continuación, a la implementación de un servicio web que publique el modelo.</span><span class="sxs-lookup"><span data-stu-id="fd337-105">It walks you through the steps of the [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition to model training, and then to the deployment of a web service that publishes the model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="fd337-106">Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd337-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="fd337-107">[Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) ofrece todas las funcionalidades necesarias para facilitar a los científicos de datos el almacenamiento de datos de cualquier tamaño, forma y velocidad, y llevar a cabo el procesamiento de datos, análisis avanzado y modelado del aprendizaje automático con alta escalabilidad de una manera rentable.</span><span class="sxs-lookup"><span data-stu-id="fd337-107">The [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all the capabilities required to make it easy for data scientists to store data of any size, shape and speed, and to conduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="fd337-108">Se paga por trabajo, solo cuando se procesan los datos.</span><span class="sxs-lookup"><span data-stu-id="fd337-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="fd337-109">Análisis de Azure Data Lake incluye U-SQL, un lenguaje que mezcla la naturaleza declarativa de SQL con la potencia expresiva de C# para proporcionar una funcionalidad de consulta distribuida escalable.</span><span class="sxs-lookup"><span data-stu-id="fd337-109">Azure Data Lake Analytics includes U-SQL, a language that blends the declarative nature of SQL with the expressive power of C# to provide scalable distributed query capability.</span></span> <span data-ttu-id="fd337-110">Permite procesar datos sin estructura mediante la aplicación de un esquema al leer, la inserción de lógica personalizada y funciones definidas por el usuario (UDF), e incluye extensibilidad para habilitar un control más preciso sobre la ejecución a escala.</span><span class="sxs-lookup"><span data-stu-id="fd337-110">It enables you to process unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility to enable fine grained control over how to execute at scale.</span></span> <span data-ttu-id="fd337-111">Para más información acerca de la filosofía de diseño tras U-SQL, consulte esta [entrada del blog de Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="fd337-111">To learn more about the design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="fd337-112">Análisis de Data Lake es también una parte fundamental del conjunto de aplicaciones Cortana Analytics y funciona con Almacenamiento de datos SQL de Azure, Power BI y Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fd337-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="fd337-113">Esto proporciona una plataforma completa de análisis avanzado y macrodatos en la nube.</span><span class="sxs-lookup"><span data-stu-id="fd337-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="fd337-114">Este tutorial comienza con la descripción de los requisitos previos y recursos necesarios para completar con Análisis de Data Lake las tareas que forman el proceso de ciencia de datos y cómo instalarlos.</span><span class="sxs-lookup"><span data-stu-id="fd337-114">This walkthrough begins by describing the prerequisites and resources that are needed to complete the tasks with Data Lake Analytics that form the data science process and how to install them.</span></span> <span data-ttu-id="fd337-115">A continuación, se describen los pasos de procesamiento de datos mediante U-SQL y se concluye con una demostración de cómo usar Python y Hive con Estudio de aprendizaje automático de Azure para generar e implementar los modelos predictivos.</span><span class="sxs-lookup"><span data-stu-id="fd337-115">Then it outlines the data processing steps using U-SQL and concludes by showing how to use Python and Hive with Azure Machine Learning Studio to build and deploy the predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="fd337-116">U-SQL y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd337-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="fd337-117">En este tutorial se recomienda usar Visual Studio para editar scripts U-SQL para procesar el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="fd337-117">This walkthrough recommends using Visual Studio to edit U-SQL scripts to process the dataset.</span></span> <span data-ttu-id="fd337-118">Los scripts U-SQL se describen aquí y se proporcionan en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="fd337-118">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="fd337-119">El proceso incluye el consumo, la exploración y el muestreo de los datos.</span><span class="sxs-lookup"><span data-stu-id="fd337-119">The process includes ingesting, exploring, and sampling the data.</span></span> <span data-ttu-id="fd337-120">También se muestra cómo ejecutar un trabajo con scripts U-SQL desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-120">It also shows how to run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="fd337-121">Se crean tablas de Hive para los datos en un clúster de HDInsight asociado para facilitar la generación e implementación de un modelo de clasificación binaria en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-121">Hive tables are created for the data in an associated HDInsight cluster to facilitate the building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="fd337-122">Python</span><span class="sxs-lookup"><span data-stu-id="fd337-122">Python</span></span>
<span data-ttu-id="fd337-123">Este tutorial también contiene una sección que muestra cómo generar e implementar un modelo predictivo con Estudio de aprendizaje automático de Azure mediante Python.</span><span class="sxs-lookup"><span data-stu-id="fd337-123">This walkthrough also contains a section that shows how to build and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="fd337-124">Ofrecemos un cuaderno de Jupyter Notebook con los scripts Python para estos pasos del proceso.</span><span class="sxs-lookup"><span data-stu-id="fd337-124">We provide a Jupyter notebook with the Python scripts for these steps in this process.</span></span> <span data-ttu-id="fd337-125">El cuaderno de Jupyter Notebook incluye código para varios pasos de ingeniería de características adicionales y construcción de modelos, como la clasificación multiclase y los modelos de regresión, además del modelo de clasificación binaria descrito aquí.</span><span class="sxs-lookup"><span data-stu-id="fd337-125">The notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition to the binary classification model outlined here.</span></span> <span data-ttu-id="fd337-126">La tarea de la regresión consiste en predecir el importe de la propina en función de otras características de la propina.</span><span class="sxs-lookup"><span data-stu-id="fd337-126">The regression task is to predict the amount of the tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="fd337-127">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-127">Azure Machine Learning</span></span>
<span data-ttu-id="fd337-128">Se usa Estudio de aprendizaje automático de Azure para generar e implementar los modelos predictivos.</span><span class="sxs-lookup"><span data-stu-id="fd337-128">Azure Machine Learning Studio is used to build and deploy the predictive models.</span></span> <span data-ttu-id="fd337-129">Para esto se aplican dos enfoques: primero con scripts Python y después con tablas de Hive en un clúster de HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="fd337-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="fd337-130">Scripts</span><span class="sxs-lookup"><span data-stu-id="fd337-130">Scripts</span></span>
<span data-ttu-id="fd337-131">En este tutorial solo se describen los principales pasos.</span><span class="sxs-lookup"><span data-stu-id="fd337-131">Only the principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="fd337-132">Tanto el **script U-SQL** como **Jupyter Notebook** se pueden descargar de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="fd337-132">You can download the full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd337-133">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd337-133">Prerequisites</span></span>
<span data-ttu-id="fd337-134">Antes de empezar estos temas, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd337-134">Before you begin these topics, you must have the following:</span></span>

* <span data-ttu-id="fd337-135">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-135">An Azure subscription.</span></span> <span data-ttu-id="fd337-136">Si aún no tiene una, consulte [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)(Obtener una evaluación gratuita de Azure).</span><span class="sxs-lookup"><span data-stu-id="fd337-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="fd337-137">[Recomendado] Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="fd337-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="fd337-138">Si aún no tiene ninguna de estas versiones instaladas, puede descargar una versión gratuita de Community desde [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="fd337-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="fd337-139">En lugar de Visual Studio, también puede usar el Portal de Azure para enviar las consultas de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd337-139">Instead of Visual Studio, you can also use the Azure Portal to submit Azure Data Lake queries.</span></span> <span data-ttu-id="fd337-140">Se proporcionarán instrucciones sobre cómo hacerlo con Visual Studio y en el portal en la sección titulada **Procesamiento de datos con U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="fd337-140">We will provide instructions on how to do so both with Visual Studio and on the portal in the section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="fd337-141">Preparación del entorno de la ciencia de datos para Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd337-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="fd337-142">Para preparar el entorno de la ciencia de datos para este tutorial, cree los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="fd337-142">To prepare the data science environment for this walkthrough, create the following resources:</span></span>

* <span data-ttu-id="fd337-143">Almacén de Azure Data Lake (ADLS)</span><span class="sxs-lookup"><span data-stu-id="fd337-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="fd337-144">Análisis de Azure Data Lake (ADLA)</span><span class="sxs-lookup"><span data-stu-id="fd337-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="fd337-145">Cuenta de Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-145">Azure Blob storage account</span></span>
* <span data-ttu-id="fd337-146">Cuenta de Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="fd337-147">Herramientas de Azure Data Lake para Visual Studio (se recomienda)</span><span class="sxs-lookup"><span data-stu-id="fd337-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="fd337-148">Esta sección proporciona instrucciones sobre cómo crear cada uno de estos recursos.</span><span class="sxs-lookup"><span data-stu-id="fd337-148">This section provides instructions on how to create each of these resources.</span></span> <span data-ttu-id="fd337-149">Si opta por usar tablas de Hive con Azure Machine Learning, en lugar de Python, para generar un modelo, también necesitará aprovisionar un clúster de HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="fd337-149">If you choose to use Hive tables with Azure Machine Learning, instead of Python, to build a model,you will also need to provision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="fd337-150">Este procedimiento alternativo se describe en la sección correspondiente.</span><span class="sxs-lookup"><span data-stu-id="fd337-150">This alternative procedure in described in the appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="fd337-151">Se puede crear **Azure Data Lake Store** por separado o cuando se crea **Azure Data Lake Analytics** como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="fd337-151">The **Azure Data Lake Store** can be created either separately or when you create the **Azure Data Lake Analytics** as the default storage.</span></span> <span data-ttu-id="fd337-152">A continuación, se hace referencia a las instrucciones para crear cada uno de estos recursos por separado, pero no es preciso crear la cuenta del Almacén de Data Lake de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="fd337-152">Instructions are referenced for creating each of these resources separately below, but the Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="fd337-153">Creación de un Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd337-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="fd337-154">Cree un ADLS desde el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd337-154">Create an ADLS from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="fd337-155">Para más información, consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd337-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="fd337-156">Asegúrese de configurar la identidad de AAD del clúster en la hoja **Origen de datos** de la hoja **Configuración opcional** descrita allí.</span><span class="sxs-lookup"><span data-stu-id="fd337-156">Be sure to set up the Cluster AAD Identity in the **DataSource** blade of the **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="fd337-158">Creación de una cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd337-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="fd337-159">Cree una cuenta de ADLA desde el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd337-159">Create an ADLA account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="fd337-160">Para más información, consulte [Tutorial: Introducción a Análisis de Azure Data Lake mediante el Portal de Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd337-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="fd337-162">Creación de una cuenta de Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="fd337-163">Cree una cuenta de Almacenamiento de blobs de Azure desde el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd337-163">Create an Azure Blob storage account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="fd337-164">Para más información, consulte la sección Crear una cuenta de almacenamiento de [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="fd337-164">For details, see the Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="fd337-166">Configuración de una cuenta de Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="fd337-167">Suscríbase a Estudio de aprendizaje automático de Azure o inicie sesión en él desde la página [Aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) .</span><span class="sxs-lookup"><span data-stu-id="fd337-167">Sign up/into Azure Machine Learning Studio from the [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="fd337-168">Haga clic en el botón **Empiece ahora** y elija "Free Workspace" (Área de trabajo libre) o "Standard Workspace" (Área de trabajo estándar).</span><span class="sxs-lookup"><span data-stu-id="fd337-168">Click on the **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="fd337-169">Una vez hecho esto podrá crear experimentos en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-169">After this you will be able to create experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="fd337-170">Instalación de las herramientas de Azure Data Lake [recomendación]</span><span class="sxs-lookup"><span data-stu-id="fd337-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="fd337-171">Instale las herramientas de Azure Data Lake para su versión de Visual Studio desde [Azure Data Lake Tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)(Herramientas de Azure Data Lake para Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="fd337-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="fd337-173">Después de que la instalación finalice correctamente, abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd337-173">After the installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="fd337-174">Debería ver la pestaña Data Lake en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="fd337-174">You should see the Data Lake tab the menu at the top.</span></span> <span data-ttu-id="fd337-175">Los recursos de Azure deben aparecer en el panel izquierdo al iniciar sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-175">Your Azure resources should appear in the left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="the-nyc-taxi-trips-dataset"></a><span data-ttu-id="fd337-177">El conjunto de datos NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="fd337-177">The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="fd337-178">El conjunto de datos que usamos aquí está disponible públicamente, el [conjunto de datos NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="fd337-178">The data set we used here is a publicly available dataset -- the [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="fd337-179">El conjunto de datos NYC Taxi Trips consta de aproximadamente 20 GB de archivos de valores separados por comas (CSV) comprimidos (aproximadamente, 48 GB sin comprimir), que registran más de 173 millones de carreras individuales y las tarifas pagadas por cada carrera.</span><span class="sxs-lookup"><span data-stu-id="fd337-179">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="fd337-180">Cada registro de carrera incluye la hora y el lugar de recogida y llegada, el número de licencia del taxista anonimizado y el número de placa (número de identificación único del taxi).</span><span class="sxs-lookup"><span data-stu-id="fd337-180">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="fd337-181">Los datos cubren todos los viajes del año 2013 y se proporcionan en los dos conjuntos de datos siguientes para cada mes:</span><span class="sxs-lookup"><span data-stu-id="fd337-181">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

* <span data-ttu-id="fd337-182">El archivo CSV 'trip_data' contiene información detallada de las carreras, como el número de pasajeros, los puntos de recogida y destino, la duración de las carreras y la longitud del recorrido.</span><span class="sxs-lookup"><span data-stu-id="fd337-182">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="fd337-183">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd337-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="fd337-184">El archivo CSV 'trip_fare' contiene información detallada de la tarifa que se paga en cada carrera, como el tipo de pago, el importe de la tarifa, los suplementos e impuestos, las propinas y peajes, y el importe total pagado.</span><span class="sxs-lookup"><span data-stu-id="fd337-184">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="fd337-185">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd337-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="fd337-186">La clave única para unir trip\_data y trip\_fare se compone de los siguientes campos: medallion, hack\_license y pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="fd337-186">The unique key to join trip\_data and trip\_fare is composed of the following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="fd337-187">A los archivos CSV sin formato se puede acceder desde un blob de Almacenamiento de Azure público.</span><span class="sxs-lookup"><span data-stu-id="fd337-187">The raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="fd337-188">El script U-SQL para esta combinación está en la sección [Combinación de las tablas de carreras y tarifas](#join) .</span><span class="sxs-lookup"><span data-stu-id="fd337-188">The U-SQL script for this join is in the [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="fd337-189">Procesamiento de datos con U-SQL</span><span class="sxs-lookup"><span data-stu-id="fd337-189">Process data with U-SQL</span></span>
<span data-ttu-id="fd337-190">Las tareas de procesamiento de datos que se ilustran en esta sección incluyen el consumo, la comprobación de la calidad, la exploración y el muestreo de los datos.</span><span class="sxs-lookup"><span data-stu-id="fd337-190">The data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling the data.</span></span> <span data-ttu-id="fd337-191">También se muestra cómo combinar las tablas de carreras y tarifas.</span><span class="sxs-lookup"><span data-stu-id="fd337-191">We also show how to join trip and fare tables.</span></span> <span data-ttu-id="fd337-192">La sección final muestra cómo ejecutar un trabajo con scripts U-SQL desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-192">The final section shows run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="fd337-193">Estos son los vínculos a cada subsección:</span><span class="sxs-lookup"><span data-stu-id="fd337-193">Here are links to each subsection:</span></span>

* [<span data-ttu-id="fd337-194">Ingesta de datos: leer datos de un blob público</span><span class="sxs-lookup"><span data-stu-id="fd337-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="fd337-195">Comprobaciones de la calidad de los datos</span><span class="sxs-lookup"><span data-stu-id="fd337-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="fd337-196">Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="fd337-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="fd337-197">Combinación de las tablas de carreras y tarifas</span><span class="sxs-lookup"><span data-stu-id="fd337-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="fd337-198">Muestreo de datos</span><span class="sxs-lookup"><span data-stu-id="fd337-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="fd337-199">Ejecución de trabajos U-SQL</span><span class="sxs-lookup"><span data-stu-id="fd337-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="fd337-200">Los scripts U-SQL se describen aquí y se proporcionan en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="fd337-200">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="fd337-201">Los **scripts U-SQL** completos se pueden descargar de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="fd337-201">You can download the full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="fd337-202">Para ejecutar U-SQL, abra Visual Studio, haga clic en **Archivo --> Nuevo --> Proyecto**, elija **Proyecto U-SQL**, asígnele un nombre y guárdelo en una carpeta.</span><span class="sxs-lookup"><span data-stu-id="fd337-202">To execute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it to a folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="fd337-204">Se puede usar el Portal de Azure para ejecutar U-SQL en lugar de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd337-204">It is possible to use the Azure Portal to execute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="fd337-205">Puede ir hasta al recurso de Análisis de Azure Data Lake en el portal y enviar consultas directamente, como se muestra en la ilustración siguiente.</span><span class="sxs-lookup"><span data-stu-id="fd337-205">You can navigate to the Azure Data Lake Analytics resource on the portal and submit queries directly as illustrated in the following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="fd337-207"><a name="ingest"></a>Ingesta de datos: leer datos de un blob público</span><span class="sxs-lookup"><span data-stu-id="fd337-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="fd337-208">A la ubicación de los datos en el blob de Azure se hace referencia como **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** y puede extraerse mediante **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="fd337-208">The location of the data in the Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="fd337-209">Sustituya el nombre de su propio contenedor y el nombre de la cuenta de almacenamiento en los siguientes scripts por container_name@blob_storage_account_name en la dirección wasb.</span><span class="sxs-lookup"><span data-stu-id="fd337-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in the wasb address.</span></span> <span data-ttu-id="fd337-210">Dado que los nombres de archivo están en el mismo formato, podemos usar **trip\_data_{\*\}.csv** para leer los 12 archivos de carreras.</span><span class="sxs-lookup"><span data-stu-id="fd337-210">Since the file names are in same format, we can use **trip\_data_{\*\}.csv** to read in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="fd337-211">Dado que hay encabezados en la primera fila, es preciso quitar los encabezados y cambiar los tipos de columna por los apropiados.</span><span class="sxs-lookup"><span data-stu-id="fd337-211">Since there are headers in the first row, we need to remove the headers and change column types into appropriate ones.</span></span> <span data-ttu-id="fd337-212">Puede guardar los datos procesados en Azure Data Lake Storage mediante **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ o en la cuenta de Azure Blob Storage mediante **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span><span class="sxs-lookup"><span data-stu-id="fd337-212">We can either save the processed data to Azure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or to Azure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data to ADL
    OUTPUT @trip   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data to blob
    OUTPUT @trip   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="fd337-213">Del mismo modo podemos leer en los conjuntos de datos de tarifas.</span><span class="sxs-lookup"><span data-stu-id="fd337-213">Similarly we can read in the fare data sets.</span></span> <span data-ttu-id="fd337-214">Haga clic con el botón derecho en Azure Data Lake Store; puede elegir ver los datos en **Azure Portal --> Explorador de datos** o **Explorador de archivos** dentro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd337-214">Right click Azure Data Lake Store, you can choose to look at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="fd337-217"><a name="quality"></a>Comprobaciones de la calidad de los datos</span><span class="sxs-lookup"><span data-stu-id="fd337-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="fd337-218">Después de que se hayan leído las tablas de carreras y tarifas, las comprobaciones de la calidad de los datos pueden realizarse de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="fd337-218">After trip and fare tables have been read in, data quality checks can be done in the following way.</span></span> <span data-ttu-id="fd337-219">Los archivos CSV resultantes pueden ser la salida de Almacenamiento de blobs de Azure o de Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd337-219">The resulting CSV files can be output to Azure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="fd337-220">Busque el número de placas de licencia y un número único de placas de licencia:</span><span class="sxs-lookup"><span data-stu-id="fd337-220">Find the number of medallions and unique number of medallions:</span></span>

    ///check the number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="fd337-221">Busque las placas de licencia que tenían más de 100 carreras:</span><span class="sxs-lookup"><span data-stu-id="fd337-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="fd337-222">Busque los registros no válidos en términos de pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="fd337-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="fd337-223">Busque los valores que faltan en algunas variables:</span><span class="sxs-lookup"><span data-stu-id="fd337-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="fd337-224"><a name="explore"></a>Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="fd337-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="fd337-225">Podemos realizar una exploración de datos para comprenderlos mejor.</span><span class="sxs-lookup"><span data-stu-id="fd337-225">We can do some data exploration to get a better understanding of the data.</span></span>

<span data-ttu-id="fd337-226">Busque la distribución de las carreras con y sin propina:</span><span class="sxs-lookup"><span data-stu-id="fd337-226">Find the distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="fd337-227">Busque la distribución del importe de las propinas con valores límite: 0, 5, 10 y 20 dólares.</span><span class="sxs-lookup"><span data-stu-id="fd337-227">Find the distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="fd337-228">Busque las estadísticas básicas de la distancia de las carreras:</span><span class="sxs-lookup"><span data-stu-id="fd337-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="fd337-229">Busque los percentiles de la distancia de las carreras:</span><span class="sxs-lookup"><span data-stu-id="fd337-229">Find the percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="fd337-230"><a name="join"></a>Combinación de las tablas de carreras y tarifas</span><span class="sxs-lookup"><span data-stu-id="fd337-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="fd337-231">Las tablas de carreras y tarifas pueden combinarse por placa de licencia, hack_license y pickup_time.</span><span class="sxs-lookup"><span data-stu-id="fd337-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output to blob
    OUTPUT @model_data_full   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data to ADL
    OUTPUT @model_data_full   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="fd337-232">Para cada nivel de recuento de pasajeros, calcule el número de registros, el importe medio de la propina, la varianza del importe de la propina y el porcentaje de carreras con propina.</span><span class="sxs-lookup"><span data-stu-id="fd337-232">For each level of passenger count, calculate the number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="fd337-233"><a name="sample"></a>Muestreo de datos</span><span class="sxs-lookup"><span data-stu-id="fd337-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="fd337-234">En primer lugar, se selecciona aleatoriamente un 0,1 % de los datos de la tabla combinada:</span><span class="sxs-lookup"><span data-stu-id="fd337-234">First we randomly select 0.1% of the data from the joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="fd337-235">A continuación, se realiza un muestreo estratificado por la variable binaria tip_class:</span><span class="sxs-lookup"><span data-stu-id="fd337-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output to blob
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data to ADL
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="fd337-236"><a name="run"></a>Ejecución de trabajos U-SQL</span><span class="sxs-lookup"><span data-stu-id="fd337-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="fd337-237">Cuando termine la edición de los scripts U-SQL, puede enviarlos al servidor mediante su cuenta de Análisis de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd337-237">When you finish editing U-SQL scripts, you can submit them to the server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="fd337-238">Haga clic en **Data Lake**, **Enviar trabajo**, seleccione su **cuenta de Analytics**, elija **Paralelismo** y haga clic en el botón **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="fd337-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="fd337-240">Si el trabajo se cumple correctamente, su estado se mostrará en Visual Studio para su supervisión.</span><span class="sxs-lookup"><span data-stu-id="fd337-240">When the job is complied successfully, the status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="fd337-241">Cuando finalice la ejecución del trabajo, incluso puede reproducir el proceso de ejecución del trabajo y descubrir los pasos del cuello de botella para mejorar la eficacia del trabajo.</span><span class="sxs-lookup"><span data-stu-id="fd337-241">After the job finishes running, you can even replay the job execution process and find out the bottleneck steps to improve your job efficiency.</span></span> <span data-ttu-id="fd337-242">También puede ir al Portal de Azure para comprobar el estado de los trabajos U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fd337-242">You can also go to Azure Portal to check the status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="fd337-245">Ahora puede comprobar los archivos de salida en Almacenamiento de blobs de Azure o en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-245">Now you can check the output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="fd337-246">En el paso siguiente, utilizaremos los datos de ejemplo estratificado para nuestro modelo.</span><span class="sxs-lookup"><span data-stu-id="fd337-246">We will use the stratified sample data for our modeling in the next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="fd337-249">Generación e implementación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="fd337-250">Se demuestran las dos opciones disponibles para extraer datos e introducirlos en Aprendizaje automático de Azure para generar y</span><span class="sxs-lookup"><span data-stu-id="fd337-250">We demonstrate two options available for you to pull data into Azure Machine Learning to build and</span></span> 

* <span data-ttu-id="fd337-251">En la primera opción, usar los datos muestreados que se han escrito en un blob de Azure (en el paso anterior, **Muestreo de datos** ) y usar Python para generar e implementar modelos desde Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fd337-251">In the first option, you use the sampled data that has been written to an Azure Blob (in the **Data sampling** step above) and use Python to build and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="fd337-252">En la segunda opción, consultar los datos en Azure Data Lake directamente mediante una consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="fd337-252">In the second option, you query the data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="fd337-253">Para esta opción es necesario que cree un clúster de HDInsight o use uno existente en el que las tablas de Hive apunten a los datos de los taxis de Nueva York en Almacenamiento de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd337-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where the Hive tables point to the NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="fd337-254">Las dos opciones se explican a continuación.</span><span class="sxs-lookup"><span data-stu-id="fd337-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-to-build-and-deploy-machine-learning-models"></a><span data-ttu-id="fd337-255">Opción 1: Usar Python para generar e implementar modelos de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="fd337-255">Option 1: Use Python to build and deploy machine learning models</span></span>
<span data-ttu-id="fd337-256">Para generar e implementar modelos de aprendizaje automático con Python, cree un cuaderno de Jupyter Notebook en el equipo local o en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-256">To build and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="fd337-257">El cuaderno de Jupyter Notebook en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contiene el código completo que se explora, los datos que se visualizan y la ingeniería, el modelado y la implementación de características.</span><span class="sxs-lookup"><span data-stu-id="fd337-257">The Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains the full code to explore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="fd337-258">En este artículo se mostrarán solo los pasos de implementación y modelado.</span><span class="sxs-lookup"><span data-stu-id="fd337-258">In this article, we show just the modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="fd337-259">Importación de bibliotecas de Python</span><span class="sxs-lookup"><span data-stu-id="fd337-259">Import Python libraries</span></span>
<span data-ttu-id="fd337-260">Para ejecutar el cuaderno de Jupyter Notebook de ejemplo o el archivo de scripts de Python, se necesitan los siguientes paquetes Python.</span><span class="sxs-lookup"><span data-stu-id="fd337-260">In order to run the sample Jupyter Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="fd337-261">Si usa el servicio Notebook de Aprendizaje automático de Azure, estos paquetes ya están preinstalados.</span><span class="sxs-lookup"><span data-stu-id="fd337-261">If you are using the AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-the-data-from-blob"></a><span data-ttu-id="fd337-262">Lectura de los datos del blob</span><span class="sxs-lookup"><span data-stu-id="fd337-262">Read in the data from blob</span></span>
* <span data-ttu-id="fd337-263">Cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="fd337-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="fd337-264">Leer como texto</span><span class="sxs-lookup"><span data-stu-id="fd337-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds to read in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="fd337-266">Agregar nombres de columna y separar las columnas</span><span class="sxs-lookup"><span data-stu-id="fd337-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="fd337-267">Cambiar algunas columnas a numérico</span><span class="sxs-lookup"><span data-stu-id="fd337-267">Change some columns to numeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="fd337-268">Generación de modelos de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="fd337-268">Build machine learning models</span></span>
<span data-ttu-id="fd337-269">Aquí se crea un modelo de clasificación binaria para predecir si un viaje va a tener propina, o no.</span><span class="sxs-lookup"><span data-stu-id="fd337-269">Here we build a binary classification model to predict whether a trip is tipped or not.</span></span> <span data-ttu-id="fd337-270">En Jupyter Notebook puede encontrar otros dos modelos: clasificación multiclase y modelos de regresión.</span><span class="sxs-lookup"><span data-stu-id="fd337-270">In the Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="fd337-271">En primer lugar, es preciso crear variables ficticias que se puedan utilizar en modelos de scikit-learn</span><span class="sxs-lookup"><span data-stu-id="fd337-271">First we need to create dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="fd337-272">Crear la trama de datos para el modelado</span><span class="sxs-lookup"><span data-stu-id="fd337-272">Create data frame for the modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="fd337-273">División 60 - 40 de entrenamiento y pruebas</span><span class="sxs-lookup"><span data-stu-id="fd337-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="fd337-274">Regresión logística en conjunto de pruebas</span><span class="sxs-lookup"><span data-stu-id="fd337-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="fd337-275">Puntuar conjunto de datos de pruebas</span><span class="sxs-lookup"><span data-stu-id="fd337-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="fd337-276">Calcular métricas de evaluación</span><span class="sxs-lookup"><span data-stu-id="fd337-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="fd337-277">Generación de API de servicio web y su consumo en Python</span><span class="sxs-lookup"><span data-stu-id="fd337-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="fd337-278">Deseamos aplicar el modelo de aprendizaje automático una vez que se haya compilado.</span><span class="sxs-lookup"><span data-stu-id="fd337-278">We want to operationalize the machine learning model after it has been built.</span></span> <span data-ttu-id="fd337-279">Aquí usamos el modelo de logística binaria como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fd337-279">Here we use the binary logistic model as an example.</span></span> <span data-ttu-id="fd337-280">Asegúrese de que la versión de scikit-learn del equipo local es la 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="fd337-280">Make sure the scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="fd337-281">Si usa el servicio Estudio de aprendizaje automático de Azure, no es preciso que se preocupe de este tema.</span><span class="sxs-lookup"><span data-stu-id="fd337-281">You don't have to worry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="fd337-282">Busque las credenciales del área de trabajo en la configuración de Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="fd337-283">En Azure Machine Learning Studio, haga clic en **Configuración** --> **Nombre** --> **Tokens de autorización**.</span><span class="sxs-lookup"><span data-stu-id="fd337-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="fd337-285">Cree un servicio web</span><span class="sxs-lookup"><span data-stu-id="fd337-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="fd337-286">Obtenga las credenciales del servicio web</span><span class="sxs-lookup"><span data-stu-id="fd337-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="fd337-287">Llame a una API de servicio web.</span><span class="sxs-lookup"><span data-stu-id="fd337-287">Call Web service API.</span></span> <span data-ttu-id="fd337-288">Después del paso anterior tendrá que esperar entre 5 y 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="fd337-288">You have to wait 5-10 seconds after the previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="fd337-289">Opción 2: Crear e implementar modelos directamente en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="fd337-290">Estudio de aprendizaje automático de Azure puede leer datos directamente desde el Almacén de Azure Data Lake y después usarse para crear e implementar modelos.</span><span class="sxs-lookup"><span data-stu-id="fd337-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used to create and deploy models.</span></span> <span data-ttu-id="fd337-291">Este enfoque usa una tabla de Hive que apunta al Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd337-291">This approach uses a Hive table that points at the Azure Data Lake Store.</span></span> <span data-ttu-id="fd337-292">Para esto, es necesario aprovisionar un clúster de HDInsight de Azure independiente, en el que se crea la tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="fd337-292">This requires that a separate Azure HDInsight cluster be provisioned, on which the Hive table is created.</span></span> <span data-ttu-id="fd337-293">Se muestra cómo hacerlo en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="fd337-293">The following sections show how to do this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="fd337-294">Creación de un clúster de HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="fd337-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="fd337-295">Cree un clúster de HDInsight (Linux) desde [Azure Portal](http://portal.azure.com). Para más información, consulte la sección **Creación de un clúster de HDInsight con acceso a Azure Data Lake Store** del artículo [Creación de un clúster de HDInsight con Data Lake Store mediante Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd337-295">Create an HDInsight Cluster (Linux) from the [Azure Portal](http://portal.azure.com).For details, see the **Create an HDInsight cluster with access to Azure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="fd337-297">Creación de una tabla de Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd337-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="fd337-298">Ahora se crean tablas de Hive que se usarán en Estudio de aprendizaje automático de Azure en el clúster de HDInsight con los datos que se guardaron en el Almacén de Azure Data Lake en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="fd337-298">Now we create Hive tables to be used in Azure Machine Learning Studio in the HDInsight cluster using the data stored in Azure Data Lake Store in the previous step.</span></span> <span data-ttu-id="fd337-299">Vaya al clúster de HDInsight que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="fd337-299">Go to the HDInsight cluster just created.</span></span> <span data-ttu-id="fd337-300">Haga clic en **Configuración** --> **Propiedades** --> **Identidad de AAD del clúster** --> **Acceso a ADLS** y asegúrese de que su cuenta de Azure Data Lake Store se agrega a la lista con derechos de lectura, escritura y ejecución.</span><span class="sxs-lookup"><span data-stu-id="fd337-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in the list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="fd337-302">Luego, haga clic en **Panel**, junto al botón **Configuración**, y emergerá una ventana.</span><span class="sxs-lookup"><span data-stu-id="fd337-302">Then click **Dashboard** next to the **Settings** button and a window will pop up.</span></span> <span data-ttu-id="fd337-303">Haga clic en **Vista de Hive** en la esquina superior derecha de la página y verá el **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="fd337-303">Click **Hive View** in the upper right corner of the page and you will see the **Query Editor**.</span></span>

 ![20 |](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="fd337-306">Para crear una tabla, pegue los siguientes scripts de Hive.</span><span class="sxs-lookup"><span data-stu-id="fd337-306">Paste in the following Hive scripts to create a table.</span></span> <span data-ttu-id="fd337-307">La ubicación del origen de datos está en la referencia de Azure Data Lake Store de esta forma: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span><span class="sxs-lookup"><span data-stu-id="fd337-307">The location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="fd337-308">Cuando finalice la consulta, verá los resultados similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd337-308">When the query finishes running, you will see the results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="fd337-310">Generación e implementación de modelos en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="fd337-311">Ahora estamos preparados para generar e implementar con Aprendizaje automático de Azure un modelo que prediga si se paga o no propina.</span><span class="sxs-lookup"><span data-stu-id="fd337-311">We are now ready to build and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="fd337-312">Los datos de ejemplo estratificados están listos para usarse en este problema de clasificación binaria (propina o no).</span><span class="sxs-lookup"><span data-stu-id="fd337-312">The stratified sample data is ready to be used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="fd337-313">Los modelos predictivos que utilizan la clasificación de varias clases (tip_class) y la regresión (tip_amount) también se pueden generar e implementar con Estudio de aprendizaje automático de Azure. Sin embargo, aquí solo se muestra cómo hacerlo con el modelo de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="fd337-313">The predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how to handle the case using the binary classification model.</span></span>

1. <span data-ttu-id="fd337-314">Obtenga los datos e introdúzcalos en Azure ML mediante el módulo **Importar datos**, que se encuentra disponible en la sección **Entrada y salida de datos**.</span><span class="sxs-lookup"><span data-stu-id="fd337-314">Get the data into Azure ML using the **Import Data** module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="fd337-315">Para obtener más información, consulte la página de referencia sobre el módulo [Importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) .</span><span class="sxs-lookup"><span data-stu-id="fd337-315">For more information, see the [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="fd337-316">Seleccione **Consulta de Hive** como **Origen de datos** en el panel **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="fd337-316">Select **Hive Query** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="fd337-317">Pegue el siguiente script de Hive en el editor **Hive database query** (Consulta de base de datos de Hive).</span><span class="sxs-lookup"><span data-stu-id="fd337-317">Paste the following Hive script in the **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="fd337-318">Escriba el identificador URI del clúster de HDInsight (se encuentra en el Portal de Azure), las credenciales de Hadoop, la ubicación de los datos de salida y el nombre de contenedor, la clave o el nombre de la cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd337-318">Enter the URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="fd337-320">En la ilustración siguiente se muestra un ejemplo de un experimento de clasificación binaria que lee los datos directamente de la tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="fd337-320">An example of a binary classification experiment reading data from Hive table is shown in the figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="fd337-322">Una vez creado el experimento, haga clic en **Configurar servicio web** --> **Servicio web predictivo**</span><span class="sxs-lookup"><span data-stu-id="fd337-322">After the experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="fd337-324">Ejecute el experimento de puntuación creado automáticamente y, cuando haya terminado, haga clic en **Deploy Web Service**</span><span class="sxs-lookup"><span data-stu-id="fd337-324">Run the automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="fd337-326">Poco después se mostrará el panel del servicio web:</span><span class="sxs-lookup"><span data-stu-id="fd337-326">The web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="fd337-328">Resumen</span><span class="sxs-lookup"><span data-stu-id="fd337-328">Summary</span></span>
<span data-ttu-id="fd337-329">Al completar este tutorial, ha creado un entorno de ciencia de datos para generar soluciones completas escalables en Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd337-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="fd337-330">Este entorno se usó para analizar un conjunto de datos público grande. Para ello se recorrieron los pasos canónicos del proceso de ciencia de datos, desde la adquisición de datos y el entrenamiento del modelo hasta la implementación del modelo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="fd337-330">This environment was used to analyze a large public dataset, taking it through the canonical steps of the Data Science Process, from data acquisition through model training, and then to the deployment of the model as a web service.</span></span> <span data-ttu-id="fd337-331">Se usó U-SQL para procesar, explorar y muestrear los datos.</span><span class="sxs-lookup"><span data-stu-id="fd337-331">U-SQL was used to process, explore and sample the data.</span></span> <span data-ttu-id="fd337-332">Se utilizaron Python y Hive con Estudio de aprendizaje automático de Azure para generar e implementar modelos predictivos.</span><span class="sxs-lookup"><span data-stu-id="fd337-332">Python and Hive were used with Azure Machine Learning Studio to build and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="fd337-333">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd337-333">What's next?</span></span>
<span data-ttu-id="fd337-334">La ruta de aprendizaje del [proceso de ciencia de datos en equipos (TDSP)](http://aka.ms/datascienceprocess) proporciona vínculos a temas que describen cada paso del proceso de análisis avanzado.</span><span class="sxs-lookup"><span data-stu-id="fd337-334">The learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links to topics describing each step in the advanced analytics process.</span></span> <span data-ttu-id="fd337-335">Hay una serie de tutoriales en la página [Tutoriales del proceso de ciencia de datos en equipos](data-science-process-walkthroughs.md) que muestran cómo usar los recursos y servicios en diversos escenarios de análisis predictivo:</span><span class="sxs-lookup"><span data-stu-id="fd337-335">There are a series of walkthroughs itemized on the [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how to use resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="fd337-336">Proceso de ciencia de datos en equipos en acción: uso de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="fd337-336">The Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="fd337-337">Proceso de ciencia de datos en equipos en acción: uso de clústeres de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd337-337">The Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="fd337-338">Proceso de ciencia de datos en equipos: uso de SQL Server</span><span class="sxs-lookup"><span data-stu-id="fd337-338">The Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="fd337-339">Información general sobre el proceso de ciencia de datos con Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="fd337-339">Overview of the Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

