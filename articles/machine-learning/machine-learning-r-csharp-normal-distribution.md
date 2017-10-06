---
title: "aaa(deprecated) Suite de servicio Web de la distribución Normal - Azure | Documentos de Microsoft"
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
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="71747-103">(obsoleto) Conjunto de distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="71747-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="71747-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="71747-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="71747-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="71747-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="71747-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="71747-107">Hola Suite de distribución Normal es un conjunto de servicios web de ejemplo ([generador](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Calculadora de Cuantil](https://datamarket.azure.com/dataset/aml_labs/ndq5), [probabilidad calculadora](https://datamarket.azure.com/dataset/aml_labs/ndp5)) que ayudan en la generación y control distribuciones normales.</span><span class="sxs-lookup"><span data-stu-id="71747-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="71747-108">Servicios de Hello permiten generar una secuencia de distribución normal de cualquier longitud, calcula los cuantiles desde una probabilidad determinado y calcular la probabilidad de un determinado cuantil.</span><span class="sxs-lookup"><span data-stu-id="71747-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="71747-109">Cada uno de los servicios de hello emite salidas diferentes en función de servicio de hello seleccionado (vea la descripción siguiente).</span><span class="sxs-lookup"><span data-stu-id="71747-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="71747-110">Hola Suite de distribución Normal se basa en hello R funciones qnorm, rnorm y pnorm, que se incluyen en el paquete de estadísticas de R.</span><span class="sxs-lookup"><span data-stu-id="71747-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="71747-111">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="71747-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="71747-112">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="71747-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="71747-113">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="71747-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="71747-114">servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="71747-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="71747-115">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="71747-115">Consumption of web service</span></span>
<span data-ttu-id="71747-116">Hola distribución Normal Suite incluye Hola siguientes 3 servicios.</span><span class="sxs-lookup"><span data-stu-id="71747-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="71747-117">Calculadora de cuantil para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="71747-118">Este servicio acepta 4 argumentos de una distribución normal y calcula los cuantiles Hola asociado.</span><span class="sxs-lookup"><span data-stu-id="71747-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="71747-119">argumentos de entrada de Hello son:</span><span class="sxs-lookup"><span data-stu-id="71747-119">hello input arguments are:</span></span>

* <span data-ttu-id="71747-120">p: una única probabilidad de un evento con distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="71747-121">Significa: Hola Media de la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="71747-122">SD - desviación estándar de hello distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="71747-123">Lado - L para la parte inferior de Hola de distribución de Hola y U para el lado superior de Hola de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="71747-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="71747-124">salida de Hello del servicio de hello es cuantil Hola calculado que está asociado con hello dada la probabilidad.</span><span class="sxs-lookup"><span data-stu-id="71747-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="71747-125">Calculadora de probabilidad para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="71747-126">Este servicio acepta 4 argumentos de una distribución normal y calcula la probabilidad de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="71747-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="71747-127">argumentos de entrada de Hello son:</span><span class="sxs-lookup"><span data-stu-id="71747-127">hello input arguments are:</span></span>

* <span data-ttu-id="71747-128">q: un único cuantil de un evento con distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="71747-129">Significa: Hola Media de la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="71747-130">SD - desviación estándar de hello distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="71747-131">Lado - L para la parte inferior de Hola de distribución de Hola y U para el lado superior de Hola de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="71747-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="71747-132">salida de Hello del servicio de hello es la probabilidad de hello calculado que está asociado con hello proporcionado por cuantiles.</span><span class="sxs-lookup"><span data-stu-id="71747-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="71747-133">Generador de distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-133">Normal Distribution Generator</span></span>
<span data-ttu-id="71747-134">Este servicio acepta 3 argumentos de una distribución normal y genera una secuencia aleatoria de números que se distribuyen de manera normal.</span><span class="sxs-lookup"><span data-stu-id="71747-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="71747-135">Hello argumentos siguientes deben proporcionarse tooit dentro de la solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="71747-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="71747-136">n - número de Hola de observaciones.</span><span class="sxs-lookup"><span data-stu-id="71747-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="71747-137">significa: Hola Media de la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="71747-138">SD - desviación estándar de hello distribución normal.</span><span class="sxs-lookup"><span data-stu-id="71747-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="71747-139">salida de Hello del servicio de hello es una secuencia de longitud n con una distribución normal en función de los argumentos de Media y sd de Hola.</span><span class="sxs-lookup"><span data-stu-id="71747-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="71747-140">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="71747-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="71747-141">Hay varias maneras de consumo de servicio de Hola de forma automática (aplicaciones de ejemplo se están aquí: [generador](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [probabilidad calculadora](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Cuantil calculadora](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="71747-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="71747-142">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="71747-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="71747-143">Calculadora de cuantil para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-143">Normal Distribution Quantile Calculator</span></span>
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


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="71747-144">Calculadora de probabilidad para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-144">Normal Distribution Probability Calculator</span></span>
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

### <a name="normal-distribution-generator"></a><span data-ttu-id="71747-145">Generador de distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-145">Normal Distribution Generator</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="71747-146">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="71747-146">Creation of web service</span></span>
> <span data-ttu-id="71747-147">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="71747-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="71747-148">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="71747-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="71747-149">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="71747-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="71747-150">Calculadora de cuantil para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="71747-151">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="71747-151">Experiment flow:</span></span>

![Flujo de experimento][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="71747-153">Calculadora de probabilidad para la distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="71747-154">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="71747-154">Experiment flow:</span></span>

![Flujo de experimento][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="71747-156">Generador de distribución normal</span><span class="sxs-lookup"><span data-stu-id="71747-156">Normal Distribution Generator</span></span>
<span data-ttu-id="71747-157">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="71747-157">Experiment flow:</span></span>

![Flujo de experimento][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="71747-159">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="71747-159">Limitations</span></span>
<span data-ttu-id="71747-160">Estos son ejemplos muy simples que rodean la distribución normal Hola.</span><span class="sxs-lookup"><span data-stu-id="71747-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="71747-161">Como se puede ver desde el código de ejemplo de Hola anterior, se implementan poco realizar capturas de errores.</span><span class="sxs-lookup"><span data-stu-id="71747-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="71747-162">P+F</span><span class="sxs-lookup"><span data-stu-id="71747-162">FAQ</span></span>
<span data-ttu-id="71747-163">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="71747-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

