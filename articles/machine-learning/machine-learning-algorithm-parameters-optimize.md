---
title: "aaaOptimize sus algoritmos de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Explica cómo establece el parámetro óptimo de hello toochoose un algoritmo de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Elegir parámetros toooptimize sus algoritmos de aprendizaje automático de Azure
Este tema describe cómo establece toochoose Hola derecho hyperparameter un algoritmo de aprendizaje automático de Azure. La mayoría de los algoritmos de aprendizaje de máquina tiene parámetros tooset. Cuando se entrena un modelo, debe tooprovide valores para esos parámetros. eficacia de Hola de modelo entrenado Hola depende de los parámetros de modelo de Hola que elija. Hello proceso de búsqueda de conjunto óptimo de Hola de parámetros se denomina *selección de modelo*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

No hay selección del modelo de toodo de diversas maneras. En el aprendizaje automático, la validación cruzada es uno de los métodos de Hola que más se usan para la selección de modelo y es el mecanismo de selección de modelo de hello predeterminado en el aprendizaje automático de Azure. Como R y Python son compatibles con Azure Machine Learning, siempre puede implementar sus propios mecanismos de selección de modelo mediante R o Python.

Hay cuatro pasos en proceso de Hola de encontrar Hola mejor conjunto de parámetros:

1. **Definir espacio de parámetro hello**: para el algoritmo de hello, decida primero valores de parámetro exacto de Hola que desee tooconsider.
2. **Definir la configuración de validación cruzada de Hola**: decidir cómo se contrae toochoose la validación cruzada para el conjunto de datos de Hola.
3. **Definir métrica Hola**: decida qué toouse métrica para determinar el mejor conjunto de parámetros, como la precisión de hello, raíz cuadrada cuadrático medio error, precisión, recuperación o valor f.
4. **Entrenar, evaluar y comparar**: para cada combinación única de valores de parámetro de hello, la validación cruzada es realizada por y en función de la métrica de error de Hola que define. Después de la evaluación y la comparación, puede elegir modelo perfecto rendimiento Hola.

Hola después de la imagen de muestra se muestra cómo se puede lograr de aprendizaje automático de Azure.

![Buscar Hola mejor conjunto de parámetros](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Definir espacio de parámetro hello
Puede definir el parámetro hello establecido en el paso de inicialización del modelo de Hola. panel de parámetros de todos los algoritmos de aprendizaje automático Hello tiene dos modos de entrenamiento: *único parámetro* y *intervalo de parámetros*. Elija el modo del intervalo de parámetros. En el modo del intervalo de parámetros, puede escribir varios valores para cada parámetro. Puede especificar valores separados por comas en el cuadro de texto de Hola.

![Árbol de decisión ampliado de dos clases, único parámetro](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 Como alternativa, puede definir puntos máxima y mínima de Hola de cuadrícula de Hola y Hola el número total de toobe de puntos que se genera con **usar generador de intervalo**. De forma predeterminada, los valores de parámetro de Hola se generan en una escala lineal. Pero si **escala logarítmica** se activa, se generan valores de hello en escala de registro de hello (es decir, relación de Hola de puntos adyacentes hello es constante en lugar de su diferencia). Para los parámetros de número entero, puede definir un intervalo con un guión. Por ejemplo, "1-10" significa que todos los enteros entre 1 y 10 (ambos inclusive) forman el conjunto de parámetros de Hola. También se admite un modo mixto. Hola, por ejemplo, el conjunto de parámetros "1-10, 20, 50" incluiría enteros de 1 a 10, 20 y 50.

![Árbol de decisión ampliado de dos clases, intervalo de parámetros](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Definir los plegamientos de validación cruzada
Hola [crear particiones y muestrear] [ partition-and-sample] módulo puede ser usado toorandomly asignar subconjuntos toohello datos. En hello después de la configuración de ejemplo para el módulo de hello, definimos cinco pliegues y asignar al azar a su vez número instancias de ejemplo toohello.

![Partición y ejemplo](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Definir métrica Hola
Hola [optimizar modelo Hiperparámetros] [ tune-model-hyperparameters] módulo proporciona compatibilidad para elegir empíricamente Hola mejor conjunto de parámetros para un algoritmo dado y un conjunto de datos. Además tooother información sobre Hola de entrenamiento del modelo, hello **propiedades** panel de este módulo incluye métrica de Hola para determinar el mejor conjunto de parámetros Hola. Tiene dos cuadros de lista desplegables diferentes para los algoritmos de clasificación y regresión, respectivamente. Si el algoritmo de hello en cuestión es un algoritmo de clasificación, se omite la métrica de regresión de Hola y viceversa. En este ejemplo concreto, métrica de hello es **precisión**.   

![Limpiar parámetros](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Formar, evaluar y comparar
Hola mismo [optimizar modelo Hiperparámetros] [ tune-model-hyperparameters] módulo entrena todos los modelos de hello corresponden toohello conjunto de parámetros, se evalúa como varias métricas y, a continuación, crea Hola perfecto entrenado en función de Hola métrica que elija. Este módulo contiene dos entradas obligatorias:

* aprendiz no entrenado Hola
* conjunto de datos de Hola

módulo de Hello también tiene un conjunto de datos opcional de entrada. Conecte el conjunto de datos de hello con entrada de plegamiento información toohello obligatorio del conjunto de datos. Si el conjunto de datos de hello no se asigna ninguna información de plegamiento, una validación cruzada 10 veces más rápidos se ejecuta automáticamente de forma predeterminada. Si no se realiza la asignación de subconjuntos de Hola y se proporciona un conjunto de datos de validación en el puerto del conjunto de datos opcional de hello, a continuación, se elige un modo de prueba de entrenamiento y Hola primer conjunto de datos es el modelo de Hola de tootrain utilizado para cada combinación de parámetros.

![Clasificador del árbol de decisión ampliado](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

modelo de Hello, a continuación, se evalúa en el conjunto de datos de validación de Hola. Hola deja puerto de salida de muestra de Hola módulo diferentes métricas como las funciones de valores de parámetro. Hola derecho de puerto de salida proporciona entrenado Hola correspondiente toohello modelo perfecto rendimiento según toohello elegido métrica (**precisión** en este caso).  

![Conjunto de datos de validación](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Puede ver los parámetros exactos Hola elegido al visualizar el puerto de salida derecho de Hola. Este modelo puede utilizarse para determinar la puntuación de un conjunto de pruebas o en un servicio web de operaciones después de guardarlo como un modelo formado.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
