---
title: "Exploración y modelado de datos con Spark | Microsoft Docs"
description: "Muestra las funcionalidades de exploración y modelado de datos del kit de herramientas Spark MLlib en Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 711407f7dd9e6d442e3f04a23962487f4808e8e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="132f4-103">Exploración y modelado de datos con Spark</span><span class="sxs-lookup"><span data-stu-id="132f4-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="132f4-104">Este tutorial usa Spark en HDInsight para realizar tareas de modelado por exploración de datos, clasificación binaria y regresión en una muestra del conjunto de datos de carreras y tarifas de taxi de 2013 en la ciudad de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="132f4-104">This walkthrough uses HDInsight Spark to do data exploration and binary classification and regression modeling tasks on a sample of the NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="132f4-105">Lo guía por los pasos del [proceso de la ciencia de los datos](http://aka.ms/datascienceprocess), de principio a fin, usando un clúster de Spark en HDInsight para el procesamiento y blobs de Azure para almacenar los datos y los modelos.</span><span class="sxs-lookup"><span data-stu-id="132f4-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="132f4-106">El proceso analiza y visualiza los datos extraídos de un Blob de Almacenamiento de Azure y, después, los prepara para crear modelos predictivos.</span><span class="sxs-lookup"><span data-stu-id="132f4-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="132f4-107">Estos modelos se crean usando el kit de herramientas MLlib de Spark para realizar las tareas de clasificación binaria y modelado por regresión.</span><span class="sxs-lookup"><span data-stu-id="132f4-107">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="132f4-108">La tarea de **clasificación binaria** consiste en predecir si se dará propina por la carrera o no.</span><span class="sxs-lookup"><span data-stu-id="132f4-108">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="132f4-109">La tarea de **regresión** consiste en predecir el importe de la propina en función de otras características de la propina.</span><span class="sxs-lookup"><span data-stu-id="132f4-109">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="132f4-110">Los modelos que usamos incluyen regresión logística y lineal, bosques aleatorios y árboles impulsados por gradiente:</span><span class="sxs-lookup"><span data-stu-id="132f4-110">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="132f4-111">[regresión lineal con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) es un modelo de regresión lineal que usa un método de descenso de gradiente estocástico (SGD) para la optimización y el ajuste de la escala de las características para predecir las propinas.</span><span class="sxs-lookup"><span data-stu-id="132f4-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="132f4-112">[regresión logística con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) , o regresión "logit", es un modelo de regresión que puede usarse cuando la variable dependiente es de categorías para realizar la clasificación de los datos.</span><span class="sxs-lookup"><span data-stu-id="132f4-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="132f4-113">LBFGS es un algoritmo de optimización cuasi Newton que aproxima el algoritmo Broyden–Fletcher Goldfarb–Shanno (BFGS) usando una cantidad limitada de memoria de proceso, y que se usa ampliamente en el aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="132f4-113">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="132f4-114">[bosques aleatorios](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="132f4-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="132f4-115">Combinan varios árboles de decisión para reducir el riesgo de sobreajuste.</span><span class="sxs-lookup"><span data-stu-id="132f4-115">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="132f4-116">Los bosques aleatorios se usan para clasificación y regresión, y pueden controlar características categóricas, amplían la configuración de clasificación multiclase;</span><span class="sxs-lookup"><span data-stu-id="132f4-116">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="132f4-117">no requieren ajustar la escala de las características y pueden capturar errores de alineación e interacciones de las características.</span><span class="sxs-lookup"><span data-stu-id="132f4-117">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="132f4-118">Los bosques aleatorios son uno de los modelos de aprendizaje automático de más éxito para clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="132f4-118">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="132f4-119">[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="132f4-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="132f4-120">Los GBT entrenan árboles de decisión de forma iterativa para minimizar una función de pérdida.</span><span class="sxs-lookup"><span data-stu-id="132f4-120">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="132f4-121">Los GBT se usan para clasificación y regresión, y pueden controlar características categóricas, no requieren ajustar la escala de las características y pueden capturar errores de alineación e interacciones de las características.</span><span class="sxs-lookup"><span data-stu-id="132f4-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="132f4-122">También se pueden usar en una configuración de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="132f4-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="132f4-123">Los pasos de modelado también contienen código que muestra cómo entrenar, evaluar y guardar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="132f4-123">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="132f4-124">Se ha usado Python para codificar la solución y mostrar los trazados relevantes.</span><span class="sxs-lookup"><span data-stu-id="132f4-124">Python has been used to code the solution and to show the relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="132f4-125">Aunque el kit de herramientas MLlib de Spark está diseñado para trabajar con grandes conjuntos de datos, se usa por comodidad una muestra relativamente pequeña (~30 MB, 170 filas; aproximadamente el 0,1 % del conjunto de datos original de Nueva York).</span><span class="sxs-lookup"><span data-stu-id="132f4-125">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="132f4-126">El ejercicio que aquí se proporciona se ejecuta eficazmente en un clúster de HDInsight con 2 nodos de trabajo (en unos 10 minutos).</span><span class="sxs-lookup"><span data-stu-id="132f4-126">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="132f4-127">Se puede usar el mismo código, con modificaciones menores, para procesar conjuntos de datos mayores, con las modificaciones correspondientes para almacenar datos en memoria caché o cambiar el tamaño del clúster.</span><span class="sxs-lookup"><span data-stu-id="132f4-127">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="132f4-128">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="132f4-128">Prerequisites</span></span>
<span data-ttu-id="132f4-129">Necesita una cuenta de Azure y un clúster de Spark 1.6 o Spark 2.0 HDInsight para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="132f4-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="132f4-130">Consulte el artículo [Información general sobre la ciencia de los datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md) para obtener instrucciones sobre cómo satisfacer estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="132f4-130">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="132f4-131">Ese tema también contiene una descripción de los datos de taxis de Nueva York de 2013 que se usan aquí, además de instrucciones sobre cómo ejecutar el código de un cuaderno de Jupyter Notebook en el clúster Spark.</span><span class="sxs-lookup"><span data-stu-id="132f4-131">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="132f4-132">Clústeres y cuadernos de Spark</span><span class="sxs-lookup"><span data-stu-id="132f4-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="132f4-133">Los pasos de instalación y el código proporcionado en este tutorial son para HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="132f4-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="132f4-134">Sin embargo, Jupyter Notebooks se proporciona para clústeres de HDInsight Spark 1.6 y Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="132f4-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="132f4-135">Se proporciona una descripción de los cuadernos y de los vínculos a estos en el archivo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) del repositorio de GitHub que los contiene.</span><span class="sxs-lookup"><span data-stu-id="132f4-135">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="132f4-136">No obstante, este código y los cuadernos vinculados son genéricos y deberían funcionar en cualquier clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="132f4-136">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="132f4-137">Los pasos de configuración y administración del clúster pueden ser ligeramente diferentes de los que se muestran aquí si no está usando Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="132f4-137">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="132f4-138">Para mayor comodidad, estos son los vínculos a los cuadernos de Jupyter para Spark 1.6 (para ejecutarse en el kernel pySpark del servidor de Jupyter Notebook) y Spark 2.0 (para ejecutarse en el kernel pySpark3 del servidor de Jupyter Notebook):</span><span class="sxs-lookup"><span data-stu-id="132f4-138">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 (to be run in the pySpark kernel of the Jupyter Notebook server) and  Spark 2.0 (to be run in the pySpark3 kernel of the Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="132f4-139">Cuadernos de Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="132f4-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="132f4-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): proporciona información sobre cómo realizar una exploración de datos, el modelado y la puntuación con diversos algoritmos.</span><span class="sxs-lookup"><span data-stu-id="132f4-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how to perform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="132f4-141">Cuadernos de Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="132f4-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="132f4-142">Las tareas de clasificación y regresión que se implementan mediante un clúster de Spark 2.0 se encuentran en cuadernos diferentes y el cuaderno de clasificación usa un conjunto de datos distinto:</span><span class="sxs-lookup"><span data-stu-id="132f4-142">The regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and the classification notebook uses a different data set:</span></span>

