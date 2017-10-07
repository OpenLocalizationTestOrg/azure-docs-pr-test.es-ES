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
# <a name="debug-your-model-in-azure-machine-learning"></a>Depurar el modelo en Aprendizaje automático de Azure

Este artículo explica por qué cualquiera de hello después de dos errores puede producirse cuando se ejecuta un modelo de posibles razones de hello:

* Hola [entrenar modelo] [ train-model] módulo genera un error 
* Hola [puntuar modelo] [ score-model] module produce resultados incorrectos 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>El módulo Entrenar modelo produce un error

![imagen1](./media/machine-learning-debug-models/train_model-1.png)

Hola [entrenar modelo] [ train-model] módulo espera dos entradas:

1. tipo de Hola de modelo de aprendizaje automático de colección de Hola de modelos proporcionados por el aprendizaje automático de Azure.
2. datos de entrenamiento con una columna de etiqueta especificado que especifica Hola Hola toopredict variable (hello otras columnas se supone que las características de toobe).

Este módulo puede producir un error en hello casos siguientes:

1. columna de etiqueta de Hola se especificó correctamente. Esto puede ocurrir si se selecciona más de una columna como etiqueta de Hola o se selecciona un índice de columna es incorrecto. Por ejemplo, segundo caso de hello aplicaría si se utiliza un índice de columna de 30 años con un conjunto de datos de entrada que tiene 25 solo columnas.

2. Hola dataset no contiene ninguna columna de característica. Por ejemplo, si el conjunto de datos de entrada de hello tiene solo una columna, que se marca como columna de etiqueta de hello, no habría ninguna característica con qué modelo de hello toobuild. En este caso, Hola [entrenar modelo] [ train-model] módulo genera un error.

3. conjunto de entrada de datos Hello (características o etiqueta) contiene infinito como valor.

## <a name="score-model-module-produces-incorrect-results"></a>El módulo Puntuar modelo produce resultados incorrectos

![imagen2](./media/machine-learning-debug-models/train_test-2.png)

En un experimento de entrenamiento y pruebas típico de aprendizaje supervisado, Hola [dividir datos] [ split] módulo divide el conjunto de datos original de hello en dos partes: una parte es el modelo de Hola de tootrain usado y se usa una parte tooscore grado entrenado Hola realiza. modelo entrenado Hello es tooscore usado Hola datos de prueba, después del cual los resultados de hello son toodetermine evaluado Hola precisión del modelo de Hola.

Hola [puntuar modelo] [ score-model] módulo requiere dos entradas:

1. Una salida entrenado de hello [entrenar modelo] [ train-model] módulo.
2. Un conjunto de datos de puntuación que es diferente del conjunto de datos de hello usa modelos de hello tootrain.

Lo del posible que incluso si se realiza correctamente el experimento de hello, Hola [puntuar modelo] [ score-model] module produce resultados incorrectos. Varios escenarios pueden provocar esta toohappen:

1. Si Hola especifica la etiqueta es de categoría y un modelo de regresión está entrenado con datos de hello, se genera una salida incorrecta por hello [puntuar modelo] [ score-model] módulo. Esto es debido a que la regresión requiere una variable de respuesta continua. En este caso, sería más adecuado toouse un modelo de clasificación. 

2. De forma similar, si un modelo de clasificación está entrenado en un conjunto de datos con números de punto flotante en la columna de etiqueta de hello, se podrían producir resultados no deseados. Esto es debido a que la clasificación requiere una variable de respuesta discreta que solo permite valores que abarcan un conjunto finito y generalmente bastante pequeño de clases.

3. Si Hola la puntuación del conjunto de datos no contiene todos los modelos de hello tootrain de hello características que se utilizan, Hola [puntuar modelo] [ score-model] genera un error.

4. Si una fila de Hola la puntuación del conjunto de datos contiene un valor que falta o un valor infinito para cualquiera de sus características, Hola [puntuar modelo] [ score-model] no producirá ninguna fila toothat de salida correspondiente.

5. Hola [puntuar modelo] [ score-model] puede producir resultados idénticos para todas las filas de Hola la puntuación del conjunto de datos. Esto puede ocurrir, por ejemplo, al tratar de clasificación con bosques de decisión de si se elige Hola un número mínimo de muestras por nodo hoja toobe más de hello número de ejemplos de entrenamiento disponibles.

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

