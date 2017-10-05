---
title: Depurar el modelo en Azure Machine Learning | Microsoft Docs
description: "Cómo depurar los errores producidos por los módulos Entrenar modelo y Puntuar modelo en Azure Machine Learning."
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
ms.openlocfilehash: d4cc94a6395ea45bccf65d9a9f3118ec98cb258d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="f588b-103">Depurar el modelo en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="f588b-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="f588b-104">En este artículo se explican las posibles razones por las cuales podría encontrar uno de los dos siguientes errores al ejecutar un modelo:</span><span class="sxs-lookup"><span data-stu-id="f588b-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="f588b-105">el módulo [Entrenar modelo][train-model] produce un error</span><span class="sxs-lookup"><span data-stu-id="f588b-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="f588b-106">el módulo [Puntuar modelo][score-model] produce resultados incorrectos</span><span class="sxs-lookup"><span data-stu-id="f588b-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="f588b-107">El módulo Entrenar modelo produce un error</span><span class="sxs-lookup"><span data-stu-id="f588b-107">Train Model Module produces an error</span></span>

![imagen1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="f588b-109">El módulo [Entrenar modelo][train-model] espera dos entradas:</span><span class="sxs-lookup"><span data-stu-id="f588b-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="f588b-110">El tipo de modelo de aprendizaje automático de la colección de modelos que proporciona Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f588b-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="f588b-111">Los datos de aprendizaje con una columna de etiqueta que especifica la variable de predicción (se da por hecho que las otras columnas son de características).</span><span class="sxs-lookup"><span data-stu-id="f588b-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="f588b-112">Este módulo puede producir un error en los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="f588b-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="f588b-113">La columna de etiqueta se especifica incorrectamente.</span><span class="sxs-lookup"><span data-stu-id="f588b-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="f588b-114">Esto puede ocurrir si se selecciona más de una columna como de etiqueta o se selecciona un índice de columna incorrecto.</span><span class="sxs-lookup"><span data-stu-id="f588b-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="f588b-115">Por ejemplo, el segundo caso se aplicaría si se usa un índice de columna de 30 con un conjunto de datos de entrada que solo tiene 25 columnas.</span><span class="sxs-lookup"><span data-stu-id="f588b-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="f588b-116">Si el conjunto de datos no contiene ninguna columna de característica.</span><span class="sxs-lookup"><span data-stu-id="f588b-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="f588b-117">Por ejemplo, si el conjunto de datos de entrada tiene solo una columna, que se marca como la columna de etiqueta, no habría ninguna característica con la que se pudiera generar el modelo.</span><span class="sxs-lookup"><span data-stu-id="f588b-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="f588b-118">En este caso, el módulo [Entrenar modelo][train-model] produce un error.</span><span class="sxs-lookup"><span data-stu-id="f588b-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="f588b-119">El conjunto de datos de entrada (características o de etiqueta) contiene infinito como valor.</span><span class="sxs-lookup"><span data-stu-id="f588b-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="f588b-120">El módulo Puntuar modelo produce resultados incorrectos</span><span class="sxs-lookup"><span data-stu-id="f588b-120">Score Model Module produces incorrect results</span></span>

![imagen2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="f588b-122">En un experimento típico de entrenamiento y pruebas de aprendizaje supervisado, el módulo [Dividir datos][split] separa el conjunto de datos original en dos partes: una parte se utiliza para entrenar el modelo y la otra se reserva para puntuar el rendimiento del modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="f588b-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="f588b-123">A continuación, se usa el modelo entrenado para puntuar los datos de prueba y, luego, se evalúan los resultados para determinar la precisión del modelo.</span><span class="sxs-lookup"><span data-stu-id="f588b-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="f588b-124">El módulo [Puntuar modelo][score-model] requiere dos entradas:</span><span class="sxs-lookup"><span data-stu-id="f588b-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="f588b-125">Una salida de modelo entrenado del módulo [Entrenar modelo][train-model].</span><span class="sxs-lookup"><span data-stu-id="f588b-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="f588b-126">Un conjunto de datos de puntuación que sea diferente del conjunto de datos utilizado para entrenar el modelo.</span><span class="sxs-lookup"><span data-stu-id="f588b-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="f588b-127">Es posible que, aunque el experimento se realice correctamente, el módulo [Puntuar modelo][score-model] produzca resultados incorrectos.</span><span class="sxs-lookup"><span data-stu-id="f588b-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="f588b-128">Varios escenarios pueden provocar que esto ocurra:</span><span class="sxs-lookup"><span data-stu-id="f588b-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="f588b-129">Si la etiqueta especificada es de categoría y se entrena un modelo de regresión con los datos, módulo de [Puntuar modelo][score-model] genera una salida incorrecta.</span><span class="sxs-lookup"><span data-stu-id="f588b-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="f588b-130">Esto es debido a que la regresión requiere una variable de respuesta continua.</span><span class="sxs-lookup"><span data-stu-id="f588b-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="f588b-131">En este caso, sería más adecuado usar un modelo de clasificación.</span><span class="sxs-lookup"><span data-stu-id="f588b-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="f588b-132">De forma similar, si un modelo de clasificación se entrena con un conjunto de datos con números de punto flotante en la columna de etiqueta, se podrían producir resultados no deseados.</span><span class="sxs-lookup"><span data-stu-id="f588b-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="f588b-133">Esto es debido a que la clasificación requiere una variable de respuesta discreta que solo permite valores que abarcan un conjunto finito y generalmente bastante pequeño de clases.</span><span class="sxs-lookup"><span data-stu-id="f588b-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="f588b-134">Si el conjunto de datos de puntuación no contiene todas las características que se usan para entrenar el modelo, [Puntuar modelo][score-model] generará un error.</span><span class="sxs-lookup"><span data-stu-id="f588b-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="f588b-135">Si una fila del conjunto de datos de puntuación contiene un valor que falte o un valor infinito de cualquiera de sus características, [Puntuar modelo][score-model] no producirá ningún resultado correspondiente a esa fila.</span><span class="sxs-lookup"><span data-stu-id="f588b-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="f588b-136">[Puntuar modelo][score-model] puede producir resultados idénticos para todas las filas del conjunto de datos de puntuación.</span><span class="sxs-lookup"><span data-stu-id="f588b-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="f588b-137">Esto puede ocurrir, por ejemplo, cuando se intenta la clasificación mediante bosques de decisión, si se elige que el número mínimo de muestras por cada nodo de hoja sea mayor que el número de ejemplos de aprendizaje disponibles.</span><span class="sxs-lookup"><span data-stu-id="f588b-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

