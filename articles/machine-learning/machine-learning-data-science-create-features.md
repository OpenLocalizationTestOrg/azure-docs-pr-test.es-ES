---
title: "ingeniería aaaFeature de ciencia de datos | Documentos de Microsoft"
description: "Explica con fines de Hola de ingeniería de características y proporciona ejemplos de su función en el proceso de mejora de hello datos de aprendizaje automático."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>Ingeniería de características en ciencia de datos
En este tema se explica con fines de Hola de ingeniería de características y proporciona ejemplos de su función en el proceso de mejora de hello datos de aprendizaje automático. ejemplos de Hello usar tooillustrate este proceso se extraen del estudio de aprendizaje automático de Azure. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Esto **menú** vincula tootopics que describen cómo toocreate características para los datos en varios entornos. Esta tarea es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Las características de ingeniería intentos tooincrease Hola predictiva de algoritmos de aprendizaje mediante la creación de características de los datos sin procesar que facilitan el proceso de aprendizaje de Hola. Hola de ingeniería y selección de características es una parte de hello TDSP descrito en hello [¿qué es el ciclo de vida de hello proceso de ciencia de datos de equipo?](data-science-process-overview.md) Característica ingeniería y selección son partes de hello **desarrollar características** paso de hello TDSP. 

* **característica ingeniería**: este proceso intenta características adicionales de relevante toocreate de características sin formato existente de hello en datos de Hola y tooincrease Hola predictiva de algoritmo de aprendizaje de Hola.
* **selección de características**: este proceso selecciona subconjunto de clave de Hola de características de datos original en una dimensionalidad de hello tooreduce intento de problema de entrenamiento de Hola.

Normalmente **característica ingeniería** es aplicado primeras características adicionales de toogenerate y, a continuación, hello **selección de características** paso es realizar tooeliminate altamente correlacionada, redundante o irrelevante características.

a menudo se pueden mejorar los datos de entrenamiento Hola utilizados en el aprendizaje automático extracción de características de datos sin procesar de hello recopilados. Un ejemplo de una característica de ingeniería en contexto de Hola de aprender cómo imágenes de hello tooclassify de caracteres escrito a mano es la creación de asignación de densidad un poco construido a partir de datos de distribución de Hola bit sin formato. Esta asignación puede ayudar a encontrar bordes Hola de caracteres de hello forma más eficiente que simplemente con distribución sin procesar de hello directamente.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>Creación de características a partir de sus datos: diseño de características
los datos de entrenamiento de Hello constan de una matriz formada por ejemplos (registros o las observaciones que se almacenan en filas), cada uno de los cuales tiene un conjunto de características (variables o campos almacenados en columnas). características de Hello especificadas en el procedimiento experimental Hola son toocharacterize esperado Hola patrones en datos de Hola. Aunque muchos de los datos sin procesar de hello campos pueden incluirse directamente en hello tootrain de la característica seleccionada conjunto usa un modelo, a menudo resulta caso Hola que otras características (ingeniería) necesitan toobe construido a partir de características de hello en toogenerate de datos sin procesar de hello una mejorada conjunto de datos de entrenamiento.

¿Qué tipos de características se deben crear el conjunto de datos de tooenhance Hola al entrenar un modelo? Ingeniería características que mejoran la formación de hello proporcionan información que diferencia mejor los patrones de hello en los datos de Hola. Esperamos que Hola nuevas características tooprovide información adicional que no es el conjunto de características original o existente de hello claramente capturado o evidente en. Pero este proceso es, en cierto modo, un arte. Las decisiones acertadas y productivas a menudo requieren cierto conocimiento especializado.

Cuando a partir de aprendizaje automático de Azure, es más fácil toograsp este proceso en concreto mediante ejemplos proporcionado en hello Studio. Aquí se muestran dos ejemplos:

