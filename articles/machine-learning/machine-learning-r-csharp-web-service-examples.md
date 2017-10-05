---
title: (en desuso) Ejemplos de servicios web Machine Learning creados con R - Azure | Microsoft Docs
description: "(en desuso) Encuentre un útil conjunto de ejemplos de servicios creados con código R y Machine Learning y publicados en Azure Marketplace."
keywords: "csharp, código r, ejemplos de servicios web"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="3b720-104">(en desuso) Ejemplos de servicios web con R en Azure Machine Learning y publicados en Microsoft Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="3b720-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="3b720-105">Microsoft DataMarket está en proceso de retirada y estas API están en desuso.</span><span class="sxs-lookup"><span data-stu-id="3b720-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="3b720-106">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3b720-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3b720-107">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3b720-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3b720-108">En este artículo se crearon servicios web de ejemplo mediante Aprendizaje automático de Azure y se publicaron en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3b720-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="3b720-109">Cada ejemplo de servicio web tiene un documento exhaustivo asociado, donde se integran conjuntos de datos de ejemplo para probar los servicios y se explica cómo el usuario puede crear un servicio similar.</span><span class="sxs-lookup"><span data-stu-id="3b720-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="3b720-110">Con Estudio de aprendizaje automático de Azure, los usuarios pueden escribir código de R y, con tan solo hacer algunos clics, publicarlo como un servicio web para que lo consuman aplicaciones y dispositivos en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="3b720-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="3b720-111">Desde la producción de calculadoras sencillas que proporcionan funcionalidad estadística hasta la creación de un previsor de análisis de opiniones para la minería de texto personalizado, los usuarios noveles y profesionales de R pueden beneficiarse de la facilidad con que los usuarios de Aprendizaje automático de Azure pueden aplicar el código R.</span><span class="sxs-lookup"><span data-stu-id="3b720-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="3b720-112">Si bien estos servicios web podrían haberlos consumido los usuarios, posiblemente a través de una aplicación móvil o un sitio web, su propósito es mostrar el modo en que Aprendizaje automático puede aplicar scripts de R para fines analíticos y usarlos para crear servicios web basados en código R.</span><span class="sxs-lookup"><span data-stu-id="3b720-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="3b720-113">Cada ejemplo incluye un ejemplo de C# para el consumo de servicios web.</span><span class="sxs-lookup"><span data-stu-id="3b720-113">Each example includes a C# example for web service consumption.</span></span>

![Diagrama de código de R en Aprendizaje automático de Azure: soluciones de R para uso propietario o publicado en Azure Marketplace.][1]

<span data-ttu-id="3b720-115">Considere los siguientes escenarios.</span><span class="sxs-lookup"><span data-stu-id="3b720-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="3b720-116">Escenario 1: modelo genérico</span><span class="sxs-lookup"><span data-stu-id="3b720-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="3b720-117">Un usuario trabaja con un modelo genérico que se puede aplicar a los datos de un nuevo usuario, como una previsión básica de datos de serie temporal o un método de R personalizado e integrado con análisis avanzado.</span><span class="sxs-lookup"><span data-stu-id="3b720-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="3b720-118">Este usuario publica el modelo como un servicio web para que otros usuarios puedan utilizar sus datos.</span><span class="sxs-lookup"><span data-stu-id="3b720-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="3b720-119">Clasificador binario</span><span class="sxs-lookup"><span data-stu-id="3b720-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="3b720-120">Modelo de clúster</span><span class="sxs-lookup"><span data-stu-id="3b720-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="3b720-121">Regresión lineal multivariada</span><span class="sxs-lookup"><span data-stu-id="3b720-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="3b720-122">Previsión: suavizado exponencial</span><span class="sxs-lookup"><span data-stu-id="3b720-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="3b720-123">Previsión con ETS + STL</span><span class="sxs-lookup"><span data-stu-id="3b720-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="3b720-124">Previsión - Media móvil integrada autorregresiva (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="3b720-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="3b720-125">Análisis de supervivencia</span><span class="sxs-lookup"><span data-stu-id="3b720-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="3b720-126">Escenario 2: modelo entrenado - datos específicos</span><span class="sxs-lookup"><span data-stu-id="3b720-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="3b720-127">Un usuario tiene datos que proporcionan útiles predicciones a través del código R, como un ejemplo grande de cuestionarios de personalidad agrupados mediante un algoritmo k-means para predecir el tipo de personalidad del usuario o los datos de encuestas de salud que pueden utilizarse para predecir el riesgo de que un individuo padezca cáncer de pulmón mediante un paquete de análisis de supervivencia basado en R.</span><span class="sxs-lookup"><span data-stu-id="3b720-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="3b720-128">El usuario publica los datos a través de un servicio web que predice el resultado del nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="3b720-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="3b720-129">Escenario 3: modelo entrenado - datos genéricos</span><span class="sxs-lookup"><span data-stu-id="3b720-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="3b720-130">Un usuario tiene datos genéricos (por ejemplo, un conjunto de texto) que permiten crear y aplicar de manera general un servicio web en diferentes tipos de escenarios y casos de uso.</span><span class="sxs-lookup"><span data-stu-id="3b720-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="3b720-131">Análisis de opiniones basado en léxico</span><span class="sxs-lookup"><span data-stu-id="3b720-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="3b720-132">Escenario 4: calculadora avanzada</span><span class="sxs-lookup"><span data-stu-id="3b720-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="3b720-133">Un usuario proporciona cálculos avanzados o simulaciones, que no requieren ningún modelo entrenado o ajuste de un modelo a los datos del usuario.</span><span class="sxs-lookup"><span data-stu-id="3b720-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="3b720-134">Diferencia en la prueba de proporciones</span><span class="sxs-lookup"><span data-stu-id="3b720-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="3b720-135">Conjunto de distribución normal</span><span class="sxs-lookup"><span data-stu-id="3b720-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="3b720-136">Conjunto de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="3b720-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="3b720-137">P+F</span><span class="sxs-lookup"><span data-stu-id="3b720-137">FAQ</span></span>
<span data-ttu-id="3b720-138">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3b720-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



