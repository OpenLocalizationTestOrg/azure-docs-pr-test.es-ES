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
# <a name="deprecated-survival-analysis"></a>(en desuso) Análisis de supervivencia

> [!NOTE]
> Hola Microsoft DataMarket se ha retirado y esta API está en desuso. 
> 
> Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com). Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).

En muchos escenarios, resultado principal de hello en evaluación es suceso tooan Hola de interés. En otras palabras, las preguntas de hello "Si este evento se producirá?" "¿cuándo se producirá este evento?" Como ejemplos, tenga en cuenta situaciones donde los datos de hello describen Hola tiempo (días, años, kilometraje, etc.) hasta que Hola se produce el evento de interés (relapse enfermedad, grado de doctorado recibido, frenos panel error). Cada instancia de datos de hello representa un objeto específico (un paciente, un estudiante, un automóvil, etcetera).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Esto [servicio web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) se responde Hola pregunta "¿Cuál es la probabilidad de Hola Hola eventos de interés se producen por n de tiempo para el objeto x?" Al proporcionar un modelo de análisis de supervivencia, este servicio web permite a los usuarios toosupply datos tootrain Hola modelo y la prueba. tema principal de Hello del experimento de hello es la longitud de Hola de toomodel de hello tiempo hasta que se produzca el evento de Hola de interés. 

> Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo. Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R. Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web. servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servicio web
se muestra el esquema de datos de entrada de Hello del servicio web de hello en hello en la tabla siguiente. Se necesitan seis partes de información como entrada de hello: datos de entrenamiento, datos de prueba, tiempo de interés, índice de Hola de dimensión "hora", el índice de Hola de dimensión "evento" y los tipos de variable hello (continua o factor). datos de entrenamiento de saludo se representan con una cadena, donde hello filas están separadas por comas y columnas de hello están separadas por punto y coma. número de Hola de características de los datos de hello es flexible. Todos los elementos de hello en la cadena de entrada de hello deben ser numéricos. En datos de entrenamiento de hello, dimensión de tiempo"hello" indica Hola varias unidades de tiempo (días, años, kilometraje, etc.) transcurren desde el punto de partida de Hola de hello estudiar (un paciente recibir programas de tratamiento de drogas, un estudio de doctorado inicial de estudiantes, un automóvil a partir de toobe controlado por, etcetera). hasta que hello eventos de interés (paciente de hello devolver toodrug uso, grado de hello estudiante obtención Hola doctorado, car Hola con error de controlador de frenos, etc.) se produce. dimensión de "evento" Hello indica si el evento Hola de interés se produce final Hola de estudio de Hola. Un valor de "evento = 1" significa que los eventos de interés de Hola se produce en tiempo de hello indicado por dimensión de "hora" hello; "evento = 0" significa que los eventos de interés de Hola no se ha producido por Hola de tiempo indicado por dimensión de "hora" Hola.

* trainingdata: una cadena de caracteres Las filas están separadas por coma y las columnas están separadas por punto y coma. Cada fila incluye la dimensión de "tiempo", la dimensión de "evento" y las variables del previsor.
* testingdata: una fila de datos que contiene variables del previsor para un objeto determinado.
* time_of_interest - Hola tiempo transcurrido en n de interés.
* index_time - índice de columna de Hola de dimensión de "hora" hello (a partir de 1).
* index_event - índice de columna de Hola de dimensión de "evento" hello (a partir de 1).
* variable_types: una cadena de caracteres con punto y coma como separadores. 0 representa variables continuas y 1 representa variables factor.

salida de Hello es la probabilidad de Hola de un evento que ocurra en una fecha determinada. 

> Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET. 
> 
> 

Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Inicio del código C# para el uso del servicio web:
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




interpretación de Hola de esta prueba es como sigue. Suponiendo que objetivo Hola de datos de hello toomodel Hola tiempo hasta Hola devolver toodrug uso de pacientes Hola que reciben alguno de los programas de tratamiento de hello dos. Hola salida de hello web servicio lecturas: para los pacientes que se va a 35 años de antigüedad, tener anterior fármaco tratamiento 2 veces, teniendo el programa de tratamiento residencial larga de hello, y con el uso de heroína y cocaína, probabilidad Hola de devolver el uso de fármaco toohello es 95.64% por día 500.

## <a name="creation-of-web-service"></a>Creación del servicio web
> Este servicio web se ha creado con el Aprendizaje automático de Azure. Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.
> 
> 

Desde dentro del aprendizaje automático de Azure, un experimento en blanco nueva se crea y dos [ejecutar Script de R] [ execute-r-script] módulos se extrajeron en el área de trabajo de Hola. Hello esquema de datos creado con un sencillo [ejecutar Script de R][execute-r-script], que define el esquema de datos de entrada de hello para el servicio web de Hola. Este módulo es, a continuación, vincula toohello en segundo lugar [ejecutar Script de R] [ execute-r-script] módulo, que las principales de trabajo. Este módulo realiza el preprocesamiento de datos, la creación de modelos y las previsiones. En el paso de procesamiento de datos de hello, los datos de entrada de hello representados por una cadena larga se transforman y se convierte en una trama de datos. En el paso de compilación de modelo de hello, un paquete de R externo "survival_2.37 7.zip" se instala por primera vez para llevar a cabo análisis de supervivencia. A continuación, se ejecuta la función de "coxph" de hello después de una tarea de procesamiento de datos de serie. pueden leer los detalles del Hola de función de "coxph" hello para el análisis de supervivencia de documentación de hello R. En el paso de la predicción de hello, se proporciona una instancia de prueba en entrenado Hola con función de "surfit" hello y curva de supervivencia de Hola para esta instancia de prueba se genera como variable de "curve". Por último, se obtiene la probabilidad de Hola de tiempo de Hola de interés. 

### <a name="experiment-flow"></a>Flujo de experimento:
![flujo de experimento][1]

#### <a name="module-1"></a>Módulo 1:
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

#### <a name="module-2"></a>Módulo 2:
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




## <a name="limitations"></a>Limitaciones
Este servicio web solo puede aceptar valores numéricos como variables de característica (columnas). columna de "evento" Hello acepta sólo valor 0 ó 1. columna de "hora" Hello debe toobe un número entero positivo.

## <a name="faq"></a>P+F
Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

