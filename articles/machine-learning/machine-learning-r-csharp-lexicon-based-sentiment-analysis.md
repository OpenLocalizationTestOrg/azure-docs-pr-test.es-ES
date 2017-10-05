---
title: "(obsoleto) Análisis de sentimiento basado en léxico - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7bc80a1e1067296528eca1a843ea30b0c27af616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="e0b24-103">(obsoleto) Análisis de sentimiento basado en léxico</span><span class="sxs-lookup"><span data-stu-id="e0b24-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="e0b24-104">Microsoft DataMarket está en proceso de retirada y esta API está en desuso.</span><span class="sxs-lookup"><span data-stu-id="e0b24-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="e0b24-105">Puede encontrar muchos experimentos y API de ejemplo útiles en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="e0b24-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="e0b24-106">Para más información sobre la Galería, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="e0b24-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="e0b24-107">¿Cómo puede medir las opiniones de los usuarios y actitudes de marcas o temas de redes sociales en línea, como publicaciones en Facebook, tweets, revisiones, etc.?</span><span class="sxs-lookup"><span data-stu-id="e0b24-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="e0b24-108">El análisis de opiniones proporciona un método para analizar esas preguntas.</span><span class="sxs-lookup"><span data-stu-id="e0b24-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e0b24-109">Por lo general, hay dos métodos para el análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="e0b24-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="e0b24-110">Uno es usar un algoritmo de aprendizaje supervisado y el otro se puede tratar como aprendizaje no supervisado.</span><span class="sxs-lookup"><span data-stu-id="e0b24-110">One is using a supervised learning algorithm, and the other can be treated as unsupervised learning.</span></span> <span data-ttu-id="e0b24-111">Generalmente, un algoritmo de aprendizaje supervisado genera un modelo de clasificación en un gran corpus anotado.</span><span class="sxs-lookup"><span data-stu-id="e0b24-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="e0b24-112">La precisión se basa principalmente en la calidad de la anotación y normalmente el proceso de entrenamiento tardará mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="e0b24-112">Its accuracy is mainly based on the quality of the annotation, and usually the training process will take a long time.</span></span> <span data-ttu-id="e0b24-113">Además de eso, cuando se aplica el algoritmo a otro dominio, el resultado normalmente no es bueno.</span><span class="sxs-lookup"><span data-stu-id="e0b24-113">Besides that, when we apply the algorithm to another domain, the result is usually not good.</span></span> <span data-ttu-id="e0b24-114">En comparación con el aprendizaje supervisado, el aprendizaje no supervisado basado en léxico usa un diccionario de opinión, que no requiere almacenar un grand conjunto de datos ni aprendizaje, lo que hace que todo el proceso sea mucho más rápido.</span><span class="sxs-lookup"><span data-stu-id="e0b24-114">Compared to supervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes the whole process much faster.</span></span> 

<span data-ttu-id="e0b24-115">Nuestro [servicio](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) se basa en el léxico de subjetividad de MPQA (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), que es uno de los lexicones de subjetividad más usados.</span><span class="sxs-lookup"><span data-stu-id="e0b24-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on the MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of the most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="e0b24-116">Hay 5.097 palabras negativas y 2.533 palabras positivas en MPQA.</span><span class="sxs-lookup"><span data-stu-id="e0b24-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="e0b24-117">Y todas estas palabras se anotan como polaridad fuerte o débil.</span><span class="sxs-lookup"><span data-stu-id="e0b24-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="e0b24-118">El conjunto completo está sujeto a la licencia pública general GNU.</span><span class="sxs-lookup"><span data-stu-id="e0b24-118">The whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="e0b24-119">El servicio web puede aplicarse a cualquier frase corta, como tweets y publicaciones de Facebook.</span><span class="sxs-lookup"><span data-stu-id="e0b24-119">The web service can be applied to any short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="e0b24-120">Este servicio web puede ser consumido por los usuarios; posiblemente a través de una aplicación móvil, a través de un sitio web o incluso en un equipo local, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e0b24-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="e0b24-121">Pero el objetivo del servicio web también es actuar como un ejemplo de cómo se puede usar Aprendizaje automático de Azure para crear servicios web encima del código R.</span><span class="sxs-lookup"><span data-stu-id="e0b24-121">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="e0b24-122">Con tan solo unas líneas de código R y algunos clics en un botón en Estudio de aprendizaje automático de Microsoft Azure, puede crear un experimento con código R y publicarlo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="e0b24-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="e0b24-123">A continuación, el servicio web se puede publicar en Azure Marketplace para que lo puedan usar usuarios y dispositivos en todo el mundo sin necesidad de que el autor del servicio web configure la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="e0b24-123">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="e0b24-124">Uso del servicio web</span><span class="sxs-lookup"><span data-stu-id="e0b24-124">Consumption of web service</span></span>
<span data-ttu-id="e0b24-125">Se puede utilizar cualquier texto como datos de entrada, pero el servicio web funciona mejor con frases cortas.</span><span class="sxs-lookup"><span data-stu-id="e0b24-125">The input data can be any text, but the web service works better with short sentences.</span></span> <span data-ttu-id="e0b24-126">El resultado es un valor numérico entre -1 y 1.</span><span class="sxs-lookup"><span data-stu-id="e0b24-126">The output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="e0b24-127">Cualquier valor por debajo de 0 indica que la opinión del texto es negativa; positiva si es superior a 0.</span><span class="sxs-lookup"><span data-stu-id="e0b24-127">Any value below 0 denotes that the sentiment of the text is negative; positive if above 0.</span></span> <span data-ttu-id="e0b24-128">El valor absoluto del resultado indica la intensidad de la opinión asociada.</span><span class="sxs-lookup"><span data-stu-id="e0b24-128">The absolute value of the result denotes the strength of the associated sentiment.</span></span> 

