---
title: "aaa(deprecated) análisis de supervivencia con aprendizaje automático de Azure | Documentos de Microsoft"
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
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="87d24-103">(en desuso) Análisis de supervivencia</span><span class="sxs-lookup"><span data-stu-id="87d24-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="87d24-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="87d24-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="87d24-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="87d24-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="87d24-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="87d24-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="87d24-107">En muchos escenarios, resultado principal de hello en evaluación es suceso tooan Hola de interés.</span><span class="sxs-lookup"><span data-stu-id="87d24-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="87d24-108">En otras palabras, las preguntas de hello "Si este evento se producirá?"</span><span class="sxs-lookup"><span data-stu-id="87d24-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="87d24-109">"¿cuándo se producirá este evento?"</span><span class="sxs-lookup"><span data-stu-id="87d24-109">is asked.</span></span> <span data-ttu-id="87d24-110">Como ejemplos, tenga en cuenta situaciones donde los datos de hello describen Hola tiempo (días, años, kilometraje, etc.) hasta que Hola se produce el evento de interés (relapse enfermedad, grado de doctorado recibido, frenos panel error).</span><span class="sxs-lookup"><span data-stu-id="87d24-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="87d24-111">Cada instancia de datos de hello representa un objeto específico (un paciente, un estudiante, un automóvil, etcetera).</span><span class="sxs-lookup"><span data-stu-id="87d24-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="87d24-112">Esto [servicio web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) se responde Hola pregunta "¿Cuál es la probabilidad de Hola Hola eventos de interés se producen por n de tiempo para el objeto x?"</span><span class="sxs-lookup"><span data-stu-id="87d24-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="87d24-113">Al proporcionar un modelo de análisis de supervivencia, este servicio web permite a los usuarios toosupply datos tootrain Hola modelo y la prueba.</span><span class="sxs-lookup"><span data-stu-id="87d24-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="87d24-114">tema principal de Hello del experimento de hello es la longitud de Hola de toomodel de hello tiempo hasta que se produzca el evento de Hola de interés.</span><span class="sxs-lookup"><span data-stu-id="87d24-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="87d24-115">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="87d24-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="87d24-116">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="87d24-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="87d24-117">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="87d24-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="87d24-118">servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="87d24-119">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="87d24-119">Consumption of web service</span></span>
<span data-ttu-id="87d24-120">se muestra el esquema de datos de entrada de Hello del servicio web de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="87d24-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="87d24-121">Se necesitan seis partes de información como entrada de hello: datos de entrenamiento, datos de prueba, tiempo de interés, índice de Hola de dimensión "hora", el índice de Hola de dimensión "evento" y los tipos de variable hello (continua o factor).</span><span class="sxs-lookup"><span data-stu-id="87d24-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="87d24-122">datos de entrenamiento de saludo se representan con una cadena, donde hello filas están separadas por comas y columnas de hello están separadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="87d24-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="87d24-123">número de Hola de características de los datos de hello es flexible.</span><span class="sxs-lookup"><span data-stu-id="87d24-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="87d24-124">Todos los elementos de hello en la cadena de entrada de hello deben ser numéricos.</span><span class="sxs-lookup"><span data-stu-id="87d24-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="87d24-125">En datos de entrenamiento de hello, dimensión de tiempo"hello" indica Hola varias unidades de tiempo (días, años, kilometraje, etc.) transcurren desde el punto de partida de Hola de hello estudiar (un paciente recibir programas de tratamiento de drogas, un estudio de doctorado inicial de estudiantes, un automóvil a partir de toobe controlado por, etcetera). hasta que hello eventos de interés (paciente de hello devolver toodrug uso, grado de hello estudiante obtención Hola doctorado, car Hola con error de controlador de frenos, etc.) se produce.</span><span class="sxs-lookup"><span data-stu-id="87d24-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="87d24-126">dimensión de "evento" Hello indica si el evento Hola de interés se produce final Hola de estudio de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="87d24-127">Un valor de "evento = 1" significa que los eventos de interés de Hola se produce en tiempo de hello indicado por dimensión de "hora" hello; "evento = 0" significa que los eventos de interés de Hola no se ha producido por Hola de tiempo indicado por dimensión de "hora" Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="87d24-128">trainingdata: una cadena de caracteres</span><span class="sxs-lookup"><span data-stu-id="87d24-128">trainingdata - A character string.</span></span> <span data-ttu-id="87d24-129">Las filas están separadas por coma y las columnas están separadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="87d24-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="87d24-130">Cada fila incluye la dimensión de "tiempo", la dimensión de "evento" y las variables del previsor.</span><span class="sxs-lookup"><span data-stu-id="87d24-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="87d24-131">testingdata: una fila de datos que contiene variables del previsor para un objeto determinado.</span><span class="sxs-lookup"><span data-stu-id="87d24-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="87d24-132">time_of_interest - Hola tiempo transcurrido en n de interés.</span><span class="sxs-lookup"><span data-stu-id="87d24-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="87d24-133">index_time - índice de columna de Hola de dimensión de "hora" hello (a partir de 1).</span><span class="sxs-lookup"><span data-stu-id="87d24-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="87d24-134">index_event - índice de columna de Hola de dimensión de "evento" hello (a partir de 1).</span><span class="sxs-lookup"><span data-stu-id="87d24-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="87d24-135">variable_types: una cadena de caracteres con punto y coma como separadores.</span><span class="sxs-lookup"><span data-stu-id="87d24-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="87d24-136">0 representa variables continuas y 1 representa variables factor.</span><span class="sxs-lookup"><span data-stu-id="87d24-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="87d24-137">salida de Hello es la probabilidad de Hola de un evento que ocurra en una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="87d24-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="87d24-138">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="87d24-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="87d24-139">Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="87d24-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="87d24-140">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="87d24-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="87d24-141">interpretación de Hola de esta prueba es como sigue.</span><span class="sxs-lookup"><span data-stu-id="87d24-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="87d24-142">Suponiendo que objetivo Hola de datos de hello toomodel Hola tiempo hasta Hola devolver toodrug uso de pacientes Hola que reciben alguno de los programas de tratamiento de hello dos.</span><span class="sxs-lookup"><span data-stu-id="87d24-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="87d24-143">Hola salida de hello web servicio lecturas: para los pacientes que se va a 35 años de antigüedad, tener anterior fármaco tratamiento 2 veces, teniendo el programa de tratamiento residencial larga de hello, y con el uso de heroína y cocaína, probabilidad Hola de devolver el uso de fármaco toohello es 95.64% por día 500.</span><span class="sxs-lookup"><span data-stu-id="87d24-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="87d24-144">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="87d24-144">Creation of web service</span></span>
> <span data-ttu-id="87d24-145">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="87d24-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="87d24-146">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="87d24-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="87d24-147">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="87d24-148">Desde dentro del aprendizaje automático de Azure, un experimento en blanco nueva se crea y dos [ejecutar Script de R] [ execute-r-script] módulos se extrajeron en el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="87d24-149">Hello esquema de datos creado con un sencillo [ejecutar Script de R][execute-r-script], que define el esquema de datos de entrada de hello para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="87d24-150">Este módulo es, a continuación, vincula toohello en segundo lugar [ejecutar Script de R] [ execute-r-script] módulo, que las principales de trabajo.</span><span class="sxs-lookup"><span data-stu-id="87d24-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="87d24-151">Este módulo realiza el preprocesamiento de datos, la creación de modelos y las previsiones.</span><span class="sxs-lookup"><span data-stu-id="87d24-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="87d24-152">En el paso de procesamiento de datos de hello, los datos de entrada de hello representados por una cadena larga se transforman y se convierte en una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="87d24-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="87d24-153">En el paso de compilación de modelo de hello, un paquete de R externo "survival_2.37 7.zip" se instala por primera vez para llevar a cabo análisis de supervivencia.</span><span class="sxs-lookup"><span data-stu-id="87d24-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="87d24-154">A continuación, se ejecuta la función de "coxph" de hello después de una tarea de procesamiento de datos de serie.</span><span class="sxs-lookup"><span data-stu-id="87d24-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="87d24-155">pueden leer los detalles del Hola de función de "coxph" hello para el análisis de supervivencia de documentación de hello R.</span><span class="sxs-lookup"><span data-stu-id="87d24-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="87d24-156">En el paso de la predicción de hello, se proporciona una instancia de prueba en entrenado Hola con función de "surfit" hello y curva de supervivencia de Hola para esta instancia de prueba se genera como variable de "curve".</span><span class="sxs-lookup"><span data-stu-id="87d24-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="87d24-157">Por último, se obtiene la probabilidad de Hola de tiempo de Hola de interés.</span><span class="sxs-lookup"><span data-stu-id="87d24-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="87d24-158">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="87d24-158">Experiment flow:</span></span>
![flujo de experimento][1]

#### <a name="module-1"></a><span data-ttu-id="87d24-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="87d24-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="87d24-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="87d24-161">Module 2:</span></span>
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

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
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

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
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

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="87d24-162">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="87d24-162">Limitations</span></span>
<span data-ttu-id="87d24-163">Este servicio web solo puede aceptar valores numéricos como variables de característica (columnas).</span><span class="sxs-lookup"><span data-stu-id="87d24-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="87d24-164">columna de "evento" Hello acepta sólo valor 0 ó 1.</span><span class="sxs-lookup"><span data-stu-id="87d24-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="87d24-165">columna de "hora" Hello debe toobe un número entero positivo.</span><span class="sxs-lookup"><span data-stu-id="87d24-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="87d24-166">P+F</span><span class="sxs-lookup"><span data-stu-id="87d24-166">FAQ</span></span>
<span data-ttu-id="87d24-167">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="87d24-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