- <span data-ttu-id="132f4-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este archivo proporciona información sobre cómo realizar el modelado, la puntuación y la exploración de datos en clústeres de Spark 2.0 mediante el conjunto de datos de carreras y tarifas de taxis en Nueva York que se describe [aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="132f4-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="132f4-144">Este cuaderno puede ser un buen punto de partida para explorar rápidamente el código proporcionado para Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="132f4-144">This notebook may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> <span data-ttu-id="132f4-145">Para obtener un análisis más pormenorizado de los datos del cuaderno sobre taxis en Nueva York, vea el siguiente cuaderno de esta lista.</span><span class="sxs-lookup"><span data-stu-id="132f4-145">For a more detailed notebook analyzes the NYC Taxi data, see the next notebook in this list.</span></span> <span data-ttu-id="132f4-146">Vea las notas después de esta lista en las que se establece una comparación de estos cuadernos.</span><span class="sxs-lookup"><span data-stu-id="132f4-146">See the notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="132f4-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): este archivo muestra cómo realizar la comparación de datos (Spark SQL y operaciones de trama de datos), la exploración, modelado y puntuación mediante el conjunto de datos de carreras y tarifas de NYC Taxi descrito [aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="132f4-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="132f4-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): este archivo muestra cómo realizar la comparación de datos (Spark SQL y operaciones de trama de datos), la exploración, modelado y puntuación mediante el conocido conjunto de datos de salidas puntuales de líneas aéreas de 2011 y 2012.</span><span class="sxs-lookup"><span data-stu-id="132f4-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="132f4-149">Se ha integrado el conjunto de datos de las líneas aéreas con los datos climatológicos del aeropuerto (por ejemplo, velocidad del viento, temperatura, altitud, etc.), antes de realizar el modelado, para que estas características climatológicas puedan incluirse en el modelo.</span><span class="sxs-lookup"><span data-stu-id="132f4-149">We integrated the airline dataset with the airport weather data (e.g. windspeed, temperature, altitude etc.) prior to modeling, so these weather features can be included in the model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="132f4-150">El conjunto de datos de las líneas aéreas se agregó a los cuadernos de Spark 2.0 para ilustrar mejor el uso de algoritmos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="132f4-150">The airline dataset was added to the Spark 2.0 notebooks to better illustrate the use of classification algorithms.</span></span> <span data-ttu-id="132f4-151">Consulte los siguientes vínculos para obtener información sobre el conjunto de datos de salidas puntuales de las líneas aéreas y sobre el de datos climatológicos:</span><span class="sxs-lookup"><span data-stu-id="132f4-151">See the following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="132f4-152">Datos de salida puntuales de líneas aéreas: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="132f4-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="132f4-153">Datos climatológicos del aeropuerto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="132f4-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="132f4-154">Los cuadernos de Spark 2.0 sobre los conjuntos de datos de los taxis de Nueva York y de retrasos en los vuelos pueden tardar 10 minutos o más en ejecutarse (dependiendo del tamaño del clúster de HDI).</span><span class="sxs-lookup"><span data-stu-id="132f4-154">The Spark 2.0 notebooks on the NYC taxi and airline flight delay data-sets can take 10 mins or more to run (depending on the size of your HDI cluster).</span></span> <span data-ttu-id="132f4-155">En el primer cuaderno de la lista anterior se reflejan muchos aspectos de la exploración de datos, la visualización y el entrenamiento del modelo de ML en un cuaderno que tarda menos tiempo en ejecutarse con el conjunto de datos de Nueva York muestreado, en el que los archivos de taxis y tarifas se han unido previamente: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) Este cuaderno tarda mucho menos tiempo en terminar (2-3 minutos) y puede ser un buen punto de partida para realizar una exploración rápida del código proporcionado para Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="132f4-155">The first notebook in the above list shows many aspects of the data exploration, visualization and ML model training in a notebook that takes less time to run with down-sampled NYC data set, in which the taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time to finish (2-3 mins) and may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="132f4-156">Las descripciones siguientes guardan relación con el uso de Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="132f4-156">The descriptions below are related to using Spark 1.6.</span></span> <span data-ttu-id="132f4-157">En las versiones de Spark 2.0, use los cuadernos descritos anteriormente, con sus correspondientes vínculos.</span><span class="sxs-lookup"><span data-stu-id="132f4-157">For Spark 2.0 versions, please use the notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="132f4-158">Configuración: Ubicaciones de almacenamiento, bibliotecas y el contexto de Spark preestablecido</span><span class="sxs-lookup"><span data-stu-id="132f4-158">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="132f4-159">Spark puede leer y escribir en un blob de Almacenamiento de Azure (también conocido como WASB),</span><span class="sxs-lookup"><span data-stu-id="132f4-159">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="132f4-160">por lo que cualquiera de los datos existentes almacenados allí pueden procesarse mediante Spark y volver a almacenarse en WASB.</span><span class="sxs-lookup"><span data-stu-id="132f4-160">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="132f4-161">Para guardar modelos o archivos en WASB, la ruta de acceso debe especificarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="132f4-161">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="132f4-162">Se puede hacer referencia al contenedor predeterminado asociado al clúster de Spark con un ruta que comience con: "wasb///".</span><span class="sxs-lookup"><span data-stu-id="132f4-162">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="132f4-163">Para hacer referencia a otras ubicaciones, se usa "wasb://".</span><span class="sxs-lookup"><span data-stu-id="132f4-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="132f4-164">Establecimiento de rutas de directorio para las ubicaciones de almacenamiento de WASB</span><span class="sxs-lookup"><span data-stu-id="132f4-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="132f4-165">El ejemplo de código siguiente especifica la ubicación de los datos que se van a leer y la ruta de acceso del directorio de almacenamiento del modelo donde se guardará la salida del modelo:</span><span class="sxs-lookup"><span data-stu-id="132f4-165">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="132f4-166">Importación de bibliotecas</span><span class="sxs-lookup"><span data-stu-id="132f4-166">Import libraries</span></span>
<span data-ttu-id="132f4-167">Para la configuración también es necesario importar las bibliotecas necesarias.</span><span class="sxs-lookup"><span data-stu-id="132f4-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="132f4-168">Establezca el contexto de Spark e importe las bibliotecas necesarias con el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="132f4-168">Set spark context and import necessary libraries with the following code:</span></span>

    # IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="132f4-169">Contexto de Spark preestablecido e instrucciones mágicas de PySpark</span><span class="sxs-lookup"><span data-stu-id="132f4-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="132f4-170">Los kernels de PySpark que se proporcionan con cuadernos de Jupyter Notebook tienen contextos preestablecidos.</span><span class="sxs-lookup"><span data-stu-id="132f4-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="132f4-171">No es necesario establecer explícitamente los contextos de Spark o Hive antes de empezar a trabajar con la aplicación que se esté desarrollando.</span><span class="sxs-lookup"><span data-stu-id="132f4-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="132f4-172">Estos contextos están disponibles de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="132f4-172">These contexts are available for you by default.</span></span> <span data-ttu-id="132f4-173">Estos contextos son:</span><span class="sxs-lookup"><span data-stu-id="132f4-173">These contexts are:</span></span>

