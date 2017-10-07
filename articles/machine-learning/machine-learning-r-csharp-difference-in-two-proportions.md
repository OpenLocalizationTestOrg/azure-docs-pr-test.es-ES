---
title: aaa(deprecated) diferencia en proporciones prueba - Azure | Documentos de Microsoft
description: (obsoleto) Diferencia en la prueba de proporciones
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="a73c0-103">(obsoleto) Diferencia en la prueba de proporciones</span><span class="sxs-lookup"><span data-stu-id="a73c0-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="a73c0-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="a73c0-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="a73c0-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="a73c0-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="a73c0-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="a73c0-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="a73c0-107">¿Las dos proporciones son diferentes desde el punto de vista estadístico?</span><span class="sxs-lookup"><span data-stu-id="a73c0-107">Are two proportions statistically different?</span></span> <span data-ttu-id="a73c0-108">Suponga que un usuario desea toocompare dos películas toodetermine si una película tiene una proporción significativamente superior del 'le gusta' cuando compara toohello otro.</span><span class="sxs-lookup"><span data-stu-id="a73c0-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="a73c0-109">Con un ejemplo de gran tamaño, podría haber una diferencia significativa estadísticamente entre las proporciones Hola 0,50 y 0,51.</span><span class="sxs-lookup"><span data-stu-id="a73c0-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="a73c0-110">Con una pequeña muestra, que no haya suficiente toodetermine datos si estas proporciones son realmente diferentes.</span><span class="sxs-lookup"><span data-stu-id="a73c0-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="a73c0-111">Esto [servicio web](https://datamarket.azure.com/dataset/aml_labs/prop_test) lleva a cabo una prueba de la hipótesis de diferencia de hello en dos proporciones basadas en la entrada de usuario de número de Hola de operaciones correctas y Hola el número total de pruebas para los grupos de comparación de hello 2.</span><span class="sxs-lookup"><span data-stu-id="a73c0-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="a73c0-112">En un escenario posible, este servicio web podría invocarse desde dentro de una aplicación de comparación de película, indicando que el usuario de hello si uno de películas de hello es 'gustó' con más frecuencia que Hola otro, en función de las clasificaciones de películas.</span><span class="sxs-lookup"><span data-stu-id="a73c0-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="a73c0-113">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a73c0-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="a73c0-114">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="a73c0-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="a73c0-115">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="a73c0-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="a73c0-116">servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="a73c0-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="a73c0-117">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="a73c0-117">Consumption of web service</span></span>
<span data-ttu-id="a73c0-118">Este servicio acepta 4 argumentos y realiza una prueba hipotética de las proporciones.</span><span class="sxs-lookup"><span data-stu-id="a73c0-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="a73c0-119">argumentos de entrada de Hello son:</span><span class="sxs-lookup"><span data-stu-id="a73c0-119">hello input arguments are:</span></span>

* <span data-ttu-id="a73c0-120">Éxitos1: número de eventos de éxito del ejemplo 1.</span><span class="sxs-lookup"><span data-stu-id="a73c0-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="a73c0-121">Éxitos2: número de eventos de éxito del ejemplo 2.</span><span class="sxs-lookup"><span data-stu-id="a73c0-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="a73c0-122">Total1: tamaño de la muestra 1.</span><span class="sxs-lookup"><span data-stu-id="a73c0-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="a73c0-123">Total2: tamaño de la muestra 2.</span><span class="sxs-lookup"><span data-stu-id="a73c0-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="a73c0-124">salida de Hello del servicio de hello es resultado de hello de hipótesis Hola probar junto con hello chi-square estadística, df, p-valor y proporción en los límites del ejemplo 1/2 y el intervalo de confianza.</span><span class="sxs-lookup"><span data-stu-id="a73c0-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="a73c0-125">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="a73c0-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="a73c0-126">Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a73c0-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="a73c0-127">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="a73c0-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="a73c0-128">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="a73c0-128">Creation of web service</span></span>
> <span data-ttu-id="a73c0-129">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="a73c0-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="a73c0-130">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="a73c0-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="a73c0-131">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a73c0-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="a73c0-132">En Azure Machine Learning, se creó un nuevo experimento en blanco con dos módulos [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a73c0-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="a73c0-133">En el primer módulo de hello esquema de datos de Hola se define, mientras que segundo módulo de hello utiliza comandos de prop.test de hello en pruebas de hipótesis de R tooperform Hola para 2 proporciones.</span><span class="sxs-lookup"><span data-stu-id="a73c0-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="a73c0-134">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="a73c0-134">Experiment flow:</span></span>
![Flujo de experimento][2]

#### <a name="module-1"></a><span data-ttu-id="a73c0-136">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="a73c0-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="a73c0-137">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="a73c0-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="a73c0-138">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="a73c0-138">Limitations</span></span>
<span data-ttu-id="a73c0-139">Se trata de un ejemplo muy sencillo para probar las diferencias entre dos proporciones.</span><span class="sxs-lookup"><span data-stu-id="a73c0-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="a73c0-140">Como se puede ver desde el código de ejemplo de Hola anterior, no se implementa la ningún error que detecte y servicio Hola se da por supuesto que todas las variables de hello son continuas.</span><span class="sxs-lookup"><span data-stu-id="a73c0-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="a73c0-141">P+F</span><span class="sxs-lookup"><span data-stu-id="a73c0-141">FAQ</span></span>
<span data-ttu-id="a73c0-142">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a73c0-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

