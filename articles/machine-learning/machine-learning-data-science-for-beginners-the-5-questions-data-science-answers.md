---
title: "ciencia de datos de aaaThe 5 preguntas de aprendizaje automático de Azure - ciencia de datos para principiantes - | Documentos de Microsoft"
description: "Ciencia de datos para principiantes es explica los conceptos básicos de 5 breves vídeos, a partir de respuestas de ciencia de datos de hello 5 preguntas. De Azure Machine Learning."
keywords: "realizar ciencia de datos,ciencia de datos para principiantes,aspectos básicos de ciencia de datos,preguntas de ciencia de datos,vídeo de ciencia de datos, introducción a la ciencia de datos"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a01f93ee-01eb-4afe-abbd-cfa035c119b0
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 6de0ca22556771a3044520d9ccc6771c3de78771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-for-beginners-video-1-hello-5-questions-data-science-answers"></a>Ciencia de datos para principiantes 1 vídeo: Hola 5 preguntas respuestas de ciencia de datos
Obtener una ciencia toodata de introducción rápida de *ciencia de datos para principiantes* en cinco vídeos breves de científico de datos principales. Estos vídeos son básicos pero útiles si está interesado en realizar ciencia de datos o trabajar con científicos de datos.

Este primer vídeo es sobre tipos de Hola de preguntas que puede responder la ciencia de datos. Hola tooget máximo partido de la serie de hello, ver todas ellas. [Vaya toohello lista de vídeos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/8/player]
>
>

## <a name="other-videos-in-this-series"></a>Otros vídeos de la serie
*Ciencia de datos para principiantes* es una ciencia toodata de introducción rápida tarda aproximadamente 25 minutos en total. Consulte los cinco vídeos:

* Vídeo 1: Hola 5 preguntas respuestas de ciencia de datos
* Vídeo 2: [¿Están sus datos preparados para la ciencia de datos?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 minutos y 56 segundos)*
* Vídeo 3: [Realización de preguntas que pueden responderse con datos](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 minutos y 17 segundos)*
* Vídeo 4: [Predicción de respuestas con un modelo sencillo](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 minutos y 42 segundos)*
* Vídeo 5: [copiar ciencia de datos de otras personas trabajo toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 18 min.)*

## <a name="transcript-hello-5-questions-data-science-answers"></a>Transcripción: Hola 5 preguntas respuestas de ciencia de datos
¡Hola! Esta es la serie de vídeos de toohello *ciencia de datos para principiantes*.

Ciencia de datos puede ser algo intimidante, por lo que presentaremos Fundamentos de hello aquí sin necesidad de ecuaciones o equipo jerga de programación.

En este primer vídeo, hablaremos sobre "respuestas de ciencia de datos para 5 preguntas de hello."

Ciencia de datos utiliza números y responde a nombres (también conocido como categorías o etiquetas) toopredict tooquestions.

Puede sorprenderle, pero *solo hay cinco preguntas a las que responde la ciencia de datos*:

* ¿Esto es A o B?
* ¿Es extraño?
* ¿Cuánto? o ¿cuántos?
* ¿Cómo está organizado?
* ¿Qué debo hacer a continuación?

Cada una de estas preguntas se responde mediante una familia de métodos de aprendizaje automático independientes, denominados algoritmos.

Resulta útil toothink sobre un algoritmo como una receta y los datos como ingredientes Hola. Un algoritmo indica cómo toocombine y combinación Hola datos en orden tooget una respuesta. Los equipos son similares a una batidora. Lo hacen la mayoría de esfuerzo de hello del algoritmo de hello automáticamente y lo hacen bastante rápido.

## <a name="question-1-is-this-a-or-b-uses-classification-algorithms"></a>Pregunta 1: ¿esto es A o B? utiliza algoritmos de clasificación
¿Comenzaremos con la pregunta de hello: es este A o B?

![Algoritmos de clasificación: ¿esto es A o B?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/classification-algorithms.png)

Esta familia de algoritmos se llama clasificación de dos clases.

Es útil para cualquier pregunta que solo tenga dos respuestas posibles.

Por ejemplo:

* ¿Este tire producirá un error en hello siguientes 1.000 millas: Yes o no?
* Qué aporta más clientes ¿un cupón de 5 USD o un descuento del 25 %?

¿Esta cuestión también se pueden volver a escribir tooinclude más de dos opciones: es este A o B o C o D, etcetera.?  Esto se denomina clasificación multiclase y es útil cuando hay varias respuestas (o varios miles de respuestas) posibles. Clasificación multiclase elige hello más probable.

