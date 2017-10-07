---
title: aaa(deprecated) clasificador binario - Azure | Documentos de Microsoft
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
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a>(obsoleto) Clasificador binario

> [!NOTE]
> Hola Microsoft DataMarket se ha retirado y esta API está en desuso. 
> 
> Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com). Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).

Suponga que tiene un conjunto de datos y desea que una variable dependiente binaria en función de las variables independientes de hello toopredict. La "regresión logística" es una técnica estadística popular utilizada para tales predicciones. Aquí Hola dependiente de la variable es binario o dicotómicas y p es la probabilidad de Hola de presencia de la característica de Hola de interés. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Podría ser un escenario simple donde un investigadores está tratando de toopredict si un estudiante potencial es probable que tooaccept una universidad de tooa de oferta de admisión en función de información (GPA en el Instituto, ingresos familiares, state residente, género). resultado previsto de Hello es la probabilidad de Hola de estudiante posibles Hola Aceptar oferta de admisión de Hola. Esto [servicio web](https://datamarket.azure.com/dataset/aml_labs/log_regression) encajan Hola datos de toohello del modelo de regresión logística y salidas Hola valores de probabilidad (y) para cada una de las observaciones de hello en los datos de Hola.  

> Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo. Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R. Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web. servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servicio web
Este Hola de web service proporciona predecir valores de variable dependiente de hello basadas en las variables independientes de Hola para todas las observaciones de Hola. servicio web de Hola espera datos de tooinput de usuario final de saludo como una cadena donde filas están separadas por coma (,) y las columnas se separan mediante punto y coma (;). servicio web de Hello espera 1 fila a la vez y espera Hola primera columna toobe Hola dependiente de la variable. Un conjunto de datos de ejemplo podría tener este aspecto:

![Datos de ejemplo][1]

Las observaciones sin una variable dependiente deben especificarse como "NA" para Y. Hello datos de entrada para hello por encima del conjunto de datos podría Hola después de cadena: "1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4". Hola de salida es hello valor de predicción para cada una de las filas de hello en función de hello independiente variables. 

> Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET. 
> 
> 

Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Inicio del código C# para el uso del servicio web:
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


## <a name="creation-of-web-service"></a>Creación del servicio web
> Este servicio web se ha creado con el Aprendizaje automático de Azure. Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.
> 
> 

Desde dentro del aprendizaje automático de Azure, un experimento en blanco nueva se crea y dos [ejecutar Script de R] [ execute-r-script] módulos extraen en el área de trabajo de Hola. Este servicio web ejecuta un experimento de Aprendizaje automático de Azure con un script de R subyacente. Hay 2 partes toothis experimentar: definición de esquema y el modelo de entrenamiento + la puntuación. primer módulo de Hello define la estructura de hello esperado de hello entrada conjunto de datos, donde hello primera variable es variable dependiente de Hola y Hola restantes variables son independientes. segundo módulo de Hello ajusta un modelo de regresión logística genérico para los datos de entrada de Hola.    

![Flujo de experimento][2]

#### <a name="module-1"></a>Módulo 1:
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>Módulo 2:
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


## <a name="limitations"></a>Limitaciones
Se trata de un ejemplo muy sencillo de un servicio web de clasificación binaria. Como se puede ver desde el código de ejemplo de Hola anterior, no se implementa la ningún error que detecte y Hola servicio supone que todo lo que es una variable continua/binario (no hay categorías características permitidas), como Hola servicio solo entradas valores numéricos en tiempo de Hola de creación de hello de este servicio Web. Además, servicio Hola actualmente controla el tamaño de datos limitado, debido toohello naturaleza de solicitud/respuesta del servicio web de hello es que se va a ajustar hello y llamada de hechos que Hola modelo cada vez que se llama servicio de hello web. 

## <a name="faq"></a>P+F
Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