* <span data-ttu-id="132f4-174">sc: Para Spark</span><span class="sxs-lookup"><span data-stu-id="132f4-174">sc - for Spark</span></span> 
* <span data-ttu-id="132f4-175">sqlContext: Para Hive</span><span class="sxs-lookup"><span data-stu-id="132f4-175">sqlContext - for Hive</span></span>

<span data-ttu-id="132f4-176">El kernel PySpark proporciona algunas “instrucciones mágicas” predefinidas, que son comandos especiales que se pueden llamar con %%.</span><span class="sxs-lookup"><span data-stu-id="132f4-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="132f4-177">Hay dos comandos de este tipo que se utilizan en estos ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="132f4-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="132f4-178">**%%local**: especifica que el código de las líneas siguientes se ejecutará localmente.</span><span class="sxs-lookup"><span data-stu-id="132f4-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="132f4-179">El código debe ser un código de Python válido.</span><span class="sxs-lookup"><span data-stu-id="132f4-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="132f4-180">**%%sql -o <variable name>** Ejecuta una consulta de Hive en sqlContext.</span><span class="sxs-lookup"><span data-stu-id="132f4-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="132f4-181">Si se pasa el parámetro -o, el resultado de la consulta se conserva en el contexto %%local de Python como trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="132f4-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="132f4-182">Para obtener más información sobre los kernels de cuadernos de Jupyter Notebook y las instrucciones mágicas predefinidas llamadas con %% (por ejemplo, %%local) que proporcionan, consulte [Kernels disponibles para cuadernos de Jupyter con clústeres de Spark en HDInsight basados en Linux en HDInsight (versión preliminar)](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="132f4-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="132f4-183">Ingesta de datos de blob público</span><span class="sxs-lookup"><span data-stu-id="132f4-183">Data ingestion from public blob</span></span>
<span data-ttu-id="132f4-184">El primer paso del proceso de ciencia de datos consiste en incorporar la información que se va a analizar desde los orígenes donde residen, a su entorno de exploración y modelado de datos.</span><span class="sxs-lookup"><span data-stu-id="132f4-184">The first step in the data science process is to ingest the data to be analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="132f4-185">Este entorno es Spark en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="132f4-185">The environment is Spark in this walkthrough.</span></span> <span data-ttu-id="132f4-186">Esta sección contiene el código para completar una serie de tareas:</span><span class="sxs-lookup"><span data-stu-id="132f4-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="132f4-187">incorporar la muestra de datos que se va a modelar</span><span class="sxs-lookup"><span data-stu-id="132f4-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="132f4-188">leer el conjunto de datos de entrada (almacenado como un archivo .tsv)</span><span class="sxs-lookup"><span data-stu-id="132f4-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="132f4-189">dar formato y limpiar los datos</span><span class="sxs-lookup"><span data-stu-id="132f4-189">format and clean the data</span></span>
* <span data-ttu-id="132f4-190">crear objetos en la memoria (RDD o tramas de datos) y almacenarlos en caché</span><span class="sxs-lookup"><span data-stu-id="132f4-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="132f4-191">registrarlos como una tabla temporal en el contexto de SQL</span><span class="sxs-lookup"><span data-stu-id="132f4-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="132f4-192">Este es el código para la incorporación de los datos.</span><span class="sxs-lookup"><span data-stu-id="132f4-192">Here is the code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="132f4-193">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-193">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-194">Time taken to execute above cell: 51.72 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-194">Time taken to execute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="132f4-195">Visualización y exploración de datos</span><span class="sxs-lookup"><span data-stu-id="132f4-195">Data exploration & visualization</span></span>
<span data-ttu-id="132f4-196">Una vez incorporados los datos en Spark, el siguiente paso del proceso de la ciencia de los datos es conocer mejor los datos mediante la exploración y la visualización.</span><span class="sxs-lookup"><span data-stu-id="132f4-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="132f4-197">En esta sección, examinaremos los datos de taxi mediante consultas SQL y trazaremos las variables de destino y las posibles características para su inspección visual.</span><span class="sxs-lookup"><span data-stu-id="132f4-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="132f4-198">En concreto, trazaremos la frecuencia de los recuentos de pasajeros en las carreras de taxi, la frecuencia de los importes de las propinas y cómo varían las propinas según el tipo y el importe del pago.</span><span class="sxs-lookup"><span data-stu-id="132f4-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="132f4-199">Trazado de un histograma de frecuencias de recuento de pasajeros en el ejemplo de carreras de taxi</span><span class="sxs-lookup"><span data-stu-id="132f4-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="132f4-200">Este código y fragmentos de código siguientes utilizan instrucciones mágicas de SQL para consultar los ejemplos e instrucciones mágicas locales para trazar los datos.</span><span class="sxs-lookup"><span data-stu-id="132f4-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="132f4-201">**Instrucciones mágicas de SQL (`%%sql`)** El kernel PySpark de HDInsight admite consultas sencillas de HiveQL en línea en sqlContext.</span><span class="sxs-lookup"><span data-stu-id="132f4-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="132f4-202">El argumento (-o VARIABLE_NAME) conserva la salida de la consulta SQL como una trama de datos de Pandas en el servidor de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="132f4-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="132f4-203">Esto significa que estará disponible en el modo local.</span><span class="sxs-lookup"><span data-stu-id="132f4-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="132f4-204">La **`%%local`** se utiliza para ejecutar código de forma local en el servidor de Jupyter, que es el nodo principal del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="132f4-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="132f4-205">Normalmente, se utilizan juntas las instrucciones mágicas `%%local` y `%%sql` con el parámetro -o.</span><span class="sxs-lookup"><span data-stu-id="132f4-205">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="132f4-206">El parámetro -o conservaría la salida de la consulta SQL localmente y luego la instrucción mágica %%local desencadenaría el siguiente conjunto de fragmento de código para ejecutarse localmente en la salida de las consultas SQL que se conserva localmente.</span><span class="sxs-lookup"><span data-stu-id="132f4-206">The -o parameter would persist the output of the SQL query locally and then %%local magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally</span></span>

<span data-ttu-id="132f4-207">La salida se visualizará automáticamente después de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="132f4-207">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="132f4-208">Esta consulta recupera los viajes por el número de pasajeros.</span><span class="sxs-lookup"><span data-stu-id="132f4-208">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="132f4-209">Este código crea una trama de datos local a partir de la salida de la consulta y traza los datos.</span><span class="sxs-lookup"><span data-stu-id="132f4-209">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="132f4-210">La instrucción mágica `%%local` crea una trama de datos local, `sqlResults`, que puede usarse para trazar la información con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="132f4-210">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="132f4-211">Esta instrucción mágica de PySpark se utiliza varias veces en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="132f4-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="132f4-212">Si la cantidad de datos es grande, debe muestrear para crear una trama de datos que pueda caber en la memoria local.</span><span class="sxs-lookup"><span data-stu-id="132f4-212">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="132f4-213">Este es el código para trazar los viajes por recuentos de pasajeros:</span><span class="sxs-lookup"><span data-stu-id="132f4-213">Here is the code to plot the trips by passenger counts</span></span>

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="132f4-214">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-214">**OUTPUT:**</span></span>

![Frecuencia de las carreras por número de pasajeros](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="132f4-216">Puede seleccionar entre diferentes tipos de visualizaciones (tabla, circular, línea, área o barra) mediante los botones del menú **Tipo** del cuaderno.</span><span class="sxs-lookup"><span data-stu-id="132f4-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="132f4-217">Aquí se muestra el gráfico de barras.</span><span class="sxs-lookup"><span data-stu-id="132f4-217">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="132f4-218">Trazado de un histograma de importes de propinas y de las variaciones en las propinas según número de pasajeros y tarifas.</span><span class="sxs-lookup"><span data-stu-id="132f4-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="132f4-219">Utilice una consulta SQL para muestrear datos.</span><span class="sxs-lookup"><span data-stu-id="132f4-219">Use a SQL query to sample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped 
    FROM taxi_train 
    WHERE passenger_count > 0 
    AND passenger_count < 7 
    AND fare_amount > 0 
    AND fare_amount < 200 
    AND payment_type in ('CSH', 'CRD') 
    AND tip_amount > 0 
    AND tip_amount < 25


<span data-ttu-id="132f4-220">Esta celda de código usa la consulta SQL para crear tres trazados de los datos.</span><span class="sxs-lookup"><span data-stu-id="132f4-220">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


<span data-ttu-id="132f4-221">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-221">**OUTPUT:**</span></span> 

![Distribución del importe de las propinas](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Importe de las propinas por número de pasajeros](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importe de las propinas por importe de la tarifa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="132f4-225">Diseño, transformación y preparación de los datos para el modelado de características</span><span class="sxs-lookup"><span data-stu-id="132f4-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="132f4-226">Esta sección describe y proporciona el código para los procedimientos que se usan para preparar los datos para su uso en el modelado de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="132f4-226">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="132f4-227">Muestra cómo realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="132f4-227">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="132f4-228">Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico</span><span class="sxs-lookup"><span data-stu-id="132f4-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="132f4-229">Indexación y codificación de características categóricas</span><span class="sxs-lookup"><span data-stu-id="132f4-229">Index and encode categorical features</span></span>
* <span data-ttu-id="132f4-230">Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="132f4-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="132f4-231">Creación de una submuestra aleatoria de datos y su división en conjuntos de entrenamiento y de pruebas</span><span class="sxs-lookup"><span data-stu-id="132f4-231">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="132f4-232">Ajuste de la escala de las características</span><span class="sxs-lookup"><span data-stu-id="132f4-232">Feature scaling</span></span>
* <span data-ttu-id="132f4-233">Almacenamiento de objetos en caché</span><span class="sxs-lookup"><span data-stu-id="132f4-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="132f4-234">Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico</span><span class="sxs-lookup"><span data-stu-id="132f4-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="132f4-235">Este código muestra cómo crear una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico y, después, cómo almacenar en caché la trama de datos resultante en memoria.</span><span class="sxs-lookup"><span data-stu-id="132f4-235">This code shows how to create a new feature by binning hours into traffic time buckets and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="132f4-236">Cuando se usan repetidamente conjuntos de datos distribuidos resistentes (RDD) y tramas de datos, el almacenamiento en caché mejora los tiempos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="132f4-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="132f4-237">Por lo tanto, almacenaremos en caché los RDD y las tramas de datos en varias fases del tutorial.</span><span class="sxs-lookup"><span data-stu-id="132f4-237">Accordingly, we cache RDDs and data-frames at several stages in the walkthrough.</span></span> 

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="132f4-238">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-238">**OUTPUT:**</span></span> 

<span data-ttu-id="132f4-239">126050</span><span class="sxs-lookup"><span data-stu-id="132f4-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="132f4-240">Indexación y codificación de características categóricas para la entrada en funciones de modelado</span><span class="sxs-lookup"><span data-stu-id="132f4-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="132f4-241">Esta sección muestra cómo indexar o codificar las características categóricas para la entrada en las funciones de modelado.</span><span class="sxs-lookup"><span data-stu-id="132f4-241">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="132f4-242">Las funciones de modelado y predicción de MLlib requieren características con datos de entrada categóricos indexados o codificados antes de usarlos.</span><span class="sxs-lookup"><span data-stu-id="132f4-242">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="132f4-243">Dependiendo del modelo, deberá indexar o codificarlos de maneras diferentes:</span><span class="sxs-lookup"><span data-stu-id="132f4-243">Depending on the model, you need to index or encode them in different ways:</span></span>  

* <span data-ttu-id="132f4-244">**modelado basado en árboles** requiere que las categorías se codifiquen como valores numéricos (por ejemplo, una característica con tres categorías se puede codificar con 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="132f4-244">**Tree-based modeling** requires categories to be encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="132f4-245">Esto lo proporciona la función [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) de MLlib.</span><span class="sxs-lookup"><span data-stu-id="132f4-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="132f4-246">Esta función codifica una columna de cadena de etiquetas en una columna de índices de etiqueta que se ordenan por frecuencias de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="132f4-246">This function encodes a string column of labels to a column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="132f4-247">Aunque se indexan con valores numéricos para facilitar la entrada y la manipulación de los datos, los algoritmos basados en árboles se pueden configurar para que los traten como categorías.</span><span class="sxs-lookup"><span data-stu-id="132f4-247">Although indexed with numerical values for input and data handling, the tree-based algorithms can be specified to treat them appropriately as categories.</span></span> 
* <span data-ttu-id="132f4-248">Los **modelos de regresión logística y lineal** requieren una codificación "uno de n", donde una característica con 3 categorías puede ampliarse a 3 columnas de característica, cada una de las cuales contiene 0 o 1 según la categoría de una observación.</span><span class="sxs-lookup"><span data-stu-id="132f4-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="132f4-249">MLlib proporciona la función [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) para realizar la codificación "one-hot".</span><span class="sxs-lookup"><span data-stu-id="132f4-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="132f4-250">Este codificador asigna una columna de índices de etiqueta a una columna de vectores binarios, con un solo valor uno como máximo.</span><span class="sxs-lookup"><span data-stu-id="132f4-250">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="132f4-251">Esta codificación permite aplicar algoritmos que esperan características con valores numéricos, como la regresión logística, a características categóricas.</span><span class="sxs-lookup"><span data-stu-id="132f4-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="132f4-252">Este es el código para indexar y codificar características categóricas:</span><span class="sxs-lookup"><span data-stu-id="132f4-252">Here is the code to index and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-253">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-253">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-254">Time taken to execute above cell: 1.28 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-254">Time taken to execute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="132f4-255">Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="132f4-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="132f4-256">Esta sección contiene código que muestra cómo indexar datos de texto categóricos como un tipo de datos de punto con etiqueta, y codificarlos para poder usarlos para entrenar y probar la regresión logística de MLlib y otros modelos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="132f4-256">This section contains code that shows how to index categorical text data as a labeled point data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="132f4-257">Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) con el formato de datos de entrada que necesita la mayoría de los algoritmos de aprendizaje automático de MLlib.</span><span class="sxs-lookup"><span data-stu-id="132f4-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="132f4-258">Un [punto con etiqueta](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) es un vector local, denso o disperso, asociado con una etiqueta o respuesta.</span><span class="sxs-lookup"><span data-stu-id="132f4-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="132f4-259">Esta sección contiene código que muestra cómo indexar datos de texto categóricos como un tipo de [datos de punto](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) con etiqueta, y codificarlos para poder usarlos para entrenar y probar la regresión logística de MLlib y otros modelos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="132f4-259">This section contains code that shows how to index categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="132f4-260">Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) que constan de una etiqueta (variable destino/respuesta) y un vector de característica.</span><span class="sxs-lookup"><span data-stu-id="132f4-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="132f4-261">Muchos algoritmos de aprendizaje automático de MLlib necesitan este formato de entrada.</span><span class="sxs-lookup"><span data-stu-id="132f4-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="132f4-262">Este es el código para indexar y codificar las características de texto para la clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="132f4-262">Here is the code to index and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="132f4-263">Este es el código para codificar e indexar características de texto de categorías para el análisis de regresión lineal.</span><span class="sxs-lookup"><span data-stu-id="132f4-263">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])

        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="132f4-264">Creación de una submuestra aleatoria de datos y su división en conjuntos de entrenamiento y de pruebas</span><span class="sxs-lookup"><span data-stu-id="132f4-264">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="132f4-265">Este código crea una muestra aleatoria de los datos (aquí se usa el 25 %).</span><span class="sxs-lookup"><span data-stu-id="132f4-265">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="132f4-266">Aunque no es necesario para este ejemplo debido al tamaño del conjunto de datos, se muestra cómo realizar la muestra para que sepa cómo hacerlo cuando lo necesite.</span><span class="sxs-lookup"><span data-stu-id="132f4-266">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample here so you know how to use it for your own problem when needed.</span></span> <span data-ttu-id="132f4-267">Cuando las muestras son grandes, esto puede ahorrar mucho tiempo al entrenar modelos.</span><span class="sxs-lookup"><span data-stu-id="132f4-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="132f4-268">Después, dividimos la muestra en una parte de entrenamiento (75 %) y una parte de pruebas (25 %) para el modelado de clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="132f4-268">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-269">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-269">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-270">Time taken to execute above cell: 0.24 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-270">Time taken to execute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="132f4-271">Ajuste de la escala de las características</span><span class="sxs-lookup"><span data-stu-id="132f4-271">Feature scaling</span></span>
