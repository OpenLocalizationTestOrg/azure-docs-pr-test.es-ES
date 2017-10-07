---
title: "aaaFeature ingeniería y selección de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Explica con fines de Hola de selección de características y la ingeniería de característica y proporciona ejemplos de su función en el proceso de mejora de los datos de Hola de aprendizaje automático."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Diseño y selección de características en Aprendizaje automático de Azure
Este tema explica con fines de Hola de ingeniería de característica y selección de características en el proceso de mejora de los datos de Hola de aprendizaje automático. Este tema muestra lo que implican estos procesos con ejemplos que ofrece Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

datos de entrenamiento de Hello utilizados en el aprendizaje automático a menudo se pueden mejorar mediante la selección de Hola o extracción de características de datos sin procesar de hello recopilados. Un ejemplo de una característica de ingeniería en contexto de Hola de aprender cómo las imágenes de hello tooclassify de caracteres escrito a mano es un mapa de bits densidad construido a partir de datos de distribución de Hola bit sin formato. Esta asignación puede ayudar a encontrar bordes Hola de caracteres de hello forma más eficiente que la distribución de hello sin formato.

Características de ingeniería y seleccionadas aumentan la eficacia de hello del proceso de entrenamiento de hello, que intenta tooextract Hola clave la información contenida en los datos de Hola. También mejoran la potencia de Hola de estos datos de entrada de modelos tooclassify Hola con precisión y resultados de toopredict de interesan más Fortalezca de forma. Característica ingeniería y la selección también pueden combinar aprendizaje de hello toomake manejable más procesamiento. Para ello, mejorar y, a continuación, lo que reduce número Hola de características necesario toocalibrate o entrenar un modelo. Matemáticamente hablando, modelo de Hola de hello características tootrain seleccionados son un conjunto mínimo de variables independientes que expliquen los patrones de hello en los datos de hello y, a continuación, predecir correctamente los resultados.

ingeniería de Hola y selección de características es una parte de un proceso mayor, que normalmente consta de cuatro pasos:

* Colección de datos
* Mejora de datos
* Construcción del modelo
* Posprocesamiento

Ingeniería y selección son Hola paso de mejora de datos de aprendizaje automático. Para nuestros propósitos, es posible distinguir tres aspectos de este proceso:

* **Preprocesamiento de datos**: este proceso tooensure de intentos que los datos recopilados de Hola esté limpio y coherente. Incluye tareas como la integración de varios conjuntos de datos, el control de los datos que faltan, el control de datos incoherentes y la conversión de los tipos de datos.
* **Característica ingeniería**: características adicionales de relevante toocreate características sin formato existente de hello en hello datos y tooincrease predictiva toohello algoritmo de aprendizaje de intentos de este proceso.
* **Selección de características**: este proceso selecciona subconjunto de clave de Hola de dimensiones del Hola de tooreduce de características de originales datos de problema de entrenamiento de Hola.

