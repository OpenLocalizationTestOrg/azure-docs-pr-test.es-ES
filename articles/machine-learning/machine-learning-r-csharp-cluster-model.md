---
title: "(obsoleto) Modelo de clústeres - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="2b9ae-103">(obsoleto) Modelo de clústeres</span><span class="sxs-lookup"><span data-stu-id="2b9ae-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="2b9ae-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2b9ae-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="2b9ae-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2b9ae-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="2b9ae-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2b9ae-107">¿Cómo podemos predecir grupos de comportamientos de los titulares de tarjetas de crédito para reducir el riesgo de impago al que están expuestos los emisores de dichas tarjetas?</span><span class="sxs-lookup"><span data-stu-id="2b9ae-107">How can we predict groups of credit cardholders’ behaviors in order to reduce the charge-off risk of credit card issuers?</span></span> <span data-ttu-id="2b9ae-108">¿Cómo podemos definir grupos de rasgos de personalidad de empleados con el fin de mejorar su rendimiento en el trabajo?</span><span class="sxs-lookup"><span data-stu-id="2b9ae-108">How can we define groups of personality traits of employees in order to improve their performance at work?</span></span> <span data-ttu-id="2b9ae-109">¿Cómo pueden clasificar los médicos a los pacientes en grupos en función de las características de sus enfermedades?</span><span class="sxs-lookup"><span data-stu-id="2b9ae-109">How can doctors classify patients into groups based on the characteristics of their diseases?</span></span> <span data-ttu-id="2b9ae-110">En principio, todas estas preguntas pueden responderse mediante el análisis del clúster.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2b9ae-111">El análisis del clúster clasifica un conjunto de observaciones en dos o más grupos desconocidos mutuamente excluyentes conforme a combinaciones de variables.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="2b9ae-112">El propósito del análisis del clúster es detectar un sistema para organizar en grupos las observaciones, normalmente las personas o sus características, donde los miembros de los grupos tienen propiedades en común.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-112">The purpose of cluster analysis is to discover a system of organizing observations, usually people or their characteristics, into groups, where members of the groups share properties in common.</span></span> <span data-ttu-id="2b9ae-113">Este [servicio](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) usa la metodología de K-Means, una técnica de agrupación en clústeres de uso habitual, para agrupar datos arbitrarios en grupos.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses the K-Means methodology, a commonly used clustering technique, to cluster arbitrary data into groups.</span></span> <span data-ttu-id="2b9ae-114">Este servicio web recibe los datos y el número de clústeres k como entradas y genera las predicciones del grupo k al que pertenece cada observación.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-114">This web service takes the data and the number of k clusters as input, and produces predictions of which of the k groups to which each observations belongs.</span></span> 

> <span data-ttu-id="2b9ae-115">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="2b9ae-116">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="2b9ae-117">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2b9ae-118">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2b9ae-119">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="2b9ae-119">Consumption of web service</span></span>
<span data-ttu-id="2b9ae-120">Este servicio web agrupa los datos en un conjunto de grupos k y genera la asignación de grupo para cada fila.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-120">This web service groups the data into a set of k groups and outputs the group assignment for each row.</span></span> <span data-ttu-id="2b9ae-121">El servicio web espera que el usuario final escriba sus datos como una cadena, donde las filas están separadas por comas (,) y las columnas se separan mediante punto y coma (;).</span><span class="sxs-lookup"><span data-stu-id="2b9ae-121">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="2b9ae-122">El servicio web espera 1 fila a la vez.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-122">The web service expects 1 row at a time.</span></span> <span data-ttu-id="2b9ae-123">Un conjunto de datos de ejemplo podría tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="2b9ae-123">An example dataset could look like this:</span></span>

![Datos de ejemplo][1]

<span data-ttu-id="2b9ae-125">Supongamos que el usuario desea separar estos datos en tres grupos mutuamente excluyentes.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-125">Suppose the user wanted to separate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="2b9ae-126">Los datos de entrada para el conjunto de datos anterior serían los siguientes: valor = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-126">The data input for the above dataset would be the following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="2b9ae-127">El resultado es la pertenencia prevista a un grupo para cada una de las filas.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-127">The output is the predicted group membership for each of the rows.</span></span>

> <span data-ttu-id="2b9ae-128">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-128">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2b9ae-129">Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)se puede ver una aplicación de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="2b9ae-129">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2b9ae-130">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="2b9ae-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="2b9ae-131">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="2b9ae-131">Creation of web service</span></span>
> <span data-ttu-id="2b9ae-132">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2b9ae-133">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="2b9ae-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2b9ae-134">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-134">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="2b9ae-135">En Machine Learning de Azure se creó un nuevo experimento en blanco y se extrajeron dos módulos [Ejecutar scripts R][execute-r-script] en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="2b9ae-136">El esquema de datos se creó con un módulo [Ejecutar script R][execute-r-script] sencillo.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-136">The data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="2b9ae-137">A continuación, el esquema de datos se vinculó a la sección del modelo de clúster, que también se creó con un comando [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="2b9ae-137">Then, the data schema was linked to the cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="2b9ae-138">En el comando [Ejecutar script R][execute-r-script] utilizado para el modelo de clúster, el servicio web utiliza la función "k-means", que está preintegrada en el comando [Ejecutar script R][execute-r-script] de Machine Learning de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-138">In the [Execute R Script][execute-r-script] used for the cluster model, the web service then utilizes the “k-means” function, which is prebuilt into the [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Flujo de experimento][3]

#### <a name="module-1"></a><span data-ttu-id="2b9ae-140">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="2b9ae-140">Module 1:</span></span>
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="2b9ae-141">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="2b9ae-141">Module 2:</span></span>
    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="2b9ae-142">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="2b9ae-142">Limitations</span></span>
<span data-ttu-id="2b9ae-143">Se trata de un ejemplo muy sencillo de un servicio web de agrupación en clústeres.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="2b9ae-144">Como puede observarse en el código de ejemplo anterior, no se implementa ninguna detección de errores y el servicio asume que todo es una variable continua (ninguna característica categórica permitida), ya que el servicio solo recibe valores numéricos en el momento de la creación de este servicio web.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-144">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="2b9ae-145">Además, el servicio actualmente controla el tamaño de datos limitado, debido a la naturaleza de solicitud y respuesta de la llamada al servicio web y el hecho de que el modelo se ajusta cada vez que se llama al servicio web.</span><span class="sxs-lookup"><span data-stu-id="2b9ae-145">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="2b9ae-146">P+F</span><span class="sxs-lookup"><span data-stu-id="2b9ae-146">FAQ</span></span>
<span data-ttu-id="2b9ae-147">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2b9ae-147">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

