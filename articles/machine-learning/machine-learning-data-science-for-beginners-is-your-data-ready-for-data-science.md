---
title: "¿aaaIs los datos que está listo para la ciencia de datos? Evaluación de datos: Azure Machine Learning | Microsoft Docs"
description: "Obtenga información acerca de los criterios de hello 4 para toobe de datos lista para la ciencia de datos. Ciencia de datos para principiantes vídeo 2 tiene toohelp ejemplos concretos con evaluación de datos básicos."
keywords: datos pertinentes, evaluar los datos, preparar datos, criterios de datos, datos preparados
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a>¿Están sus datos preparados para la ciencia de datos?
## <a name="video-2-data-science-for-beginners-series"></a>Vídeo 2: serie Ciencia de datos para principiantes
Obtenga información acerca de cómo tooevaluate su toomake de datos que cumple los criterios básicos toobe listo para la ciencia de datos.

Hola tooget máximo partido de la serie de hello, ver todas ellas. [Vaya toohello lista de vídeos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a>Otros vídeos de la serie
*Ciencia de datos para principiantes* es una ciencia de toodata introducción rápida en cinco vídeos breves.

* Vídeo 1: [Hola 5 preguntas respuestas de ciencia de datos](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min s 14)*
* Vídeo 2: ¿Están sus datos preparados para la ciencia de datos?
* Vídeo 3: [Realización de preguntas que pueden responderse con datos](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 minutos y 17 segundos)*
* Vídeo 4: [Predicción de respuestas con un modelo sencillo](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 minutos y 42 segundos)*
* Vídeo 5: [copiar ciencia de datos de otras personas trabajo toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 18 min.)*

## <a name="transcript-is-your-data-ready-for-data-science"></a>Transcripción: ¿Están sus datos preparados para la ciencia de datos?
Éste es demasiado "es los datos listo para la ciencia de datos?" Hola segundo vídeo en serie de hello *ciencia de datos para principiantes*.  

Antes de ciencia de datos puede permitir Hola respuestas que desee, tendrá que toogive algunos toowork materias primas de alta calidad con. Al igual que realizar una pizza, ingredientes Hola de hello mejor empezar con, Hola mejor producto final Hola. 

## <a name="criteria-for-data"></a>Criterios para los datos
Por lo tanto, en caso de hello de ciencia de datos, hay algunas características que necesitamos toopull juntos.

Necesitamos datos que sean:

* Pertinentes
* Conectado
* Precisos
* Suficiente toowork con

## <a name="is-your-data-relevant"></a>¿Son sus datos pertinentes?
Por lo que ingredientes primera hello - necesitamos datos relevantes.

![Datos pertinentes frente a datos no pertinentes: evaluar los datos](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

Mire tabla Hola Hola izquierda. Se cumpla con siete personas fuera de barras de Boston, mide su nivel de alcohol de sangre, el promedio de bateo de Red Sox hello en su última partida y el precio de Hola de leche en hello más cercano de almacén de comodidad.

Todos ellos son datos perfectamente legítimos. El único problema es que no son pertinentes. No hay ninguna relación obvia entre estos números. Si le asignó Hola precio actual de promedio de bateo Red Sox hello y leche, no hay ninguna manera podría adivinar el contenido de alcohol de sangre.

Ahora mire tabla hello en hello derecho. Este tiempo se mide el número de hello masivo y recuento de cuerpo de cada persona de bebidas que han tenido.  números de Hello en cada fila ahora son relevante tooeach otro. Si le asignó el número de hello y masa de cuerpo de Margaritas tengo desde, que podría realizar una estimación en mi sangre alcohol contenido.

## <a name="do-you-have-connected-data"></a>¿Tiene datos conectados?
ingredientes siguiente Hello son datos conectados.

![Datos conectados frente a datos desconectados: criterios de datos y datos preparados](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

Presentamos algunos datos relevantes en calidad de Hola de hamburguesas: rejilla temperatura, peso patty y la clasificación en la revista de alimentos Hola local. Pero observe vacíos de hello en la tabla de Hola Hola izquierda.

A la mayoría de los conjuntos de datos les faltan algunos valores. Es común agujeros toohave similar al siguiente y hay formas toowork alrededor de ellos. Pero si hay demasiados falta, los datos comienzan toolook como cheese suizo.

Si observa tabla Hola Hola izquierda, hay por lo que la cantidad de datos que faltan, resulta difícil toocome seguridad con cualquier tipo de relación entre rejilla temperatura y patty peso. Este es un ejemplo de datos desconectados.

tabla Hola Hola directamente, sin embargo, está lleno y - un ejemplo completo de datos conectados.

## <a name="is-your-data-accurate"></a>¿Son precisos los datos?
Hola siguiente ingredientes que necesitamos es precisión. Estos son los cuatro destinos que nos gustaría toohit con flechas.

![Datos precisos frente a datos imprecisos: criterios de datos](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

Mire el destino de hello en la esquina superior derecha de Hola. Tenemos una agrupación estrecha derecha alrededor de hello bullseye. Esto, por supuesto, es preciso. Curiosamente, en lenguaje de Hola de ciencia de datos, nuestro rendimiento derecha de destino de Hola por debajo de él también se considera precisa.

Si se encontraba toomap centro de Hola de estas flechas, vería que es muy próxima toohello bullseye. flechas de Hola se reparten todo destino hello, por lo que se consideran imprecisas, pero están centrados en hello bullseye, por lo que se consideran precisos.

Ahora examinemos destino de hello superior izquierda. Aquí nuestras flechas dieron todas muy cerca, en una agrupación apretada. Sean más precisos, pero son inexactos porque center Hola forma desactivar bullseye Hola. Y, por supuesto, flechas de hello en el destino de la parte inferior izquierda de hello están correcta e imprecisas. Este arquero necesita más práctica.

## <a name="do-you-have-enough-data-toowork-with"></a>¿Tiene suficiente toowork datos con?
Por último, ingredientes #4 - necesitamos toohave suficientes datos.

![¿Tiene suficientes datos para el análisis? Evaluación de datos](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

Piense que cada punto de datos de la tabla es una pincelada en una pintura. Si tiene sólo algunas de ellas, pintura Hola puede ser bastante aproximada: es tootell disco duro lo es.

Si agrega algunos trazos de pincel más, la pintura inicia tooget un poco más de enfocada.

Cuando haya apenas suficiente trazos, puede ver solo suficiente toomake algunas decisiones amplios. ¿Es otra parte que podría ser conveniente toovisit? Parece soleado y con agua limpia; sí, ahí es a donde voy a ir de vacaciones.

Si agrega más datos, imagen Hola pasa a ser más clara y puede tomar decisiones más detalladas. Ahora puedo buscar en hello tres hoteles en bank izquierdo Hola. Sabe, realmente como unas características arquitectónicas de hello en primer plano de Hola Hola. Deberá permanecer allí, en suelo tercer Hola.

Con los datos que son pertinente, conectado, precisión, y suficiente, tenemos que todos los ingredientes Hola necesitamos toodo algunos ciencia de datos de alta calidad.

Ser seguro toocheck out Hola otros cuatro vídeos en *ciencia de datos para principiantes* de aprendizaje automático de Microsoft Azure.

## <a name="next-steps"></a>Pasos siguientes
* [Prueba de su primer experimento de ciencia de datos con Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtener una introducción tooMachine aprendizaje en Microsoft Azure](machine-learning-what-is-machine-learning.md)
