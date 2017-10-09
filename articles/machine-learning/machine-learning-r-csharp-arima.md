---
title: "(En desuso) Previsión: media móvil integrada autorregresiva (ARIMA) - Azure | Microsoft Docs"
description: "(En desuso) Previsión: media móvil integrada autorregresiva (ARIMA)"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: 1e0d525f-8a9e-4b42-87e0-c9423f059f8c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 4f3af41fd8873fdf75c6426fd395351cb41db190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a><span data-ttu-id="28dd5-103">(En desuso) Previsión: media móvil integrada autorregresiva (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="28dd5-103">(deprecated) Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>

> [!NOTE]
> <span data-ttu-id="28dd5-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="28dd5-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="28dd5-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="28dd5-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="28dd5-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="28dd5-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>


<span data-ttu-id="28dd5-107">Esto [servicio](https://datamarket.azure.com/dataset/aml_labs/arima) implementa predicciones de tooproduce de regresión automática integrada mover promedio (ARIMA) basadas en datos históricos de hello proporcionados por usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="28dd5-107">This [service](https://datamarket.azure.com/dataset/aml_labs/arima) implements Autoregressive Integrated Moving Average (ARIMA) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="28dd5-108">¿Hola a petición para un aumento de productos específica este año?</span><span class="sxs-lookup"><span data-stu-id="28dd5-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="28dd5-109">¿Predecir Mis ventas de producto para hello Navidad, para que puedo planear eficazmente mi inventario?</span><span class="sxs-lookup"><span data-stu-id="28dd5-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="28dd5-110">Modelos de predicción son tooaddress apt esas preguntas.</span><span class="sxs-lookup"><span data-stu-id="28dd5-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="28dd5-111">Dados hello más allá de los datos, estos modelos examinan tendencias ocultas y las tendencias futuras estacionalidad toopredict.</span><span class="sxs-lookup"><span data-stu-id="28dd5-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="28dd5-112">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="28dd5-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="28dd5-113">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="28dd5-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="28dd5-114">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="28dd5-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="28dd5-115">servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="28dd5-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="28dd5-116">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="28dd5-116">Consumption of web service</span></span>
<span data-ttu-id="28dd5-117">Este servicio acepta 4 argumentos y calcula las previsiones de hello ARIMA.</span><span class="sxs-lookup"><span data-stu-id="28dd5-117">This service accepts 4 arguments and calculates hello ARIMA forecasts.</span></span>
<span data-ttu-id="28dd5-118">argumentos de entrada de Hello son:</span><span class="sxs-lookup"><span data-stu-id="28dd5-118">hello input arguments are:</span></span>

* <span data-ttu-id="28dd5-119">Frecuencia: indica la frecuencia de Hola de datos sin procesar de hello (diaria/semanal/mensual o trimestral/anual).</span><span class="sxs-lookup"><span data-stu-id="28dd5-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="28dd5-120">Horizonte: intervalo de tiempo de previsión del futuro.</span><span class="sxs-lookup"><span data-stu-id="28dd5-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="28dd5-121">Fecha: agregar datos de la serie temporal de la nueva Hola por vez.</span><span class="sxs-lookup"><span data-stu-id="28dd5-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="28dd5-122">Valor: agregar en valores de datos en la serie de tiempo de hello nueva.</span><span class="sxs-lookup"><span data-stu-id="28dd5-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="28dd5-123">salida de Hello del servicio de hello es Hola calcula valores pronosticados.</span><span class="sxs-lookup"><span data-stu-id="28dd5-123">hello output of hello service is hello calculated forecast values.</span></span> 

<span data-ttu-id="28dd5-124">La entrada de ejemplo podría ser:</span><span class="sxs-lookup"><span data-stu-id="28dd5-124">Sample input could be:</span></span> 

* <span data-ttu-id="28dd5-125">Frecuencia: 12</span><span class="sxs-lookup"><span data-stu-id="28dd5-125">Frequency - 12</span></span>
* <span data-ttu-id="28dd5-126">Horizonte: 12</span><span class="sxs-lookup"><span data-stu-id="28dd5-126">Horizon - 12</span></span>
* <span data-ttu-id="28dd5-127">Fecha: 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="28dd5-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="28dd5-128">Valor: 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="28dd5-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="28dd5-129">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="28dd5-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="28dd5-130">Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="28dd5-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="28dd5-131">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="28dd5-131">Starting C# code for web service consumption:</span></span>
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
          var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri =  "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";

          var httpClient = new HttpClient();
           httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere","ChangeToAPIKey");
           httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
          var query = httpClient.PostAsync(acitionUri,new StringContent(json));
          var result = query.Result.Content;
          var scoreResult = result.ReadAsStringAsync().Result;
      }

## <a name="creation-of-web-service"></a><span data-ttu-id="28dd5-132">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="28dd5-132">Creation of web service</span></span>
> <span data-ttu-id="28dd5-133">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="28dd5-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="28dd5-134">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="28dd5-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="28dd5-135">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="28dd5-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="28dd5-136">Desde el Aprendizaje automático de Azure, se creó un nuevo experimento en blanco.</span><span class="sxs-lookup"><span data-stu-id="28dd5-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="28dd5-137">Se cargaron datos de entrada de muestra con un esquema de datos predefinido.</span><span class="sxs-lookup"><span data-stu-id="28dd5-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="28dd5-138">Esquema de datos de toohello vinculado es un [ejecutar Script de R] [ execute-r-script] módulo, que se genera el modelo de pronóstico Hola ARIMA mediante 'auto.arima' y 'previsión' funciones de R.</span><span class="sxs-lookup"><span data-stu-id="28dd5-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module, which generates hello ARIMA forecasting model by using ‘auto.arima’ and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="28dd5-139">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="28dd5-139">Experiment flow:</span></span>
![Creación del espacio de trabajo][2]

#### <a name="module-1"></a><span data-ttu-id="28dd5-141">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="28dd5-141">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Creación del espacio de trabajo][3]    

#### <a name="module-2"></a><span data-ttu-id="28dd5-143">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="28dd5-143">Module 2:</span></span>
    # data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- auto.arima(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # produce forecasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="28dd5-144">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="28dd5-144">Limitations</span></span>
<span data-ttu-id="28dd5-145">Este es un ejemplo muy sencillo de previsión de ARIMA.</span><span class="sxs-lookup"><span data-stu-id="28dd5-145">This is a very simple example for ARIMA forecasting.</span></span> <span data-ttu-id="28dd5-146">Como se puede ver desde el código de ejemplo de Hola anterior, realizar capturas de errores no se implementan y servicio Hola se supone que todas las variables de hello son valores continuos/positive y frecuencia de hello debe ser un entero mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="28dd5-146">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="28dd5-147">longitud de Hola de vectores de valor de fecha y de Hola se debería Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="28dd5-147">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="28dd5-148">variable de fecha Hola debe respetar toohello formato "mm/dd/aaaa'.</span><span class="sxs-lookup"><span data-stu-id="28dd5-148">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="28dd5-149">P+F</span><span class="sxs-lookup"><span data-stu-id="28dd5-149">FAQ</span></span>
<span data-ttu-id="28dd5-150">Para las preguntas más frecuentes en el consumo del servicio web de Hola o toomarketplace de publicación, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="28dd5-150">For frequently asked questions on consumption of hello web service or publishing toomarketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

