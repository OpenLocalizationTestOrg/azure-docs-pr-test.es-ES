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
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Usar Spark MLlib toobuild una aplicación de aprendizaje automático y analizar un conjunto de datos

Obtenga información acerca de cómo toouse Spark **MLlib** toocreate un análisis predictivos de aplicación toodo simple en un conjunto de datos abierto de aprendizaje automático. De las bibliotecas de aprendizaje automático integradas de Spark, en este ejemplo se usa una *clasificación* mediante una regresión logística. 

> [!TIP]
> Este ejemplo también está disponible en formato de cuaderno de Jupyter en un clúster Spark (Linux) que se crea en HDInsight. experiencia de Bloc de notas de Hello le permite ejecutar fragmentos de código de Python Hola desde Bloc de notas de hello propio. tutorial de hello toofollow desde dentro de un bloc de notas, cree un Spark clúster e inicie Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). A continuación, ejecute el Bloc de notas de hello **aprendizaje automático de Spark - análisis predictivos en datos de la inspección de alimentos con MLlib.ipynb** en hello **Python** carpeta.
>
>

MLlib es una biblioteca básica de Spark que proporciona numerosas utilidades que resultan prácticas para las tareas de aprendizaje automático, como utilidades adecuadas para:

* clasificación
* Regresión
* Agrupación en clústeres
* Modelado de tema
* Descomposición en valores singulares (SVD) y Análisis de los componentes principales (PCA)
* Comprobación de hipótesis y cálculo de estadísticas de ejemplo

## <a name="what-are-classification-and-logistic-regression"></a>¿Qué entendemos por clasificación y por regresión logística?
*Clasificación*, una tarea, de aprendizaje de automático popular es Hola proceso de ordenación de datos de entrada en categorías. Es trabajo Hola de un toofigure de algoritmo de clasificación más información sobre cómo tooassign "etiqueta" tooinput datos que proporcione. Por ejemplo, imagine un algoritmo de aprendizaje de máquina que acepta información bursátil como entrada y divide Hola existencias en dos categorías: existencias que debe vender tanto que debería tener.

La regresión logística es el algoritmo de Hola que utilice para la clasificación. La API de regresión logística de Spark es útil para la *clasificación binaria*, o para la clasificación de datos de entrada en uno de los dos grupos. Para obtener más información acerca de la regresión logística, consulte [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).

