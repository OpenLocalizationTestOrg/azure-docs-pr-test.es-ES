---
title: "aaaAsk pueden responder a los datos de una pregunta - problemas de ciencia de datos: aprendizaje automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooformulate una ciencia de datos agudo pregunta de ciencia de datos para principiantes de vídeo 3. Incluye una comparación de preguntas de clasificación y regresión."
keywords: "problemas de ciencia de datos,preguntas de ciencias de datos,formular pregunta,preguntas de regresión,preguntas de clasificación,pregunta directa"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Realización de preguntas que pueden responderse con datos
## <a name="video-3-data-science-for-beginners-series"></a>Vídeo 3: Ciencia de datos para principiantes
Obtenga información acerca de cómo tooformulate un problema de ciencia de datos en una pregunta en la ciencia de datos para principiantes vídeo 3. Este vídeo incluye una comparación de preguntas para algoritmos de clasificación y regresión.

Hola tooget máximo partido de la serie de hello, ver todas ellas. [Vaya toohello lista de vídeos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Otros vídeos de la serie
*Ciencia de datos para principiantes* es una ciencia de toodata introducción rápida en cinco vídeos breves.

* Vídeo 1: [Hola 5 preguntas respuestas de ciencia de datos](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min s 14)*
* Vídeo 2: [¿Están sus datos preparados para la ciencia de datos?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 minutos y 56 segundos)*
* Vídeo 3: Realización de preguntas que pueden responderse con datos
* Vídeo 4: [Predicción de respuestas con un modelo sencillo](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 minutos y 42 segundos)*
* Vídeo 5: [copiar ciencia de datos de otras personas trabajo toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 18 min.)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>Transcripción: Realización de preguntas que pueden responderse con datos
Página principal toohello tercer vídeo en serie de Hola "Ciencia de datos para principiantes".  

En este vídeo, recibirá algunas sugerencias para formular una pregunta que se pueda responder con datos.

Podría aprovecha al máximo este vídeo, si observa primero dos vídeos anteriores Hola de esta serie: "ciencia de datos de hello 5 preguntas puede responder" y "Son los datos están listos para la ciencia de datos?"

## <a name="ask-a-sharp-question"></a>Formulación de una pregunta directa
Hemos hablado de la ciencia de datos es proceso Hola del uso de nombres (también denominados categorías o etiquetas) y números toopredict una pregunta de tooa de respuesta. Pero no puede ser cualquier pregunta; tiene toobe un *agudo pregunta.*

Una pregunta imprecisa no tiene toobe respondido con un nombre o un número. Una pregunta directa sí.

Imagine que encuentra una lámpara mágica con un genio que responde de forma veraz a cualquier pregunta que formule. Pero es un genie perjudiciales, e intentaremos toomake su respuesta como vaga y poco confuso como que pueda empezar inmediatamente. Desea toopin le hacia abajo junto a una pregunta tan hermética que no se puede ayudar a pero saber lo que desea tooknow.

Si estaba tooask una pregunta imprecisa, como "Lo que está ocurriendo toohappen con mi existencias?", puede responder genie hello, "cambiará el precio de Hola". Es una respuesta veraz, pero no sirve de mucha ayuda.

Pero si tuviera tooask una pregunta aguda, como "¿qué precio de venta de la mi acción será semanas siguientes?", hello genie no puede ayudar a pero proporcionarle un determinado responda y predecir un precio de venta.

## <a name="examples-of-your-answer-target-data"></a>Ejemplos de respuesta: datos de destino
Una vez que formular su pregunta, compruebe toosee tanto si tienen algunos ejemplos de respuesta de hello en los datos.

Si la pregunta es "¿A qué precio de venta estarán mis acciones la semana próxima?", a continuación, tenemos toomake seguro de que nuestros datos incluyen el historial de precios de cotización de Hola.

Si la pregunta es "qué automóvil en mi flota es continuo toofail primero?" a continuación, tenemos toomake seguro de que nuestros datos incluyen información acerca de los errores anteriores.

![Datos de destino: ejemplos de la respuesta. Formular una pregunta de ciencia de datos.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Estos ejemplos de respuestas se denominan destino. Un destino es lo que se está intentando toopredict acerca de los puntos de datos en el futuro, ya sea una categoría o un número.

Si no tiene los datos de destino, necesitará algunas tooget. No será capaz de tooanswer su pregunta sin él.

## <a name="reformulate-your-question"></a>Reformulación de la pregunta
En ocasiones, puede cambiar el texto de su tooget pregunta una respuesta más útil.

Hola pregunta "es este punto de datos A o B?" predice la categoría de hello (o nombre o etiqueta) de algo. tooanswer, usamos un *algoritmo de clasificación*.

Hola pregunta "¿cuánto?" o "¿Cuántos?" predice una cantidad. tooanswer utilizamos una *algoritmo de regresión*.

toosee cómo se pueden transformar estos elementos, echemos un vistazo a pregunta de hello, "¿qué noticia es lector toothis más interesante de hello?" Se pregunta por una predicción de una sola opción entre muchas posibilidades, es decir: ¿Es A, B, C o D?, y se usaría un algoritmo de clasificación.

Pero esta pregunta puede ser más fácil tooanswer si cambiar el texto como "lo interesante es cada caso en este sistema de lectura de lista toothis?" Ahora puede asignar a cada artículo una puntuación numérica y, a continuación, es fácil tooidentify Hola puntuación más alta artículo. ¿Se trata de un Rehacer de la pregunta de clasificación de hello en una pregunta de regresión o cuánto?

![Reformular la pregunta. Pregunta de clasificación frente a pregunta de regresión.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

¿Cómo pide que una pregunta es un algoritmo de toowhich pista puede proporcionar una respuesta.

Encontrará que ciertas familias de algoritmos - como Hola que en nuestro ejemplo de caso de noticias - están estrechamente relacionados. Error puede volver a formular en el algoritmo de Hola de toouse pregunta que le ofrece Hola respuesta más útil.

Pero, más importante aún, hacer esa pregunta aguda - pregunta Hola que puede solucionar con datos. Y compruebe que hay tooanswer de datos adecuado de Hola.

Hemos hablado de algunos principios básicos para formular una pregunta que se pueda responder con datos.

Ser seguro toocheck out Hola otros vídeos en "Datos ciencia para principiantes" de aprendizaje automático de Microsoft Azure.

## <a name="next-steps"></a>Pasos siguientes
* [Prueba de su primer experimento de ciencia de datos con Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtener una introducción tooMachine aprendizaje en Microsoft Azure](machine-learning-what-is-machine-learning.md)
