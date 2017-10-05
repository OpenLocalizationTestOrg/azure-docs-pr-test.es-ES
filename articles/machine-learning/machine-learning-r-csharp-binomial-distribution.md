---
title: "(obsoleto) Conjunto de distribución binomial - Azure | Microsoft Docs"
description: "(obsoleto) Conjunto de distribución binomial"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
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
ms.openlocfilehash: 6f0a6d06e7401c8360a92a707a0552f41ff3657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="9aaf5-103">(obsoleto) Conjunto de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="9aaf5-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="9aaf5-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9aaf5-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9aaf5-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="9aaf5-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9aaf5-107">El conjunto de distribución binomial es una serie de servicios web de ejemplo ([Generador binomial](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Calculadora de probabilidad](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Calculadora de cuantil](https://datamarket.azure.com/dataset/aml_labs/bdq5)) que ayudan a generar y administrar distribuciones binomiales.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="9aaf5-108">Los servicios permiten generar una secuencia de distribución binomial de cualquier longitud, calcular los cuantiles de una probabilidad determinada y calcular la probabilidad a partir de un cuantil específico.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="9aaf5-109">Cada uno de los servicios genera salidas diferentes en función del servicio seleccionado (consulte la siguiente descripción).</span><span class="sxs-lookup"><span data-stu-id="9aaf5-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="9aaf5-110">El conjunto de distribución binomial se basa en funciones qbinom, rbinom y pbinom de R que se incluyen en el paquete de estadísticas de R.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="9aaf5-111">Los servicio web pueden ser consumidos por los usuarios, bien directamente en marketplace, a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="9aaf5-112">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="9aaf5-113">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="9aaf5-114">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan consumir usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="9aaf5-115">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="9aaf5-115">Consumption of web service</span></span>
<span data-ttu-id="9aaf5-116">El conjunto de distribución binomial incluye los tres servicios siguientes.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="9aaf5-117">Calculadora de cuantil para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="9aaf5-118">Este servicio acepta 4 argumentos de una distribución normal y calcula el cuantil asociado.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="9aaf5-119">Los argumentos de entrada son:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-119">The input arguments are:</span></span>

* <span data-ttu-id="9aaf5-120">p: una única probabilidad agregada de varias pruebas.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="9aaf5-121">tamaño: el número de pruebas.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-121">size - The number of trials.</span></span>
* <span data-ttu-id="9aaf5-122">probabilidad: la probabilidad de éxito en una prueba.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="9aaf5-123">Lado: L para la parte inferior de la distribución, U para la parte superior de la distribución.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="9aaf5-124">La salida del servicio es el cuantil calculado asociado con la probabilidad dada.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="9aaf5-125">Calculadora de probabilidad para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="9aaf5-126">Este servicio acepta 4 argumentos de una distribución binomial y calcula la probabilidad asociada.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="9aaf5-127">Los argumentos de entrada son:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-127">The input arguments are:</span></span>

* <span data-ttu-id="9aaf5-128">q: un único cuantil de un evento con distribución binomial.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="9aaf5-129">tamaño: el número de pruebas.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-129">size - The number of trials.</span></span>
* <span data-ttu-id="9aaf5-130">probabilidad: la probabilidad de éxito en una prueba.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="9aaf5-131">Lado: L para la parte inferior de la distribución, U para la parte superior de la distribución o E que es igual a un único número de éxitos.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="9aaf5-132">La salida del servicio es la probabilidad calculada asociada con el cuantil dado.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="9aaf5-133">Generador de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="9aaf5-134">Este servicio acepta 3 argumentos de una distribución binomial y genera una secuencia aleatoria de números que se distribuyen de manera binomial.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="9aaf5-135">Se le deben proporcionar los siguientes argumentos en la solicitud:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="9aaf5-136">n: número de observaciones.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-136">n - Number of observations.</span></span> 
* <span data-ttu-id="9aaf5-137">tamaño: número de pruebas.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-137">size - Number of trials.</span></span>
* <span data-ttu-id="9aaf5-138">prob: probabilidad de éxito.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-138">prob - Probability of success.</span></span>

<span data-ttu-id="9aaf5-139">La salida del servicio es una secuencia de longitud n con una distribución binomial basada en los argumentos de tamaño y probabilidad.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="9aaf5-140">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="9aaf5-141">Hay varias maneras de consumir el servicio de forma automática (las aplicaciones de ejemplo son: [Generador](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Calculadora de probabilidad](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Calculadora de cuantil](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="9aaf5-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="9aaf5-142">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="9aaf5-143">Calculadora de cuantil para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="9aaf5-144">Calculadora de probabilidad para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="9aaf5-145">Generador de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="9aaf5-146">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="9aaf5-146">Creation of web service</span></span>
> <span data-ttu-id="9aaf5-147">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="9aaf5-148">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="9aaf5-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="9aaf5-149">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="9aaf5-150">Calculadora de cuantil para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-150">Binomial Distribution Quantile Calculator</span></span>
![Creación del espacio de trabajo][4]

#### <a name="module-1"></a><span data-ttu-id="9aaf5-152">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="9aaf5-153">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="9aaf5-154">Calculadora de probabilidad para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-154">Binomial Distribution Probability Calculator</span></span>
![Creación del espacio de trabajo][5]

#### <a name="module-1"></a><span data-ttu-id="9aaf5-156">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="9aaf5-157">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="9aaf5-158">Generador de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="9aaf5-158">Binomial Distribution Generator</span></span>
![Creación del espacio de trabajo][6]

#### <a name="module-1"></a><span data-ttu-id="9aaf5-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="9aaf5-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="9aaf5-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="9aaf5-162">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="9aaf5-162">Limitations</span></span>
<span data-ttu-id="9aaf5-163">Se trata de ejemplos muy sencillos relacionados con la distribución binomial.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="9aaf5-164">Como puede observarse en el código de ejemplo anterior, se implementa una detección de errores mínima.</span><span class="sxs-lookup"><span data-stu-id="9aaf5-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="9aaf5-165">P+F</span><span class="sxs-lookup"><span data-stu-id="9aaf5-165">FAQ</span></span>
<span data-ttu-id="9aaf5-166">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9aaf5-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

