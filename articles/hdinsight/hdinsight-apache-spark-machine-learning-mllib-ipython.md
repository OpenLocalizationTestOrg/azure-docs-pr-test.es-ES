---
title: aaaMachine aprendizaje de ejemplo con MLlib Spark en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Spark MLlib toocreate una aplicación de aprendizaje de máquina que analiza un conjunto de datos mediante la clasificación de regresión logística."
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="4503f-104">Usar Spark MLlib toobuild una aplicación de aprendizaje automático y analizar un conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="4503f-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="4503f-105">Obtenga información acerca de cómo toouse Spark **MLlib** toocreate un análisis predictivos de aplicación toodo simple en un conjunto de datos abierto de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="4503f-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="4503f-106">De las bibliotecas de aprendizaje automático integradas de Spark, en este ejemplo se usa una *clasificación* mediante una regresión logística.</span><span class="sxs-lookup"><span data-stu-id="4503f-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="4503f-107">Este ejemplo también está disponible en formato de cuaderno de Jupyter en un clúster Spark (Linux) que se crea en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4503f-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="4503f-108">experiencia de Bloc de notas de Hello le permite ejecutar fragmentos de código de Python Hola desde Bloc de notas de hello propio.</span><span class="sxs-lookup"><span data-stu-id="4503f-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="4503f-109">tutorial de hello toofollow desde dentro de un bloc de notas, cree un Spark clúster e inicie Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="4503f-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="4503f-110">A continuación, ejecute el Bloc de notas de hello **aprendizaje automático de Spark - análisis predictivos en datos de la inspección de alimentos con MLlib.ipynb** en hello **Python** carpeta.</span><span class="sxs-lookup"><span data-stu-id="4503f-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="4503f-111">MLlib es una biblioteca básica de Spark que proporciona numerosas utilidades que resultan prácticas para las tareas de aprendizaje automático, como utilidades adecuadas para:</span><span class="sxs-lookup"><span data-stu-id="4503f-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="4503f-112">clasificación</span><span class="sxs-lookup"><span data-stu-id="4503f-112">Classification</span></span>
* <span data-ttu-id="4503f-113">Regresión</span><span class="sxs-lookup"><span data-stu-id="4503f-113">Regression</span></span>
* <span data-ttu-id="4503f-114">Agrupación en clústeres</span><span class="sxs-lookup"><span data-stu-id="4503f-114">Clustering</span></span>
* <span data-ttu-id="4503f-115">Modelado de tema</span><span class="sxs-lookup"><span data-stu-id="4503f-115">Topic modeling</span></span>
* <span data-ttu-id="4503f-116">Descomposición en valores singulares (SVD) y Análisis de los componentes principales (PCA)</span><span class="sxs-lookup"><span data-stu-id="4503f-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="4503f-117">Comprobación de hipótesis y cálculo de estadísticas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4503f-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="4503f-118">¿Qué entendemos por clasificación y por regresión logística?</span><span class="sxs-lookup"><span data-stu-id="4503f-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="4503f-119">*Clasificación*, una tarea, de aprendizaje de automático popular es Hola proceso de ordenación de datos de entrada en categorías.</span><span class="sxs-lookup"><span data-stu-id="4503f-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="4503f-120">Es trabajo Hola de un toofigure de algoritmo de clasificación más información sobre cómo tooassign "etiqueta" tooinput datos que proporcione.</span><span class="sxs-lookup"><span data-stu-id="4503f-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="4503f-121">Por ejemplo, imagine un algoritmo de aprendizaje de máquina que acepta información bursátil como entrada y divide Hola existencias en dos categorías: existencias que debe vender tanto que debería tener.</span><span class="sxs-lookup"><span data-stu-id="4503f-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="4503f-122">La regresión logística es el algoritmo de Hola que utilice para la clasificación.</span><span class="sxs-lookup"><span data-stu-id="4503f-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="4503f-123">La API de regresión logística de Spark es útil para la *clasificación binaria*, o para la clasificación de datos de entrada en uno de los dos grupos.</span><span class="sxs-lookup"><span data-stu-id="4503f-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="4503f-124">Para obtener más información acerca de la regresión logística, consulte [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="4503f-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="4503f-125">En resumen, proceso de Hola de regresión logística genera un *función logística* que pueden ser utilizados toopredict Hola probabilidad que un vector de entrada pertenece a un grupo u Hola otro.</span><span class="sxs-lookup"><span data-stu-id="4503f-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="4503f-126">Ejemplo de análisis predictivo en datos de inspección alimentaria</span><span class="sxs-lookup"><span data-stu-id="4503f-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="4503f-127">En este ejemplo, use Spark tooperform algunos análisis predictivos de datos de la inspección de comida (**Food_Inspections1.csv**) que se ha adquirido a través de hello [portal de datos de la ciudad de Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="4503f-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="4503f-128">Este conjunto de datos contiene información acerca de los controles de establecimiento de alimentos que se llevaron a cabo en Chicago, incluida la información sobre cada uno de ellos, infracciones de hello encuentran (si existe) y Hola resultados de inspección de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="4503f-129">archivo de datos CSV Hello ya está disponible en hello cuenta de almacenamiento asociada con el clúster de hello en **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="4503f-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="4503f-130">En hello estos pasos, puede desarrolla un modelo toosee lo que cuesta toopass o se producirá un error en una inspección de comida.</span><span class="sxs-lookup"><span data-stu-id="4503f-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="4503f-131">Empezar a compilar una aplicación de aprendizaje automático de Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="4503f-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="4503f-132">De hello [portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="4503f-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="4503f-133">También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4503f-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="4503f-134">En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="4503f-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="4503f-135">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4503f-136">También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="4503f-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="4503f-137">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="4503f-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="4503f-138">Cree un cuaderno.</span><span class="sxs-lookup"><span data-stu-id="4503f-138">Create a notebook.</span></span> <span data-ttu-id="4503f-139">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="4503f-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="4503f-140">![Crear un cuaderno de Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="4503f-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="4503f-141">Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="4503f-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="4503f-142">Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="4503f-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="4503f-143">![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "proporcione un nombre para el Bloc de notas de Hola")</span><span class="sxs-lookup"><span data-stu-id="4503f-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="4503f-144">Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="4503f-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="4503f-145">contextos de Spark y Hive Hola se crean automáticamente cuando se ejecuta la primera celda de código de hello.</span><span class="sxs-lookup"><span data-stu-id="4503f-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="4503f-146">Puede empezar a crear la máquina en la aplicación de aprendizaje mediante la importación de tipos de hello necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="4503f-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="4503f-147">toodo por lo tanto, coloque cursor de hello en la celda de hello y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="4503f-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="4503f-148">Construcción de una trama de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="4503f-148">Construct an input dataframe</span></span>
<span data-ttu-id="4503f-149">Podemos usar `sqlContext` tooperform transformaciones en los datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="4503f-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="4503f-150">Hola primera tarea es datos de ejemplo de Hola tooload ((**Food_Inspections1.csv**)) en una instancia de SQL Spark *trama de datos*.</span><span class="sxs-lookup"><span data-stu-id="4503f-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="4503f-151">Dado que los datos sin procesar de hello están en un formato CSV, necesitamos toouse Hola Spark contexto toopull cada línea del archivo de hello en la memoria como texto no estructurado; a continuación, se utiliza tooparse de biblioteca CSV de Python cada línea individualmente.</span><span class="sxs-lookup"><span data-stu-id="4503f-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="4503f-152">Ahora tenemos el archivo CSV de hello como un diseño dirigido por responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="4503f-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="4503f-153">esquema de hello toounderstand de datos de hello, recuperamos una fila de hello RDD.</span><span class="sxs-lookup"><span data-stu-id="4503f-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="4503f-154">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-154">You should see an output like hello following:</span></span>

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="4503f-155">Hello salida anterior nos da una idea del esquema de Hola Hola del archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="4503f-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="4503f-156">Incluye el nombre de Hola de cada establecimiento, el tipo de saludo de establecimiento, dirección de hello, hello y datos de inspecciones hello, ubicación de hello, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="4503f-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="4503f-157">Vamos a seleccionar unas pocas columnas que son útiles para nuestro análisis predictivos y agrupar los resultados de hello como una trama de datos, que es, a continuación, usar toocreate una tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="4503f-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="4503f-158">Ahora tenemos una *trama de datos*, `df`, en la que podemos realizar el análisis.</span><span class="sxs-lookup"><span data-stu-id="4503f-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="4503f-159">También contamos con una llamada a la tabla temporal **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="4503f-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="4503f-160">Hemos incluido cuatro columnas de interés en la trama de datos de hello: **identificador**, **nombre**, **resultados**, y **infracciones**.</span><span class="sxs-lookup"><span data-stu-id="4503f-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="4503f-161">Vamos a una pequeña muestra de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="4503f-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="4503f-162">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-162">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a><span data-ttu-id="4503f-163">Comprender los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="4503f-163">Understand hello data</span></span>
1. <span data-ttu-id="4503f-164">Comencemos tooget una idea de lo que contiene el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="4503f-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="4503f-165">Por ejemplo, ¿qué valores distintos de hello en hello **resultados** columna?</span><span class="sxs-lookup"><span data-stu-id="4503f-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="4503f-166">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="4503f-167">Una visualización rápida puede ayudarnos a razonar sobre la distribución de Hola de estos resultados.</span><span class="sxs-lookup"><span data-stu-id="4503f-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="4503f-168">Ya tenemos datos hello en una tabla temporal **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="4503f-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="4503f-169">Puede ejecutar Hola después de consulta SQL contra Hola tabla tooget una mejor comprensión de cómo se distribuyen los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="4503f-170">Hola `%%sql` mágico seguido `-o countResultsdf` garantiza que la salida de hello de consulta de Hola se conserva localmente en el servidor de Jupyter Hola (normalmente Hola nodo principal del clúster de hello).</span><span class="sxs-lookup"><span data-stu-id="4503f-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="4503f-171">salida de Hello se almacena como un [Pandas](http://pandas.pydata.org/) trama de datos con hello especificado nombre **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="4503f-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="4503f-172">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="4503f-173">![Salida de la consulta SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Salida de la consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="4503f-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="4503f-174">Para obtener más información acerca de hello `%%sql` mágico y otros magics disponibles con kernel PySpark de hello, vea [núcleos disponibles en los equipos portátiles Jupyter con clústeres de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="4503f-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="4503f-175">También puede utilizar Matplotlib, una biblioteca usa tooconstruct visualización de datos, toocreate un gráfico.</span><span class="sxs-lookup"><span data-stu-id="4503f-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="4503f-176">Porque se debe crear trazado de Hola de hello localmente conservan **countResultsdf** trama de datos, el fragmento de código de hello debe comienzan con hello `%%local` magia.</span><span class="sxs-lookup"><span data-stu-id="4503f-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="4503f-177">Esto garantiza que el código de hello se ejecuta localmente en el servidor de Jupyter Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="4503f-178">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="4503f-179">![Salida de la aplicación de aprendizaje automático de Spark: gráfico circular con cinco resultados de inspección distintos](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Salida de resultados de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="4503f-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="4503f-180">Vemos que una inspección puede tener cinco resultados diferentes:</span><span class="sxs-lookup"><span data-stu-id="4503f-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="4503f-181">Business not located (no se encontró el negocio)</span><span class="sxs-lookup"><span data-stu-id="4503f-181">Business not located</span></span>
   * <span data-ttu-id="4503f-182">Fail (no superado)</span><span class="sxs-lookup"><span data-stu-id="4503f-182">Fail</span></span>
   * <span data-ttu-id="4503f-183">Pass (pasado)</span><span class="sxs-lookup"><span data-stu-id="4503f-183">Pass</span></span>
   * <span data-ttu-id="4503f-184">Pss w/ conditions (superado con condiciones)</span><span class="sxs-lookup"><span data-stu-id="4503f-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="4503f-185">Out of Business (negocio cerrado)</span><span class="sxs-lookup"><span data-stu-id="4503f-185">Out of Business</span></span>

     <span data-ttu-id="4503f-186">Permítanos desarrollar un modelo que se puede adivinar el resultado de hello de una inspección de comida, infracciones de hello determinado.</span><span class="sxs-lookup"><span data-stu-id="4503f-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="4503f-187">Puesto que la regresión logística es un método de clasificación binaria, tiene sentido toogroup nuestros datos en dos categorías: **producirá un error** y **pasar**.</span><span class="sxs-lookup"><span data-stu-id="4503f-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="4503f-188">Un "pasar con condiciones" sigue siendo un paso, por lo que cuando se entrena el modelo de hello, consideramos Hola dos resultados equivalentes.</span><span class="sxs-lookup"><span data-stu-id="4503f-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="4503f-189">Datos con hello otros resultados ("No se encuentra empresarial" o "Out of Business") no son útiles para quitarlos de nuestro conjunto de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="4503f-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="4503f-190">Debe ser correcto ya que estas dos categorías constituyen un porcentaje muy pequeño de los resultados de Hola de todos modos.</span><span class="sxs-lookup"><span data-stu-id="4503f-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="4503f-191">Vamos a seguir y convertir nuestra trama de datos existente (`df`) en una trama de datos nueva, donde cada inspección se representa como un par de etiquetas de infracción.</span><span class="sxs-lookup"><span data-stu-id="4503f-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="4503f-192">En nuestro caso, una etiqueta de `0.0` representa un resultado de "no superado", una etiqueta de `1.0` representa un resultado de "pasado" y una etiqueta de `-1.0` representa resultados que no sean los dos anteriores.</span><span class="sxs-lookup"><span data-stu-id="4503f-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="4503f-193">Se filtran los otros resultados al calcular la trama de datos nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="4503f-194">toosee datos parece que la etiqueta qué hello, vamos a recuperar una fila.</span><span class="sxs-lookup"><span data-stu-id="4503f-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="4503f-195">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="4503f-196">Crear un modelo de regresión logística de trama de datos de entrada de Hola</span><span class="sxs-lookup"><span data-stu-id="4503f-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="4503f-197">La tarea final es hello tooconvert con la etiqueta de datos en un formato que se puede analizar por regresión logística.</span><span class="sxs-lookup"><span data-stu-id="4503f-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="4503f-198">algoritmo de regresión logística de Hello tooa entrada debe ser un conjunto de *pares de vector de característica de etiqueta*, donde hello "vector de característica" es un vector de números representa el punto de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="4503f-199">Por lo tanto, necesitamos columna de infracciones"hello" tooconvert, que es semiestructurados y contiene muchos comentarios de matriz de tooan de texto sin formato, de los números reales que una máquina puede comprender fácilmente.</span><span class="sxs-lookup"><span data-stu-id="4503f-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="4503f-200">Un enfoque de aprendizaje de máquina estándar de lenguaje natural de procesamiento es tooassign cada palabra distinct un "índice" y, a continuación, pase una máquina de vectores de toohello algoritmo de aprendizaje de forma que el valor de cada índice contiene frecuencia relativa de Hola de esa palabra en el texto hello cadena.</span><span class="sxs-lookup"><span data-stu-id="4503f-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="4503f-201">MLlib proporciona una manera sencilla de tooperform esta operación.</span><span class="sxs-lookup"><span data-stu-id="4503f-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="4503f-202">En primer lugar, "dividir" cada infracciones cadena tooget Hola palabras individuales de cada cadena.</span><span class="sxs-lookup"><span data-stu-id="4503f-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="4503f-203">A continuación, utilice un `HashingTF` tooconvert cada conjunto de tokens en un vector de característica que se puede tooconstruct de algoritmo de regresión logística toohello pasado un modelo.</span><span class="sxs-lookup"><span data-stu-id="4503f-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="4503f-204">Llevaremos a cabo todos estos pasos en secuencia mediante una "canalización".</span><span class="sxs-lookup"><span data-stu-id="4503f-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="4503f-205">Evaluar el modelo de hello en un conjunto de datos de prueba independiente</span><span class="sxs-lookup"><span data-stu-id="4503f-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="4503f-206">Podemos usar modelo Hola hemos creado con anterioridad demasiado*predecir* qué Hola serán resultados de los nuevos controles, en función de las infracciones de Hola que se han observado.</span><span class="sxs-lookup"><span data-stu-id="4503f-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="4503f-207">Se entrenó este modelo en el conjunto de datos de hello **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="4503f-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="4503f-208">Nos gustaría usar un segundo conjunto de datos, **Food_Inspections2.csv**, demasiado*evaluar* Hola intensidad de este modelo con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="4503f-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="4503f-209">Este segundo conjunto de datos (**Food_Inspections2.csv**) ya debe estar en el contenedor de almacenamiento de hello predeterminado asociado con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="4503f-210">Hello fragmento de código siguiente crea una trama de datos nueva, **predictionsDf** que contiene la predicción de hello generada por el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="4503f-211">fragmento de código de Hello también crea una tabla temporal denominada **predicciones** en función de la trama de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="4503f-212">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="4503f-213">Examine una de las predicciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-213">Look at one of hello predictions.</span></span> <span data-ttu-id="4503f-214">Ejecute este fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="4503f-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="4503f-215">Hay una predicción para la primera entrada de hello en el conjunto de datos de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="4503f-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="4503f-216">Hola `model.transform()` Hola aplica el método mismo datos nuevos de tooany de transformación con Hola mismo esquema y llegan a una predicción de cómo tooclassify Hola datos.</span><span class="sxs-lookup"><span data-stu-id="4503f-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="4503f-217">Podemos hacer una idea del grado de precisión nuestro las predicciones fueron algunos tooget estadísticas muy sencillas:</span><span class="sxs-lookup"><span data-stu-id="4503f-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="4503f-218">salida de Hello aspecto Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4503f-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="4503f-219">Usar la regresión logística con Spark nos da un modelo preciso de relación de hello entre las descripciones de las infracciones en inglés y si una determinada empresa podría pasar o se producirá un error en una inspección de comida.</span><span class="sxs-lookup"><span data-stu-id="4503f-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="4503f-220">Crear una representación visual de la predicción de Hola</span><span class="sxs-lookup"><span data-stu-id="4503f-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="4503f-221">Ahora podemos crear un toohelp de visualización final que nos razonar sobre resultados de Hola de esta prueba.</span><span class="sxs-lookup"><span data-stu-id="4503f-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="4503f-222">Comenzamos extrayendo distintas predicciones de Hola y Hola resultantes **predicciones** tabla temporal creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4503f-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="4503f-223">Hello las consultas siguientes Hola otra salida distinta como *true_positive*, *false_positive*, *true_negative*, y *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="4503f-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="4503f-224">En consultas de hello siguientes, es necesario desactivar la visualización mediante el uso de `-q` y también guarda la salida de hello (mediante el uso de `-o`) como tramas de datos que se puede usar con hello `%%local` magia.</span><span class="sxs-lookup"><span data-stu-id="4503f-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="4503f-225">Por último, utilice Hola siguiente fragmento de código toogenerate Hola trazado usando **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="4503f-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="4503f-226">Debería ver Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="4503f-226">You should see hello following output:</span></span>

    <span data-ttu-id="4503f-227">![Salida de la aplicación de aprendizaje automático de Spark: gráfico circular con porcentajes de inspecciones alimentarias no superadas](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Salida de resultados de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="4503f-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="4503f-228">En este gráfico, un resultado "positivo" hace referencia toohello no se pudo comida inspección, mientras que un resultado negativo hace referencia tooa pasado la inspección.</span><span class="sxs-lookup"><span data-stu-id="4503f-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="4503f-229">Cierre el Bloc de notas de Hola</span><span class="sxs-lookup"><span data-stu-id="4503f-229">Shut down hello notebook</span></span>
<span data-ttu-id="4503f-230">Una vez haya terminado de ejecutar la aplicación hello, debería apagar recursos de hello toorelease de hello Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="4503f-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="4503f-231">toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.</span><span class="sxs-lookup"><span data-stu-id="4503f-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="4503f-232">Esto apaga y se cierra Hola Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="4503f-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="4503f-233"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="4503f-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4503f-234">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4503f-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="4503f-235">Escenarios</span><span class="sxs-lookup"><span data-stu-id="4503f-235">Scenarios</span></span>
* [<span data-ttu-id="4503f-236">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="4503f-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4503f-237">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4503f-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4503f-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="4503f-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="4503f-239">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4503f-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4503f-240">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4503f-240">Create and run applications</span></span>
* [<span data-ttu-id="4503f-241">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="4503f-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4503f-242">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="4503f-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4503f-243">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="4503f-243">Tools and extensions</span></span>
* [<span data-ttu-id="4503f-244">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="4503f-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4503f-245">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="4503f-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4503f-246">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4503f-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4503f-247">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="4503f-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4503f-248">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="4503f-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4503f-249">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="4503f-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4503f-250">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="4503f-250">Manage resources</span></span>
* [<span data-ttu-id="4503f-251">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4503f-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4503f-252">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="4503f-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