En este tema solo cubre Hola característica ingeniería y la característica de selección aspectos Hola datos mejora del proceso de. Para obtener más información sobre el paso de previas al procesamiento de datos de hello, consulte [procesar previamente los datos en estudio de aprendizaje automático de Azure](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Creación de características a partir de sus datos: diseño de características
los datos de entrenamiento de Hello constan de una matriz formada por ejemplos (registros o las observaciones que se almacenan en filas), cada uno de los cuales tiene un conjunto de características (variables o campos almacenados en columnas). características de Hello especificadas en el procedimiento experimental Hola son toocharacterize esperado Hola patrones en datos de Hola. Aunque muchos de los datos sin procesar de hello campos pueden incluirse directamente en hello tootrain de la característica seleccionada conjunto usa un modelo, las características adicionales de ingeniería suelen necesitan toobe construido a partir de las características de hello en datos sin procesar de hello toogenerate un conjunto de datos de entrenamiento mejorada.

¿Qué tipos de características se deben crear conjunto de datos de hello tooenhance al entrenar un modelo? Ingeniería características que mejoran la formación de hello proporcionan información que diferencia mejor los patrones de hello en los datos de Hola. Esperar Hola nuevas características tooprovide información adicional que no sea evidente en hello original o claramente capturado o conjunto de características existentes, pero este proceso es un arte. Las decisiones acertadas y productivas a menudo requieren cierto conocimiento especializado.

Cuando a partir de aprendizaje automático de Azure, es más fácil toograsp este proceso en concreto mediante el uso de ejemplos proporciona en estudio de aprendizaje automático. Aquí se muestran dos ejemplos:

* Un ejemplo de regresión ([predicción del número de Hola de alquiler de bicicletas](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) en un experimento supervisado, donde se conocen los valores de destino de Hola
* Un ejemplo de clasificación de minería de texto con [Hash de características][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Ejemplo 1: Incorporación de características temporales para un modelo de regresión
toodemonstrate cómo tooengineer funciones en una tarea de regresión, vamos a usar Hola experimento "previsión de demanda de bicicletas" en estudio de aprendizaje automático de Azure. objetivo de Hola de este experimento es petición de hello toopredict de bicicletas de hello, es decir, el número de Hola de alquiler de bicicletas dentro de un mes concreto, día o una hora. conjunto de datos de Hello **conjunto de datos UCI de alquiler de bicicletas** se utiliza como datos de entrada sin formato de saludo.

Este conjunto de datos se basa en datos reales de hello empresa Capital Bikeshare que mantiene una red de alquiler de bicicletas en Washington DC Hola Estados Unidos. conjunto de datos de Hello representa el número de Hola de alquiler de bicicletas dentro de una hora concreta de un día, desde 2011 too2012 y contiene 17379 filas y 17 columnas. conjunto de características sin procesar de Hello contiene las condiciones meteorológicas (temperatura, humedad, velocidad del viento) y el tipo de saludo del día de hello (vacaciones o día de la semana). Hola campo toopredict es **cnt**, un número que representa el alquiler de bicicletas de hello dentro de una hora concreta y que va de 1 too977.

tooconstruct características efectiva en los datos de entrenamiento de hello, cuatro de los modelos de regresión se generan usando Hola mismo algoritmo, pero con cuatro de los datos de entrenamiento diferentes establece. Hola cuatro conjuntos de datos representan Hola los mismos datos de entrada sin formato, pero con un creciente número de características establecido. Estas características se agrupan en cuatro categorías:

1. A = tiempo vacaciones + weekday + fines de semana características día predicho Hola
2. B = número de bicicletas alquiladas en cada uno de hello anteriores 12 horas
3. C = número de bicicletas se alquiladas en cada uno de hello anteriores 12 días en hello igual de hora
4. D. = número de bicicletas se alquiladas en cada uno de hello anteriores 12 semanas a Hola mismo hello y hora el mismo día

Además de un conjunto de característica, que ya existe en los datos sin formato originales de hello, hello otros tres conjuntos de características se crean a través de la característica de hello proceso de ingeniería. Conjunto de características B capturas Hola reciente demanda de bicicletas de Hola. Conjunto de características C capturas petición Hola de bicicletas en una hora determinada. Establecer la característica de D capturas demanda de bicicletas a determinada hora y día concreto de la semana de Hola. Cada uno de los conjuntos de datos de entrenamiento de hello cuatro incluye conjuntos de características A, A + B, A + B + C y A + B + C + D, respectivamente.

Hola experimento de aprendizaje automático de Azure, estos cuatro conjuntos de datos de entrenamiento se forman a través de cuatro ramas de conjunto de datos de entrada preprocesados de Hola. Excepto para la bifurcación del extremo izquierdo hello, cada una de estas bifurcaciones contiene un [ejecutar Script de R] [ execute-r-script] módulo en el que un conjunto de derivado características (conjuntos de características B, C y D) se construye y se anexa respectivamente toohello importa el conjunto de datos. Hola figura siguiente muestra el script de Hola R utiliza toocreate conjunto de características B en la segunda bifurcación izquierdo de Hola.

![Creación de un conjunto de características](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Hello siguiente tabla resume comparación Hola de resultados de rendimiento de Hola de cuatro modelos de Hola. obtener los mejores resultados de Hola se muestran de características A + B + C. Tenga en cuenta que esa tasa de errores de hello disminuye cuando conjuntos de características adicionales se incluyen en los datos de entrenamiento de Hola. Esto comprueba nuestro suposición que Hola conjuntos de características B y C proporcionan información adicional relevante para la tarea de regresión de hello. Agregar conjunto de características de hello D parece no tooprovide cualquier reducción adicional en la tasa de errores de Hola.

![Comparar los resultados de rendimiento](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> Ejemplo 2: Creación de características en minería de texto
Característica ingeniería se aplica ampliamente en tootext relacionado de tareas de minería de datos, como el análisis de clasificación y opiniones de documento. Por ejemplo, cuando quiera tooclassify documentos en varias categorías, una suposición típica es que palabras de Hola o frases incluidos en la categoría de un documento son menos probable que toooccur en otra categoría de documento. En otras palabras, frecuencia de Hola de distribución de palabra o frase hello es capaz de toocharacterize categorías de documento diferente. En las aplicaciones de minería de datos de texto, proceso de ingeniería de característica de Hola es características de Hola de toocreate necesarios implicadas en la palabra o frase frecuencias porque las partes individuales de contenido de texto normalmente funcionan como Hola datos de entrada.

tooachieve esta tarea, una técnica denominada *hash de características* es tooefficiently aplicado características en índices de texto arbitrarios. En lugar de asociar cada característica (palabras o frases) tooa determinado índice de texto, este método funciona aplicando un características toohello de función de hash y directamente con sus valores hash como índices.

En Azure Machine Learning, existe un módulo de [Hash de características][feature-hashing] que crea estas características de palabras o frases. Hello en la ilustración siguiente se muestra un ejemplo del uso de este módulo. conjunto de datos de entrada de Hello contiene dos columnas: clasificación de libreta de hello comprendido entre 1 hello y too5 real revisión del contenido. objetivo de Hola de este [hash de características] [ feature-hashing] módulo es tooretrieve nuevas características que muestran la frecuencia de aparición de Hola de palabras correspondiente de Hola o frases dentro de revisión de libro en particular de Hola. toouse este módulo, necesita hello toocomplete pasos:

1. Columna de hello SELECT que contiene el texto de entrada de hello (**Col2** en este ejemplo).
2. Establecer *hash de tamaño de bits* too8, lo que significa 2 ^ 8 = 256 características se crean. Hola palabra o frase en el texto hello es, a continuación, aplica un algoritmo hash too256 índices. Hola parámetro *hash de tamaño de bits* comprendido entre 1 too31. Si el parámetro hello se establece tooa mayor número, Hola de palabras o frases están menos probable que toobe aplica un algoritmo hash en hello mismo índice.
3. Establezca el parámetro hello *n-gramas* too2. Esta opción recupera frecuencia de aparición de Hola de (una característica para cada palabra única) de unigramas y bigramas (una característica para cada par de palabras adyacentes) de texto de entrada de Hola. Hola parámetro *n-gramas* comprendido entre 0 too10, lo que indica el número máximo de Hola de toobe palabras secuencial incluido en una característica.  

![Módulo de hash de características](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Hello en la ilustración siguiente se muestra el aspecto de estas nuevas características.

![Ejemplo de hash de características](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Filtrado de características desde sus datos: selección de características
*Selección de características* es un proceso que suele ser aplica toohello construcción de conjuntos de datos de entrenamiento para tareas de modelado de predicción, como tareas de clasificación o regresión. objetivo de Hello es un subconjunto de características de Hola Hola original en conjunto de datos que reduce sus dimensiones mediante el uso de un conjunto mínimo de cantidad máxima Hola de características toorepresent de varianza en los datos de hello tooselect. Este subconjunto de características contiene Hola solo características toobe incluida tootrain Hola modelo. La selección de características tiene dos propósitos principales:

* La selección de características a menudo aumenta la precisión de la clasificación a través de la eliminación de características irrelevantes, redundantes o altamente correlacionadas.
* Característica selección disminuye Hola número de características, que hace que el proceso de entrenamiento del modelo de hello sea más eficaces. Esto es especialmente importante para aprendices que son costosa tootrain como las máquinas de vectores de soporte técnico.

Aunque la selección de características búsquedas tooreduce número de Hola de funciones hello conjunto de datos usa tootrain Hola modelo, no es normalmente a que se refiere término de hello tooby *reducir la dimensionalidad.* Métodos de selección de características extraen un subconjunto de características originales de los datos de hello sin modificarlas.  Métodos de reducción de dimensionalidad utilizan funciones de ingeniería que se pueden transformar características original de hello y, por tanto, modificarlos. Algunos ejemplos de métodos de reducción de dimensionalidad incluyen el análisis del componente principal, el análisis de correlación canónica y la descomposición en valores singulares.

Una categoría ampliamente aplicada de los métodos de selección de características en un contexto supervisado se llama selección de características basada en filtro. Mediante la evaluación de correlación de hello entre cada atributo de destino hello y características, estos métodos aplican un tooassign medida estadística una característica de tooeach de puntuación. Hello características se clasifican por puntuación de hello, que puede usar umbral de hello tooset para mantener o eliminar una característica específica. Correlación de Pearson, la información mutua y prueba de chi cuadrado Hola son ejemplos de medidas estadísticas Hola utilizadas en estos métodos.

Azure Machine Learning Studio incluye módulos para la selección de características. Como se muestra en la figura siguiente de Hola, estos módulos incluyen [selección de características basada en filtros] [ filter-based-feature-selection] y [análisis discriminante lineal de Fisher] [ fisher-linear-discriminant-analysis].

![Ejemplo de selección de características](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Por ejemplo, usar hello [selección de características basada en filtros] [ filter-based-feature-selection] módulo con el ejemplo de minería de datos de texto hello descrito anteriormente. Suponga que desea toobuild un modelo de regresión después de crea un conjunto de características de 256 a través de hello [hash de características] [ feature-hashing] módulo y esa variable de respuesta de hello es **Col1**y representa un libro revisar clasificación comprendido entre 1 too5. Establecer **método de puntuación de características** demasiado**correlación de Pearson**, **columna de destino** demasiado**Col1**, y **deseado de número de características** demasiado**50**. módulo de Hello [selección de características basada en filtros] [ filter-based-feature-selection] , a continuación, genera un conjunto de datos que contiene 50 características junto con el atributo de destino de hello **Col1**. Hola a continuación figura muestra hello flujo de este experimento y Hola parámetros de entrada.

![Ejemplo de selección de características](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Hello en la ilustración siguiente se muestra hello conjuntos de datos resultante. Cada característica es una puntuación basada en la correlación de Pearson entre él y Hola Hola atributo target **Col1**. características de Hello con puntuaciones más altas se mantienen.

![Conjuntos de datos de selección de características basada en filtros](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Hola siguiente figura muestra Hola correspondientes puntuaciones de características de hello seleccionado.

![Puntuaciones de las características seleccionadas](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Aplicando esto [selección de características basada en filtros] [ filter-based-feature-selection] módulo, se seleccionan características porque tienen Hola mayoría de las características que se correlacionan con variable de destino de hello 50 fuera de 256 **Col1** basado en método de puntuación de hello **correlación de Pearson**.

## <a name="conclusion"></a>Conclusión
Ingeniería de característica y selección de características son dos pasos usuales de datos de entrenamiento de hello tooprepare al generar un modelo de aprendizaje automático. Normalmente, ingeniería de característica es aplicado primeras características adicionales de toogenerate y, a continuación, el paso de selección de características de hello es realizada tooeliminate irrelevante y redundante o características altamente correlacionadas.

No siempre es necesariamente tooperform selección de ingeniería o una característica de característica. Si es necesario depende de datos de hello tiene o recopilar, se elige, el algoritmo de Hola y Hola objetivo del experimento de Hola.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
