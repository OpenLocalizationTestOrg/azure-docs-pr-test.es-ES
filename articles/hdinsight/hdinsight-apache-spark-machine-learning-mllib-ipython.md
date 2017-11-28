---
title: "Ejemplo de aprendizaje automático con Spark MLlib en HDInsight - Azure | Microsoft Docs"
description: "Aprenda a usar Spark MLlib para crear una aplicación de aprendizaje automático que analice un conjunto de datos usando la clasificación mediante una regresión logística."
keywords: "aprendizaje automático con spark, ejemplo de aprendizaje automático con spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="d5abf-104">Usar Spark MLlib para compilar una aplicación de aprendizaje automático y analizar un conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="d5abf-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="d5abf-105">Aprenda a usar Spark **MLlib** para crear una aplicación de aprendizaje automático para efectuar análisis predictivos simples en un conjunto de datos abierto.</span><span class="sxs-lookup"><span data-stu-id="d5abf-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="d5abf-106">De las bibliotecas de aprendizaje automático integradas de Spark, en este ejemplo se usa una *clasificación* mediante una regresión logística.</span><span class="sxs-lookup"><span data-stu-id="d5abf-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="d5abf-107">Este ejemplo también está disponible en formato de cuaderno de Jupyter en un clúster Spark (Linux) que se crea en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5abf-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="d5abf-108">La experiencia del cuaderno le permite ejecutar los fragmentos de código de Python desde el propio Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="d5abf-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="d5abf-109">Para seguir el tutorial desde un cuaderno, cree un clúster de Spark y abra un cuaderno de Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="d5abf-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="d5abf-110">Luego, ejecute el cuaderno **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** en la carpeta **Python**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="d5abf-111">MLlib es una biblioteca básica de Spark que proporciona numerosas utilidades que resultan prácticas para las tareas de aprendizaje automático, como utilidades adecuadas para:</span><span class="sxs-lookup"><span data-stu-id="d5abf-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="d5abf-112">clasificación</span><span class="sxs-lookup"><span data-stu-id="d5abf-112">Classification</span></span>
* <span data-ttu-id="d5abf-113">Regresión</span><span class="sxs-lookup"><span data-stu-id="d5abf-113">Regression</span></span>
* <span data-ttu-id="d5abf-114">Agrupación en clústeres</span><span class="sxs-lookup"><span data-stu-id="d5abf-114">Clustering</span></span>
* <span data-ttu-id="d5abf-115">Modelado de tema</span><span class="sxs-lookup"><span data-stu-id="d5abf-115">Topic modeling</span></span>
* <span data-ttu-id="d5abf-116">Descomposición en valores singulares (SVD) y Análisis de los componentes principales (PCA)</span><span class="sxs-lookup"><span data-stu-id="d5abf-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="d5abf-117">Comprobación de hipótesis y cálculo de estadísticas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d5abf-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="d5abf-118">¿Qué entendemos por clasificación y por regresión logística?</span><span class="sxs-lookup"><span data-stu-id="d5abf-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="d5abf-119">*Clasificación*, una tarea habitual en el aprendizaje automático, es el proceso de ordenación de datos de entrada en categorías.</span><span class="sxs-lookup"><span data-stu-id="d5abf-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="d5abf-120">El trabajo de averiguar cómo asignar "etiquetas" a las entradas de datos que se proporcionen lo realiza un algoritmo de clasificación.</span><span class="sxs-lookup"><span data-stu-id="d5abf-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="d5abf-121">Por ejemplo, imagínese un algoritmo de aprendizaje automático que acepta información bursátil como entrada y divide las existencias en dos categorías: acciones que se deberían vender y acciones que se deberían conservar.</span><span class="sxs-lookup"><span data-stu-id="d5abf-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="d5abf-122">La regresión logística es el algoritmo que se usa para la clasificación.</span><span class="sxs-lookup"><span data-stu-id="d5abf-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="d5abf-123">La API de regresión logística de Spark es útil para la *clasificación binaria*, o para la clasificación de datos de entrada en uno de los dos grupos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="d5abf-124">Para obtener más información acerca de la regresión logística, consulte [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="d5abf-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="d5abf-125">En resumen, el proceso de regresión logística genera una *función logística* que se puede usar para predecir la probabilidad de que un vector de entrada pertenezca a un grupo o al otro.</span><span class="sxs-lookup"><span data-stu-id="d5abf-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="d5abf-126">Ejemplo de análisis predictivo en datos de inspección alimentaria</span><span class="sxs-lookup"><span data-stu-id="d5abf-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="d5abf-127">En este ejemplo usará Spark para llevar a cabo un análisis predictivo sobre unos datos de inspección alimentaria (**Food_Inspections1.csv**) que se han adquirido a través del [portal de datos de la ciudad de Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="d5abf-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="d5abf-128">Este conjunto de datos contiene información sobre las inspecciones alimentarias que se llevaron a cabo en establecimientos de Chicago (información sobre cada establecimiento, las infracciones que se detectaron (en caso de detectarse alguna) y los resultados de la inspección).</span><span class="sxs-lookup"><span data-stu-id="d5abf-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="d5abf-129">El archivo de datos CSV ya está disponible en la cuenta de almacenamiento asociada al clúster, en **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="d5abf-130">En los pasos siguientes, va a desarrollar un modelo para ver lo que es necesario para superar o no una inspección de alimentos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="d5abf-131">Empezar a compilar una aplicación de aprendizaje automático de Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="d5abf-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="d5abf-132">Desde [Azure Portal](https://portal.azure.com/), en el panel de inicio, haga clic en el icono del clúster Spark (si lo ancló al panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="d5abf-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="d5abf-133">También puede navegar hasta el clúster en **Examinar todo** > **Clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="d5abf-134">En la hoja del clúster Spark, haga clic en **Panel de clúster** y, luego, en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="d5abf-135">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="d5abf-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5abf-136">También puede comunicarse con el equipo Jupyter Notebook en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d5abf-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="d5abf-137">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="d5abf-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="d5abf-138">Cree un cuaderno.</span><span class="sxs-lookup"><span data-stu-id="d5abf-138">Create a notebook.</span></span> <span data-ttu-id="d5abf-139">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="d5abf-140">![Crear un cuaderno de Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="d5abf-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="d5abf-141">Se crea y se abre un nuevo cuaderno con el nombre Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="d5abf-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="d5abf-142">Haga clic en el nombre del cuaderno en la parte superior y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="d5abf-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="d5abf-143">![Proporcionar un nombre para el cuaderno](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Proporcionar un nombre para el cuaderno")</span><span class="sxs-lookup"><span data-stu-id="d5abf-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="d5abf-144">Dado que creó un cuaderno con el kernel PySpark, no necesitará crear ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="d5abf-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="d5abf-145">Los contextos de Spark y Hive se crean automáticamente al ejecutar la primera celda de código.</span><span class="sxs-lookup"><span data-stu-id="d5abf-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="d5abf-146">Puede empezar a crear la aplicación de aprendizaje automático importando los tipos necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="d5abf-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="d5abf-147">Para ello, coloque el cursor en la celda y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="d5abf-148">Construcción de una trama de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="d5abf-148">Construct an input dataframe</span></span>
<span data-ttu-id="d5abf-149">Podemos usar `sqlContext` para realizar las transformaciones de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="d5abf-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="d5abf-150">La primera tarea consiste en cargar los datos de ejemplo (**[Food_Inspections1.csv**]) en una *trama de datos* de Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="d5abf-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="d5abf-151">Dado que los datos sin procesar están en formato CSV, tiene que usar el contexto de Spark para extraer cada línea del archivo en memoria como texto no estructurado; a continuación, utilice la biblioteca CSV de Python para analizar cada línea individualmente.</span><span class="sxs-lookup"><span data-stu-id="d5abf-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="d5abf-152">Ahora tenemos el archivo CSV como un conjunto RDD.</span><span class="sxs-lookup"><span data-stu-id="d5abf-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="d5abf-153">Vamos a recuperar una fila del RDD para comprender el esquema de los datos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="d5abf-154">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="d5abf-155">La salida anterior nos da una idea del esquema del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="d5abf-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="d5abf-156">Incluye el nombre de cada establecimiento, el tipo de establecimiento, la dirección, los datos de las inspecciones y la ubicación, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="d5abf-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="d5abf-157">Seleccionemos algunas columnas que nos van a ser útiles para nuestro análisis predictivo y agrupemos los resultados como una trama de datos, que luego usaremos para crear una tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="d5abf-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="d5abf-158">Ahora tenemos una *trama de datos*, `df`, en la que podemos realizar el análisis.</span><span class="sxs-lookup"><span data-stu-id="d5abf-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="d5abf-159">También contamos con una llamada a la tabla temporal **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="d5abf-160">Hemos incluido cuatro columnas de interés en la trama de datos: **id** (identificador), **name** (nombre), **results** (resultados) y **violations** (infracciones).</span><span class="sxs-lookup"><span data-stu-id="d5abf-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="d5abf-161">Vamos a obtener una pequeña muestra de los datos:</span><span class="sxs-lookup"><span data-stu-id="d5abf-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="d5abf-162">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="d5abf-163">Comprensión de los datos</span><span class="sxs-lookup"><span data-stu-id="d5abf-163">Understand the data</span></span>
1. <span data-ttu-id="d5abf-164">Vamos a empezar a hacernos una idea de lo que contiene el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="d5abf-165">Por ejemplo, ¿cuáles son los diferentes valores en la columna **results** ?</span><span class="sxs-lookup"><span data-stu-id="d5abf-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="d5abf-166">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="d5abf-167">Una visualización rápida puede ayudarnos a razonar sobre la distribución de estos resultados.</span><span class="sxs-lookup"><span data-stu-id="d5abf-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="d5abf-168">Ya tenemos los datos en una tabla temporal **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="d5abf-169">Puede ejecutar la siguiente consulta SQL en la tabla para una mejor descripción de cómo se distribuyen los resultados.</span><span class="sxs-lookup"><span data-stu-id="d5abf-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="d5abf-170">La instrucción mágica `%%sql` seguida de `-o countResultsdf` garantiza que el resultado de la consulta persista localmente en el servidor de Jupyter (normalmente, el nodo principal del clúster).</span><span class="sxs-lookup"><span data-stu-id="d5abf-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="d5abf-171">El resultado se conserva como una trama de datos [Pandas](http://pandas.pydata.org/) con el nombre especificado **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="d5abf-172">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-172">You should see an output like the following:</span></span>

    <span data-ttu-id="d5abf-173">![Salida de la consulta SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Salida de la consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="d5abf-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="d5abf-174">Para más información sobre la instrucción mágica `%%sql`, así como otras instrucciones mágicas disponibles con el kernel de PySpark, consulte [Kernels disponibles en Jupyter Notebook con clústeres de Spark en HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="d5abf-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="d5abf-175">También puede utilizar Matplotlib, una biblioteca que se usa para construir la visualización de datos, para crear un gráfico.</span><span class="sxs-lookup"><span data-stu-id="d5abf-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="d5abf-176">Dado que el gráfico debe crearse a partir de la trama de datos localmente persistente **countResultsdf**, el fragmento de código debe comenzar con la instrucción mágica `%%local`.</span><span class="sxs-lookup"><span data-stu-id="d5abf-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="d5abf-177">Esto garantiza que el código se ejecuta localmente en el servidor de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d5abf-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="d5abf-178">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-178">You should see an output like the following:</span></span>

    <span data-ttu-id="d5abf-179">![Salida de la aplicación de aprendizaje automático de Spark: gráfico circular con cinco resultados de inspección distintos](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Salida de resultados de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="d5abf-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="d5abf-180">Vemos que una inspección puede tener cinco resultados diferentes:</span><span class="sxs-lookup"><span data-stu-id="d5abf-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="d5abf-181">Business not located (no se encontró el negocio)</span><span class="sxs-lookup"><span data-stu-id="d5abf-181">Business not located</span></span>
   * <span data-ttu-id="d5abf-182">Fail (no superado)</span><span class="sxs-lookup"><span data-stu-id="d5abf-182">Fail</span></span>
   * <span data-ttu-id="d5abf-183">Pass (pasado)</span><span class="sxs-lookup"><span data-stu-id="d5abf-183">Pass</span></span>
   * <span data-ttu-id="d5abf-184">Pss w/ conditions (superado con condiciones)</span><span class="sxs-lookup"><span data-stu-id="d5abf-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="d5abf-185">Out of Business (negocio cerrado)</span><span class="sxs-lookup"><span data-stu-id="d5abf-185">Out of Business</span></span>

     <span data-ttu-id="d5abf-186">Vamos a desarrollar un modelo que pueda predecir el resultado de una inspección de alimentos, teniendo en cuenta las infracciones (violations).</span><span class="sxs-lookup"><span data-stu-id="d5abf-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="d5abf-187">Puesto que la regresión logística es un método de clasificación binaria, tiene sentido agrupar los datos en dos categorías: **Fail** y **Pass**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="d5abf-188">"Pass w/ Conditions" sigue siendo una categoría Pass (superado), por lo que cuando se entrena el modelo, consideraremos los dos resultados como equivalentes.</span><span class="sxs-lookup"><span data-stu-id="d5abf-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="d5abf-189">Los datos que tienen los otros resultados ("Business Not Located" o "Out of Business") no son útiles, por lo que los eliminaremos de nuestro conjunto de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="d5abf-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="d5abf-190">Esta eliminación no tiene importancia ya que estas dos categorías constituyen un porcentaje muy pequeño de los resultados.</span><span class="sxs-lookup"><span data-stu-id="d5abf-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="d5abf-191">Vamos a seguir y convertir nuestra trama de datos existente (`df`) en una trama de datos nueva, donde cada inspección se representa como un par de etiquetas de infracción.</span><span class="sxs-lookup"><span data-stu-id="d5abf-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="d5abf-192">En nuestro caso, una etiqueta de `0.0` representa un resultado de "no superado", una etiqueta de `1.0` representa un resultado de "pasado" y una etiqueta de `-1.0` representa resultados que no sean los dos anteriores.</span><span class="sxs-lookup"><span data-stu-id="d5abf-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="d5abf-193">Filtraremos esos otros resultados al calcular la nueva trama de datos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="d5abf-194">Vamos a recuperar una fila para ver el aspecto de los datos etiquetados.</span><span class="sxs-lookup"><span data-stu-id="d5abf-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="d5abf-195">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="d5abf-196">Creación de un modelo de regresión logística a partir de la trama de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="d5abf-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="d5abf-197">Nuestra última tarea consiste en convertir los datos etiquetados a un formato que se pueda analizar con regresión logística.</span><span class="sxs-lookup"><span data-stu-id="d5abf-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="d5abf-198">La entrada a un algoritmo de regresión logística debe ser un conjunto de *pares de vector de característica de etiqueta*, donde el "vector de característica" es un vector de números que representa el punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="d5abf-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="d5abf-199">Por lo tanto, tenemos que convertir la columna "violations", que está semiestructurada y contiene numerosos comentarios de texto sin formato, en una matriz de números reales que una máquina pueda comprender.</span><span class="sxs-lookup"><span data-stu-id="d5abf-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="d5abf-200">Un enfoque estándar en el aprendizaje automático para procesar el lenguaje natural consiste en asignar a cada palabra diferente un "índice" y, a continuación, pasar un vector al algoritmo de aprendizaje automático, de forma que el valor de cada índice contenga la frecuencia relativa de esa palabra en la cadena de texto.</span><span class="sxs-lookup"><span data-stu-id="d5abf-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="d5abf-201">MLlib proporciona una forma sencilla de efectuar esta operación.</span><span class="sxs-lookup"><span data-stu-id="d5abf-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="d5abf-202">En primer lugar, vamos a tratar como tokens todas las cadenas de infracciones para obtener las palabras de cada cadena.</span><span class="sxs-lookup"><span data-stu-id="d5abf-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="d5abf-203">Luego, use un `HashingTF` para convertir cada conjunto de tokens en un vector de característica que se pueda pasar al algoritmo de regresión logística para construir un modelo.</span><span class="sxs-lookup"><span data-stu-id="d5abf-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="d5abf-204">Llevaremos a cabo todos estos pasos en secuencia mediante una "canalización".</span><span class="sxs-lookup"><span data-stu-id="d5abf-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="d5abf-205">Evaluación del modelo en un conjunto de datos de prueba independiente</span><span class="sxs-lookup"><span data-stu-id="d5abf-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="d5abf-206">Podemos usar el modelo que hemos creado anteriormente para *predecir* cuáles serán los resultados de las nuevas inspecciones, basándose en las infracciones que se han observado.</span><span class="sxs-lookup"><span data-stu-id="d5abf-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="d5abf-207">Hemos probado este modelo en el conjunto de datos **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="d5abf-208">Ahora, vamos a usar un segundo conjunto, **Food_Inspections2.csv**, para *evaluar* la solidez de este modelo con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="d5abf-209">Este segundo conjunto de datos (**Food_Inspections2.csv**) debe estar ya en el contenedor de almacenamiento predeterminado asociado al clúster.</span><span class="sxs-lookup"><span data-stu-id="d5abf-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="d5abf-210">El siguiente fragmento de código crea una trama de datos, **predictionsDf**, que contiene la predicción generada por el modelo.</span><span class="sxs-lookup"><span data-stu-id="d5abf-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="d5abf-211">El fragmento de código también crea una tabla temporal, llamada **Predictions**, basada en la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="d5abf-212">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="d5abf-213">Examine una de las predicciones.</span><span class="sxs-lookup"><span data-stu-id="d5abf-213">Look at one of the predictions.</span></span> <span data-ttu-id="d5abf-214">Ejecute este fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="d5abf-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="d5abf-215">Hay una predicción para la primera entrada en el conjunto de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="d5abf-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="d5abf-216">El método `model.transform()` aplica la misma transformación a todos los datos nuevos que tengan el mismo esquema y llega a una predicción sobre cómo clasificar los datos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="d5abf-217">Podemos hacer algunas estadísticas muy sencillas para hacernos una idea del grado de precisión alcanzado por nuestras predicciones:</span><span class="sxs-lookup"><span data-stu-id="d5abf-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="d5abf-218">El resultado tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5abf-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="d5abf-219">El uso de la regresión logística con Spark nos ofrece un modelo preciso de la relación entre las descripciones de las infracciones en inglés y el hecho de si un negocio determinado superará o no una inspección de alimentos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="d5abf-220">Creación de una representación visual de la predicción</span><span class="sxs-lookup"><span data-stu-id="d5abf-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="d5abf-221">Ahora podemos crear una visualización final que nos ayude a analizar los resultados de esta prueba.</span><span class="sxs-lookup"><span data-stu-id="d5abf-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="d5abf-222">Empezaremos por extraer los distintos resultados y predicciones de la tabla temporal **Predictions** creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d5abf-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="d5abf-223">Las siguientes consultas separan la salida en distintos grupos: *true_positive*, *false_positive*, *true_negative* y *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="d5abf-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="d5abf-224">En las consultas siguientes, hay que desactivar la visualización mediante el uso de `-q` y guardar también la salida (usando `-o`) como tramas de datos que pueden usarse con la instrucción mágica `%%local`.</span><span class="sxs-lookup"><span data-stu-id="d5abf-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="d5abf-225">Por último, utilice el siguiente fragmento de código para generar el gráfico mediante **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="d5abf-226">Debería ver la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="d5abf-226">You should see the following output:</span></span>

    <span data-ttu-id="d5abf-227">![Salida de la aplicación de aprendizaje automático de Spark: gráfico circular con porcentajes de inspecciones alimentarias no superadas](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Salida de resultados de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="d5abf-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="d5abf-228">En este gráfico, un resultado "positivo" hace referencia a la inspección de alimentos no superada, mientras que un resultado negativo hace referencia a una inspección pasada.</span><span class="sxs-lookup"><span data-stu-id="d5abf-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="d5abf-229">Cierre del cuaderno</span><span class="sxs-lookup"><span data-stu-id="d5abf-229">Shut down the notebook</span></span>
<span data-ttu-id="d5abf-230">Cuando haya terminado de ejecutar la aplicación, deberá cerrar el cuaderno para liberar los recursos.</span><span class="sxs-lookup"><span data-stu-id="d5abf-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="d5abf-231">Para ello, en el menú **Archivo** del cuaderno, haga clic en **Cerrar y detener**.</span><span class="sxs-lookup"><span data-stu-id="d5abf-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="d5abf-232">Con esta acción se cerrará el cuaderno.</span><span class="sxs-lookup"><span data-stu-id="d5abf-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="d5abf-233"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d5abf-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d5abf-234">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="d5abf-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d5abf-235">Escenarios</span><span class="sxs-lookup"><span data-stu-id="d5abf-235">Scenarios</span></span>
* [<span data-ttu-id="d5abf-236">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="d5abf-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d5abf-237">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="d5abf-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d5abf-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="d5abf-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d5abf-239">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5abf-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d5abf-240">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d5abf-240">Create and run applications</span></span>
* [<span data-ttu-id="d5abf-241">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="d5abf-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d5abf-242">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="d5abf-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d5abf-243">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="d5abf-243">Tools and extensions</span></span>
* [<span data-ttu-id="d5abf-244">Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="d5abf-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d5abf-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="d5abf-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d5abf-246">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5abf-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d5abf-247">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5abf-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d5abf-248">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="d5abf-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="d5abf-249">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="d5abf-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="d5abf-250">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="d5abf-250">Manage resources</span></span>
* [<span data-ttu-id="d5abf-251">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="d5abf-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d5abf-252">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d5abf-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
