---
title: "(en desuso) Análisis de supervivencia con Azure Machine Learning | Microsoft Docs"
description: "(en desuso) Probabilidad de aparición de eventos de análisis de supervivencia"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="a2dec-103">(en desuso) Análisis de supervivencia</span><span class="sxs-lookup"><span data-stu-id="a2dec-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="a2dec-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="a2dec-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="a2dec-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="a2dec-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="a2dec-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="a2dec-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="a2dec-107">En muchos escenarios, el resultado principal de la evaluación es el momento en que se producirá un evento de interés.</span><span class="sxs-lookup"><span data-stu-id="a2dec-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="a2dec-108">En otras palabras, se plantea la pregunta </span><span class="sxs-lookup"><span data-stu-id="a2dec-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="a2dec-109">"¿cuándo se producirá este evento?"</span><span class="sxs-lookup"><span data-stu-id="a2dec-109">is asked.</span></span> <span data-ttu-id="a2dec-110">Como ejemplos, tenga en cuenta las situaciones donde los datos describen el tiempo transcurrido (días, años, kilometraje, etc.) hasta que el evento de interés (recaída de la enfermedad, grado de doctorado recibido o pastillas de freno estropeadas) se produce.</span><span class="sxs-lookup"><span data-stu-id="a2dec-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="a2dec-111">Cada instancia de los datos representa un objeto específico (un paciente, un alumno, un automóvil, etc.).</span><span class="sxs-lookup"><span data-stu-id="a2dec-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="a2dec-112">Este [servicio web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) responde a la pregunta "¿qué probabilidad hay de que el evento de interés se produzca en el momento n para el objeto x?".</span><span class="sxs-lookup"><span data-stu-id="a2dec-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="a2dec-113">Al proporcionar un modelo de análisis de supervivencia, este servicio web permite a los usuarios proporcionar datos para entrenar el modelo y probarlo.</span><span class="sxs-lookup"><span data-stu-id="a2dec-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="a2dec-114">El tema principal del experimento es modelar la duración del tiempo que transcurre hasta que se produzca el evento de interés.</span><span class="sxs-lookup"><span data-stu-id="a2dec-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="a2dec-115">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a2dec-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="a2dec-116">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="a2dec-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="a2dec-117">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="a2dec-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="a2dec-118">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="a2dec-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="a2dec-119">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="a2dec-119">Consumption of web service</span></span>
<span data-ttu-id="a2dec-120">El esquema de datos de entrada del servicio web se muestra en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="a2dec-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="a2dec-121">Se necesitan seis elementos de información como entrada: los datos de aprendizaje, los datos de prueba, el tiempo de interés, el índice de la dimensión de "tiempo", el índice de la dimensión de "evento" y los tipos de variables (continua o factor).</span><span class="sxs-lookup"><span data-stu-id="a2dec-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="a2dec-122">Los datos de aprendizaje se representan con una cadena, donde las filas están separadas por comas y las columnas están separadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="a2dec-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="a2dec-123">El número de características de los datos es flexible.</span><span class="sxs-lookup"><span data-stu-id="a2dec-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="a2dec-124">Todos los elementos de la cadena de entrada deben ser numéricos.</span><span class="sxs-lookup"><span data-stu-id="a2dec-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="a2dec-125">En los datos de aprendizaje, la dimensión de "tiempo" indica que el número de unidades de tiempo (días, años, kilometraje, etc.) transcurrido desde el inicio del estudio (un paciente recibe los programas de tratamiento contra el consumo de drogas, un alumno que empieza el doctorado, un automóvil que empieza a conducirse, etc.) hasta que se produce el evento de interés (el paciente vuelve a consumir droga, el alumno obtiene el título de doctorado, el vehículo presenta desgaste de las pastillas de freno, etc.).</span><span class="sxs-lookup"><span data-stu-id="a2dec-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="a2dec-126">La dimensión de "evento" indica si se produce el evento de interés al final del estudio.</span><span class="sxs-lookup"><span data-stu-id="a2dec-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="a2dec-127">El valor "evento = 1" significa que se produce el evento de interés en el momento indicado por la dimensión de "tiempo"; mientras que "evento = 0" significa que el evento de interés no se ha producido todavía en el momento indicado por la dimensión de "tiempo".</span><span class="sxs-lookup"><span data-stu-id="a2dec-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="a2dec-128">trainingdata: una cadena de caracteres</span><span class="sxs-lookup"><span data-stu-id="a2dec-128">trainingdata - A character string.</span></span> <span data-ttu-id="a2dec-129">Las filas están separadas por coma y las columnas están separadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="a2dec-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="a2dec-130">Cada fila incluye la dimensión de "tiempo", la dimensión de "evento" y las variables del previsor.</span><span class="sxs-lookup"><span data-stu-id="a2dec-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="a2dec-131">testingdata: una fila de datos que contiene variables del previsor para un objeto determinado.</span><span class="sxs-lookup"><span data-stu-id="a2dec-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="a2dec-132">time_of_interest: el tiempo transcurrido de interés n.</span><span class="sxs-lookup"><span data-stu-id="a2dec-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="a2dec-133">index_time: el índice de columna de la dimensión de "tiempo" (a partir de 1)</span><span class="sxs-lookup"><span data-stu-id="a2dec-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="a2dec-134">index_event: el índice de columna de la dimensión de "evento" (a partir de 1)</span><span class="sxs-lookup"><span data-stu-id="a2dec-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="a2dec-135">variable_types: una cadena de caracteres con punto y coma como separadores.</span><span class="sxs-lookup"><span data-stu-id="a2dec-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="a2dec-136">0 representa variables continuas y 1 representa variables factor.</span><span class="sxs-lookup"><span data-stu-id="a2dec-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="a2dec-137">El resultado es la probabilidad de que un evento se produzca en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="a2dec-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="a2dec-138">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="a2dec-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="a2dec-139">Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)se puede ver una aplicación de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="a2dec-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="a2dec-140">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="a2dec-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="a2dec-141">Esta prueba se interpreta de la siguiente forma.</span><span class="sxs-lookup"><span data-stu-id="a2dec-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="a2dec-142">Supongamos que el objetivo de los datos es modelar el tiempo transcurrido hasta que los pacientes sometidos a algunos de los dos programas de tratamiento contra las drogas vuelven a consumir drogas.</span><span class="sxs-lookup"><span data-stu-id="a2dec-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="a2dec-143">El resultado del servicio web es: para pacientes de 35 años, que se han sometido dos veces a un tratamiento anterior contra el consumo de drogas, con un largo programa de tratamiento residencial y que consumían heroína y cocaína, la probabilidad de volver a consumir drogas es del 95,64 % el día 500.</span><span class="sxs-lookup"><span data-stu-id="a2dec-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="a2dec-144">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="a2dec-144">Creation of web service</span></span>
> <span data-ttu-id="a2dec-145">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2dec-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="a2dec-146">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="a2dec-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="a2dec-147">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="a2dec-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="a2dec-148">En Azure Machine Learning se creó un nuevo experimento en blanco y se extrajeron dos módulos [Ejecutar scripts R][execute-r-script] en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a2dec-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="a2dec-149">El esquema de datos se creó con un módulo [Ejecutar script R][execute-r-script] sencillo, que define el esquema de datos de entrada para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="a2dec-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="a2dec-150">Este módulo está vinculado al segundo módulo [Ejecutar script R][execute-r-script], que hace la mayor parte del trabajo.</span><span class="sxs-lookup"><span data-stu-id="a2dec-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="a2dec-151">Este módulo realiza el preprocesamiento de datos, la creación de modelos y las previsiones.</span><span class="sxs-lookup"><span data-stu-id="a2dec-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="a2dec-152">En el paso del preprocesamiento de los datos, los datos de entrada representados por una cadena larga se transforman y convierten en una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="a2dec-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="a2dec-153">En el paso de creación del modelo, un paquete R externo "survival_2.37 7.zip" se instala en primer lugar para llevar a cabo el análisis de supervivencia.</span><span class="sxs-lookup"><span data-stu-id="a2dec-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="a2dec-154">A continuación, se ejecuta la función "coxph" después de una serie de tareas de procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="a2dec-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="a2dec-155">Se pueden leer los detalles de la función "coxph" para el análisis de supervivencia en la documentación de R.</span><span class="sxs-lookup"><span data-stu-id="a2dec-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="a2dec-156">En el paso de previsión, se proporciona una instancia de prueba en el modelo de entrenado con la función "surfit", y la curva de supervivencia para esta instancia de prueba se genera como variable "curva".</span><span class="sxs-lookup"><span data-stu-id="a2dec-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="a2dec-157">Por último, se obtiene la probabilidad del tiempo de interés.</span><span class="sxs-lookup"><span data-stu-id="a2dec-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="a2dec-158">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="a2dec-158">Experiment flow:</span></span>
![flujo de experimento][1]

#### <a name="module-1"></a><span data-ttu-id="a2dec-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="a2dec-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="a2dec-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="a2dec-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="a2dec-162">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="a2dec-162">Limitations</span></span>
<span data-ttu-id="a2dec-163">Este servicio web solo puede aceptar valores numéricos como variables de característica (columnas).</span><span class="sxs-lookup"><span data-stu-id="a2dec-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="a2dec-164">La columna "evento" solo puede aceptar el valor 0 o 1.</span><span class="sxs-lookup"><span data-stu-id="a2dec-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="a2dec-165">La columna "tiempo" debe ser un entero positivo.</span><span class="sxs-lookup"><span data-stu-id="a2dec-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="a2dec-166">P+F</span><span class="sxs-lookup"><span data-stu-id="a2dec-166">FAQ</span></span>
<span data-ttu-id="a2dec-167">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a2dec-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

