---
title: "aaaDebug su modelo de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Cómo toodebug los errores generados por entrenar modelo y el modelo de puntuación de módulos de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="66a80-103">Depurar el modelo en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="66a80-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="66a80-104">Este artículo explica por qué cualquiera de hello después de dos errores puede producirse cuando se ejecuta un modelo de posibles razones de hello:</span><span class="sxs-lookup"><span data-stu-id="66a80-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="66a80-105">Hola [entrenar modelo] [ train-model] módulo genera un error</span><span class="sxs-lookup"><span data-stu-id="66a80-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="66a80-106">Hola [puntuar modelo] [ score-model] module produce resultados incorrectos</span><span class="sxs-lookup"><span data-stu-id="66a80-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="66a80-107">El módulo Entrenar modelo produce un error</span><span class="sxs-lookup"><span data-stu-id="66a80-107">Train Model Module produces an error</span></span>

![imagen1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="66a80-109">Hola [entrenar modelo] [ train-model] módulo espera dos entradas:</span><span class="sxs-lookup"><span data-stu-id="66a80-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="66a80-110">tipo de Hola de modelo de aprendizaje automático de colección de Hola de modelos proporcionados por el aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="66a80-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="66a80-111">datos de entrenamiento con una columna de etiqueta especificado que especifica Hola Hola toopredict variable (hello otras columnas se supone que las características de toobe).</span><span class="sxs-lookup"><span data-stu-id="66a80-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="66a80-112">Este módulo puede producir un error en hello casos siguientes:</span><span class="sxs-lookup"><span data-stu-id="66a80-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="66a80-113">columna de etiqueta de Hola se especificó correctamente.</span><span class="sxs-lookup"><span data-stu-id="66a80-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="66a80-114">Esto puede ocurrir si se selecciona más de una columna como etiqueta de Hola o se selecciona un índice de columna es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="66a80-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="66a80-115">Por ejemplo, segundo caso de hello aplicaría si se utiliza un índice de columna de 30 años con un conjunto de datos de entrada que tiene 25 solo columnas.</span><span class="sxs-lookup"><span data-stu-id="66a80-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="66a80-116">Hola dataset no contiene ninguna columna de característica.</span><span class="sxs-lookup"><span data-stu-id="66a80-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="66a80-117">Por ejemplo, si el conjunto de datos de entrada de hello tiene solo una columna, que se marca como columna de etiqueta de hello, no habría ninguna característica con qué modelo de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="66a80-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="66a80-118">En este caso, Hola [entrenar modelo] [ train-model] módulo genera un error.</span><span class="sxs-lookup"><span data-stu-id="66a80-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="66a80-119">conjunto de entrada de datos Hello (características o etiqueta) contiene infinito como valor.</span><span class="sxs-lookup"><span data-stu-id="66a80-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="66a80-120">El módulo Puntuar modelo produce resultados incorrectos</span><span class="sxs-lookup"><span data-stu-id="66a80-120">Score Model Module produces incorrect results</span></span>

![imagen2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="66a80-122">En un experimento de entrenamiento y pruebas típico de aprendizaje supervisado, Hola [dividir datos] [ split] módulo divide el conjunto de datos original de hello en dos partes: una parte es el modelo de Hola de tootrain usado y se usa una parte tooscore grado entrenado Hola realiza.</span><span class="sxs-lookup"><span data-stu-id="66a80-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="66a80-123">modelo entrenado Hello es tooscore usado Hola datos de prueba, después del cual los resultados de hello son toodetermine evaluado Hola precisión del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66a80-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="66a80-124">Hola [puntuar modelo] [ score-model] módulo requiere dos entradas:</span><span class="sxs-lookup"><span data-stu-id="66a80-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="66a80-125">Una salida entrenado de hello [entrenar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="66a80-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="66a80-126">Un conjunto de datos de puntuación que es diferente del conjunto de datos de hello usa modelos de hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="66a80-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="66a80-127">Lo del posible que incluso si se realiza correctamente el experimento de hello, Hola [puntuar modelo] [ score-model] module produce resultados incorrectos.</span><span class="sxs-lookup"><span data-stu-id="66a80-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="66a80-128">Varios escenarios pueden provocar esta toohappen:</span><span class="sxs-lookup"><span data-stu-id="66a80-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="66a80-129">Si Hola especifica la etiqueta es de categoría y un modelo de regresión está entrenado con datos de hello, se genera una salida incorrecta por hello [puntuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="66a80-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="66a80-130">Esto es debido a que la regresión requiere una variable de respuesta continua.</span><span class="sxs-lookup"><span data-stu-id="66a80-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="66a80-131">En este caso, sería más adecuado toouse un modelo de clasificación.</span><span class="sxs-lookup"><span data-stu-id="66a80-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="66a80-132">De forma similar, si un modelo de clasificación está entrenado en un conjunto de datos con números de punto flotante en la columna de etiqueta de hello, se podrían producir resultados no deseados.</span><span class="sxs-lookup"><span data-stu-id="66a80-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="66a80-133">Esto es debido a que la clasificación requiere una variable de respuesta discreta que solo permite valores que abarcan un conjunto finito y generalmente bastante pequeño de clases.</span><span class="sxs-lookup"><span data-stu-id="66a80-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="66a80-134">Si Hola la puntuación del conjunto de datos no contiene todos los modelos de hello tootrain de hello características que se utilizan, Hola [puntuar modelo] [ score-model] genera un error.</span><span class="sxs-lookup"><span data-stu-id="66a80-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="66a80-135">Si una fila de Hola la puntuación del conjunto de datos contiene un valor que falta o un valor infinito para cualquiera de sus características, Hola [puntuar modelo] [ score-model] no producirá ninguna fila toothat de salida correspondiente.</span><span class="sxs-lookup"><span data-stu-id="66a80-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="66a80-136">Hola [puntuar modelo] [ score-model] puede producir resultados idénticos para todas las filas de Hola la puntuación del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="66a80-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="66a80-137">Esto puede ocurrir, por ejemplo, al tratar de clasificación con bosques de decisión de si se elige Hola un número mínimo de muestras por nodo hoja toobe más de hello número de ejemplos de entrenamiento disponibles.</span><span class="sxs-lookup"><span data-stu-id="66a80-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

