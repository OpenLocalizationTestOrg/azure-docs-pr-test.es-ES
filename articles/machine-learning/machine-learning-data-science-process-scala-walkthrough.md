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
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="bd9ce-103">Ciencia de datos mediante Scala y Spark en Azure</span><span class="sxs-lookup"><span data-stu-id="bd9ce-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="bd9ce-104">Este artículo muestra cómo toouse Scala para tareas de aprendizaje automático supervisado con hello MLlib escalable Spark y aprendizaje automático de Spark paquetes en un clúster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="bd9ce-105">Le guía a través de las tareas de Hola que constituyen hello [proceso de ciencia de datos](http://aka.ms/datascienceprocess): recopilación de datos y exploración, visualización, ingeniería de característica, modelado y consumo de modelo.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="bd9ce-106">los modelos de Hello en el artículo Hola incluyen regresión logística y lineal, los bosques aleatorios y los árboles incrementados de degradado (GBTs), además tootwo común supervisado tareas de aprendizaje automático:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="bd9ce-107">Problema de regresión: predicción de cantidad de sugerencia de hello ($) para un recorrido de taxi</span><span class="sxs-lookup"><span data-stu-id="bd9ce-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="bd9ce-108">Clasificación binaria: predicción de si se dará propina o no (1/0) en una carrera de taxi</span><span class="sxs-lookup"><span data-stu-id="bd9ce-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="bd9ce-109">proceso de modelado de Hello requiere aprendizaje y evaluación en un conjunto de datos de prueba y métricas de precisión relevante.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="bd9ce-110">En este artículo, aprenderá cómo toostore estos modelos de almacenamiento de blobs de Azure y cómo tooscore y evaluar su rendimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="bd9ce-111">En este artículo también cubre la Hola temas de cómo toooptimize modelos mediante el uso de barrido de la validación cruzada y parámetro hyper más avanzados.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="bd9ce-112">datos de Hello utilizados son un ejemplo de Hola 2013 NYC taxi tarifas y recorridos del conjunto de datos disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="bd9ce-113">[Scala](http://www.scala-lang.org/), un lenguaje basado en máquina virtual Java a hello, integra los conceptos de lenguaje funcional y orientada a objetos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="bd9ce-114">Es un lenguaje escalable que se adapta perfectamente toodistributed de procesamiento en la nube de hello y se ejecuta en Azure Spark clústeres.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="bd9ce-115">[Spark](http://spark.apache.org/) es un marco de trabajo de procesamiento en paralelo de código abierto que admite en memoria tooboost Hola rendimiento de aplicaciones de análisis de grandes cantidades de datos del procesamiento.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="bd9ce-116">motor de procesamiento de Hello Spark se compila para acelerar el proceso, facilidad de uso y análisis sofisticados.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="bd9ce-117">Las capacidades de cálculo distribuido en memoria de Spark lo convierten en una buena opción para algoritmos iterativos en los cálculos de gráficos y aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="bd9ce-118">Hola [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) paquete proporciona un conjunto uniforme de alto nivel API que se basa en datos marcos que pueden ayudarle a crear y optimizar las canalizaciones de aprendizaje de automático resulta muy práctico.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="bd9ce-119">[MLlib](http://spark.apache.org/mllib/) Library de aprendizaje automático escalable de Spark, que ofrece capacidades de modelado entorno distribuido de toothis.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="bd9ce-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) es Hola hospedado de Azure oferta de Spark de código abierto.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="bd9ce-121">También incluye compatibilidad para Jupyter Scala blocs de notas en clúster de Spark hello y puede tootransform de las consultas interactivas de ejecución Spark SQL, filtrar y visualizar los datos almacenados en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="bd9ce-122">Hola Scala fragmentos de código de este artículo que ofrecen soluciones de Hola y muestran gráficos relevantes de hello toovisualize datos de saludo se ejecutan en blocs de notas de Jupyter instalados en los clústeres de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="bd9ce-123">pasos de modelado de Hello en estos temas tiene código que se muestra cómo tootrain, evaluar, guardar y utilizar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="bd9ce-124">pasos de instalación de Hola y el código de este artículo son para 3.4 de Azure HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="bd9ce-125">Sin embargo, Hola código de este artículo y hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) son genéricos y deben funcionar en cualquier clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="bd9ce-126">el programa de instalación de clúster de Hola y paso para la administración puede ser ligeramente diferente de lo que se muestra en este artículo si no usas HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="bd9ce-127">Para un tema que muestra cómo toouse Python en lugar de Scala toocomplete las tareas de un proceso de ciencia de datos-to-end, vea [ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bd9ce-128">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bd9ce-128">Prerequisites</span></span>
* <span data-ttu-id="bd9ce-129">Debe tener una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-129">You must have an Azure subscription.</span></span> <span data-ttu-id="bd9ce-130">Si aún no tiene una, [consiga una evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="bd9ce-131">Es necesario un Hola de toocomplete de clúster de Azure HDInsight 3.4 Spark 1.6 siguiendo los procedimientos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="bd9ce-132">toocreate un clúster, consulte las instrucciones de hello en [Introducción: crear Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="bd9ce-133">Establecer tipo de clúster de Hola y la versión en hello **Seleccionar tipo de clúster** menú.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Configuración de tipo de clúster de HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="bd9ce-135">Para obtener una descripción de datos de ida y vuelta de hello NYC taxi e instrucciones sobre cómo tooexecute código de Jupyter notebook en clúster de Spark hello, consulte las secciones relevantes de hello en [información general de ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="bd9ce-136">Ejecutar el código Scala desde Jupyter notebook en clúster de Spark Hola</span><span class="sxs-lookup"><span data-stu-id="bd9ce-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="bd9ce-137">Puede iniciar Jupyter notebook de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="bd9ce-138">Busque el clúster de Spark hello en el panel y, a continuación, haga clic en él tooenter página de administración de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="bd9ce-139">A continuación, haga clic en **paneles de clúster**y, a continuación, haga clic en **Jupyter Notebook** tooopen Bloc de notas de hello asociado con el clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Panel del clúster y cuadernos de Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="bd9ce-141">También puede ir a https://&lt;nombreDeClúster&gt;.azurehdinsight.net/jupyter para acceder a los cuadernos de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="bd9ce-142">Reemplace *clustername* con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="bd9ce-143">Es necesaria la contraseña de hello para los administrador cuenta tooaccess hello Jupyter blocs de notas.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Ir tooJupyter portátiles mediante el nombre del clúster de Hola](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="bd9ce-145">Seleccione **Scala** toosee un directorio que tiene algunos ejemplos de preestablecida blocs de notas que hello PySpark API de uso.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="bd9ce-146">Hola exploración de modelado y puntuación mediante el Bloc de notas de Scala.ipynb que contiene ejemplos de código de hello para este conjunto de temas de Spark está disponible en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="bd9ce-147">Puede cargar el Bloc de notas de hello directamente desde GitHub toohello servidor de Jupyter Notebook en su clúster Spark.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="bd9ce-148">En la página principal de Jupyter, haga clic en hello **cargar** botón.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="bd9ce-149">En el Explorador de archivos de hello, pegue dirección URL de GitHub (contenido sin formato) de Hola de Bloc de notas de hello Scala y, a continuación, haga clic en **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="bd9ce-150">el Bloc de notas de Hello Scala está disponible en hello después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="bd9ce-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="bd9ce-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="bd9ce-152">Instalación: contextos preestablecidos de Spark y Hive, instrucciones mágicas de Spark y bibliotecas de Spark</span><span class="sxs-lookup"><span data-stu-id="bd9ce-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="bd9ce-153">Contextos preestablecidos de Spark y Hive</span><span class="sxs-lookup"><span data-stu-id="bd9ce-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="bd9ce-154">los kernels de Spark Hola que se proporcionan con blocs de notas de Jupyter tengan contextos preestablecidos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="bd9ce-155">No es necesario tooexplicitly Hola Spark o subárbol contextos del conjunto antes de empezar a trabajar con la aplicación hello que está desarrollando.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="bd9ce-156">Hello contextos preestablecidos son:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-156">hello preset contexts are:</span></span>

* <span data-ttu-id="bd9ce-157">`sc` para SparkContext</span><span class="sxs-lookup"><span data-stu-id="bd9ce-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="bd9ce-158">`sqlContext` para HiveContext</span><span class="sxs-lookup"><span data-stu-id="bd9ce-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="bd9ce-159">Instrucciones mágicas de Spark</span><span class="sxs-lookup"><span data-stu-id="bd9ce-159">Spark magics</span></span>
<span data-ttu-id="bd9ce-160">Hello kernel Spark proporciona algunos predefinidas "magics", que son comandos especiales que se pueden llamar con `%%`.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="bd9ce-161">Dos de estos comandos se usan en los siguientes ejemplos de código de hello.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="bd9ce-162">`%%local`Especifica que el código de hello en las líneas siguientes se ejecutarán localmente.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="bd9ce-163">código de Hello debe ser código Scala válido.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="bd9ce-164">`%%sql -o <variable name>` ejecuta una consulta de Hive en `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="bd9ce-165">Si hello `-o` se pasa el parámetro, resultado de hello de consulta de Hola se conserva en hello `%%local` Scala contexto como una trama de datos de Spark.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="bd9ce-166">Para obtener más información sobre los kernels de Hola para blocs de notas de Jupyter y sus predefinido "magics" que se llama a con `%%` (por ejemplo, `%%local`), consulte [núcleos disponibles para equipos portátiles Jupyter con HDInsight Spark Linux se agrupa en HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="bd9ce-167">Importación de bibliotecas</span><span class="sxs-lookup"><span data-stu-id="bd9ce-167">Import libraries</span></span>
<span data-ttu-id="bd9ce-168">Importar Hola Spark, MLlib y otras bibliotecas que necesitará utilizando Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="bd9ce-169">Ingesta de datos</span><span class="sxs-lookup"><span data-stu-id="bd9ce-169">Data ingestion</span></span>
<span data-ttu-id="bd9ce-170">Hola primer paso en hello proceso de ciencia de datos es datos de hello tooingest que desea tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="bd9ce-171">Lleve los datos de Hola desde orígenes externos o sistemas que se encuentra en el entorno de exploración y el modelado de datos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="bd9ce-172">En este artículo, los datos de saludo que se introduce están un ejemplo de 0,1% combinadas de hello taxi de ida y vuelta y tarifa del archivo (almacenado como un archivo .tsv).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="bd9ce-173">entorno de exploración y el modelado de datos de Hello es Spark.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="bd9ce-174">Esta sección contiene Hola Hola de toocomplete de código después de la serie de tareas:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="bd9ce-175">Establecer rutas de acceso a directorios para almacenar datos y modelos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="bd9ce-176">Leer Hola entrada conjunto de datos (almacenado como un archivo .tsv).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="bd9ce-177">Definir un esquema para los datos de Hola y Hola limpia.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="bd9ce-178">Crear una trama de datos limpia y almacenarla en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="bd9ce-179">Registrar datos de hello como una tabla temporal en SQLContext.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="bd9ce-180">Consultar la tabla de hello e importar resultados de hello en una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="bd9ce-181">Establecer rutas de acceso de directorio para las ubicaciones de almacenamiento en el Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="bd9ce-182">Spark puede leer y escribir tooAzure el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="bd9ce-183">Puede usar Spark tooprocess cualquiera de los datos existentes y, a continuación, almacene los resultados de hello en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="bd9ce-184">modelos de toosave o archivos de almacenamiento de blobs, deberá tooproperly especificar ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="bd9ce-185">Contenedor predeterminado de Hola de referencia adjunta clúster de Spark toohello mediante una ruta de acceso que comienza con `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="bd9ce-186">Haga referencia a otras ubicaciones mediante `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="bd9ce-187">Hello ejemplo de código siguiente especifica Hola ubicación de toobe de datos de entrada de hello leer y Hola ruta de acceso tooBlob almacenamiento de clúster de Spark toohello adjunto donde se guardará el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="bd9ce-188">Importar datos, crear un diseño dirigido por responsabilidades y definir una trama de datos según el esquema de toohello</span><span class="sxs-lookup"><span data-stu-id="bd9ce-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
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


<span data-ttu-id="bd9ce-189">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-189">**Output:**</span></span>

<span data-ttu-id="bd9ce-190">Celda de tiempo toorun Hola: 8 segundos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="bd9ce-191">Consultar la tabla de hello e importar resultados en una trama de datos</span><span class="sxs-lookup"><span data-stu-id="bd9ce-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="bd9ce-192">A continuación, tabla de Hola de consulta para la tarifa, pasajeros y datos de tip; filtrar datos dañados y periféricas; e imprimir varias filas.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

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

<span data-ttu-id="bd9ce-193">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-193">**Output:**</span></span>

| <span data-ttu-id="bd9ce-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="bd9ce-194">fare_amount</span></span> | <span data-ttu-id="bd9ce-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="bd9ce-195">passenger_count</span></span> | <span data-ttu-id="bd9ce-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="bd9ce-196">tip_amount</span></span> | <span data-ttu-id="bd9ce-197">tipped</span><span class="sxs-lookup"><span data-stu-id="bd9ce-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="bd9ce-198">13.5</span><span class="sxs-lookup"><span data-stu-id="bd9ce-198">13.5</span></span> |<span data-ttu-id="bd9ce-199">1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-199">1.0</span></span> |<span data-ttu-id="bd9ce-200">2.9</span><span class="sxs-lookup"><span data-stu-id="bd9ce-200">2.9</span></span> |<span data-ttu-id="bd9ce-201">1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-201">1.0</span></span> |
|        <span data-ttu-id="bd9ce-202">16.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-202">16.0</span></span> |<span data-ttu-id="bd9ce-203">2.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-203">2.0</span></span> |<span data-ttu-id="bd9ce-204">3.4</span><span class="sxs-lookup"><span data-stu-id="bd9ce-204">3.4</span></span> |<span data-ttu-id="bd9ce-205">1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-205">1.0</span></span> |
|        <span data-ttu-id="bd9ce-206">10.5</span><span class="sxs-lookup"><span data-stu-id="bd9ce-206">10.5</span></span> |<span data-ttu-id="bd9ce-207">2.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-207">2.0</span></span> |<span data-ttu-id="bd9ce-208">1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-208">1.0</span></span> |<span data-ttu-id="bd9ce-209">1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ce-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="bd9ce-210">Visualización y exploración de datos</span><span class="sxs-lookup"><span data-stu-id="bd9ce-210">Data exploration and visualization</span></span>
<span data-ttu-id="bd9ce-211">Después de conectar datos hello en Spark, Hola siguiente paso de hello proceso de ciencia de datos es toogain una comprensión más profunda de los datos de hello mediante exploración y visualización.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="bd9ce-212">En esta sección, examina los datos de taxi de hello mediante consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="bd9ce-213">A continuación, importar resultados de hello en un tooplot del marco de datos Hola características posibles para la inspección visual y las variables de destino mediante el uso de características de visualización automática de Hola de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="bd9ce-214">Usar local y datos de SQL tooplot mágica</span><span class="sxs-lookup"><span data-stu-id="bd9ce-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="bd9ce-215">De forma predeterminada, la salida de hello de cualquier fragmento de código que se ejecuta desde Jupyter notebook está disponible en contexto de Hola de sesión de Hola que se conserva en los nodos de trabajador de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="bd9ce-216">Si desea toosave un nodos de trabajador de toohello de ida y vuelta para cada cálculo y, si todos los hello datos que necesita para el cálculo está disponible localmente en el nodo del servidor de Jupyter hello (que es el nodo principal de hello), puede usar hello `%%local` mágico código de hello toorun fragmento de código en el servidor de Jupyter Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="bd9ce-217">**Instrucciones mágicas SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="bd9ce-218">Hola kernel HDInsight Spark admite consultas de HiveQL de en línea fácil en SQLContext.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="bd9ce-219">Hola (`-o VARIABLE_NAME`) argumento conserva la salida de hello de consulta SQL de hello como una trama de datos de Pandas en el servidor de Jupyter Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="bd9ce-220">Esto significa que estará disponible en modo local Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="bd9ce-221">**Instrucciones mágicas**`%%local`</span><span class="sxs-lookup"><span data-stu-id="bd9ce-221">`%%local` **magic**.</span></span> <span data-ttu-id="bd9ce-222">Hola `%%local` mágico ejecuta código de hello localmente en el servidor de Jupyter hello, que es el nodo principal de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="bd9ce-223">Normalmente, se utiliza `%%local` mágico junto con hello `%%sql` mágico con hello `-o` parámetro.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="bd9ce-224">Hola `-o` parámetro debería conservar la salida de hello de consulta SQL Hola localmente y, a continuación, `%%local` mágico desencadenaría conjunto siguiente de Hola de toorun de fragmento de código localmente en la salida de hello de consultas SQL de Hola que se guarda localmente.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="bd9ce-225">Consultar datos de hello mediante SQL</span><span class="sxs-lookup"><span data-stu-id="bd9ce-225">Query hello data by using SQL</span></span>
<span data-ttu-id="bd9ce-226">Esta consulta recupera Hola taxi ciclos de ida y cantidad de tarifa, número de pasajeros y cantidad de sugerencia.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="bd9ce-227">En el siguiente código de hello, Hola `%%local` mágico crea una trama de datos local, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="bd9ce-228">Puede usar sqlResults tooplot mediante matplotlib.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="bd9ce-229">La instrucción mágica local se emplea varias veces en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="bd9ce-230">Si el conjunto de datos es grande, por favor, ejemplo toocreate una trama de datos que cabe en la memoria local.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="bd9ce-231">Trazar datos Hola</span><span class="sxs-lookup"><span data-stu-id="bd9ce-231">Plot hello data</span></span>
<span data-ttu-id="bd9ce-232">Se pueden trazar mediante código de Python después de trama de datos de hello en el contexto local como una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="bd9ce-233">núcleo de Spark Hola automáticamente visualiza la salida de hello de consultas SQL (HiveQL) después de ejecutar código de hello.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="bd9ce-234">Puede elegir entre varios tipos de visualizaciones:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="bd9ce-235">Tabla</span><span class="sxs-lookup"><span data-stu-id="bd9ce-235">Table</span></span>
* <span data-ttu-id="bd9ce-236">Circular</span><span class="sxs-lookup"><span data-stu-id="bd9ce-236">Pie</span></span>
* <span data-ttu-id="bd9ce-237">Línea</span><span class="sxs-lookup"><span data-stu-id="bd9ce-237">Line</span></span>
* <span data-ttu-id="bd9ce-238">Ámbito</span><span class="sxs-lookup"><span data-stu-id="bd9ce-238">Area</span></span>
* <span data-ttu-id="bd9ce-239">Barra</span><span class="sxs-lookup"><span data-stu-id="bd9ce-239">Bar</span></span>

<span data-ttu-id="bd9ce-240">Aquí es datos de saludo de hello código tooplot:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-240">Here's hello code tooplot hello data:</span></span>

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


<span data-ttu-id="bd9ce-241">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-241">**Output:**</span></span>

![Histograma del importe de la propina](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Importe de las propinas por número de pasajeros](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Importe de las propinas por importe de la tarifa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="bd9ce-245">Creación y transformación de características, y preparación de datos para su entrada en funciones de modelado</span><span class="sxs-lookup"><span data-stu-id="bd9ce-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="bd9ce-246">Para las funciones de modelado basadas en el árbol de aprendizaje automático de Spark y MLlib, tienen tooprepare destino y características mediante diversas técnicas, como la discretización, indización, caliente una codificación y vectorización.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="bd9ce-247">Estos son hello toofollow de procedimientos de esta sección:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="bd9ce-248">Creación de una nueva característica mediante la **discretización** de horas en ciclos de tráfico.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="bd9ce-249">Aplicar **indización y estrechamente con una codificación** toocategorical características.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="bd9ce-250">**Muestrear y dividir Hola conjunto de datos** en fracciones de entrenamiento y prueba.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="bd9ce-251">**Especificación de variables de entrenamiento y características**, y creación de tramas de datos o datos distribuidos resistentes (RDD) de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="bd9ce-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="bd9ce-252">Automáticamente **categorizar y vectorizar características y los destinos** toouse como entradas para los modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="bd9ce-253">Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico</span><span class="sxs-lookup"><span data-stu-id="bd9ce-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="bd9ce-254">Este código muestra cómo los depósitos de toocreate una nueva característica discretizando horas en vez de tráfico y cómo toocache Hola resultante trama de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="bd9ce-255">Donde marcos RDDs y los datos se usan varias veces, el almacenamiento en caché conduce tooimproved los tiempos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="bd9ce-256">En consecuencia, podrá caché fotogramas RDDs y los datos en varias fases de hello procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

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


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="bd9ce-257">Indexación y codificación "one-hot" de características categóricas</span><span class="sxs-lookup"><span data-stu-id="bd9ce-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="bd9ce-258">Hola modelado y predecir las funciones de MLlib requieren características con los datos de entrada categorías toobe la indización o codifican toouse anterior.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="bd9ce-259">Esta sección muestra cómo tooindex o codificar las características de categorías para la entrada en hello las funciones de modelado.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="bd9ce-260">Necesita tooindex o codificar los modelos de diferentes maneras, según el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="bd9ce-261">Por ejemplo, los modelos de regresión logística y lineal requieren una codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="bd9ce-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="bd9ce-262">Asimismo, una función con tres categorías puede ampliarse en tres columnas de característica.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="bd9ce-263">Cada columna contendría 0 o 1 según la categoría de Hola de una observación.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="bd9ce-264">MLlib proporciona hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) función para los activos de una codificación.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="bd9ce-265">Este codificador asigna una columna de la columna de etiqueta índices tooa de vectores binarios con a lo sumo un solo un valor.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="bd9ce-266">Con esta codificación, algoritmos que esperan las características con valores numéricas, como la regresión logística, pueden ser características toocategorical aplicada.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="bd9ce-267">Aquí se transforman los ejemplos de tooshow solo cuatro variables, que son cadenas de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="bd9ce-268">También se pueden indexar otras variables como variables categóricas (por ejemplo, el día de la semana) que se representan mediante valores numéricos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="bd9ce-269">Para la indexación usamos `StringIndexer()`, y para la codificación "one-hot", funciones `OneHotEncoder()` de MLlib.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="bd9ce-270">Este es Hola código tooindex y codificar las características de categorías:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-270">Here is hello code tooindex and encode categorical features:</span></span>

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


<span data-ttu-id="bd9ce-271">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-271">**Output:**</span></span>

<span data-ttu-id="bd9ce-272">Celda de tiempo toorun Hola: 4 segundos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="bd9ce-273">Muestrear y dividir Hola conjunto de datos en fracciones de entrenamiento y prueba</span><span class="sxs-lookup"><span data-stu-id="bd9ce-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="bd9ce-274">Este código crea un muestreo aleatorio de datos de hello (25%, en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="bd9ce-275">Aunque no es necesario para este ejemplo debido toohello tamaño del conjunto de datos de Hola de muestreo, Hola artículo muestra cómo puede muestrear para que sepa cómo toouse para sus propios problemas cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="bd9ce-276">Cuando las muestras son grandes, esto puede ahorrar mucho tiempo al entrenar modelos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="bd9ce-277">A continuación, dividir ejemplo hello en una parte de entrenamiento (75%, en este ejemplo) y una prueba parte toouse (25%, en este ejemplo) en la clasificación y el modelo de regresión.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="bd9ce-278">Agregue una fila de tooeach de número aleatorio (entre 0 y 1) (en una columna "rand") que puede ser subconjuntos de validación cruzada tooselect utilizados durante el entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

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


<span data-ttu-id="bd9ce-279">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-279">**Output:**</span></span>

<span data-ttu-id="bd9ce-280">Celda de tiempo toorun Hola: 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="bd9ce-281">Especificación de variables de entrenamiento y características, y creación de tramas de datos o RDD de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot"</span><span class="sxs-lookup"><span data-stu-id="bd9ce-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="bd9ce-282">Esta sección contiene código que se muestra cómo el tipo de datos de punto tooindex datos de categorías de texto como un etiquetado y codifican, por lo que puede usar tootrain y prueba MLlib la regresión logística y otros modelos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="bd9ce-283">Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) con el formato de datos de entrada necesario para la mayoría de los algoritmos de aprendizaje automático de MLlib.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="bd9ce-284">Un [punto con etiqueta](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) es un vector local, denso o disperso, asociado con una etiqueta o respuesta.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="bd9ce-285">En este código, puede especificar variable (dependiente) de destino de Hola y modelos de hello características toouse tootrain.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="bd9ce-286">Después, cree tramas de datos o RDD de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="bd9ce-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

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


<span data-ttu-id="bd9ce-287">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-287">**Output:**</span></span>

<span data-ttu-id="bd9ce-288">Celda de tiempo toorun Hola: 4 segundos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="bd9ce-289">Clasificar automáticamente y vectorizar toouse características y los destinos como entradas para los modelos de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="bd9ce-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="bd9ce-290">Usar aprendizaje automático de Spark toocategorize Hola destino y características toouse en funciones de modelado basadas en el árbol.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="bd9ce-291">código de Hello realiza dos tareas:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="bd9ce-292">Crea un destino para la clasificación binario asignando un valor de 0 o 1 punto de datos de tooeach entre 0 y 1 con un valor de umbral de 0,5.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="bd9ce-293">Categoriza automáticamente las características.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-293">Automatically categorizes features.</span></span> <span data-ttu-id="bd9ce-294">Si el número de Hola de valores numéricos distintos para todas las características es menor que 32, se clasifica por categorías en esa característica.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="bd9ce-295">Este es el código de hello para estas dos tareas.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-295">Here's hello code for these two tasks.</span></span>

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



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="bd9ce-296">Clasificación binaria: predicción de si se debe dar propina</span><span class="sxs-lookup"><span data-stu-id="bd9ce-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="bd9ce-297">En esta sección, crea tres tipos de toopredict de modelos de clasificación binaria o no de pago de una sugerencia:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="bd9ce-298">A **modelo de regresión logística** mediante el uso de hello Spark ML `LogisticRegression()` (función)</span><span class="sxs-lookup"><span data-stu-id="bd9ce-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="bd9ce-299">A **modelo de clasificación de bosque aleatorio** mediante el uso de hello Spark ML `RandomForestClassifier()` (función)</span><span class="sxs-lookup"><span data-stu-id="bd9ce-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="bd9ce-300">A **degradado modelo de clasificación de árbol aumento** mediante el uso de hello MLlib `GradientBoostedTrees()` (función)</span><span class="sxs-lookup"><span data-stu-id="bd9ce-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="bd9ce-301">Creación de un modelo de regresión logística</span><span class="sxs-lookup"><span data-stu-id="bd9ce-301">Create a logistic regression model</span></span>
<span data-ttu-id="bd9ce-302">A continuación, crear un modelo de regresión logística mediante Hola Spark ML `LogisticRegression()` función.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="bd9ce-303">Crear modelo Hola compilar el código en una serie de pasos:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="bd9ce-304">**Entrenar el modelo de hello** datos con un conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="bd9ce-305">**Evaluar el modelo de hello** en un conjunto de datos de prueba con las métricas.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="bd9ce-306">**Guardar modelo hello** en almacenamiento de blobs para su futura utilización.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="bd9ce-307">**Modelo de puntuación hello** con datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="bd9ce-308">**Trazar resultados hello** receptor operativo curvas de característica (ROC).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="bd9ce-309">Este es el código de hello para estos procedimientos:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-309">Here's hello code for these procedures:</span></span>

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

<span data-ttu-id="bd9ce-310">Cargar, puntuación y guardar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-310">Load, score, and save hello results.</span></span>

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


<span data-ttu-id="bd9ce-311">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-311">**Output:**</span></span>

<span data-ttu-id="bd9ce-312">ROC de los datos de prueba = 0,9827381497557599</span><span class="sxs-lookup"><span data-stu-id="bd9ce-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="bd9ce-313">Uso de Python en curva de local Pandas datos marcos tooplot Hola ROC.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

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


<span data-ttu-id="bd9ce-314">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-314">**Output:**</span></span>

![Curva de ROC sobre si se dará propina o no](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="bd9ce-316">Creación de un modelo de clasificación de bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="bd9ce-316">Create a random forest classification model</span></span>
<span data-ttu-id="bd9ce-317">A continuación, crear un modelo de clasificación de bosque aleatorio mediante Hola Spark ML `RandomForestClassifier()` función y, a continuación, evaluar el modelo de hello en los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="bd9ce-318">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-318">**Output:**</span></span>

<span data-ttu-id="bd9ce-319">ROC de los datos de prueba = 0,9847103571552683</span><span class="sxs-lookup"><span data-stu-id="bd9ce-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="bd9ce-320">Creación de un modelo de clasificación GBT</span><span class="sxs-lookup"><span data-stu-id="bd9ce-320">Create a GBT classification model</span></span>
<span data-ttu-id="bd9ce-321">A continuación, cree un modelo de clasificación GBT mediante el uso del MLlib `GradientBoostedTrees()` función y, a continuación, evaluar el modelo de hello en los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="bd9ce-322">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-322">**Output:**</span></span>

<span data-ttu-id="bd9ce-323">Área bajo la curva de ROC = 0,9846895479241554</span><span class="sxs-lookup"><span data-stu-id="bd9ce-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="bd9ce-324">Modelo de regresión: predicción del importe de la propina</span><span class="sxs-lookup"><span data-stu-id="bd9ce-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="bd9ce-325">En esta sección, crea dos tipos de cantidad de regresión modelos toopredict Hola Sugerencia:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="bd9ce-326">A **modelo de regresión lineal regularizada** mediante el uso de hello Spark ML `LinearRegression()` función.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="bd9ce-327">Podrá guardar modelo hello y evaluar el modelo de hello en los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="bd9ce-328">A **modelo de regresión de árbol de impulso de gradiente** mediante el uso de hello Spark ML `GBTRegressor()` función.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="bd9ce-329">Creación de un modelo d regresión lineal regularizada</span><span class="sxs-lookup"><span data-stu-id="bd9ce-329">Create a regularized linear regression model</span></span>
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


<span data-ttu-id="bd9ce-330">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-330">**Output:**</span></span>

<span data-ttu-id="bd9ce-331">Celda de tiempo toorun Hola: 13 segundos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-331">Time toorun hello cell: 13 seconds.</span></span>

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


<span data-ttu-id="bd9ce-332">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-332">**Output:**</span></span>

<span data-ttu-id="bd9ce-333">R-sqr de los datos de prueba = 0,5960320470835743</span><span class="sxs-lookup"><span data-stu-id="bd9ce-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="bd9ce-334">A continuación, consulta Hola de resultados de pruebas como una trama de datos y use toovisualize AutoVizWidget y matplotlib se.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="bd9ce-335">código de Hello crea una trama de datos local de resultado de la consulta de Hola y representa los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="bd9ce-336">Hola `%%local` mágico crea una trama de datos local, `sqlResults`, que puede usar tooplot con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="bd9ce-337">Esta instrucción mágica de Spark se emplea varias veces en este artículo.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="bd9ce-338">Si la cantidad de Hola de datos es grande, debe muestrear toocreate una trama de datos que cabe en la memoria local.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="bd9ce-339">Creación de trazados con matplotlib de Python.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-339">Create plots by using Python matplotlib.</span></span>

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

<span data-ttu-id="bd9ce-340">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-340">**Output:**</span></span>

![Importe de la propina: real frente a predicción](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="bd9ce-342">Creación de un modelo de regresión GBT</span><span class="sxs-lookup"><span data-stu-id="bd9ce-342">Create a GBT regression model</span></span>
<span data-ttu-id="bd9ce-343">Crear un modelo de regresión GBT mediante Hola Spark ML `GBTRegressor()` función y, a continuación, evaluar el modelo de hello en los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="bd9ce-344">[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="bd9ce-345">Árboles de decisión de entrenamiento de GBTs forma iterativa toominimize una función de pérdida.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="bd9ce-346">Puede usar GBT para la clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="bd9ce-347">Permiten controlar características categóricas, no requieren ajustar la escala de las características y pueden capturar errores de alineación e interacciones de las características.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="bd9ce-348">También se pueden usar en una configuración de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-348">You also can use them in a multiclass-classification setting.</span></span>

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


<span data-ttu-id="bd9ce-349">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-349">**Output:**</span></span>

<span data-ttu-id="bd9ce-350">R-sqr de prueba = 0,7655383534596654</span><span class="sxs-lookup"><span data-stu-id="bd9ce-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="bd9ce-351">Utilidades avanzadas de modelado para la optimización</span><span class="sxs-lookup"><span data-stu-id="bd9ce-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="bd9ce-352">En esta sección, utilizará herramientas de aprendizaje automático que los desarrolladores usan con frecuencia para la optimización de modelos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="bd9ce-353">En concreto, pueden optimizarse los modelos de aprendizaje automático de tres maneras distintas mediante barrido de parámetros y validación cruzada:</span><span class="sxs-lookup"><span data-stu-id="bd9ce-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="bd9ce-354">Dividir los datos de hello en conjuntos de entrenamiento y validación, optimizar el modelo de hello mediante el uso de barrido de parámetros hyper en un conjunto de entrenamiento y evaluar en un conjunto de validación (regresión lineal)</span><span class="sxs-lookup"><span data-stu-id="bd9ce-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="bd9ce-355">Optimizar el modelo de hello mediante la validación cruzada y hyper-parámetro barrido mediante CrossValidator función del aprendizaje automático de Spark (clasificación binaria)</span><span class="sxs-lookup"><span data-stu-id="bd9ce-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="bd9ce-356">Optimizar el modelo Hola utilizando código personalizado de validación cruzada y barrido de parámetros toouse cualquier conjunto de parámetros y la función (regresión lineal) de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="bd9ce-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="bd9ce-357">**La validación cruzada** es una técnica que evalúa la medida un modelo entrenado en un conjunto conocido de datos generalizará toopredict Hola características de conjuntos de datos en el que no se está entrenada.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="bd9ce-358">Hello una idea general de esta técnica es que un modelo está entrenado en un conjunto de datos de los datos conocidos, y, a continuación, hello precisión de las predicciones se prueba en un conjunto de datos independiente.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="bd9ce-359">Una implementación común es toodivide un conjunto de datos en *k*-contrae y, a continuación, entrenar modelo de hello en un modo round-robin en todos excepto uno de los subconjuntos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="bd9ce-360">**Optimización de Hyper-parámetro** Hola problema de elegir un conjunto de hyper-parámetros para un algoritmo de aprendizaje, normalmente con el objetivo de Hola de optimizar una medida de rendimiento del algoritmo de hello en un conjunto de datos independiente.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="bd9ce-361">Un parámetro de hyper-es un valor que debe especificar fuera de procedimiento de entrenamiento del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="bd9ce-362">Suposiciones acerca de los valores de parámetro de hyper-pueden afectar a flexibilidad de Hola y la precisión del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="bd9ce-363">Árboles de decisión tienen hyper-parámetros, por ejemplo, como Hola había deseado profundidad y el número de hojas de árbol de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="bd9ce-364">Debe establecer un término de penalización para las clasificaciones incorrectas en las máquinas de vectores de soporte (SVM).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="bd9ce-365">Una optimización de parámetro hyper de tooperform forma común es toouse una búsqueda de la cuadrícula, también se denomina un **barrido de parámetros**.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="bd9ce-366">En una búsqueda de la cuadrícula, se realiza una búsqueda exhaustiva a través de los valores de hello de un subconjunto específico de espacio en hyper-parámetro hello para un algoritmo de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="bd9ce-367">La validación cruzada puede proporcionar un toosort de métrica de rendimiento out resultados óptimos Hola generado por el algoritmo de búsqueda de cuadrícula de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="bd9ce-368">Si usas barrido de hyper-parámetros de validación cruzada, puede ayudar a problemas de límite como sobreajuste una tootraining de datos de modelo.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="bd9ce-369">De esta manera, el modelo de hello conserva Hola capacidad tooapply toohello general conjunto de datos del que Hola se extrajeron los datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="bd9ce-370">Optimización del modelo de regresión lineal mediante barrido de hiperparámetros</span><span class="sxs-lookup"><span data-stu-id="bd9ce-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="bd9ce-371">A continuación, dividir datos en conjuntos de entrenamiento y validación, use hyper-parámetro barrido en un entrenamiento establezca toooptimize Hola modelo y evaluar en un conjunto de validación (regresión lineal).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

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


<span data-ttu-id="bd9ce-372">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-372">**Output:**</span></span>

<span data-ttu-id="bd9ce-373">R-sqr de prueba = 0,6226484708501209</span><span class="sxs-lookup"><span data-stu-id="bd9ce-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="bd9ce-374">Optimizar el modelo de clasificación binaria de hello mediante el uso de barrido de la validación cruzada y parámetro de hyper-</span><span class="sxs-lookup"><span data-stu-id="bd9ce-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="bd9ce-375">Esta sección muestra cómo modelar con validación cruzada y parámetro hyper barrido toooptimize una clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="bd9ce-376">Esto utiliza Hola Spark ML `CrossValidator` función.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-376">This uses hello Spark ML `CrossValidator` function.</span></span>

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


<span data-ttu-id="bd9ce-377">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-377">**Output:**</span></span>

<span data-ttu-id="bd9ce-378">Celda de tiempo toorun Hola: 33 segundos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="bd9ce-379">Optimizar el modelo de regresión lineal de hello mediante código personalizado de validación cruzada y barrido de parámetros</span><span class="sxs-lookup"><span data-stu-id="bd9ce-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="bd9ce-380">A continuación, optimizar el modelo de hello mediante código personalizado e identificar los parámetros del modelo mejor hello mediante criterios de Hola de mayor precisión.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="bd9ce-381">A continuación, cree el modelo final hello, evaluar el modelo de hello en los datos de prueba y Guardar modelo hello en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="bd9ce-382">Por último, cargar el modelo de hello, puntuar datos de prueba y evaluar la precisión.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

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


<span data-ttu-id="bd9ce-383">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="bd9ce-383">**Output:**</span></span>

<span data-ttu-id="bd9ce-384">Celda de tiempo toorun Hola: 61 segundos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="bd9ce-385">Uso automático en Scala de los modelos de aprendizaje automático creados en Spark</span><span class="sxs-lookup"><span data-stu-id="bd9ce-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="bd9ce-386">Para obtener información general de temas que le guiarán por tareas de Hola que componen el proceso de ciencia de datos de hello en Azure, consulte [proceso de ciencia de datos de equipo](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="bd9ce-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="bd9ce-387">[Tutoriales de proceso de ciencia de datos del equipo](data-science-process-walkthroughs.md) describe otros tutoriales to-end que muestran pasos Hola Hola proceso de ciencia de datos de equipo para escenarios concretos.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="bd9ce-388">Hola tutoriales también muestran el funcionamiento de cloud toocombine y herramientas local y servicios en un flujo de trabajo o canalización toocreate una aplicación inteligente.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="bd9ce-389">[Puntuación de modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md) se muestra cómo toouse Scala código tooautomatically cargar y puntuación nuevos conjuntos de datos con modelos de aprendizaje automático creados en Spark y guardarlos en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="bd9ce-390">Puede seguir instrucciones Hola siempre que haya y simplemente reemplace Hola código Python con código de Scala en este artículo para un consumo automatizado.</span><span class="sxs-lookup"><span data-stu-id="bd9ce-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

