---
title: "resultados del modelo aaaInterpret en aprendizaje automático | Documentos de Microsoft"
description: "Cómo parámetro óptimo de hello toochoose establecida para un algoritmo de uso y visualizar los resultados del modelo de puntuación."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Cómo interpretar los resultados del modelo de Azure Machine Learning
Este tema se explica cómo toovisualize e interpretar los resultados de predicción en estudio de aprendizaje automático de Azure. Después de entrenar un modelo y realizar predicciones sobre él ("puntúan modelo Hola"), es necesario toounderstand e interpretar los resultados de predicción de Hola.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Hay cuatro tipos de modelos de aprendizaje automático principales en Aprendizaje automático de Azure:

* clasificación
* agrupación en clústeres
* regresión
* Sistemas de recomendación

módulos de Hello usados para la predicción encima de estos modelos son:

* módulo [Modelo de puntuación][score-model] para la clasificación y regresión
* [Asignar tooClusters] [ assign-to-clusters] módulo de agrupación en clústeres
* [Score Matchbox Recommender][score-matchbox-recommender] para sistemas de recomendación

Este documento explica cómo resultados de predicción toointerpret para cada uno de estos módulos. Para obtener información general de estos módulos, vea [cómo toochoose parámetros toooptimize sus algoritmos de aprendizaje automático de Azure](machine-learning-algorithm-parameters-optimize.md).

Este tema aborda la interpretación de predicción, pero no la evaluación de modelos. Para obtener más información acerca de cómo tooevaluate el modelo, vea [cómo tooevaluate modelo rendimiento aprendizaje automático de Azure](machine-learning-evaluate-model-performance.md).

Si va a tooAzure nuevo aprendizaje automático y necesita ayuda para la creación de un tooget de experimento sencillo iniciado, consulte [crear un experimento sencillo en estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md) en estudio de aprendizaje automático de Azure.

## <a name="classification"></a>Clasificación
Existen dos subcategorías de problemas de clasificación:

* Problemas con solo dos clases (clasificación de dos clases o binaria)
* Problemas con más de dos clases (clasificación multiclase)

Aprendizaje automático de Azure tiene toodeal módulos diferentes a cada uno de estos tipos de clasificación, pero los métodos de Hola para interpretar los resultados de predicción son similares.

### <a name="two-class-classification"></a>Clasificación multiclase
**Experimento de ejemplo**

