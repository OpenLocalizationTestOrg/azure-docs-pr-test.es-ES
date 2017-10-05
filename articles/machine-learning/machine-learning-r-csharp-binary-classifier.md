---
title: (obsoleto) Clasificador binario - Azure | Microsoft Docs
description: (obsoleto) Clasificador binario
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="7de92-103">(obsoleto) Clasificador binario</span><span class="sxs-lookup"><span data-stu-id="7de92-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="7de92-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="7de92-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="7de92-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="7de92-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="7de92-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="7de92-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="7de92-107">Suponga que tiene un conjunto de datos y desea predecir una variable dependiente binaria en función de las variables independientes.</span><span class="sxs-lookup"><span data-stu-id="7de92-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="7de92-108">La "regresión logística" es una técnica estadística popular utilizada para tales predicciones.</span><span class="sxs-lookup"><span data-stu-id="7de92-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="7de92-109">En este caso, la variable dependiente es binaria o dicotómica, y p es la probabilidad de la presencia de la característica de interés.</span><span class="sxs-lookup"><span data-stu-id="7de92-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="7de92-110">Un escenario sencillo podría ser aquel en el que un investigador trata de predecir la probabilidad de que un posible estudiante acepte una oferta de admisión a una universidad en función de información determinada (nota media en educación superior, ingresos familiares, residencia y sexo).</span><span class="sxs-lookup"><span data-stu-id="7de92-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="7de92-111">El resultado de la predicción es la probabilidad de que el posible estudiante acepte la oferta de admisión.</span><span class="sxs-lookup"><span data-stu-id="7de92-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="7de92-112">Este [servicio web](https://datamarket.azure.com/dataset/aml_labs/log_regression) ajusta el modelo de regresión logística a los datos y calcula el valor de probabilidad (y) para cada una de las observaciones de los datos.</span><span class="sxs-lookup"><span data-stu-id="7de92-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="7de92-113">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7de92-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="7de92-114">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="7de92-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="7de92-115">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="7de92-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="7de92-116">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="7de92-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="7de92-117">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="7de92-117">Consumption of web service</span></span>
<span data-ttu-id="7de92-118">Este servicio web proporciona los valores de predicción de la variable dependiente según las variables independientes para todas las observaciones.</span><span class="sxs-lookup"><span data-stu-id="7de92-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="7de92-119">El servicio web espera que el usuario final escriba sus datos como una cadena, donde las filas están separadas por coma (,) y las columnas se separan mediante punto y coma (;).</span><span class="sxs-lookup"><span data-stu-id="7de92-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="7de92-120">El servicio web espera 1 fila a la vez y que la primera columna sea la variable dependiente.</span><span class="sxs-lookup"><span data-stu-id="7de92-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="7de92-121">Un conjunto de datos de ejemplo podría tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7de92-121">An example dataset could look like this:</span></span>

![Datos de ejemplo][1]

<span data-ttu-id="7de92-123">Las observaciones sin una variable dependiente deben especificarse como "NA" para Y.</span><span class="sxs-lookup"><span data-stu-id="7de92-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="7de92-124">Los datos de entrada para el conjunto de datos anterior serían los siguientes: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span><span class="sxs-lookup"><span data-stu-id="7de92-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="7de92-125">El resultado es el valor de predicción para cada una de las filas en función de las variables independientes.</span><span class="sxs-lookup"><span data-stu-id="7de92-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="7de92-126">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="7de92-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="7de92-127">Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)se puede ver una aplicación de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="7de92-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="7de92-128">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="7de92-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="7de92-129">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="7de92-129">Creation of web service</span></span>
> <span data-ttu-id="7de92-130">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="7de92-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="7de92-131">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="7de92-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="7de92-132">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="7de92-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="7de92-133">En Machine Learning de Azure se creó un nuevo experimento en blanco y se extrajeron dos módulos [Ejecutar scripts R][execute-r-script] en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7de92-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="7de92-134">Este servicio web ejecuta un experimento de Aprendizaje automático de Azure con un script de R subyacente.</span><span class="sxs-lookup"><span data-stu-id="7de92-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="7de92-135">Hay dos partes para este experimento: definición de esquema y modelo de aprendizaje + puntuación.</span><span class="sxs-lookup"><span data-stu-id="7de92-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="7de92-136">El primer módulo define la estructura esperada del conjunto de datos de entrada, donde la primera variable es la variable dependiente y las demás variables son independientes.</span><span class="sxs-lookup"><span data-stu-id="7de92-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="7de92-137">El segundo módulo ajusta un modelo de regresión logística genérico para los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="7de92-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Flujo de experimento][2]

#### <a name="module-1"></a><span data-ttu-id="7de92-139">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="7de92-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="7de92-140">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="7de92-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="7de92-141">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="7de92-141">Limitations</span></span>
<span data-ttu-id="7de92-142">Se trata de un ejemplo muy sencillo de un servicio web de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="7de92-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="7de92-143">Como puede observarse en el código de ejemplo anterior, no se implementa ninguna detección de errores y el servicio asume que todo es una variable binaria o continua (ninguna característica categórica permitida), ya que el servicio solo recibe valores numéricos en el momento de la creación de este servicio web.</span><span class="sxs-lookup"><span data-stu-id="7de92-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="7de92-144">Además, el servicio actualmente controla el tamaño de datos limitado, debido a la naturaleza de solicitud y respuesta de la llamada al servicio web y el hecho de que el modelo se ajusta cada vez que se llama al servicio web.</span><span class="sxs-lookup"><span data-stu-id="7de92-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="7de92-145">P+F</span><span class="sxs-lookup"><span data-stu-id="7de92-145">FAQ</span></span>
<span data-ttu-id="7de92-146">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="7de92-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

