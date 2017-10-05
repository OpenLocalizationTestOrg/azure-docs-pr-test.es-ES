---
title: "Proceso de ciencia de datos en equipos en acción: uso de un clúster de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB | Microsoft Docs"
description: "Uso del proceso de ciencia de datos en equipos en un escenario completo con un clúster de Hadoop de HDInsight para crear e implementar un modelo con un conjunto de datos disponible públicamente de gran tamaño (1 TB)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 8e6143bca819c9a0484221f8b4feb319aaaa73f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="0031e-103">Proceso de ciencia de datos en equipos en acción: uso de un clúster de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB</span><span class="sxs-lookup"><span data-stu-id="0031e-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="0031e-104">En este tutorial, se describe cómo usar el proceso de ciencia de datos en equipos en un escenario completo con un [clúster de Hadoop de Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) para almacenar, explorar y estudiar sus características desde el punto de vista de los ingenieros y reducir los datos de ejemplo de uno de los conjuntos de datos de [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) que están disponibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="0031e-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="0031e-105">Usamos Aprendizaje automático de Azure para crear un modelo de clasificación binaria con estos datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-105">We use Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="0031e-106">Asimismo, se muestra cómo publicar uno de estos modelos como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="0031e-106">We also show how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="0031e-107">También es posible usar un cuaderno de iPython para realizar las tareas que se presentan en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0031e-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="0031e-108">Los usuarios que deseen probar este método deben consultar el tema [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) (tutorial de Criteo con una conexión de ODBC de Hive).</span><span class="sxs-lookup"><span data-stu-id="0031e-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="0031e-109"><a name="dataset"></a>Descripción del conjunto de datos de Criteo</span><span class="sxs-lookup"><span data-stu-id="0031e-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="0031e-110">Los datos de Criteo son un conjunto de datos de predicción de clics que ocupan aproximadamente 370 GB de archivos TSV comprimidos en gzip (1,3 TB aproximadamente sin comprimir). Constan de más de 4300 millones de registros.</span><span class="sxs-lookup"><span data-stu-id="0031e-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="0031e-111">Estos datos proceden de 24 días de datos de clics que ofrece [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="0031e-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="0031e-112">Para facilitar el trabajo de los científicos que estudian los datos, hemos descomprimido los datos disponibles para nosotros a fin de experimentar con ellos.</span><span class="sxs-lookup"><span data-stu-id="0031e-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span></span>

<span data-ttu-id="0031e-113">Cada registro de este conjunto de datos contiene 40 columnas:</span><span class="sxs-lookup"><span data-stu-id="0031e-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="0031e-114">La primera columna es una columna de etiqueta que indica si un usuario hace clic en un **anuncio** (valor 1) o si no hace clic (valor 0)</span><span class="sxs-lookup"><span data-stu-id="0031e-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="0031e-115">Las 13 columnas siguientes son numéricas.</span><span class="sxs-lookup"><span data-stu-id="0031e-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="0031e-116">Las últimas 26 son columnas de categorías.</span><span class="sxs-lookup"><span data-stu-id="0031e-116">last 26 are categorical columns</span></span>

<span data-ttu-id="0031e-117">Las columnas son anónimas y utilizan una serie de nombres enumerados: desde "Col1" (para la columna de etiqueta) hasta 'Col40 "(para la última columna de categoría).</span><span class="sxs-lookup"><span data-stu-id="0031e-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="0031e-118">Este es un extracto de las 20 primeras columnas de dos observaciones (filas) de este conjunto de datos:</span><span class="sxs-lookup"><span data-stu-id="0031e-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="0031e-119">Hay valores que faltan en las columnas numéricas y de categorías de este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="0031e-120">A continuación, se describe un método sencillo para controlar los valores que faltan.</span><span class="sxs-lookup"><span data-stu-id="0031e-120">We describe a simple method for handling the missing values.</span></span> <span data-ttu-id="0031e-121">Más adelante, se describen detalles adicionales de los datos cuando se almacenen en tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0031e-121">Additional details of the data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="0031e-122">**Definición:** *Porcentaje de clics (CTR, del inglés Click-through rate):* es el porcentaje de clics que se hacen en los datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="0031e-123">En este conjunto de datos de Criteo, el valor de CTR es aproximadamente del 3,3 % (o 0,033).</span><span class="sxs-lookup"><span data-stu-id="0031e-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="0031e-124"><a name="mltasks"></a>Ejemplos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="0031e-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="0031e-125">En este tutorial, se describen dos problemas de predicción de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0031e-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="0031e-126">**Clasificación binaria**: predice si un usuario ha hecho clic o no en un anuncio:</span><span class="sxs-lookup"><span data-stu-id="0031e-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="0031e-127">Clase 0: no hace clic.</span><span class="sxs-lookup"><span data-stu-id="0031e-127">Class 0: No Click</span></span>
   * <span data-ttu-id="0031e-128">Clase 1: sí hace clic.</span><span class="sxs-lookup"><span data-stu-id="0031e-128">Class 1: Click</span></span>
2. <span data-ttu-id="0031e-129">**Regresión**: predice la probabilidad de que se haga clic en un anuncio en función de las características del usuario.</span><span class="sxs-lookup"><span data-stu-id="0031e-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <span data-ttu-id="0031e-130"><a name="setup"></a>Configuración de un clúster de Hadoop de HDInsight para la ciencia de los datos</span><span class="sxs-lookup"><span data-stu-id="0031e-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="0031e-131">**Nota:** Esta tarea la suelen hacer los **administradores**.</span><span class="sxs-lookup"><span data-stu-id="0031e-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="0031e-132">Configure su entorno de ciencia de datos de Azure para crear soluciones de análisis predictivos con los clústeres de HDInsight en tres pasos:</span><span class="sxs-lookup"><span data-stu-id="0031e-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="0031e-133">[Cree una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md): esta cuenta de almacenamiento se utiliza para almacenar datos en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="0031e-134">Los datos utilizados en los clústeres de HDInsight se almacenan aquí.</span><span class="sxs-lookup"><span data-stu-id="0031e-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="0031e-135">[Personalice los clústeres de Hadoop de HDInsight de Azure para la ciencia de los datos](machine-learning-data-science-customize-hadoop-cluster.md): en este paso, se crea un clúster de Hadoop de HDInsight de Azure con Anaconda Python 2.7 de 64 bits instalado en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="0031e-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="0031e-136">Hay que llevar a cabo dos pasos importantes (descritos en este tema) para personalizar el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0031e-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="0031e-137">Hay que vincular la cuenta de almacenamiento que creó en el paso 1 con el clúster de HDInsight en el momento de su creación.</span><span class="sxs-lookup"><span data-stu-id="0031e-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="0031e-138">Esta cuenta de almacenamiento se utiliza para tener acceso a datos que se pueden procesar en el clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="0031e-139">Debe habilitar el acceso remoto en el nodo principal del clúster después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="0031e-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="0031e-140">Recuerde las credenciales de acceso remoto que especifique aquí (distintas de las especificadas para el clúster durante su creación), ya que las necesitará para realizar los procedimientos a continuación.</span><span class="sxs-lookup"><span data-stu-id="0031e-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="0031e-141">[Cree un área de trabajo de Aprendizaje automático (ML) de Azure](machine-learning-create-workspace.md): esta área de trabajo de Aprendizaje automático de Azure se usa para generar modelos de Aprendizaje automático después de una exploración de datos inicial y una reducción de su tamaño en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0031e-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <span data-ttu-id="0031e-142"><a name="getdata"></a>Obtención y consumo de datos desde un origen público</span><span class="sxs-lookup"><span data-stu-id="0031e-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="0031e-143">Para acceder al conjunto de datos de [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) , haga clic en el vínculo, acepte las condiciones de uso y especifique un nombre.</span><span class="sxs-lookup"><span data-stu-id="0031e-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="0031e-144">Aquí se muestra una instantánea de esta pantalla:</span><span class="sxs-lookup"><span data-stu-id="0031e-144">A snapshot of what this looks like is shown here:</span></span>

