---
title: "aaa(deprecated) análisis de opiniones basado en léxico - Azure | Documentos de Microsoft"
description: "(obsoleto) Análisis de sentimiento basado en léxico"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(obsoleto) Análisis de sentimiento basado en léxico

> [!NOTE]
> Hola Microsoft DataMarket se ha retirado y esta API está en desuso. 
> 
> Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com). Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).

¿Cómo puede medir las opiniones de los usuarios y actitudes de marcas o temas de redes sociales en línea, como publicaciones en Facebook, tweets, revisiones, etc.? El análisis de opiniones proporciona un método para analizar esas preguntas.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Por lo general, hay dos métodos para el análisis de opiniones. Una usa un algoritmo de aprendizaje supervisado y Hola otra se puede tratar como aprendizaje no supervisada. Generalmente, un algoritmo de aprendizaje supervisado genera un modelo de clasificación en un gran corpus anotado. Su precisión se basa principalmente en calidad de Hola de anotación de Hola y normalmente el proceso de entrenamiento de hello tardará mucho tiempo. Además de eso, cuando se aplica el dominio de tooanother del algoritmo de hello, resultado de hello normalmente no es buena. En comparación con el aprendizaje de toosupervised, basado en léxico aprendizaje supervisado usa un diccionario de opinión, lo que no requiere almacenar un corpus de datos de gran tamaño y entrenamiento - lo que hace Hola todo proceso mucho más rápido. 

Nuestro [servicio](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) se basa en hello MPQA subjetividad léxico (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), que es uno de hello suelen usada subjetividad léxicos. Hay 5.097 palabras negativas y 2.533 palabras positivas en MPQA. Y todas estas palabras se anotan como polaridad fuerte o débil. corpus de Hello todo está bajo licencia pública General GNU. servicio web de Hello puede ser frases breves de tooany aplicada, como tweets y publicaciones de Facebook. 

> Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo. Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R. Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web. servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servicio web
datos de entrada de Hello pueden ser cualquier texto, pero el servicio web de hello funciona mejor con frases breves. salida de Hello es un valor numérico entre -1 y 1. Cualquier valor por debajo de 0 indica que la opinión de hello texto hello es negativo; positivo si superior a 0. valor absoluto de Hola de resultado de hello denota intensidad Hola de opiniones Hola asociado. 

> Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET. 
> 
> 

Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>Inicio del código C# para el uso del servicio web:
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



entrada de Hello es "Hoy es un buen día." salida de Hello es "1", que indica una opinión positivo asociada oración de entrada de Hola. 

## <a name="creation-of-web-service"></a>Creación del servicio web
> Este servicio web se ha creado con el Aprendizaje automático de Azure. Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.
> 
> 

Desde el Aprendizaje automático de Azure, se creó un nuevo experimento en blanco. Hola siguiente ilustración muestra el flujo de experimento Hola de análisis de opiniones basado en léxico. archivo de "sent_dict.csv" Hello es léxico de hello MPQA subjetividad y se configura como una de las entradas de Hola de [ejecutar Script de R][execute-r-script]. Otra entrada es una revisión muestreada de conjunto de datos de hello Amazon revisión de prueba, donde se realiza la selección, la modificación del nombre de columna y operaciones de división. Utilizamos un léxico hash paquete toostore Hola subjetividad en la memoria de Hola y acelerar el proceso de cálculo de puntuación de Hola. texto completo de Hola se acorta por paquete de "tm" y en comparación con la palabra Hola en el diccionario de opiniones Hola. Por último, se calculará una puntuación mediante la adición de peso de Hola de cada palabra subjetiva en texto hello. 

### <a name="experiment-flow"></a>Flujo de experimento:
![flujo de experimento][2]

#### <a name="module-1"></a>Módulo 1:
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Instalación del paquete hash
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a>Limitaciones
Desde una perspectiva de algoritmo, análisis de opiniones basado en léxico es una herramienta de análisis de opiniones general, no puede funcionar mejor que el método de clasificación de Hola para campos específicos. problema de negación de Hello no se aborda también. Codificamos varias palabras de negación en nuestro programa, pero una mejor manera es usar un diccionario de negación y crear algunas reglas. servicio web de Hello funciona mejor en frases cortos y sencillas, como tweets y publicaciones de Facebook, que en frases más largas y complejas como las revisiones de Amazon. 

## <a name="faq"></a>P+F
Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