Un ejemplo de un problema de clasificación de dos clases es la clasificación de Hola de flores iris. tarea Hello es tooclassify flores de iris en función de sus características. conjunto de datos de Iris especificado en aprendizaje automático de Azure Hello es un subconjunto de hello popular [conjunto de datos de Iris](http://en.wikipedia.org/wiki/Iris_flower_data_set) que contiene instancias de solo dos flor especies (clases 0 y 1). Existen cuatro características para cada flor (longitud del sépalo, ancho del sépalo, longitud del pétalo y ancho del pétalo).

![Captura de pantalla del experimento de iris](./media/machine-learning-interpret-model-results/1.png)

Figura 1. Experimento del problema de clasificación de dos clases de iris

Un experimento se ha realizado toosolve este problema, tal como se muestra en la figura 1. Se ha entrenado y puntuado un modelo de árbol de decisión de dos clases. Ahora puede visualizar los resultados de predicción de Hola de hello [puntuar modelo] [ score-model] módulo haciendo clic en el puerto de salida de hello de hello [puntuar modelo] [ score-model]módulo y, a continuación, haga clic en **visualizar**.

![Módulo Puntuar modelo](./media/machine-learning-interpret-model-results/1_1.png)

Se abrirá Hola resultados de puntuación, como se muestra en la figura 2.

![Resultados del experimento de clasificación de dos clases de iris](./media/machine-learning-interpret-model-results/2.png)

Ilustración 2. Visualización del resultado del modelo de puntuación en la clasificación de dos clases

**Interpretación de resultados**

Hay seis columnas en tabla de resultados de Hola. columnas de cuatro izquierdo Hola son características de cuatro Hola. Hola derecha dos columnas, puntuación de etiquetas y las probabilidades con puntuación, son los resultados de predicción de Hola. Hola probabilidades con puntuación columna muestra hello probabilidad que una flor pertenece toohello positivo clase (clase 1). Por ejemplo, Hola primer número de hello columna (0.028571) significa que no existe probabilidad 0.028571 que Hola flor primera pertenece tooClass 1. Hola Hola de muestra de columna de puntuación de etiquetas predecir la clase para cada flor. Esto se basa en la columna de probabilidades con puntuación Hola. Si es mayor que 0.5 Hola con puntuación de probabilidad de una flor, se predice como clase 1. En caso contrario, se prevé que sea la Clase 0.

**Publicación de servicios web**

Tras han entender los resultados de predicción de Hola y considera sonido, hello experimento puede publicarse como un servicio web para que pueda implementar en varias aplicaciones y llamar a las predicciones de clase tooobtain en una flor iris nueva. toolearn cómo toochange entrenamiento experimentar en un experimento de puntuación y publicarlo como un servicio web, consulte [publicar el servicio web de aprendizaje automático de Azure de hello](machine-learning-walkthrough-5-publish-web-service.md). Este procedimiento proporciona un experimento de puntuación, como muestra la figura 3.

![Captura de pantalla del experimento de puntuación](./media/machine-learning-interpret-model-results/3.png)

Figura 3. La puntuación del experimento de problema de clasificación de dos clases de hello iris

Ahora debe tooset Hola entrada y salida para el servicio web de Hola. entrada Hello es puerto de entrada derecho Hola de [puntuar modelo][score-model], que es Hola Iris flor características entrada. Hello elección de salida de hello depende de si está interesado en hello predecir clase (etiqueta con puntuación), Hola con puntuación de probabilidad, o ambos. En este ejemplo, se supone que está interesado en ambas. Hola tooselect deseado columnas de salida, use un [seleccionar las columnas de conjunto de datos] [ select-columns] módulo. Haga clic en [Seleccionar columnas de conjunto de datos][select-columns] y en **Iniciar el selector de columnas**, y seleccione **Etiquetas puntuadas** y **Probabilidades puntuadas**. Después de configurar el puerto de salida de hello de [seleccionar las columnas de conjunto de datos] [ select-columns] y ejecutarlo de nuevo, debe ser experimento de puntuación de hello toopublish listo como un servicio web, haga clic en **publicar WEB SERVICIO**. experimento final Hello es similar a la figura 4.

![experimento de clasificación de dos clases de Hello iris](./media/machine-learning-interpret-model-results/4.png)

Figura 4. Experimento de puntuación final de un problema de clasificación de dos clases de iris

Después de ejecutar el servicio web de Hola y escriba algunos valores de las características de una instancia de prueba, el resultado de hello devuelve dos números. primer número de Hello es Hola puntuado etiqueta, y hello en segundo lugar es hello con puntuación de probabilidad. Se prevé que esta flor sea de Clase 1 con probabilidad de 0,9655.

![Modelo de puntuación de interpretación de prueba](./media/machine-learning-interpret-model-results/4_1.png)

![Resultados de la prueba de puntuación](./media/machine-learning-interpret-model-results/5.png)

Figura 5. Resultado de servicio web de la clasificación de dos clases de iris

### <a name="multi-class-classification"></a>Clasificación multiclase
**Experimento de ejemplo**

En este experimento se llevará a cabo una tarea de reconocimiento de letras como un ejemplo de clasificación multiclase. Hello clasificador intenta toopredict un determinado letra (clase) en función de algunos valores de atributo escrita a mano extraídos de imágenes de hello escrita a mano.

![Ejemplo de reconocimiento de letras](./media/machine-learning-interpret-model-results/5_1.png)

En los datos de entrenamiento hello, hay 16 características extraídos de imágenes de letra escrita a mano. Hola 26 letras forman nuestro 26 clases. La figura 6 se muestra en un experimento entrenará una clasificación multiclase de modelo para reconocimiento de letras y predecir Hola mismo conjunto en un conjunto de datos de prueba de características.

![Experimento de clasificación multiclase de reconocimiento de letras](./media/machine-learning-interpret-model-results/6.png)

Figura 6. Experimento del problema de clasificación multiclase de reconocimiento de letras

Visualizar los resultados de Hola de hello [puntuar modelo] [ score-model] módulo haciendo clic en el puerto de salida de hello de [puntuar modelo] [ score-model] módulo y, a continuación, Haga clic en **visualizar**, debería ver el contenido tal como se muestra en la figura 7.

![Resultados del modelo de puntuación](./media/machine-learning-interpret-model-results/7.png)

Figura 7. Visualización de los resultados del modelo de puntuación en una clasificación multiclase

**Interpretación de resultados**

izquierda 16 columnas de Hello representan valores de las características del conjunto de pruebas de Hola Hola. Hola las columnas con nombres como las probabilidades con puntuación para la clase "XX" son como columna de probabilidades con puntuación hello en caso de dos clases de Hola. Muestran la probabilidad de Hola Hola entrada correspondiente se encuentra dentro de una clase determinada. Por ejemplo, para la primera entrada de hello, hay 0.003571 probabilidad de que sea una "A" 0.000451 probabilidad de que sea una "B" y así sucesivamente. última columna de Hello (puntuado etiquetas) es Hola igual que la puntuación de etiquetas en caso de dos clases de Hola. Selecciona la clase hello con hello mayor puntuado de probabilidad como Hola clase de predicción de entrada correspondiente de Hola. Por ejemplo, para la primera entrada de hello, Hola puntuado etiqueta es "F" porque tiene Hola mayor probabilidad toobe una "F" (0.916995).

**Publicación de servicios web**

También puede obtener Hola puntuado etiqueta para cada probabilidad hello y entrada de hello puntúan etiqueta. lógica básica de Hello es mayor probabilidad de Hola de toofind entre Hola todas las probabilidades de puntuación. toodo, necesita hello toouse [ejecutar Script de R] [ execute-r-script] módulo. Hola código R se muestra en la figura 8 y resultado de hello del experimento de Hola se muestra en la figura 9.

![Ejemplo de código R](./media/machine-learning-interpret-model-results/8.png)

Figura 8. Código de R para extraer hello y puntuación de etiquetas asociadas las probabilidades de las etiquetas de Hola

![Resultado del experimento](./media/machine-learning-interpret-model-results/9.png)

Figura 9. Experimento de puntuación final del problema de clasificación multiclase de reconocimiento de letras de Hola

Después de publicar y ejecutar el servicio web de Hola y escriba algunos valores de las características de entrada, Hola devuelve el resultado parece figura 10. Esta letra escrita a mano, con sus características de 16 extraídos es predicho toobe una "T" con probabilidad 0.9715.

![Módulo de puntuación de interpretación de prueba](./media/machine-learning-interpret-model-results/9_1.png)

![Resultado de la prueba](./media/machine-learning-interpret-model-results/10.png)

Figura 10. Resultado de servicio web de la clasificación multiclase

## <a name="regression"></a>regresión
Los problemas de regresión son diferentes de los problemas de clasificación. En un problema de clasificación, que está tratando de clases de toopredict discreta, como qué clase pertenece una flor iris. Pero, como puede ver en el siguiente ejemplo de un problema de regresión de hello, que está tratando de toopredict una variable continua, como el precio de Hola de un automóvil.

**Experimento de ejemplo**

Use la predicción de precios de automóviles como su ejemplo de regresión. Está tratando de precio de hello toopredict de un automóvil en función de sus características, incluidos la marca, tipo de combustible, tipo de cuerpo y rueda de unidad. el experimento de Hola se muestra en la figura 11.

![Experimento de regresión de precios de automóviles](./media/machine-learning-interpret-model-results/11.png)

Figura 11. Experimento del problema de regresión de precios de automóviles

Hola visualizar [puntuar modelo] [ score-model] módulo, el resultado de hello es similar a la figura 12.

![Resultados de puntuación del problema de predicción de precios de automóviles](./media/machine-learning-interpret-model-results/12.png)

Ilustración 12. La puntuación del resultado para el problema de predicción de precios de automóviles Hola

**Interpretación de resultados**

Las etiquetas con puntuación es la columna de resultado de hello en este resultado de puntuación. Hola números son precios previstos de Hola para cada uno.

**Publicación de servicios web**

Puede publicar el experimento de regresión de hello en un servicio web y llamarlo para la predicción de precios de automóviles en hello igual que en la clasificación de dos clases de hello caso de uso.

![Experimento de puntuación del problema de regresión de precios de automóviles](./media/machine-learning-interpret-model-results/13.png)

Ilustración 13. Experimento de puntuación de un problema de regresión de precios de automóviles

Ejecute servicio web de hello, hello devuelve el resultado parece figura 14. precio de predicción de Hola para este coche es $15,085.52.

![Módulo de puntuación de interpretación de prueba](./media/machine-learning-interpret-model-results/13_1.png)

![Resultados del módulo de puntuación](./media/machine-learning-interpret-model-results/14.png)

Figura 14. Resultado del servicio web de un problema de regresión de precios de automóviles

## <a name="clustering"></a>agrupación en clústeres
**Experimento de ejemplo**

Vamos a usar Hola conjunto de datos de Iris nuevo toobuild un experimento de agrupación en clústeres. Aquí, se puede filtrar las etiquetas de clase de Hola Hola conjunto de datos para que solo tiene características y puede usarse para la agrupación en clústeres. En este iris caso de uso, especifique el número de Hola de toobe clústeres dos durante el proceso de entrenamiento de hello, lo que significa que podría agrupar flores hello en dos clases. el experimento de Hola se muestra en la figura 15.

![Experimento del problema de agrupación en clústeres de iris](./media/machine-learning-interpret-model-results/15.png)

Figura 15. Experimento del problema de agrupación en clústeres de iris

Agrupación en clústeres difiere de la clasificación de ese conjunto de datos de entrenamiento de hello no tienen etiquetas de datos verdaderos por sí mismo. Grupos de agrupación en clústeres Hola instancias de conjunto de datos de entrenamiento en clústeres distintos. Durante el proceso de entrenamiento de hello, las etiquetas de modelo de Hola Hola entradas diferencias de hello entre sus características de aprendizaje. Después de eso, puede utilizarse el modelo entrenado hello toofurther clasificar las entradas futuras. Hay dos partes del resultado de hello que nos interesa dentro de un problema de agrupación en clústeres. primera parte de Hello está etiquetado conjunto de datos de entrenamiento de Hola y Hola en segundo lugar está clasificando un nuevo conjunto de datos con el modelo entrenado Hola.

Hello primera parte del resultado de hello se puede visualizar haciendo clic en hello dejado el puerto de salida del [entrenar el modelo de agrupación en clústeres] [ train-clustering-model] y, a continuación, haga clic en **visualizar**. Visualización de Hola se muestra en la figura 16.

![Resultado de la agrupación en clústeres](./media/machine-learning-interpret-model-results/16.png)

Figura 16. Visualizar el resultado de conjunto de datos de entrenamiento de Hola de agrupación en clústeres

resultado de Hello de la segunda parte hello, agrupación en clústeres nuevas entradas con el modelo de agrupación en clústeres entrenado hello, se muestra en la figura 17.

![Visualización de resultado de agrupación en clústeres](./media/machine-learning-interpret-model-results/17.png)

Figura 17. Visualización de resultado de agrupación en clústeres en un nuevo conjunto de datos

**Interpretación de resultados**

Aunque los resultados de Hola de partes de hello dos derivan de un experimento diferentes fases, parecen Hola mismo y se interpretan en hello igual. Hello cuatro primeras columnas son características. última columna Hello, asignaciones, es resultado de predicción de Hola. Hola Hola de entradas asignadas se ha predicho tantos toobe Hola mismo clúster, es decir, comparten similitudes de alguna manera (este experimento usa métrica de hello predeterminado calcula la distancia Euclidiana). Dado que especifica el número de Hola de clústeres toobe 2, las entradas de hello en las asignaciones se etiquetan 0 ó 1.

**Publicación de servicios web**

Puede publicar Hola experimento de agrupación en clústeres en un servicio web y llamarlo para las predicciones de agrupación en clústeres Hola misma manera que en la clasificación de dos clases de hello caso de uso.

![Experimento de puntuación del problema de agrupación en clústeres de iris](./media/machine-learning-interpret-model-results/18.png)

Figura 18. Experimento de puntuación de un problema de agrupación en clústeres de iris

Después de ejecutar el servicio web de hello, Hola devuelve resultados parece figura 19. Este flor es toobe previsto en el clúster 0.

![Módulo de puntuación de interpretación de prueba](./media/machine-learning-interpret-model-results/18_1.png)

![Resultado del módulo de puntuación](./media/machine-learning-interpret-model-results/19.png)

Figura 19. Resultado de servicio web de la clasificación de dos clases de iris

## <a name="recommender-system"></a>Sistema de recomendación
**Experimento de ejemplo**

Para los sistemas de recomendación, puede usar el problema de recomendación de restaurante de hello como ejemplo: puede recomendar restaurantes para los clientes según su historial de clasificación. datos de entrada de Hello consta de tres partes:

* Valoraciones de restaurantes de los clientes
* Datos de características de los clientes
* Datos de características de restaurantes

Hay varias cosas que podemos hacer con hello [entrenar el Recomendador Matchbox] [ train-matchbox-recommender] módulo aprendizaje automático de Azure:

* predecir las valoraciones para un usuario determinado y un elemento;
* Recomienda tooa de elementos de usuario
* Buscar usuarios tooa relacionados de usuario
* Buscar elementos tooa relacionados dado elemento

Puede elegir qué desea toodo mediante la selección de opciones de hello cuatro Hola **tipo de predicción de Recomendador** menú. De este modo, podrá recorrer los cuatro escenarios.

![Recomendador Matchbox](./media/machine-learning-interpret-model-results/19_1.png)

Un experimento de Azure Machine Learning típico para un sistema de recomendación es similar al de la figura 20. Para obtener información acerca de cómo toouse los módulos del sistema Recomendador, consulte [entrenar el Recomendador matchbox] [ train-matchbox-recommender] y [Recomendador matchbox] [ score-matchbox-recommender].

![Experimento del sistema de recomendación](./media/machine-learning-interpret-model-results/20.png)

Figura 20. Experimento del sistema de recomendación

**Interpretación de resultados**

**Predecir las valoraciones para un usuario determinado y un elemento**

Si selecciona **predicción de clasificación** en **tipo de predicción de Recomendador**, le pregunta Recomendador Hola Hola toopredict de sistema de clasificación para un usuario determinado y un elemento. Hola visualización de hello [Recomendador Matchbox] [ score-matchbox-recommender] salida es similar a la figura 21.

![Resultados del sistema de Recomendador hello: predicción de clasificación de puntuación](./media/machine-learning-interpret-model-results/21.png)

Figura 21. Visualizar el resultado de la puntuación de Hola de sistema de Recomendador hello: predicción de clasificación

Hola dos primeras columnas son pares de usuario-elemento Hola proporcionadas por los datos de entrada de Hola. tercera columna de Hello es Hola clasificación de predicción de un usuario para un elemento determinado. Por ejemplo, en la primera fila de Hola, cliente que U1048 es predecir toorate restaurante 135026 como 2.

**Recomienda tooa de elementos de usuario**

Si selecciona **recomendación de elementos** en **tipo de predicción de Recomendador**, está solicitando el Recomendador Hola sistema toorecommend elementos tooa de usuario. Hola último parámetro toochoose en este escenario es *recomienda la selección de elementos*. Hola opción **de los elementos clasificados (para evaluación de modelos)** es principalmente para la evaluación de modelos durante el proceso de entrenamiento de Hola. Para esta fase de predicción, elegiremos **De todos los elementos**. Hola visualización de hello [Recomendador Matchbox] [ score-matchbox-recommender] salida es similar a la figura 22.

![Resultado de puntuación del sistema de recomendación: recomendación de elementos](./media/machine-learning-interpret-model-results/22.png)

Figura 22. Visualizar el resultado de la puntuación del sistema de Recomendador hello: recomendación de elementos

Hola primero de hello representa Hola seis columnas que tiene elementos de toorecommend de Id. de usuario, proporcionado por los datos de entrada de Hola. Hello otras cinco columnas representan los elementos de hello recomendados usuario toohello en orden descendente de relevancia. Por ejemplo, en la primera fila de hello, hello más recomendable restaurante para cliente U1048 es 134986, seguido por 135018, 134975, 135021 y 132862.

**Buscar usuarios tooa relacionados de usuario**

Si selecciona **usuarios relacionados** en **tipo de predicción de Recomendador**, está solicitando el Recomendador Hola usuario del sistema toofind usuarios relacionados tooa dado. Usuarios relacionados son los usuarios de Hola que tengan preferencias similares. Hola último parámetro toochoose en este escenario es *relacionados con la selección del usuario*. Hola opción **de los usuarios que clasificaron elementos (para evaluación de modelos)** es principalmente para la evaluación de modelos durante el proceso de entrenamiento de Hola. Para esta fase de predicción, elija **De todos los usuarios**. Hola visualización de hello [Recomendador Matchbox] [ score-matchbox-recommender] salida es similar a la figura 23.

![Resultado de puntuación del sistema de recomendación: usuarios relacionados](./media/machine-learning-interpret-model-results/23.png)

Figura 23. Visualizar los resultados de puntuación de sistema de Recomendador Hola--usuarios relacionados

Hola primero de hello de muestra de Hola seis columnas dado toofind de identificadores que necesita de usuario relacionados con los usuarios, proporcionados por los datos de entrada. Hello otro almacén de cinco columnas Hola usuarios relacionados previstos de usuario de hello en orden descendente de relevancia. Por ejemplo, en la primera fila de hello, hello más relevante para el cliente U1048 es cliente U1051, seguido por U1066, U1044, U1017 y U1072.

**Buscar elementos tooa relacionados dado elemento**

Si selecciona **elementos relacionados** en **tipo de predicción de Recomendador**, le pregunta Recomendador hello tooa dado elemento de sistema toofind elementos relacionados. Relacionados con los elementos son Hola elementos probablemente toobe gustó por hello mismo usuario. Hola último parámetro toochoose en este escenario es *relacionados con la selección de elementos*. Hola opción **de los elementos clasificados (para evaluación de modelos)** es principalmente para la evaluación de modelos durante el proceso de entrenamiento de Hola. Para esta fase de predicción, elegiremos **De todos los elementos** . Hola visualización de hello [Recomendador Matchbox] [ score-matchbox-recommender] salida es similar a la figura 24.

![Resultado de puntuación del sistema de recomendación: elementos relacionados](./media/machine-learning-interpret-model-results/24.png)

Figura 24. Visualizar los resultados de puntuación de sistema de Recomendador Hola--elementos relacionados

Hola primero de hello representa Hola seis columnas que tiene los identificadores de elemento que sea necesitados toofind relacionados con los elementos proporcionados por los datos de entrada de Hola. Hello otro almacén de cinco columnas Hola elementos relacionados previstos de elemento de hello en orden descendente en términos de relevancia. Por ejemplo, en la primera fila de hello, elemento más relevante de hello para el elemento 135026 es 135074, seguido por 135035, 132875, 135055 y 134992.

**Publicación de servicios web**

proceso de Hello sobre la publicación de estos experimentos como predicciones de tooget de servicios web es similar para cada uno de los cuatro escenarios de Hola. Aquí se toman segundo escenario de hello (recomendar elementos tooa dado usuario) como un ejemplo. Puede seguir Hola mismo procedimiento con hello otras tres.

Hola guardar entrenado sistema Recomendador como un modelo entrenado y filtrado tooa de datos de entrada de hello columna de Id. de usuario único como solicitado, puede enlazar experimento hello como se muestra en la figura 25 y publicarlo como un servicio web.

![La puntuación del experimento de problema de recomendación de hello restaurante](./media/machine-learning-interpret-model-results/25.png)

Figura 25. La puntuación del experimento de problema de recomendación de hello restaurante

Ejecute servicio web de hello, hello devuelve el resultado parece figura 26. los restaurantes recomendada cinco Hello para el usuario U1048 son 134986, 135018, 134975, 135021 y 132862.

![Ejemplo de servicio del sistema de recomendación](./media/machine-learning-interpret-model-results/25_1.png)

![Resultados del experimento de ejemplo](./media/machine-learning-interpret-model-results/26.png)

Figura 26. Resultado de servicio web del problema de recomendación de restaurante

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
