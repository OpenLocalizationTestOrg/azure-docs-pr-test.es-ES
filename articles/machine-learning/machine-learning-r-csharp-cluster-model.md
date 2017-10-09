---
title: "aaa(deprecated) modelo de clúster - Azure | Documentos de Microsoft"
description: "(obsoleto) Modelo de clústeres"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="0bcf8-103">(obsoleto) Modelo de clústeres</span><span class="sxs-lookup"><span data-stu-id="0bcf8-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="0bcf8-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0bcf8-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0bcf8-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0bcf8-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0bcf8-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0bcf8-107">¿Cómo puedan se predecir grupos de comportamientos de crédito titular de la tarjeta en orden tooreduce Hola cargo desactivar riesgo de emisores de tarjeta de crédito?</span><span class="sxs-lookup"><span data-stu-id="0bcf8-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="0bcf8-108">¿Cómo podemos se definen grupos de rasgos de personalidad de empleados en orden tooimprove su rendimiento en el trabajo?</span><span class="sxs-lookup"><span data-stu-id="0bcf8-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="0bcf8-109">¿Cómo pueden los médicos clasificar pacientes en grupos basados en las características de Hola de sus enfermedades?</span><span class="sxs-lookup"><span data-stu-id="0bcf8-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="0bcf8-110">En principio, todas estas preguntas pueden responderse mediante el análisis del clúster.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0bcf8-111">El análisis del clúster clasifica un conjunto de observaciones en dos o más grupos desconocidos mutuamente excluyentes conforme a combinaciones de variables.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="0bcf8-112">Hola de análisis de clúster sirve toodiscover un sistema de la organización de observaciones, normalmente personas o sus características en grupos, donde los miembros de grupos de hello tienen propiedades en común.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="0bcf8-113">Esto [servicio](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) usa Hola metodología K-Means, una técnica de agrupación en clústeres utilizada, toocluster datos arbitrarios en grupos.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="0bcf8-114">Este servicio web toma los datos de Hola y el número de Hola de k clústeres como entrada y genera predicciones de los cuales Hola k grupos toowhich pertenece cada observaciones.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="0bcf8-115">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0bcf8-116">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="0bcf8-117">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0bcf8-118">servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0bcf8-119">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="0bcf8-119">Consumption of web service</span></span>
<span data-ttu-id="0bcf8-120">Este servicio web agrupa datos hello en un conjunto de k grupos y salidas Hola asignación de grupo para cada fila.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="0bcf8-121">servicio web de Hola espera datos de tooinput de usuario final de saludo como una cadena donde filas están separadas por comas (,) y las columnas se separan mediante punto y coma (;).</span><span class="sxs-lookup"><span data-stu-id="0bcf8-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="0bcf8-122">servicio web de Hello espera 1 fila a la vez.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="0bcf8-123">Un conjunto de datos de ejemplo podría tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="0bcf8-123">An example dataset could look like this:</span></span>

![Datos de ejemplo][1]

<span data-ttu-id="0bcf8-125">Suponga que Hola usuario deseado tooseparate estos datos en 3 grupos mutuamente excluyentes.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="0bcf8-126">Hola Hola por encima del conjunto de datos sería siguiente Hola de entrada de datos: valor = "10; 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3".</span><span class="sxs-lookup"><span data-stu-id="0bcf8-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="0bcf8-127">salida de Hello es hello pertenencia a grupos de predicción para cada una de las filas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="0bcf8-128">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0bcf8-129">Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0bcf8-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0bcf8-130">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="0bcf8-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="0bcf8-131">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="0bcf8-131">Creation of web service</span></span>
> <span data-ttu-id="0bcf8-132">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0bcf8-133">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0bcf8-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0bcf8-134">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="0bcf8-135">Desde dentro del aprendizaje automático de Azure, un experimento en blanco nueva se crea y dos [ejecutar Script de R] [ execute-r-script] módulos extraen en el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="0bcf8-136">esquema de datos de Hola se creó con un sencillo [ejecutar Script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="0bcf8-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="0bcf8-137">A continuación, esquema de datos de hello estaba vinculado toohello de clúster modelo, vuelva a crear con un [ejecutar Script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="0bcf8-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="0bcf8-138">Hola [ejecutar Script de R] [ execute-r-script] utilizado para el modelo de clústeres de hello, servicio web de hello, a continuación, utiliza función hello "k-means", que es creada previamente en hello [ejecutar Script de R] [ execute-r-script] de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Flujo de experimento][3]

#### <a name="module-1"></a><span data-ttu-id="0bcf8-140">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="0bcf8-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="0bcf8-141">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="0bcf8-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="0bcf8-142">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="0bcf8-142">Limitations</span></span>
<span data-ttu-id="0bcf8-143">Se trata de un ejemplo muy sencillo de un servicio web de agrupación en clústeres.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="0bcf8-144">Como se puede ver desde el código de ejemplo de Hola anterior, no se implementa la ningún error que detecte y Hola servicio supone que todo lo que es una variable continua (no hay categorías características permitidas), como Hola servicio solo entradas valores numéricos en tiempo de Hola de creación de hello de este sitio web servicio.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="0bcf8-145">Además, servicio Hola actualmente controla el tamaño de datos limitado, debido toohello naturaleza de solicitud/respuesta del servicio web de hello es que se va a ajustar hello y llamada de hechos que Hola modelo cada vez que se llama servicio de hello web.</span><span class="sxs-lookup"><span data-stu-id="0bcf8-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="0bcf8-146">P+F</span><span class="sxs-lookup"><span data-stu-id="0bcf8-146">FAQ</span></span>
<span data-ttu-id="0bcf8-147">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0bcf8-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

