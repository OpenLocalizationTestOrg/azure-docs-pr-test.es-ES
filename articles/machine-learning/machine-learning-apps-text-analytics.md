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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>API de Machine Learning: análisis de texto de opinión, extracción de frases clave, detección de idiomas y detección de temas
> [!NOTE]
> Esta guía es para la versión 1 de hello API. Para la versión 2, [ **consulte toothis documento**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Versión 2 es ahora la versión preferida de Hola de esta API.
> 
> 

## <a name="overview"></a>Información general
Hola API de análisis de texto es un conjunto de análisis de texto [servicios web](https://datamarket.azure.com/dataset/amla/text-analytics) compiladas con aprendizaje automático de Azure. Hola API puede ser usado tooanalyze texto no estructurado para tareas como el análisis de opiniones, extracción de frases clave, la detección de idioma y detección de tema. No están de datos de entrenamiento necesario toouse esta API: simplemente poner los datos de texto. Esta API usa un lenguaje natural avanzado toodeliver de técnicas de procesamiento mejor en las predicciones de la clase.

Puede ver el análisis de texto en acción en nuestros [sitio de demostración](https://text-analytics-demo.azurewebsites.net/), donde también encontrará [ejemplos](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) acerca de cómo tooimplement el análisis de texto en C# y Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>análisis de opiniones
Hola API devuelve un valor numérico entre 0 y 1. Puntuaciones cerrar too1 indican opiniones, mientras que too0 cerrar puntuaciones indicar opiniones negativo. La puntuación de las opiniones se genera mediante técnicas de clasificación. Hola entrada características toohello clasificador incluyen n-gramas, generados a partir de etiquetas de la parte de la oración y word incrustaciones de características. Actualmente, el inglés está Hola solo admite el idioma.

## <a name="key-phrase-extraction"></a>Extracción de la frase clave
Hola API devuelve una lista de cadenas que denotan Hola puntos clave de conversación en texto de entrada de Hola. Empleamos las técnicas del kit de herramientas de procesamiento de lenguaje natural sofisticadas de Microsoft Office. Actualmente, el inglés está Hola solo admite el idioma.

## <a name="language-detection"></a>Detección de idiomas
Hola API devuelve Hola detectó idioma y una puntuación numérica entre 0 y 1. Puntuaciones cerrar too1 indicar certeza de 100% que el idioma de hello identificado sea true. Se admiten un total de 120 idiomas.

## <a name="topic-detection"></a>Detección de temas
Se trata de una API publicada recientemente que devuelve temas principales de detectado Hola para obtener una lista de registros de texto enviado. Se identifica un tema con una frase clave, que puede ser una o más palabras relacionadas. Esta API requiere un mínimo de 100 texto registra toobe enviado, pero está diseñada toodetect temas entre cientos toothousands de registros. Tenga en cuenta que esta API cobra una transacción por registro de texto enviado. Hola API es toowork diseñado correctamente para humanos corto, escrito texto como revisiones y comentarios del usuario.

- - -
## <a name="api-definition"></a>Definición de la API
### <a name="headers"></a>Encabezados
Asegúrese de que incluye encabezados de hello correcto en la solicitud, que debería ser como sigue:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Puede encontrar la clave de cuenta de la cuenta de hello [Azure Data Market](https://datamarket.azure.com/account/keys). Tenga en cuenta que actualmente JSON solo se acepta para formatos de entrada y salida. XML no se admite.

- - -
## <a name="single-response-apis"></a>API de respuesta única
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Solicitud de ejemplo**

En la llamada de Hola a continuación, se está solicitando análisis de opiniones frase de saludo "¡Hello World":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Esto devolverá una respuesta como sigue:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Solicitud de ejemplo**

En la llamada de Hola a continuación, se está solicitando frases clave Hola se encuentra en texto hello "Es una maravillosa toostay hotel en, decoración único y descriptivo personal":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Esto devolverá una respuesta como sigue:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Solicitud de ejemplo**

En la llamada GET de Hola a continuación, estamos solicitando de opinión de Hola de frases clave de hello en texto hello *Hola a todos*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Esto devolverá una respuesta como sigue:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Parámetros opcionales**

`NumberOfLanguagesToDetect` es un parámetro opcional. Hola predeterminado es 1.

- - -
## <a name="batch-apis"></a>API de lote
Hola servicio de análisis de texto permite toodo opiniones y las extracciones de frase clave en modo por lotes. Tenga en cuenta que cada uno de los registros de hello puntuarse recuentos como una transacción. A modo de ejemplo, si solicita una opinión para 1000 registros en una sola llamada, se deducirán 1000 transacciones.

Tenga en cuenta que los identificadores de hello introducidos en sistema Hola son identificadores de hello devueltos por el sistema de Hola. servicio web de Hello no comprueba que estos identificadores son únicos. Es responsabilidad de Hola de unicidad de hello llamador tooverify. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Solicitud de ejemplo**

Hola POST llamar a continuación, se está solicitando para mensajes de Hola de frases de saludo "¡Hello World", "Foo ¡Hello World" y "Hola mundo mi" en el cuerpo de saludo de solicitud de hello:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Cuerpo de la solicitud:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

En la respuesta de Hola a continuación, se obtiene la lista de Hola de puntuaciones asociado con el Id. de texto:

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
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Solicitud de ejemplo**

En este ejemplo, nos estamos solicita lista Hola de mensajes para frases clave de Hola Hola siguientes textos: 

* "Es una maravillosa toostay hotel en, decoración único y descriptivo personal"
* "It was an amazing build conference, with very interesting talks"
* "tráfico Hola se desastroso a la hora, pasó tres horas va toohello aeropuerto"

Esta solicitud se realiza como un punto de conexión de entrada llamada toohello:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Cuerpo de la solicitud:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

En la respuesta de Hola a continuación, se obtiene la lista de Hola de frases clave asociadas con el Id. de texto:

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
### <a name="getlanguagebatch"></a>GetLanguageBatch

En la llamada POST Hola a continuación, se precisa la detección de idioma para las dos entradas de texto:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Cuerpo de la solicitud:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Esto devuelve Hola después de respuesta, donde se detecta inglés en la primera entrada de Hola y el francés en la segunda entrada de hello:

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
## <a name="topic-detection-apis"></a>API de detección de temas
Se trata de una API publicada recientemente que devuelve temas principales de detectado Hola para obtener una lista de registros de texto enviado. Se identifica un tema con una frase clave, que puede ser una o más palabras relacionadas. Tenga en cuenta que esta API cobra una transacción por registro de texto enviado.

Esta API requiere un mínimo de 100 texto registra toobe enviado, pero está diseñada toodetect temas entre cientos toothousands de registros.

### <a name="topics--submit-job"></a>Temas: Envío de trabajo
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Solicitud de ejemplo**

En la llamada POST de Hola a continuación, se precisa temas para un conjunto de 100 artículos, donde hello primero y último de entrada se muestran los artículos, y se incluyen dos StopPhrases.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Cuerpo de la solicitud:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

En la respuesta de hello siguiente, obtendrá Hola JobId para trabajo enviado hello:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Una lista de palabras únicas o frases con varias palabras que no se deben devolver como temas. Puede ser usado toofilter temas muy genérico. Por ejemplo, en un conjunto de datos acerca de reseñas de hoteles, "hotel" y "hostal" pueden ser frases de detección razonables.  

### <a name="topics--poll-for-job-results"></a>Temas: Sondeo de resultados del trabajo
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Solicitud de ejemplo**

Pasar Hola que JobID procedentes de hello 'Enviar trabajo' paso toofetch hello, se. Se recomienda llamar a este punto de conexión cada minuto hasta que el estado = 'Complete' en la respuesta de Hola. Tardará unos 10 minutos durante una toocomplete de trabajo, o más trabajos con varios miles de registros.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Mientras se está procesando, respuesta de hello será como se indica a continuación:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Hola API devuelve el resultado en formato JSON en hello siguiendo el formato:

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


propiedades de Hola para cada parte de la respuesta de hello son los siguientes:

**Propiedades de TopicInfo**

| Clave | Description |
|:--- |:--- |
| TopicId |Un identificador único para cada tema. |
| Score |Número de registros asigna tootopic. |
| KeyPhrase |Una con palabra o frase para tema de Hola. Puede ser una palabra o varias. |

**Propiedades de TopicAssignment**

| Clave | Description |
|:--- |:--- |
| Id |Identificador de registro de hello. Es el mismo Id. de toohello incluido en la entrada de Hola. |
| TopicId |Hola Id. del tema qué registro de hello se ha asignado a. |
| Distancia |Confianza de que el registro de hello pertenece toohello tema. Distancia cuanto más se acerque toozero indica mayor confianza. |

