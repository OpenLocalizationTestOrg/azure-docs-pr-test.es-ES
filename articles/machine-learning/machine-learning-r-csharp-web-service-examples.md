---
title: "ejemplos que se generan con R - Azure de los servicios web de aprendizaje de máquina AAA(deprecated) | Documentos de Microsoft"
description: "(desusado) Busque un conjunto útil de ejemplos de servicios web creados con código de R y aprendizaje automático y publica toohello Azure Marketplace."
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
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="83ca1-104">(desusado) Ejemplos que utilizan código R en aprendizaje automático de Azure y Azure Marketplace de tooMicrosoft publicado los servicios Web</span><span class="sxs-lookup"><span data-stu-id="83ca1-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="83ca1-105">Hola Microsoft DataMarket se ha retirado y estas API han quedado en desuso.</span><span class="sxs-lookup"><span data-stu-id="83ca1-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="83ca1-106">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="83ca1-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="83ca1-107">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="83ca1-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="83ca1-108">En este artículo son web de ejemplo, los servicios creados con aprendizaje automático de Azure y publicar toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="83ca1-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="83ca1-109">Cada ejemplo de servicio web tiene un solo documento completo adjunto, incrustar los conjuntos de datos de ejemplo para probar los servicios de Hola y explicar cómo Hola usuario puede crear un servicio similar a sí mismos.</span><span class="sxs-lookup"><span data-stu-id="83ca1-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="83ca1-110">En estudio de aprendizaje automático de Azure, los usuarios pueden escribir código en R y con unos pocos clics, publicarlo como un servicio web para aplicaciones y dispositivos tooconsume alrededor de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="83ca1-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="83ca1-111">Desde produciendo calculadoras simples que proporcionan funcionalidad estadística toocreating un elemento de predicción de análisis de opiniones de minería de texto personalizado, los usuarios de R nuevos y experimentados pueden beneficiarse de facilidad Hola con la que los usuarios de aprendizaje automático de Azure pueden poner R código.</span><span class="sxs-lookup"><span data-stu-id="83ca1-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="83ca1-112">Mientras que los usuarios, posiblemente a través de una aplicación móvil o un sitio Web, estos servicios web que pueden consumir propósito Hola de estos ejemplos es tooshow cómo puede comenzar el aprendizaje automático de los servicios web R secuencias de comandos con fines analíticos y estar toocreate usa servicios web en parte superior del código R.</span><span class="sxs-lookup"><span data-stu-id="83ca1-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="83ca1-113">Cada ejemplo incluye un ejemplo de C# para el consumo de servicios web.</span><span class="sxs-lookup"><span data-stu-id="83ca1-113">Each example includes a C# example for web service consumption.</span></span>

![Diagrama de código de R en aprendizaje automático de Azure: soluciones de R para uso propio o publicado toohello Azure Marketplace.][1]

<span data-ttu-id="83ca1-115">Considere la posibilidad de hello los escenarios siguientes.</span><span class="sxs-lookup"><span data-stu-id="83ca1-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="83ca1-116">Escenario 1: modelo genérico</span><span class="sxs-lookup"><span data-stu-id="83ca1-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="83ca1-117">Un usuario trabaja con un modelo genérico que puede ser datos del nuevo usuario de tooa aplicado, como un pronóstico básica de datos de serie temporal o un método de R personalizado con análisis avanzado.</span><span class="sxs-lookup"><span data-stu-id="83ca1-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="83ca1-118">Este usuario publica hello tooconsume con sus datos de modelo como un servicio web para que otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="83ca1-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="83ca1-119">Clasificador binario</span><span class="sxs-lookup"><span data-stu-id="83ca1-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="83ca1-120">Modelo de clúster</span><span class="sxs-lookup"><span data-stu-id="83ca1-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="83ca1-121">Regresión lineal multivariada</span><span class="sxs-lookup"><span data-stu-id="83ca1-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="83ca1-122">Previsión: suavizado exponencial</span><span class="sxs-lookup"><span data-stu-id="83ca1-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="83ca1-123">Previsión con ETS + STL</span><span class="sxs-lookup"><span data-stu-id="83ca1-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="83ca1-124">Previsión - Media móvil integrada autorregresiva (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="83ca1-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="83ca1-125">Análisis de supervivencia</span><span class="sxs-lookup"><span data-stu-id="83ca1-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="83ca1-126">Escenario 2: modelo entrenado - datos específicos</span><span class="sxs-lookup"><span data-stu-id="83ca1-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="83ca1-127">Un usuario tiene datos que proporciona predicciones útiles a través del código de R, como un ejemplo de los cuestionarios de personalidad grande en clúster mediante el tipo de la personalidad de k-means algoritmo toopredict Hola de un usuario o mantenimiento de datos que pueden ser utilizado toopredict la encuesta de un individuo riesgo de cáncer pulmonar con un paquete de R de análisis de supervivencia.</span><span class="sxs-lookup"><span data-stu-id="83ca1-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="83ca1-128">usuario de Hello publica datos Hola a través de un servicio web que predice el resultado de un usuario nuevo.</span><span class="sxs-lookup"><span data-stu-id="83ca1-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="83ca1-129">Escenario 3: modelo entrenado - datos genéricos</span><span class="sxs-lookup"><span data-stu-id="83ca1-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="83ca1-130">Un usuario tiene datos genéricos (por ejemplo, un corpus de texto) que permite un toobe de servicio web creado y aplicar genéricamente a través de diferentes tipos de casos de uso y escenarios.</span><span class="sxs-lookup"><span data-stu-id="83ca1-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="83ca1-131">Análisis de opiniones basado en léxico</span><span class="sxs-lookup"><span data-stu-id="83ca1-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="83ca1-132">Escenario 4: calculadora avanzada</span><span class="sxs-lookup"><span data-stu-id="83ca1-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="83ca1-133">Un usuario proporciona cálculos avanzados o simulaciones que no requieren ningún modelo entrenado o conexión de datos de un usuario de toohello de modelo.</span><span class="sxs-lookup"><span data-stu-id="83ca1-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="83ca1-134">Diferencia en la prueba de proporciones</span><span class="sxs-lookup"><span data-stu-id="83ca1-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="83ca1-135">Conjunto de distribución normal</span><span class="sxs-lookup"><span data-stu-id="83ca1-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="83ca1-136">Conjunto de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="83ca1-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="83ca1-137">P+F</span><span class="sxs-lookup"><span data-stu-id="83ca1-137">FAQ</span></span>
<span data-ttu-id="83ca1-138">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="83ca1-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