<span data-ttu-id="132f4-272">El ajuste de la escala de las características, también conocido como normalización de los datos, garantiza que características con valores situados muy en los extremos no tengan un peso excesivo en la función objetivo.</span><span class="sxs-lookup"><span data-stu-id="132f4-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="132f4-273">El código para ajustar la escala de las características usa [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) para ajustarlas a la varianza de la unidad.</span><span class="sxs-lookup"><span data-stu-id="132f4-273">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="132f4-274">MLlib lo proporciona para su uso en la regresión lineal con descenso de gradiente estocástico (SGD), un popular algoritmo para entrenar una amplia variedad de otros modelos de aprendizaje automático tales como regresiones regularizadas o máquinas de vectores de soporte (SVM).</span><span class="sxs-lookup"><span data-stu-id="132f4-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="132f4-275">Hemos descubierto que el algoritmo LinearRegressionWithSGD es sensible al ajuste de la escala de las características.</span><span class="sxs-lookup"><span data-stu-id="132f4-275">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>
> 
> 

<span data-ttu-id="132f4-276">Con este código, se ajusta la escala de variables para usarlas con el algoritmo SGD lineal regularizado.</span><span class="sxs-lookup"><span data-stu-id="132f4-276">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

    # FEATURE SCALING

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-277">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-277">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-278">Time taken to execute above cell: 13.17 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-278">Time taken to execute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="132f4-279">Almacenamiento de objetos en caché</span><span class="sxs-lookup"><span data-stu-id="132f4-279">Cache objects in memory</span></span>
<span data-ttu-id="132f4-280">Para reducir el tiempo necesario para entrenar y probar los algoritmos de aprendizaje automático, puede almacenar en caché los objetos de trama de datos de entrada usados para clasificación, regresión y características con ajuste de la escala.</span><span class="sxs-lookup"><span data-stu-id="132f4-280">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression, and scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-281">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-281">**OUTPUT:**</span></span> 

