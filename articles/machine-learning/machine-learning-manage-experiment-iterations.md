---
title: "aaaManage experimentar iteraciones en estudio de aprendizaje automático | Documentos de Microsoft"
description: "¿Cómo toomanage experimentar iteraciones en estudio de aprendizaje automático de Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Administrar iteraciones de experimentos en Estudio de aprendizaje automático de Azure
Desarrollar un modelo de análisis predictivo es un proceso iterativo - mientras modificas hello diversas funciones y parámetros de su experimento, los resultados convergen hasta que esté satisfecho que tienen un modelo entrenado y eficaz. Proceso de toothis de clave es varias iteraciones de los parámetros de experimento y las configuraciones de hello de seguimiento.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Puede revisar las ejecuciones anteriores de sus experimentos en cualquier momento en orden toochallenge, volver a visitar y en última instancia confirmar o refinar suposiciones anteriores. Cuando se ejecuta un experimento, estudio de aprendizaje automático mantiene un historial de hello ejecutar, incluido el conjunto de datos, módulo, las conexiones de puerto y parámetros. Este historial también captura los resultados, información de tiempo de ejecución (como el inicio y las detenciones), los mensajes de registro y el estado de ejecución. Se puede volver atrás en cualquiera de estas ejecuciones en cualquier orden cronológico Hola de tooreview de tiempo de su experimento y los resultados intermedios. Incluso puede usar una ejecución anterior de su toolaunch experimento en una nueva fase de consulta y la detección en su ruta de acceso toocreating simple, complejo o incluso "conjunto" soluciones de modelado.

> [!NOTE]
> Cuando ve una ejecución anterior de un experimento, esa versión del experimento de hello está bloqueada y no se puede editar. Sin embargo, puede guardar una copia del mismo haciendo clic en **SAVE AS** y proporcionar un nombre nuevo para la copia de Hola. Estudio de aprendizaje automático abre copia nueva de hello, que, a continuación, puede editar y ejecutar. Esta copia de su experimento está disponible en hello **EXPERIMENTOS** lista junto con todos sus experimentos.
> 
> 

## <a name="viewing-hello-prior-run"></a>Hola de visualización ejecutar anterior
Una vez que se han ejecutado al menos una vez abierto experimento, puede ver Hola anterior ejecución del experimento de hello haciendo clic en **antes de ejecutar** en el panel de propiedades de Hola.

Por ejemplo, suponga que crea un experimento y ejecuta versiones de este a las 11:23, 11:42 y 11:55. Si abre la última ejecución de hello del experimento de hello (11:55) y haga clic en **antes de ejecutar**, se abre la versión de Hola ejecutados a las 11:42.

## <a name="viewing-hello-run-history"></a>Hola Ver historial de ejecución
Puede ver todas las ejecuciones anteriores de Hola de un experimento, haga clic en **ver el historial de ejecución** en un experimento abierto.

Por ejemplo, suponga que crea un experimento con hello [regresión lineal] [ linear-regression] módulo y desea tooobserve efecto de Hola de cambiar el valor de Hola de **velocidad de aprendizaje** en los resultados del experimento. Se ejecuta Hola experimento varias veces con distintos valores para este parámetro, como se indica a continuación:

| Valor de velocidad de aprendizaje | Hora de inicio de la ejecución |
| --- | --- |
| 0,1 |9/11/2014 4:18:58 PM |
| 0,2 |9/11/2014 4:24:33 PM |
| 0,4 |9/11/2014 4:28:36 PM |
| 0,5 |9/11/2014 4:33:31 PM |

Si hace clic en **VER HISTORIAL DE EJECUCIONES**, verá una lista de todas estas ejecuciones:

![Historial de ejecución de ejemplo][runhistory]

Haga clic en cualquiera de estos tooview se ejecuta una instantánea de hello experimentar en tiempo de Hola que la ejecutó. Hello valores de parámetro, de la configuración, los comentarios y los resultados son toogive conserva todos los que un registro completo de esa ejecución de su experimento.

> [!TIP]
> toodocument las iteraciones del experimento de hello, puede modificar Hola título cada vez que se ejecuta, puede actualizar hello **resumen** de hello experimentar en panel de propiedades de Hola y puede agregar o actualizar comentarios acerca de los módulos individuales toorecord los cambios. comentarios de título, resumen y módulo Hola se guardan con cada ejecución del experimento de Hola.
> 
> 

lista de Hola de experimentos en hello **EXPERIMENTOS** ficha en estudio de aprendizaje automático siempre muestra la versión más reciente de Hola de un experimento. Si abre una ejecución anterior del experimento de hello (mediante **ejecutar anterior** o **ver el historial de ejecución**), puede devolver toohello versión de borrador, haga clic en **ver el historial de ejecución** y seleccione Hola iteración que tenga un **estado** de **Editable**.

## <a name="iterating-on-a-previous-run"></a>Iterar en una ejecución anterior
Al hacer clic en **Ejecución anterior** o en **VER HISTORIAL DE EJECUCIÓN**, puede ver un experimento terminado en modo de solo lectura.

Si desea toobegin una iteración de su experimento a partir de manera Hola está configurado para una ejecución anterior, puede hacerlo Hola abriendo ejecutar y haga clic en **SAVE AS**. Esto crea un experimento de nuevo con otro título, un historial de ejecución vacío y todos los componentes de Hola y valores de parámetro de hello anterior ejecutar. Este experimento nuevo aparece en hello **EXPERIMENTOS** pestaña en la página principal de estudio de aprendizaje automático de Hola y se puede modificar e historial para esta iteración de su experimento de ejecutarlo, iniciar una nueva ejecución. 

Por ejemplo, suponga que tiene experimento Hola historial que se muestra en la sección anterior de Hola de ejecución. Desea tooobserve ¿qué ocurre cuando se establece hello **velocidad de aprendizaje** parámetro too0.4 y pruebe distintos valores de hello **número de épocas de entrenamiento** parámetro.

1. Haga clic en **ver el historial de ejecución** y abra iteración Hola del experimento de saludo que ejecutó a las 4:28:36 p.m. (en el que establecer too0.4 de valor de parámetro hello).
2. Haga clic en **GUARDAR COMO**.
3. Escriba un título nuevo y haga clic en hello **Aceptar** marca de verificación. Se crea una nueva copia del experimento de Hola.
4. Modificar hello **número de épocas de entrenamiento** parámetro.
5. Haga clic en **EJECUTAR**.

Ahora puede continuar toomodify y ejecutar esta versión de su experimento, crear un nuevo toorecord de historial de ejecución de su trabajo.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