> <span data-ttu-id="e0b24-129">Este servicio cuando está hospedado en Azure Marketplace es un servicio de OData, al que se puede llamar mediante los métodos POST o GET.</span><span class="sxs-lookup"><span data-stu-id="e0b24-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="e0b24-130">Hay varias maneras de consumir el servicio de forma automática ( [aquí](http://microsoftazuremachinelearning.azurewebsites.net/)se puede ver una aplicación de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="e0b24-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="e0b24-131">Inicio del código C# para el uso del servicio web:</span><span class="sxs-lookup"><span data-stu-id="e0b24-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="e0b24-132">La entrada es "Hoy es un buen día".</span><span class="sxs-lookup"><span data-stu-id="e0b24-132">The input is “Today is a good day.”</span></span> <span data-ttu-id="e0b24-133">El resultado es "1", que indica la idea positiva asociada a la frase de entrada.</span><span class="sxs-lookup"><span data-stu-id="e0b24-133">The output is “1”, which indicates a positive sentiment associated with the input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="e0b24-134">Creación del servicio web</span><span class="sxs-lookup"><span data-stu-id="e0b24-134">Creation of web service</span></span>
> <span data-ttu-id="e0b24-135">Este servicio web se ha creado con el Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b24-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="e0b24-136">Para obtener acceso a una evaluación gratuita y a vídeos introductorios sobre la creación de experimentos y la [publicación de servicios web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="e0b24-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="e0b24-137">A continuación se muestra una captura de pantalla del experimento que creó el código de ejemplo y el servicio web para cada uno de los módulos dentro del experimento.</span><span class="sxs-lookup"><span data-stu-id="e0b24-137">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="e0b24-138">Desde el Aprendizaje automático de Azure, se creó un nuevo experimento en blanco.</span><span class="sxs-lookup"><span data-stu-id="e0b24-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="e0b24-139">En la siguiente ilustración se muestra el flujo de experimento del análisis de opiniones basado en léxico.</span><span class="sxs-lookup"><span data-stu-id="e0b24-139">The figure below shows the experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="e0b24-140">El archivo "sent_dict.csv" es el léxico de subjetividad de MPQA y está establecido como una de las entradas de [Ejecutar scripts R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="e0b24-140">The “sent_dict.csv” file is the MPQA subjectivity lexicon, and is set as one of the inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="e0b24-141">Otra entrada es una revisión muestreada del conjunto de datos de revisión de Amazon para pruebas, donde se realizan la selección, la modificación del nombre de columna y las operaciones de separación.</span><span class="sxs-lookup"><span data-stu-id="e0b24-141">Another input is a sampled review from the Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="e0b24-142">Usamos un paquete de hash para almacenar el léxico de subjetividad en la memoria y acelerar el proceso de cálculo de la puntuación.</span><span class="sxs-lookup"><span data-stu-id="e0b24-142">We use a hash package to store the subjectivity lexicon in the memory and accelerate the score computation process.</span></span> <span data-ttu-id="e0b24-143">Todo el texto se acortará con el paquete "tm" y se comparará con la palabra del diccionario de opiniones.</span><span class="sxs-lookup"><span data-stu-id="e0b24-143">The whole text will be tokenized by “tm” package and compared with the word in the sentiment dictionary.</span></span> <span data-ttu-id="e0b24-144">Por último, se calculará una puntuación agregando la ponderación de cada palabra subjetiva del texto.</span><span class="sxs-lookup"><span data-stu-id="e0b24-144">Finally, a score will be calculated by adding the weight of each subjective word in the text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="e0b24-145">Flujo de experimento:</span><span class="sxs-lookup"><span data-stu-id="e0b24-145">Experiment flow:</span></span>
![flujo de experimento][2]

#### <a name="module-1"></a><span data-ttu-id="e0b24-147">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="e0b24-147">Module 1:</span></span>
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="e0b24-148">Instalación del paquete hash</span><span class="sxs-lookup"><span data-stu-id="e0b24-148">Install hash package</span></span>
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="e0b24-149">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="e0b24-149">Limitations</span></span>
<span data-ttu-id="e0b24-150">Desde una perspectiva del algoritmo, el análisis de opiniones basado en léxico es una herramienta de análisis de opiniones generales, aunque es posible que no funcione mejor que el método de clasificación para campos específicos.</span><span class="sxs-lookup"><span data-stu-id="e0b24-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than the classification method for specific fields.</span></span> <span data-ttu-id="e0b24-151">No se aborda en gran detalle el problema de la negación.</span><span class="sxs-lookup"><span data-stu-id="e0b24-151">The negation problem is not well dealt with.</span></span> <span data-ttu-id="e0b24-152">Codificamos varias palabras de negación en nuestro programa, pero una mejor manera es usar un diccionario de negación y crear algunas reglas.</span><span class="sxs-lookup"><span data-stu-id="e0b24-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="e0b24-153">El servicio web funciona mejor con frases cortas y sencillas como tweets y publicaciones de Facebook que con frases largas y complejas como las de las revisiones de Amazon.</span><span class="sxs-lookup"><span data-stu-id="e0b24-153">The web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="e0b24-154">P+F</span><span class="sxs-lookup"><span data-stu-id="e0b24-154">FAQ</span></span>
<span data-ttu-id="e0b24-155">Para ver las preguntas más frecuentes sobre el uso del servicio web o la publicación en Azure Marketplace, haga clic [aquí](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="e0b24-155">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