<span data-ttu-id="132f4-282">Time taken to execute above cell: 0.15 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-282">Time taken to execute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="132f4-283">Predicción de si se dio propina o no con modelos de clasificación binaria</span><span class="sxs-lookup"><span data-stu-id="132f4-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="132f4-284">Esta sección muestra cómo usar tres modelos para la tarea de clasificación binaria para predecir si se dio propina o no en una carrera de taxi.</span><span class="sxs-lookup"><span data-stu-id="132f4-284">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="132f4-285">Los modelos que se presentan son:</span><span class="sxs-lookup"><span data-stu-id="132f4-285">The models presented are:</span></span>

* <span data-ttu-id="132f4-286">Regresión logística regularizada</span><span class="sxs-lookup"><span data-stu-id="132f4-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="132f4-287">Modelo de bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="132f4-287">Random forest model</span></span>
* <span data-ttu-id="132f4-288">Árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="132f4-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="132f4-289">Cada sección de código de generación del modelo se dividirá en pasos:</span><span class="sxs-lookup"><span data-stu-id="132f4-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="132f4-290">**entrenamiento del modelo** con un conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="132f4-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="132f4-291">**Evaluación del modelo** en un conjunto de datos de prueba con métricas</span><span class="sxs-lookup"><span data-stu-id="132f4-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="132f4-292">**Guardado del modelo** en un blob para utilizarse en el futuro</span><span class="sxs-lookup"><span data-stu-id="132f4-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="132f4-293">Clasificación mediante regresión logística</span><span class="sxs-lookup"><span data-stu-id="132f4-293">Classification using logistic regression</span></span>
<span data-ttu-id="132f4-294">El código de esta sección muestra cómo entrenar, evaluar y guardar un modelo de regresión logística con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , que predice si se dio propina o no en una carrera, en el conjunto de datos de carreras y tarifas de taxi de la ciudad de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="132f4-294">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="132f4-295">**Entrenamiento del modelo de regresión logística con CV y barrido de hiperparámetros**</span><span class="sxs-lookup"><span data-stu-id="132f4-295">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="132f4-296">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-296">**OUTPUT:**</span></span> 

