---
title: "aaa(deprecated) la regresión lineal Multivariante - Azure | Documentos de Microsoft"
description: "(En desuso) Regresión lineal multivariada"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="3bd2a-103">(En desuso) Regresión lineal multivariada</span><span class="sxs-lookup"><span data-stu-id="3bd2a-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="3bd2a-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="3bd2a-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3bd2a-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3bd2a-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3bd2a-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3bd2a-107">Suponga que tiene un conjunto de datos y podría predecir una variable dependiente (y) como tooquickly de cada cliente individual (i) en función de las variables independientes.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="3bd2a-108">La regresión lineal es una técnica estadística popular utilizada para tales predicciones.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="3bd2a-109">Aquí Hola variable dependiente y se supone que toobe un valor continuo.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="3bd2a-110">Podría ser un escenario simple donde investigadores Hola está tratando de peso de hello toopredict de una persona (y) en función de su alto (x).</span><span class="sxs-lookup"><span data-stu-id="3bd2a-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="3bd2a-111">Podría ser un escenario más avanzado donde investigadores hello tengan información adicional para hello individual (por ejemplo, peso, sexo, carrera) e intentos de peso de hello toopredict de hello individuales.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="3bd2a-112">Esto [servicio web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) encajan Hola datos de toohello del modelo de regresión lineal y salidas Hola predicho valores (y) para cada una de las observaciones de hello en los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="3bd2a-113">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="3bd2a-114">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="3bd2a-115">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="3bd2a-116">servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="3bd2a-117">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="3bd2a-117">Consumption of web service</span></span>
<span data-ttu-id="3bd2a-118">Este Hola de web service proporciona predecir valores de variable dependiente de hello basadas en las variables independientes de Hola para todas las observaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="3bd2a-119">servicio web de Hola espera datos de tooinput de usuario final de saludo como una cadena donde filas están separadas por comas (,) y las columnas se separan mediante punto y coma (;).</span><span class="sxs-lookup"><span data-stu-id="3bd2a-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="3bd2a-120">servicio web de Hello espera 1 fila a la vez y espera Hola primera columna toobe Hola dependiente de la variable.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="3bd2a-121">Un conjunto de datos de ejemplo podría tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="3bd2a-121">An example dataset could look like this:</span></span>

![Datos de ejemplo][1]

<span data-ttu-id="3bd2a-123">Las observaciones sin una variable dependiente deben especificarse como "NA" para Y.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="3bd2a-124">Hello datos de entrada para hello por encima del conjunto de datos podría Hola después de cadena: "10; 5 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, NA; 3; 4".</span><span class="sxs-lookup"><span data-stu-id="3bd2a-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="3bd2a-125">Hola de salida es hello valor de predicción para cada una de las filas de hello en función de hello independiente variables.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="3bd2a-126">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="3bd2a-127">Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="3bd2a-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="3bd2a-128">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="3bd2a-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="3bd2a-129">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="3bd2a-129">Creation of web service</span></span>
> <span data-ttu-id="3bd2a-130">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="3bd2a-131">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="3bd2a-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="3bd2a-132">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="3bd2a-133">Desde dentro del aprendizaje automático de Azure, un experimento en blanco nueva se crea y dos [ejecutar Script de R] [ execute-r-script] módulos se extrajeron en el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="3bd2a-134">Este servicio web ejecuta un experimento de Aprendizaje automático de Azure con un script de R subyacente.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="3bd2a-135">Hay 2 partes toothis experimentar: definición de esquema y el modelo de entrenamiento + la puntuación.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="3bd2a-136">primer módulo de Hello define la estructura de hello esperado de hello entrada conjunto de datos, donde hello primera variable es variable dependiente de Hola y Hola restantes variables son independientes.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="3bd2a-137">segundo módulo de Hello ajusta un modelo de regresión lineal genérico para los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Flujo de experimento][3]

#### <a name="module-1"></a><span data-ttu-id="3bd2a-139">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="3bd2a-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="3bd2a-140">Definición de esquema</span><span class="sxs-lookup"><span data-stu-id="3bd2a-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="3bd2a-141">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="3bd2a-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="3bd2a-142">Modelado de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="3bd2a-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="3bd2a-143">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="3bd2a-143">Limitations</span></span>
<span data-ttu-id="3bd2a-144">Se trata de un ejemplo muy sencillo de un servicio web de regresión lineal múltiple.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="3bd2a-145">Como se puede ver desde el código de ejemplo de Hola anterior, no se implementa la ningún error que detecte y Hola servicio supone que todo lo que es una variable continua (no hay categorías características permitidas), como Hola servicio solo entradas valores numéricos en tiempo de Hola de creación de hello de este sitio web servicio.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="3bd2a-146">Además, servicio Hola actualmente controla el tamaño de datos limitado, debido toohello naturaleza de solicitud/respuesta del servicio web de hello es que se va a ajustar hello y llamada de hechos que Hola modelo cada vez que se llama servicio de hello web.</span><span class="sxs-lookup"><span data-stu-id="3bd2a-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="3bd2a-147">P+F</span><span class="sxs-lookup"><span data-stu-id="3bd2a-147">FAQ</span></span>
<span data-ttu-id="3bd2a-148">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3bd2a-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

