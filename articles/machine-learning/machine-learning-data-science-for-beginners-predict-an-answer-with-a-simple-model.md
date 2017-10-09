---
title: "aaaPredict una respuesta con un modelo de regresión simple - aprendizaje automático de Azure | Documentos de Microsoft"
description: "¿Cómo toocreate una regresión simple modelo toopredict un precio de ciencia de datos para principiantes vídeo 4. Incluye una regresión lineal con los datos de destino."
keywords: "crear un modelo, modelo simple, predicción del precio, modelo de regresión simple"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>Predicción de respuestas con un modelo sencillo
## <a name="video-4-data-science-for-beginners-series"></a>Vídeo 4: serie Ciencia de datos para principiantes
Obtenga información acerca de cómo toocreate un toopredict del modelo de regresión simple Hola precio de un rombo de ciencia de datos para principiantes vídeo 4. Dibujaremos un modelo de regresión con los datos de destino.

Hola tooget máximo partido de la serie de hello, ver todas ellas. [Vaya toohello lista de vídeos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>Otros vídeos de la serie
*Ciencia de datos para principiantes* es una ciencia de toodata introducción rápida en cinco vídeos breves.

* Vídeo 1: [Hola 5 preguntas respuestas de ciencia de datos](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min s 14)*
* Vídeo 2: [¿Están sus datos preparados para la ciencia de datos?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 minutos y 56 segundos)*
* Vídeo 3: [Realización de preguntas que pueden responderse con datos](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 minutos y 17 segundos)*
* Vídeo 4: Predicción de respuestas con un modelo sencillo
* Vídeo 5: [copiar ciencia de datos de otras personas trabajo toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 18 min.)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>Transcripción: Predicción de respuestas con un modelo sencillo
Bienvenido toohello cuarto vídeo Hola serie "Ciencia de datos para principiantes". En este caso, crearemos un modelo simple y realizaremos una predicción.

Un *modelo* es un caso simplificado sobre nuestros datos. Le mostraré lo que quiero decir.

## <a name="collect-relevant-accurate-connected-enough-data"></a>Recopilación de datos pertinentes, precisos, conectados y suficientes
Digamos que deseo tooshop para un rombo. Tengo un anillo que pertenecía toomy abuela con una configuración para un rombo de acento circunflejo 1,35 y deseo tooget una idea de cuánto costará. Puedo tomar un lápiz y el Bloc de notas en almacén de joyas hello y anotar precio de Hola de todos los de diamantes hello en caso de hello y cuánto pesan en número de quilates. A partir de hello rombo - su 1.01 número de quilates y $7,366.

Ahora contemplar y hacerlo para hello todos los otros diamantes en almacén Hola.

![Columnas de datos de los diamantes](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

Observe que nuestra lista tiene dos columnas. Cada columna tiene un atributo diferente, quilates y precio, y cada fila es un único punto de datos que representa un solo diamante.

En realidad, hemos creado un pequeño conjunto de datos aquí: una tabla. Observe que cumple los criterios de calidad:

* Hola datos **relevante** -peso es tooprice definitivamente relacionado
* Tiene **precisa** -hemos comprobado precios Hola que escribimos hacia abajo
* Están **conectados** : no hay ningún espacio en blanco en ninguna de estas columnas.
* Y, como veremos, tiene **suficiente** datos tooanswer nuestra pregunta

## <a name="ask-a-sharp-question"></a>Formulación de una pregunta directa
Ahora se le presentan nuestra pregunta de manera aguda: "cuánto va a costar toobuy un rombo de acento circunflejo 1,35?"

Nuestra lista no tiene un rombo de acento circunflejo 1,35 en él, por lo que tendremos rest de hello toouse de nuestro tooget de datos una pregunta de toohello de respuesta.

## <a name="plot-hello-existing-data"></a>Trazar datos existentes de Hola
Hola primera cosa que haremos es dibujar una línea horizontal de número, llamada a un eje, pesos de hello toochart. intervalo de Hola de pesos de hello es too2 0, por lo que se podrá dibujar una línea que incluya que intervalo y colocar marcas de paso para cada acento circunflejo mitad.

A continuación se dibuja un precio de hello toorecord de eje vertical y conectarlo eje horizontal de peso de toohello. Utilizaremos unidades en dólares. Ahora tenemos un conjunto de ejes de coordenadas.

![Ejes de peso y precio](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

Se está tootake continuo estos datos y convertirla en una *gráfico de dispersión*. Se trata de un conjuntos de datos numéricos de manera estupenda toovisualize.

Para el primer punto de datos hello, hemos ver completa una línea vertical en el número de quilates 1.01. A continuación, dibujamos mentalmente una línea horizontal en 7366 USD. Donde se encuentran, dibujamos un punto. Esto representa nuestro primer diamante.

Ahora se vaya a través de cada forma de rombo en esta lista y Hola lo mismo. Cuando hayamos terminado, esto es lo que obtenemos: una serie de puntos, uno para cada diamante.

![gráfico de dispersión](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Modelo de Hola de dibujo a través de puntos de datos de Hola
Ahora si observa squint y puntos de hello, colección de hello parece una línea fat, aproximada. Podemos tomar nuestro marcador y dibujar una línea recta a través de ellos.

Al dibujar una línea, hemos creado un *modelo*. Pensar en esto como tomar Hola mundo real y hacer una versión de dibujos animados simplista del mismo. Ahora dibujos animados hello es incorrecto: línea hello no vaya a través de todos los puntos de datos de Hola. Pero es una simplificación útil.

![Línea de regresión lineal](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

hecho de Hola que todos los puntos de hello no recorren exactamente línea hello es correcto. Los científicos de datos explican diciendo que hay Hola modelo - línea hello - y, a continuación, cada punto tiene algunas *ruido* o *varianza* asociados a él. Hay Hola subyacente perfecta relación y, a continuación, hay Hola esencia vida real que agrega ruido e incertidumbre.

Dado que estamos intentando pregunta de hello tooanswer *cuánto?* Esto se denomina una *regresión*. Y puesto que estamos usando una línea recta, es una *regresión lineal*.

## <a name="use-hello-model-toofind-hello-answer"></a>Usar la respuesta de hello modelo toofind Hola
Ahora ya tenemos un modelo y le planteamos nuestra pregunta: ¿cuánto costará un diamante de 1,35 quilates?

tooanswer nuestra pregunta, hemos ver completa número de quilates 1,35 y dibujar una línea vertical. Donde cruce línea hello del modelo, se ver completa un eje de dólar toohello línea horizontal. Se encuentra justo en 10 000. ¡Bum! Respuesta de hello es: un rombo de acento circunflejo 1,35 cuesta aproximadamente 10.000 $.

![Encontrar la respuesta de hello en el modelo de Hola](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>Creación de un intervalo de confianza
Es natural toowonder cómo precisa esta predicción es. Resulta útil tooknow si rombo de acento circunflejo 1,35 Hola será muy próxima demasiado 10.000$ o mucho mayor o menor. toofigure este, vamos a dibujar una envoltura alrededor de la línea de regresión de Hola que incluye la mayoría de los puntos de Hola. Se llama a este sobre nuestro *intervalo de confianza*: estamos bastante seguros de que los precios pertenecen a este sobre de tipo, porque Hola anteriores tiene la mayoría de ellos. Podemos dibujar dos líneas horizontales más desde donde cruza con línea de acento circunflejo 1,35 Hola Hola inferior y superior Hola de dicho sobre.

![intervalo de confianza](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

Ahora podemos decir algo sobre el intervalo de confianza: que podamos poner confiable que precio de Hola de una forma de rombo acento circunflejo 1,35 es aproximadamente $10.000 - pero podría ser tan bajo como $8.000 y podría ser tan alto como 12.000 USD.

## <a name="were-done-with-no-math-or-computers"></a>Hemos terminado, sin matemáticas ni equipos informáticos.
Hicimos los científicos de datos recibir los pagos toodo e hicimos simplemente dibujando:

* Hemos planteado una pregunta a la que hemos podido responder con datos.
* Hemos creado un *modelo* mediante la *regresión lineal*.
* Hemos realizado una *predicción* y la hemos completado con un *intervalo de confianza*.

No usamos toodo matemáticas o equipos.

Ahora bien, si hubiéramos tenido más información, como...

* Hola corta de rombo Hola
* variaciones de color (cómo cerrar rombo hello es toobeing blanco)
* número de Hola de inclusiones en forma de rombo Hola

...habríamos tenido más columnas. En ese caso, las matemáticas hubieran sido útiles. Si tiene más de dos columnas, resulta puntos de disco duro toodraw en papel. matemáticas de Hello le permite ajustar esa línea o plano tooyour datos muy bien.

Además, si en lugar de un puñado de diamantes, tuviéramos dos mil o dos millones, podría hacer ese trabajo de forma mucho más rápida con un equipo informático.

En la actualidad, que hemos hablado cómo toodo la regresión lineal y se realiza una predicción usando datos.

Ser seguro toocheck out Hola otros vídeos en "Datos ciencia para principiantes" de aprendizaje automático de Microsoft Azure.

## <a name="next-steps"></a>Pasos siguientes
* [Prueba de su primer experimento de ciencia de datos con Machine Learning Studio](machine-learning-create-experiment.md)
* [Obtener una introducción tooMachine aprendizaje en Microsoft Azure](machine-learning-what-is-machine-learning.md)