<span data-ttu-id="132f4-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="132f4-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="132f4-298">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="132f4-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="132f4-299">Time taken to execute above cell: 14.43 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-299">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="132f4-300">**Evaluación del modelo de clasificación binaria con métricas estándares**</span><span class="sxs-lookup"><span data-stu-id="132f4-300">**Evaluate the binary classification model with standard metrics**</span></span>

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="132f4-301">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-301">**OUTPUT:**</span></span> 

<span data-ttu-id="132f4-302">Area under PR = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="132f4-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="132f4-303">Area under ROC = 0.983714670256</span><span class="sxs-lookup"><span data-stu-id="132f4-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="132f4-304">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="132f4-304">Summary Stats</span></span>

<span data-ttu-id="132f4-305">Precision = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="132f4-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="132f4-306">Recall = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="132f4-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="132f4-307">F1 Score = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="132f4-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="132f4-308">Time taken to execute above cell: 57.61 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-308">Time taken to execute above cell: 57.61 seconds</span></span>

<span data-ttu-id="132f4-309">**Trazado de la curva ROC.**</span><span class="sxs-lookup"><span data-stu-id="132f4-309">**Plot the ROC curve.**</span></span>

<span data-ttu-id="132f4-310">*predictionAndLabelsDF* está registrado como una tabla, *tmp_results*, en la celda anterior.</span><span class="sxs-lookup"><span data-stu-id="132f4-310">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="132f4-311">*tmp_results* puede utilizarse para hacer consultas y mostrar los resultados en la trama de datos de sqlResults para el trazado.</span><span class="sxs-lookup"><span data-stu-id="132f4-311">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="132f4-312">Este es el código.</span><span class="sxs-lookup"><span data-stu-id="132f4-312">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="132f4-313">Este es el código para realizar predicciones y trazar la curva ROC.</span><span class="sxs-lookup"><span data-stu-id="132f4-313">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


