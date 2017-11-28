---
title: 'Ciencia de datos escalables con Azure Data Lake: tutorial completo | Microsoft Docs'
description: "¿Cómo toouse Azure Data Lake toodo datos exploración binario la clasificación y tareas en un conjunto de datos."
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
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="4616c-103">Ciencia de datos escalables con Azure Data Lake: tutorial completo</span><span class="sxs-lookup"><span data-stu-id="4616c-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="4616c-104">Este tutorial muestra cómo toouse la exploración de datos de Azure Data Lake toodo y tareas de clasificación binaria de una muestra de Hola NYC taxi tarifas y recorridos toopredict de conjunto de datos o no una sugerencia que se va a pagar por una tarifa.</span><span class="sxs-lookup"><span data-stu-id="4616c-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="4616c-105">Le guiará por los pasos de Hola de hello [proceso de ciencia de datos de equipo](http://aka.ms/datascienceprocess)-to- end, de entrenamiento de toomodel de adquisición de datos y, a continuación, la implementación de toohello de un servicio web que publica el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="4616c-106">Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="4616c-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="4616c-107">Hola [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) tiene todos los Hola capacidades necesario toomake más sencilla para datos científicos toostore cualquier tamaño, forma y velocidad y tooconduct de procesamiento de datos, análisis y modelado de aprendizaje de máquina avanzados con alta escalabilidad de una manera rentable.</span><span class="sxs-lookup"><span data-stu-id="4616c-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="4616c-108">Se paga por trabajo, solo cuando se procesan los datos.</span><span class="sxs-lookup"><span data-stu-id="4616c-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="4616c-109">Análisis de Azure Data Lake incluye U-SQL, un lenguaje que mezclas Hola naturaleza declarativa de SQL con expresivo de Hola de C# tooprovide escalable distribuye la capacidad de consulta.</span><span class="sxs-lookup"><span data-stu-id="4616c-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="4616c-110">Le permite tooprocess datos no estructurados mediante la aplicación de esquema en lectura, insertar lógica personalizada y definida por el usuario (UDF) las funciones e incluye extensibilidad tooenable específica un control exhaustivo sobre cómo tooexecute a escala.</span><span class="sxs-lookup"><span data-stu-id="4616c-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="4616c-111">toolearn más información acerca de la filosofía de diseño de hello detrás de T-SQL, consulte [entrada de blog de Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="4616c-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="4616c-112">Análisis de Data Lake es también una parte fundamental del conjunto de aplicaciones Cortana Analytics y funciona con Almacenamiento de datos SQL de Azure, Power BI y Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4616c-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="4616c-113">Esto proporciona una plataforma completa de análisis avanzado y macrodatos en la nube.</span><span class="sxs-lookup"><span data-stu-id="4616c-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="4616c-114">Este tutorial comienza con la descripción de los requisitos previos de Hola y recursos que son necesarios toocomplete Hola tareas con análisis de Data Lake que forman el proceso de ciencia de datos de Hola y cómo tooinstall ellos.</span><span class="sxs-lookup"><span data-stu-id="4616c-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="4616c-115">A continuación, se describen los pasos de procesamiento de datos de hello con U-SQL y concluye mostrándole cómo toouse Python y Hive con toobuild de estudio de aprendizaje automático de Azure e implementar modelos predictivos Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="4616c-116">U-SQL y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4616c-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="4616c-117">En este tutorial se recomienda el uso conjunto de datos de Visual Studio tooedit U-SQL scripts tooprocess Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="4616c-118">las secuencias de comandos de U-SQL de Hola están descritos aquí y proporcionan en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="4616c-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="4616c-119">proceso de Hello incluye ingesta en bloque, explorar y Hola datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="4616c-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="4616c-120">También muestra cómo toorun U T-SQL incluir en un script de trabajo de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="4616c-121">Se crean tablas de subárbol para los datos de hello en una generación de Hola de toofacilitate de clúster de HDInsight asociado y la implementación de un modelo de clasificación binaria en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="4616c-122">Python</span><span class="sxs-lookup"><span data-stu-id="4616c-122">Python</span></span>
<span data-ttu-id="4616c-123">En este tutorial también contiene una sección que muestra cómo toobuild e implementar un modelo de predicción mediante Python con estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="4616c-124">Proporcionamos Jupyter notebook con scripts de Python de Hola para estos pasos de este proceso.</span><span class="sxs-lookup"><span data-stu-id="4616c-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="4616c-125">Bloc de notas de Hello incluye código para algunos pasos de ingeniería de características adicionales y la construcción de modelos, como clasificación multiclase y regresión además modelado toohello modelo de clasificación binaria que se describen aquí.</span><span class="sxs-lookup"><span data-stu-id="4616c-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="4616c-126">tarea de regresión de Hello es la cantidad de Hola de toopredict de sugerencia de hello en función de otras características de sugerencia.</span><span class="sxs-lookup"><span data-stu-id="4616c-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="4616c-127">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-127">Azure Machine Learning</span></span>
<span data-ttu-id="4616c-128">Estudio de aprendizaje automático de Azure es toobuild usado e implementar los modelos de predicción de Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="4616c-129">Para esto se aplican dos enfoques: primero con scripts Python y después con tablas de Hive en un clúster de HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="4616c-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="4616c-130">Scripts</span><span class="sxs-lookup"><span data-stu-id="4616c-130">Scripts</span></span>
<span data-ttu-id="4616c-131">Solo los pasos principales Hola se describen en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4616c-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="4616c-132">Puede descargar Hola completa **script U-SQL** y **Jupyter Notebook** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="4616c-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4616c-133">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4616c-133">Prerequisites</span></span>
<span data-ttu-id="4616c-134">Antes de comenzar estos temas, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="4616c-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="4616c-135">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-135">An Azure subscription.</span></span> <span data-ttu-id="4616c-136">Si aún no tiene una, consulte [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)(Obtener una evaluación gratuita de Azure).</span><span class="sxs-lookup"><span data-stu-id="4616c-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4616c-137">[Recomendado] Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4616c-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="4616c-138">Si aún no tiene ninguna de estas versiones instaladas, puede descargar una versión gratuita de Community desde [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="4616c-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="4616c-139">En lugar de Visual Studio, también puede usar las consultas de hello Azure Portal toosubmit Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4616c-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="4616c-140">Se proporcionarán instrucciones acerca de cómo toodo así con Visual Studio y en el portal de hello en la sección de hello titulada **procesar datos con SQL U**.</span><span class="sxs-lookup"><span data-stu-id="4616c-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="4616c-141">Preparación del entorno de la ciencia de datos para Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="4616c-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="4616c-142">entorno de ciencia de datos tooprepare hello en este tutorial, cree Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4616c-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="4616c-143">Almacén de Azure Data Lake (ADLS)</span><span class="sxs-lookup"><span data-stu-id="4616c-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="4616c-144">Análisis de Azure Data Lake (ADLA)</span><span class="sxs-lookup"><span data-stu-id="4616c-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="4616c-145">Cuenta de Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-145">Azure Blob storage account</span></span>
* <span data-ttu-id="4616c-146">Cuenta de Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="4616c-147">Herramientas de Azure Data Lake para Visual Studio (se recomienda)</span><span class="sxs-lookup"><span data-stu-id="4616c-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="4616c-148">Esta sección proporciona instrucciones sobre cómo toocreate de estos recursos.</span><span class="sxs-lookup"><span data-stu-id="4616c-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="4616c-149">Si elige toouse tablas de Hive con aprendizaje automático de Azure, en lugar de Python, toobuild un modelo, también necesitará tooprovision un clúster de HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="4616c-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="4616c-150">Este procedimiento alternativo en descrito en hello sección apropiada.</span><span class="sxs-lookup"><span data-stu-id="4616c-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="4616c-151">Hola **almacén de Azure Data Lake** se pueden crear por separado o bien cuando cree hello **análisis de Azure Data Lake** como almacenamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="4616c-152">Se hace referencia a las instrucciones para crear cada uno de estos recursos por separado a continuación, pero Hola cuenta de almacenamiento de Data Lake no es necesario crear por separado.</span><span class="sxs-lookup"><span data-stu-id="4616c-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="4616c-153">Creación de un Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="4616c-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="4616c-154">Crear un ADLS de hello [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4616c-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="4616c-155">Para más información, consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4616c-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="4616c-156">Ser seguro tooset seguridad Hola identidad de AAD de clúster en hello **origen de datos** hoja de hello **configuración opcional** hoja descritos no existe.</span><span class="sxs-lookup"><span data-stu-id="4616c-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="4616c-158">Creación de una cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="4616c-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="4616c-159">Crear una cuenta ADLA de hello [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4616c-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="4616c-160">Para más información, consulte [Tutorial: Introducción a Análisis de Azure Data Lake mediante el Portal de Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4616c-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="4616c-162">Creación de una cuenta de Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="4616c-163">Crear una cuenta de almacenamiento de blobs de Azure de hello [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4616c-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="4616c-164">Para obtener más información, vea Hola crear una cuenta de almacenamiento sección [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4616c-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="4616c-166">Configuración de una cuenta de Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="4616c-167">Iniciar en estudio de aprendizaje automático de Azure de hello [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) página.</span><span class="sxs-lookup"><span data-stu-id="4616c-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="4616c-168">Haga clic en hello **empezar ahora** botón y, a continuación, elija un "Área de trabajo estándar" o "Área de trabajo gratuita".</span><span class="sxs-lookup"><span data-stu-id="4616c-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="4616c-169">Después de esto será capaz de toocreate experimentos en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="4616c-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="4616c-170">Instalación de las herramientas de Azure Data Lake [recomendación]</span><span class="sxs-lookup"><span data-stu-id="4616c-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="4616c-171">Instale las herramientas de Azure Data Lake para su versión de Visual Studio desde [Azure Data Lake Tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)(Herramientas de Azure Data Lake para Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="4616c-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="4616c-173">Una vez finalizada correctamente la instalación de hello, abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4616c-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="4616c-174">Debería ver el menú de Hola Hola Data Lake ficha en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="4616c-175">Los recursos de Azure deben aparecer en el panel izquierdo de hello cuando inicia sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="4616c-177">el conjunto de datos de Hello NYC Taxi viajes</span><span class="sxs-lookup"><span data-stu-id="4616c-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="4616c-178">Hello conjunto de datos se usa aquí es un conjunto de datos disponible públicamente--hello [conjunto de datos de Nueva York Taxi viajes](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="4616c-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="4616c-179">Hola datos NYC Taxi recorridos consta de unos 20GB de archivos comprimidos de CSV (sin comprimir de ~ 48GB), más de 173 millones de grabación hello y viajes individuales puntuación de pago para cada recorrido.</span><span class="sxs-lookup"><span data-stu-id="4616c-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="4616c-180">Cada registro de ida y vuelta incluye ubicaciones de recogida y entrega de Hola y tiempos, anónimos hack número de licencia (del controlador) y Hola número medallion (identificador único del taxi).</span><span class="sxs-lookup"><span data-stu-id="4616c-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="4616c-181">datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:</span><span class="sxs-lookup"><span data-stu-id="4616c-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="4616c-182">Hola 'trip_data' CSV contiene los detalles de ida y vuelta, como el número de los pasajeros, recogida y puntos de caída, duración de ida y vuelta y duración del viaje.</span><span class="sxs-lookup"><span data-stu-id="4616c-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="4616c-183">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4616c-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="4616c-184">Hello 'trip_fare' CSV contiene detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago.</span><span class="sxs-lookup"><span data-stu-id="4616c-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="4616c-185">Estos son algunos registros de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4616c-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="4616c-186">recorridos de toojoin de clave única de Hello\_datos y recorridos\_tarifa se compone de hello después de tres campos: medallion, prueba\_licencia y recogida\_fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="4616c-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="4616c-187">archivos CSV raw de Hello pueden tener acceso desde un blob de almacenamiento de Azure pública.</span><span class="sxs-lookup"><span data-stu-id="4616c-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="4616c-188">Hola script U-SQL para esta combinación es Hola [unir tablas de ida y vuelta y tarifa](#join) sección.</span><span class="sxs-lookup"><span data-stu-id="4616c-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="4616c-189">Procesamiento de datos con U-SQL</span><span class="sxs-lookup"><span data-stu-id="4616c-189">Process data with U-SQL</span></span>
<span data-ttu-id="4616c-190">las tareas de procesamiento de datos de Hello mostradas en esta sección incluyen ingesta en bloque, comprobar la calidad, explorar y Hola datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="4616c-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="4616c-191">También se muestran cómo toojoin de ida y vuelta y tarifa tablas.</span><span class="sxs-lookup"><span data-stu-id="4616c-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="4616c-192">sección final Hello muestra ejecución un trabajo de script U-SQL desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="4616c-193">Estos son vínculos tooeach subsección:</span><span class="sxs-lookup"><span data-stu-id="4616c-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="4616c-194">Ingesta de datos: leer datos de un blob público</span><span class="sxs-lookup"><span data-stu-id="4616c-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="4616c-195">Comprobaciones de la calidad de los datos</span><span class="sxs-lookup"><span data-stu-id="4616c-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="4616c-196">Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="4616c-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="4616c-197">Combinación de las tablas de carreras y tarifas</span><span class="sxs-lookup"><span data-stu-id="4616c-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="4616c-198">Muestreo de datos</span><span class="sxs-lookup"><span data-stu-id="4616c-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="4616c-199">Ejecución de trabajos U-SQL</span><span class="sxs-lookup"><span data-stu-id="4616c-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="4616c-200">las secuencias de comandos de U-SQL de Hola están descritos aquí y proporcionan en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="4616c-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="4616c-201">Puede descargar Hola completa **secuencias de comandos SQL U** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="4616c-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="4616c-202">tooexecute T-SQL, abra Visual Studio, haga clic en **archivo--> Nuevo--> proyecto**, elija **U-SQL proyecto**, nombre y guardar tooa carpeta.</span><span class="sxs-lookup"><span data-stu-id="4616c-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="4616c-204">Es posible toouse hello Azure Portal tooexecute U-SQL en lugar de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4616c-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="4616c-205">Puede navegar por los recursos de análisis de Azure Data Lake toohello en el portal de Hola y enviar consultas directamente, como se ilustra en la figura siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="4616c-207"><a name="ingest"></a>Ingesta de datos: leer datos de un blob público</span><span class="sxs-lookup"><span data-stu-id="4616c-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="4616c-208">ubicación de Hola de datos de Hola Hola blobs de Azure se hace referencia como  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  y puede extraerse mediante **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="4616c-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="4616c-209">Sustituir su propio nombre del contenedor y el nombre de cuenta de almacenamiento en los siguientes scripts para container_name@blob_storage_account_name en la dirección de wasb Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="4616c-210">Puesto que son nombres de archivo de hello en el mismo formato, podemos usar **recorridos\_data_ {\*\}.csv** tooread en todos los archivos de 12 de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="4616c-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

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

<span data-ttu-id="4616c-211">Dado que hay encabezados en la primera fila de hello, se necesitan encabezados de hello tooremove y cambiar los tipos de columna en las columnas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="4616c-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="4616c-212">Se puede guardar Hola procesa datos tooAzure datos Lake almacenamiento usando **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**cuenta de almacenamiento de blobs _ o tooAzure mediante  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="4616c-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

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

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="4616c-213">De igual forma podemos leer Hola tarifa en conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="4616c-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="4616c-214">Haga clic con el almacén de Azure Data Lake, puede elegir toolook de los datos **Portal de Azure--> Explorador de datos** o **Explorador de archivos** dentro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4616c-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="4616c-217"><a name="quality"></a>Comprobaciones de la calidad de los datos</span><span class="sxs-lookup"><span data-stu-id="4616c-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="4616c-218">Después de que se han leído tarifas y recorridos de tablas, comprobaciones de calidad de datos pueden realizarse en hello siguiente forma.</span><span class="sxs-lookup"><span data-stu-id="4616c-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="4616c-219">Hola resultante archivos CSV puede ser almacenamiento de blobs de salida tooAzure o almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4616c-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="4616c-220">Buscar el número de Hola de medallions y número único de medallions:</span><span class="sxs-lookup"><span data-stu-id="4616c-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="4616c-221">Busque las placas de licencia que tenían más de 100 carreras:</span><span class="sxs-lookup"><span data-stu-id="4616c-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="4616c-222">Busque los registros no válidos en términos de pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="4616c-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="4616c-223">Busque los valores que faltan en algunas variables:</span><span class="sxs-lookup"><span data-stu-id="4616c-223">Find missing values for some variables:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="4616c-224"><a name="explore"></a>Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="4616c-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="4616c-225">Podemos hacer una mejor comprensión de los datos de hello algunos tooget de exploración de datos.</span><span class="sxs-lookup"><span data-stu-id="4616c-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="4616c-226">Buscar distribución Hola de viajes superpuestos y no superpuesto de:</span><span class="sxs-lookup"><span data-stu-id="4616c-226">Find hello distribution of tipped and non-tipped trips:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="4616c-227">Buscar distribución Hola de cantidad de sugerencia con valores de corte: 0,5,10 y 20 dólares.</span><span class="sxs-lookup"><span data-stu-id="4616c-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="4616c-228">Busque las estadísticas básicas de la distancia de las carreras:</span><span class="sxs-lookup"><span data-stu-id="4616c-228">Find basic statistics of trip distance:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="4616c-229">Buscar percentiles Hola de distancia de ida y vuelta:</span><span class="sxs-lookup"><span data-stu-id="4616c-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="4616c-230"><a name="join"></a>Combinación de las tablas de carreras y tarifas</span><span class="sxs-lookup"><span data-stu-id="4616c-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="4616c-231">Las tablas de carreras y tarifas pueden combinarse por placa de licencia, hack_license y pickup_time.</span><span class="sxs-lookup"><span data-stu-id="4616c-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="4616c-232">Para cada nivel de recuento de pasajeros, calcule el número de Hola de registros, sugerencia promedio, la varianza de la cantidad de información sobre, porcentaje de viajes superpuestos de.</span><span class="sxs-lookup"><span data-stu-id="4616c-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="4616c-233"><a name="sample"></a>Muestreo de datos</span><span class="sxs-lookup"><span data-stu-id="4616c-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="4616c-234">En primer lugar se selecciona de forma aleatoria 0,1% de los datos de Hola Hola de tabla combinada:</span><span class="sxs-lookup"><span data-stu-id="4616c-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="4616c-235">A continuación, se realiza un muestreo estratificado por la variable binaria tip_class:</span><span class="sxs-lookup"><span data-stu-id="4616c-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="4616c-236"><a name="run"></a>Ejecución de trabajos U-SQL</span><span class="sxs-lookup"><span data-stu-id="4616c-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="4616c-237">Cuando termine de editar scripts SQL U, puede enviarlos a server toohello con su cuenta de análisis de Data Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="4616c-238">Haga clic en **Data Lake**, **Enviar trabajo**, seleccione su **cuenta de Analytics**, elija **Paralelismo** y haga clic en el botón **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="4616c-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="4616c-240">Cuando el trabajo de hello es considerado correctamente, estado de Hola de su trabajo se mostrará en Visual Studio para la supervisión.</span><span class="sxs-lookup"><span data-stu-id="4616c-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="4616c-241">Cuando finalice el trabajo de hello, puede que el proceso de ejecución reproducción Hola trabajo incluso y obtenga más información sobre Hola crear cuellos de botella pasos tooimprove la eficacia de su proceso de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4616c-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="4616c-242">También puede ir tooAzure estado de hello toocheck de Portal de los trabajos de SQL U.</span><span class="sxs-lookup"><span data-stu-id="4616c-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="4616c-245">Ahora puede comprobar los archivos de salida de hello en almacenamiento de blobs de Azure o Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="4616c-246">Datos de ejemplo de Hola estratificado se usará para el modelado en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="4616c-249">Generación e implementación de modelos en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="4616c-250">Se muestran dos opciones disponibles para que los datos de toopull en toobuild de aprendizaje automático de Azure y</span><span class="sxs-lookup"><span data-stu-id="4616c-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="4616c-251">En la primera opción hello, usa los datos de hello muestreada que se ha escrito tooan blobs de Azure (Hola **muestreo de datos** paso anterior) y usar Python toobuild e implementar modelos de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="4616c-252">En la segunda opción hello, consultar datos hello en Azure Data Lake directamente mediante una consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="4616c-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="4616c-253">Esta opción requiere que cree un nuevo clúster de HDInsight o use un clúster de HDInsight existente donde hello Hive tablas toohello de punto de datos de Nueva York Taxi datos Lake en almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="4616c-254">Las dos opciones se explican a continuación.</span><span class="sxs-lookup"><span data-stu-id="4616c-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="4616c-255">Opción 1: Uso de Python toobuild e implementar modelos de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="4616c-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="4616c-256">toobuild e implementar modelos de aprendizaje automático con Python, crear Jupyter Notebook en el equipo local o en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="4616c-257">Hello Jupyter Notebook proporcionada en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contiene Hola tooexplore de código completo, visualizar datos, ingeniería de característica, modelado y la implementación.</span><span class="sxs-lookup"><span data-stu-id="4616c-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="4616c-258">En este artículo, se muestran solo modelado Hola e implementación.</span><span class="sxs-lookup"><span data-stu-id="4616c-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="4616c-259">Importación de bibliotecas de Python</span><span class="sxs-lookup"><span data-stu-id="4616c-259">Import Python libraries</span></span>
<span data-ttu-id="4616c-260">Hola toorun de pedido de ejemplo Jupyter Notebook u Hola archivo de script de Python, hello siguientes Python paquetes son necesarios.</span><span class="sxs-lookup"><span data-stu-id="4616c-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="4616c-261">Si usas Hola servicio Bloc de notas de aprendizaje automático de Azure, estos paquetes se han instalado previamente.</span><span class="sxs-lookup"><span data-stu-id="4616c-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

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


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="4616c-262">Leer datos de Hola de blob</span><span class="sxs-lookup"><span data-stu-id="4616c-262">Read in hello data from blob</span></span>
* <span data-ttu-id="4616c-263">Cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="4616c-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="4616c-264">Leer como texto</span><span class="sxs-lookup"><span data-stu-id="4616c-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="4616c-266">Agregar nombres de columna y separar las columnas</span><span class="sxs-lookup"><span data-stu-id="4616c-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="4616c-267">Cambiar algunos toonumeric de columnas</span><span class="sxs-lookup"><span data-stu-id="4616c-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="4616c-268">Generación de modelos de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="4616c-268">Build machine learning models</span></span>
<span data-ttu-id="4616c-269">Este artículo se crea un toopredict de modelo de clasificación binaria si está superpuesto un viaje o no.</span><span class="sxs-lookup"><span data-stu-id="4616c-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="4616c-270">Hola Jupyter Notebook puede encontrar otros dos modelos: clasificación multiclase y los modelos de regresión.</span><span class="sxs-lookup"><span data-stu-id="4616c-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="4616c-271">Primero necesitamos toocreate variables ficticia que se pueden usar en scikit-Obtenga información acerca de los modelos</span><span class="sxs-lookup"><span data-stu-id="4616c-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="4616c-272">Crear la trama de datos para el modelado de Hola</span><span class="sxs-lookup"><span data-stu-id="4616c-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="4616c-273">División 60 - 40 de entrenamiento y pruebas</span><span class="sxs-lookup"><span data-stu-id="4616c-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="4616c-274">Regresión logística en conjunto de pruebas</span><span class="sxs-lookup"><span data-stu-id="4616c-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="4616c-275">Puntuar conjunto de datos de pruebas</span><span class="sxs-lookup"><span data-stu-id="4616c-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="4616c-276">Calcular métricas de evaluación</span><span class="sxs-lookup"><span data-stu-id="4616c-276">Calculate Evaluation metrics</span></span>
  
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

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="4616c-277">Generación de API de servicio web y su consumo en Python</span><span class="sxs-lookup"><span data-stu-id="4616c-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="4616c-278">Queremos que la máquina de hello toooperationalize modelo de aprendizaje después de que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="4616c-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="4616c-279">Aquí usamos modelo logística binaria de hello como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4616c-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="4616c-280">Asegúrese de que scikit Hola-Obtenga información acerca de la versión en el equipo local es 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="4616c-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="4616c-281">Tooworry sobre esto no es necesario si utiliza el servicio de Azure ML studio.</span><span class="sxs-lookup"><span data-stu-id="4616c-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="4616c-282">Busque las credenciales del área de trabajo en la configuración de Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="4616c-283">En Azure Machine Learning Studio, haga clic en **Configuración** --> **Nombre** --> **Tokens de autorización**.</span><span class="sxs-lookup"><span data-stu-id="4616c-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="4616c-285">Cree un servicio web</span><span class="sxs-lookup"><span data-stu-id="4616c-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="4616c-286">Obtenga las credenciales del servicio web</span><span class="sxs-lookup"><span data-stu-id="4616c-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="4616c-287">Llame a una API de servicio web.</span><span class="sxs-lookup"><span data-stu-id="4616c-287">Call Web service API.</span></span> <span data-ttu-id="4616c-288">Tener toowait entre 5 y 10 segundos después del paso anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="4616c-289">Opción 2: Crear e implementar modelos directamente en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="4616c-290">Estudio de aprendizaje automático de Azure puede leer los datos directamente desde el almacén de Azure Data Lake y, a continuación, puede toocreate usado e implementar modelos.</span><span class="sxs-lookup"><span data-stu-id="4616c-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="4616c-291">Este enfoque utiliza una tabla de Hive que apunta al almacén de Azure Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="4616c-292">Esto requiere que se aprovisiona un clúster de HDInsight de Azure diferente, en qué Hola subárbol se crea la tabla.</span><span class="sxs-lookup"><span data-stu-id="4616c-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="4616c-293">Hola siguientes secciones muestran cómo toodo esto.</span><span class="sxs-lookup"><span data-stu-id="4616c-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="4616c-294">Creación de un clúster de HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="4616c-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="4616c-295">Crear un clúster de HDInsight (Linux) de hello [Portal de Azure](http://portal.azure.com). Para obtener más información, vea hello **crear un clúster de HDInsight con acceso tooAzure almacén de Data Lake** sección [crear un clúster de HDInsight con el almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4616c-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="4616c-297">Creación de una tabla de Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4616c-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="4616c-298">Ahora creamos Hive tablas toobe usar en el estudio de aprendizaje automático de Azure en clúster de HDInsight de hello mediante datos de hello almacenados en el almacén de Azure Data Lake en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="4616c-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="4616c-299">Vaya toohello acaba de crear el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4616c-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="4616c-300">Haga clic en **configuración** --> **propiedades** --> **clúster identidad AAD** --> **acceso a ADLS**, Asegúrese de que se agrega la cuenta de almacén de Azure Data Lake en lista de hello con lectura, escritura y ejecución derechos.</span><span class="sxs-lookup"><span data-stu-id="4616c-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="4616c-302">A continuación, haga clic en **panel** toohello siguiente **configuración** botón y una ventana se abrirá.</span><span class="sxs-lookup"><span data-stu-id="4616c-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="4616c-303">Haga clic en **vista Hive** Hola esquina superior derecha de la página de Hola y se verán hello **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="4616c-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20 |](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="4616c-306">Pegar en hello después toocreate de scripts de Hive una tabla.</span><span class="sxs-lookup"><span data-stu-id="4616c-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="4616c-307">Hola de origen de datos se encuentra en la referencia de almacén de Azure Data Lake de esta manera: **adl://data_lake_store_name.azuredatalakestore.net:443/nombreCarpeta/nombre_archivo**.</span><span class="sxs-lookup"><span data-stu-id="4616c-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

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


<span data-ttu-id="4616c-308">Cuando finaliza la ejecución de consultas de hello, verá resultados de hello similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4616c-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="4616c-310">Generación e implementación de modelos en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="4616c-311">Se está ahora listo toobuild e implementa un modelo que predice si no se le paga una sugerencia con aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="4616c-312">datos de ejemplo estratificado Hello están listo toobe utilizado en esta clasificación binaria (sugerencia o no) problema.</span><span class="sxs-lookup"><span data-stu-id="4616c-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="4616c-313">Hola modelos predictivos con clasificación multiclase (tip_class) y regresión (tip_amount) también se generó e implantó estudio de aprendizaje automático de Azure, pero sólo le mostramos cómo usar casos de toohandle Hola Hola modelo de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="4616c-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="4616c-314">Obtener datos de hello en aprendizaje automático de Azure con hello **importar datos** módulo, disponibles en hello **datos de entrada y salida** sección.</span><span class="sxs-lookup"><span data-stu-id="4616c-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="4616c-315">Para obtener más información, vea hello [módulo importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) página de referencia.</span><span class="sxs-lookup"><span data-stu-id="4616c-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="4616c-316">Seleccione **consulta de Hive** como hello **origen de datos** en hello **propiedades** panel.</span><span class="sxs-lookup"><span data-stu-id="4616c-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="4616c-317">Hola pegar después de script de Hive en hello **consulta de base de datos de Hive** editor</span><span class="sxs-lookup"><span data-stu-id="4616c-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="4616c-318">Escriba el clúster de URI de HDInsight de hello (Esto puede encontrarse en el Portal de Azure), las credenciales de Hadoop, ubicación de datos de salida y el nombre de contenedor/nombre/clave de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4616c-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="4616c-320">En la figura de Hola a continuación se muestra un ejemplo de un experimento de clasificación binaria leer los datos de tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="4616c-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="4616c-322">Una vez creado el experimento de hello, haga clic en **configurar el servicio de Web** --> **predictivo servicio Web**</span><span class="sxs-lookup"><span data-stu-id="4616c-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="4616c-324">La puntuación del experimento, cuando termine, haga clic en ejecución Hola crea automáticamente **implementar el servicio de Web**</span><span class="sxs-lookup"><span data-stu-id="4616c-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="4616c-326">panel del servicio web Hola aparecerá en breve:</span><span class="sxs-lookup"><span data-stu-id="4616c-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="4616c-328">Resumen</span><span class="sxs-lookup"><span data-stu-id="4616c-328">Summary</span></span>
<span data-ttu-id="4616c-329">Al completar este tutorial, ha creado un entorno de ciencia de datos para generar soluciones completas escalables en Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4616c-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="4616c-330">Este entorno fue tooanalyze usa un conjunto de datos público grande, vamos a través de pasos canónica Hola Hola proceso de ciencia de datos, de adquisición de datos a través de entrenamiento del modelo, y, a continuación, modelo de implementación toohello de hello como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="4616c-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="4616c-331">U-SQL era tooprocess usado, explorar y Hola datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4616c-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="4616c-332">Python y Hive usan con toobuild de estudio de aprendizaje automático de Azure e implementación modelos de predicción.</span><span class="sxs-lookup"><span data-stu-id="4616c-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="4616c-333">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4616c-333">What's next?</span></span>
<span data-ttu-id="4616c-334">ruta de acceso de aprendizaje de Hola la [proceso de ciencia de datos de equipo (TDSP)](http://aka.ms/datascienceprocess) proporciona tootopics de vínculos que describen cada uno paso a paso Hola avanzada de proceso de análisis.</span><span class="sxs-lookup"><span data-stu-id="4616c-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="4616c-335">Hay una serie de tutoriales que se detallan en hello [tutoriales de proceso de ciencia de datos de equipo](data-science-process-walkthroughs.md) página ese showcase cómo toouse recursos y servicios en varios escenarios de análisis predictivos:</span><span class="sxs-lookup"><span data-stu-id="4616c-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="4616c-336">Hola proceso de ciencia de datos de equipo en acción: con almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="4616c-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="4616c-337">Hola proceso de ciencia de datos de equipo en acción: uso de clústeres de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="4616c-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="4616c-338">Hola proceso de ciencia de datos de equipo: uso de SQL Server</span><span class="sxs-lookup"><span data-stu-id="4616c-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="4616c-339">Información general del uso de proceso de ciencia de datos de hello inspirará en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4616c-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

