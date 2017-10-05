---
title: Ciencia de datos mediante Scala y Spark en Azure | Microsoft Docs
description: "Este artículo muestra cómo utilizar Scala para tareas de aprendizaje automático supervisado con los paquetes MLlib escalable y ML de Spark en un clúster de Spark de HDInsight de Azure."
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
ms.openlocfilehash: b2419f53bdc3236d7de76b89f2a0a76704e85391
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="280f8-103">Ciencia de datos mediante Scala y Spark en Azure</span><span class="sxs-lookup"><span data-stu-id="280f8-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="280f8-104">Este artículo muestra cómo utilizar Scala para tareas de aprendizaje automático supervisado con los paquetes MLlib escalable y ML de Spark en un clúster de Spark en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-104">This article shows you how to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="280f8-105">Además, se explican cuáles son las tareas que constituyen el [proceso de ciencia de datos](http://aka.ms/datascienceprocess): exploración e ingesta de datos, visualización, ingeniería de características, modelado y consumo de modelos.</span><span class="sxs-lookup"><span data-stu-id="280f8-105">It walks you through the tasks that constitute the [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="280f8-106">Los modelos en el artículo incluyen regresión logística y lineal, bosques aleatorios y árboles incrementados de degradado (GBTs), además de dos tareas habituales de aprendizaje automático supervisado:</span><span class="sxs-lookup"><span data-stu-id="280f8-106">The models in the article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition to two common supervised machine learning tasks:</span></span>

* <span data-ttu-id="280f8-107">Problema de regresión: predicción de propinas (en dólares) por una carrera de taxi</span><span class="sxs-lookup"><span data-stu-id="280f8-107">Regression problem: Prediction of the tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="280f8-108">Clasificación binaria: predicción de si se dará propina o no (1/0) en una carrera de taxi</span><span class="sxs-lookup"><span data-stu-id="280f8-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="280f8-109">Para llevar a cabo el proceso de modelado hay que realizar entrenamientos y evaluaciones en conjuntos de datos de pruebas y métricas de precisión pertinentes.</span><span class="sxs-lookup"><span data-stu-id="280f8-109">The modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="280f8-110">En este artículo se describe cómo almacenar estos modelos en el Almacenamiento de blobs de Azure, además de puntuar y evaluar su rendimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="280f8-110">In this article, you can learn how to store these models in Azure Blob storage and how to score and evaluate their predictive performance.</span></span> <span data-ttu-id="280f8-111">También se tratan temas más avanzados sobre cómo optimizar modelos mediante validación cruzada y barridos de hiperparámetros.</span><span class="sxs-lookup"><span data-stu-id="280f8-111">This article also covers the more advanced topics of how to optimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="280f8-112">Los datos que se utilizan son un ejemplo del conjunto de datos de carreras y tarifas de taxi de la ciudad de Nueva York en 2013 disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="280f8-112">The data used is a sample of the 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="280f8-113">[Scala](http://www.scala-lang.org/)es un lenguaje basado en la Máquina virtual Java que integra los conceptos del lenguaje funcional y la programación orientada a objetos.</span><span class="sxs-lookup"><span data-stu-id="280f8-113">[Scala](http://www.scala-lang.org/), a language based on the Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="280f8-114">Se trata de un lenguaje escalable apropiado para efectuar el procesamiento distribuido en la nube y que se ejecuta en los clústeres de Spark de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-114">It's a scalable language that is well suited to distributed processing in the cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="280f8-115">[Spark](http://spark.apache.org/) es una plataforma de procesamiento paralelo de código abierto que admite el procesamiento en memoria para mejorar el rendimiento de las aplicaciones de análisis de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="280f8-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing to boost the performance of big data analytics applications.</span></span> <span data-ttu-id="280f8-116">El motor de procesamiento Spark se ha creado para ofrecer velocidad, facilidad de uso y análisis sofisticados.</span><span class="sxs-lookup"><span data-stu-id="280f8-116">The Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="280f8-117">Las capacidades de cálculo distribuido en memoria de Spark lo convierten en una buena opción para algoritmos iterativos en los cálculos de gráficos y aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="280f8-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="280f8-118">El paquete [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) proporciona un conjunto uniforme de API de alto nivel creadas a partir de tramas de datos que ayudan a crear y ajustar canalizaciones prácticas de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="280f8-118">The [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="280f8-119">[MLlib](http://spark.apache.org/mllib/) es la biblioteca de aprendizaje automático escalable de Spark que ofrece funcionalidades de modelado en este entorno distribuido.</span><span class="sxs-lookup"><span data-stu-id="280f8-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities to this distributed environment.</span></span>

<span data-ttu-id="280f8-120">[Spark en HDInsight](../hdinsight/hdinsight-apache-spark-overview.md) es la oferta de Spark de código abierto hospedada por Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is the Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="280f8-121">Asimismo, incluye compatibilidad con cuadernos de Scala de Jupyter Notebook en el clúster de Spark, y permite ejecutar consultas interactivas de Spark SQL para transformar, filtrar y visualizar los datos almacenados en Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-121">It also includes support for Jupyter Scala notebooks on the Spark cluster, and can run Spark SQL interactive queries to transform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="280f8-122">Los fragmentos de código de Scala en este artículo proporcionan las soluciones y muestran los trazados pertinentes para visualizar los datos que se ejecutan en cuadernos de Jupyter Notebook instalados en los clústeres de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-122">The Scala code snippets in this article that provide the solutions and show the relevant plots to visualize the data run in Jupyter notebooks installed on the Spark clusters.</span></span> <span data-ttu-id="280f8-123">En estos temas, los pasos de modelado también contienen código que muestra cómo entrenar, evaluar, guardar y usar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="280f8-123">The modeling steps in these topics have code that shows you how to train, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="280f8-124">Los pasos de instalación y el código de este artículo están diseñados para Spark 1.6 con HDInsight de Azure 3.4.</span><span class="sxs-lookup"><span data-stu-id="280f8-124">The setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="280f8-125">Sin embargo, este código y el de [Jupyter Notebook de Scala](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) son genéricos y deberían funcionar en cualquier clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-125">However, the code in this article and in the [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="280f8-126">Los pasos de configuración y administración del clúster pueden ser ligeramente diferentes de los que se muestran aquí si no está usando Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="280f8-126">The cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="280f8-127">Si quiere leer un tema que muestre cómo utilizar Python en lugar de Scala para completar las tareas de un proceso de ciencia de datos de un extremo a otro, consulte [Información general sobre la ciencia de los datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="280f8-127">For a topic that shows you how to use Python rather than Scala to complete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="280f8-128">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="280f8-128">Prerequisites</span></span>
* <span data-ttu-id="280f8-129">Debe tener una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-129">You must have an Azure subscription.</span></span> <span data-ttu-id="280f8-130">Si aún no tiene una, [consiga una evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="280f8-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="280f8-131">Necesita un clúster de Spark 1.6 con HDInsight de Azure 3.4 para completar los procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="280f8-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster to complete the following procedures.</span></span> <span data-ttu-id="280f8-132">Para crear un clúster, consulte las instrucciones proporcionadas en [Introducción: creación de clústeres Apache Spark en HDInsight para Linux y ejecución de consultas interactivas mediante Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="280f8-132">To create a cluster, see the instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="280f8-133">Establezca el tipo de clúster y la versión en el menú **Seleccionar tipo de clúster** .</span><span class="sxs-lookup"><span data-stu-id="280f8-133">Set the cluster type and version on the **Select Cluster Type** menu.</span></span>

![Configuración de tipo de clúster de HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="280f8-135">Para ver una descripción de los datos de taxis de Nueva York y las instrucciones para ejecutar código desde un cuaderno de Jupyter Notebook en el clúster de Spark, consulte las secciones apropiadas de [Información general sobre la ciencia de los datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="280f8-135">For a description of the NYC taxi trip data and instructions on how to execute code from a Jupyter notebook on the Spark cluster, see the relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-the-spark-cluster"></a><span data-ttu-id="280f8-136">Ejecución del código de Scala desde un cuaderno de Jupyter Notebook del clúster Spark</span><span class="sxs-lookup"><span data-stu-id="280f8-136">Execute Scala code from a Jupyter notebook on the Spark cluster</span></span>
<span data-ttu-id="280f8-137">Puede iniciar un cuaderno de Jupyter Notebook desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-137">You can launch a Jupyter notebook from the Azure portal.</span></span> <span data-ttu-id="280f8-138">Busque el clúster de Spark en el panel y haga clic en él para entrar en la página de administración del clúster.</span><span class="sxs-lookup"><span data-stu-id="280f8-138">Find the Spark cluster on your dashboard, and then click it to enter the management page for your cluster.</span></span> <span data-ttu-id="280f8-139">Después, haga clic en **Paneles de clúster** y, después, en **Jupyter Notebook** para abrir el cuaderno asociado al clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** to open the notebook associated with the Spark cluster.</span></span>

![Panel del clúster y cuadernos de Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="280f8-141">También puede ir a https://&lt;nombreDeClúster&gt;.azurehdinsight.net/jupyter para acceder a los cuadernos de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="280f8-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="280f8-142">Reemplace *clustername* por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="280f8-142">Replace *clustername* with the name of your cluster.</span></span> <span data-ttu-id="280f8-143">Necesitará la contraseña de su cuenta de administrador para acceder a los cuadernos de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="280f8-143">You need the password for your administrator account to access the Jupyter notebooks.</span></span>

![Vaya a Jupyter Notebook mediante el nombre de clúster](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="280f8-145">Seleccione **Scala** para ver un directorio con algunos ejemplos de cuadernos preempaquetados que utilizan la API PySpark.</span><span class="sxs-lookup"><span data-stu-id="280f8-145">Select **Scala** to see a directory that has a few examples of prepackaged notebooks that use the PySpark API.</span></span> <span data-ttu-id="280f8-146">La exploración de modelado y puntuación mediante el cuaderno de Scala.ipynb con muestras de código de este conjunto de temas Spark está disponible en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="280f8-146">The Exploration Modeling and Scoring using Scala.ipynb notebook that contains the code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="280f8-147">Puede cargar el cuaderno directamente desde GitHub en el servidor de Jupyter Notebook del clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-147">You can upload the notebook directly from GitHub to the Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="280f8-148">En la página principal de Jupyter, haga clic en el botón **Upload** (Cargar).</span><span class="sxs-lookup"><span data-stu-id="280f8-148">On your Jupyter home page, click the **Upload** button.</span></span> <span data-ttu-id="280f8-149">En el Explorador de archivos, pegue la URL de GitHub (contenido sin procesar) del cuaderno Scala y haga clic en **Open**(Abrir).</span><span class="sxs-lookup"><span data-stu-id="280f8-149">In the file explorer, paste the GitHub (raw content) URL of the Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="280f8-150">El cuaderno de Scala está disponible en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="280f8-150">The Scala notebook is available at the following URL:</span></span>

[<span data-ttu-id="280f8-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="280f8-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="280f8-152">Instalación: contextos preestablecidos de Spark y Hive, instrucciones mágicas de Spark y bibliotecas de Spark</span><span class="sxs-lookup"><span data-stu-id="280f8-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="280f8-153">Contextos preestablecidos de Spark y Hive</span><span class="sxs-lookup"><span data-stu-id="280f8-153">Preset Spark and Hive contexts</span></span>
    # SET THE START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="280f8-154">Los kernels de Spark que se proporcionan con cuadernos de Jupyter Notebook tienen contextos preestablecidos.</span><span class="sxs-lookup"><span data-stu-id="280f8-154">The Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="280f8-155">No es necesario establecer explícitamente los contextos de Spark o Hive antes de empezar a trabajar con la aplicación que se esté desarrollando.</span><span class="sxs-lookup"><span data-stu-id="280f8-155">You don't need to explicitly set the Spark or Hive contexts before you start working with the application you are developing.</span></span> <span data-ttu-id="280f8-156">Los contextos preestablecidos son:</span><span class="sxs-lookup"><span data-stu-id="280f8-156">The preset contexts are:</span></span>

* <span data-ttu-id="280f8-157">`sc` para SparkContext</span><span class="sxs-lookup"><span data-stu-id="280f8-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="280f8-158">`sqlContext` para HiveContext</span><span class="sxs-lookup"><span data-stu-id="280f8-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="280f8-159">Instrucciones mágicas de Spark</span><span class="sxs-lookup"><span data-stu-id="280f8-159">Spark magics</span></span>
<span data-ttu-id="280f8-160">El kernel de Spark proporciona algunas instrucciones "mágicas" predefinidas, que son comandos especiales a los que pueden llamarse con `%%`.</span><span class="sxs-lookup"><span data-stu-id="280f8-160">The Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="280f8-161">Dos de estos comandos se utilizan en los siguientes ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="280f8-161">Two of these commands are used in the following code samples.</span></span>

* <span data-ttu-id="280f8-162">`%%local` especifica que el código de las líneas siguientes se ejecutará localmente.</span><span class="sxs-lookup"><span data-stu-id="280f8-162">`%%local` specifies that the code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="280f8-163">El código debe estar en el lenguaje Scala.</span><span class="sxs-lookup"><span data-stu-id="280f8-163">The code must be valid Scala code.</span></span>
* <span data-ttu-id="280f8-164">`%%sql -o <variable name>` ejecuta una consulta de Hive en `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="280f8-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="280f8-165">Si se pasa el parámetro `-o`, el resultado de la consulta se conserva en el contexto de Scala `%%local` como trama de datos de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-165">If the `-o` parameter is passed, the result of the query is persisted in the `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="280f8-166">Para más información sobre los kernels de cuadernos de Jupyter Notebook y las "instrucciones mágicas" predefinidas que llama con `%%` (por ejemplo, `%%local`), vea [Kernels disponibles para cuadernos de Jupyter con clústeres de Apache Spark en HDInsight Linux](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="280f8-166">For more information about the kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="280f8-167">Importación de bibliotecas</span><span class="sxs-lookup"><span data-stu-id="280f8-167">Import libraries</span></span>
<span data-ttu-id="280f8-168">Importe las bibliotecas de Spark, MLlib y otras que necesite con el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="280f8-168">Import the Spark, MLlib, and other libraries you'll need by using the following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="280f8-169">Ingesta de datos</span><span class="sxs-lookup"><span data-stu-id="280f8-169">Data ingestion</span></span>
<span data-ttu-id="280f8-170">El primer paso en el proceso de ciencia de datos es introducir los datos que desea analizar.</span><span class="sxs-lookup"><span data-stu-id="280f8-170">The first step in the Data Science process is to ingest the data that you want to analyze.</span></span> <span data-ttu-id="280f8-171">Se traen los datos de orígenes o sistemas externos en los que residan a su entorno de exploración y modelado de datos.</span><span class="sxs-lookup"><span data-stu-id="280f8-171">You bring the data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="280f8-172">En este artículo, los datos introducidos representan conjuntamente un 0,1 % del archivo de carreras y tarifas de taxi (almacenado como un archivo .tsv).</span><span class="sxs-lookup"><span data-stu-id="280f8-172">In this article, the data you ingest is a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="280f8-173">El entorno de exploración y modelado de datos es Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-173">The data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="280f8-174">Esta sección contiene el código para completar una serie de tareas:</span><span class="sxs-lookup"><span data-stu-id="280f8-174">This section contains the code to complete the following series of tasks:</span></span>

1. <span data-ttu-id="280f8-175">Establecer rutas de acceso a directorios para almacenar datos y modelos.</span><span class="sxs-lookup"><span data-stu-id="280f8-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="280f8-176">Leer el conjunto de datos de entrada (almacenado como un archivo .tsv).</span><span class="sxs-lookup"><span data-stu-id="280f8-176">Read in the input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="280f8-177">Definir un esquema para los datos y limpiarlos.</span><span class="sxs-lookup"><span data-stu-id="280f8-177">Define a schema for the data and clean the data.</span></span>
4. <span data-ttu-id="280f8-178">Crear una trama de datos limpia y almacenarla en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="280f8-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="280f8-179">Registrar los datos como una tabla temporal en SQLContext.</span><span class="sxs-lookup"><span data-stu-id="280f8-179">Register the data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="280f8-180">Consultar la tabla e importar los resultados en una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="280f8-180">Query the table and import the results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="280f8-181">Establecer rutas de acceso de directorio para las ubicaciones de almacenamiento en el Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="280f8-182">Spark puede leer y escribir en el Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-182">Spark can read and write to Azure Blob storage.</span></span> <span data-ttu-id="280f8-183">Puede usar Spark para procesar cualquiera de los datos existentes y almacenar los resultados en el Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="280f8-183">You can use Spark to process any of your existing data, and then store the results again in Blob storage.</span></span>

<span data-ttu-id="280f8-184">Para guardar modelos o archivos en el Almacenamiento de blobs, debe especificar la ruta de acceso de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="280f8-184">To save models or files in Blob storage, you need to properly specify the path.</span></span> <span data-ttu-id="280f8-185">Se puede hacer referencia al contenedor predeterminado asociado al clúster de Spark con un ruta que comience con `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="280f8-185">Reference the default container attached to the Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="280f8-186">Haga referencia a otras ubicaciones mediante `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="280f8-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="280f8-187">El siguiente ejemplo de código especifica la ubicación de los datos de entrada que se leerán y la ruta de acceso al Almacenamiento de blobs conectado al clúster de Spark donde se guardará el modelo.</span><span class="sxs-lookup"><span data-stu-id="280f8-187">The following code sample specifies the location of the input data to be read and the path to Blob storage that is attached to the Spark cluster where the model will be saved.</span></span>

    # SET PATHS TO DATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET THE MODEL STORAGE DIRECTORY PATH
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-to-the-schema"></a><span data-ttu-id="280f8-188">Importación de datos, creación de un conjunto de datos distribuidos resistentes (RDD) y definición de tramas de datos según el esquema</span><span class="sxs-lookup"><span data-stu-id="280f8-188">Import data, create an RDD, and define a data frame according to the schema</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE SCHEMA BASED ON THE HEADER OF THE FILE
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

    # CAST VARIABLES ACCORDING TO THE SCHEMA
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

    # CACHE AND MATERIALIZE THE CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER THE DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="280f8-189">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-189">**Output:**</span></span>

<span data-ttu-id="280f8-190">Tiempo de ejecución de la celda: 8 segundos.</span><span class="sxs-lookup"><span data-stu-id="280f8-190">Time to run the cell: 8 seconds.</span></span>

### <a name="query-the-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="280f8-191">Consulta de la tabla e importación de resultados en una trama de datos</span><span class="sxs-lookup"><span data-stu-id="280f8-191">Query the table and import results in a data frame</span></span>
<span data-ttu-id="280f8-192">Ahora, consulte la tabla para obtener datos de tarifas, pasajeros y propinas, filtrar la información dañada y no relevante, e imprimir varias filas.</span><span class="sxs-lookup"><span data-stu-id="280f8-192">Next, query the table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY THE DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY THE TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="280f8-193">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-193">**Output:**</span></span>

| <span data-ttu-id="280f8-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="280f8-194">fare_amount</span></span> | <span data-ttu-id="280f8-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="280f8-195">passenger_count</span></span> | <span data-ttu-id="280f8-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="280f8-196">tip_amount</span></span> | <span data-ttu-id="280f8-197">tipped</span><span class="sxs-lookup"><span data-stu-id="280f8-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="280f8-198">13.5</span><span class="sxs-lookup"><span data-stu-id="280f8-198">13.5</span></span> |<span data-ttu-id="280f8-199">1.0</span><span class="sxs-lookup"><span data-stu-id="280f8-199">1.0</span></span> |<span data-ttu-id="280f8-200">2.9</span><span class="sxs-lookup"><span data-stu-id="280f8-200">2.9</span></span> |<span data-ttu-id="280f8-201">1.0</span><span class="sxs-lookup"><span data-stu-id="280f8-201">1.0</span></span> |
|        <span data-ttu-id="280f8-202">16.0</span><span class="sxs-lookup"><span data-stu-id="280f8-202">16.0</span></span> |<span data-ttu-id="280f8-203">2.0</span><span class="sxs-lookup"><span data-stu-id="280f8-203">2.0</span></span> |<span data-ttu-id="280f8-204">3.4</span><span class="sxs-lookup"><span data-stu-id="280f8-204">3.4</span></span> |<span data-ttu-id="280f8-205">1.0</span><span class="sxs-lookup"><span data-stu-id="280f8-205">1.0</span></span> |
|        <span data-ttu-id="280f8-206">10.5</span><span class="sxs-lookup"><span data-stu-id="280f8-206">10.5</span></span> |<span data-ttu-id="280f8-207">2.0</span><span class="sxs-lookup"><span data-stu-id="280f8-207">2.0</span></span> |<span data-ttu-id="280f8-208">1.0</span><span class="sxs-lookup"><span data-stu-id="280f8-208">1.0</span></span> |<span data-ttu-id="280f8-209">1.0</span><span class="sxs-lookup"><span data-stu-id="280f8-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="280f8-210">Visualización y exploración de datos</span><span class="sxs-lookup"><span data-stu-id="280f8-210">Data exploration and visualization</span></span>
<span data-ttu-id="280f8-211">Una vez incorporados los datos en Spark, el siguiente paso del proceso de la ciencia de los datos es conocer mejor los datos mediante la exploración y la visualización.</span><span class="sxs-lookup"><span data-stu-id="280f8-211">After you bring the data into Spark, the next step in the Data Science process is to gain a deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="280f8-212">En esta sección se examinan los datos de taxi mediante consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="280f8-212">In this section, you examine the taxi data by using SQL queries.</span></span> <span data-ttu-id="280f8-213">Tras ello, se importan los resultados en una trama de datos para trazar las variables de destino y las posibles características para inspeccionarlas de manera visual mediante la funcionalidad de visualización automática de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="280f8-213">Then, import the results into a data frame to plot the target variables and prospective features for visual inspection by using the auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-to-plot-data"></a><span data-ttu-id="280f8-214">Uso de instrucciones mágicas de SQL y locales para trazar datos</span><span class="sxs-lookup"><span data-stu-id="280f8-214">Use local and SQL magic to plot data</span></span>
<span data-ttu-id="280f8-215">De forma predeterminada, el resultado de cualquier fragmento de código que se ejecuta desde un cuaderno de Jupyter Notebook está disponible en el contexto de la sesión que se conserva en los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="280f8-215">By default, the output of any code snippet that you run from a Jupyter notebook is available within the context of the session that is persisted on the worker nodes.</span></span> <span data-ttu-id="280f8-216">Si quiere guardar una carrera en los nodos de trabajo de cada cálculo y todos los datos que necesita para dichos cálculos están disponibles de forma local en el nodo del servidor de Jupyter (el nodo principal), puede utilizar la instrucción mágica `%%local` para ejecutar el fragmento de código en el servidor de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="280f8-216">If you want to save a trip to the worker nodes for every computation, and if all the data that you need for your computation is available locally on the Jupyter server node (which is the head node), you can use the `%%local` magic to run the code snippet on the Jupyter server.</span></span>

* <span data-ttu-id="280f8-217">**Instrucciones mágicas SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="280f8-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="280f8-218">El kernel de Spark en HDInsight admite consultas sencillas de HiveQL en línea en SQLContext.</span><span class="sxs-lookup"><span data-stu-id="280f8-218">The HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="280f8-219">El argumento (`-o VARIABLE_NAME`) conserva la salida de la consulta SQL como una trama de datos de Pandas en el servidor de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="280f8-219">The (`-o VARIABLE_NAME`) argument persists the output of the SQL query as a Pandas data frame on the Jupyter server.</span></span> <span data-ttu-id="280f8-220">Esto significa que estará disponible en el modo local.</span><span class="sxs-lookup"><span data-stu-id="280f8-220">This means it'll be available in the local mode.</span></span>
* <span data-ttu-id="280f8-221">**Instrucciones mágicas** `%%local`</span><span class="sxs-lookup"><span data-stu-id="280f8-221">`%%local` **magic**.</span></span> <span data-ttu-id="280f8-222">Las instrucciones mágicas `%%local` se utilizan para ejecutar código de forma local en el servidor de Jupyter, que es el nodo principal del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="280f8-222">The `%%local` magic runs the code locally on the Jupyter server, which is the head node of the HDInsight cluster.</span></span> <span data-ttu-id="280f8-223">Normalmente, se utilizan juntas las instrucciones mágicas `%%local` y `%%sql` con el parámetro `-o`.</span><span class="sxs-lookup"><span data-stu-id="280f8-223">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with the `-o` parameter.</span></span> <span data-ttu-id="280f8-224">El parámetro `-o` conservaría la salida de la consulta SQL localmente y luego la instrucción mágica `%%local` desencadenaría el siguiente conjunto de fragmento de código para ejecutarse localmente en la salida de las consultas SQL que se conserva localmente.</span><span class="sxs-lookup"><span data-stu-id="280f8-224">The `-o` parameter would persist the output of the SQL query locally, and then `%%local` magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally.</span></span>

### <a name="query-the-data-by-using-sql"></a><span data-ttu-id="280f8-225">Consulta de datos mediante SQL</span><span class="sxs-lookup"><span data-stu-id="280f8-225">Query the data by using SQL</span></span>
<span data-ttu-id="280f8-226">Esta consulta recupera carreras de taxi por importe de la tarifa, número de pasajeros y propina.</span><span class="sxs-lookup"><span data-stu-id="280f8-226">This query retrieves the taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN THE SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="280f8-227">En el código siguiente, la instrucción mágica `%%local` crea una trama de datos local, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="280f8-227">In the following code, the `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="280f8-228">Puede utilizar sqlResults para el trazado mediante matplotlib.</span><span class="sxs-lookup"><span data-stu-id="280f8-228">You can use sqlResults to plot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="280f8-229">La instrucción mágica local se emplea varias veces en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="280f8-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="280f8-230">Si la cantidad de datos es elevada, realice un muestreo para crear una trama de datos que pueda caber en la memoria local.</span><span class="sxs-lookup"><span data-stu-id="280f8-230">If your data set is large, please sample to create a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-the-data"></a><span data-ttu-id="280f8-231">Trazado de datos</span><span class="sxs-lookup"><span data-stu-id="280f8-231">Plot the data</span></span>
<span data-ttu-id="280f8-232">Se pueden trazar datos con código Python cuando la trama de datos esté en el contexto local como trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="280f8-232">You can plot by using Python code after the data frame is in local context as a Pandas data frame.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES.
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="280f8-233">Tras ejecutar el código, el kernel de Spark visualiza automáticamente el resultado de las consultas SQL (HiveQL).</span><span class="sxs-lookup"><span data-stu-id="280f8-233">The Spark kernel automatically visualizes the output of SQL (HiveQL) queries after you run the code.</span></span> <span data-ttu-id="280f8-234">Puede elegir entre varios tipos de visualizaciones:</span><span class="sxs-lookup"><span data-stu-id="280f8-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="280f8-235">Tabla</span><span class="sxs-lookup"><span data-stu-id="280f8-235">Table</span></span>
* <span data-ttu-id="280f8-236">Circular</span><span class="sxs-lookup"><span data-stu-id="280f8-236">Pie</span></span>
* <span data-ttu-id="280f8-237">Línea</span><span class="sxs-lookup"><span data-stu-id="280f8-237">Line</span></span>
* <span data-ttu-id="280f8-238">Ámbito</span><span class="sxs-lookup"><span data-stu-id="280f8-238">Area</span></span>
* <span data-ttu-id="280f8-239">Barra</span><span class="sxs-lookup"><span data-stu-id="280f8-239">Bar</span></span>

<span data-ttu-id="280f8-240">Este es el código para trazar los datos:</span><span class="sxs-lookup"><span data-stu-id="280f8-240">Here's the code to plot the data:</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="280f8-241">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-241">**Output:**</span></span>

![Histograma del importe de la propina](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Importe de las propinas por número de pasajeros](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Importe de las propinas por importe de la tarifa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="280f8-245">Creación y transformación de características, y preparación de datos para su entrada en funciones de modelado</span><span class="sxs-lookup"><span data-stu-id="280f8-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="280f8-246">Para utilizar las funciones de modelado de árbol en SparkML y MLlib, el destino y las características se deben preparar mediante diferentes técnicas, como discretización, indexación, codificación "one-hot" y vectorización.</span><span class="sxs-lookup"><span data-stu-id="280f8-246">For tree-based modeling functions from Spark ML and MLlib, you have to prepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="280f8-247">Estos son los procedimientos que seguir en esta sección:</span><span class="sxs-lookup"><span data-stu-id="280f8-247">Here are the procedures to follow in this section:</span></span>

1. <span data-ttu-id="280f8-248">Creación de una nueva característica mediante la **discretización** de horas en ciclos de tráfico.</span><span class="sxs-lookup"><span data-stu-id="280f8-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="280f8-249">Aplicación de **indexación y codificación "one-hot"** a características categóricas.</span><span class="sxs-lookup"><span data-stu-id="280f8-249">Apply **indexing and one-hot encoding** to categorical features.</span></span>
3. <span data-ttu-id="280f8-250">**Muestreo y división de conjuntos de datos** en fracciones de entrenamiento y prueba.</span><span class="sxs-lookup"><span data-stu-id="280f8-250">**Sample and split the data set** into training and test fractions.</span></span>
4. <span data-ttu-id="280f8-251">**Especificación de variables de entrenamiento y características**, y creación de tramas de datos o datos distribuidos resistentes (RDD) de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="280f8-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="280f8-252">**Categorización y vectorización automáticas de características y destinos** con el objetivo de utilizarlas como entradas para los modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="280f8-252">Automatically **categorize and vectorize features and targets** to use as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="280f8-253">Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico</span><span class="sxs-lookup"><span data-stu-id="280f8-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="280f8-254">Este código muestra cómo crear una nueva característica mediante la discretización de horas en ciclos de tráfico y cómo almacenar en caché la trama de datos resultante en memoria.</span><span class="sxs-lookup"><span data-stu-id="280f8-254">This code shows you how to create a new feature by binning hours into traffic time buckets and how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="280f8-255">Cuando se usan repetidamente conjuntos de datos distribuidos resistentes (RDD) y tramas de datos, el almacenamiento en caché mejora los tiempos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="280f8-255">Where RDDs and data frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="280f8-256">Por lo tanto, almacenaremos en caché los RDD y las tramas de datos en varias fases en los procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="280f8-256">Accordingly, you'll cache RDDs and data frames at several stages in the following procedures.</span></span>

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

    # CACHE THE DATA FRAME IN MEMORY AND MATERIALIZE THE DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="280f8-257">Indexación y codificación "one-hot" de características categóricas</span><span class="sxs-lookup"><span data-stu-id="280f8-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="280f8-258">Las funciones de modelado y predicción de MLlib requieren características con datos de entrada categóricos indexados o codificados antes de usarlos.</span><span class="sxs-lookup"><span data-stu-id="280f8-258">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="280f8-259">Esta sección muestra cómo indexar o codificar las características categóricas para su entrada en las funciones de modelado.</span><span class="sxs-lookup"><span data-stu-id="280f8-259">This section shows you how to index or encode categorical features for input into the modeling functions.</span></span>

<span data-ttu-id="280f8-260">Dependiendo del modelo, deberá indexarlo o codificarlo de maneras diferentes.</span><span class="sxs-lookup"><span data-stu-id="280f8-260">You need to index or encode your models in different ways, depending on the model.</span></span> <span data-ttu-id="280f8-261">Por ejemplo, los modelos de regresión logística y lineal requieren una codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="280f8-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="280f8-262">Asimismo, una función con tres categorías puede ampliarse en tres columnas de característica.</span><span class="sxs-lookup"><span data-stu-id="280f8-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="280f8-263">Cada columna contiene 0 o 1 según la categoría de una observación.</span><span class="sxs-lookup"><span data-stu-id="280f8-263">Each column would contain 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="280f8-264">MLlib proporciona la función [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) para realizar la codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="280f8-264">MLlib provides the [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="280f8-265">Este codificador asigna una columna de índices de etiqueta a una columna de vectores binarios, con un solo valor uno como máximo.</span><span class="sxs-lookup"><span data-stu-id="280f8-265">This encoder maps a column of label indices to a column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="280f8-266">Esta codificación permite aplicar algoritmos que esperan características con valores numéricos, como la regresión logística, a características categóricas.</span><span class="sxs-lookup"><span data-stu-id="280f8-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied to categorical features.</span></span>

<span data-ttu-id="280f8-267">Aquí solo transformamos cuatro variables para mostrar los ejemplos, que son cadenas de caracteres.</span><span class="sxs-lookup"><span data-stu-id="280f8-267">Here you transform only four variables to show examples, which are character strings.</span></span> <span data-ttu-id="280f8-268">También se pueden indexar otras variables como variables categóricas (por ejemplo, el día de la semana) que se representan mediante valores numéricos.</span><span class="sxs-lookup"><span data-stu-id="280f8-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="280f8-269">Para la indexación usamos `StringIndexer()`, y para la codificación "one-hot", funciones `OneHotEncoder()` de MLlib.</span><span class="sxs-lookup"><span data-stu-id="280f8-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="280f8-270">Este es el código para indexar y codificar características categóricas:</span><span class="sxs-lookup"><span data-stu-id="280f8-270">Here is the code to index and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD THE START TIME
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

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="280f8-271">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-271">**Output:**</span></span>

<span data-ttu-id="280f8-272">Tiempo de ejecución de la celda: 4 segundos.</span><span class="sxs-lookup"><span data-stu-id="280f8-272">Time to run the cell: 4 seconds.</span></span>

### <a name="sample-and-split-the-data-set-into-training-and-test-fractions"></a><span data-ttu-id="280f8-273">Muestreo y división de conjuntos de datos en fracciones de entrenamiento y prueba</span><span class="sxs-lookup"><span data-stu-id="280f8-273">Sample and split the data set into training and test fractions</span></span>
<span data-ttu-id="280f8-274">Este código crea una muestra aleatoria de los datos (en este ejemplo, el 25 %).</span><span class="sxs-lookup"><span data-stu-id="280f8-274">This code creates a random sampling of the data (25%, in this example).</span></span> <span data-ttu-id="280f8-275">Aunque no es necesario para este ejemplo debido al tamaño del conjunto de datos, el artículo describe cómo realizar la muestra para que sepa cómo hacerlo cuando lo necesite.</span><span class="sxs-lookup"><span data-stu-id="280f8-275">Although sampling is not required for this example due to the size of the data set, the article shows you how you can sample so that you know how to use it for your own problems when needed.</span></span> <span data-ttu-id="280f8-276">Cuando las muestras son grandes, esto puede ahorrar mucho tiempo al entrenar modelos.</span><span class="sxs-lookup"><span data-stu-id="280f8-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="280f8-277">Después, se divide la muestra en una parte de entrenamiento (en este ejemplo, el 75 %) y una parte de pruebas (25 %) para el modelado de clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="280f8-277">Next, split the sample into a training part (75%, in this example) and a testing part (25%, in this example) to use in classification and regression modeling.</span></span>

<span data-ttu-id="280f8-278">Se agrega un número aleatorio (entre 0 y 1) a cada fila (en una columna llamada "rand") que puede utilizarse para seleccionar subconjuntos de validación cruzada durante el entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="280f8-278">Add a random number (between 0 and 1) to each row (in a "rand" column) that can be used to select cross-validation folds during training.</span></span>

    # RECORD THE START TIME
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

    # SPLIT THE SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="280f8-279">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-279">**Output:**</span></span>

<span data-ttu-id="280f8-280">Tiempo de ejecución de la celda: 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="280f8-280">Time to run the cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="280f8-281">Especificación de variables de entrenamiento y características, y creación de tramas de datos o RDD de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot"</span><span class="sxs-lookup"><span data-stu-id="280f8-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="280f8-282">Esta sección contiene código que muestra cómo indexar datos de texto categóricos como un tipo de datos de punto con etiqueta, y codificarlos para poder usarlos para entrenar y probar la regresión logística de MLlib y otros modelos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="280f8-282">This section contains code that shows you how to index categorical text data as a labeled point data type, and encode it so you can use it to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="280f8-283">Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) con el formato de datos de entrada necesario para la mayoría de los algoritmos de aprendizaje automático de MLlib.</span><span class="sxs-lookup"><span data-stu-id="280f8-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="280f8-284">Un [punto con etiqueta](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) es un vector local, denso o disperso, asociado con una etiqueta o respuesta.</span><span class="sxs-lookup"><span data-stu-id="280f8-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="280f8-285">En este código, puede especificar la variable de destino (dependiente) y las características que se va a usar para entrenar modelos.</span><span class="sxs-lookup"><span data-stu-id="280f8-285">In this code, you specify the target (dependent) variable and the features to use to train models.</span></span> <span data-ttu-id="280f8-286">Después, cree tramas de datos o RDD de punto con etiqueta de entrada para entrenamientos y pruebas mediante indexación o codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="280f8-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY THE TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="280f8-287">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-287">**Output:**</span></span>

<span data-ttu-id="280f8-288">Tiempo de ejecución de la celda: 4 segundos.</span><span class="sxs-lookup"><span data-stu-id="280f8-288">Time to run the cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-to-use-as-inputs-for-machine-learning-models"></a><span data-ttu-id="280f8-289">Categorización y vectorización automáticas de características y destinos con el objetivo de utilizarlas como entradas para los modelos de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="280f8-289">Automatically categorize and vectorize features and targets to use as inputs for machine learning models</span></span>
<span data-ttu-id="280f8-290">Utilice SparkML para categorizar correctamente las características y el destino para las funciones de modelado de árbol.</span><span class="sxs-lookup"><span data-stu-id="280f8-290">Use Spark ML to categorize the target and features to use in tree-based modeling functions.</span></span> <span data-ttu-id="280f8-291">El código realiza dos tareas:</span><span class="sxs-lookup"><span data-stu-id="280f8-291">The code completes two tasks:</span></span>

* <span data-ttu-id="280f8-292">Crea un destino binario para la clasificación mediante la asignación de un valor de 0 o 1 a cada punto de datos entre 0 y 1 con un valor de umbral de 0,5.</span><span class="sxs-lookup"><span data-stu-id="280f8-292">Creates a binary target for classification by assigning a value of 0 or 1 to each data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="280f8-293">Categoriza automáticamente las características.</span><span class="sxs-lookup"><span data-stu-id="280f8-293">Automatically categorizes features.</span></span> <span data-ttu-id="280f8-294">Si el número de valores numéricos distintos de cualquiera de las características es inferior a 32, se categoriza la característica.</span><span class="sxs-lookup"><span data-stu-id="280f8-294">If the number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="280f8-295">Este es el código para estas dos tareas.</span><span class="sxs-lookup"><span data-stu-id="280f8-295">Here's the code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE THE TARGET FOR THE BINARY CLASSIFICATION PROBLEM

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

    # CATEGORIZE FEATURES FOR THE REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="280f8-296">Clasificación binaria: predicción de si se debe dar propina</span><span class="sxs-lookup"><span data-stu-id="280f8-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="280f8-297">En esta sección, crearemos tres tipos de modelos de clasificación binaria para predecir si se debe pagar propina:</span><span class="sxs-lookup"><span data-stu-id="280f8-297">In this section, you create three types of binary classification models to predict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="280f8-298">Un **modelo de regresión logística** con la función `LogisticRegression()` del aprendizaje automático de Spark</span><span class="sxs-lookup"><span data-stu-id="280f8-298">A **logistic regression model** by using the Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="280f8-299">Un **modelo de clasificación de bosque aleatorio** con la función `RandomForestClassifier()` del aprendizaje automático de Spark</span><span class="sxs-lookup"><span data-stu-id="280f8-299">A **random forest classification model** by using the Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="280f8-300">Un **modelo de clasificación de árboles impulsados por gradientes** con la función `GradientBoostedTrees()` de MLlib</span><span class="sxs-lookup"><span data-stu-id="280f8-300">A **gradient boosting tree classification model** by using the MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="280f8-301">Creación de un modelo de regresión logística</span><span class="sxs-lookup"><span data-stu-id="280f8-301">Create a logistic regression model</span></span>
<span data-ttu-id="280f8-302">Ahora, cree un modelo de regresión logística utilizando la función `LogisticRegression()` del aprendizaje automático de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-302">Next, create a logistic regression model by using the Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="280f8-303">El código de creación del modelo se genera en varios pasos:</span><span class="sxs-lookup"><span data-stu-id="280f8-303">You create the model building code in a series of steps:</span></span>

1. <span data-ttu-id="280f8-304">**Entrenamiento de datos del modelo** con un conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="280f8-304">**Train the model** data with one parameter set.</span></span>
2. <span data-ttu-id="280f8-305">**Evaluación del modelo** en un conjunto de datos de prueba con métricas.</span><span class="sxs-lookup"><span data-stu-id="280f8-305">**Evaluate the model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="280f8-306">**Guardado del modelo** en Almacenamiento de blobs para utilizarse en el futuro.</span><span class="sxs-lookup"><span data-stu-id="280f8-306">**Save the model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="280f8-307">**Puntuación del modelo** con los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="280f8-307">**Score the model** against test data.</span></span>
5. <span data-ttu-id="280f8-308">**Trazado de los resultados** con curvas de característica operativa del receptor (ROC).</span><span class="sxs-lookup"><span data-stu-id="280f8-308">**Plot the results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="280f8-309">Este es el código para estos procedimientos:</span><span class="sxs-lookup"><span data-stu-id="280f8-309">Here's the code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON THE TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE THE MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="280f8-310">Cargue, puntúe y guarde los resultados.</span><span class="sxs-lookup"><span data-stu-id="280f8-310">Load, score, and save the results.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD THE SAVED MODEL AND SCORE THE TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON THE TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="280f8-311">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-311">**Output:**</span></span>

<span data-ttu-id="280f8-312">ROC de los datos de prueba = 0,9827381497557599</span><span class="sxs-lookup"><span data-stu-id="280f8-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="280f8-313">Use Python en las tramas de datos locales de Pandas para trazar la curva de ROC.</span><span class="sxs-lookup"><span data-stu-id="280f8-313">Use Python on local Pandas data frames to plot the ROC curve.</span></span>

    # QUERY THE RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT THE ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT THE ROC CURVE
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


<span data-ttu-id="280f8-314">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-314">**Output:**</span></span>

![Curva de ROC sobre si se dará propina o no](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="280f8-316">Creación de un modelo de clasificación de bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="280f8-316">Create a random forest classification model</span></span>
<span data-ttu-id="280f8-317">Ahora, cree un modelo de clasificación de bosque aleatorio mediante la función `RandomForestClassifier()` del aprendizaje automático de Spark y evalúe el modelo con los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="280f8-317">Next, create a random forest classification model by using the Spark ML `RandomForestClassifier()` function, and then evaluate the model on test data.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE THE RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT THE MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE THE MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="280f8-318">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-318">**Output:**</span></span>

<span data-ttu-id="280f8-319">ROC de los datos de prueba = 0,9847103571552683</span><span class="sxs-lookup"><span data-stu-id="280f8-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="280f8-320">Creación de un modelo de clasificación GBT</span><span class="sxs-lookup"><span data-stu-id="280f8-320">Create a GBT classification model</span></span>
<span data-ttu-id="280f8-321">Ahora, cree un modelo de clasificación GBT mediante la función `GradientBoostedTrees()` de MLlib y evalúe el modelo con los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="280f8-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate the model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN THE MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE THE MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE THE MODEL ON TEST INSTANCES AND THE COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS TO EVALUATE THE MODEL ON THE TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="280f8-322">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-322">**Output:**</span></span>

<span data-ttu-id="280f8-323">Área bajo la curva de ROC = 0,9846895479241554</span><span class="sxs-lookup"><span data-stu-id="280f8-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="280f8-324">Modelo de regresión: predicción del importe de la propina</span><span class="sxs-lookup"><span data-stu-id="280f8-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="280f8-325">En esta sección, se crean dos tipos de modelos de regresión para predecir el importe de la propina:</span><span class="sxs-lookup"><span data-stu-id="280f8-325">In this section, you create two types of regression models to predict the tip amount:</span></span>

* <span data-ttu-id="280f8-326">Un **modelo de regresión lineal regularizada** con la función `LinearRegression()` del aprendizaje automático de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-326">A **regularized linear regression model** by using the Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="280f8-327">Debe guardar el modelo y evaluarlo con datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="280f8-327">You'll save the model and evaluate the model on test data.</span></span>
* <span data-ttu-id="280f8-328">Un **modelo de regresión de árboles impulsados por gradientes** con la función `GBTRegressor()` del aprendizaje automático de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-328">A **gradient-boosting tree regression model** by using the Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="280f8-329">Creación de un modelo d regresión lineal regularizada</span><span class="sxs-lookup"><span data-stu-id="280f8-329">Create a regularized linear regression model</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING THE SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT THE MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE THE MODEL OVER THE TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE THE MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT THE COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="280f8-330">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-330">**Output:**</span></span>

<span data-ttu-id="280f8-331">Tiempo de ejecución de la celda: 13 segundos.</span><span class="sxs-lookup"><span data-stu-id="280f8-331">Time to run the cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="280f8-332">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-332">**Output:**</span></span>

<span data-ttu-id="280f8-333">R-sqr de los datos de prueba = 0,5960320470835743</span><span class="sxs-lookup"><span data-stu-id="280f8-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="280f8-334">A continuación, consulta los resultados de pruebas como una trama de datos y usa AutoVizWidget y matplotlib para visualizarlos.</span><span class="sxs-lookup"><span data-stu-id="280f8-334">Next, query the test results as a data frame and use AutoVizWidget and matplotlib to visualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="280f8-335">Este código crea una trama de datos local a partir de los resultados de la consulta y traza los datos.</span><span class="sxs-lookup"><span data-stu-id="280f8-335">The code creates a local data frame from the query output and plots the data.</span></span> <span data-ttu-id="280f8-336">La instrucción mágica `%%local` crea una trama de datos local, `sqlResults`, que puede usarse para trazar la información con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="280f8-336">The `%%local` magic creates a local data frame, `sqlResults`, which you can use to plot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="280f8-337">Esta instrucción mágica de Spark se emplea varias veces en este artículo.</span><span class="sxs-lookup"><span data-stu-id="280f8-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="280f8-338">Si la cantidad de datos es grande, realice un muestreo para crear una trama de datos que pueda caber en la memoria local.</span><span class="sxs-lookup"><span data-stu-id="280f8-338">If the amount of data is large, you should sample to create a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="280f8-339">Creación de trazados con matplotlib de Python.</span><span class="sxs-lookup"><span data-stu-id="280f8-339">Create plots by using Python matplotlib.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT THE RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="280f8-340">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-340">**Output:**</span></span>

![Importe de la propina: real frente a predicción](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="280f8-342">Creación de un modelo de regresión GBT</span><span class="sxs-lookup"><span data-stu-id="280f8-342">Create a GBT regression model</span></span>
<span data-ttu-id="280f8-343">Cree un modelo de clasificación de bosque aleatorio mediante la función `GBTRegressor()` del aprendizaje automático de Spark y evalúe el modelo con los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="280f8-343">Create a GBT regression model by using the Spark ML `GBTRegressor()` function, and then evaluate the model on test data.</span></span>

<span data-ttu-id="280f8-344">[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="280f8-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="280f8-345">Los GBT entrenan árboles de decisión de forma iterativa para minimizar una función de pérdida.</span><span class="sxs-lookup"><span data-stu-id="280f8-345">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="280f8-346">Puede usar GBT para la clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="280f8-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="280f8-347">Permiten controlar características categóricas, no requieren ajustar la escala de las características y pueden capturar errores de alineación e interacciones de las características.</span><span class="sxs-lookup"><span data-stu-id="280f8-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="280f8-348">También se pueden usar en una configuración de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="280f8-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="280f8-349">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-349">**Output:**</span></span>

<span data-ttu-id="280f8-350">R-sqr de prueba = 0,7655383534596654</span><span class="sxs-lookup"><span data-stu-id="280f8-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="280f8-351">Utilidades avanzadas de modelado para la optimización</span><span class="sxs-lookup"><span data-stu-id="280f8-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="280f8-352">En esta sección, utilizará herramientas de aprendizaje automático que los desarrolladores usan con frecuencia para la optimización de modelos.</span><span class="sxs-lookup"><span data-stu-id="280f8-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="280f8-353">En concreto, pueden optimizarse los modelos de aprendizaje automático de tres maneras distintas mediante barrido de parámetros y validación cruzada:</span><span class="sxs-lookup"><span data-stu-id="280f8-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="280f8-354">Dividir los datos en conjuntos de entrenamiento y validación, y optimizar el modelo mediante barrido de hiperparámetros en un conjunto de entrenamiento y mediante evaluación en un conjunto de validación (regresión lineal)</span><span class="sxs-lookup"><span data-stu-id="280f8-354">Split the data into train and validation sets, optimize the model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="280f8-355">Optimizar el modelo mediante validación cruzada y barrido de hiperparámetros con la función CrossValidator de SparkML (clasificación binaria)</span><span class="sxs-lookup"><span data-stu-id="280f8-355">Optimize the model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="280f8-356">Optimizar modelo usando código personalizado de validación cruzada y barrido de parámetros para usar cualquier función de aprendizaje automático y conjunto de parámetros (regresión lineal)</span><span class="sxs-lookup"><span data-stu-id="280f8-356">Optimize the model by using custom cross-validation and parameter-sweeping code to use any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="280f8-357">**validación cruzada** es una técnica que evalúa la calidad de la generalización que realizará un modelo entrenado con un conjunto conocido de datos para predecir las características de conjuntos de datos con los que no se haya entrenado.</span><span class="sxs-lookup"><span data-stu-id="280f8-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize to predict the features of data sets on which it has not been trained.</span></span> <span data-ttu-id="280f8-358">La idea general tras esta técnica es que se entrena un modelo con un conjunto conocido de datos y después se prueba la precisión de sus predicciones con un conjunto de datos independiente.</span><span class="sxs-lookup"><span data-stu-id="280f8-358">The general idea behind this technique is that a model is trained on a data set of known data, and then the accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="280f8-359">En este caso, se usa una implementación habitual en la que se divide un conjunto de datos en *k*iteraciones y después se entrena el modelo como round-robin en todas las iteraciones menos una.</span><span class="sxs-lookup"><span data-stu-id="280f8-359">A common implementation is to divide a data set into *k*-folds, and then train the model in a round-robin fashion on all but one of the folds.</span></span>

<span data-ttu-id="280f8-360">**optimización de los hiperparámetros** es el problema de elegir un conjunto de hiperparámetros para un algoritmo de aprendizaje, normalmente con el fin de optimizar una medida del rendimiento del algoritmo con un conjunto de datos independiente.</span><span class="sxs-lookup"><span data-stu-id="280f8-360">**Hyper-parameter optimization** is the problem of choosing a set of hyper-parameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="280f8-361">Un hiperparámetro es un valor que debe especificar fuera del procedimiento de entrenamiento del modelo.</span><span class="sxs-lookup"><span data-stu-id="280f8-361">A hyper-parameter is a value that you must specify outside the model training procedure.</span></span> <span data-ttu-id="280f8-362">Las suposiciones que se hagan sobre estos hiperparámetros pueden afectar a la flexibilidad y la precisión de los modelos.</span><span class="sxs-lookup"><span data-stu-id="280f8-362">Assumptions about hyper-parameter values can affect the flexibility and accuracy of the model.</span></span> <span data-ttu-id="280f8-363">Los árboles de decisión tienen hiperparámetros, como la profundidad que desee y el número de hojas del árbol.</span><span class="sxs-lookup"><span data-stu-id="280f8-363">Decision trees have hyper-parameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="280f8-364">Debe establecer un término de penalización para las clasificaciones incorrectas en las máquinas de vectores de soporte (SVM).</span><span class="sxs-lookup"><span data-stu-id="280f8-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="280f8-365">Una forma habitual de realizar la optimización de hiperparámetros es una búsqueda de cuadrícula, también denominada **barrido de parámetros**.</span><span class="sxs-lookup"><span data-stu-id="280f8-365">A common way to perform hyper-parameter optimization is to use a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="280f8-366">En una búsqueda de cuadrícula, se lleva a cabo una búsqueda exhaustiva en los valores de un subconjunto concreto del espacio de hiperparámetros para un algoritmo de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="280f8-366">In a grid search, an exhaustive search is performed through the values of a specified subset of the hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="280f8-367">La validación cruzada puede proporcionar una métrica de rendimiento para ordenar los resultados óptimos generados por el algoritmo de búsqueda de cuadrícula.</span><span class="sxs-lookup"><span data-stu-id="280f8-367">Cross-validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="280f8-368">Si utiliza el barrido de hiperparámetros de validación cruzada, puede limitar problemas, como el sobreajuste de un modelo de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="280f8-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model to training data.</span></span> <span data-ttu-id="280f8-369">De este modo, el modelo sigue aplicándose a un conjunto general de datos del que se extrajeron los datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="280f8-369">This way, the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="280f8-370">Optimización del modelo de regresión lineal mediante barrido de hiperparámetros</span><span class="sxs-lookup"><span data-stu-id="280f8-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="280f8-371">Ahora, divida los datos en conjuntos de entrenamiento y validación, optimice el modelo mediante barrido de hiperparámetros en un conjunto de entrenamiento y evalúe en un conjunto de validación (regresión lineal).</span><span class="sxs-lookup"><span data-stu-id="280f8-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set to optimize the model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE THE ESTIMATOR FUNCTION: `THE LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE THE PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET), AND THEN THE SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="280f8-372">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-372">**Output:**</span></span>

<span data-ttu-id="280f8-373">R-sqr de prueba = 0,6226484708501209</span><span class="sxs-lookup"><span data-stu-id="280f8-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-the-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="280f8-374">Optimización del modelo de clasificación binaria mediante barrido de hiperparámetros y validación cruzada</span><span class="sxs-lookup"><span data-stu-id="280f8-374">Optimize the binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="280f8-375">En esta sección se muestra cómo optimizar el modelo de clasificación binaria mediante barrido de hiperparámetros y validación cruzada.</span><span class="sxs-lookup"><span data-stu-id="280f8-375">This section shows you how to optimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="280f8-376">Esto utiliza la función `CrossValidator` del aprendizaje automático de Spark.</span><span class="sxs-lookup"><span data-stu-id="280f8-376">This uses the Spark ML `CrossValidator` function.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS TO USE WITH THE TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE THE ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY THE NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE THE TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE THE TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="280f8-377">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-377">**Output:**</span></span>

<span data-ttu-id="280f8-378">Tiempo de ejecución de la celda: 33 segundos.</span><span class="sxs-lookup"><span data-stu-id="280f8-378">Time to run the cell: 33 seconds.</span></span>

### <a name="optimize-the-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="280f8-379">Optimización del modelo de regresión lineal mediante código personalizado de validación cruzada y barrido de parámetros</span><span class="sxs-lookup"><span data-stu-id="280f8-379">Optimize the linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="280f8-380">A continuación, optimice el modelo usando código personalizado e identifique los mejores parámetros del modelo mediante el criterio de mayor precisión.</span><span class="sxs-lookup"><span data-stu-id="280f8-380">Next, optimize the model by using custom code, and identify the best model parameters by using the criterion of highest accuracy.</span></span> <span data-ttu-id="280f8-381">Después, cree el modelo final, evalúelo con los datos de prueba y guárdelo en Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="280f8-381">Then, create the final model, evaluate the model on test data, and save the model in Blob storage.</span></span> <span data-ttu-id="280f8-382">Por último, cargue el modelo, puntúe los datos de prueba y evalúe su precisión.</span><span class="sxs-lookup"><span data-stu-id="280f8-382">Finally, load the model, score test data, and evaluate accuracy.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE PARAMETER GRID AND THE NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY THE NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
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


    # LOOP THROUGH K-FOLDS AND THE PARAMETER GRID TO GET AND IDENTIFY THE BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 to (nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 to (numModels-1)) {
            for (nParams <- 0 to (numParamsinGrid-1)) {
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

    # GET THE BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 to (numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE THE BEST MODEL WITH THE BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE THE BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON THE TRAINING SET WITH THE BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


    # LOAD THE MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST THE MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="280f8-383">**Salida:**</span><span class="sxs-lookup"><span data-stu-id="280f8-383">**Output:**</span></span>

<span data-ttu-id="280f8-384">Tiempo de ejecución de la celda: 61 segundos.</span><span class="sxs-lookup"><span data-stu-id="280f8-384">Time to run the cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="280f8-385">Uso automático en Scala de los modelos de aprendizaje automático creados en Spark</span><span class="sxs-lookup"><span data-stu-id="280f8-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="280f8-386">Para ver una introducción de los temas que lo guiarán por las tareas que componen el proceso de ciencia de datos en Azure, consulte [Proceso de ciencia de los datos en equipos (TDSP)](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="280f8-386">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="280f8-387">[Tutoriales del proceso de ciencia de datos en equipos](data-science-process-walkthroughs.md) describe otros tutoriales de extremo a extremo que muestran los pasos en el proceso de ciencia de datos de equipo en escenarios específicos.</span><span class="sxs-lookup"><span data-stu-id="280f8-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="280f8-388">En los tutoriales también se muestra cómo combinar servicios y herramientas en la nube y locales en un flujo de trabajo o una canalización con el fin de crear una aplicación inteligente.</span><span class="sxs-lookup"><span data-stu-id="280f8-388">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>

<span data-ttu-id="280f8-389">[Puntuación de modelos de aprendizaje automático creados con Spark](machine-learning-data-science-spark-model-consumption.md) muestra cómo utilizar código de Scala para cargar y puntuar automáticamente nuevos conjuntos de datos con modelos de aprendizaje automático creados en Spark y guardarlos en Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="280f8-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how to use Scala code to automatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="280f8-390">Se pueden seguir las instrucciones de ese artículo y, simplemente, reemplazar el código de Python por el de Scala que se indica aquí para permitir el uso automatizado.</span><span class="sxs-lookup"><span data-stu-id="280f8-390">You can follow the instructions provided there, and simply replace the Python code with Scala code in this article for automated consumption.</span></span>