## <a name="question-2-is-this-weird-uses-anomaly-detection-algorithms"></a>Pregunta 2: ¿es extraño? utiliza algoritmos de detección de anomalías
¿Hola siguiente pregunta puede responder la ciencia de datos es: es este extraño? Esta pregunta se responde mediante una familia de algoritmos denominada detección de anomalías.

![Algoritmos de detección de anomalías: ¿es extraño?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/anomaly-detection-algorithms.png)

Si tiene una tarjeta de crédito, ya se habrá beneficiado de la detección de anomalías. La compañía de tarjeta de crédito analiza los patrones de compra, por lo que puede avisar toopossible fraude. Cargos "extraños" podrían ser una compra en una tienda donde normalmente no compra o comprar un artículo inusualmente caro.

Esta pregunta puede ser útil de muchas formas. Por ejemplo:

* ¿Si tiene un automóvil con presión de medidores, puede ser conveniente tooknow: es este medidor de presión de lectura normal?
* ¿Si se está supervisando Hola internet, desearía tooknow: este mensaje de Hola típico de internet?

La detección de anomalías marca eventos o comportamientos inesperados o poco habituales. Proporciona pistas donde toolook de problemas.

## <a name="question-3-how-much-or-how-many-uses-regression-algorithms"></a>Pregunta 3: ¿cuánto? o ¿cuántos? utiliza algoritmos de regresión
¿Aprendizaje automático puede predecir Hola respuesta tooHow mucho? ¿o cómo muchas? familia de algoritmos de Hola que responda a esta pregunta se denomina regresión.

![Algoritmos de regresión: ¿Cuánto? o ¿Cuántos?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/regression-algorithms.png)

Los algoritmos de regresión realizan predicciones numéricas, como:

* ¿Qué Hola temperatura puede martes siguiente?  
* ¿Cuáles serán las ventas del cuarto trimestre?

Ayudan a responder cualquier pregunta que pueda solicitar un número.

## <a name="question-4-how-is-this-organized-uses-clustering-algorithms"></a>Pregunta 4: ¿cómo está organizado? utiliza algoritmos de clústeres
Ahora dos últimas preguntas Hola son un poco más avanzado.

A veces desea toounderstand Hola estructura de un conjunto de datos, cómo se organiza? Para esta pregunta, no hay ejemplos para los que ya conozca resultados.

Hay muchas maneras tootease estructura Hola de datos. Un enfoque son los clústeres. Separa los datos en "grupos" naturales para interpretarlos más fácilmente. Con los clústeres no hay una respuesta correcta.

![Algoritmos de clústeres ¿Cómo está organizado?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/clustering-algorithms.png)

Algunos ejemplos comunes de preguntas con agrupación en clústeres son:

* ¿Los visores como Hola mismo tipos de películas?
* ¿Hola producirá un error en los modelos de impresora igual?

Al comprender cómo se organizan los datos, puede comprender y predecir mejor eventos y comportamientos.  

## <a name="question-5-what-should-i-do-now-uses-reinforcement-learning-algorithms"></a>Pregunta 5: ¿qué debo hacer ahora? utiliza algoritmos de aprendizaje reforzado
Hola última pregunta: ¿qué debo hacer ahora? utiliza una familia de algoritmos llamados aprendizaje reforzado.

Aprendizaje de refuerzo está inspirado por cómo cerebro de Hola de ratas y a las personas responde toopunishment y recompensas. Estos algoritmos aprender de resultados y decidir sobre la acción siguiente Hola.

Por lo general, aprendizaje de refuerzo es una buena elección para los sistemas automatizados que contienen muchas pequeñas decisiones sin instrucciones humano toomake.

![Algoritmos de aprendizaje reforzado ¿Qué debo hacer a continuación?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/reinforcement-learning-algorithms.png)

Las preguntas a las que responde son siempre sobre la acción que debe llevar a cabo una máquina o un robot (normalmente). Algunos ejemplos son:

* ¿Si soy un sistema de control de temperatura de una casa: ajustar la temperatura de Hola o dejarla donde resulta?  
* Si soy un automóvil sin conductor: ante un semáforo en ámbar ¿freno o acelero?  
* ¿Para un vacío de robot: mantener Vacuumer, "o" volver toohello estación de carga?

Los algoritmos de aprendizaje reforzado recopilan datos a medida que avanzan, aprendiendo mediante prueba y error.

Por lo que eso es todo - puede responder a ciencia de datos de hello 5 preguntas.

## <a name="next-steps"></a>Pasos siguientes
* [Prueba de su primer experimento de ciencia de datos con Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtener una introducción tooMachine aprendizaje en Microsoft Azure](machine-learning-what-is-machine-learning.md)
