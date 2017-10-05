---
title: "(obsoleto) Conjunto de servicios web de distribución normal - Azure | Microsoft Docs"
description: "(obsoleto) Conjunto de servicios web de distribución normal"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="aff98-103">(obsoleto) Conjunto de distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="aff98-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="aff98-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="aff98-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="aff98-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="aff98-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="aff98-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="aff98-107">El conjunto de distribución normal es una serie de servicios web de ejemplo ([Generador](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Calculadora de cuantil](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Calculadora de probabilidad](https://datamarket.azure.com/dataset/aml_labs/ndp5)) que ayudan a generar y administrar distribuciones normales.</span><span class="sxs-lookup"><span data-stu-id="aff98-107">The Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="aff98-108">Los servicios permiten generar una secuencia de distribución normal de cualquier longitud, calcular los cuantiles de una probabilidad determinada y calcular la probabilidad a partir de un cuantil específico.</span><span class="sxs-lookup"><span data-stu-id="aff98-108">The services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="aff98-109">Cada uno de los servicios genera salidas diferentes en función del servicio seleccionado (consulte la siguiente descripción).</span><span class="sxs-lookup"><span data-stu-id="aff98-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="aff98-110">El conjunto de distribución normal se basa en funciones qnorm, rnorm y pnorm de R que se incluyen en el paquete de estadísticas de R.</span><span class="sxs-lookup"><span data-stu-id="aff98-110">The Normal Distribution Suite is based on the R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="aff98-111">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="aff98-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="aff98-112">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="aff98-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="aff98-113">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="aff98-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="aff98-114">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="aff98-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="aff98-115">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="aff98-115">Consumption of web service</span></span>
<span data-ttu-id="aff98-116">El conjunto de distribución normal incluye los tres servicios siguientes:</span><span class="sxs-lookup"><span data-stu-id="aff98-116">The Normal Distribution Suite includes the following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="aff98-117">Calculadora de cuantil para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="aff98-118">Este servicio acepta 4 argumentos de una distribución normal y calcula el cuantil asociado.</span><span class="sxs-lookup"><span data-stu-id="aff98-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>

<span data-ttu-id="aff98-119">Los argumentos de entrada son:</span><span class="sxs-lookup"><span data-stu-id="aff98-119">The input arguments are:</span></span>

* <span data-ttu-id="aff98-120">p: una única probabilidad de un evento con distribución normal.</span><span class="sxs-lookup"><span data-stu-id="aff98-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="aff98-121">Media: la media de la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-121">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="aff98-122">SD: la desviación estándar de la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="aff98-122">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="aff98-123">Lado: L para la parte inferior de la distribución y U para la parte superior de la distribución.</span><span class="sxs-lookup"><span data-stu-id="aff98-123">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="aff98-124">La salida del servicio es el cuantil calculado asociado con la probabilidad dada.</span><span class="sxs-lookup"><span data-stu-id="aff98-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="aff98-125">Calculadora de probabilidad para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="aff98-126">Este servicio acepta 4 argumentos de una distribución normal y calcula la probabilidad asociada.</span><span class="sxs-lookup"><span data-stu-id="aff98-126">This service accepts 4 arguments of a normal distribution and calculates the associated probability.</span></span>

<span data-ttu-id="aff98-127">Los argumentos de entrada son:</span><span class="sxs-lookup"><span data-stu-id="aff98-127">The input arguments are:</span></span>

* <span data-ttu-id="aff98-128">q: un único cuantil de un evento con distribución normal.</span><span class="sxs-lookup"><span data-stu-id="aff98-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="aff98-129">Media: la media de la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-129">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="aff98-130">SD: la desviación estándar de la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="aff98-130">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="aff98-131">Lado: L para la parte inferior de la distribución y U para la parte superior de la distribución.</span><span class="sxs-lookup"><span data-stu-id="aff98-131">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="aff98-132">La salida del servicio es la probabilidad calculada asociada con el cuantil dado.</span><span class="sxs-lookup"><span data-stu-id="aff98-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="aff98-133">Generador de distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-133">Normal Distribution Generator</span></span>
<span data-ttu-id="aff98-134">Este servicio acepta 3 argumentos de una distribución normal y genera una secuencia aleatoria de números que se distribuyen de manera normal.</span><span class="sxs-lookup"><span data-stu-id="aff98-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="aff98-135">Se le deben proporcionar los siguientes argumentos en la solicitud:</span><span class="sxs-lookup"><span data-stu-id="aff98-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="aff98-136">n: número de observaciones.</span><span class="sxs-lookup"><span data-stu-id="aff98-136">n - The number of observations.</span></span> 
* <span data-ttu-id="aff98-137">Media: la media de la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-137">mean - The normal distribution mean.</span></span>
* <span data-ttu-id="aff98-138">SD: la desviación estándar de la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="aff98-138">sd - The normal distribution standard deviation.</span></span> 

<span data-ttu-id="aff98-139">La salida del servicio es una secuencia de longitud n con una distribución normal basada en los argumentos media y desviación estándar.</span><span class="sxs-lookup"><span data-stu-id="aff98-139">The output of the service is a sequence of length n with a normal distribution based on the mean and sd arguments.</span></span>

> <span data-ttu-id="aff98-140">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="aff98-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="aff98-141">Hay varias maneras de consumir el servicio de forma automática (las aplicaciones de ejemplo son: [Generador](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Calculadora de probabilidad](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Calculadora de cuantil](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="aff98-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="aff98-142">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="aff98-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="aff98-143">Calculadora de cuantil para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="aff98-144">Calculadora de probabilidad para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="aff98-145">Generador de distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="aff98-146">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="aff98-146">Creation of web service</span></span>
> <span data-ttu-id="aff98-147">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="aff98-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="aff98-148">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="aff98-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="aff98-149">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="aff98-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="aff98-150">Calculadora de cuantil para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="aff98-151">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="aff98-151">Experiment flow:</span></span>

![Flujo de experimento][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="aff98-153">Calculadora de probabilidad para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="aff98-154">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="aff98-154">Experiment flow:</span></span>

![Flujo de experimento][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="aff98-156">Generador de distribución normal</span><span class="sxs-lookup"><span data-stu-id="aff98-156">Normal Distribution Generator</span></span>
<span data-ttu-id="aff98-157">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="aff98-157">Experiment flow:</span></span>

![Flujo de experimento][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="aff98-159">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="aff98-159">Limitations</span></span>
<span data-ttu-id="aff98-160">Se trata de ejemplos muy sencillos relacionados con la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="aff98-160">These are very simple examples surrounding the normal distribution.</span></span> <span data-ttu-id="aff98-161">Como puede observarse en el código de ejemplo anterior, se implementa una detección de errores mínima.</span><span class="sxs-lookup"><span data-stu-id="aff98-161">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="aff98-162">P+F</span><span class="sxs-lookup"><span data-stu-id="aff98-162">FAQ</span></span>
<span data-ttu-id="aff98-163">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="aff98-163">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

