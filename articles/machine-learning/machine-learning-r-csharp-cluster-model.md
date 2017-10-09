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
# <a name="deprecated-cluster-model"></a>(obsoleto) Modelo de clústeres

> [!NOTE]
> Hola Microsoft DataMarket se ha retirado y esta API está en desuso. 
> 
> Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com). Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).

¿Cómo puedan se predecir grupos de comportamientos de crédito titular de la tarjeta en orden tooreduce Hola cargo desactivar riesgo de emisores de tarjeta de crédito? ¿Cómo podemos se definen grupos de rasgos de personalidad de empleados en orden tooimprove su rendimiento en el trabajo? ¿Cómo pueden los médicos clasificar pacientes en grupos basados en las características de Hola de sus enfermedades? En principio, todas estas preguntas pueden responderse mediante el análisis del clúster.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

El análisis del clúster clasifica un conjunto de observaciones en dos o más grupos desconocidos mutuamente excluyentes conforme a combinaciones de variables. Hola de análisis de clúster sirve toodiscover un sistema de la organización de observaciones, normalmente personas o sus características en grupos, donde los miembros de grupos de hello tienen propiedades en común. Esto [servicio](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) usa Hola metodología K-Means, una técnica de agrupación en clústeres utilizada, toocluster datos arbitrarios en grupos. Este servicio web toma los datos de Hola y el número de Hola de k clústeres como entrada y genera predicciones de los cuales Hola k grupos toowhich pertenece cada observaciones. 

> Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo. Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R. Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web. servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servicio web
Este servicio web agrupa datos hello en un conjunto de k grupos y salidas Hola asignación de grupo para cada fila. servicio web de Hola espera datos de tooinput de usuario final de saludo como una cadena donde filas están separadas por comas (,) y las columnas se separan mediante punto y coma (;). servicio web de Hello espera 1 fila a la vez. Un conjunto de datos de ejemplo podría tener este aspecto:

![Datos de ejemplo][1]

Suponga que Hola usuario deseado tooseparate estos datos en 3 grupos mutuamente excluyentes. Hola Hola por encima del conjunto de datos sería siguiente Hola de entrada de datos: valor = "10; 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3". salida de Hello es hello pertenencia a grupos de predicción para cada una de las filas de Hola.

> Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET. 
> 
> 

Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Inicio del código C# para el uso del servicio web:
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




## <a name="creation-of-web-service"></a>Creación del servicio web
> Este servicio web se ha creado con el Aprendizaje automático de Azure. Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.
> 
> 

Desde dentro del aprendizaje automático de Azure, un experimento en blanco nueva se crea y dos [ejecutar Script de R] [ execute-r-script] módulos extraen en el área de trabajo de Hola. esquema de datos de Hola se creó con un sencillo [ejecutar Script de R][execute-r-script]. A continuación, esquema de datos de hello estaba vinculado toohello de clúster modelo, vuelva a crear con un [ejecutar Script de R][execute-r-script]. Hola [ejecutar Script de R] [ execute-r-script] utilizado para el modelo de clústeres de hello, servicio web de hello, a continuación, utiliza función hello "k-means", que es creada previamente en hello [ejecutar Script de R] [ execute-r-script] de aprendizaje automático de Azure.    

![Flujo de experimento][3]

#### <a name="module-1"></a>Módulo 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>Módulo 2:
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


## <a name="limitations"></a>Limitaciones
Se trata de un ejemplo muy sencillo de un servicio web de agrupación en clústeres. Como se puede ver desde el código de ejemplo de Hola anterior, no se implementa la ningún error que detecte y Hola servicio supone que todo lo que es una variable continua (no hay categorías características permitidas), como Hola servicio solo entradas valores numéricos en tiempo de Hola de creación de hello de este sitio web servicio. Además, servicio Hola actualmente controla el tamaño de datos limitado, debido toohello naturaleza de solicitud/respuesta del servicio web de hello es que se va a ajustar hello y llamada de hechos que Hola modelo cada vez que se llama servicio de hello web. 

## <a name="faq"></a>P+F
Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

