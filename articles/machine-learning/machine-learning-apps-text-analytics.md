---
title: "API de Machine Learning: análisis de texto | Microsoft Docs"
description: "El API de análisis de Microsoft para máquinas aprendizaje texto puede ser usado tooanalyze texto no estructurado para la detección de tema, de la detección de idioma y de análisis de opiniones, extracción de la frase clave."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="b6612-103">API de Machine Learning: análisis de texto de opinión, extracción de frases clave, detección de idiomas y detección de temas</span><span class="sxs-lookup"><span data-stu-id="b6612-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="b6612-104">Esta guía es para la versión 1 de hello API.</span><span class="sxs-lookup"><span data-stu-id="b6612-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="b6612-105">Para la versión 2, [ **consulte toothis documento**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="b6612-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="b6612-106">Versión 2 es ahora la versión preferida de Hola de esta API.</span><span class="sxs-lookup"><span data-stu-id="b6612-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="b6612-107">Información general</span><span class="sxs-lookup"><span data-stu-id="b6612-107">Overview</span></span>
<span data-ttu-id="b6612-108">Hola API de análisis de texto es un conjunto de análisis de texto [servicios web](https://datamarket.azure.com/dataset/amla/text-analytics) compiladas con aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6612-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="b6612-109">Hola API puede ser usado tooanalyze texto no estructurado para tareas como el análisis de opiniones, extracción de frases clave, la detección de idioma y detección de tema.</span><span class="sxs-lookup"><span data-stu-id="b6612-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="b6612-110">No están de datos de entrenamiento necesario toouse esta API: simplemente poner los datos de texto.</span><span class="sxs-lookup"><span data-stu-id="b6612-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="b6612-111">Esta API usa un lenguaje natural avanzado toodeliver de técnicas de procesamiento mejor en las predicciones de la clase.</span><span class="sxs-lookup"><span data-stu-id="b6612-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="b6612-112">Puede ver el análisis de texto en acción en nuestros [sitio de demostración](https://text-analytics-demo.azurewebsites.net/), donde también encontrará [ejemplos](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) acerca de cómo tooimplement el análisis de texto en C# y Python.</span><span class="sxs-lookup"><span data-stu-id="b6612-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="b6612-113">análisis de opiniones</span><span class="sxs-lookup"><span data-stu-id="b6612-113">Sentiment analysis</span></span>
<span data-ttu-id="b6612-114">Hola API devuelve un valor numérico entre 0 y 1.</span><span class="sxs-lookup"><span data-stu-id="b6612-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="b6612-115">Puntuaciones cerrar too1 indican opiniones, mientras que too0 cerrar puntuaciones indicar opiniones negativo.</span><span class="sxs-lookup"><span data-stu-id="b6612-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="b6612-116">La puntuación de las opiniones se genera mediante técnicas de clasificación.</span><span class="sxs-lookup"><span data-stu-id="b6612-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="b6612-117">Hola entrada características toohello clasificador incluyen n-gramas, generados a partir de etiquetas de la parte de la oración y word incrustaciones de características.</span><span class="sxs-lookup"><span data-stu-id="b6612-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="b6612-118">Actualmente, el inglés está Hola solo admite el idioma.</span><span class="sxs-lookup"><span data-stu-id="b6612-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="b6612-119">Extracción de la frase clave</span><span class="sxs-lookup"><span data-stu-id="b6612-119">Key phrase extraction</span></span>
<span data-ttu-id="b6612-120">Hola API devuelve una lista de cadenas que denotan Hola puntos clave de conversación en texto de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6612-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="b6612-121">Empleamos las técnicas del kit de herramientas de procesamiento de lenguaje natural sofisticadas de Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="b6612-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="b6612-122">Actualmente, el inglés está Hola solo admite el idioma.</span><span class="sxs-lookup"><span data-stu-id="b6612-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="b6612-123">Detección de idiomas</span><span class="sxs-lookup"><span data-stu-id="b6612-123">Language detection</span></span>
<span data-ttu-id="b6612-124">Hola API devuelve Hola detectó idioma y una puntuación numérica entre 0 y 1.</span><span class="sxs-lookup"><span data-stu-id="b6612-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="b6612-125">Puntuaciones cerrar too1 indicar certeza de 100% que el idioma de hello identificado sea true.</span><span class="sxs-lookup"><span data-stu-id="b6612-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="b6612-126">Se admiten un total de 120 idiomas.</span><span class="sxs-lookup"><span data-stu-id="b6612-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="b6612-127">Detección de temas</span><span class="sxs-lookup"><span data-stu-id="b6612-127">Topic detection</span></span>
<span data-ttu-id="b6612-128">Se trata de una API publicada recientemente que devuelve temas principales de detectado Hola para obtener una lista de registros de texto enviado.</span><span class="sxs-lookup"><span data-stu-id="b6612-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="b6612-129">Se identifica un tema con una frase clave, que puede ser una o más palabras relacionadas.</span><span class="sxs-lookup"><span data-stu-id="b6612-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="b6612-130">Esta API requiere un mínimo de 100 texto registra toobe enviado, pero está diseñada toodetect temas entre cientos toothousands de registros.</span><span class="sxs-lookup"><span data-stu-id="b6612-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="b6612-131">Tenga en cuenta que esta API cobra una transacción por registro de texto enviado.</span><span class="sxs-lookup"><span data-stu-id="b6612-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="b6612-132">Hola API es toowork diseñado correctamente para humanos corto, escrito texto como revisiones y comentarios del usuario.</span><span class="sxs-lookup"><span data-stu-id="b6612-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="b6612-133">Definición de la API</span><span class="sxs-lookup"><span data-stu-id="b6612-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="b6612-134">Encabezados</span><span class="sxs-lookup"><span data-stu-id="b6612-134">Headers</span></span>
<span data-ttu-id="b6612-135">Asegúrese de que incluye encabezados de hello correcto en la solicitud, que debería ser como sigue:</span><span class="sxs-lookup"><span data-stu-id="b6612-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="b6612-136">Puede encontrar la clave de cuenta de la cuenta de hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="b6612-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="b6612-137">Tenga en cuenta que actualmente JSON solo se acepta para formatos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="b6612-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="b6612-138">XML no se admite.</span><span class="sxs-lookup"><span data-stu-id="b6612-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="b6612-139">API de respuesta única</span><span class="sxs-lookup"><span data-stu-id="b6612-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="b6612-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="b6612-140">GetSentiment</span></span>
<span data-ttu-id="b6612-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="b6612-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="b6612-142">**Solicitud de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b6612-142">**Example request**</span></span>

<span data-ttu-id="b6612-143">En la llamada de Hola a continuación, se está solicitando análisis de opiniones frase de saludo "¡Hello World":</span><span class="sxs-lookup"><span data-stu-id="b6612-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="b6612-144">Esto devolverá una respuesta como sigue:</span><span class="sxs-lookup"><span data-stu-id="b6612-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="b6612-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="b6612-145">GetKeyPhrases</span></span>
<span data-ttu-id="b6612-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="b6612-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="b6612-147">**Solicitud de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b6612-147">**Example request**</span></span>

<span data-ttu-id="b6612-148">En la llamada de Hola a continuación, se está solicitando frases clave Hola se encuentra en texto hello "Es una maravillosa toostay hotel en, decoración único y descriptivo personal":</span><span class="sxs-lookup"><span data-stu-id="b6612-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="b6612-149">Esto devolverá una respuesta como sigue:</span><span class="sxs-lookup"><span data-stu-id="b6612-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="b6612-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="b6612-150">GetLanguage</span></span>
<span data-ttu-id="b6612-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="b6612-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="b6612-152">**Solicitud de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b6612-152">**Example request**</span></span>

<span data-ttu-id="b6612-153">En la llamada GET de Hola a continuación, estamos solicitando de opinión de Hola de frases clave de hello en texto hello *Hola a todos*</span><span class="sxs-lookup"><span data-stu-id="b6612-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="b6612-154">Esto devolverá una respuesta como sigue:</span><span class="sxs-lookup"><span data-stu-id="b6612-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="b6612-155">**Parámetros opcionales**</span><span class="sxs-lookup"><span data-stu-id="b6612-155">**Optional parameters**</span></span>

<span data-ttu-id="b6612-156">`NumberOfLanguagesToDetect` es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="b6612-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="b6612-157">Hola predeterminado es 1.</span><span class="sxs-lookup"><span data-stu-id="b6612-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="b6612-158">API de lote</span><span class="sxs-lookup"><span data-stu-id="b6612-158">Batch APIs</span></span>
<span data-ttu-id="b6612-159">Hola servicio de análisis de texto permite toodo opiniones y las extracciones de frase clave en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="b6612-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="b6612-160">Tenga en cuenta que cada uno de los registros de hello puntuarse recuentos como una transacción.</span><span class="sxs-lookup"><span data-stu-id="b6612-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="b6612-161">A modo de ejemplo, si solicita una opinión para 1000 registros en una sola llamada, se deducirán 1000 transacciones.</span><span class="sxs-lookup"><span data-stu-id="b6612-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="b6612-162">Tenga en cuenta que los identificadores de hello introducidos en sistema Hola son identificadores de hello devueltos por el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6612-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="b6612-163">servicio web de Hello no comprueba que estos identificadores son únicos.</span><span class="sxs-lookup"><span data-stu-id="b6612-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="b6612-164">Es responsabilidad de Hola de unicidad de hello llamador tooverify.</span><span class="sxs-lookup"><span data-stu-id="b6612-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="b6612-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="b6612-165">GetSentimentBatch</span></span>
<span data-ttu-id="b6612-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="b6612-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="b6612-167">**Solicitud de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b6612-167">**Example request**</span></span>

<span data-ttu-id="b6612-168">Hola POST llamar a continuación, se está solicitando para mensajes de Hola de frases de saludo "¡Hello World", "Foo ¡Hello World" y "Hola mundo mi" en el cuerpo de saludo de solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="b6612-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="b6612-169">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b6612-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="b6612-170">En la respuesta de Hola a continuación, se obtiene la lista de Hola de puntuaciones asociado con el Id. de texto:</span><span class="sxs-lookup"><span data-stu-id="b6612-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="b6612-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="b6612-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="b6612-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="b6612-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="b6612-173">**Solicitud de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b6612-173">**Example request**</span></span>

<span data-ttu-id="b6612-174">En este ejemplo, nos estamos solicita lista Hola de mensajes para frases clave de Hola Hola siguientes textos:</span><span class="sxs-lookup"><span data-stu-id="b6612-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="b6612-175">"Es una maravillosa toostay hotel en, decoración único y descriptivo personal"</span><span class="sxs-lookup"><span data-stu-id="b6612-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="b6612-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="b6612-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="b6612-177">"tráfico Hola se desastroso a la hora, pasó tres horas va toohello aeropuerto"</span><span class="sxs-lookup"><span data-stu-id="b6612-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="b6612-178">Esta solicitud se realiza como un punto de conexión de entrada llamada toohello:</span><span class="sxs-lookup"><span data-stu-id="b6612-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="b6612-179">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b6612-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="b6612-180">En la respuesta de Hola a continuación, se obtiene la lista de Hola de frases clave asociadas con el Id. de texto:</span><span class="sxs-lookup"><span data-stu-id="b6612-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a><span data-ttu-id="b6612-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="b6612-181">GetLanguageBatch</span></span>

<span data-ttu-id="b6612-182">En la llamada POST Hola a continuación, se precisa la detección de idioma para las dos entradas de texto:</span><span class="sxs-lookup"><span data-stu-id="b6612-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="b6612-183">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b6612-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="b6612-184">Esto devuelve Hola después de respuesta, donde se detecta inglés en la primera entrada de Hola y el francés en la segunda entrada de hello:</span><span class="sxs-lookup"><span data-stu-id="b6612-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a><span data-ttu-id="b6612-185">API de detección de temas</span><span class="sxs-lookup"><span data-stu-id="b6612-185">Topic Detection APIs</span></span>
<span data-ttu-id="b6612-186">Se trata de una API publicada recientemente que devuelve temas principales de detectado Hola para obtener una lista de registros de texto enviado.</span><span class="sxs-lookup"><span data-stu-id="b6612-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="b6612-187">Se identifica un tema con una frase clave, que puede ser una o más palabras relacionadas.</span><span class="sxs-lookup"><span data-stu-id="b6612-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="b6612-188">Tenga en cuenta que esta API cobra una transacción por registro de texto enviado.</span><span class="sxs-lookup"><span data-stu-id="b6612-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="b6612-189">Esta API requiere un mínimo de 100 texto registra toobe enviado, pero está diseñada toodetect temas entre cientos toothousands de registros.</span><span class="sxs-lookup"><span data-stu-id="b6612-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="b6612-190">Temas: Envío de trabajo</span><span class="sxs-lookup"><span data-stu-id="b6612-190">Topics – Submit job</span></span>
<span data-ttu-id="b6612-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="b6612-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="b6612-192">**Solicitud de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b6612-192">**Example request**</span></span>

<span data-ttu-id="b6612-193">En la llamada POST de Hola a continuación, se precisa temas para un conjunto de 100 artículos, donde hello primero y último de entrada se muestran los artículos, y se incluyen dos StopPhrases.</span><span class="sxs-lookup"><span data-stu-id="b6612-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="b6612-194">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b6612-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="b6612-195">En la respuesta de hello siguiente, obtendrá Hola JobId para trabajo enviado hello:</span><span class="sxs-lookup"><span data-stu-id="b6612-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="b6612-196">Una lista de palabras únicas o frases con varias palabras que no se deben devolver como temas.</span><span class="sxs-lookup"><span data-stu-id="b6612-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="b6612-197">Puede ser usado toofilter temas muy genérico.</span><span class="sxs-lookup"><span data-stu-id="b6612-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="b6612-198">Por ejemplo, en un conjunto de datos acerca de reseñas de hoteles, "hotel" y "hostal" pueden ser frases de detección razonables.</span><span class="sxs-lookup"><span data-stu-id="b6612-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="b6612-199">Temas: Sondeo de resultados del trabajo</span><span class="sxs-lookup"><span data-stu-id="b6612-199">Topics – Poll for job results</span></span>
<span data-ttu-id="b6612-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="b6612-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="b6612-201">**Solicitud de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="b6612-201">**Example request**</span></span>

<span data-ttu-id="b6612-202">Pasar Hola que JobID procedentes de hello 'Enviar trabajo' paso toofetch hello, se.</span><span class="sxs-lookup"><span data-stu-id="b6612-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="b6612-203">Se recomienda llamar a este punto de conexión cada minuto hasta que el estado = 'Complete' en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6612-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="b6612-204">Tardará unos 10 minutos durante una toocomplete de trabajo, o más trabajos con varios miles de registros.</span><span class="sxs-lookup"><span data-stu-id="b6612-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="b6612-205">Mientras se está procesando, respuesta de hello será como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b6612-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="b6612-206">Hola API devuelve el resultado en formato JSON en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="b6612-206">hello API returns output in JSON format in hello following format:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


<span data-ttu-id="b6612-207">propiedades de Hola para cada parte de la respuesta de hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b6612-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="b6612-208">**Propiedades de TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="b6612-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="b6612-209">Clave</span><span class="sxs-lookup"><span data-stu-id="b6612-209">Key</span></span> | <span data-ttu-id="b6612-210">Description</span><span class="sxs-lookup"><span data-stu-id="b6612-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6612-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="b6612-211">TopicId</span></span> |<span data-ttu-id="b6612-212">Un identificador único para cada tema.</span><span class="sxs-lookup"><span data-stu-id="b6612-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="b6612-213">Score</span><span class="sxs-lookup"><span data-stu-id="b6612-213">Score</span></span> |<span data-ttu-id="b6612-214">Número de registros asigna tootopic.</span><span class="sxs-lookup"><span data-stu-id="b6612-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="b6612-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="b6612-215">KeyPhrase</span></span> |<span data-ttu-id="b6612-216">Una con palabra o frase para tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6612-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="b6612-217">Puede ser una palabra o varias.</span><span class="sxs-lookup"><span data-stu-id="b6612-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="b6612-218">**Propiedades de TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="b6612-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="b6612-219">Clave</span><span class="sxs-lookup"><span data-stu-id="b6612-219">Key</span></span> | <span data-ttu-id="b6612-220">Description</span><span class="sxs-lookup"><span data-stu-id="b6612-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b6612-221">Id</span><span class="sxs-lookup"><span data-stu-id="b6612-221">Id</span></span> |<span data-ttu-id="b6612-222">Identificador de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="b6612-222">Identifier for hello record.</span></span> <span data-ttu-id="b6612-223">Es el mismo Id. de toohello incluido en la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6612-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="b6612-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="b6612-224">TopicId</span></span> |<span data-ttu-id="b6612-225">Hola Id. del tema qué registro de hello se ha asignado a.</span><span class="sxs-lookup"><span data-stu-id="b6612-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="b6612-226">Distancia</span><span class="sxs-lookup"><span data-stu-id="b6612-226">Distance</span></span> |<span data-ttu-id="b6612-227">Confianza de que el registro de hello pertenece toohello tema.</span><span class="sxs-lookup"><span data-stu-id="b6612-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="b6612-228">Distancia cuanto más se acerque toozero indica mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="b6612-228">Distance closer toozero indicates higher confidence.</span></span> |

