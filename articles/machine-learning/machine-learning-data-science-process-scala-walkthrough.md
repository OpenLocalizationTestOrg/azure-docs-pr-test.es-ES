---
title: aaaData ciencia mediante Scala y Spark en Azure | Documentos de Microsoft
description: "¿Cómo toouse Scala para tareas con de aprendizaje de automático supervisado Hola los paquetes escalables de MLlib y aprendizaje automático de Spark de Spark en un clúster de Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>Ciencia de datos mediante Scala y Spark en Azure
Este artículo muestra cómo toouse Scala para tareas de aprendizaje automático supervisado con hello MLlib escalable Spark y aprendizaje automático de Spark paquetes en un clúster de Azure HDInsight Spark. Le guía a través de las tareas de Hola que constituyen hello [proceso de ciencia de datos](http://aka.ms/datascienceprocess): recopilación de datos y exploración, visualización, ingeniería de característica, modelado y consumo de modelo. los modelos de Hello en el artículo Hola incluyen regresión logística y lineal, los bosques aleatorios y los árboles incrementados de degradado (GBTs), además tootwo común supervisado tareas de aprendizaje automático:

* Problema de regresión: predicción de cantidad de sugerencia de hello ($) para un recorrido de taxi
* Clasificación binaria: predicción de si se dará propina o no (1/0) en una carrera de taxi

proceso de modelado de Hello requiere aprendizaje y evaluación en un conjunto de datos de prueba y métricas de precisión relevante. En este artículo, aprenderá cómo toostore estos modelos de almacenamiento de blobs de Azure y cómo tooscore y evaluar su rendimiento predictivo. En este artículo también cubre la Hola temas de cómo toooptimize modelos mediante el uso de barrido de la validación cruzada y parámetro hyper más avanzados. datos de Hello utilizados son un ejemplo de Hola 2013 NYC taxi tarifas y recorridos del conjunto de datos disponible en GitHub.

[Scala](http://www.scala-lang.org/), un lenguaje basado en máquina virtual Java a hello, integra los conceptos de lenguaje funcional y orientada a objetos. Es un lenguaje escalable que se adapta perfectamente toodistributed de procesamiento en la nube de hello y se ejecuta en Azure Spark clústeres.

[Spark](http://spark.apache.org/) es un marco de trabajo de procesamiento en paralelo de código abierto que admite en memoria tooboost Hola rendimiento de aplicaciones de análisis de grandes cantidades de datos del procesamiento. motor de procesamiento de Hello Spark se compila para acelerar el proceso, facilidad de uso y análisis sofisticados. Las capacidades de cálculo distribuido en memoria de Spark lo convierten en una buena opción para algoritmos iterativos en los cálculos de gráficos y aprendizaje automático. Hola [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) paquete proporciona un conjunto uniforme de alto nivel API que se basa en datos marcos que pueden ayudarle a crear y optimizar las canalizaciones de aprendizaje de automático resulta muy práctico. [MLlib](http://spark.apache.org/mllib/) Library de aprendizaje automático escalable de Spark, que ofrece capacidades de modelado entorno distribuido de toothis.

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) es Hola hospedado de Azure oferta de Spark de código abierto. También incluye compatibilidad para Jupyter Scala blocs de notas en clúster de Spark hello y puede tootransform de las consultas interactivas de ejecución Spark SQL, filtrar y visualizar los datos almacenados en el almacenamiento de blobs de Azure. Hola Scala fragmentos de código de este artículo que ofrecen soluciones de Hola y muestran gráficos relevantes de hello toovisualize datos de saludo se ejecutan en blocs de notas de Jupyter instalados en los clústeres de Spark Hola. pasos de modelado de Hello en estos temas tiene código que se muestra cómo tootrain, evaluar, guardar y utilizar cada tipo de modelo.

pasos de instalación de Hola y el código de este artículo son para 3.4 de Azure HDInsight Spark 1.6. Sin embargo, Hola código de este artículo y hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) son genéricos y deben funcionar en cualquier clúster de Spark. el programa de instalación de clúster de Hola y paso para la administración puede ser ligeramente diferente de lo que se muestra en este artículo si no usas HDInsight Spark.

> [!NOTE]
> Para un tema que muestra cómo toouse Python en lugar de Scala toocomplete las tareas de un proceso de ciencia de datos-to-end, vea [ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
* Debe tener una suscripción de Azure. Si aún no tiene una, [consiga una evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Es necesario un Hola de toocomplete de clúster de Azure HDInsight 3.4 Spark 1.6 siguiendo los procedimientos. toocreate un clúster, consulte las instrucciones de hello en [Introducción: crear Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Establecer tipo de clúster de Hola y la versión en hello **Seleccionar tipo de clúster** menú.

![Configuración de tipo de clúster de HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Para obtener una descripción de datos de ida y vuelta de hello NYC taxi e instrucciones sobre cómo tooexecute código de Jupyter notebook en clúster de Spark hello, consulte las secciones relevantes de hello en [información general de ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Ejecutar el código Scala desde Jupyter notebook en clúster de Spark Hola
Puede iniciar Jupyter notebook de hello portal de Azure. Busque el clúster de Spark hello en el panel y, a continuación, haga clic en él tooenter página de administración de hello para el clúster. A continuación, haga clic en **paneles de clúster**y, a continuación, haga clic en **Jupyter Notebook** tooopen Bloc de notas de hello asociado con el clúster de Spark Hola.

![Panel del clúster y cuadernos de Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

También puede ir a https://&lt;nombreDeClúster&gt;.azurehdinsight.net/jupyter para acceder a los cuadernos de Jupyter Notebook. Reemplace *clustername* con nombre hello del clúster. Es necesaria la contraseña de hello para los administrador cuenta tooaccess hello Jupyter blocs de notas.

![Ir tooJupyter portátiles mediante el nombre del clúster de Hola](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Seleccione **Scala** toosee un directorio que tiene algunos ejemplos de preestablecida blocs de notas que hello PySpark API de uso. Hola exploración de modelado y puntuación mediante el Bloc de notas de Scala.ipynb que contiene ejemplos de código de hello para este conjunto de temas de Spark está disponible en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

Puede cargar el Bloc de notas de hello directamente desde GitHub toohello servidor de Jupyter Notebook en su clúster Spark. En la página principal de Jupyter, haga clic en hello **cargar** botón. En el Explorador de archivos de hello, pegue dirección URL de GitHub (contenido sin formato) de Hola de Bloc de notas de hello Scala y, a continuación, haga clic en **abiertos**. el Bloc de notas de Hello Scala está disponible en hello después de la dirección URL:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Instalación: contextos preestablecidos de Spark y Hive, instrucciones mágicas de Spark y bibliotecas de Spark
### <a name="preset-spark-and-hive-contexts"></a>Contextos preestablecidos de Spark y Hive
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


los kernels de Spark Hola que se proporcionan con blocs de notas de Jupyter tengan contextos preestablecidos. No es necesario tooexplicitly Hola Spark o subárbol contextos del conjunto antes de empezar a trabajar con la aplicación hello que está desarrollando. Hello contextos preestablecidos son:

* `sc` para SparkContext
* `sqlContext` para HiveContext

### <a name="spark-magics"></a>Instrucciones mágicas de Spark
Hello kernel Spark proporciona algunos predefinidas "magics", que son comandos especiales que se pueden llamar con `%%`. Dos de estos comandos se usan en los siguientes ejemplos de código de hello.

* `%%local`Especifica que el código de hello en las líneas siguientes se ejecutarán localmente. código de Hello debe ser código Scala válido.
* `%%sql -o <variable name>` ejecuta una consulta de Hive en `sqlContext`. Si hello `-o` se pasa el parámetro, resultado de hello de consulta de Hola se conserva en hello `%%local` Scala contexto como una trama de datos de Spark.

Para obtener más información sobre los kernels de Hola para blocs de notas de Jupyter y sus predefinido "magics" que se llama a con `%%` (por ejemplo, `%%local`), consulte [núcleos disponibles para equipos portátiles Jupyter con HDInsight Spark Linux se agrupa en HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Importación de bibliotecas
Importar Hola Spark, MLlib y otras bibliotecas que necesitará utilizando Hola siguiente código.

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>Ingesta de datos
Hola primer paso en hello proceso de ciencia de datos es datos de hello tooingest que desea tooanalyze. Lleve los datos de Hola desde orígenes externos o sistemas que se encuentra en el entorno de exploración y el modelado de datos. En este artículo, los datos de saludo que se introduce están un ejemplo de 0,1% combinadas de hello taxi de ida y vuelta y tarifa del archivo (almacenado como un archivo .tsv). entorno de exploración y el modelado de datos de Hello es Spark. Esta sección contiene Hola Hola de toocomplete de código después de la serie de tareas:

1. Establecer rutas de acceso a directorios para almacenar datos y modelos.
2. Leer Hola entrada conjunto de datos (almacenado como un archivo .tsv).
3. Definir un esquema para los datos de Hola y Hola limpia.
4. Crear una trama de datos limpia y almacenarla en la memoria caché.
5. Registrar datos de hello como una tabla temporal en SQLContext.
6. Consultar la tabla de hello e importar resultados de hello en una trama de datos.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Establecer rutas de acceso de directorio para las ubicaciones de almacenamiento en el Almacenamiento de blobs de Azure.
Spark puede leer y escribir tooAzure el almacenamiento de blobs. Puede usar Spark tooprocess cualquiera de los datos existentes y, a continuación, almacene los resultados de hello en almacenamiento de blobs.

modelos de toosave o archivos de almacenamiento de blobs, deberá tooproperly especificar ruta de acceso de Hola. Contenedor predeterminado de Hola de referencia adjunta clúster de Spark toohello mediante una ruta de acceso que comienza con `wasb:///`. Haga referencia a otras ubicaciones mediante `wasb://`.

Hello ejemplo de código siguiente especifica Hola ubicación de toobe de datos de entrada de hello leer y Hola ruta de acceso tooBlob almacenamiento de clúster de Spark toohello adjunto donde se guardará el modelo de Hola.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Importar datos, crear un diseño dirigido por responsabilidades y definir una trama de datos según el esquema de toohello
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Salida:**

Celda de tiempo toorun Hola: 8 segundos.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Consultar la tabla de hello e importar resultados en una trama de datos
A continuación, tabla de Hola de consulta para la tarifa, pasajeros y datos de tip; filtrar datos dañados y periféricas; e imprimir varias filas.

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**Salida:**

| fare_amount | passenger_count | tip_amount | tipped |
| --- | --- | --- | --- |
|        13.5 |1.0 |2.9 |1.0 |
|        16.0 |2.0 |3.4 |1.0 |
|        10.5 |2.0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Visualización y exploración de datos
Después de conectar datos hello en Spark, Hola siguiente paso de hello proceso de ciencia de datos es toogain una comprensión más profunda de los datos de hello mediante exploración y visualización. En esta sección, examina los datos de taxi de hello mediante consultas SQL. A continuación, importar resultados de hello en un tooplot del marco de datos Hola características posibles para la inspección visual y las variables de destino mediante el uso de características de visualización automática de Hola de Jupyter.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Usar local y datos de SQL tooplot mágica
De forma predeterminada, la salida de hello de cualquier fragmento de código que se ejecuta desde Jupyter notebook está disponible en contexto de Hola de sesión de Hola que se conserva en los nodos de trabajador de Hola. Si desea toosave un nodos de trabajador de toohello de ida y vuelta para cada cálculo y, si todos los hello datos que necesita para el cálculo está disponible localmente en el nodo del servidor de Jupyter hello (que es el nodo principal de hello), puede usar hello `%%local` mágico código de hello toorun fragmento de código en el servidor de Jupyter Hola.

* **Instrucciones mágicas SQL** (`%%sql`). Hola kernel HDInsight Spark admite consultas de HiveQL de en línea fácil en SQLContext. Hola (`-o VARIABLE_NAME`) argumento conserva la salida de hello de consulta SQL de hello como una trama de datos de Pandas en el servidor de Jupyter Hola. Esto significa que estará disponible en modo local Hola.
* **Instrucciones mágicas**`%%local` Hola `%%local` mágico ejecuta código de hello localmente en el servidor de Jupyter hello, que es el nodo principal de Hola Hola del clúster de HDInsight. Normalmente, se utiliza `%%local` mágico junto con hello `%%sql` mágico con hello `-o` parámetro. Hola `-o` parámetro debería conservar la salida de hello de consulta SQL Hola localmente y, a continuación, `%%local` mágico desencadenaría conjunto siguiente de Hola de toorun de fragmento de código localmente en la salida de hello de consultas SQL de Hola que se guarda localmente.

### <a name="query-hello-data-by-using-sql"></a>Consultar datos de hello mediante SQL
Esta consulta recupera Hola taxi ciclos de ida y cantidad de tarifa, número de pasajeros y cantidad de sugerencia.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

En el siguiente código de hello, Hola `%%local` mágico crea una trama de datos local, sqlResults. Puede usar sqlResults tooplot mediante matplotlib.

> [!TIP]
> La instrucción mágica local se emplea varias veces en este tutorial. Si el conjunto de datos es grande, por favor, ejemplo toocreate una trama de datos que cabe en la memoria local.
> 
> 

### <a name="plot-hello-data"></a>Trazar datos Hola
Se pueden trazar mediante código de Python después de trama de datos de hello en el contexto local como una trama de datos de Pandas.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 núcleo de Spark Hola automáticamente visualiza la salida de hello de consultas SQL (HiveQL) después de ejecutar código de hello. Puede elegir entre varios tipos de visualizaciones:

* Tabla
* Circular
* Línea
* Ámbito
* Barra

Aquí es datos de saludo de hello código tooplot:

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**Salida:**

![Histograma del importe de la propina](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Importe de las propinas por número de pasajeros](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Importe de las propinas por importe de la tarifa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Creación y transformación de características, y preparación de datos para su entrada en funciones de modelado
Para las funciones de modelado basadas en el árbol de aprendizaje automático de Spark y MLlib, tienen tooprepare destino y características mediante diversas técnicas, como la discretización, indización, caliente una codificación y vectorización. Estos son hello toofollow de procedimientos de esta sección:

1. Creación de una nueva característica mediante la **discretización** de horas en ciclos de tráfico.
2. Aplicar **indización y estrechamente con una codificación** toocategorical características.
3. **Muestrear y dividir Hola conjunto de datos** en fracciones de entrenamiento y prueba.
4. **Especificación de variables de entrenamiento y características**, y creación de tramas de datos o datos distribuidos resistentes (RDD) de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot".
5. Automáticamente **categorizar y vectorizar características y los destinos** toouse como entradas para los modelos de aprendizaje automático.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico
Este código muestra cómo los depósitos de toocreate una nueva característica discretizando horas en vez de tráfico y cómo toocache Hola resultante trama de datos en memoria. Donde marcos RDDs y los datos se usan varias veces, el almacenamiento en caché conduce tooimproved los tiempos de ejecución. En consecuencia, podrá caché fotogramas RDDs y los datos en varias fases de hello procedimientos siguientes.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Indexación y codificación "one-hot" de características categóricas
Hola modelado y predecir las funciones de MLlib requieren características con los datos de entrada categorías toobe la indización o codifican toouse anterior. Esta sección muestra cómo tooindex o codificar las características de categorías para la entrada en hello las funciones de modelado.

Necesita tooindex o codificar los modelos de diferentes maneras, según el modelo de Hola. Por ejemplo, los modelos de regresión logística y lineal requieren una codificación "one-hot". Asimismo, una función con tres categorías puede ampliarse en tres columnas de característica. Cada columna contendría 0 o 1 según la categoría de Hola de una observación. MLlib proporciona hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) función para los activos de una codificación. Este codificador asigna una columna de la columna de etiqueta índices tooa de vectores binarios con a lo sumo un solo un valor. Con esta codificación, algoritmos que esperan las características con valores numéricas, como la regresión logística, pueden ser características toocategorical aplicada.

Aquí se transforman los ejemplos de tooshow solo cuatro variables, que son cadenas de caracteres. También se pueden indexar otras variables como variables categóricas (por ejemplo, el día de la semana) que se representan mediante valores numéricos.

Para la indexación usamos `StringIndexer()`, y para la codificación "one-hot", funciones `OneHotEncoder()` de MLlib. Este es Hola código tooindex y codificar las características de categorías:

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Salida:**

Celda de tiempo toorun Hola: 4 segundos.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Muestrear y dividir Hola conjunto de datos en fracciones de entrenamiento y prueba
Este código crea un muestreo aleatorio de datos de hello (25%, en este ejemplo). Aunque no es necesario para este ejemplo debido toohello tamaño del conjunto de datos de Hola de muestreo, Hola artículo muestra cómo puede muestrear para que sepa cómo toouse para sus propios problemas cuando sea necesario. Cuando las muestras son grandes, esto puede ahorrar mucho tiempo al entrenar modelos. A continuación, dividir ejemplo hello en una parte de entrenamiento (75%, en este ejemplo) y una prueba parte toouse (25%, en este ejemplo) en la clasificación y el modelo de regresión.

Agregue una fila de tooeach de número aleatorio (entre 0 y 1) (en una columna "rand") que puede ser subconjuntos de validación cruzada tooselect utilizados durante el entrenamiento.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Salida:**

Celda de tiempo toorun Hola: 2 segundos.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Especificación de variables de entrenamiento y características, y creación de tramas de datos o RDD de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot"
Esta sección contiene código que se muestra cómo el tipo de datos de punto tooindex datos de categorías de texto como un etiquetado y codifican, por lo que puede usar tootrain y prueba MLlib la regresión logística y otros modelos de clasificación. Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) con el formato de datos de entrada necesario para la mayoría de los algoritmos de aprendizaje automático de MLlib. Un [punto con etiqueta](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) es un vector local, denso o disperso, asociado con una etiqueta o respuesta.

En este código, puede especificar variable (dependiente) de destino de Hola y modelos de hello características toouse tootrain. Después, cree tramas de datos o RDD de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot".

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Salida:**

Celda de tiempo toorun Hola: 4 segundos.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Clasificar automáticamente y vectorizar toouse características y los destinos como entradas para los modelos de aprendizaje automático
Usar aprendizaje automático de Spark toocategorize Hola destino y características toouse en funciones de modelado basadas en el árbol. código de Hello realiza dos tareas:

* Crea un destino para la clasificación binario asignando un valor de 0 o 1 punto de datos de tooeach entre 0 y 1 con un valor de umbral de 0,5.
* Categoriza automáticamente las características. Si el número de Hola de valores numéricos distintos para todas las características es menor que 32, se clasifica por categorías en esa característica.

Este es el código de hello para estas dos tareas.

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>Clasificación binaria: predicción de si se debe dar propina
En esta sección, crea tres tipos de toopredict de modelos de clasificación binaria o no de pago de una sugerencia:

* A **modelo de regresión logística** mediante el uso de hello Spark ML `LogisticRegression()` (función)
* A **modelo de clasificación de bosque aleatorio** mediante el uso de hello Spark ML `RandomForestClassifier()` (función)
* A **degradado modelo de clasificación de árbol aumento** mediante el uso de hello MLlib `GradientBoostedTrees()` (función)

### <a name="create-a-logistic-regression-model"></a>Creación de un modelo de regresión logística
A continuación, crear un modelo de regresión logística mediante Hola Spark ML `LogisticRegression()` función. Crear modelo Hola compilar el código en una serie de pasos:

1. **Entrenar el modelo de hello** datos con un conjunto de parámetros.
2. **Evaluar el modelo de hello** en un conjunto de datos de prueba con las métricas.
3. **Guardar modelo hello** en almacenamiento de blobs para su futura utilización.
4. **Modelo de puntuación hello** con datos de prueba.
5. **Trazar resultados hello** receptor operativo curvas de característica (ROC).

Este es el código de hello para estos procedimientos:

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

Cargar, puntuación y guardar los resultados de Hola.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**Salida:**

ROC de los datos de prueba = 0,9827381497557599

Uso de Python en curva de local Pandas datos marcos tooplot Hola ROC.

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**Salida:**

![Curva de ROC sobre si se dará propina o no](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Creación de un modelo de clasificación de bosque aleatorio
A continuación, crear un modelo de clasificación de bosque aleatorio mediante Hola Spark ML `RandomForestClassifier()` función y, a continuación, evaluar el modelo de hello en los datos de prueba.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**Salida:**

ROC de los datos de prueba = 0,9847103571552683

### <a name="create-a-gbt-classification-model"></a>Creación de un modelo de clasificación GBT
A continuación, cree un modelo de clasificación GBT mediante el uso del MLlib `GradientBoostedTrees()` función y, a continuación, evaluar el modelo de hello en los datos de prueba.

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**Salida:**

Área bajo la curva de ROC = 0,9846895479241554

## <a name="regression-model-predict-tip-amount"></a>Modelo de regresión: predicción del importe de la propina
En esta sección, crea dos tipos de cantidad de regresión modelos toopredict Hola Sugerencia:

* A **modelo de regresión lineal regularizada** mediante el uso de hello Spark ML `LinearRegression()` función. Podrá guardar modelo hello y evaluar el modelo de hello en los datos de prueba.
* A **modelo de regresión de árbol de impulso de gradiente** mediante el uso de hello Spark ML `GBTRegressor()` función.

### <a name="create-a-regularized-linear-regression-model"></a>Creación de un modelo d regresión lineal regularizada
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Salida:**

Celda de tiempo toorun Hola: 13 segundos.

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**Salida:**

R-sqr de los datos de prueba = 0,5960320470835743

A continuación, consulta Hola de resultados de pruebas como una trama de datos y use toovisualize AutoVizWidget y matplotlib se.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

código de Hello crea una trama de datos local de resultado de la consulta de Hola y representa los datos de Hola. Hola `%%local` mágico crea una trama de datos local, `sqlResults`, que puede usar tooplot con matplotlib.

> [!NOTE]
> Esta instrucción mágica de Spark se emplea varias veces en este artículo. Si la cantidad de Hola de datos es grande, debe muestrear toocreate una trama de datos que cabe en la memoria local.
> 
> 

Creación de trazados con matplotlib de Python.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**Salida:**

![Importe de la propina: real frente a predicción](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Creación de un modelo de regresión GBT
Crear un modelo de regresión GBT mediante Hola Spark ML `GBTRegressor()` función y, a continuación, evaluar el modelo de hello en los datos de prueba.

[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión. Árboles de decisión de entrenamiento de GBTs forma iterativa toominimize una función de pérdida. Puede usar GBT para la clasificación y regresión. Permiten controlar características categóricas, no requieren ajustar la escala de las características y pueden capturar errores de alineación e interacciones de las características. También se pueden usar en una configuración de clasificación multiclase.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**Salida:**

R-sqr de prueba = 0,7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>Utilidades avanzadas de modelado para la optimización
En esta sección, utilizará herramientas de aprendizaje automático que los desarrolladores usan con frecuencia para la optimización de modelos. En concreto, pueden optimizarse los modelos de aprendizaje automático de tres maneras distintas mediante barrido de parámetros y validación cruzada:

* Dividir los datos de hello en conjuntos de entrenamiento y validación, optimizar el modelo de hello mediante el uso de barrido de parámetros hyper en un conjunto de entrenamiento y evaluar en un conjunto de validación (regresión lineal)
* Optimizar el modelo de hello mediante la validación cruzada y hyper-parámetro barrido mediante CrossValidator función del aprendizaje automático de Spark (clasificación binaria)
* Optimizar el modelo Hola utilizando código personalizado de validación cruzada y barrido de parámetros toouse cualquier conjunto de parámetros y la función (regresión lineal) de aprendizaje automático

**La validación cruzada** es una técnica que evalúa la medida un modelo entrenado en un conjunto conocido de datos generalizará toopredict Hola características de conjuntos de datos en el que no se está entrenada. Hello una idea general de esta técnica es que un modelo está entrenado en un conjunto de datos de los datos conocidos, y, a continuación, hello precisión de las predicciones se prueba en un conjunto de datos independiente. Una implementación común es toodivide un conjunto de datos en *k*-contrae y, a continuación, entrenar modelo de hello en un modo round-robin en todos excepto uno de los subconjuntos de Hola.

**Optimización de Hyper-parámetro** Hola problema de elegir un conjunto de hyper-parámetros para un algoritmo de aprendizaje, normalmente con el objetivo de Hola de optimizar una medida de rendimiento del algoritmo de hello en un conjunto de datos independiente. Un parámetro de hyper-es un valor que debe especificar fuera de procedimiento de entrenamiento del modelo de Hola. Suposiciones acerca de los valores de parámetro de hyper-pueden afectar a flexibilidad de Hola y la precisión del modelo de Hola. Árboles de decisión tienen hyper-parámetros, por ejemplo, como Hola había deseado profundidad y el número de hojas de árbol de Hola. Debe establecer un término de penalización para las clasificaciones incorrectas en las máquinas de vectores de soporte (SVM).

Una optimización de parámetro hyper de tooperform forma común es toouse una búsqueda de la cuadrícula, también se denomina un **barrido de parámetros**. En una búsqueda de la cuadrícula, se realiza una búsqueda exhaustiva a través de los valores de hello de un subconjunto específico de espacio en hyper-parámetro hello para un algoritmo de aprendizaje. La validación cruzada puede proporcionar un toosort de métrica de rendimiento out resultados óptimos Hola generado por el algoritmo de búsqueda de cuadrícula de Hola. Si usas barrido de hyper-parámetros de validación cruzada, puede ayudar a problemas de límite como sobreajuste una tootraining de datos de modelo. De esta manera, el modelo de hello conserva Hola capacidad tooapply toohello general conjunto de datos del que Hola se extrajeron los datos de entrenamiento.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Optimización del modelo de regresión lineal mediante barrido de hiperparámetros
A continuación, dividir datos en conjuntos de entrenamiento y validación, use hyper-parámetro barrido en un entrenamiento establezca toooptimize Hola modelo y evaluar en un conjunto de validación (regresión lineal).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**Salida:**

R-sqr de prueba = 0,6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Optimizar el modelo de clasificación binaria de hello mediante el uso de barrido de la validación cruzada y parámetro de hyper-
Esta sección muestra cómo modelar con validación cruzada y parámetro hyper barrido toooptimize una clasificación binaria. Esto utiliza Hola Spark ML `CrossValidator` función.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Salida:**

Celda de tiempo toorun Hola: 33 segundos.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Optimizar el modelo de regresión lineal de hello mediante código personalizado de validación cruzada y barrido de parámetros
A continuación, optimizar el modelo de hello mediante código personalizado e identificar los parámetros del modelo mejor hello mediante criterios de Hola de mayor precisión. A continuación, cree el modelo final hello, evaluar el modelo de hello en los datos de prueba y Guardar modelo hello en almacenamiento de blobs. Por último, cargar el modelo de hello, puntuar datos de prueba y evaluar la precisión.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**Salida:**

Celda de tiempo toorun Hola: 61 segundos.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Uso automático en Scala de los modelos de aprendizaje automático creados en Spark
Para obtener información general de temas que le guiarán por tareas de Hola que componen el proceso de ciencia de datos de hello en Azure, consulte [proceso de ciencia de datos de equipo](http://aka.ms/datascienceprocess).

[Tutoriales de proceso de ciencia de datos del equipo](data-science-process-walkthroughs.md) describe otros tutoriales to-end que muestran pasos Hola Hola proceso de ciencia de datos de equipo para escenarios concretos. Hola tutoriales también muestran el funcionamiento de cloud toocombine y herramientas local y servicios en un flujo de trabajo o canalización toocreate una aplicación inteligente.

[Puntuación de modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md) se muestra cómo toouse Scala código tooautomatically cargar y puntuación nuevos conjuntos de datos con modelos de aprendizaje automático creados en Spark y guardarlos en el almacenamiento de blobs de Azure. Puede seguir instrucciones Hola siempre que haya y simplemente reemplace Hola código Python con código de Scala en este artículo para un consumo automatizado.