<span data-ttu-id="132f4-314">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="132f4-316">Clasificación de bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="132f4-316">Random forest classification</span></span>
<span data-ttu-id="132f4-317">El código de esta sección muestra cómo entrenar, evaluar y guardar un modelo de bosque aleatorio que predice si se dio propina o no en una carrera, en el conjunto de datos de carreras de taxi y tarifas de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="132f4-317">The code in this section shows how to train, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT TO PRINT TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-318">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-318">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-319">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="132f4-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="132f4-320">Time taken to execute above cell: 31.09 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-320">Time taken to execute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="132f4-321">Clasificación de árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="132f4-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="132f4-322">El código de esta sección muestra cómo entrenar, evaluar y guardar un modelo de árboles impulsados por gradiente que predice si se dio propina o no en una carrera, en el conjunto de datos de carreras de taxi y tarifas de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="132f4-322">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="132f4-323">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-323">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-324">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="132f4-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="132f4-325">Time taken to execute above cell: 19.76 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-325">Time taken to execute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="132f4-326">Predicción de los importes de las propinas en las carreras de taxi con modelos de regresión</span><span class="sxs-lookup"><span data-stu-id="132f4-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="132f4-327">Esta sección muestra cómo usar tres modelos para la tarea de regresión para predecir el importe de la propina para una carrera de taxi en función de otras características de propina.</span><span class="sxs-lookup"><span data-stu-id="132f4-327">This section shows how use three models for the regression task of predicting the amount of the tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="132f4-328">Los modelos que se presentan son:</span><span class="sxs-lookup"><span data-stu-id="132f4-328">The models presented are:</span></span>

