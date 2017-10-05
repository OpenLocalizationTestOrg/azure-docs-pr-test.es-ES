---
title: (obsoleto) Diferencia en la prueba de proporciones - Azure | Microsoft Docs
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
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="94d9b-103">(obsoleto) Diferencia en la prueba de proporciones</span><span class="sxs-lookup"><span data-stu-id="94d9b-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="94d9b-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="94d9b-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="94d9b-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="94d9b-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="94d9b-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="94d9b-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="94d9b-107">¿Las dos proporciones son diferentes desde el punto de vista estadístico?</span><span class="sxs-lookup"><span data-stu-id="94d9b-107">Are two proportions statistically different?</span></span> <span data-ttu-id="94d9b-108">Supongamos que un usuario desea comparar dos películas para determinar si una película tiene una mayor proporción de "me gusta" en comparación con la otra.</span><span class="sxs-lookup"><span data-stu-id="94d9b-108">Suppose a user wants to compare two movies to determine if one movie has a significantly higher proportion of ‘likes’ when compared to the other.</span></span> <span data-ttu-id="94d9b-109">Con un ejemplo grande, podría haber una diferencia significativa estadísticamente entre las proporciones 0,50 y 0,51.</span><span class="sxs-lookup"><span data-stu-id="94d9b-109">With a large sample, there could be a statistically significant difference between the proportions 0.50 and 0.51.</span></span> <span data-ttu-id="94d9b-110">Con un ejemplo pequeño, es posible que no haya suficientes datos para determinar si estas proporciones son realmente diferentes.</span><span class="sxs-lookup"><span data-stu-id="94d9b-110">With a small sample, there may not be enough data to determine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="94d9b-111">Este [servicio web](https://datamarket.azure.com/dataset/aml_labs/prop_test) realiza una prueba hipotética de la diferencia entre las dos proporciones basada en la entrada del usuario del número de éxitos y del número total de pruebas para los dos grupos objeto de comparación.</span><span class="sxs-lookup"><span data-stu-id="94d9b-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of the difference in two proportions based on user input of the number of successes and the total number of trials for the 2 comparison groups.</span></span> <span data-ttu-id="94d9b-112">En un posible escenario, este servicio web podría invocarse desde dentro de una aplicación de comparación de películas, que indica al usuario, si una de las películas realmente "gustó" con más frecuencia que la otra, basado en las clasificaciones de películas.</span><span class="sxs-lookup"><span data-stu-id="94d9b-112">In one possible scenario, this web service could be called from within a movie comparison app, telling the user whether one of the movies is really ‘liked’ more often than the other, based on movie ratings.</span></span>

> <span data-ttu-id="94d9b-113">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="94d9b-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="94d9b-114">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="94d9b-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="94d9b-115">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="94d9b-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="94d9b-116">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="94d9b-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="94d9b-117">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="94d9b-117">Consumption of web service</span></span>
<span data-ttu-id="94d9b-118">Este servicio acepta 4 argumentos y realiza una prueba hipotética de las proporciones.</span><span class="sxs-lookup"><span data-stu-id="94d9b-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="94d9b-119">Los argumentos de entrada son:</span><span class="sxs-lookup"><span data-stu-id="94d9b-119">The input arguments are:</span></span>

* <span data-ttu-id="94d9b-120">Éxitos1: número de eventos de éxito del ejemplo 1.</span><span class="sxs-lookup"><span data-stu-id="94d9b-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="94d9b-121">Éxitos2: número de eventos de éxito del ejemplo 2.</span><span class="sxs-lookup"><span data-stu-id="94d9b-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="94d9b-122">Total1: tamaño de la muestra 1.</span><span class="sxs-lookup"><span data-stu-id="94d9b-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="94d9b-123">Total2: tamaño de la muestra 2.</span><span class="sxs-lookup"><span data-stu-id="94d9b-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="94d9b-124">La salida del servicio es el resultado de la prueba hipotética junto con la prueba estadística de Chi cuadrado, el valor df, el valor p y la proporción del ejemplo 1 y 2 y los límites del intervalo de confianza.</span><span class="sxs-lookup"><span data-stu-id="94d9b-124">The output of the service is the result of the hypothesis test along with the chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="94d9b-125">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="94d9b-125">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="94d9b-126">Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)se puede ver una aplicación de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="94d9b-126">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="94d9b-127">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="94d9b-127">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="94d9b-128">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="94d9b-128">Creation of web service</span></span>
> <span data-ttu-id="94d9b-129">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="94d9b-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="94d9b-130">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="94d9b-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="94d9b-131">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="94d9b-131">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="94d9b-132">En Azure Machine Learning, se creó un nuevo experimento en blanco con dos módulos [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="94d9b-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="94d9b-133">En el primer módulo se define el esquema de datos, mientras que el segundo módulo utiliza el comando prop.test en R para realizar la prueba hipotética para dos proporciones.</span><span class="sxs-lookup"><span data-stu-id="94d9b-133">In the first module the data schema is defined, while the second module uses the prop.test command within R to perform the hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="94d9b-134">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="94d9b-134">Experiment flow:</span></span>
![Flujo de experimento][2]

#### <a name="module-1"></a><span data-ttu-id="94d9b-136">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="94d9b-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="94d9b-137">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="94d9b-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="94d9b-138">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="94d9b-138">Limitations</span></span>
<span data-ttu-id="94d9b-139">Se trata de un ejemplo muy sencillo para probar las diferencias entre dos proporciones.</span><span class="sxs-lookup"><span data-stu-id="94d9b-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="94d9b-140">Como puede observarse en el código de ejemplo anterior, no se implementa ninguna detección de errores y el servicio supone que todas las variables son continuas.</span><span class="sxs-lookup"><span data-stu-id="94d9b-140">As can be seen from the example code above, no error catching is implemented and the service assumes that all the variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="94d9b-141">P+F</span><span class="sxs-lookup"><span data-stu-id="94d9b-141">FAQ</span></span>
<span data-ttu-id="94d9b-142">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="94d9b-142">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

