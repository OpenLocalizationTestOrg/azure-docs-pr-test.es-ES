---
title: "exploración de aaaData y modelado con Spark | Documentos de Microsoft"
description: "Exhibe Hola funciones del Kit de herramientas de hello MLlib Spark en Azure de modelado y exploración de datos."
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
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="a5e5d-103">Exploración y modelado de datos con Spark</span><span class="sxs-lookup"><span data-stu-id="a5e5d-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="a5e5d-104">En este tutorial usa exploración de datos de HDInsight Spark toodo y clasificación binaria y regresión tareas de modelado en una muestra de Hola NYC taxi de ida y vuelta y resultados son el conjunto de datos de 2013.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="a5e5d-105">Le guiará por los pasos de Hola de hello [proceso de ciencia de datos](http://aka.ms/datascienceprocess), -to-end, con un HDInsight Spark de clúster para el procesamiento y modelos de datos y Hola Hola toostore de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="a5e5d-106">proceso de Hello explora y visualiza los datos agregados de un Blob de almacenamiento de Azure y, a continuación, prepara Hola datos toobuild modelos predictivos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="a5e5d-107">Estos modelos son compilación con clasificación binaria del toodo Hola Spark MLlib Kit de herramientas y tareas de modelado de regresión.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="a5e5d-108">Hola **clasificación binaria** tarea es toopredict haya o no una sugerencia se paga por los recorridos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="a5e5d-109">Hola **regresión** tarea es la cantidad de Hola de toopredict de sugerencia de hello en función de otras características de sugerencia.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="a5e5d-110">los modelos de Hello que usamos incluyen regresión logística y lineal, los bosques aleatorios y los árboles impulsados degradados:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="a5e5d-111">[Regresión lineal con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) es un modelo de regresión lineal que usa un método de descenso de gradiente estocástico (SGD) y para la optimización y la característica de ajuste de escala en cantidades de sugerencia de hello toopredict pago.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="a5e5d-112">[Regresión logística con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) o regresión "logit", es un modelo de regresión que puede usarse en la variable dependiente de hello es la clasificación de datos de categorías toodo.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="a5e5d-113">LBFGS es un algoritmo de optimización de Newton tipo que se aproxima al algoritmo de hello Broyden – Fletcher – Goldfarb – Shanno (BFGS) con una cantidad limitada de memoria del equipo y que se usa ampliamente en el aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="a5e5d-114">[bosques aleatorios](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="a5e5d-115">Combina riesgo del Hola de tooreduce de árboles de muchos decisión de desbordamiento.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="a5e5d-116">Bosques aleatorios se utilizan para la clasificación y regresión, pueden controlar las características de categorías y se pueden ampliar Configuración de clasificación multiclase toohello.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="a5e5d-117">No se requieren característica ajuste de escala y se pueda toocapture no linealidades e interacciones de característica.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="a5e5d-118">Bosques aleatorios son uno de los modelos para la clasificación y regresión de aprendizaje de máquina más éxito Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="a5e5d-119">[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="a5e5d-120">Árboles de decisión de entrenamiento de GBTs forma iterativa toominimize una función de pérdida.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="a5e5d-121">GBTs se usan para la clasificación y regresión y puede controlar las características de categorías, no requieren la característica escalado y no es capaz de toocapture linealidades y las interacciones de características.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="a5e5d-122">También se pueden usar en una configuración de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="a5e5d-123">pasos de modelado de Hello también contienen código que muestra cómo tootrain, evaluar y guardar cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="a5e5d-124">Python ha sido toocode usado Hola solución y tooshow Hola relevantes trazados.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="a5e5d-125">Aunque el Kit de herramientas de hello Spark MLlib es toowork diseñado en grandes conjuntos de datos, un ejemplo relativamente pequeño (con filas de 170K, aproximadamente 0,1% del conjunto de datos de Nueva York original Hola de ~ 30 Mb) se utiliza aquí por comodidad.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="a5e5d-126">ejercicio Hola aquí especificado se ejecuta eficazmente (en unos 10 minutos) en un clúster de HDInsight con 2 nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="a5e5d-127">Hello mismo código, con modificaciones menores, puede ser tooprocess usado más grandes conjuntos de datos, con las modificaciones apropiadas para almacenar en caché datos en la memoria y cambiar el tamaño de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a5e5d-128">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-128">Prerequisites</span></span>
<span data-ttu-id="a5e5d-129">Se necesita una cuenta de Azure y un Spark 1.6 (o 2.0 de Spark) clúster de HDInsight toocomplete en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="a5e5d-130">Vea hello [información general de ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md) para obtener instrucciones sobre cómo toosatisfy estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="a5e5d-131">Este tema también contiene una descripción de hello datos NYC 2013 Taxi emplear e instrucciones sobre cómo tooexecute código de Jupyter notebook en clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="a5e5d-132">Clústeres y cuadernos de Spark</span><span class="sxs-lookup"><span data-stu-id="a5e5d-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="a5e5d-133">Los pasos de instalación y el código proporcionado en este tutorial son para HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="a5e5d-134">Sin embargo, Jupyter Notebooks se proporciona para clústeres de HDInsight Spark 1.6 y Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="a5e5d-135">Se proporciona una descripción de hello blocs de notas y vínculos toothem Hola [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para el repositorio de GitHub de Hola que los contienen.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="a5e5d-136">Además, código de hello aquí y en blocs de notas de hello vinculada genérica y debe funcionar en cualquier clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="a5e5d-137">Si no utilizas HDInsight Spark, pasos de configuración y administración de clúster de hello pueden ser ligeramente diferentes de lo que se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="a5e5d-138">Para mayor comodidad, estos son Hola vínculos toohello Jupyter portátiles con Spark 1.6 (toobe ejecutar en el núcleo de pySpark Hola de hello servidor de Jupyter Notebook) y Spark 2.0 (se ejecuta en el núcleo de pySpark3 Hola de servidor de Jupyter Notebook hello toobe):</span><span class="sxs-lookup"><span data-stu-id="a5e5d-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="a5e5d-139">Cuadernos de Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="a5e5d-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="a5e5d-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): proporciona información acerca de cómo tooperform la exploración de datos, modelado y puntuación con varios algoritmos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="a5e5d-141">Cuadernos de Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="a5e5d-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="a5e5d-142">tareas de clasificación y regresión de Hola que se implementan mediante un clúster de Spark 2.0 son en blocs de notas independientes y portátil de clasificación de hello utiliza otro conjunto de datos:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="a5e5d-143">[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este archivo proporciona información sobre cómo tooperform la exploración de datos, modelado y puntuación en Spark 2.0 clústeres utilizando Hola recorridos Taxi de Nueva York y se describe de conjunto de datos tarifa [aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="a5e5d-144">Este bloc de notas puede ser un buen punto de partida para analizar rápidamente el código de hello que se proporcionan para Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="a5e5d-145">Para un bloc de notas más detallada analiza Hola datos Taxi de Nueva York, consulte Bloc de notas siguiente hello en esta lista.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="a5e5d-146">Vea las notas de hello después de la lista que comparan estos blocs de notas.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="a5e5d-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): este archivo muestra cómo tooperform datos problemas con (Spark SQL y trama de datos de operaciones), la exploración, modelado y puntuación mediante Hola tarifas conjunto de datos se describe y recorridos de Nueva York Taxi [ aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="a5e5d-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): este archivo muestra cómo tooperform datos problemas con (Spark SQL y trama de datos de operaciones), la exploración, modelado y puntuación mediante Hola conocido salida en el momento de Airline conjunto de datos de 2011 y 2012.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="a5e5d-149">El conjunto de datos de hello airline se habían integrado con hello aeropuerto tiempo datos (por ejemplo, velocidad del viento, temperatura, altitud, etc.) anteriores toomodeling para que estas características de tiempo pueden incluirse en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="a5e5d-150">el conjunto de datos de Hello airline agregó blocs de notas toohello Spark 2.0 toobetter ilustran el uso de Hola de algoritmos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="a5e5d-151">Vea Hola siguientes vínculos para obtener información sobre el conjunto de datos de salida en el momento de airline y conjunto de datos de tiempo:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="a5e5d-152">Datos de salida puntuales de líneas aéreas: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="a5e5d-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="a5e5d-153">Datos climatológicos del aeropuerto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="a5e5d-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="a5e5d-154">blocs de notas de Hello Spark 2.0 en hello taxi de Nueva York y airline vuelo retraso conjuntos de datos pueden tardar 10 minutos o más toorun (según el tamaño de Hola de su clúster HDI).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="a5e5d-155">Hello primer portátil Hola por encima de la lista muestra muchos aspectos Hola de exploración de datos, visualización y aprendizaje automático del modelo de entrenamiento en un portátil que toma menos toorun de tiempo con muestrear abajo NYC conjunto de datos, en qué Hola taxi y tarifa que se hayan archivos previamente combinados: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) este bloc de notas toma una cantidad menor tiempo toofinish (2-3 minutos) y puede ser un buen punto de partida para analizar rápidamente el código de hello tenemos se proporcionan para Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="a5e5d-156">las descripciones de Hola a continuación están relacionado toousing Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="a5e5d-157">En las versiones 2.0 Spark, use blocs de notas de Hola se describe e indicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="a5e5d-158">El programa de instalación: Hola, bibliotecas y ubicaciones de almacenamiento preestablecido contexto Spark</span><span class="sxs-lookup"><span data-stu-id="a5e5d-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="a5e5d-159">Spark es capaz de tooAzure tooread y escritura Blob de almacenamiento (también conocido como WASB).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="a5e5d-160">Por lo tanto, cualquiera de los datos existentes almacenados en ella se pueden procesar mediante Spark y Hola resultados almacenados en WASB.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="a5e5d-161">modelos de toosave o archivos en WASB, ruta de acceso de hello debe toobe especificado correctamente.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="a5e5d-162">Hola de clúster predeterminado contenedor adjuntada toohello Spark puede hacer referencia mediante un ruta que comienza con: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="a5e5d-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="a5e5d-163">Para hacer referencia a otras ubicaciones, se usa "wasb://".</span><span class="sxs-lookup"><span data-stu-id="a5e5d-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="a5e5d-164">Establecimiento de rutas de directorio para las ubicaciones de almacenamiento de WASB</span><span class="sxs-lookup"><span data-stu-id="a5e5d-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="a5e5d-165">ejemplo de código siguiente Hello Especifica ubicación Hola de hello toobe de datos de lectura y se guarda la ruta de acceso de hello para la salida de hello modelo almacenamiento directory toowhich Hola modelo:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="a5e5d-166">Importación de bibliotecas</span><span class="sxs-lookup"><span data-stu-id="a5e5d-166">Import libraries</span></span>
<span data-ttu-id="a5e5d-167">Para la configuración también es necesario importar las bibliotecas necesarias.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="a5e5d-168">Establecer contexto de spark e importar bibliotecas necesarias con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-168">Set spark context and import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="a5e5d-169">Contexto de Spark preestablecido e instrucciones mágicas de PySpark</span><span class="sxs-lookup"><span data-stu-id="a5e5d-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="a5e5d-170">los kernels de Hello PySpark que se proporcionan con blocs de notas Jupyter tienen un contexto de valores preestablecido.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="a5e5d-171">Por lo que no es necesario tooset Hola Spark o subárbol contextos explícitamente antes de empezar a trabajar con la aplicación hello que está desarrollando.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="a5e5d-172">Estos contextos están disponibles de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-172">These contexts are available for you by default.</span></span> <span data-ttu-id="a5e5d-173">Estos contextos son:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-173">These contexts are:</span></span>

* <span data-ttu-id="a5e5d-174">sc: Para Spark</span><span class="sxs-lookup"><span data-stu-id="a5e5d-174">sc - for Spark</span></span> 
* <span data-ttu-id="a5e5d-175">sqlContext: Para Hive</span><span class="sxs-lookup"><span data-stu-id="a5e5d-175">sqlContext - for Hive</span></span>

<span data-ttu-id="a5e5d-176">Hello PySpark kernel proporciona algunos predefinidas "magics", que son comandos especiales que se pueden llamar con %%.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="a5e5d-177">Hay dos comandos de este tipo que se utilizan en estos ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="a5e5d-178">**%% local** especifica que el código de hello en las líneas siguientes es toobe ejecutado de forma local.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="a5e5d-179">El código debe ser un código de Python válido.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="a5e5d-180">**%% sql -o <variable name>**  ejecuta una consulta de Hive en hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="a5e5d-181">Si se pasa el parámetro -o de hello, resultado de hello de consulta de Hola se conserva en hello %% contexto Python local como una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="a5e5d-182">Para obtener más información sobre los kernels de Hola para hello predefinidos y blocs de notas de Jupyter "magics" que proporcionan, consulte [clústeres de núcleos disponibles para equipos portátiles Jupyter con Linux de HDInsight Spark en HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="a5e5d-183">Ingesta de datos de blob público</span><span class="sxs-lookup"><span data-stu-id="a5e5d-183">Data ingestion from public blob</span></span>
<span data-ttu-id="a5e5d-184">Hola primer paso en el proceso de ciencia de datos de hello es tooingest Hola datos toobe analizado de orígenes donde es reside en el entorno de exploración y el modelado de datos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="a5e5d-185">entorno de Hello es Spark en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="a5e5d-186">Esta sección contiene código de hello toocomplete una serie de tareas:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="a5e5d-187">Introducción toobe de ejemplo de Hola datos modelada</span><span class="sxs-lookup"><span data-stu-id="a5e5d-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="a5e5d-188">leer en el conjunto de datos de entrada hello (almacenado como un archivo .tsv)</span><span class="sxs-lookup"><span data-stu-id="a5e5d-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="a5e5d-189">formato y Hola limpiar datos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-189">format and clean hello data</span></span>
* <span data-ttu-id="a5e5d-190">crear objetos en la memoria (RDD o tramas de datos) y almacenarlos en caché</span><span class="sxs-lookup"><span data-stu-id="a5e5d-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="a5e5d-191">registrarlos como una tabla temporal en el contexto de SQL</span><span class="sxs-lookup"><span data-stu-id="a5e5d-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="a5e5d-192">Este es el código de hello para la recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-192">Here is hello code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="a5e5d-193">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-193">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-194">Tiempo que tarda tooexecute encima de la celda: 51.72 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="a5e5d-195">Visualización y exploración de datos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-195">Data exploration & visualization</span></span>
<span data-ttu-id="a5e5d-196">Una vez introducidos los datos de hello en Spark, hello siguiente paso en el proceso de ciencia de datos de hello es toogain descripción más profunda de los datos de hello mediante exploración y visualización.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="a5e5d-197">En esta sección, se examinan datos de taxi hello mediante consultas SQL y las variables de destino de trazado hello y características posibles para la inspección visual.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="a5e5d-198">En concreto, se traza frecuencia Hola de recuentos de pasajeros en viajes taxi, la frecuencia de Hola de cantidades de sugerencia y cómo sugerencias varían según el tipo y la cantidad de pago.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="a5e5d-199">Trazar un histograma de frecuencias de recuento de pasajeros en el ejemplo hello de viajes de taxi</span><span class="sxs-lookup"><span data-stu-id="a5e5d-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="a5e5d-200">Este código y fragmentos de código siguientes usan SQL tooquery mágico Hola datos de ejemplo y local tooplot mágico Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="a5e5d-201">**Magia SQL (`%%sql`)** HDInsight PySpark kernel hello admite consultas de HiveQL en línea fácil contra Hola sqlContext.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="a5e5d-202">Hola (-o VARIABLE_NAME) argumento conserva la salida de hello de consulta SQL de hello como una trama de datos de Pandas en el servidor de Jupyter Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="a5e5d-203">Esto significa que está disponible en modo local Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="a5e5d-204">Hola  **`%%local` mágico** es código toorun los utiliza localmente en el servidor de Jupyter hello, que es el nodo principal de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="a5e5d-205">Normalmente, se utiliza `%%local` mágico junto con hello `%%sql` mágico con el parámetro -o.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="a5e5d-206">parámetro de Hello -o podría conservar la salida de hello de consulta SQL Hola localmente y, a continuación, %% magia local desencadenaría conjunto siguiente de Hola de toorun de fragmento de código localmente en la salida de hello de consultas SQL de Hola que se guarda localmente</span><span class="sxs-lookup"><span data-stu-id="a5e5d-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="a5e5d-207">salida de Hello se visualiza automáticamente después de ejecutar código de hello.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="a5e5d-208">Esta consulta recupera el recuento de pasajeros ciclos de ida y Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="a5e5d-209">Este código crea una trama de datos local de resultado de la consulta de Hola y representa los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="a5e5d-210">Hola `%%local` mágico crea una trama de datos local, `sqlResults`, que se puede utilizar para trazar con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="a5e5d-211">Esta instrucción mágica de PySpark se utiliza varias veces en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="a5e5d-212">Si la cantidad de Hola de datos es grande, debe muestrear toocreate una trama de datos que cabe en la memoria local.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="a5e5d-213">Aquí es viajes de hello código tooplot Hola pasajeros recuentos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-213">Here is hello code tooplot hello trips by passenger counts</span></span>

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

<span data-ttu-id="a5e5d-214">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-214">**OUTPUT:**</span></span>

![Frecuencia de las carreras por número de pasajeros](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="a5e5d-216">Puede seleccionar entre los distintos tipos de visualizaciones (tabla, circular, línea, el área o barra) mediante el uso de hello **tipo** botones de menú en el Bloc de notas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="a5e5d-217">aquí se muestra un gráfico de barras de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="a5e5d-218">Trazado de un histograma de importes de propinas y de las variaciones en las propinas según número de pasajeros y tarifas.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="a5e5d-219">Utilice una consulta toosample datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-219">Use a SQL query toosample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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


<span data-ttu-id="a5e5d-220">Esta celda de código usa Hola SQL consulta toocreate tres traza Hola datos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
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


<span data-ttu-id="a5e5d-221">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-221">**OUTPUT:**</span></span> 

![Distribución del importe de las propinas](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Importe de las propinas por número de pasajeros](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importe de las propinas por importe de la tarifa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="a5e5d-225">Diseño, transformación y preparación de los datos para el modelado de características</span><span class="sxs-lookup"><span data-stu-id="a5e5d-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="a5e5d-226">En esta sección se describe y proporciona código de hello para conocer los procedimientos que utiliza datos tooprepare para su uso en el modelado de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="a5e5d-227">Muestra cómo hello toodo siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="a5e5d-228">Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico</span><span class="sxs-lookup"><span data-stu-id="a5e5d-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="a5e5d-229">Indexación y codificación de características categóricas</span><span class="sxs-lookup"><span data-stu-id="a5e5d-229">Index and encode categorical features</span></span>
* <span data-ttu-id="a5e5d-230">Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="a5e5d-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="a5e5d-231">Crear un muestreo aleatorio dentro de los datos de Hola y dividir en entrenamiento y conjuntos de pruebas</span><span class="sxs-lookup"><span data-stu-id="a5e5d-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="a5e5d-232">Ajuste de la escala de las características</span><span class="sxs-lookup"><span data-stu-id="a5e5d-232">Feature scaling</span></span>
* <span data-ttu-id="a5e5d-233">Almacenamiento de objetos en caché</span><span class="sxs-lookup"><span data-stu-id="a5e5d-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="a5e5d-234">Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico</span><span class="sxs-lookup"><span data-stu-id="a5e5d-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="a5e5d-235">Este código muestra cómo los depósitos de toocreate una nueva característica discretizando horas en vez de tráfico y, a continuación, cómo toocache Hola resultante trama de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="a5e5d-236">Cuando se utilicen repetidamente resistente distribuidas los conjuntos de datos (RDDs) y tramas de datos, el almacenamiento en caché conduce tooimproved los tiempos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="a5e5d-237">En consecuencia, se almacenará en caché RDDs y tramas de datos en varias fases de tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

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
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="a5e5d-238">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-238">**OUTPUT:**</span></span> 

<span data-ttu-id="a5e5d-239">126050</span><span class="sxs-lookup"><span data-stu-id="a5e5d-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="a5e5d-240">Indexación y codificación de características categóricas para la entrada en funciones de modelado</span><span class="sxs-lookup"><span data-stu-id="a5e5d-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="a5e5d-241">Esta sección se muestra cómo tooindex o codificar las características de categorías para la entrada en hello las funciones de modelado.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="a5e5d-242">Hola modelado y predecir las funciones de MLlib requieren características con los datos de entrada categorías toobe la indización o codifican toouse anterior.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="a5e5d-243">Según el modelo de hello, necesita tooindex o codificarlos de maneras diferentes:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="a5e5d-244">**Modelado basados en árbol** requiere toobe categorías codificado como valores numéricos (por ejemplo, una función con tres categorías puede codificarse con 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="a5e5d-245">Esto lo proporciona la función [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) de MLlib.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="a5e5d-246">Esta función codifica una columna de cadena de la columna de etiquetas de tooa de índices de etiqueta que se ordenan por frecuencias de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="a5e5d-247">Aunque indizada con valores numéricos de entrada y manipulación de datos, algoritmos de hello basados en árbol pueden ser tootreat especificado correctamente como categorías.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="a5e5d-248">**Modelos de regresión lineal y logística** requieren estrechamente con una codificación, donde, por ejemplo, una función con tres categorías se puede expandir en tres columnas de característica, cada contenedor 0 o 1 según la categoría de Hola de una observación.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="a5e5d-249">Proporciona MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) función toodo estrechamente con una codificación.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="a5e5d-250">Este codificador asigna una columna de la columna de etiqueta índices tooa de vectores binarios, con al menos un solo uno valor.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="a5e5d-251">Esta codificación permite algoritmos que esperan las características con valores numéricas, como la regresión logística, toobe aplica toocategorical características.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="a5e5d-252">Este es Hola código tooindex y codificar las características de categorías:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-252">Here is hello code tooindex and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-253">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-253">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-254">Tiempo que tarda tooexecute encima de la celda: 1,28 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="a5e5d-255">Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="a5e5d-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="a5e5d-256">Esta sección contiene código que muestra cómo tipo de datos de texto de categorías de tooindex como datos de un punto con la etiqueta y codifican, por lo que puede ser usado tootrain y prueba MLlib la regresión logística y otros modelos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="a5e5d-257">Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) con el formato de datos de entrada que necesita la mayoría de los algoritmos de aprendizaje automático de MLlib.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="a5e5d-258">Un [punto con etiqueta](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) es un vector local, denso o disperso, asociado con una etiqueta o respuesta.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="a5e5d-259">Esta sección contiene código que muestra cómo tooindex datos de texto por categorías como un [con la etiqueta punto](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) tipo de datos y codificar, por lo que puede ser usado tootrain y prueba MLlib la regresión logística y otros modelos de clasificación.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="a5e5d-260">Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) que constan de una etiqueta (variable destino/respuesta) y un vector de característica.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="a5e5d-261">Muchos algoritmos de aprendizaje automático de MLlib necesitan este formato de entrada.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="a5e5d-262">Este es Hola código tooindex y codificar las características de texto para clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="a5e5d-263">Este es el código de hello tooencode e índice características de texto de categorías para el análisis de regresión lineal.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="a5e5d-264">Crear un muestreo aleatorio dentro de los datos de Hola y dividir en entrenamiento y conjuntos de pruebas</span><span class="sxs-lookup"><span data-stu-id="a5e5d-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="a5e5d-265">Este código crea un muestreo aleatorio de datos de hello (25% se utiliza aquí).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="a5e5d-266">Aunque no es necesario para este ejemplo debido toohello tamaño del conjunto de datos de hello, demostraremos cómo puede muestrear aquí para saber cómo toouse para su propio problema cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="a5e5d-267">Cuando las muestras son grandes, esto puede ahorrar mucho tiempo al entrenar modelos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="a5e5d-268">A continuación, dividiremos ejemplo hello en una parte de entrenamiento (aquí 75%) y una prueba toouse parte (aquí 25%) en la clasificación y el modelo de regresión.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-269">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-269">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-270">Tiempo que tarda tooexecute encima de la celda: 0,24 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="a5e5d-271">Ajuste de la escala de las características</span><span class="sxs-lookup"><span data-stu-id="a5e5d-271">Feature scaling</span></span>
<span data-ttu-id="a5e5d-272">Ampliación de característica, también conocida como la normalización de datos, se garantiza que funciones con valores muy dispersos no se le otorgó excesivo sopesar en función del objetivo de hello.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="a5e5d-273">código para el escalado de la característica Hello usa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) varianza de tooscale Hola características toounit.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="a5e5d-274">MLlib lo proporciona para su uso en la regresión lineal con descenso de gradiente estocástico (SGD), un popular algoritmo para entrenar una amplia variedad de otros modelos de aprendizaje automático tales como regresiones regularizadas o máquinas de vectores de soporte (SVM).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="a5e5d-275">Hemos encontrado hello LinearRegressionWithSGD algoritmo toobe toofeature confidencial ajuste de escala.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="a5e5d-276">Aquí es tooscale variables de código de hello para su uso con un algoritmo SGD lineal Hola regularizado.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-277">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-277">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-278">Tiempo que tarda tooexecute encima de la celda: 13.17 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="a5e5d-279">Almacenamiento de objetos en caché</span><span class="sxs-lookup"><span data-stu-id="a5e5d-279">Cache objects in memory</span></span>
<span data-ttu-id="a5e5d-280">tiempo Hola para entrenamiento y prueba de algoritmos de aprendizaje automático pueden reducirse mediante objetos de marco de hello datos de entrada utilizados para la clasificación de regresión, el almacenamiento en caché y escalar características.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-281">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-281">**OUTPUT:**</span></span> 

<span data-ttu-id="a5e5d-282">Tiempo que tarda tooexecute encima de la celda: 0,15 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="a5e5d-283">Predicción de si se dio propina o no con modelos de clasificación binaria</span><span class="sxs-lookup"><span data-stu-id="a5e5d-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="a5e5d-284">Esta sección muestra cómo usar tres modelos para la tarea de clasificación binaria de hello de predecir si no se le paga una sugerencia para un recorrido de taxi.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="a5e5d-285">modelos de Hello presentados son:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-285">hello models presented are:</span></span>

* <span data-ttu-id="a5e5d-286">Regresión logística regularizada</span><span class="sxs-lookup"><span data-stu-id="a5e5d-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="a5e5d-287">Modelo de bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="a5e5d-287">Random forest model</span></span>
* <span data-ttu-id="a5e5d-288">Árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="a5e5d-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="a5e5d-289">Cada sección de código de generación del modelo se dividirá en pasos:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="a5e5d-290">**entrenamiento del modelo** con un conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="a5e5d-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="a5e5d-291">**Evaluación del modelo** en un conjunto de datos de prueba con métricas</span><span class="sxs-lookup"><span data-stu-id="a5e5d-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="a5e5d-292">**Guardado del modelo** en un blob para utilizarse en el futuro</span><span class="sxs-lookup"><span data-stu-id="a5e5d-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="a5e5d-293">Clasificación mediante regresión logística</span><span class="sxs-lookup"><span data-stu-id="a5e5d-293">Classification using logistic regression</span></span>
<span data-ttu-id="a5e5d-294">código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de regresión logística con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos dataset.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="a5e5d-295">**Entrenar el modelo de regresión logística de hello mediante CV y barrido hyperparameter**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="a5e5d-296">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-296">**OUTPUT:**</span></span> 

<span data-ttu-id="a5e5d-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="a5e5d-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="a5e5d-298">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="a5e5d-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="a5e5d-299">Tiempo que tarda tooexecute encima de la celda: 14.43 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="a5e5d-300">**Evaluar el modelo de clasificación binaria de hello con métricas estándares**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-300">**Evaluate hello binary classification model with standard metrics**</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="a5e5d-301">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-301">**OUTPUT:**</span></span> 

<span data-ttu-id="a5e5d-302">Area under PR = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="a5e5d-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="a5e5d-303">Area under ROC = 0.983714670256</span><span class="sxs-lookup"><span data-stu-id="a5e5d-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="a5e5d-304">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="a5e5d-304">Summary Stats</span></span>

<span data-ttu-id="a5e5d-305">Precision = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="a5e5d-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="a5e5d-306">Recall = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="a5e5d-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="a5e5d-307">F1 Score = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="a5e5d-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="a5e5d-308">Tiempo que tarda tooexecute encima de la celda: 57.61 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="a5e5d-309">**Trazar la curva ROC Hola.**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="a5e5d-310">Hola *predictionAndLabelsDF* está registrado como una tabla, *tmp_results*, en la celda anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="a5e5d-311">*tmp_results* pueden toodo usado consultas y generar resultados en hello sqlResults-trama de datos para trazar.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="a5e5d-312">Este es el código de hello.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="a5e5d-313">Aquí es predicciones de toomake de código de Hola y Hola trazado ROC curva.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="a5e5d-314">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="a5e5d-316">Clasificación de bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="a5e5d-316">Random forest classification</span></span>
<span data-ttu-id="a5e5d-317">código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de bosque aleatorio que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-318">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-318">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-319">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="a5e5d-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="a5e5d-320">Tiempo que tarda tooexecute encima de la celda: 31.09 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="a5e5d-321">Clasificación de árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="a5e5d-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="a5e5d-322">código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de árboles de aumento de degradado que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="a5e5d-323">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-323">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-324">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="a5e5d-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="a5e5d-325">Tiempo que tarda tooexecute encima de la celda: 19.76 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="a5e5d-326">Predicción de los importes de las propinas en las carreras de taxi con modelos de regresión</span><span class="sxs-lookup"><span data-stu-id="a5e5d-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="a5e5d-327">Esta sección muestra cómo utilizar tres modelos para la tarea de regresión de hello de predecir la cantidad de Hola de sugerencia de hello pagado por una taxi de ida y vuelta en función de otras características de sugerencia.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="a5e5d-328">modelos de Hello presentados son:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-328">hello models presented are:</span></span>

* <span data-ttu-id="a5e5d-329">Regresión lineal regularizada</span><span class="sxs-lookup"><span data-stu-id="a5e5d-329">Regularized linear regression</span></span>
* <span data-ttu-id="a5e5d-330">Bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="a5e5d-330">Random forest</span></span>
* <span data-ttu-id="a5e5d-331">Árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="a5e5d-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="a5e5d-332">Estos modelos se describen en la introducción de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-332">These models were described in hello introduction.</span></span> <span data-ttu-id="a5e5d-333">Cada sección de código de generación del modelo se dividirá en pasos:</span><span class="sxs-lookup"><span data-stu-id="a5e5d-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="a5e5d-334">**entrenamiento del modelo** con un conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="a5e5d-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="a5e5d-335">**Evaluación del modelo** en un conjunto de datos de prueba con métricas</span><span class="sxs-lookup"><span data-stu-id="a5e5d-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="a5e5d-336">**Guardado del modelo** en un blob para utilizarse en el futuro</span><span class="sxs-lookup"><span data-stu-id="a5e5d-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="a5e5d-337">regresión lineal con SGD</span><span class="sxs-lookup"><span data-stu-id="a5e5d-337">Linear regression with SGD</span></span>
<span data-ttu-id="a5e5d-338">Hello código en esta sección muestra cómo toouse escalarse características tootrain una regresión lineal que usa el descenso de gradiente estocástico (SGD) para la optimización, y cómo tooscore, evaluar y guardar el modelo de hello en el almacenamiento de blobs de Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="a5e5d-339">En nuestra experiencia, puede haber problemas con la convergencia de Hola de modelos LinearRegressionWithSGD y parámetros necesitan toobe cambiado/optimizado cuidadosamente para obtener un modelo válido.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="a5e5d-340">El ajuste de la escala de las variables ayuda con la convergencia.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-341">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-341">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="a5e5d-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="a5e5d-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="a5e5d-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="a5e5d-344">RMSE = 1.24190115863</span><span class="sxs-lookup"><span data-stu-id="a5e5d-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="a5e5d-345">R-sqr = 0.608017146081</span><span class="sxs-lookup"><span data-stu-id="a5e5d-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="a5e5d-346">Tiempo que tarda tooexecute encima de la celda: 58,42 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="a5e5d-347">Regresión con bosque aleatorio</span><span class="sxs-lookup"><span data-stu-id="a5e5d-347">Random Forest regression</span></span>
<span data-ttu-id="a5e5d-348">código de Hello en esta sección muestra cómo tootrain, evaluar y guardar una regresión de bosque aleatorio que predice la cantidad de sugerencia para hello datos de Nueva York taxi de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-349">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-349">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-350">RMSE = 0.891209218139</span><span class="sxs-lookup"><span data-stu-id="a5e5d-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="a5e5d-351">R-sqr = 0.759661334921</span><span class="sxs-lookup"><span data-stu-id="a5e5d-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="a5e5d-352">Tiempo que tarda tooexecute encima de la celda: 49.21 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="a5e5d-353">Regresión con árboles impulsados por gradiente</span><span class="sxs-lookup"><span data-stu-id="a5e5d-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="a5e5d-354">código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de árboles de aumento degradado que predice la cantidad de sugerencia para hello datos de Nueva York taxi de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="a5e5d-355">**Entrenamiento y evaluación**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-355">**Train and evaluate **</span></span>

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

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a5e5d-356">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-356">**OUTPUT:**</span></span>

<span data-ttu-id="a5e5d-357">RMSE = 0.908473148639</span><span class="sxs-lookup"><span data-stu-id="a5e5d-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="a5e5d-358">R-sqr = 0.753835096681</span><span class="sxs-lookup"><span data-stu-id="a5e5d-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="a5e5d-359">Tiempo que tarda tooexecute encima de la celda: 34.52 segundos</span><span class="sxs-lookup"><span data-stu-id="a5e5d-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="a5e5d-360">**Trazado**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-360">**Plot**</span></span>

<span data-ttu-id="a5e5d-361">*tmp_results* está registrado como una tabla de Hive en la celda anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="a5e5d-362">Resultados de tabla Hola son salidas en hello *sqlResults* trama de datos para trazar.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="a5e5d-363">Este es el código de hello</span><span class="sxs-lookup"><span data-stu-id="a5e5d-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="a5e5d-364">Aquí es Hola código tooplot Hola datos mediante servidor de Jupyter Hola.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="a5e5d-365">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="a5e5d-367">Limpieza de objetos de la memoria</span><span class="sxs-lookup"><span data-stu-id="a5e5d-367">Clean up objects from memory</span></span>
<span data-ttu-id="a5e5d-368">Use `unpersist()` objetos toodelete en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="a5e5d-369">Ubicaciones de almacenamiento de registro de los modelos de hello para el consumo y la puntuación</span><span class="sxs-lookup"><span data-stu-id="a5e5d-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="a5e5d-370">tooconsume y puntuación de un conjunto de datos independiente descrito en hello [puntuación y evalúe los modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md) tema, deberá toocopy y pegar estos archivos nombres que contienen modelos de hello guarda creados aquí en hello Bloc de notas de Jupyter de consumo.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="a5e5d-371">Aquí es tooprint de código de hello los archivos toomodel hello las rutas de acceso que necesita no existe.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="a5e5d-372">**SALIDA**</span><span class="sxs-lookup"><span data-stu-id="a5e5d-372">**OUTPUT**</span></span>

<span data-ttu-id="a5e5d-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="a5e5d-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="a5e5d-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="a5e5d-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="a5e5d-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="a5e5d-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="a5e5d-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="a5e5d-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="a5e5d-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="a5e5d-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="a5e5d-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="a5e5d-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="a5e5d-379">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5e5d-379">What's next?</span></span>
<span data-ttu-id="a5e5d-380">Ahora que ha creado los modelos de regresión y de clasificación con hello Spark MlLib, cómo está listo toolearn tooscore y evaluar estos modelos.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="a5e5d-381">Hola avanzada de exploración de datos y modelado más profunda, profundiza Bloc de notas en incluida la validación cruzada, parámetro de hyper-barrido y el modelo de evaluación.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="a5e5d-382">**Consumo de modelo:** toolearn cómo tooscore y evaluar modelos de clasificación y regresión de hello creados en este tema, consulte [puntuación y evaluar modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="a5e5d-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="a5e5d-383">**Validación cruzada y barrido de hiperparámetros**: consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) sobre cómo pueden prepararse los modelos con el barrido de hiperparámetros y la validación cruzada.</span><span class="sxs-lookup"><span data-stu-id="a5e5d-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