* Un ejemplo de regresión [predicción del número de Hola de alquiler de bicicletas](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) en un experimento supervisado, donde se conocen los valores de destino de Hola
* Un ejemplo de clasificación de minería de texto con [Hash de características](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>Ejemplo 1: incorporación de características temporales para el modelo de regresión
Vamos a usar Hola experimento "previsión de demanda de bicicletas" en cómo las características de tooengineer de toodemonstrate de estudio de aprendizaje automático de Azure para una tarea de regresión. objetivo de Hola de este experimento es petición de hello toopredict de bicicletas de hello, es decir, el número de Hola de alquiler de bicicletas dentro de una mes, día y hora específica. Hola dataset "alquiler de bicicletas conjunto de datos UCI" se utiliza como datos de entrada sin formato de saludo. Este conjunto de datos se basa en datos reales de hello empresa Capital Bikeshare que mantiene una red de alquiler de bicicletas en Washington DC Hola Estados Unidos. conjunto de datos de Hello representa el número de Hola de alquiler de bicicletas en una hora concreta de un día de años de hello 2011 y año 2012 y contiene 17379 filas y 17 columnas. conjunto de características sin procesar de Hola contiene condiciones meteorológicas (velocidad de temperatura y humedad/viento) y tipo de Hola de hello día (día festivo/día de la semana). Hola campo toopredict es "cnt", que es un número que representa alquileres de bicicletas de hello dentro de una hora concreta y que va de 1 too977 de intervalos.

Con el objetivo de Hola de creación de eficaces características de datos de entrenamiento de hello, cuatro de los modelos de regresión se compilan con hello mismo algoritmo, pero con cuatro conjuntos de datos de entrenamiento diferentes. Hola cuatro conjuntos de datos representan Hola los mismos datos de entrada sin formato, pero con un creciente número de características establecido. Estas características se agrupan en cuatro categorías:

1. A = tiempo vacaciones + weekday + fines de semana características día predicho Hola
2. B = número de bicicletas alquiladas en cada uno de hello anteriores 12 horas
3. C = número de bicicletas se alquiladas en cada uno de hello anteriores 12 días en hello igual de hora
4. D. = número de bicicletas se alquiladas en cada uno de hello anteriores 12 semanas a Hola mismo hello y hora el mismo día

Además de A conjunto de características, que ya existen en datos sin formato originales de hello, hello otros tres conjuntos de características se crean a través de la característica de hello proceso de ingeniería. Conjunto de características B capturas muy reciente demanda de bicicletas de Hola. Conjunto de características C capturas petición Hola de bicicletas en una hora determinada. Establecer la característica de D capturas demanda de bicicletas a determinada hora y día concreto de la semana de Hola. Hola cuatro entrenamiento conjuntos de datos cada incluye un conjunto de características, A + B, A + B + C y A + B + C + D, respectivamente.

Hola experimento de aprendizaje automático de Azure, estos cuatro conjuntos de datos de entrenamiento se forman a través de cuatro ramas de hello conjunto de datos de entrada preprocesados. Salvo hello izquierda bifurcación mayoría, cada una de estas bifurcaciones contiene un [ejecutar Script de R](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) módulo, en el que un conjunto de características derivadas (conjunto de características B, C y D) es el conjunto de datos de toohello respectivamente construido y anexados importado. Hola figura siguiente muestra el script de Hola R utiliza toocreate conjunto de características B en la segunda bifurcación izquierdo de Hola.

![crear funciones](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

comparación de Hola de resultados de rendimiento de Hola de hello en hello en la tabla siguiente se resumen las cuatro modelos. obtener los mejores resultados de Hola se muestran de características A + B + C. Tenga en cuenta que Hola disminuye de tasa de error al conjunto de características adicionales se incluyen en los datos de entrenamiento de Hola. Comprueba nuestro suposición que conjunto de características de hello B, C proporcionan información adicional relevante para la tarea de regresión de hello. Pero agregar característica Hola D parece no estar tooprovide cualquier reducción adicional en la tasa de errores de Hola.

![comparación de resultados](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a> Ejemplo 2: creación de características en minería de texto
Característica ingeniería se aplica ampliamente en tootext relacionado de tareas de minería de datos, como el análisis de clasificación y opiniones de documento. Por ejemplo, si queremos tooclassify documentos en varias categorías, una suposición típica es que Hola palabras o frases, incluidas en la categoría de un documento son menos probable que toooccur en otra categoría de doc. Dicho de otro modo, frecuencia de Hola de distribución de palabras o frases de hello es capaz de toocharacterize categorías de documento diferente. En las aplicaciones de minería de datos de texto, porque las partes individuales de contenido de texto normalmente funcionan como datos de entrada de hello, característica de hello ingeniería proceso es toocreate necesarios Hola características que implican las frecuencias de palabra o frase.

tooachieve esta tarea, una técnica denominada **hash de características** es tooefficiently aplicado características en índices de texto arbitrarios. En lugar de asociar cada característica (palabras o frases) tooa determinado índice de texto, este método funciona aplicando un características toohello de función de hash y con sus valores de hash como índices directamente.

En Aprendizaje automático de Azure, existe un módulo llamado [Hash de características](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) que crea oportunamente estas características de palabras/frases. La figura siguiente muestra un ejemplo del uso de este módulo. conjunto de datos de entrada de Hello contiene dos columnas: Hola clasificación libreta comprendido entre 1 too5 y Hola contenido real de revisión. objetivo de Hola de este [hash de características](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) módulo se tooretrieve una serie de nuevas características que muestran la frecuencia de aparición de Hola de hello correspondiente palabras o frases dentro de revisión de libro en particular de Hola. toouse este módulo, necesitamos hello toocomplete pasos:

* En primer lugar, seleccionar columna de Hola que contiene el texto de entrada de hello ("Col2" en este ejemplo).
* En segundo lugar, establezca hello too8 "Tamaño de bits de hash", lo que significa 2 ^ 8 = 256 características que se va a crear. Hello word/fase en todo el texto hello será índices hash too256. el parámetro Hello "Tamaño de bits de hash" comprendido entre 1 too31. Hola palabras o frases están toobe menos probable que aplica un algoritmo hash en el mismo índice si se establecer toobe un número mayor de Hola.
* En tercer lugar, establezca too2 de parámetro "N-gramas" Hola. Esta forma obtiene frecuencia de aparición de Hola de (una característica para cada palabra única) de unigramas y bigramas (una característica para cada par de palabras adyacentes) Hola texto de entrada. intervalos de "N-gramas" Hello parámetros de too10 0, lo que indica el número máximo de Hola de palabras secuencial toobe incluyen en una característica.  

![Módulo "Hash de características"](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

Hello en la ilustración siguiente se muestra lo que estos Hola nueva característica de aspecto.

![Ejemplo de "Hash de características"](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>Conclusión
Características de ingeniería y seleccionadas aumentan la eficacia de hello del proceso de entrenamiento de Hola que intenta tooextract Hola clave la información contenida en los datos de Hola. También mejoran la potencia de Hola de estos datos de entrada de modelos tooclassify Hola con precisión y resultados de toopredict de interesan más Fortalezca de forma. Característica ingeniería y la selección también pueden combinar aprendizaje de hello toomake manejable más procesamiento. Para ello, mejorar y, a continuación, lo que reduce número Hola de características necesario toocalibrate o entrenar un modelo. Matemáticamente hablando, modelo de Hola de hello características tootrain seleccionados son un conjunto mínimo de variables independientes que expliquen los patrones de hello en los datos de hello y, a continuación, predecir correctamente los resultados.

Tenga en cuenta que no siempre es necesariamente tooperform selección de ingeniería o una característica de característica. Si es necesario o no depende de datos de hello disponemos o recopilar, hemos elegido, el algoritmo de Hola y Hola objetivo del experimento de Hola.