En resumen, proceso de Hola de regresión logística genera un *función logística* que pueden ser utilizados toopredict Hola probabilidad que un vector de entrada pertenece a un grupo u Hola otro.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Ejemplo de análisis predictivo en datos de inspección alimentaria
En este ejemplo, use Spark tooperform algunos análisis predictivos de datos de la inspección de comida (**Food_Inspections1.csv**) que se ha adquirido a través de hello [portal de datos de la ciudad de Chicago](https://data.cityofchicago.org/). Este conjunto de datos contiene información acerca de los controles de establecimiento de alimentos que se llevaron a cabo en Chicago, incluida la información sobre cada uno de ellos, infracciones de hello encuentran (si existe) y Hola resultados de inspección de Hola. archivo de datos CSV Hello ya está disponible en hello cuenta de almacenamiento asociada con el clúster de hello en **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

En hello estos pasos, puede desarrolla un modelo toosee lo que cuesta toopass o se producirá un error en una inspección de comida.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Empezar a compilar una aplicación de aprendizaje automático de Spark MLlib
1. De hello [portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.   
1. En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.

   > [!NOTE]
   > También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Cree un cuaderno. Haga clic en **Nuevo** y, luego, en **PySpark**.

    ![Crear un cuaderno de Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Crear un nuevo cuaderno de Jupyter")
1. Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.

    ![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "proporcione un nombre para el Bloc de notas de Hola")
1. Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente. contextos de Spark y Hive Hola se crean automáticamente cuando se ejecuta la primera celda de código de hello. Puede empezar a crear la máquina en la aplicación de aprendizaje mediante la importación de tipos de hello necesarios para este escenario. toodo por lo tanto, coloque cursor de hello en la celda de hello y presione **MAYÚS + ENTRAR**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Construcción de una trama de datos de entrada
Podemos usar `sqlContext` tooperform transformaciones en los datos estructurados. Hola primera tarea es datos de ejemplo de Hola tooload ((**Food_Inspections1.csv**)) en una instancia de SQL Spark *trama de datos*.

1. Dado que los datos sin procesar de hello están en un formato CSV, necesitamos toouse Hola Spark contexto toopull cada línea del archivo de hello en la memoria como texto no estructurado; a continuación, se utiliza tooparse de biblioteca CSV de Python cada línea individualmente.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. Ahora tenemos el archivo CSV de hello como un diseño dirigido por responsabilidades.  esquema de hello toounderstand de datos de hello, recuperamos una fila de hello RDD.

        inspections.take(1)

    Debería ver una salida similar Hola siguiente:

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
1. Hello salida anterior nos da una idea del esquema de Hola Hola del archivo de entrada. Incluye el nombre de Hola de cada establecimiento, el tipo de saludo de establecimiento, dirección de hello, hello y datos de inspecciones hello, ubicación de hello, entre otras cosas. Vamos a seleccionar unas pocas columnas que son útiles para nuestro análisis predictivos y agrupar los resultados de hello como una trama de datos, que es, a continuación, usar toocreate una tabla temporal.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Ahora tenemos una *trama de datos*, `df`, en la que podemos realizar el análisis. También contamos con una llamada a la tabla temporal **CountResults**. Hemos incluido cuatro columnas de interés en la trama de datos de hello: **identificador**, **nombre**, **resultados**, y **infracciones**.

    Vamos a una pequeña muestra de datos de hello:

        df.show(5)

    Debería ver una salida similar Hola siguiente:

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

## <a name="understand-hello-data"></a>Comprender los datos de Hola
1. Comencemos tooget una idea de lo que contiene el conjunto de datos. Por ejemplo, ¿qué valores distintos de hello en hello **resultados** columna?

        df.select('results').distinct().show()

    Debería ver una salida similar Hola siguiente:

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
1. Una visualización rápida puede ayudarnos a razonar sobre la distribución de Hola de estos resultados. Ya tenemos datos hello en una tabla temporal **CountResults**. Puede ejecutar Hola después de consulta SQL contra Hola tabla tooget una mejor comprensión de cómo se distribuyen los resultados de Hola.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Hola `%%sql` mágico seguido `-o countResultsdf` garantiza que la salida de hello de consulta de Hola se conserva localmente en el servidor de Jupyter Hola (normalmente Hola nodo principal del clúster de hello). salida de Hello se almacena como un [Pandas](http://pandas.pydata.org/) trama de datos con hello especificado nombre **countResultsdf**.

    Debería ver una salida similar Hola siguiente:

    ![Salida de la consulta SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Salida de la consulta SQL")

    Para obtener más información acerca de hello `%%sql` mágico y otros magics disponibles con kernel PySpark de hello, vea [núcleos disponibles en los equipos portátiles Jupyter con clústeres de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. También puede utilizar Matplotlib, una biblioteca usa tooconstruct visualización de datos, toocreate un gráfico. Porque se debe crear trazado de Hola de hello localmente conservan **countResultsdf** trama de datos, el fragmento de código de hello debe comienzan con hello `%%local` magia. Esto garantiza que el código de hello se ejecuta localmente en el servidor de Jupyter Hola.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Debería ver una salida similar Hola siguiente:

    ![Salida de la aplicación de aprendizaje automático de Spark: gráfico circular con cinco resultados de inspección distintos](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Salida de resultados de aprendizaje automático de Spark")
1. Vemos que una inspección puede tener cinco resultados diferentes:

   * Business not located (no se encontró el negocio)
   * Fail (no superado)
   * Pass (pasado)
   * Pss w/ conditions (superado con condiciones)
   * Out of Business (negocio cerrado)

     Permítanos desarrollar un modelo que se puede adivinar el resultado de hello de una inspección de comida, infracciones de hello determinado. Puesto que la regresión logística es un método de clasificación binaria, tiene sentido toogroup nuestros datos en dos categorías: **producirá un error** y **pasar**. Un "pasar con condiciones" sigue siendo un paso, por lo que cuando se entrena el modelo de hello, consideramos Hola dos resultados equivalentes. Datos con hello otros resultados ("No se encuentra empresarial" o "Out of Business") no son útiles para quitarlos de nuestro conjunto de entrenamiento. Debe ser correcto ya que estas dos categorías constituyen un porcentaje muy pequeño de los resultados de Hola de todos modos.
1. Vamos a seguir y convertir nuestra trama de datos existente (`df`) en una trama de datos nueva, donde cada inspección se representa como un par de etiquetas de infracción. En nuestro caso, una etiqueta de `0.0` representa un resultado de "no superado", una etiqueta de `1.0` representa un resultado de "pasado" y una etiqueta de `-1.0` representa resultados que no sean los dos anteriores. Se filtran los otros resultados al calcular la trama de datos nueva Hola.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee datos parece que la etiqueta qué hello, vamos a recuperar una fila.

        labeledData.take(1)

    Debería ver una salida similar Hola siguiente:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Crear un modelo de regresión logística de trama de datos de entrada de Hola
La tarea final es hello tooconvert con la etiqueta de datos en un formato que se puede analizar por regresión logística. algoritmo de regresión logística de Hello tooa entrada debe ser un conjunto de *pares de vector de característica de etiqueta*, donde hello "vector de característica" es un vector de números representa el punto de entrada de Hola. Por lo tanto, necesitamos columna de infracciones"hello" tooconvert, que es semiestructurados y contiene muchos comentarios de matriz de tooan de texto sin formato, de los números reales que una máquina puede comprender fácilmente.

Un enfoque de aprendizaje de máquina estándar de lenguaje natural de procesamiento es tooassign cada palabra distinct un "índice" y, a continuación, pase una máquina de vectores de toohello algoritmo de aprendizaje de forma que el valor de cada índice contiene frecuencia relativa de Hola de esa palabra en el texto hello cadena.

MLlib proporciona una manera sencilla de tooperform esta operación. En primer lugar, "dividir" cada infracciones cadena tooget Hola palabras individuales de cada cadena. A continuación, utilice un `HashingTF` tooconvert cada conjunto de tokens en un vector de característica que se puede tooconstruct de algoritmo de regresión logística toohello pasado un modelo. Llevaremos a cabo todos estos pasos en secuencia mediante una "canalización".

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Evaluar el modelo de hello en un conjunto de datos de prueba independiente
Podemos usar modelo Hola hemos creado con anterioridad demasiado*predecir* qué Hola serán resultados de los nuevos controles, en función de las infracciones de Hola que se han observado. Se entrenó este modelo en el conjunto de datos de hello **Food_Inspections1.csv**. Nos gustaría usar un segundo conjunto de datos, **Food_Inspections2.csv**, demasiado*evaluar* Hola intensidad de este modelo con nuevos datos. Este segundo conjunto de datos (**Food_Inspections2.csv**) ya debe estar en el contenedor de almacenamiento de hello predeterminado asociado con el clúster de Hola.

1. Hello fragmento de código siguiente crea una trama de datos nueva, **predictionsDf** que contiene la predicción de hello generada por el modelo de Hola. fragmento de código de Hello también crea una tabla temporal denominada **predicciones** en función de la trama de datos de Hola.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Debería ver una salida similar Hola siguiente:

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
1. Examine una de las predicciones de Hola. Ejecute este fragmento de código:

        predictionsDf.take(1)

   Hay una predicción para la primera entrada de hello en el conjunto de datos de prueba de Hola.
1. Hola `model.transform()` Hola aplica el método mismo datos nuevos de tooany de transformación con Hola mismo esquema y llegan a una predicción de cómo tooclassify Hola datos. Podemos hacer una idea del grado de precisión nuestro las predicciones fueron algunos tooget estadísticas muy sencillas:

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    salida de Hello aspecto Hola siguiente:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Usar la regresión logística con Spark nos da un modelo preciso de relación de hello entre las descripciones de las infracciones en inglés y si una determinada empresa podría pasar o se producirá un error en una inspección de comida.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Crear una representación visual de la predicción de Hola
Ahora podemos crear un toohelp de visualización final que nos razonar sobre resultados de Hola de esta prueba.

1. Comenzamos extrayendo distintas predicciones de Hola y Hola resultantes **predicciones** tabla temporal creada anteriormente. Hello las consultas siguientes Hola otra salida distinta como *true_positive*, *false_positive*, *true_negative*, y *false_negative*. En consultas de hello siguientes, es necesario desactivar la visualización mediante el uso de `-q` y también guarda la salida de hello (mediante el uso de `-o`) como tramas de datos que se puede usar con hello `%%local` magia.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Por último, utilice Hola siguiente fragmento de código toogenerate Hola trazado usando **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Debería ver Hola después de salida:

    ![Salida de la aplicación de aprendizaje automático de Spark: gráfico circular con porcentajes de inspecciones alimentarias no superadas](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Salida de resultados de aprendizaje automático de Spark")

    En este gráfico, un resultado "positivo" hace referencia toohello no se pudo comida inspección, mientras que un resultado negativo hace referencia tooa pasado la inspección.

## <a name="shut-down-hello-notebook"></a>Cierre el Bloc de notas de Hola
Una vez haya terminado de ejecutar la aplicación hello, debería apagar recursos de hello toorelease de hello Bloc de notas. toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**. Esto apaga y se cierra Hola Bloc de notas.

## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark Streaming: Use Spark in HDInsight for building real-time streaming applications](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)