* <span data-ttu-id="132f4-329">Regresión lineal regularizada</span><span class="sxs-lookup"><span data-stu-id="132f4-329">Regularized linear regression</span></span>
* <span data-ttu-id="132f4-330">Bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="132f4-330">Random forest</span></span>
* <span data-ttu-id="132f4-331">Árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="132f4-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="132f4-332">Estos modelos se describieron en la introducción.</span><span class="sxs-lookup"><span data-stu-id="132f4-332">These models were described in the introduction.</span></span> <span data-ttu-id="132f4-333">Cada sección de código de generación del modelo se dividirá en pasos:</span><span class="sxs-lookup"><span data-stu-id="132f4-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="132f4-334">**entrenamiento del modelo** con un conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="132f4-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="132f4-335">**Evaluación del modelo** en un conjunto de datos de prueba con métricas</span><span class="sxs-lookup"><span data-stu-id="132f4-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="132f4-336">**Guardado del modelo** en un blob para utilizarse en el futuro</span><span class="sxs-lookup"><span data-stu-id="132f4-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="132f4-337">regresión lineal con SGD</span><span class="sxs-lookup"><span data-stu-id="132f4-337">Linear regression with SGD</span></span>
<span data-ttu-id="132f4-338">El código en esta sección muestra cómo usar características con ajuste de la escala para entrenar una regresión lineal que usa el descenso de gradiente estocástico (SGD) para la optimización, y cómo puntuar, evaluar y guardar el modelo en Almacenamiento de blobs de Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="132f4-338">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="132f4-339">Nuestra experiencia nos indica que puede haber problemas con la convergencia de los modelos LinearRegressionWithSGD y es necesario cambiar u optimizar los parámetros cuidadosamente para obtener un modelo válido.</span><span class="sxs-lookup"><span data-stu-id="132f4-339">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="132f4-340">El ajuste de la escala de las variables ayuda con la convergencia.</span><span class="sxs-lookup"><span data-stu-id="132f4-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN THE DEFAULT BLOB FOR THE CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-341">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-341">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="132f4-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="132f4-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="132f4-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="132f4-344">RMSE = 1.24190115863</span><span class="sxs-lookup"><span data-stu-id="132f4-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="132f4-345">R-sqr = 0.608017146081</span><span class="sxs-lookup"><span data-stu-id="132f4-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="132f4-346">Time taken to execute above cell: 58.42 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-346">Time taken to execute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="132f4-347">Regresión con bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="132f4-347">Random Forest regression</span></span>
<span data-ttu-id="132f4-348">El código de esta sección muestra cómo entrenar, evaluar y guardar una regresión de bosque aleatoria que predice el importe de las propinas en los datos de carreras de taxi de la ciudad de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="132f4-348">The code in this section shows how to train, evaluate, and save a random forest regression that predicts tip amount for the NYC taxi trip data.</span></span>

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-349">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-349">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-350">RMSE = 0.891209218139</span><span class="sxs-lookup"><span data-stu-id="132f4-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="132f4-351">R-sqr = 0.759661334921</span><span class="sxs-lookup"><span data-stu-id="132f4-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="132f4-352">Time taken to execute above cell: 49.21 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-352">Time taken to execute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="132f4-353">Regresión con árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="132f4-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="132f4-354">El código de esta sección muestra cómo entrenar, evaluar y guardar un modelo de árboles impulsados por gradiente que predice el importe de las propinas en los datos de carreras de taxi de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="132f4-354">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="132f4-355">** Entrenar y evaluar **</span><span class="sxs-lookup"><span data-stu-id="132f4-355">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS TO DF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="132f4-356">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-356">**OUTPUT:**</span></span>

<span data-ttu-id="132f4-357">RMSE = 0.908473148639</span><span class="sxs-lookup"><span data-stu-id="132f4-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="132f4-358">R-sqr = 0.753835096681</span><span class="sxs-lookup"><span data-stu-id="132f4-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="132f4-359">Time taken to execute above cell: 34.52 seconds</span><span class="sxs-lookup"><span data-stu-id="132f4-359">Time taken to execute above cell: 34.52 seconds</span></span>

<span data-ttu-id="132f4-360">**Trazado**</span><span class="sxs-lookup"><span data-stu-id="132f4-360">**Plot**</span></span>

<span data-ttu-id="132f4-361">*tmp_results* se registra como una tabla de Hive en la celda anterior.</span><span class="sxs-lookup"><span data-stu-id="132f4-361">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="132f4-362">Los resultados de la tabla se envían a la trama de datos *sqlResults* para el trazado.</span><span class="sxs-lookup"><span data-stu-id="132f4-362">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="132f4-363">Este es el código.</span><span class="sxs-lookup"><span data-stu-id="132f4-363">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="132f4-364">Este es el código para trazar los datos mediante el servidor de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="132f4-364">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


<span data-ttu-id="132f4-365">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="132f4-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="132f4-367">Limpieza de objetos de la memoria</span><span class="sxs-lookup"><span data-stu-id="132f4-367">Clean up objects from memory</span></span>
<span data-ttu-id="132f4-368">Use `unpersist()` para eliminar objetos almacenados en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="132f4-368">Use `unpersist()` to delete objects cached in memory.</span></span>

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


## <a name="record-storage-locations-of-the-models-for-consumption-and-scoring"></a><span data-ttu-id="132f4-369">Ubicaciones de almacenamiento de registros de los modelos para consumo y puntuación</span><span class="sxs-lookup"><span data-stu-id="132f4-369">Record storage locations of the models for consumption and scoring</span></span>
<span data-ttu-id="132f4-370">Para consumir y puntuar un conjunto de datos independiente que se describe en el tema [Puntuación de modelos de aprendizaje automático creados con Spark](machine-learning-data-science-spark-model-consumption.md), deberá copiar y pegar estos nombres de archivo (que contienen los modelos guardados creados aquí) en el cuaderno de consumo de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="132f4-370">To consume and score an independent dataset described in the [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need to copy and paste these file names containing the saved models created here into the Consumption Jupyter notebook.</span></span> <span data-ttu-id="132f4-371">Este es el código para imprimir las rutas de acceso a los archivos de modelo que necesita.</span><span class="sxs-lookup"><span data-stu-id="132f4-371">Here is the code to print out the paths to model files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="132f4-372">**SALIDA**</span><span class="sxs-lookup"><span data-stu-id="132f4-372">**OUTPUT**</span></span>

<span data-ttu-id="132f4-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="132f4-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="132f4-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="132f4-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="132f4-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="132f4-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="132f4-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="132f4-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="132f4-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="132f4-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="132f4-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="132f4-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="132f4-379">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="132f4-379">What's next?</span></span>
<span data-ttu-id="132f4-380">Ahora que ha creado los modelos de clasificación y regresión con Spark MlLib, está listo para aprender a puntuar y evaluar estos modelos.</span><span class="sxs-lookup"><span data-stu-id="132f4-380">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span> <span data-ttu-id="132f4-381">El Notebook de exploración y modelado de datos avanzado profundiza más en la inclusión de la validación cruzada, el barrido de los hiperparámetros y en la evaluación de modelos.</span><span class="sxs-lookup"><span data-stu-id="132f4-381">The advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="132f4-382">**Consumo de modelos** : Para saber cómo puntuar y evaluar los modelos de clasificación y regresión creados en este tema, consulte [Puntuación de modelos de aprendizaje automático creados con Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="132f4-382">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="132f4-383">**Validación cruzada y barrido de hiperparámetros**: consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) sobre cómo pueden prepararse los modelos con el barrido de hiperparámetros y la validación cruzada.</span><span class="sxs-lookup"><span data-stu-id="132f4-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

