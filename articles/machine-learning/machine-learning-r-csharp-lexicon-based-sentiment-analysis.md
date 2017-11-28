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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="4589b-103">(obsoleto) Análisis de sentimiento basado en léxico</span><span class="sxs-lookup"><span data-stu-id="4589b-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="4589b-104">Hola Microsoft DataMarket se ha retirado y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="4589b-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4589b-105">Puede encontrar muchas API y los experimentos de ejemplo muy útil en hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4589b-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4589b-106">Para obtener más información acerca de la Galería de hello, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4589b-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4589b-107">¿Cómo puede medir las opiniones de los usuarios y actitudes de marcas o temas de redes sociales en línea, como publicaciones en Facebook, tweets, revisiones, etc.?</span><span class="sxs-lookup"><span data-stu-id="4589b-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="4589b-108">El análisis de opiniones proporciona un método para analizar esas preguntas.</span><span class="sxs-lookup"><span data-stu-id="4589b-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4589b-109">Por lo general, hay dos métodos para el análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="4589b-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="4589b-110">Una usa un algoritmo de aprendizaje supervisado y Hola otra se puede tratar como aprendizaje no supervisada.</span><span class="sxs-lookup"><span data-stu-id="4589b-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="4589b-111">Generalmente, un algoritmo de aprendizaje supervisado genera un modelo de clasificación en un gran corpus anotado.</span><span class="sxs-lookup"><span data-stu-id="4589b-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="4589b-112">Su precisión se basa principalmente en calidad de Hola de anotación de Hola y normalmente el proceso de entrenamiento de hello tardará mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="4589b-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="4589b-113">Además de eso, cuando se aplica el dominio de tooanother del algoritmo de hello, resultado de hello normalmente no es buena.</span><span class="sxs-lookup"><span data-stu-id="4589b-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="4589b-114">En comparación con el aprendizaje de toosupervised, basado en léxico aprendizaje supervisado usa un diccionario de opinión, lo que no requiere almacenar un corpus de datos de gran tamaño y entrenamiento - lo que hace Hola todo proceso mucho más rápido.</span><span class="sxs-lookup"><span data-stu-id="4589b-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="4589b-115">Nuestro [servicio](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) se basa en hello MPQA subjetividad léxico (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), que es uno de hello suelen usada subjetividad léxicos.</span><span class="sxs-lookup"><span data-stu-id="4589b-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="4589b-116">Hay 5.097 palabras negativas y 2.533 palabras positivas en MPQA.</span><span class="sxs-lookup"><span data-stu-id="4589b-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="4589b-117">Y todas estas palabras se anotan como polaridad fuerte o débil.</span><span class="sxs-lookup"><span data-stu-id="4589b-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="4589b-118">corpus de Hello todo está bajo licencia pública General GNU.</span><span class="sxs-lookup"><span data-stu-id="4589b-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="4589b-119">servicio web de Hello puede ser frases breves de tooany aplicada, como tweets y publicaciones de Facebook.</span><span class="sxs-lookup"><span data-stu-id="4589b-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="4589b-120">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4589b-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="4589b-121">Pero Hola de servicio web de hello sirve también tooserve como un ejemplo de cómo se aprendizaje automático de Azure pueden toocreate usa los servicios web sobre el código de R.</span><span class="sxs-lookup"><span data-stu-id="4589b-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="4589b-122">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="4589b-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4589b-123">servicio web de Hola, a continuación, puede ser publicado toohello Azure Marketplace y utilizado por los usuarios y dispositivos a través de Hola a todos con ninguna instalación de infraestructura, el autor del servicio web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="4589b-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4589b-124">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="4589b-124">Consumption of web service</span></span>
<span data-ttu-id="4589b-125">datos de entrada de Hello pueden ser cualquier texto, pero el servicio web de hello funciona mejor con frases breves.</span><span class="sxs-lookup"><span data-stu-id="4589b-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="4589b-126">salida de Hello es un valor numérico entre -1 y 1.</span><span class="sxs-lookup"><span data-stu-id="4589b-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="4589b-127">Cualquier valor por debajo de 0 indica que la opinión de hello texto hello es negativo; positivo si superior a 0.</span><span class="sxs-lookup"><span data-stu-id="4589b-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="4589b-128">valor absoluto de Hola de resultado de hello denota intensidad Hola de opiniones Hola asociado.</span><span class="sxs-lookup"><span data-stu-id="4589b-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="4589b-129">Este servicio, cuando está hospedado en hello Azure Marketplace, es un servicio de OData; estos se pueden llamar a través de los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="4589b-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4589b-130">Hay varias maneras de consumo de servicio de Hola de forma automática (una aplicación de ejemplo es [aquí](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="4589b-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4589b-131">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="4589b-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="4589b-132">entrada de Hello es "Hoy es un buen día."</span><span class="sxs-lookup"><span data-stu-id="4589b-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="4589b-133">salida de Hello es "1", que indica una opinión positivo asociada oración de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4589b-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="4589b-134">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="4589b-134">Creation of web service</span></span>
> <span data-ttu-id="4589b-135">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4589b-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4589b-136">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4589b-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4589b-137">A continuación se muestra una captura de pantalla del experimento de Hola que creó el código de ejemplo y el servicio web Hola para cada uno de los módulos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4589b-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="4589b-138">Desde el Aprendizaje automático de Azure, se creó un nuevo experimento en blanco.</span><span class="sxs-lookup"><span data-stu-id="4589b-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="4589b-139">Hola siguiente ilustración muestra el flujo de experimento Hola de análisis de opiniones basado en léxico.</span><span class="sxs-lookup"><span data-stu-id="4589b-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="4589b-140">archivo de "sent_dict.csv" Hello es léxico de hello MPQA subjetividad y se configura como una de las entradas de Hola de [ejecutar Script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4589b-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="4589b-141">Otra entrada es una revisión muestreada de conjunto de datos de hello Amazon revisión de prueba, donde se realiza la selección, la modificación del nombre de columna y operaciones de división.</span><span class="sxs-lookup"><span data-stu-id="4589b-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="4589b-142">Utilizamos un léxico hash paquete toostore Hola subjetividad en la memoria de Hola y acelerar el proceso de cálculo de puntuación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4589b-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="4589b-143">texto completo de Hola se acorta por paquete de "tm" y en comparación con la palabra Hola en el diccionario de opiniones Hola.</span><span class="sxs-lookup"><span data-stu-id="4589b-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="4589b-144">Por último, se calculará una puntuación mediante la adición de peso de Hola de cada palabra subjetiva en texto hello.</span><span class="sxs-lookup"><span data-stu-id="4589b-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="4589b-145">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="4589b-145">Experiment flow:</span></span>
![flujo de experimento][2]

#### <a name="module-1"></a><span data-ttu-id="4589b-147">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="4589b-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="4589b-148">Instalación del paquete hash</span><span class="sxs-lookup"><span data-stu-id="4589b-148">Install hash package</span></span>
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



## <a name="limitations"></a><span data-ttu-id="4589b-149">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="4589b-149">Limitations</span></span>
<span data-ttu-id="4589b-150">Desde una perspectiva de algoritmo, análisis de opiniones basado en léxico es una herramienta de análisis de opiniones general, no puede funcionar mejor que el método de clasificación de Hola para campos específicos.</span><span class="sxs-lookup"><span data-stu-id="4589b-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="4589b-151">problema de negación de Hello no se aborda también.</span><span class="sxs-lookup"><span data-stu-id="4589b-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="4589b-152">Codificamos varias palabras de negación en nuestro programa, pero una mejor manera es usar un diccionario de negación y crear algunas reglas.</span><span class="sxs-lookup"><span data-stu-id="4589b-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="4589b-153">servicio web de Hello funciona mejor en frases cortos y sencillas, como tweets y publicaciones de Facebook, que en frases más largas y complejas como las revisiones de Amazon.</span><span class="sxs-lookup"><span data-stu-id="4589b-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="4589b-154">P+F</span><span class="sxs-lookup"><span data-stu-id="4589b-154">FAQ</span></span>
<span data-ttu-id="4589b-155">Para las preguntas más frecuentes en el consumo del servicio web de Hola o publicación toohello Azure Marketplace, vea [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4589b-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


