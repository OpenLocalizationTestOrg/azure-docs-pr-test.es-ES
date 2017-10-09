---
title: "selección de aaaFeature Hola proceso de ciencia de datos de equipo | Documentos de Microsoft"
description: "Explica el propósito de Hola de selección de características y proporciona ejemplos de su función en el proceso de mejora de hello datos de aprendizaje automático."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Selección de características en hello proceso de ciencia de datos de equipo (TDSP)
En este artículo se explica con fines de Hola de selección de características y proporciona ejemplos de su función en el proceso de mejora de hello datos de aprendizaje automático. Estos ejemplos se extraen de Estudio de aprendizaje automático de Azure. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Hola de ingeniería y selección de características es una parte del programa Hola a ciencia de datos de equipo proceso (TDSP) que se describen en [¿qué es hello proceso de ciencia de datos de equipo?](data-science-process-overview.md). Característica ingeniería y selección son partes de hello **desarrollar características** paso de hello TDSP.

* **característica ingeniería**: características adicionales de relevante toocreate características sin formato existente de hello en datos de Hola y algoritmo de aprendizaje de toohello tooincrease predictiva de intentos de este proceso.
* **selección de características**: este proceso selecciona subconjunto de clave de Hola de características de datos original en una dimensionalidad de hello tooreduce intento de problema de entrenamiento de Hola.

Normalmente **característica ingeniería** es aplicado primeras características adicionales de toogenerate y, a continuación, hello **selección de características** paso es realizar tooeliminate altamente correlacionada, redundante o irrelevante características.

## <a name="filtering-features-from-your-data---feature-selection"></a>Filtrado de características desde sus datos: selección de características
Selección de características es un proceso que se suele aplicar para la construcción de Hola de conjuntos de datos de entrenamiento para tareas de modelado de predicción, como tareas de clasificación o regresión. objetivo de Hello es un subconjunto de características de Hola de conjunto de datos original de Hola que reducen sus dimensiones mediante el uso de un conjunto mínimo de cantidad máxima Hola de características toorepresent de varianza en los datos de hello tooselect. Este subconjunto de características son, a continuación, Hola solo características toobe incluye el modelo de hello tootrain. La selección de características tiene dos propósitos principales.

* En primer lugar, la selección de características a menudo aumenta la precisión de la clasificación a través de la eliminación de características irrelevantes, redundantes o altamente correlacionadas.
* En segundo lugar, se reduce el número de Hola de características que hace que el proceso de entrenamiento del modelo sea más eficaces. Esto es especialmente importante para aprendices que son costosa tootrain como las máquinas de vectores de soporte técnico.

Aunque la selección de características de búsqueda número de hello tooreduce de funciones hello conjunto de datos usado tootrain Hola modelo, no es normalmente lo que se conoce tooby Hola término "reducción de dimensionalidad". Métodos de selección de características extraen un subconjunto de características originales de los datos de hello sin modificarlas.  Métodos de reducción de dimensionalidad utilizan funciones de ingeniería que se pueden transformar características original de hello y, por tanto, modificarlos. Algunos ejemplos de los métodos de reducción de dimensionalidad incluyen el análisis del componente principal, el análisis de correlación canónica y la descomposición en valores singulares.

Entre otros aspectos, una categoría ampliamente aplicada de los métodos de selección de categorías en un contexto supervisado se llama "selección de características basada en filtro". Mediante la evaluación de correlación de hello entre cada atributo de destino hello y características, estos métodos aplican un tooassign medida estadística una característica de tooeach de puntuación. características de Hello, a continuación, se clasifican por puntuación de hello, que puede ser el umbral de hello establecido toohelp usado para mantener o eliminar una característica específica. Algunos ejemplos de medidas estadísticas Hola utilizados en estos métodos son correlación persona, la información mutua y prueba de hello Chi cuadrado.

En Estudio de aprendizaje automático de Azure, estos son los módulos proporcionados para la selección de características. Como se muestra en la figura siguiente de Hola, estos módulos incluyen [selección de características basada en filtros] [ filter-based-feature-selection] y [análisis discriminante lineal de Fisher] [ fisher-linear-discriminant-analysis].

![Ejemplo de selección de características](./media/machine-learning-data-science-select-features/feature-Selection.png)

Considere, por ejemplo, uso de Hola de hello [selección de características basada en filtros] [ filter-based-feature-selection] módulo. A fin de Hola de comodidad, seguimos ejemplo de minería de datos de texto toouse Hola descrita anteriormente. Supongamos que queremos toobuild un modelo de regresión después de un conjunto de 256 características creadas a través de hello [hash de características] [ feature-hashing] módulo y esa variable de respuesta de hello es "Col1" hello y representa un libro Revise las clasificaciones que van desde 1 too5. Estableciendo "Método de puntuación de la característica" toobe "Correlación de Pearson" Hola "Columna de destino" toobe "Col1" y Hola "Número de características deseadas" too50. A continuación, el módulo de hello [selección de características basada en filtros] [ filter-based-feature-selection] generará un conjunto de datos que contiene 50 características junto con el atributo de destino de Hola "Col1". Hola a continuación figura muestra hello flujo de este experimento y Hola parámetros de entrada que acabamos de describir.

![Ejemplo de selección de características](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Hello en la ilustración siguiente se muestra hello conjuntos de datos resultante. Cada característica es una puntuación basada en hello correlación de Pearson entre sí y Hola "Col1" del atributo de destino. características de Hello con puntuaciones más altas se mantienen.

![Ejemplo de selección de características](./media/machine-learning-data-science-select-features/feature-Selection2.png)

puntuaciones correspondiente Hola de características de hello seleccionado se muestran en hello figura siguiente.

![Ejemplo de selección de características](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Aplicando esto [selección de características basada en filtros] [ filter-based-feature-selection] módulo, 50 fuera de 256 características están seleccionadas porque han Hola más características correlacionadas con variable de destino de Hola "Col1", en función de la puntuación de Hola método "Correlación de Pearson".

## <a name="conclusion"></a>Conclusión
Ingeniería de característica y selección de características son dos habitualmente de ingeniería y características seleccionadas aumentan la eficacia de Hola de hello entrenamiento proceso que intenta tooextract Hola clave la información contenida en los datos de Hola. También mejoran la potencia de Hola de estos datos de entrada de modelos tooclassify Hola con precisión y resultados de toopredict de interesan más Fortalezca de forma. Característica ingeniería y la selección también pueden combinar aprendizaje de hello toomake manejable más procesamiento. Para ello, mejorar y, a continuación, lo que reduce número Hola de características necesario toocalibrate o entrenar un modelo. Matemáticamente hablando, modelo de Hola de hello características tootrain seleccionados son un conjunto mínimo de variables independientes que expliquen los patrones de hello en los datos de hello y, a continuación, predecir correctamente los resultados.

Tenga en cuenta que no siempre es necesariamente tooperform selección de ingeniería o una característica de característica. Si es necesario o no depende de datos de hello disponemos o recopilar, hemos elegido, el algoritmo de Hola y Hola objetivo del experimento de Hola.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

