---
title: "aaa(deprecated) distribución Binomial Suite - Azure | Documentos de Microsoft"
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
redirect_document_id: True
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="cbc4c-103">(obsoleto) Conjunto de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="cbc4c-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="cbc4c-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="cbc4c-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="cbc4c-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="cbc4c-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="cbc4c-107">Hola Distribución Binomial conjunto es un conjunto de servicios web de ejemplo ([Binomial generador](https://datamarket.azure.com/dataset/aml_labs/bdg5), [probabilidad calculadora](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Cuantil calculadora](https://datamarket.azure.com/dataset/aml_labs/bdq5)) que ayudan en la generación y trabajar con la distribución binomial.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="cbc4c-108">Hello servicios permiten generar una secuencia de distribución binomial de cualquier longitud, calcula los cuantiles fuera de dado probabilidad y el cálculo probabilidad de un determinado cuantil.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="cbc4c-109">Cada uno de los servicios de hello emite salidas diferentes en función de servicio de hello seleccionado (vea la descripción siguiente).</span><span class="sxs-lookup"><span data-stu-id="cbc4c-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="cbc4c-110">Hola Distribución Binomial Suite se basa en hello R funciones qbinom, rbinom y pbinom, que se incluyen en el paquete de estadísticas de hello R.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="cbc4c-111">Estos servicios web que pueden consumir los usuarios: potencialmente directamente en el marketplace de hello, a través de una aplicación móvil, a través de un sitio Web, o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="cbc4c-112">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="cbc4c-113">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="cbc4c-114">servicio web de Hello, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos en Hola a todos: se requiere ninguna configuración de infraestructura el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="cbc4c-115">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="cbc4c-115">Consumption of web service</span></span>
<span data-ttu-id="cbc4c-116">Hola Distribución Binomial Suite incluye Hola siguientes 3 servicios.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="cbc4c-117">Calculadora de cuantil para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="cbc4c-118">Este servicio acepta 4 argumentos de una distribución normal y calcula los cuantiles Hola asociado.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="cbc4c-119">argumentos de entrada de Hello son:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-119">hello input arguments are:</span></span>

* <span data-ttu-id="cbc4c-120">p: una única probabilidad agregada de varias pruebas.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="cbc4c-121">tamaño: número de Hola de pruebas.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-121">size - hello number of trials.</span></span>
* <span data-ttu-id="cbc4c-122">probabilidad: probabilidad de Hola de éxito en una versión de prueba.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="cbc4c-123">Lado - L para la parte inferior de Hola de distribución de hello, U para el lado superior de Hola de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="cbc4c-124">salida de Hello del servicio de hello es cuantil Hola calculado que está asociado con hello dada la probabilidad.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="cbc4c-125">Calculadora de probabilidad para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="cbc4c-126">Este servicio acepta 4 argumentos de una distribución binomial y calcula la probabilidad de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="cbc4c-127">argumentos de entrada de Hello son:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-127">hello input arguments are:</span></span>

* <span data-ttu-id="cbc4c-128">q: un único cuantil de un evento con distribución binomial.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="cbc4c-129">tamaño: número de Hola de pruebas.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-129">size - hello number of trials.</span></span>
* <span data-ttu-id="cbc4c-130">probabilidad: probabilidad de Hola de éxito en una versión de prueba.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="cbc4c-131">lado - L para la parte inferior de Hola de distribución de hello, U para el lado superior de Hola de distribución de Hola o (Tee) que es igual tooa único número de operaciones correctas.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="cbc4c-132">salida de Hello del servicio de hello es la probabilidad de hello calculado que está asociado con hello proporcionado por cuantiles.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="cbc4c-133">Generador de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="cbc4c-134">Este servicio acepta 3 argumentos de una distribución binomial y genera una secuencia aleatoria de números que se distribuyen de manera binomial.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="cbc4c-135">Hello argumentos siguientes deben proporcionarse tooit dentro de la solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="cbc4c-136">n: número de observaciones.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-136">n - Number of observations.</span></span> 
* <span data-ttu-id="cbc4c-137">tamaño: número de pruebas.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-137">size - Number of trials.</span></span>
* <span data-ttu-id="cbc4c-138">prob: probabilidad de éxito.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-138">prob - Probability of success.</span></span>

<span data-ttu-id="cbc4c-139">salida de Hello del servicio de hello es una secuencia de longitud n con una distribución binomial en función de los argumentos de tamaño y la probabilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="cbc4c-140">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="cbc4c-141">Hay varias maneras de consumo de servicio de Hola de forma automática (aplicaciones de ejemplo se están aquí: [generador](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [probabilidad calculadora](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Cuantil calculadora](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="cbc4c-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="cbc4c-142">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="cbc4c-143">Calculadora de cuantil para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-143">Binomial Distribution Quantile Calculator</span></span>
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

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="cbc4c-144">Calculadora de probabilidad para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-144">Binomial Distribution Probability Calculator</span></span>
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


### <a name="binomial-distribution-generator"></a><span data-ttu-id="cbc4c-145">Generador de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-145">Binomial Distribution Generator</span></span>
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





## <a name="creation-of-web-service"></a><span data-ttu-id="cbc4c-146">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="cbc4c-146">Creation of web service</span></span>
> <span data-ttu-id="cbc4c-147">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="cbc4c-148">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="cbc4c-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="cbc4c-149">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="cbc4c-150">Calculadora de cuantil para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-150">Binomial Distribution Quantile Calculator</span></span>
![Creación del espacio de trabajo][4]

#### <a name="module-1"></a><span data-ttu-id="cbc4c-152">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="cbc4c-153">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-153">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="cbc4c-154">Calculadora de probabilidad para la distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-154">Binomial Distribution Probability Calculator</span></span>
![Creación del espacio de trabajo][5]

#### <a name="module-1"></a><span data-ttu-id="cbc4c-156">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="cbc4c-157">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-157">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="cbc4c-158">Generador de distribución binomial</span><span class="sxs-lookup"><span data-stu-id="cbc4c-158">Binomial Distribution Generator</span></span>
![Creación del espacio de trabajo][6]

#### <a name="module-1"></a><span data-ttu-id="cbc4c-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="cbc4c-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="cbc4c-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="cbc4c-162">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="cbc4c-162">Limitations</span></span>
<span data-ttu-id="cbc4c-163">Estos son muy sencillos ejemplos que rodea una distribución binomial Hola.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="cbc4c-164">Como se puede ver desde el código de ejemplo de Hola anterior, se implementan poco realizar capturas de errores.</span><span class="sxs-lookup"><span data-stu-id="cbc4c-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="cbc4c-165">P+F</span><span class="sxs-lookup"><span data-stu-id="cbc4c-165">FAQ</span></span>
<span data-ttu-id="cbc4c-166">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="cbc4c-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

