---
title: Uso de las funcionalidades de Cognitive en U-SQL para Azure Data Lake Analytics | Microsoft Docs
description: "Obtenga información sobre cómo usar la inteligencia de las funcionalidades de Cognitive en U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: f77329f9838d6e824afa7234de90f62257a004de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-the-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="07b52-103">Tutorial: Introducción a las funcionalidades de Cognitive de U-SQL</span><span class="sxs-lookup"><span data-stu-id="07b52-103">Tutorial: Get started with the Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="07b52-104">Las funcionalidades de Cognitive para U-SQL permiten a los desarrolladores usar inteligencia en sus programas de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="07b52-104">Cognitive capabilities for U-SQL enable developers to use put intelligence in their big data programs.</span></span> <span data-ttu-id="07b52-105">El proceso general es sencillo:</span><span class="sxs-lookup"><span data-stu-id="07b52-105">The overall process in simple:</span></span>

* <span data-ttu-id="07b52-106">Utilice la instrucción de REFERENCE ASSEMBLY para habilitar las características de Cognitive para el script de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="07b52-106">Use the REFERENCE ASSEMBLY statement to enable the cognitive features for the U-SQL Script</span></span>
* <span data-ttu-id="07b52-107">Llame a la operación PROCESS para utilizar las funcionalidades de Cognitive</span><span class="sxs-lookup"><span data-stu-id="07b52-107">Call the PROCESS operation to use the Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="07b52-108">Escenarios de imágenes</span><span class="sxs-lookup"><span data-stu-id="07b52-108">Imaging scenarios</span></span>

### <a name="example-image-tagging"></a><span data-ttu-id="07b52-109">Ejemplo: etiquetado de imágenes</span><span class="sxs-lookup"><span data-stu-id="07b52-109">Example: Image tagging</span></span>

<span data-ttu-id="07b52-110">En el ejemplo siguiente se muestra un uso integral de las funcionalidades relacionadas con las imágenes para detectar objetos dentro de estas.</span><span class="sxs-lookup"><span data-stu-id="07b52-110">The following example shows an end-to-end use of the imaging capabilities to detect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract the number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="07b52-111">Extracción de emociones de caras humanas</span><span class="sxs-lookup"><span data-stu-id="07b52-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="07b52-112">Cálculo de la edad y el sexo de caras humanas</span><span class="sxs-lookup"><span data-stu-id="07b52-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="07b52-113">Detección de texto en imágenes (OCR)</span><span class="sxs-lookup"><span data-stu-id="07b52-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="07b52-114">Escenarios de texto</span><span class="sxs-lookup"><span data-stu-id="07b52-114">Text scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="07b52-115">Datos de entrada</span><span class="sxs-lookup"><span data-stu-id="07b52-115">Input data</span></span>

<span data-ttu-id="07b52-116">Suponga que tenemos una entrada que consta de "Guerra y Paz" por León Tolstói.</span><span class="sxs-lookup"><span data-stu-id="07b52-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

    REFERENCE ASSEMBLY [TextCommon];
    REFERENCE ASSEMBLY [TextSentiment];
    REFERENCE ASSEMBLY [TextKeyPhrase];

    @WarAndPeace =
        EXTRACT No int,
                Year string,
                Book string,
                Chapter string,
                Text string
        FROM @"/usqlext/samples/cognition/war_and_peace.csv"
        USING Extractors.Csv();

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="07b52-117">Extracción de las frases clave de cada párrafo</span><span class="sxs-lookup"><span data-stu-id="07b52-117">Extract key phrases for each paragraph</span></span>

    @keyphrase =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                KeyPhrase string
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.KeyPhraseExtractor();

    // Tokenize the key phrases.
    @kpsplits =
        SELECT No,
            Year,
            Book,
            Chapter,
            Text,
            T.KeyPhrase
        FROM @keyphrase
            CROSS APPLY
                new Cognition.Text.Splitter("KeyPhrase") AS T(KeyPhrase);
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="07b52-118">Realización del análisis de sentimiento de cada párrafo</span><span class="sxs-lookup"><span data-stu-id="07b52-118">Perform sentiment analysis on each paragraph</span></span>

    @sentiment =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                Sentiment string,
                Conf double
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.SentimentAnalyzer(true);

