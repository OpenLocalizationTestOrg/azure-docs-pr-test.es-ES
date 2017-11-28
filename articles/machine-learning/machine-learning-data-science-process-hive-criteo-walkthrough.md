---
title: "Hola proceso de ciencia de datos de equipo en acción: mediante un clúster de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB | Documentos de Microsoft"
description: "Con hello proceso de ciencia de datos de equipo para un escenario de extremo a emplear un Hadoop de HDInsight toobuild de clúster e implementar un modelo con un conjunto de datos disponible públicamente grande de (1 TB)"
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
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="af08c-103">Hola proceso de ciencia de datos de equipo en acción: mediante un clúster de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB</span><span class="sxs-lookup"><span data-stu-id="af08c-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="af08c-104">En este tutorial, se muestra cómo utilizar Hola proceso de ciencia de datos de equipo en un escenario de extremo a extremo con un [clúster de HDInsight Hadoop de Azure](https://azure.microsoft.com/services/hdinsight/) toostore, explorar, ingeniero de características y el detalle de los datos de ejemplo desde uno de hello públicamente disponible [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="af08c-105">Aprendizaje automático de Azure toobuild un modelo de clasificación binaria se usa en estos datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="af08c-106">También le mostramos cómo toopublish uno de estos modelos como un servicio Web.</span><span class="sxs-lookup"><span data-stu-id="af08c-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="af08c-107">También es posible toouse en este tutorial se presentan una tareas de hello IPython tooaccomplish de Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="af08c-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="af08c-108">Los usuarios que serían como tootry debe consultar este enfoque Hola [tutorial Criteo mediante una conexión ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tema.</span><span class="sxs-lookup"><span data-stu-id="af08c-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="af08c-109"><a name="dataset"></a>Descripción del conjunto de datos de Criteo</span><span class="sxs-lookup"><span data-stu-id="af08c-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="af08c-110">Hola Criteo datos están un conjunto de datos de predicción de clic es de aproximadamente 370GB de archivos .tsv de gzip comprimido (~1.3TB sin comprimir), que incluye más de 4.3 mil millones de registros.</span><span class="sxs-lookup"><span data-stu-id="af08c-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="af08c-111">Estos datos proceden de 24 días de datos de clics que ofrece [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="af08c-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="af08c-112">Para mayor comodidad de Hola de científicos de datos, se ha descomprimido tooexperiment toous disponibles de datos con.</span><span class="sxs-lookup"><span data-stu-id="af08c-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="af08c-113">Cada registro de este conjunto de datos contiene 40 columnas:</span><span class="sxs-lookup"><span data-stu-id="af08c-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="af08c-114">Hola primera columna es una columna de etiqueta que indica si un usuario hace clic en un **agregar** (valor 1) o no haga clic en uno (valor 0)</span><span class="sxs-lookup"><span data-stu-id="af08c-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="af08c-115">Las 13 columnas siguientes son numéricas.</span><span class="sxs-lookup"><span data-stu-id="af08c-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="af08c-116">Las últimas 26 son columnas de categorías.</span><span class="sxs-lookup"><span data-stu-id="af08c-116">last 26 are categorical columns</span></span>

<span data-ttu-id="af08c-117">columnas de Hello son anónimos y utilizar una serie de nombres enumerados: "Col1" (para la columna de etiqueta de hello) demasiado ' Col40 "(para la última columna de categorías hello).</span><span class="sxs-lookup"><span data-stu-id="af08c-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="af08c-118">Este es un extracto de hello primero 20 columnas de dos observaciones (filas) de este conjunto de datos:</span><span class="sxs-lookup"><span data-stu-id="af08c-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="af08c-119">Hay valores que faltan en ambas columnas numéricas y categorías de hello en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="af08c-120">Se describe un método sencillo para controlar los valores que faltan Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="af08c-121">Detalles adicionales de los datos de Hola se exploran al almacenarlos en tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="af08c-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="af08c-122">**Definición:** *tasa de Click-through (CTR):* trata Hola porcentaje de clics en los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="af08c-123">En este conjunto de datos Criteo, Hola CTR es aproximadamente 3.3% o 0.033.</span><span class="sxs-lookup"><span data-stu-id="af08c-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="af08c-124"><a name="mltasks"></a>Ejemplos de tareas de predicción</span><span class="sxs-lookup"><span data-stu-id="af08c-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="af08c-125">En este tutorial, se describen dos problemas de predicción de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="af08c-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="af08c-126">**Clasificación binaria**: predice si un usuario ha hecho clic o no en un anuncio:</span><span class="sxs-lookup"><span data-stu-id="af08c-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="af08c-127">Clase 0: no hace clic.</span><span class="sxs-lookup"><span data-stu-id="af08c-127">Class 0: No Click</span></span>
   * <span data-ttu-id="af08c-128">Clase 1: sí hace clic.</span><span class="sxs-lookup"><span data-stu-id="af08c-128">Class 1: Click</span></span>
2. <span data-ttu-id="af08c-129">**Regresión**: predice la probabilidad de Hola de un clic de ad a partir de funciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="af08c-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="af08c-130"><a name="setup"></a>Configuración de un clúster de Hadoop de HDInsight para la ciencia de los datos</span><span class="sxs-lookup"><span data-stu-id="af08c-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="af08c-131">**Nota:** Esta tarea la suelen hacer los **administradores**.</span><span class="sxs-lookup"><span data-stu-id="af08c-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="af08c-132">Configure su entorno de ciencia de datos de Azure para crear soluciones de análisis predictivos con los clústeres de HDInsight en tres pasos:</span><span class="sxs-lookup"><span data-stu-id="af08c-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="af08c-133">[Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md): esta cuenta de almacenamiento es toostore usa datos en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="af08c-134">datos de Hello usados en clústeres de HDInsight se almacenan aquí.</span><span class="sxs-lookup"><span data-stu-id="af08c-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="af08c-135">[Personalice los clústeres de Hadoop de HDInsight de Azure para la ciencia de los datos](machine-learning-data-science-customize-hadoop-cluster.md): en este paso, se crea un clúster de Hadoop de HDInsight de Azure con Anaconda Python 2.7 de 64 bits instalado en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="af08c-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="af08c-136">Al personalizar el clúster de HDInsight de hello, hay toocomplete de dos pasos importantes (descritas en este tema).</span><span class="sxs-lookup"><span data-stu-id="af08c-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="af08c-137">Debe vincular la cuenta de almacenamiento de hello creada en el paso 1 con el clúster de HDInsight cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="af08c-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="af08c-138">Esta cuenta de almacenamiento se utiliza para tener acceso a datos que pueden ser procesados en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="af08c-139">Debe habilitar el nodo principal de acceso remoto toohello de clúster de Hola después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="af08c-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="af08c-140">Recordar las credenciales de acceso remoto de Hola que especifique aquí (que son distintas de las especificadas para el clúster de hello en su creación): vaya necesitando toocomplete Hola procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="af08c-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="af08c-141">[Crear un área de trabajo de aprendizaje automático de Azure](machine-learning-create-workspace.md): aprendizaje automático de Azure esta área de trabajo se usa para crear modelos de aprendizaje automático después de una exploración de datos iniciales y hacia abajo de muestreo en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="af08c-142"><a name="getdata"></a>Obtención y consumo de datos desde un origen público</span><span class="sxs-lookup"><span data-stu-id="af08c-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="af08c-143">Hola [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjunto de datos puede obtenerse acceso haciendo clic en vínculo hello, acepte las condiciones de uso de Hola y proporcionar un nombre.</span><span class="sxs-lookup"><span data-stu-id="af08c-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="af08c-144">Aquí se muestra una instantánea de esta pantalla:</span><span class="sxs-lookup"><span data-stu-id="af08c-144">A snapshot of what this looks like is shown here:</span></span>

![Aceptar los términos de Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="af08c-146">Haga clic en **tooDownload continuar** tooread más información sobre el conjunto de datos de Hola y su disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="af08c-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="af08c-147">datos de Hello residen en un complemento público [almacenamiento de blobs de Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ubicación: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="af08c-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="af08c-148">Hola "wasb" hace referencia la ubicación de almacenamiento de blobs de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="af08c-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="af08c-149">datos de Hello en el almacenamiento de blobs público está formada por tres subcarpetas de datos sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="af08c-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="af08c-150">Hola subcarpeta *sin formato/count/* contiene Hola primera 21 días de datos, desde el día\_tooday 00\_20</span><span class="sxs-lookup"><span data-stu-id="af08c-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="af08c-151">Hola subcarpeta *sin formato/entrenar/* consta de un solo día de datos, día\_21</span><span class="sxs-lookup"><span data-stu-id="af08c-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="af08c-152">Hola subcarpeta *sin formato/test/* consta de dos días de datos, día\_22 y día\_23</span><span class="sxs-lookup"><span data-stu-id="af08c-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="af08c-153">Para aquellos que desean toostart con datos sin formato gzip de hello, también están disponibles en la carpeta principal de hello *sin formato /* como day_NN.gz, donde NN va de too23 00.</span><span class="sxs-lookup"><span data-stu-id="af08c-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="af08c-154">Un enfoque alternativo tooaccess, explorar y modele estos datos que no requieren las descargas locales se explica más adelante en este tutorial, cuando se crean tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="af08c-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="af08c-155"><a name="login"></a>Inicie sesión en el nodo principal del clúster de toohello</span><span class="sxs-lookup"><span data-stu-id="af08c-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="af08c-156">toolog en el nodo principal de toohello del clúster de hello, use hello [portal de Azure](https://ms.portal.azure.com) clúster de hello toolocate.</span><span class="sxs-lookup"><span data-stu-id="af08c-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="af08c-157">Haga clic en icono de hello HDInsight elefante en hello izquierda y, a continuación, haga doble clic en nombre de hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="af08c-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="af08c-158">Navegue toohello **configuración** ficha, haga doble clic en el icono de conectar hello en parte inferior de Hola de página de Hola y escriba sus credenciales de acceso remoto cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="af08c-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="af08c-159">Esto le llevará el nodo principal de toohello del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="af08c-160">Este es el aspecto de un primer registro en el nodo principal del clúster de toohello típico:</span><span class="sxs-lookup"><span data-stu-id="af08c-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Inicie sesión en toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="af08c-162">Hola izquierda, vemos Hola "Hadoop línea de comandos", que es nuestro potente para la exploración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="af08c-163">También vemos dos direcciones URL útiles: "Hadoop Yarn Status" (Estado de Hadoop Yarn) y "Hadoop Name Node" (Nombre del nodo de Hadoop).</span><span class="sxs-lookup"><span data-stu-id="af08c-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="af08c-164">dirección URL de Hello yarn estado muestra el progreso del trabajo y URL del nodo de nombre de hello proporciona detalles sobre la configuración de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="af08c-165">Ahora se configura y está listo toobegin primera parte del tutorial de Hola: exploración de datos con Hive y preparar datos para aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="af08c-166"><a name="hive-db-tables"></a> Creación de tablas y base de datos de Hive</span><span class="sxs-lookup"><span data-stu-id="af08c-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="af08c-167">toocreate Hive tablas para el conjunto de datos Criteo, abra hello ***línea de comandos de Hadoop*** en Hola escritorio del nodo principal de Hola y escriba el directorio del subárbol de hello escribiendo el comando de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="af08c-168">Ejecutar todos los comandos de Hive en este tutorial de Papelera de Hive Hola / símbolo del sistema de directorio.</span><span class="sxs-lookup"><span data-stu-id="af08c-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="af08c-169">De esta manera, cualquier problema con la ruta de acceso se soluciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="af08c-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="af08c-170">Usamos Hola términos "Prompt de directorio de Hive", "Hive bin / símbolo del sistema de directorio" y "línea de comandos de Hadoop" indistintamente.</span><span class="sxs-lookup"><span data-stu-id="af08c-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="af08c-171">tooexecute cualquier consulta de Hive, siempre se pueden usar Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="af08c-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="af08c-172">Después de hello Hive REPL aparece con un "hive >" iniciar sesión, corte y pegue Hola consulta tooexecute lo.</span><span class="sxs-lookup"><span data-stu-id="af08c-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="af08c-173">Hello código siguiente crea una base de datos "criteo" y, a continuación, genera 4 tablas:</span><span class="sxs-lookup"><span data-stu-id="af08c-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="af08c-174">un *tabla para generar recuentos* creado en el día de días\_tooday 00\_20,</span><span class="sxs-lookup"><span data-stu-id="af08c-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="af08c-175">un *tabla para su uso como conjunto de datos de entrenamiento de Hola* basado en día\_21, y</span><span class="sxs-lookup"><span data-stu-id="af08c-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="af08c-176">dos *conjuntos de datos de prueba de tablas para su uso como hello* basado en día\_22 y día\_23 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="af08c-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="af08c-177">El conjunto de datos de prueba se divide en dos tablas diferentes porque uno de los días de hello es un día festivo, y queremos toodetermine si el modelo de Hola puede detectar las diferencias entre un día festivo y no de vacaciones de velocidad de Click-through de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="af08c-178">Hola script [ejemplo &#95; hive &#95; crear &#95; criteo &#95; base de datos &#95; y &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) se muestra aquí por comodidad:</span><span class="sxs-lookup"><span data-stu-id="af08c-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

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

<span data-ttu-id="af08c-179">Se tenga en cuenta que todas estas tablas son externas como podemos simplemente punto tooAzure ubicaciones de almacenamiento de blobs (wasb).</span><span class="sxs-lookup"><span data-stu-id="af08c-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="af08c-180">**Hay dos maneras tooexecute Hive cualquier consulta que mencionamos ahora.**</span><span class="sxs-lookup"><span data-stu-id="af08c-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="af08c-181">**Usar Hola Hive REPL de línea de comandos**: hello en primer lugar es tooissue un comando "hive" y copie y pegue una consulta al Hola Hive REPL de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="af08c-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="af08c-182">toodo este, no:</span><span class="sxs-lookup"><span data-stu-id="af08c-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="af08c-183">Consulta de hello ejecuta ahora en hello REPL de línea de comandos, cortar y pegar.</span><span class="sxs-lookup"><span data-stu-id="af08c-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="af08c-184">**Guardar consultas tooa archivo y ejecutar el comando de hello**: hello en segundo lugar está el archivo .hql tooa de toosave hello las consultas ([ejemplo &#95; hive &#95; crear &#95; criteo &#95; base de datos &#95; y &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) y, a continuación, siguiente de Hola de problema comando consulta de Hola tooexecute:</span><span class="sxs-lookup"><span data-stu-id="af08c-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="af08c-185">Confirmación de la creación de la tabla y la base de datos</span><span class="sxs-lookup"><span data-stu-id="af08c-185">Confirm database and table creation</span></span>
<span data-ttu-id="af08c-186">A continuación, se confirme la creación de hello de base de datos de hello con hello siguiente comando desde la Papelera de Hive Hola / símbolo del sistema de directorio:</span><span class="sxs-lookup"><span data-stu-id="af08c-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="af08c-187">Este es el resultado:</span><span class="sxs-lookup"><span data-stu-id="af08c-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="af08c-188">Esto confirma la creación de hello de base de datos nueva hello, "criteo".</span><span class="sxs-lookup"><span data-stu-id="af08c-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="af08c-189">toosee qué tablas que hemos creado, se emite simplemente Hola comando aquí desde la Papelera de Hive Hola / símbolo del sistema de directorio:</span><span class="sxs-lookup"><span data-stu-id="af08c-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="af08c-190">A continuación, vemos Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="af08c-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="af08c-191"><a name="exploration"></a> Exploración de datos en Hive</span><span class="sxs-lookup"><span data-stu-id="af08c-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="af08c-192">Ahora estamos listos toodo una exploración de datos básicos en el subárbol.</span><span class="sxs-lookup"><span data-stu-id="af08c-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="af08c-193">Se empezar contando Hola número de ejemplos de entrenamiento de Hola y tablas de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="af08c-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="af08c-194">Número de ejemplos de "train"</span><span class="sxs-lookup"><span data-stu-id="af08c-194">Number of train examples</span></span>
<span data-ttu-id="af08c-195">Hola contenido de [ejemplo &#95; hive &#95; recuento &#95; entrenar &#95; tabla &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) se muestran a continuación:</span><span class="sxs-lookup"><span data-stu-id="af08c-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="af08c-196">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="af08c-197">O bien, uno puede emitir también Hola siguiente comando desde la Papelera de Hive Hola / símbolo del sistema de directorio:</span><span class="sxs-lookup"><span data-stu-id="af08c-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="af08c-198">Número de ejemplos de prueba de hello dos conjuntos de datos de prueba</span><span class="sxs-lookup"><span data-stu-id="af08c-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="af08c-199">Ahora contamos con número Hola de ejemplos de conjuntos de datos de dos pruebas Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="af08c-200">Hola contenido de [ejemplo &#95; hive &#95; recuento &#95; criteo &#95; prueba &#95; día &#95; 22 &#95; tabla &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) aquí:</span><span class="sxs-lookup"><span data-stu-id="af08c-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="af08c-201">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="af08c-202">Como es habitual, también podemos llamarlo script de Hola de Papelera de Hive Hola / directory símbolo del sistema mediante la emisión de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="af08c-203">Por último, examinamos número Hola de ejemplos de prueba de conjunto de datos de prueba de hello en función de día\_23.</span><span class="sxs-lookup"><span data-stu-id="af08c-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="af08c-204">Hello toodo de comando es similar toohello una muestra (consulte demasiado[ejemplo &#95; hive &#95; recuento &#95; criteo &#95; prueba &#95; día &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="af08c-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="af08c-205">Este es el resultado:</span><span class="sxs-lookup"><span data-stu-id="af08c-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="af08c-206">Distribución de etiqueta en el conjunto de datos de entrenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="af08c-207">distribución de la etiqueta de Hello en el conjunto de datos de entrenamiento de hello es de interés.</span><span class="sxs-lookup"><span data-stu-id="af08c-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="af08c-208">toosee esto, se muestra el contenido de [ejemplo &#95; hive &#95; criteo &#95; etiqueta &#95; distribución &#95; entrenar &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="af08c-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="af08c-209">Esto da como resultado la distribución de la etiqueta de hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="af08c-210">Tenga en cuenta que Hola porcentaje de las etiquetas positivas es 3.3% (coherente con el conjunto de datos original de hello).</span><span class="sxs-lookup"><span data-stu-id="af08c-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="af08c-211">Distribuciones de histograma de algunas variables numéricas en hello entrenar el conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="af08c-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="af08c-212">Podemos usar nativo del subárbol "histograma\_numérico" función toofind out qué distribución Hola de variables numéricas hello es similar.</span><span class="sxs-lookup"><span data-stu-id="af08c-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="af08c-213">Estos son contenido Hola de [ejemplo &#95; hive &#95; criteo &#95; histograma &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="af08c-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="af08c-214">Esto da como resultado siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-214">This yields hello following:</span></span>

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

<span data-ttu-id="af08c-215">Hola LATERAL vista - seccionar combinación en Hive actúa tooproduce una salida similar a SQL en lugar de lista de saludo habitual.</span><span class="sxs-lookup"><span data-stu-id="af08c-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="af08c-216">Tenga en cuenta que en Hola esta tabla, la primera columna de hello corresponde toohello bin hello y center segundo toohello bin frecuencia.</span><span class="sxs-lookup"><span data-stu-id="af08c-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="af08c-217">Percentiles aproximados de algunas variables numéricas en hello entrenar el conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="af08c-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="af08c-218">Además de interés con variables numéricas es cálculo Hola de percentiles aproximados.</span><span class="sxs-lookup"><span data-stu-id="af08c-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="af08c-219">La función nativa de Hive "percentile\_approx" permite realizar esta acción.</span><span class="sxs-lookup"><span data-stu-id="af08c-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="af08c-220">Hola contenido de [ejemplo &#95; hive &#95; criteo &#95; aproximado &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) son:</span><span class="sxs-lookup"><span data-stu-id="af08c-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="af08c-221">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="af08c-222">Se Comente que distribución Hola de percentiles suele toohello estrechamente relacionadas con el histograma distribución de cualquier variable numérica.</span><span class="sxs-lookup"><span data-stu-id="af08c-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="af08c-223">Buscar el número de valores únicos para algunas columnas de categorías en el conjunto de datos de entrenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="af08c-224">Continuar con la exploración de datos de hello, encontramos ahora, para algunas columnas de categorías, número de Hola de valores únicos que se necesitan.</span><span class="sxs-lookup"><span data-stu-id="af08c-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="af08c-225">toodo esto, se muestra el contenido de [ejemplo &#95; hive &#95; criteo &#95; único &#95; valores &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="af08c-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="af08c-226">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="af08c-227">Tenga en cuenta que Col15 tiene 19 millones de valores únicos.</span><span class="sxs-lookup"><span data-stu-id="af08c-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="af08c-228">Usar técnicas de naïve como "estrechamente con una codificación" tooencode dichas variables de categorías muy dimensionales es factible.</span><span class="sxs-lookup"><span data-stu-id="af08c-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="af08c-229">En particular, vamos a explicar y mostrar una técnica eficaz y contundente llamada [Aprendizaje con recuentos](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) para hacer frente a este problema de forma eficaz.</span><span class="sxs-lookup"><span data-stu-id="af08c-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="af08c-230">Esta subsección se finalizar examinando Hola número de valores únicos para algunas otras columnas de categorías también.</span><span class="sxs-lookup"><span data-stu-id="af08c-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="af08c-231">Hola contenido de [ejemplo &#95; hive &#95; criteo &#95; único &#95; valores &#95; varios &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) son:</span><span class="sxs-lookup"><span data-stu-id="af08c-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="af08c-232">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="af08c-233">Nuevo vemos que excepto Col20, todos Hola otras columnas tienen muchos valores únicos.</span><span class="sxs-lookup"><span data-stu-id="af08c-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="af08c-234">Recuentos de repetición coadministradores de pares de variables de categorías en el conjunto de datos de entrenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="af08c-235">Hola coadministradores repeticiones de pares de variables de categorías también es de interés.</span><span class="sxs-lookup"><span data-stu-id="af08c-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="af08c-236">Esto se puede determinar mediante código de hello en [ejemplo &#95; hive &#95; criteo &#95; emparejada &#95; categorías &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="af08c-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="af08c-237">Se invertir orden Hola recuentos por su aparición y busque en la parte superior de hello 15 en este caso.</span><span class="sxs-lookup"><span data-stu-id="af08c-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="af08c-238">El resultado obtenido es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="af08c-238">This gives us:</span></span>

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

## <span data-ttu-id="af08c-239"><a name="downsample"></a>Hacia abajo de conjuntos de datos de ejemplo hello para el aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="af08c-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="af08c-240">Tener Hola explorar conjuntos de datos y muestra cómo podemos hacer este tipo de exploración de las variables (incluidas combinaciones), que ahora hacia abajo de conjuntos de datos de ejemplo Hola por lo que podemos crear modelos de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="af08c-241">Recuerde error Hola nos centramos en es: dado un conjunto de atributos de ejemplo (valores de las características de Col2 - Col40), se predecir si Col1 es un 0 (no haga clic en) o 1 (hacer clic).</span><span class="sxs-lookup"><span data-stu-id="af08c-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="af08c-242">toodown ejemplo nuestro entrenar y probar los conjuntos de datos too1% del tamaño original de hello, usamos una función RAND() nativa del subárbol.</span><span class="sxs-lookup"><span data-stu-id="af08c-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="af08c-243">Hola la siguiente secuencia de comandos, [ejemplo &#95; hive &#95; criteo &#95; disminuir la resolución &#95; entrenar &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) hace conjunto de datos de entrenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="af08c-244">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="af08c-245">Hola script [ejemplo &#95; hive &#95; criteo &#95; disminuir la resolución &#95; prueba &#95; día &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) lo hace para los datos de prueba, día\_22:</span><span class="sxs-lookup"><span data-stu-id="af08c-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="af08c-246">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="af08c-247">Por último, Hola script [ejemplo &#95; hive &#95; criteo &#95; disminuir la resolución &#95; prueba &#95; día &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) lo hace para los datos de prueba, día\_23:</span><span class="sxs-lookup"><span data-stu-id="af08c-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="af08c-248">El resultado es:</span><span class="sxs-lookup"><span data-stu-id="af08c-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="af08c-249">Con esto, se está listo toouse nuestro abajo muestrea entrenar y probar los conjuntos de datos para generar modelos de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="af08c-250">Hay un componente importante final antes de seguir adelante tooAzure aprendizaje automático, que es la tabla de recuento de hello preocupaciones.</span><span class="sxs-lookup"><span data-stu-id="af08c-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="af08c-251">En hello siguiente subsección, se explican con más detalle.</span><span class="sxs-lookup"><span data-stu-id="af08c-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="af08c-252"><a name="count"></a>Obtener una breve descripción en la tabla de recuento de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="af08c-253">Como hemos visto, algunas variables de categorías tienen una dimensionalidad muy alta.</span><span class="sxs-lookup"><span data-stu-id="af08c-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="af08c-254">En nuestro tutorial, le presentaremos una técnica eficaz denominada [aprendizaje con recuentos](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode estas variables de una manera eficaz y sólida.</span><span class="sxs-lookup"><span data-stu-id="af08c-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="af08c-255">Para obtener más información sobre esta técnica está en vínculo Hola proporcionado.</span><span class="sxs-lookup"><span data-stu-id="af08c-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="af08c-256">En este tutorial, se centran en el uso de recuento tablas tooproduce compact representaciones de las características de categorías muy dimensionales.</span><span class="sxs-lookup"><span data-stu-id="af08c-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="af08c-257">Esto no es Hola única manera tooencode las características de categorías; Para obtener más información sobre otras técnicas, los usuarios interesados pueden extraer del repositorio [uno-activos-encoding](http://en.wikipedia.org/wiki/One-hot) y [hash de características](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="af08c-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="af08c-258">tablas de recuento de toobuild en datos de la cuenta de hello, utilizamos datos de Hola Hola/sin formato de carpeta de recuento.</span><span class="sxs-lookup"><span data-stu-id="af08c-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="af08c-259">Hola modelado sección, se muestran a los usuarios cómo toobuild estas funciones cuentan las tablas para las características de categorías desde cero o, alternativamente, toouse una tabla de recuento pregenerado para sus exploraciones.</span><span class="sxs-lookup"><span data-stu-id="af08c-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="af08c-260">En lo que se indica a continuación, cuando se hace referencia demasiado "previamente generado tablas de recuento", nos referimos usando tablas de recuento de Hola que ofrecemos.</span><span class="sxs-lookup"><span data-stu-id="af08c-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="af08c-261">Instrucciones detalladas sobre cómo tooaccess estas tablas se proporcionan en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="af08c-262"><a name="aml"></a> Creación de modelos con el Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="af08c-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="af08c-263">Nuestro proceso de creación de modelos con Azure Machine Learning consta de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="af08c-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="af08c-264">Obtener datos de Hola de las tablas de Hive en aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="af08c-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="af08c-265">Crear experimento de hello: limpiar datos de Hola y caracterizar con tablas de recuento</span><span class="sxs-lookup"><span data-stu-id="af08c-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="af08c-266">Compilación, entrenar y modelo de puntuación Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="af08c-267">Evaluar el modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="af08c-268">Publicar el modelo de Hola como un servicio web</span><span class="sxs-lookup"><span data-stu-id="af08c-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="af08c-269">Ahora estamos listos toobuild modelos en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="af08c-270">Los datos muestreados abajo se guardan como tablas de Hive en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="af08c-271">Usamos Hola aprendizaje automático de Azure **importar datos** tooread módulo estos datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="af08c-272">cuenta de almacenamiento de Hello credenciales tooaccess Hola de este clúster se muestran en qué se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="af08c-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="af08c-273"><a name="step1"></a>Paso 1: Obtener datos de las tablas de Hive en aprendizaje mediante el módulo de importación de datos de Hola y selecciónelo para un experimento de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="af08c-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="af08c-274">Para empezar, seleccione **+NUEVO** -> **EXPERIMENTO** -> **Experimento en blanco**.</span><span class="sxs-lookup"><span data-stu-id="af08c-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="af08c-275">A continuación, en hello **búsqueda** cuadro en hello esquina superior izquierda, busque "Importar datos".</span><span class="sxs-lookup"><span data-stu-id="af08c-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="af08c-276">Hola de arrastrar y colocar **importar datos** módulo en módulo toohello experimento lienzo (parte media de Hola de pantalla de bienvenida) toouse hello para el acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="af08c-277">Esto es qué hello **importar datos** aspecto al obtener datos de tabla de Hive hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Importar datos obtiene los datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="af08c-279">Para hello **importar datos** módulo, valores de hello de parámetros de Hola que se proporcionan en hello gráfico son sólo algunos ejemplos de hello, tipo de valores necesita tooprovide.</span><span class="sxs-lookup"><span data-stu-id="af08c-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="af08c-280">Aquí tiene algunas instrucciones generales acerca toofill parámetro hello de salida de hello **importar datos** módulo.</span><span class="sxs-lookup"><span data-stu-id="af08c-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="af08c-281">Elija "Consulta de Hive" como **Origen de datos**</span><span class="sxs-lookup"><span data-stu-id="af08c-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="af08c-282">Hola **consulta de base de datos de Hive** cuadro, una instrucción SELECT simple * FROM < su\_base de datos\_name.your\_tabla\_name >-es suficiente.</span><span class="sxs-lookup"><span data-stu-id="af08c-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="af08c-283">**URI del servidor de Hcatalog**: si el clúster es "abc", este valor simplemente será: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="af08c-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="af08c-284">**Nombre de cuenta de usuario de Hadoop**: nombre de usuario de hello seleccionado en el momento de Hola de puesta en servicio de Cluster Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="af08c-285">(No Hola acceso remoto nombre de usuario!)</span><span class="sxs-lookup"><span data-stu-id="af08c-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="af08c-286">**Contraseña de cuenta de usuario de Hadoop**: Hola contraseña Hola nombre de usuario seleccionado en el momento de Hola de puesta en servicio de Cluster Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="af08c-287">(No Hola contraseña de acceso remoto!)</span><span class="sxs-lookup"><span data-stu-id="af08c-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="af08c-288">**Ubicación de los datos de salida**: elija "Azure".</span><span class="sxs-lookup"><span data-stu-id="af08c-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="af08c-289">**Nombre de la cuenta de almacenamiento de Azure**: Hola cuenta de almacenamiento asociada con el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="af08c-290">**Clave de cuenta de almacenamiento de Azure**: clave Hola de hello cuenta de almacenamiento asociada con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="af08c-291">**Nombre de contenedor de Azure**: si el nombre del clúster de hello es "abc", esto suele ser simplemente "abc",.</span><span class="sxs-lookup"><span data-stu-id="af08c-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="af08c-292">Una vez Hola **importar datos** termina de obtención de datos (ver graduación Hola verde en hello módulo), guardar estos datos como un conjunto de datos (con un nombre de su elección).</span><span class="sxs-lookup"><span data-stu-id="af08c-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="af08c-293">Este es el aspecto:</span><span class="sxs-lookup"><span data-stu-id="af08c-293">What this looks like:</span></span>

![Importar datos guarda los datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="af08c-295">Puerto de hello de salida de hello contextual **importar datos** módulo.</span><span class="sxs-lookup"><span data-stu-id="af08c-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="af08c-296">Se muestran las opciones **Guardar como conjunto de datos** y **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="af08c-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="af08c-297">Hola **visualizar** opción, si hace clic en, muestra 100 filas de datos de hello, junto con un panel derecho que es útil para algunas estadísticas de resumen.</span><span class="sxs-lookup"><span data-stu-id="af08c-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="af08c-298">datos de toosave, simplemente seleccione **Guardar como conjunto de datos** y siga las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="af08c-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="af08c-299">tooselect Hola guardan conjunto de datos para su uso en un experimento de aprendizaje de máquina, buscar conjuntos de datos de hello mediante hello **búsqueda** cuadro se muestra en la figura siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="af08c-300">A continuación, sólo tiene que escribir el nombre de Hola se le asignó hello conjunto de datos parcialmente tooaccess y arrastre Hola conjunto de datos a Hola panel principal.</span><span class="sxs-lookup"><span data-stu-id="af08c-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="af08c-301">Colocar en el panel principal de hello, selecciona para su uso en el modelado de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="af08c-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Conjunto de datos de arrastre en el panel principal Hola](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="af08c-303">Hágalo para entrenar hello y conjuntos de datos de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="af08c-304">También, recuerde el nombre de base de datos de toouse hello y nombres de tabla que ha asignado para este propósito.</span><span class="sxs-lookup"><span data-stu-id="af08c-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="af08c-305">valores de Hello utilizados en la figura Hola son únicamente para ilustración purposes.* *</span><span class="sxs-lookup"><span data-stu-id="af08c-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="af08c-306"><a name="step2"></a>Paso 2: Crear un experimento sencillo en aprendizaje automático de Azure toopredict clics / no hace clic en</span><span class="sxs-lookup"><span data-stu-id="af08c-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="af08c-307">Nuestro experimento de Azure Machine Learning tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="af08c-307">Our Azure ML experiment looks like this:</span></span>

![Experimento de Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="af08c-309">Ahora se examinan los componentes clave de Hola de este experimento.</span><span class="sxs-lookup"><span data-stu-id="af08c-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="af08c-310">Como recordatorio, necesitamos toodrag nuestro guardado entrenar y probar los conjuntos de datos en el lienzo del experimento de tooour primero.</span><span class="sxs-lookup"><span data-stu-id="af08c-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="af08c-311">Limpiar datos que faltan</span><span class="sxs-lookup"><span data-stu-id="af08c-311">Clean Missing Data</span></span>
<span data-ttu-id="af08c-312">Hola **limpiar datos que faltan** módulo lo que sugiere su nombre: limpia los datos que faltan de manera que puede ser especificado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="af08c-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="af08c-313">En este módulo, veremos estos datos:</span><span class="sxs-lookup"><span data-stu-id="af08c-313">Looking into this module, we see this:</span></span>

![Limpiar datos que faltan](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="af08c-315">En este caso, elegimos tooreplace todos los valores que faltan con un 0.</span><span class="sxs-lookup"><span data-stu-id="af08c-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="af08c-316">Hay otras opciones, que pueden ser vistos examinando las listas desplegables de hello en el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="af08c-317">Característica de ingeniería en datos de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-317">Feature engineering on hello data</span></span>
<span data-ttu-id="af08c-318">Puede haber millones de valores únicos para algunas características de categoría de grandes conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="af08c-319">El uso de métodos simples como la codificación "one-hot" para representar estas características de categorías no es viable.</span><span class="sxs-lookup"><span data-stu-id="af08c-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="af08c-320">En este tutorial, se muestra cómo las características de recuento de toouse con toogenerate de módulos de aprendizaje automático de Azure integrada compact representaciones de estas variables de categorías muy dimensionales.</span><span class="sxs-lookup"><span data-stu-id="af08c-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="af08c-321">Hello resultado final es un tamaño más pequeño de modelo, velocidad de entrenamiento y las métricas de rendimiento que son bastante comparable toousing otras técnicas.</span><span class="sxs-lookup"><span data-stu-id="af08c-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="af08c-322">Creación de transformaciones de recuento</span><span class="sxs-lookup"><span data-stu-id="af08c-322">Building counting transforms</span></span>
<span data-ttu-id="af08c-323">funciones de recuento de toobuild, se usa los hello **compilar contando transformar** módulo que está disponible en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="af08c-324">módulo de Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="af08c-324">hello module looks like this:</span></span>

<span data-ttu-id="af08c-325">![Módulo Crear transformación de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Módulo Crear transformación de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="af08c-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="af08c-326">Hola **el número de columna** cuadro, escribimos las columnas que se desea tooperform cuenta.</span><span class="sxs-lookup"><span data-stu-id="af08c-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="af08c-327">Normalmente, son columnas de categorías con una alta dimensionalidad (tal y como se mencionó).</span><span class="sxs-lookup"><span data-stu-id="af08c-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="af08c-328">En el inicio de hello, mencionamos ese conjunto de datos de Criteo hello tiene 26 columnas de categorías: de Col15 tooCol40.</span><span class="sxs-lookup"><span data-stu-id="af08c-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="af08c-329">En este caso, se cuentan en todos ellos y proporcionar a sus índices (de 15 too40 separados por comas, como se muestra).</span><span class="sxs-lookup"><span data-stu-id="af08c-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="af08c-330">módulo de hello toouse en Hola MapReduce modo (adecuado para grandes conjuntos de datos), necesitamos accedemos clúster de Hadoop de HDInsight tooan (Hola uno utilizado para la exploración de la característica se puede reutilizar para este propósito así) y sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="af08c-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="af08c-331">figuras anterior de Hello muestran qué valores rellena Hola apariencia (reemplazar valores de hello dan a modo ilustrativo con los que son relevantes para su propio caso de uso).</span><span class="sxs-lookup"><span data-stu-id="af08c-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Parámetros del módulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="af08c-333">En la ilustración de hello anterior, mostramos cómo tooenter Hola entrada blob ubicación.</span><span class="sxs-lookup"><span data-stu-id="af08c-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="af08c-334">Esta ubicación tiene datos Hola reservados para la creación de tablas de recuento.</span><span class="sxs-lookup"><span data-stu-id="af08c-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="af08c-335">Una vez finaliza la ejecución de este módulo, podemos guardar transformación Hola para más tarde haciendo clic en el módulo de Hola y seleccionar hello **Guardar como transformación** opción:</span><span class="sxs-lookup"><span data-stu-id="af08c-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![Opción "Guardar como transformación"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="af08c-337">En nuestra arquitectura de experimento mostrado anteriormente, Hola dataset "ytransform2" corresponde exactamente tooa guarda la transformación de recuento.</span><span class="sxs-lookup"><span data-stu-id="af08c-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="af08c-338">Para el resto de Hola de este experimento, suponemos que ese lector hello usa un **compilar contando transformar** módulo en algunos datos toogenerate recuentos y, a continuación, puede usar las características de recuento de recuentos toogenerate en tren de Hola y conjuntos de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="af08c-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="af08c-339">Elegir qué cuenta tooinclude características como parte del entrenamiento de Hola y conjuntos de datos de prueba</span><span class="sxs-lookup"><span data-stu-id="af08c-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="af08c-340">Una vez que tenemos un recuento transformar listo, usuario Hola puede elegir qué tooinclude características en su entrenar y probar los conjuntos de datos mediante hello **modificar parámetros de tabla de recuento** módulo.</span><span class="sxs-lookup"><span data-stu-id="af08c-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="af08c-341">Mostramos este módulo a continuación solo para ofrecer una visión completa, pero para simplificar no lo usamos en nuestro experimento.</span><span class="sxs-lookup"><span data-stu-id="af08c-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Parámetros de la tabla de modificación de recuentos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="af08c-343">En este caso, tal y como se puede ver, que hemos elegido toouse probabilidades de registro solo Hola y Hola tooignore retroceder de columna.</span><span class="sxs-lookup"><span data-stu-id="af08c-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="af08c-344">También podemos establecer parámetros como Hola umbral de Papelera, cuántos tooadd ejemplos pseudo anterior para suavizar, y si toouse cualquier Laplaciana ruido o no.</span><span class="sxs-lookup"><span data-stu-id="af08c-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="af08c-345">Todos estos son características avanzados y es toobe en cuenta que los valores predeterminados de hello son un buen punto de partida para los usuarios que son el nuevo tipo de toothis de generación de la característica.</span><span class="sxs-lookup"><span data-stu-id="af08c-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="af08c-346">Transformación de datos antes de generar características de recuento de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="af08c-347">Ahora se centrarse en un punto importante acerca de la transformación nuestro entrenar y probar datos tooactually anterior generar características de recuento.</span><span class="sxs-lookup"><span data-stu-id="af08c-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="af08c-348">Tenga en cuenta que hay dos **ejecutar Script de R** módulos usados para aplicar la transformación tooour datos de recuento de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![Ejecución de módulos de script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="af08c-350">Este es el primer script de R hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-350">Here is hello first R script:</span></span>

![Primer script de R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="af08c-352">En este script de R, cambiamos el nombre de nuestro toonames columnas "Col1" demasiado "Col40".</span><span class="sxs-lookup"><span data-stu-id="af08c-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="af08c-353">Esto es porque la transformación recuento de hello espera que los nombres de este formato.</span><span class="sxs-lookup"><span data-stu-id="af08c-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="af08c-354">El segundo script de R hello, se un equilibrio entre la distribución de Hola entre clases positivas y negativas (clases 1 y 0, respectivamente) por clase de disminución de resolución Hola negativo.</span><span class="sxs-lookup"><span data-stu-id="af08c-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="af08c-355">Hola R este script muestra cómo toodo esto:</span><span class="sxs-lookup"><span data-stu-id="af08c-355">hello R script here shows how toodo this:</span></span>

![Segundo script de R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="af08c-357">En esta secuencia de comandos de R simple, se utiliza "pos\_neg\_proporción" cantidad de hello tooset de equilibrio entre las clases negativo de Hola y Hola positivo.</span><span class="sxs-lookup"><span data-stu-id="af08c-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="af08c-358">Esto es importante toodo ya que suele mejorar el desequilibrio de la clase tiene ventajas de rendimiento para problemas de clasificación donde la distribución de la clase de hello es sesgado (Recuerde que en nuestro caso, tenemos 3.3% positivo clase y clase negativo 96,7%).</span><span class="sxs-lookup"><span data-stu-id="af08c-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="af08c-359">Aplicar transformación de recuento de hello en nuestros datos</span><span class="sxs-lookup"><span data-stu-id="af08c-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="af08c-360">Por último, podemos usar hello **aplicar transformación** tooapply módulo Hola transformaciones de recuento en nuestro entrenar y probar los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="af08c-361">Este módulo toma la transformación recuento de hello guardado como una entrada y Hola entrenar o probar los conjuntos de datos como Hola otra entrada y devuelve los datos con características de recuento.</span><span class="sxs-lookup"><span data-stu-id="af08c-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="af08c-362">Se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="af08c-362">It is shown here:</span></span>

![Módulo Aplicar transformación](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="af08c-364">Un extracto del aspecto de características de recuento de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="af08c-365">Es instructivo toosee qué características de recuento de hello aspecto en nuestro caso.</span><span class="sxs-lookup"><span data-stu-id="af08c-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="af08c-366">Aquí se muestra un extracto de esto:</span><span class="sxs-lookup"><span data-stu-id="af08c-366">Here we show an excerpt of this:</span></span>

![Características de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="af08c-368">En este extracto, se mostrará que para las columnas de Hola que se enumeran en, se obtener recuentos de Hola y probabilidades de registro en suma tooany relevante backoffs.</span><span class="sxs-lookup"><span data-stu-id="af08c-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="af08c-369">Ahora estamos listo toobuild un modelo de aprendizaje automático de Azure con estos conjuntos de datos transformados.</span><span class="sxs-lookup"><span data-stu-id="af08c-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="af08c-370">En la siguiente sección hello, mostramos cómo puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="af08c-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="af08c-371"><a name="step3"></a>Paso 3: Crear, entrenar y puntuar modelo Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="af08c-372">Elección del aprendiz</span><span class="sxs-lookup"><span data-stu-id="af08c-372">Choice of learner</span></span>
<span data-ttu-id="af08c-373">En primer lugar, necesitamos toochoose un aprendiz.</span><span class="sxs-lookup"><span data-stu-id="af08c-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="af08c-374">Estamos continuo toouse un árbol de decisión impulsado de dos clases como nuestro aprendiz.</span><span class="sxs-lookup"><span data-stu-id="af08c-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="af08c-375">Estas son opciones predeterminadas de Hola para este aprendiz:</span><span class="sxs-lookup"><span data-stu-id="af08c-375">Here are hello default options for this learner:</span></span>

![Parámetros de árbol de decisiones incrementados de dos clases](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="af08c-377">Para nuestro experimento, estamos valores predeterminados de curso toochoose Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="af08c-378">Se tenga en cuenta que hello tiene como valor predeterminado son normalmente significativa y una buena manera tooget rápido las líneas de base en el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="af08c-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="af08c-379">Puede mejorar en el rendimiento mediante el barrido de parámetros si elige tooonce que tiene una línea base.</span><span class="sxs-lookup"><span data-stu-id="af08c-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="af08c-380">Entrenar el modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-380">Train hello model</span></span>
<span data-ttu-id="af08c-381">Para el entrenamiento, simplemente invocamos un módulo **Entrenar modelo** .</span><span class="sxs-lookup"><span data-stu-id="af08c-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="af08c-382">Hola dos entradas tooit son aprendiz de árbol de decisión impulsado de dos clases de Hola y el conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="af08c-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="af08c-383">Esto se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="af08c-383">This is shown here:</span></span>

![Módulo Entrenar modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="af08c-385">Modelo de Hola de puntuación</span><span class="sxs-lookup"><span data-stu-id="af08c-385">Score hello model</span></span>
<span data-ttu-id="af08c-386">Una vez que tenemos un modelo entrenado, estamos preparados tooscore en hello probar el conjunto de datos y tooevaluate su rendimiento.</span><span class="sxs-lookup"><span data-stu-id="af08c-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="af08c-387">Esto se realiza mediante hello **puntuar modelo** módulo se muestra en hello siguiente figura, junto con un **evaluar modelo** módulo:</span><span class="sxs-lookup"><span data-stu-id="af08c-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="af08c-389"><a name="step4"></a>Paso 4: Evaluar el modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="af08c-390">Por último, nos gustaría tooanalyze rendimiento del modelo.</span><span class="sxs-lookup"><span data-stu-id="af08c-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="af08c-391">Por lo general, para los dos problemas de clasificación (binaria) de clase, una buena medida es hello AUC.</span><span class="sxs-lookup"><span data-stu-id="af08c-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="af08c-392">toovisualize esto, se enlazó hello **puntuar modelo** módulo tooan **evaluar modelo** módulo para esto.</span><span class="sxs-lookup"><span data-stu-id="af08c-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="af08c-393">Haga clic en **visualizar** en hello **evaluar modelo** módulo da como resultado un gráfico como Hola sigue uno:</span><span class="sxs-lookup"><span data-stu-id="af08c-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Módulo Evaluación del modelo de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="af08c-395">En binario (o clase dos) problemas de clasificación, una buena medida de precisión de la predicción se Hola área en curva (AUC).</span><span class="sxs-lookup"><span data-stu-id="af08c-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="af08c-396">A continuación, mostramos nuestros resultados al usar este modelo en nuestro conjunto de datos "test".</span><span class="sxs-lookup"><span data-stu-id="af08c-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="af08c-397">tooget, puerto de salida de hello contextual de hello **evaluar modelo** módulo y, a continuación, **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="af08c-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Visualización del módulo Evaluar modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="af08c-399"><a name="step5"></a>Paso 5: Publicar modelo Hola como un servicio Web</span><span class="sxs-lookup"><span data-stu-id="af08c-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="af08c-400">Hola capacidad toopublish un modelo de aprendizaje automático de Azure como servicios web con un mínimo de molestias es una característica útil para realizar ampliamente disponibles.</span><span class="sxs-lookup"><span data-stu-id="af08c-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="af08c-401">Una vez hecho esto, cualquier usuario puede crear el servicio web de llamadas a toohello con datos de entrada que necesiten predicciones para y servicio web de hello usa Hola modelo tooreturn estas predicciones.</span><span class="sxs-lookup"><span data-stu-id="af08c-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="af08c-402">toodo, guardamos primero nuestro modelo de aprendizaje como un objeto de modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="af08c-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="af08c-403">Esto se hace con el botón secundario hello **entrenar modelo** módulo y usar hello **Guardar como modelo entrenado** opción.</span><span class="sxs-lookup"><span data-stu-id="af08c-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="af08c-404">A continuación, necesitamos toocreate entrada y salida de puertos para el servicio web:</span><span class="sxs-lookup"><span data-stu-id="af08c-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="af08c-405">un puerto de entrada toma los datos en hello mismo formulario como datos de Hola que necesitamos predicciones para</span><span class="sxs-lookup"><span data-stu-id="af08c-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="af08c-406">un puerto de salida devuelve Hola puntuación de etiquetas y las probabilidades de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="af08c-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="af08c-407">Seleccione algunas filas de datos para el puerto de entrada de Hola</span><span class="sxs-lookup"><span data-stu-id="af08c-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="af08c-408">Es conveniente toouse una **aplicar transformación de SQL** módulo tooselect simplemente 10 filas tooserve como Hola los datos de puerto de entrada.</span><span class="sxs-lookup"><span data-stu-id="af08c-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="af08c-409">Seleccione solo estas filas de datos para nuestro puerto de entrada mediante consultas SQL Hola que se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="af08c-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Datos del puerto de entrada](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="af08c-411">Servicio web</span><span class="sxs-lookup"><span data-stu-id="af08c-411">Web service</span></span>
<span data-ttu-id="af08c-412">Ahora estamos listos toorun un experimento pequeño que puede ser utilizado toopublish nuestro servicio web.</span><span class="sxs-lookup"><span data-stu-id="af08c-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="af08c-413">Generación de datos de entrada para el servicio web</span><span class="sxs-lookup"><span data-stu-id="af08c-413">Generate input data for webservice</span></span>
<span data-ttu-id="af08c-414">Como paso cero, puesto que es grande, la tabla de recuento de Hola se tardar unas pocas líneas de datos de prueba y generan datos de salida a partir de él con características de recuento.</span><span class="sxs-lookup"><span data-stu-id="af08c-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="af08c-415">Esto puede servir como formato de datos de entrada de Hola de nuestro servicio Web.</span><span class="sxs-lookup"><span data-stu-id="af08c-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="af08c-416">Esto se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="af08c-416">This is shown here:</span></span>

![Creación de datos de entrada de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="af08c-418">Para el formato de datos de entrada de hello, usamos ahora Hola salida de hello **Count Featurizer** módulo.</span><span class="sxs-lookup"><span data-stu-id="af08c-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="af08c-419">Una vez que esto experimentar termine la ejecución, guardar la salida de hello de hello **Count Featurizer** módulo como un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="af08c-420">Este conjunto de datos se utiliza para los datos de entrada de hello en hello webservice.</span><span class="sxs-lookup"><span data-stu-id="af08c-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="af08c-421">Puntuación del experimento para la publicación del servicio web</span><span class="sxs-lookup"><span data-stu-id="af08c-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="af08c-422">En primer lugar, veamos el aspecto que tiene.</span><span class="sxs-lookup"><span data-stu-id="af08c-422">First, we show what this looks like.</span></span> <span data-ttu-id="af08c-423">Hola esencial estructura es una **puntuar modelo** módulo que acepta el objeto de modelo entrenado y unas pocas líneas de datos de entrada que se generan en pasos anteriores de hello con hello **Count Featurizer** módulo.</span><span class="sxs-lookup"><span data-stu-id="af08c-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="af08c-424">Se utiliza "Seleccionar columnas de conjunto de datos" tooproject Hola puntuado etiquetas y las probabilidades de puntuación de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Seleccionar columnas de conjunto de datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="af08c-426">Tenga en cuenta cómo Hola **seleccionar columnas de conjunto de datos** módulo puede utilizarse para 'filtrando' datos de un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="af08c-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="af08c-427">Se muestra contenido de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="af08c-427">We show hello contents here:</span></span>

![Filtrar con hello seleccionar columnas en el módulo de conjunto de datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="af08c-429">puertos de hello azul de entrada y salida tooget, simplemente haga clic en **preparar webservice** final Hola derecho.</span><span class="sxs-lookup"><span data-stu-id="af08c-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="af08c-430">Ejecuta este experimento también permite que nos toopublish Hola servicio web: haga clic en hello **publicar servicio WEB** situado en aquí de derecho, como se muestra de la parte inferior de hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![Publicar servicio web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="af08c-432">Una vez publicado el servicio Web de hello, obtenemos tooa redirigida página que busca por lo tanto:</span><span class="sxs-lookup"><span data-stu-id="af08c-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Panel del servicio web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="af08c-434">Dos vínculos de servicios Web se muestra en el lado izquierdo de hello:</span><span class="sxs-lookup"><span data-stu-id="af08c-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="af08c-435">Hola **solicitud/respuesta** servicio (o RR) está destinados solo predicciones y es lo que se usan en el taller.</span><span class="sxs-lookup"><span data-stu-id="af08c-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="af08c-436">Hola **ejecución por lotes** servicio (BES) se utiliza para las predicciones por lotes y requiere que las predicciones de toomake de datos de entrada utilizados Hola residan en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="af08c-437">Al hacer clic en el vínculo de hello **solicitud/respuesta** nos lleva tooa página que nos da predefinidos previamente el código en C#, python y R. Este código se puede usar de forma cómoda para realizar llamadas toohello webservice.</span><span class="sxs-lookup"><span data-stu-id="af08c-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="af08c-438">Tenga en cuenta que Hola clave de API en esta página debe toobe utilizado para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="af08c-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="af08c-439">Es conveniente toocopy este python código sobre tooa nueva celda en el Bloc de notas de IPython Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="af08c-440">Aquí mostramos un segmento de código python con clave de API de hello correcta.</span><span class="sxs-lookup"><span data-stu-id="af08c-440">Here we show a segment of python code with hello correct API key.</span></span>

![Código de Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="af08c-442">Tenga en cuenta que reemplazamos clave de API de hello predeterminada con la clave de API de nuestros servicios Web.</span><span class="sxs-lookup"><span data-stu-id="af08c-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="af08c-443">Haga clic en **ejecutar** en esta celda en una IPython Bloc de notas, da como resultado Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="af08c-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![Respuesta de IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="af08c-445">Se puede ver que para hello dos pruebas ejemplos que pedimos sobre (en el marco de trabajo JSON de hello del script de python Hola), obtenemos respuestas en forma de Hola "Puntuado etiquetas, las probabilidades de puntuado".</span><span class="sxs-lookup"><span data-stu-id="af08c-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="af08c-446">Tenga en cuenta que en este caso, elegimos valores predeterminados de hello ese código predefinida Hola proporciona (0 para todas las columnas numéricas y cadena Hola "value" para todas las columnas de categorías).</span><span class="sxs-lookup"><span data-stu-id="af08c-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="af08c-447">Con esto concluye nuestra tutorial to-end que se muestra cómo toohandle dataset a gran escala mediante el aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="af08c-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="af08c-448">Trabajar con un terabyte de datos, crea un modelo de predicción y había implementado como un servicio web en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="af08c-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