![Aceptar los términos de Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="0031e-146">Haga clic en **Continue to download** (Continuar la descarga) para más información sobre el conjunto de datos y su disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="0031e-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="0031e-147">Los datos residen en una ubicación pública de [Azure Blob Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md): wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="0031e-147">The data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="0031e-148">"wasb" hace referencia a la ubicación de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="0031e-149">Los datos de este almacenamiento de blobs público constan de tres subcarpetas de datos sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="0031e-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="0031e-150">La subcarpeta *raw/count/* contiene los primeros 21 días de datos, desde day\_00 hasta day\_20</span><span class="sxs-lookup"><span data-stu-id="0031e-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="0031e-151">La subcarpeta *raw/train/* consta de un único día de datos, day\_21</span><span class="sxs-lookup"><span data-stu-id="0031e-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="0031e-152">La subcarpeta *raw/test/* consta de dos días de datos, day\_22 y day\_23</span><span class="sxs-lookup"><span data-stu-id="0031e-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="0031e-153">Para aquellos que quieran empezar con los datos gzip sin formato, podrán encontrar estos datos también en la carpeta principal *raw/*, como day_NN.gz, donde NN es un valor entre 00 y 23.</span><span class="sxs-lookup"><span data-stu-id="0031e-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="0031e-154">Más adelante en este tutorial, al hablar de la creación de tablas de Hive, se expone un enfoque alternativo para acceder a estos datos, explorarlos y modelarlos que no requiere ninguna descarga local.</span><span class="sxs-lookup"><span data-stu-id="0031e-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="0031e-155"><a name="login"></a>Inicio de sesión en el nodo principal del clúster</span><span class="sxs-lookup"><span data-stu-id="0031e-155"><a name="login"></a>Log in to the cluster headnode</span></span>
<span data-ttu-id="0031e-156">Para iniciar sesión en el nodo principal del clúster, utilice [Azure Portal](https://ms.portal.azure.com) para buscar el clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="0031e-157">Haga clic en el icono del elefante de HDInsight a la izquierda y, a continuación, haga doble clic en el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="0031e-158">Navegue hasta la pestaña **Configuration** (Configuración), haga doble clic en el icono Connect (Conectar), situado en la parte inferior de la página, y escriba las credenciales de acceso remoto cuando se le soliciten.</span><span class="sxs-lookup"><span data-stu-id="0031e-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="0031e-159">Así accederá al nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="0031e-160">Esto es lo que se ve normalmente al iniciar sesión por primera vez en el nodo principal del clúster:</span><span class="sxs-lookup"><span data-stu-id="0031e-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![Iniciar sesión en el clúster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="0031e-162">A la izquierda, vemos el icono de "Hadoop Command Line" (Línea de comandos de Hadoop), que será nuestra herramienta de trabajo para explorar los datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="0031e-163">También vemos dos direcciones URL útiles: "Hadoop Yarn Status" (Estado de Hadoop Yarn) y "Hadoop Name Node" (Nombre del nodo de Hadoop).</span><span class="sxs-lookup"><span data-stu-id="0031e-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="0031e-164">La dirección URL del estado de Yarn muestra el progreso del trabajo, mientras que la URL del nombre del nodo proporciona detalles sobre la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="0031e-165">Ya contamos con la configuración adecuada y estamos listos para comenzar la primera parte del tutorial, que es la exploración de datos mediante Hive y la preparación de estos para el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="0031e-166"><a name="hive-db-tables"></a> Creación de tablas y base de datos de Hive</span><span class="sxs-lookup"><span data-stu-id="0031e-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="0031e-167">Para crear tablas de Hive para nuestro conjunto de datos de Criteo, abra la ***Línea de comandos de Hadoop*** en el escritorio del nodo principal y especifique el directorio de Hive con este comando:</span><span class="sxs-lookup"><span data-stu-id="0031e-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="0031e-168">Ejecute todos los comandos de Hive que aparecen en este tutorial desde el símbolo del sistema del directorio bin/ de Hive.</span><span class="sxs-lookup"><span data-stu-id="0031e-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="0031e-169">De esta manera, cualquier problema con la ruta de acceso se soluciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0031e-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="0031e-170">Utilizaremos indistintamente los términos "símbolo del sistema del directorio de Hive", "símbolo del sistema del directorio bin/ de Hive" y "línea de comandos de Hadoop".</span><span class="sxs-lookup"><span data-stu-id="0031e-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="0031e-171">Para ejecutar cualquier consulta de Hive, siempre se pueden utilizar los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="0031e-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="0031e-172">Después de que aparezca Hive REPL con un signo "hive >", solo tendrá que cortar y pegar la consulta para ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="0031e-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="0031e-173">El código siguiente crea una base de datos "criteo" y, a continuación, genera 4 tablas:</span><span class="sxs-lookup"><span data-stu-id="0031e-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="0031e-174">una *tabla para generar recuentos*, correspondientes a los días desde day\_00 a day\_20,</span><span class="sxs-lookup"><span data-stu-id="0031e-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="0031e-175">una *tabla que se usa como el conjunto de datos "train"*, correspondiente a day\_21, y</span><span class="sxs-lookup"><span data-stu-id="0031e-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="0031e-176">dos *tablas que se usan como los conjuntos de datos de prueba* correspondientes a day\_22 y day\_23, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0031e-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="0031e-177">Dividimos nuestro conjunto de datos de prueba en dos tablas distintas porque uno de los días es festivo y queremos determinar si el modelo puede detectar las diferencias entre un día festivo y uno laborable a partir del porcentaje de clics.</span><span class="sxs-lookup"><span data-stu-id="0031e-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span></span>

<span data-ttu-id="0031e-178">Para mayor comodidad, el script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0031e-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="0031e-179">Observamos que todas estas tablas son externas ya que simplemente señalan a ubicaciones de almacenamiento de blobs de Azure (wasb).</span><span class="sxs-lookup"><span data-stu-id="0031e-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="0031e-180">**Hay dos maneras de ejecutar todas las consultas de Hive mencionadas.**</span><span class="sxs-lookup"><span data-stu-id="0031e-180">**There are two ways to execute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="0031e-181">**Usar la línea de comandos de REPL de Hive**: el primer método consiste en emitir un comando "hive" y, a continuación, copiar la consulta y pegarla en la línea de comandos de REPL de Hive.</span><span class="sxs-lookup"><span data-stu-id="0031e-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="0031e-182">Para ello, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0031e-182">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="0031e-183">Ahora, en la línea de comandos de REPL, la consulta se ejecuta al cortarla y pegarla.</span><span class="sxs-lookup"><span data-stu-id="0031e-183">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="0031e-184">**Guardar las consultas en un archivo y ejecutar el comando**: el segundo método consiste en guardar las consultas en un archivo .hql ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) y, después, emitir el comando siguiente para ejecutar la consulta:</span><span class="sxs-lookup"><span data-stu-id="0031e-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="0031e-185">Confirmación de la creación de la tabla y la base de datos</span><span class="sxs-lookup"><span data-stu-id="0031e-185">Confirm database and table creation</span></span>
<span data-ttu-id="0031e-186">A continuación, confirmamos la creación de la base de datos con el comando siguiente desde el símbolo del sistema del directorio bin/ de Hive:</span><span class="sxs-lookup"><span data-stu-id="0031e-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="0031e-187">Este es el resultado:</span><span class="sxs-lookup"><span data-stu-id="0031e-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="0031e-188">Esto confirma la creación de la nueva base de datos, "criteo".</span><span class="sxs-lookup"><span data-stu-id="0031e-188">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="0031e-189">Para ver qué tablas hemos creado, simplemente emitimos este comando desde el símbolo del sistema del directorio bin/ de Hive:</span><span class="sxs-lookup"><span data-stu-id="0031e-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="0031e-190">Se mostrará el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="0031e-190">We then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="0031e-191"><a name="exploration"></a> Exploración de datos en Hive</span><span class="sxs-lookup"><span data-stu-id="0031e-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="0031e-192">Ahora estamos preparados hacer algunas exploraciones de datos básicas en Hive.</span><span class="sxs-lookup"><span data-stu-id="0031e-192">Now we are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="0031e-193">Comenzamos contando el número de ejemplos de las tablas de datos "train" y "test".</span><span class="sxs-lookup"><span data-stu-id="0031e-193">We begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="0031e-194">Número de ejemplos de "train"</span><span class="sxs-lookup"><span data-stu-id="0031e-194">Number of train examples</span></span>
<span data-ttu-id="0031e-195">El contenido de [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0031e-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="0031e-196">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="0031e-197">Como alternativa, también se puede emitir el comando siguiente desde el símbolo del sistema del directorio bin/ de Hive:</span><span class="sxs-lookup"><span data-stu-id="0031e-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="0031e-198">Número de ejemplos de "test" en los dos conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="0031e-198">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="0031e-199">Ahora vamos a contar el número de ejemplos que hay en los dos conjuntos de datos "test".</span><span class="sxs-lookup"><span data-stu-id="0031e-199">We now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="0031e-200">El contenido de [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0031e-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="0031e-201">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="0031e-202">Como es habitual, también podemos llamar al script desde el símbolo del sistema del directorio bin/ de Hive emitiendo el comando:</span><span class="sxs-lookup"><span data-stu-id="0031e-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="0031e-203">Por último, examinamos el número de ejemplos de prueba que hay en el conjunto de datos "test" basado en day\_23.</span><span class="sxs-lookup"><span data-stu-id="0031e-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="0031e-204">El comando para hacer esto es similar al anterior (vea [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="0031e-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="0031e-205">Este es el resultado:</span><span class="sxs-lookup"><span data-stu-id="0031e-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="0031e-206">Distribución de etiquetas en el conjunto de datos "train"</span><span class="sxs-lookup"><span data-stu-id="0031e-206">Label distribution in the train dataset</span></span>
<span data-ttu-id="0031e-207">La distribución de etiquetas del conjunto de datos "train" es interesante.</span><span class="sxs-lookup"><span data-stu-id="0031e-207">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="0031e-208">Para verlo, mostramos el contenido de [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="0031e-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="0031e-209">De esta forma, obtenemos la distribución de etiquetas:</span><span class="sxs-lookup"><span data-stu-id="0031e-209">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="0031e-210">Tenga en cuenta que el porcentaje de las etiquetas positivas es del 3,3 % (coherente con el conjunto de datos original).</span><span class="sxs-lookup"><span data-stu-id="0031e-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="0031e-211">Distribuciones del histograma de algunas variables numéricas en el conjunto de datos "train"</span><span class="sxs-lookup"><span data-stu-id="0031e-211">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="0031e-212">Podemos usar la función nativa de Hive "histogram\_numeric" para conocer el aspecto de la distribución de las variables numéricas.</span><span class="sxs-lookup"><span data-stu-id="0031e-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="0031e-213">El contenido de [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql) es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0031e-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="0031e-214">El resultado es este:</span><span class="sxs-lookup"><span data-stu-id="0031e-214">This yields the following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="0031e-215">La combinación "LATERAL VIEW - explode" en Hive sirve para producir un resultado similar a SQL en lugar de la lista habitual.</span><span class="sxs-lookup"><span data-stu-id="0031e-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="0031e-216">Tenga en cuenta que, en esta tabla, la primera columna corresponde al centro de bin y la segunda, a la frecuencia de bin.</span><span class="sxs-lookup"><span data-stu-id="0031e-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="0031e-217">Percentiles aproximados de algunas de las variables numéricas del conjunto de datos "train"</span><span class="sxs-lookup"><span data-stu-id="0031e-217">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="0031e-218">Con respecto a las variables numéricas, también es interesante el cálculo de los percentiles aproximados.</span><span class="sxs-lookup"><span data-stu-id="0031e-218">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="0031e-219">La función nativa de Hive "percentile\_approx" permite realizar esta acción.</span><span class="sxs-lookup"><span data-stu-id="0031e-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="0031e-220">El contenido de [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0031e-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="0031e-221">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="0031e-222">Observamos que la distribución de los percentiles suele estar estrechamente relacionada con la distribución de histograma de cualquier variable numérica.</span><span class="sxs-lookup"><span data-stu-id="0031e-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="0031e-223">Búsqueda del número de valores únicos para algunas columnas de categorías en el conjunto de datos "train"</span><span class="sxs-lookup"><span data-stu-id="0031e-223">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="0031e-224">Continuamos con la exploración de datos y ahora vamos a buscar el número de valores únicos que adoptan algunas columnas de categorías.</span><span class="sxs-lookup"><span data-stu-id="0031e-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="0031e-225">Para ello, mostramos el contenido de [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="0031e-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="0031e-226">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="0031e-227">Tenga en cuenta que Col15 tiene 19 millones de valores únicos.</span><span class="sxs-lookup"><span data-stu-id="0031e-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="0031e-228">Usar técnicas simples como la codificación "one-hot" para codificar estas variables de categorías tan altamente dimensionales no es viable.</span><span class="sxs-lookup"><span data-stu-id="0031e-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="0031e-229">En particular, vamos a explicar y mostrar una técnica eficaz y contundente llamada [Aprendizaje con recuentos](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) para hacer frente a este problema de forma eficaz.</span><span class="sxs-lookup"><span data-stu-id="0031e-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="0031e-230">Terminamos esta subsección examinando también el número de valores únicos de algunas otras columnas de categorías.</span><span class="sxs-lookup"><span data-stu-id="0031e-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="0031e-231">El contenido de [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0031e-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="0031e-232">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="0031e-233">De nuevo vemos que, excepto Col20, todas las demás columnas tienen muchos valores únicos.</span><span class="sxs-lookup"><span data-stu-id="0031e-233">Again we see that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="0031e-234">Recuentos de aparición conjunta de pares de variables de categorías en el conjunto de datos "train"</span><span class="sxs-lookup"><span data-stu-id="0031e-234">Co-occurrence counts of pairs of categorical variables in the train dataset</span></span>

<span data-ttu-id="0031e-235">Los recuentos de aparición conjunta de pares de variables de categorías también son interesantes.</span><span class="sxs-lookup"><span data-stu-id="0031e-235">The co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="0031e-236">Esto se puede determinar con el código de [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="0031e-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="0031e-237">Hemos invertido el orden de los recuentos en función de su aparición y mostramos los 15 primeros en este caso.</span><span class="sxs-lookup"><span data-stu-id="0031e-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="0031e-238">El resultado obtenido es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0031e-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="0031e-239"><a name="downsample"></a> Reducción del tamaño de los conjuntos de datos para el Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="0031e-239"><a name="downsample"></a> Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="0031e-240">Una vez que hemos explorado los conjuntos de datos y que hemos mostrado cómo se hace este tipo de exploración sobre cualquier variable (incluidas las combinaciones), ahora vamos a reducir el tamaño de los conjuntos de datos para que se puedan crear modelos en el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="0031e-241">Recuerde que el problema en el que nos centramos es el siguiente: considerando un conjunto de atributos de ejemplo (valores de las características desde Col2 hasta Col40), vamos a predecir si Col1 tendrá un valor 0 (no se hace clic) o un valor 1 (sí se hace clic).</span><span class="sxs-lookup"><span data-stu-id="0031e-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="0031e-242">Para reducir el tamaño de los conjuntos de datos "train" y "test" al 1 % del tamaño original, utilizamos la función RAND() nativa de Hive.</span><span class="sxs-lookup"><span data-stu-id="0031e-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="0031e-243">El siguiente script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql), nos permite hacerlo con el conjunto de datos "train":</span><span class="sxs-lookup"><span data-stu-id="0031e-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="0031e-244">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="0031e-245">El script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) permite hacerlo con los datos de "test", en concreto, en day\_22:</span><span class="sxs-lookup"><span data-stu-id="0031e-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="0031e-246">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="0031e-247">Por último, el script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) permite hacerlo con los datos de "test", en concreto, en day\_23:</span><span class="sxs-lookup"><span data-stu-id="0031e-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="0031e-248">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="0031e-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="0031e-249">De esta forma, estamos listos para usar nuestros conjuntos de datos "train" y "test" con el tamaño reducido para crear modelos en el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="0031e-250">Hay un componente importante final antes de pasar al Aprendizaje automático de Azure, que es la preocupación con la tabla de recuento.</span><span class="sxs-lookup"><span data-stu-id="0031e-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span></span> <span data-ttu-id="0031e-251">En la siguiente subsección, se trata este tema con más detalle.</span><span class="sxs-lookup"><span data-stu-id="0031e-251">In the next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="0031e-252"><a name="count"></a> Breve explicación sobre la tabla de recuento</span><span class="sxs-lookup"><span data-stu-id="0031e-252"><a name="count"></a> A brief discussion on the count table</span></span>
<span data-ttu-id="0031e-253">Como hemos visto, algunas variables de categorías tienen una dimensionalidad muy alta.</span><span class="sxs-lookup"><span data-stu-id="0031e-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="0031e-254">En nuestro tutorial, presentamos una técnica eficaz denominada [Aprendizaje con recuentos](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) para codificar estas variables de una manera eficiente y robusta.</span><span class="sxs-lookup"><span data-stu-id="0031e-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="0031e-255">Para obtener más información sobre esta técnica, acceda al vínculo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="0031e-255">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="0031e-256">En este tutorial, nos centramos en el uso de las tablas de recuento para producir representaciones compactas de características de categorías con una alta dimensionalidad.</span><span class="sxs-lookup"><span data-stu-id="0031e-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="0031e-257">Esta no es la única manera de codificar características de las categorías. Para más información sobre otras técnicas, los usuarios interesados pueden ver la información sobre la [codificación "one-hot"](http://en.wikipedia.org/wiki/One-hot) y la [aplicación de hash a las características](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="0031e-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="0031e-258">Para crear tablas de recuento en los datos de recuento, se utilizan los datos de la carpeta raw/count.</span><span class="sxs-lookup"><span data-stu-id="0031e-258">To build count tables on the count data, we use the data in the folder raw/count.</span></span> <span data-ttu-id="0031e-259">En la sección de modelado, mostramos a los usuarios cómo crear estas tablas de recuento para características de categorías desde cero, así como a utilizar una tabla de recuento pregenerada para sus exploraciones.</span><span class="sxs-lookup"><span data-stu-id="0031e-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="0031e-260">En lo sucesivo, cuando nos referimos a las "tablas de recuento pregeneradas", nos referimos a usar las tablas de recuento proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="0031e-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span></span> <span data-ttu-id="0031e-261">En la siguiente sección encontrará instrucciones detalladas sobre cómo obtener acceso a estas tablas.</span><span class="sxs-lookup"><span data-stu-id="0031e-261">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <span data-ttu-id="0031e-262"><a name="aml"></a> Creación de modelos con el Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="0031e-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="0031e-263">Nuestro proceso de creación de modelos con Azure Machine Learning consta de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0031e-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="0031e-264">Obtención de los datos a partir de las tablas de Hive para el Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="0031e-264">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="0031e-265">Creación del experimento: limpieza de los datos y caracterización con tablas de recuento</span><span class="sxs-lookup"><span data-stu-id="0031e-265">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="0031e-266">Crear, entrenar y puntuar el modelo</span><span class="sxs-lookup"><span data-stu-id="0031e-266">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="0031e-267">Evaluación del modelo</span><span class="sxs-lookup"><span data-stu-id="0031e-267">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="0031e-268">Publicación del modelo como un servicio web</span><span class="sxs-lookup"><span data-stu-id="0031e-268">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="0031e-269">Ahora estamos preparados para generar modelos en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-269">Now we are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="0031e-270">Nuestros datos con tamaño reducido están guardados como tablas de Hive en el clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-270">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="0031e-271">Usaremos el módulo **Importar datos** de Azure Machine Learning para leer estos datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-271">We use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="0031e-272">Las credenciales para acceder a la cuenta de almacenamiento de este clúster se proporcionan a continuación.</span><span class="sxs-lookup"><span data-stu-id="0031e-272">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="0031e-273"><a name="step1"></a> Paso 1: Obtención de los datos a partir de las tablas de Hive para Azure Machine Learning usando el módulo Importar datos y seleccionándolo para un experimento de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="0031e-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="0031e-274">Para empezar, seleccione **+NUEVO** -> **EXPERIMENTO** -> **Experimento en blanco**.</span><span class="sxs-lookup"><span data-stu-id="0031e-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="0031e-275">A continuación, en el cuadro **Búsqueda** , en la parte superior izquierda, busque "Importar datos".</span><span class="sxs-lookup"><span data-stu-id="0031e-275">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="0031e-276">Arrastre y coloque el módulo **Importar datos** en el lienzo del experimento (la parte central de la pantalla) para usar el módulo para acceder a los datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="0031e-277">Este es el aspecto del módulo **Importar datos** mientas está obteniendo los datos de la tabla de Hive:</span><span class="sxs-lookup"><span data-stu-id="0031e-277">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![Importar datos obtiene los datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="0031e-279">Para el módulo **Importar datos** , los valores de los parámetros que se proporcionan en el gráfico son solo algunos ejemplos del tipo de valores que tiene que proporcionar.</span><span class="sxs-lookup"><span data-stu-id="0031e-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="0031e-280">A continuación se ofrecen algunas instrucciones generales acerca de cómo rellenar el conjunto de parámetros para el módulo **Importar datos** .</span><span class="sxs-lookup"><span data-stu-id="0031e-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="0031e-281">Elija "Consulta de Hive" como **Origen de datos**</span><span class="sxs-lookup"><span data-stu-id="0031e-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="0031e-282">En el cuadro **Consulta de base de datos de Hive**, basta con seleccionar SELECT * FROM <nombre\_base\_datos.nombre\_tabla\_>.</span><span class="sxs-lookup"><span data-stu-id="0031e-282">In the **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="0031e-283">**URI del servidor de Hcatalog**: si el clúster es "abc", este valor simplemente será: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="0031e-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="0031e-284">**Nombre de la cuenta de usuario de Hadoop**: el nombre de usuario elegido en el momento de dar de alta el clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="0031e-285">(No es el nombre de usuario de acceso remoto).</span><span class="sxs-lookup"><span data-stu-id="0031e-285">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="0031e-286">**Contraseña de la cuenta de usuario de Hadoop**: la contraseña de usuario elegida en el momento de dar de alta el clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="0031e-287">(NO es la contraseña de acceso remoto).</span><span class="sxs-lookup"><span data-stu-id="0031e-287">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="0031e-288">**Ubicación de los datos de salida**: elija "Azure".</span><span class="sxs-lookup"><span data-stu-id="0031e-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="0031e-289">**Nombre de la cuenta de almacenamiento de Azure**: la cuenta de almacenamiento asociada al clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-289">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="0031e-290">**Clave de la cuenta de almacenamiento de Azure**: la clave de almacenamiento asociada al clúster.</span><span class="sxs-lookup"><span data-stu-id="0031e-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="0031e-291">**Nombre del contenedor de Azure**: si el nombre de clúster es "abc", este campo suele ser simplemente "abc".</span><span class="sxs-lookup"><span data-stu-id="0031e-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="0031e-292">Una vez que el módulo **Importar datos** finaliza la obtención de datos (aparece una marca de verificación verde en el módulo), guarde estos datos como un conjunto de datos (con el nombre que desee).</span><span class="sxs-lookup"><span data-stu-id="0031e-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="0031e-293">Este es el aspecto:</span><span class="sxs-lookup"><span data-stu-id="0031e-293">What this looks like:</span></span>

![Importar datos guarda los datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="0031e-295">Haga clic con el botón derecho en el puerto de salida del módulo **Importar datos** .</span><span class="sxs-lookup"><span data-stu-id="0031e-295">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="0031e-296">Se muestran las opciones **Guardar como conjunto de datos** y **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="0031e-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="0031e-297">Si se hace clic en la opción **Visualize** (Visualizar), se muestran 100 filas de los datos, junto con un panel derecho que es útil para algunas estadísticas de resumen.</span><span class="sxs-lookup"><span data-stu-id="0031e-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="0031e-298">Para guardar los datos, simplemente seleccione **Save as dataset** (Guardar como conjunto de datos) y siga las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="0031e-298">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="0031e-299">Para seleccionar el conjunto de datos guardado para usarlo en un experimento de aprendizaje automático, busque los conjuntos de datos usando el cuadro **Búsqueda** que se muestra en la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="0031e-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="0031e-300">A continuación, escriba parcialmente el nombre que asignó al conjunto de datos para acceder a él y arrastre el conjunto de datos hasta el panel principal.</span><span class="sxs-lookup"><span data-stu-id="0031e-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="0031e-301">Al depositarlo en el panel principal, se selecciona para su uso en el modelado de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="0031e-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![Movimiento de arrastre del conjunto de datos hasta el panel principal](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="0031e-303">Realice esta acción para los conjuntos de datos "test" y "train".</span><span class="sxs-lookup"><span data-stu-id="0031e-303">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="0031e-304">Además, recuerde usar el nombre de la base de datos y los nombres de tabla que ha asignado para este propósito.</span><span class="sxs-lookup"><span data-stu-id="0031e-304">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="0031e-305">Los valores usados en la ilustración tienen únicamente fines ilustrativos.**</span><span class="sxs-lookup"><span data-stu-id="0031e-305">The values used in the figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="0031e-306"><a name="step2"></a> Paso 2: creación de un experimento sencillo en el estudio de Aprendizaje automático de Azure para predecir los clics y los "no clics"</span><span class="sxs-lookup"><span data-stu-id="0031e-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="0031e-307">Nuestro experimento de Azure Machine Learning tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="0031e-307">Our Azure ML experiment looks like this:</span></span>

![Experimento de Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="0031e-309">Ahora examinaremos los componentes clave de este experimento.</span><span class="sxs-lookup"><span data-stu-id="0031e-309">We now examine the key components of this experiment.</span></span> <span data-ttu-id="0031e-310">Como recordatorio, tenemos que arrastrar nuestros conjuntos de datos train y test a nuestro lienzo de experimento antes.</span><span class="sxs-lookup"><span data-stu-id="0031e-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="0031e-311">Limpiar datos que faltan</span><span class="sxs-lookup"><span data-stu-id="0031e-311">Clean Missing Data</span></span>
<span data-ttu-id="0031e-312">El módulo **Limpiar datos que faltan** hace lo que sugiere su nombre: limpia los datos que faltan siguiendo el método que especifique el usuario.</span><span class="sxs-lookup"><span data-stu-id="0031e-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="0031e-313">En este módulo, veremos estos datos:</span><span class="sxs-lookup"><span data-stu-id="0031e-313">Looking into this module, we see this:</span></span>

![Limpiar datos que faltan](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="0031e-315">Aquí, hemos optado por reemplazar todos los valores que faltan por un 0.</span><span class="sxs-lookup"><span data-stu-id="0031e-315">Here, we chose to replace all missing values with a 0.</span></span> <span data-ttu-id="0031e-316">Hay otras opciones, que se pueden ver al mirar las listas desplegables del módulo.</span><span class="sxs-lookup"><span data-stu-id="0031e-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="0031e-317">Diseño de características para los datos</span><span class="sxs-lookup"><span data-stu-id="0031e-317">Feature engineering on the data</span></span>
<span data-ttu-id="0031e-318">Puede haber millones de valores únicos para algunas características de categoría de grandes conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="0031e-319">El uso de métodos simples como la codificación "one-hot" para representar estas características de categorías no es viable.</span><span class="sxs-lookup"><span data-stu-id="0031e-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="0031e-320">En este tutorial, se muestran cómo usar las características de recuento mediante módulos de Aprendizaje automático de Azure integrados para generar representaciones compactas de estas variables de categorías con una alta dimensionalidad.</span><span class="sxs-lookup"><span data-stu-id="0031e-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="0031e-321">El resultado final es un tamaño de modelo más pequeño, tiempos de formación más rápidos y métricas de rendimiento bastante similares a usar otras técnicas.</span><span class="sxs-lookup"><span data-stu-id="0031e-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="0031e-322">Creación de transformaciones de recuento</span><span class="sxs-lookup"><span data-stu-id="0031e-322">Building counting transforms</span></span>
<span data-ttu-id="0031e-323">Para crear características de recuento, usamos el módulo **Crear transformación de recuento** , que está disponible en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="0031e-324">El módulo tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="0031e-324">The module looks like this:</span></span>

<span data-ttu-id="0031e-325">![Módulo Crear transformación de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Módulo Crear transformación de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="0031e-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0031e-326">En el cuadro **Recuento de columnas**, especificamos las columnas en las que queremos realizar recuentos.</span><span class="sxs-lookup"><span data-stu-id="0031e-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span></span> <span data-ttu-id="0031e-327">Normalmente, son columnas de categorías con una alta dimensionalidad (tal y como se mencionó).</span><span class="sxs-lookup"><span data-stu-id="0031e-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="0031e-328">Al principio, hemos mencionado que el conjunto de datos de Criteo tiene 26 columnas de categorías: de Col15 a Col40.</span><span class="sxs-lookup"><span data-stu-id="0031e-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="0031e-329">En este caso, contamos en todas ellas y les damos sus índices (de 15 a 40 separados por comas, como se muestra).</span><span class="sxs-lookup"><span data-stu-id="0031e-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="0031e-330">Para usar el módulo en el modo MapReduce (adecuado para grandes conjuntos de datos), se necesita acceso a un clúster de Hadoop de HDInsight (el que se usa para la exploración de categorías se puede reutilizar para este propósito) y sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="0031e-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="0031e-331">En las ilustraciones anteriores se muestra el aspecto de los valores rellenados (reemplace los valores de ejemplo por los que son relevantes para su propio caso de uso).</span><span class="sxs-lookup"><span data-stu-id="0031e-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![Parámetros del módulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="0031e-333">En la ilustración anterior, se muestra cómo especificar la ubicación del blob de entrada.</span><span class="sxs-lookup"><span data-stu-id="0031e-333">In the figure above, we show how to enter the input blob location.</span></span> <span data-ttu-id="0031e-334">Esta ubicación tiene los datos reservados para la creación de tablas de recuento.</span><span class="sxs-lookup"><span data-stu-id="0031e-334">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="0031e-335">Cuando finalice este módulo, se puede guardar la transformación para más adelante haciendo clic con el botón derecho en el módulo y seleccionando la opción **Save as Transform** (Guardar como transformación):</span><span class="sxs-lookup"><span data-stu-id="0031e-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

![Opción "Guardar como transformación"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="0031e-337">En nuestra arquitectura de experimento antes mostrada, el conjunto de datos "ytransform2" corresponde exactamente a una transformación de recuento guardada.</span><span class="sxs-lookup"><span data-stu-id="0031e-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="0031e-338">Para el resto de este experimento, se considera que el lector usó un módulo **Crear transformación de recuento** con algunos datos para generar recuentos y, a continuación, puede usar estos recuentos para generar características de recuento en los conjuntos de datos train y test.</span><span class="sxs-lookup"><span data-stu-id="0031e-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="0031e-339">Elección de las características de recuento que se incluirán como parte de los conjuntos de datos train y test</span><span class="sxs-lookup"><span data-stu-id="0031e-339">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="0031e-340">Una vez que tenemos una transformación de recuento lista, el usuario puede elegir las características que desea incluir en los conjuntos de datos train y test mediante el módulo **Modificar parámetros de la tabla de recuentos** .</span><span class="sxs-lookup"><span data-stu-id="0031e-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="0031e-341">Mostramos este módulo a continuación solo para ofrecer una visión completa, pero para simplificar no lo usamos en nuestro experimento.</span><span class="sxs-lookup"><span data-stu-id="0031e-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Parámetros de la tabla de modificación de recuentos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="0031e-343">En este caso, como se puede ver, hemos elegido usar solo las probabilidades e ignorar la columna de retroceso.</span><span class="sxs-lookup"><span data-stu-id="0031e-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span></span> <span data-ttu-id="0031e-344">También podemos establecer parámetros como el umbral de ubicación de elementos no utilizados, cuántos ejemplos anteriores agregar para el suavizado y si se usa cualquier ruido Laplacian o no.</span><span class="sxs-lookup"><span data-stu-id="0031e-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="0031e-345">Todas estas son características avanzadas y es conveniente tener en cuenta que los valores predeterminados son un buen punto de partida para los usuarios que no están familiarizados con este tipo de generación de características.</span><span class="sxs-lookup"><span data-stu-id="0031e-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="0031e-346">Transformación de datos antes de generar las características de recuento</span><span class="sxs-lookup"><span data-stu-id="0031e-346">Data transformation before generating the count features</span></span>
<span data-ttu-id="0031e-347">Ahora nos centraremos en un punto importante acerca de cómo transformar los datos de train y test antes de generar realmente las características de recuento.</span><span class="sxs-lookup"><span data-stu-id="0031e-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="0031e-348">Tenga en cuenta que hay dos módulos **Ejecutar script R** usados antes de aplicar la transformación de recuentos a nuestros datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span></span>

![Ejecución de módulos de script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="0031e-350">Este es el primer script R:</span><span class="sxs-lookup"><span data-stu-id="0031e-350">Here is the first R script:</span></span>

![Primer script de R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="0031e-352">En este script R, cambiamos nuestras columnas a los nombres de "Col1" a "Col40".</span><span class="sxs-lookup"><span data-stu-id="0031e-352">In this R script, we rename our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="0031e-353">Esto es así porque la transformación de recuentos espera nombres con este formato.</span><span class="sxs-lookup"><span data-stu-id="0031e-353">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="0031e-354">En el segundo script R, para equilibrar la distribución entre clases positivas y negativas (clases 1 y 0 respectivamente) reducimos la resolución de la clase negativa.</span><span class="sxs-lookup"><span data-stu-id="0031e-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span></span> <span data-ttu-id="0031e-355">El siguiente script R muestra cómo hacerlo:</span><span class="sxs-lookup"><span data-stu-id="0031e-355">The R script here shows how to do this:</span></span>

![Segundo script de R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="0031e-357">En este script R simple, se usa "pos\_neg\_ratio" para establecer la cantidad de equilibrio entre las clases positiva y negativa.</span><span class="sxs-lookup"><span data-stu-id="0031e-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="0031e-358">Es importante hacerlo, ya que mejorar el desequilibrio entre clases normalmente tiene ventajas de rendimiento para los problemas de clasificación en los que la distribución de las clases se había sesgado (recuerde que en nuestro caso, tenemos una clase positiva del 3,3% y una clase negativa del 96,7%).</span><span class="sxs-lookup"><span data-stu-id="0031e-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="0031e-359">Aplicación de la transformación de recuentos a nuestros datos</span><span class="sxs-lookup"><span data-stu-id="0031e-359">Applying the count transformation on our data</span></span>
<span data-ttu-id="0031e-360">Por último, podemos usar el módulo **Aplicar transformación** para aplicar las transformaciones de recuentos a nuestros conjuntos de datos train y test.</span><span class="sxs-lookup"><span data-stu-id="0031e-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="0031e-361">Este módulo toma la transformación de recuentos guardada como una entrada y los conjuntos de datos train o test como la otra entrada, y devuelve datos con características de recuento.</span><span class="sxs-lookup"><span data-stu-id="0031e-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="0031e-362">Se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0031e-362">It is shown here:</span></span>

![Módulo Aplicar transformación](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="0031e-364">Un extracto del aspecto de las características de recuento</span><span class="sxs-lookup"><span data-stu-id="0031e-364">An excerpt of what the count features look like</span></span>
<span data-ttu-id="0031e-365">Es instructivo para ver el aspecto de las características de recuento en nuestro caso.</span><span class="sxs-lookup"><span data-stu-id="0031e-365">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="0031e-366">Aquí se muestra un extracto de esto:</span><span class="sxs-lookup"><span data-stu-id="0031e-366">Here we show an excerpt of this:</span></span>

![Características de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="0031e-368">En este extracto, se muestra que para las columnas en las que se ha hecho el recuento, se obtienen los recuentos y probabilidades, además de cualquier retroceso pertinente.</span><span class="sxs-lookup"><span data-stu-id="0031e-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="0031e-369">Ahora estamos listos para crear un modelo de Aprendizaje automático de Azure con estos conjuntos de datos transformados.</span><span class="sxs-lookup"><span data-stu-id="0031e-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="0031e-370">En la siguiente sección, veremos cómo se puede hacer esto.</span><span class="sxs-lookup"><span data-stu-id="0031e-370">In the next section, we show how this can be done.</span></span>

### <span data-ttu-id="0031e-371"><a name="step3"></a>Paso 3: Creación, entrenamiento y puntuación del modelo</span><span class="sxs-lookup"><span data-stu-id="0031e-371"><a name="step3"></a> Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="0031e-372">Elección del aprendiz</span><span class="sxs-lookup"><span data-stu-id="0031e-372">Choice of learner</span></span>
<span data-ttu-id="0031e-373">En primer lugar, tenemos que elegir un aprendiz.</span><span class="sxs-lookup"><span data-stu-id="0031e-373">First, we need to choose a learner.</span></span> <span data-ttu-id="0031e-374">Vamos a usar como nuestro aprendiz un árbol de decisiones incrementado de dos clases.</span><span class="sxs-lookup"><span data-stu-id="0031e-374">We are going to use a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="0031e-375">Aquí están las opciones predeterminadas para este aprendiz:</span><span class="sxs-lookup"><span data-stu-id="0031e-375">Here are the default options for this learner:</span></span>

![Parámetros de árbol de decisiones incrementados de dos clases](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="0031e-377">Para nuestro experimento elegiremos los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="0031e-377">For our experiment, we are going to choose the default values.</span></span> <span data-ttu-id="0031e-378">Tenemos en cuenta que los valores predeterminados son normalmente significativos y una buena forma de obtener las líneas base rápidas del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0031e-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="0031e-379">Puede mejorar el rendimiento mediante el barrido de parámetros si elige hacerlo una vez que tenga una línea base.</span><span class="sxs-lookup"><span data-stu-id="0031e-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="0031e-380">Entrenamiento del modelo</span><span class="sxs-lookup"><span data-stu-id="0031e-380">Train the model</span></span>
<span data-ttu-id="0031e-381">Para el entrenamiento, simplemente invocamos un módulo **Entrenar modelo** .</span><span class="sxs-lookup"><span data-stu-id="0031e-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="0031e-382">Las dos entradas son el aprendiz de árbol de decisión incrementado de dos clases y nuestro conjunto de datos train.</span><span class="sxs-lookup"><span data-stu-id="0031e-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="0031e-383">Esto se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0031e-383">This is shown here:</span></span>

![Módulo Entrenar modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="0031e-385">Puntuación del modelo</span><span class="sxs-lookup"><span data-stu-id="0031e-385">Score the model</span></span>
<span data-ttu-id="0031e-386">Una vez que tenemos un modelo entrenado, estamos preparados para puntuar el conjunto de datos test y evaluar su rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0031e-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="0031e-387">Lo hacemos mediante el módulo **Score Model (Puntuar modelo)** mostrado en la siguiente figura, con un módulo **Evaluate Model (Evaluar modelo)**:</span><span class="sxs-lookup"><span data-stu-id="0031e-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="0031e-389"><a name="step4"></a> Paso 4: Evaluación del modelo</span><span class="sxs-lookup"><span data-stu-id="0031e-389"><a name="step4"></a> Step 4: Evaluate the model</span></span>
<span data-ttu-id="0031e-390">Por último, vamos a analizar el rendimiento del modelo.</span><span class="sxs-lookup"><span data-stu-id="0031e-390">Finally, we would like to analyze model performance.</span></span> <span data-ttu-id="0031e-391">Normalmente, para los problemas de clasificación (binarios) de dos clases, una buena medida es AUC.</span><span class="sxs-lookup"><span data-stu-id="0031e-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="0031e-392">Para visualizar esto, conectamos el módulo **Score Model (Puntuar modelo)** con un módulo **Evaluate Model (Evaluar modelo)**.</span><span class="sxs-lookup"><span data-stu-id="0031e-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="0031e-393">Al hacer clic en **Visualizar** en el módulo **Evaluate Model (Evaluar modelo)**, se genera un gráfico como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0031e-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![Módulo Evaluación del modelo de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="0031e-395">En los problemas de clasificación binarios (o de dos clases), una buena medida de la exactitud de la predicción es Área bajo curva (AUC).</span><span class="sxs-lookup"><span data-stu-id="0031e-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="0031e-396">A continuación, mostramos nuestros resultados al usar este modelo en nuestro conjunto de datos "test".</span><span class="sxs-lookup"><span data-stu-id="0031e-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="0031e-397">Para ver los resultados, haga clic con el botón derecho en el puerto de salida del módulo **Evaluate Model (Evaluar modelo)** y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="0031e-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![Visualización del módulo Evaluar modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="0031e-399"><a name="step5"></a> Paso 5: Publicación del modelo como un servicio web</span><span class="sxs-lookup"><span data-stu-id="0031e-399"><a name="step5"></a> Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="0031e-400">La capacidad de publicar un modelo de Aprendizaje automático de Azure como servicios web con una complicación mínima es una característica valiosa para que esté ampliamente disponible.</span><span class="sxs-lookup"><span data-stu-id="0031e-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="0031e-401">Una vez hecho esto, cualquier persona puede realizar llamadas al servicio web con los datos de entrada para los que necesitan predicciones, y el servicio web usa el modelo para devolver dichas predicciones.</span><span class="sxs-lookup"><span data-stu-id="0031e-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="0031e-402">Para ello, primero guardamos el modelo con el que hemos entrenado como un objeto del Modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="0031e-402">To do this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="0031e-403">Haga clic con el botón derecho en el módulo **Entrenar modelo** y use la opción **Save as Trained Model (Guardar como modelo entrenado)**.</span><span class="sxs-lookup"><span data-stu-id="0031e-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="0031e-404">A continuación, necesitamos crear puertos de entrada y salida para nuestro servicio web:</span><span class="sxs-lookup"><span data-stu-id="0031e-404">Next, we need to create input and output ports for our web service:</span></span>

* <span data-ttu-id="0031e-405">Un puerto de entrada toma los datos de la misma forma que los datos para los que necesitamos predicciones</span><span class="sxs-lookup"><span data-stu-id="0031e-405">an input port takes data in the same form as the data that we need predictions for</span></span>
* <span data-ttu-id="0031e-406">Un puerto de salida devuelve las etiquetas puntuadas y las probabilidades asociadas.</span><span class="sxs-lookup"><span data-stu-id="0031e-406">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="0031e-407">Selección de algunas filas de datos para el puerto de entrada</span><span class="sxs-lookup"><span data-stu-id="0031e-407">Select a few rows of data for the input port</span></span>
<span data-ttu-id="0031e-408">Es cómodo usar una **Transformación de aplicación de SQL** para seleccionar solo 10 filas que sirvan como los datos del puerto de entrada.</span><span class="sxs-lookup"><span data-stu-id="0031e-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="0031e-409">Seleccione estas filas de datos para el puerto de entrada mediante la consulta SQL que se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0031e-409">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![Datos del puerto de entrada](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="0031e-411">Servicio web</span><span class="sxs-lookup"><span data-stu-id="0031e-411">Web service</span></span>
<span data-ttu-id="0031e-412">Ahora estamos preparados para realizar un pequeño experimento que puede utilizarse para publicar el servicio web.</span><span class="sxs-lookup"><span data-stu-id="0031e-412">Now we are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="0031e-413">Generación de datos de entrada para el servicio web</span><span class="sxs-lookup"><span data-stu-id="0031e-413">Generate input data for webservice</span></span>
<span data-ttu-id="0031e-414">Como paso inicial, ya que la tabla de recuento es grande, tomamos unas pocas líneas de datos de prueba y generamos datos de salida a partir de ellos con características de recuento.</span><span class="sxs-lookup"><span data-stu-id="0031e-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="0031e-415">Esto puede servir como formato de datos de entrada para nuestro servicio web.</span><span class="sxs-lookup"><span data-stu-id="0031e-415">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="0031e-416">Esto se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0031e-416">This is shown here:</span></span>

![Creación de datos de entrada de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="0031e-418">Para el formato de datos de entrada, utilizaremos ahora la salida del módulo **Count Featurizer** (Caracterizador de recuento).</span><span class="sxs-lookup"><span data-stu-id="0031e-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="0031e-419">Una vez que este experimento termina de ejecutarse, guarde la salida del módulo **Caracterizador de recuento** como un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="0031e-420">Este conjunto de datos se usa para los datos de entrada en el servicio web.</span><span class="sxs-lookup"><span data-stu-id="0031e-420">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="0031e-421">Puntuación del experimento para la publicación del servicio web</span><span class="sxs-lookup"><span data-stu-id="0031e-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="0031e-422">En primer lugar, veamos el aspecto que tiene.</span><span class="sxs-lookup"><span data-stu-id="0031e-422">First, we show what this looks like.</span></span> <span data-ttu-id="0031e-423">La estructura fundamental es un módulo **Score Model (Puntuar modelo)** que acepta el objeto del modelo entrenado y unas pocas líneas de datos de entrada que hemos generado en los pasos anteriores con el módulo **Count Featurizer (Caracterizador de recuento)**.</span><span class="sxs-lookup"><span data-stu-id="0031e-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="0031e-424">Utilizamos "Seleccionar columnas de conjunto de datos" para proyectar las etiquetas puntuadas y las probabilidades de puntuación.</span><span class="sxs-lookup"><span data-stu-id="0031e-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![Seleccionar columnas de conjunto de datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="0031e-426">Observe cómo el módulo **Seleccionar columnas de conjunto de datos** puede usarse para 'filtrar' datos de un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="0031e-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="0031e-427">El contenido se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0031e-427">We show the contents here:</span></span>

![Filtrado con el módulo Seleccionar columnas de conjunto de datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="0031e-429">Para obtener los puertos de salida y entrada azules, basta con hacer clic en **Preparar servicio web** en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="0031e-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="0031e-430">Al realizar este experimento también podemos publicar el servicio web haciendo clic en el icono **Publicar servicio web** situado en la esquina inferior derecha, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0031e-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![Publicar servicio web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="0031e-432">Una vez publicado el servicio web, accedemos a una página como esta:</span><span class="sxs-lookup"><span data-stu-id="0031e-432">Once the webservice is published, we get redirected to a page that looks thus:</span></span>

![Panel del servicio web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="0031e-434">Podemos ver los dos vínculos a los servicios web en el lado izquierdo:</span><span class="sxs-lookup"><span data-stu-id="0031e-434">We see two links for webservices on the left side:</span></span>

* <span data-ttu-id="0031e-435">El servicio **Solicitud-respuesta** (o RRS) está destinado a predicciones únicas y es lo que usamos en este taller.</span><span class="sxs-lookup"><span data-stu-id="0031e-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="0031e-436">El Servicio de **EJECUCIÓN POR LOTES** (BES) se usa para las predicciones por lotes y requiere que los datos de entrada usados para realizar predicciones residan en Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0031e-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="0031e-437">Al hacer clic en el vínculo **PETICIÓN-RESPUESTA**, accedemos a una página que nos proporciona un código predefinido en C#, Python y R. Este código puede usarse fácilmente para realizar llamadas al servicio web.</span><span class="sxs-lookup"><span data-stu-id="0031e-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="0031e-438">Tenga en cuenta que hay que utilizar la clave de API en esta página para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="0031e-438">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="0031e-439">Se aconseja copiar este código python en una celda nueva en el cuaderno de IPython.</span><span class="sxs-lookup"><span data-stu-id="0031e-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="0031e-440">Aquí se muestra un fragmento de código python con la clave de API correcta.</span><span class="sxs-lookup"><span data-stu-id="0031e-440">Here we show a segment of python code with the correct API key.</span></span>

![Código de Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="0031e-442">Tenga en cuenta que reemplazamos la clave de API predeterminada por la clave de API de nuestros servicios web.</span><span class="sxs-lookup"><span data-stu-id="0031e-442">Note that we replaced the default API key with our webservices's API key.</span></span> <span data-ttu-id="0031e-443">Al hacer clic en **Ejecutar** en esta celda de un cuaderno de IPython, se obtiene la siguiente respuesta:</span><span class="sxs-lookup"><span data-stu-id="0031e-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![Respuesta de IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="0031e-445">Podemos ver que para los dos ejemplos de prueba por los que hemos preguntado (en el marco JSON del script de python), obtenemos respuestas con el formato "Scored Labels, Scored Probabilities" (Etiquetas puntuadas, Probabilidades puntuadas).</span><span class="sxs-lookup"><span data-stu-id="0031e-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="0031e-446">Tenga en cuenta que, en este caso, elegimos los valores predeterminados que proporciona el código predefinido (0 para todas las columnas numéricas y la cadena "value" para todas las columnas de categorías).</span><span class="sxs-lookup"><span data-stu-id="0031e-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="0031e-447">Con esto concluye nuestro tutorial completo que muestra cómo controlar un conjunto de datos grande mediante Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0031e-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="0031e-448">Hemos empezado con un terabyte de datos, hemos creado un modelo de predicción y lo hemos implementado como un servicio web en la nube.</span><span class="sxs-lookup"><span data-stu-id="0031e-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span></span>

