---
title: "(obsoleto) Previsión: ETS + STL - Azure | Microsoft Docs"
description: "(obsoleto) Previsión: ETS + STL"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a575af931a41b7a55eb2102f3553640a16099146
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---ets--stl"></a><span data-ttu-id="f4d69-103">(obsoleto) Previsión: ETS + STL</span><span class="sxs-lookup"><span data-stu-id="f4d69-103">(deprecated) Forecasting - ETS + STL</span></span>

> [!NOTE]
> <span data-ttu-id="f4d69-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="f4d69-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="f4d69-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f4d69-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f4d69-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f4d69-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f4d69-107">Este [servicio web](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implementa la descomposición de tendencias estacionales (STL) y el modelo de suavizado exponencial (ETS) para generar previsiones basadas en datos históricos facilitados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="f4d69-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implements Seasonal Trend Decomposition (STL) and Exponential Smoothing (ETS) models to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="f4d69-108">¿Aumentará la demanda de un producto específico este año?</span><span class="sxs-lookup"><span data-stu-id="f4d69-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="f4d69-109">¿Puedo prever las ventas de productos para la temporada navideña, a fin de poder planear el inventario con eficacia?</span><span class="sxs-lookup"><span data-stu-id="f4d69-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="f4d69-110">Los modelos de previsión suelen abordar estas cuestiones.</span><span class="sxs-lookup"><span data-stu-id="f4d69-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="f4d69-111">Conforme a los datos anteriores, estos modelos examinan las tendencias ocultas y la estacionalidad para prever futuras tendencias.</span><span class="sxs-lookup"><span data-stu-id="f4d69-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="f4d69-112">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f4d69-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="f4d69-113">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="f4d69-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="f4d69-114">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="f4d69-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="f4d69-115">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="f4d69-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="f4d69-116">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="f4d69-116">Consumption of web service</span></span>
<span data-ttu-id="f4d69-117">Este servicio acepta 4 argumentos y calcula las previsiones.</span><span class="sxs-lookup"><span data-stu-id="f4d69-117">This service accepts 4 arguments and calculates the forecasts.</span></span>
<span data-ttu-id="f4d69-118">Los argumentos de entrada son:</span><span class="sxs-lookup"><span data-stu-id="f4d69-118">The input arguments are:</span></span>

* <span data-ttu-id="f4d69-119">Frecuencia: indica la frecuencia de los datos sin procesar (diaria/semanal/mensual/trimestral/anual)</span><span class="sxs-lookup"><span data-stu-id="f4d69-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="f4d69-120">Horizonte: intervalo de tiempo de previsión del futuro.</span><span class="sxs-lookup"><span data-stu-id="f4d69-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="f4d69-121">Fechas: permite agregar los nuevos datos de la serie temporal para el tiempo.</span><span class="sxs-lookup"><span data-stu-id="f4d69-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="f4d69-122">Valor: permite agregar los nuevos valores de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="f4d69-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="f4d69-123">La salida del servicio se corresponde con los valores de previsión calculados.</span><span class="sxs-lookup"><span data-stu-id="f4d69-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="f4d69-124">La entrada de ejemplo podría ser:</span><span class="sxs-lookup"><span data-stu-id="f4d69-124">Sample input could be:</span></span> 

* <span data-ttu-id="f4d69-125">Frecuencia: 12</span><span class="sxs-lookup"><span data-stu-id="f4d69-125">Frequency - 12</span></span>
* <span data-ttu-id="f4d69-126">Horizonte: 12</span><span class="sxs-lookup"><span data-stu-id="f4d69-126">Horizon - 12</span></span>
* <span data-ttu-id="f4d69-127">Fecha: 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="f4d69-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="f4d69-128">Valor: 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="f4d69-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="f4d69-129">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="f4d69-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="f4d69-130">Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)se puede ver una aplicación de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="f4d69-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="f4d69-131">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="f4d69-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="f4d69-132">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="f4d69-132">Creation of web service</span></span>
> <span data-ttu-id="f4d69-133">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4d69-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="f4d69-134">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="f4d69-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="f4d69-135">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="f4d69-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="f4d69-136">Desde el Aprendizaje automático de Azure, se creó un nuevo experimento en blanco.</span><span class="sxs-lookup"><span data-stu-id="f4d69-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="f4d69-137">Se cargaron datos de entrada de muestra con un esquema de datos predefinido.</span><span class="sxs-lookup"><span data-stu-id="f4d69-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="f4d69-138">Vinculado al esquema de datos hay un módulo [Ejecutar scripts R][execute-r-script] que genera el modelo de previsión STL y ETS mediante las funciones "auto.arima" y "previsión" de R.</span><span class="sxs-lookup"><span data-stu-id="f4d69-138">Linked to the data schema is an [Execute R Script][execute-r-script] module, which generates STL and ETS forecasting models by using ‘stl’, ‘ets’, and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="f4d69-139">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="f4d69-139">Experiment flow:</span></span>
![Flujo de experimento][2]

#### <a name="module-1"></a><span data-ttu-id="f4d69-141">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="f4d69-141">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Datos de ejemplo][3]    

#### <a name="module-2"></a><span data-ttu-id="f4d69-143">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="f4d69-143">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a><span data-ttu-id="f4d69-144">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="f4d69-144">Limitations</span></span>
<span data-ttu-id="f4d69-145">Este es un ejemplo muy sencillo de previsión de ETS+STL.</span><span class="sxs-lookup"><span data-stu-id="f4d69-145">This is a very simple example for ETS + STL forecasting.</span></span> <span data-ttu-id="f4d69-146">Como puede verse en el código de ejemplo anterior, no se implementa ninguna detección de errores y el servicio asume que todas las variables son valores continuos/positivos y la frecuencia debe ser un entero mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="f4d69-146">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="f4d69-147">La longitud de los vectores de fecha y valor debe ser la misma, y la longitud de la serie temporal debe ser superior a 2*frecuencia.</span><span class="sxs-lookup"><span data-stu-id="f4d69-147">The length of the date and value vectors should be the same, and the length of the time series should be greater than 2*frequency.</span></span> <span data-ttu-id="f4d69-148">La variable de fecha debe respetar el formato "dd/mm/aaaa".</span><span class="sxs-lookup"><span data-stu-id="f4d69-148">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="f4d69-149">P+F</span><span class="sxs-lookup"><span data-stu-id="f4d69-149">FAQ</span></span>
<span data-ttu-id="f4d69-150">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f4d69-150">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

