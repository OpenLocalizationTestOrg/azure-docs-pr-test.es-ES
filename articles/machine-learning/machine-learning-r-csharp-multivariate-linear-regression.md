---
title: "(En desuso) Regresión lineal multivariada - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="aa483-103">(En desuso) Regresión lineal multivariada</span><span class="sxs-lookup"><span data-stu-id="aa483-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="aa483-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="aa483-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="aa483-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="aa483-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="aa483-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="aa483-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="aa483-107">Suponga que tiene un conjunto de datos y desea predecir rápidamente una variable dependiente (y) para cada individuo (i) en función de las variables independientes.</span><span class="sxs-lookup"><span data-stu-id="aa483-107">Suppose you have a dataset and would like to quickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="aa483-108">La regresión lineal es una técnica estadística popular utilizada para tales predicciones.</span><span class="sxs-lookup"><span data-stu-id="aa483-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="aa483-109">En este caso, se supone que la variable dependiente y es un valor continuo.</span><span class="sxs-lookup"><span data-stu-id="aa483-109">Here the dependent variable y is assumed to be a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="aa483-110">Un escenario sencillo podría ser aquel en el que el investigador intenta predecir el peso de un individuo (y) en función de su altura (x).</span><span class="sxs-lookup"><span data-stu-id="aa483-110">A simple scenario could be where the researcher is trying to predict the weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="aa483-111">Un escenario más avanzado podría ser aquel en el que el investigador tiene información adicional sobre el individuo (por ejemplo, peso, sexo y raza) e intenta predecir el peso del individuo.</span><span class="sxs-lookup"><span data-stu-id="aa483-111">A more advanced scenario could be where the researcher has additional information for the individual (such as weight, gender, race) and attempts to predict the weight of the individual.</span></span> <span data-ttu-id="aa483-112">Este [servicio web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) ajusta el modelo de regresión lineal a los datos y calcula el valor previsto (y) para cada una de las observaciones de los datos.</span><span class="sxs-lookup"><span data-stu-id="aa483-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits the linear regression model to the data and outputs the predicted value (y) for each of the observations in the data.</span></span>

> <span data-ttu-id="aa483-113">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="aa483-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="aa483-114">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="aa483-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="aa483-115">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="aa483-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="aa483-116">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="aa483-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="aa483-117">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="aa483-117">Consumption of web service</span></span>
<span data-ttu-id="aa483-118">Este servicio web proporciona los valores de predicción de la variable dependiente según las variables independientes para todas las observaciones.</span><span class="sxs-lookup"><span data-stu-id="aa483-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="aa483-119">El servicio web espera que el usuario final escriba sus datos como una cadena, donde las filas están separadas por comas (,) y las columnas se separan mediante punto y coma (;).</span><span class="sxs-lookup"><span data-stu-id="aa483-119">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="aa483-120">El servicio web espera 1 fila a la vez y que la primera columna sea la variable dependiente.</span><span class="sxs-lookup"><span data-stu-id="aa483-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="aa483-121">Un conjunto de datos de ejemplo podría tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="aa483-121">An example dataset could look like this:</span></span>

![Datos de ejemplo][1]

<span data-ttu-id="aa483-123">Las observaciones sin una variable dependiente deben especificarse como "NA" para Y.</span><span class="sxs-lookup"><span data-stu-id="aa483-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="aa483-124">Los datos de entrada para el conjunto de datos anterior serían los siguientes: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span><span class="sxs-lookup"><span data-stu-id="aa483-124">The data input for the above dataset would be the following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="aa483-125">El resultado es el valor de predicción para cada una de las filas en función de las variables independientes.</span><span class="sxs-lookup"><span data-stu-id="aa483-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="aa483-126">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="aa483-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="aa483-127">Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)se puede ver una aplicación de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="aa483-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="aa483-128">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="aa483-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="aa483-129">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="aa483-129">Creation of web service</span></span>
> <span data-ttu-id="aa483-130">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa483-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="aa483-131">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="aa483-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="aa483-132">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="aa483-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="aa483-133">En Azure Machine Learning se creó un nuevo experimento en blanco y se extrajeron dos módulos [Ejecutar scripts R][execute-r-script] en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="aa483-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="aa483-134">Este servicio web ejecuta un experimento de Aprendizaje automático de Azure con un script de R subyacente.</span><span class="sxs-lookup"><span data-stu-id="aa483-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="aa483-135">Hay dos partes para este experimento: definición de esquema y modelo de aprendizaje + puntuación.</span><span class="sxs-lookup"><span data-stu-id="aa483-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="aa483-136">El primer módulo define la estructura esperada del conjunto de datos de entrada, donde la primera variable es la variable dependiente y las demás variables son independientes.</span><span class="sxs-lookup"><span data-stu-id="aa483-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="aa483-137">El segundo módulo ajusta un modelo de regresión lineal genérico para los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="aa483-137">The second module fits a generic linear regression model for the input data.</span></span>  

![Flujo de experimento][3]

#### <a name="module-1"></a><span data-ttu-id="aa483-139">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="aa483-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="aa483-140">Definición de esquema</span><span class="sxs-lookup"><span data-stu-id="aa483-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="aa483-141">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="aa483-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="aa483-142">Modelado de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="aa483-142">LM modeling</span></span>
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

## <a name="limitations"></a><span data-ttu-id="aa483-143">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="aa483-143">Limitations</span></span>
<span data-ttu-id="aa483-144">Se trata de un ejemplo muy sencillo de un servicio web de regresión lineal múltiple.</span><span class="sxs-lookup"><span data-stu-id="aa483-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="aa483-145">Como puede observarse en el código de ejemplo anterior, no se implementa ninguna detección de errores y el servicio asume que todo es una variable continua (ninguna característica categórica permitida), ya que el servicio solo recibe valores numéricos en el momento de la creación de este servicio web.</span><span class="sxs-lookup"><span data-stu-id="aa483-145">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="aa483-146">Además, el servicio actualmente controla el tamaño de datos limitado, debido a la naturaleza de solicitud y respuesta de la llamada al servicio web y el hecho de que el modelo se ajusta cada vez que se llama al servicio web.</span><span class="sxs-lookup"><span data-stu-id="aa483-146">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="aa483-147">P+F</span><span class="sxs-lookup"><span data-stu-id="aa483-147">FAQ</span></span>
<span data-ttu-id="aa483-148">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="aa483-148">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

