---
title: "aaaHow un modelo de aprendizaje automático de Azure se convierte en un servicio web | Documentos de Microsoft"
description: "Información general sobre los mecanismos de Hola de modo que avanza el modelo de aprendizaje automático de Azure desde un desarrollo experimentar tooan de operaciones servicio Web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>Cómo un pasa de modelo de aprendizaje automático de un experimento tooan operaciones servicio Web
Estudio de aprendizaje automático de Azure proporciona un lienzo interactivo que permite toodevelop, ejecutar, probar y recorrer en iteración un ***experimentar*** que representa un modelo de análisis predictivos. Hay una gran variedad de módulos que le permiten realizar las acciones siguientes:

* Introducir datos en el experimento
* Manipular datos Hola
* Entrenar un modelo con algoritmos de aprendizaje automático
* Modelo de Hola de puntuación
* Evaluar los resultados de Hola
* Generar los resultados finales

Cuando esté satisfecho con el experimento, puede implementarlo como un ***servicio web Azure Machine Learning clásico*** o un ***servicio web Azure Machine Learning nuevo*** para que los usuarios puedan enviar datos nuevos y recibir los resultados de vuelta.

En este artículo, se ofrece una visión general de los mecanismos de Hola de modo que avanza el modelo de aprendizaje automático de un tooan de experimento de desarrollo operaciones servicio Web.

> [!NOTE]
> Hay otra maneras toodevelop e implementar modelos de aprendizaje automático, pero en este artículo se centra en cómo utilizar estudio de aprendizaje automático. Por ejemplo, tooread una descripción de cómo toocreate un servicio Web predictivo clásico con R, consulte Hola entrada de blog [compilación & implementar predictivo Web aplicaciones utilizando RStudio y aprendizaje automático de Azure](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx).
> 
> 

Mientras estudio de aprendizaje automático de Azure está diseñado toohelp desarrollar e implementar un *modelo de análisis predictivos*, es posible toouse Studio toodevelop un experimento no incluye un modelo de análisis predictivos. Por ejemplo, un experimento podría simplemente entrada de datos, manipular y, a continuación, mostrar los resultados de Hola. Al igual que un experimento de análisis predictivo, puede implementar este experimento no predicción como un servicio Web, pero es un proceso más sencillo porque experimento hello no entrenamiento o puntuar un modelo de aprendizaje automático. Mientras no resulta Hola típico toouse Studio de esta manera, se podrá incluir en las conversaciones de Hola para que podamos proporcionar a una explicación más completa de cómo funciona la Studio.

## <a name="developing-and-deploying-a-predictive-web-service"></a>Desarrollo e implementación de un servicio web predictivo
Estas son las fases de Hola que sigue una solución típica como desarrolla e implementa mediante el estudio de aprendizaje automático:

![Flujo de implementación](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*Ilustración 1 - Fases de un modelo de análisis predictivo típico*

### <a name="hello-training-experiment"></a>experimento de entrenamiento de Hola
Hola ***experimento de entrenamiento*** Hola fase inicial de desarrollo del servicio Web en estudio de aprendizaje automático. Hola de experimento de entrenamiento de hello sirve toogive un toodevelop lugar, probar, recorrer en iteración y finalmente entrenar un modelo de aprendizaje automático. Puede incluso entrenar varios modelos al mismo tiempo como Busque soluciones recomendadas hello, pero una vez que haya terminado experimentar se seleccionará un solo el entrenamiento del modelo y eliminar rest Hola de experimento de Hola. Para ver un ejemplo de desarrollo de un experimento de análisis predictivo, consulte [Desarrollo de una solución de análisis predictivo para la evaluación del riesgo de crédito en Aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="hello-predictive-experiment"></a>experimento predictivo Hola
Una vez que tenga un modelo entrenado en el experimento de entrenamiento, haga clic en **configurar el servicio de Web** y seleccione **predictivo servicio Web** en proceso de hello tooinitiate de estudio de aprendizaje automático de convertir el entrenamiento experimentar tooa ***experimento predictivo***. Hola propósito del experimento de predicción de hello es toouse los modelo entrenado tooscore nuevos datos, con el objetivo de Hola de finalmente se convierta en operaciones como un servicio Web de Azure.

Esta conversión se realiza automáticamente a través de hello pasos:

* Convertir Hola conjunto de módulos usados para el entrenamiento en un módulo único y guárdelo como un modelo entrenado
* Eliminar los módulos extraños no relacionado con tooscoring
* Agregar entrada y salida puertos que Hola eventual Web servicio va a usar

Puede haber más cambios que desee toomake tooget su toodeploy listo predictivo experimento como un servicio Web. Por ejemplo, si desea hello Web servicio toooutput solo un subconjunto de resultados, puede agregar un módulo de filtrado antes de puerto de salida de hello.

En este proceso de conversión, no se descarta el experimento de entrenamiento de Hola. Una vez completado el proceso de hello, tiene dos pestañas en Studio: uno para experimento de entrenamiento de hello y otro para experimento predictivo Hola. Este modo puede realizar cambios toohello experimento de entrenamiento antes de implementar el servicio Web y volver a generar experimento predictivo Hola. O bien, puede guardar una copia de toostart de experimento de entrenamiento de hello otra línea de experimentación.

> [!NOTE]
> Al hacer clic en **predictivo servicio Web** que inicia un proceso automático tooconvert el experimento de entrenamiento experimento tooa predictivo y esto funciona bien en la mayoría de los casos. Si el experimento de entrenamiento es complejo (por ejemplo, si tienen varias rutas de acceso para el entrenamiento que unen entre sí), podría ser preferible toodo esta conversión manualmente. Para obtener más información, consulte [cómo tooprepare el modelo para la implementación en estudio de aprendizaje automático de Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).
> 
> 

### <a name="hello-web-service"></a>Hola servicio Web
Cuando crea firmemente que el experimento predictivo está listo, puede implementar el servicio como servicio web clásico o nuevo basado en Azure Resource Manager. toooperationalize el modelo mediante la implementación como un *servicio Web de aprendizaje de máquina clásico*, haga clic en **implementar el servicio de Web** y seleccione **implementar servicio Web [estándar]**. toodeploy como *servicio Web de aprendizaje de máquina nueva*, haga clic en **implementar el servicio de Web** y seleccione **implementar [New] servicio Web**. Los usuarios ahora pueden enviar modelo de tooyour de datos mediante el servicio Web de hello API de REST y recibir resultados de Hola atrás. Para obtener más información, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>Hola caso no típico: crear un servicio Web no predictivo
Si el experimento no entrenar un modelo de análisis predictivos, entonces no es necesario toocreate un experimento de entrenamiento y un experimento de puntuación: hay solo un experimento y se puede implementar como un servicio Web. Estudio de aprendizaje automático detecta si el experimento contiene un modelo de predicción mediante el análisis de módulos de hello que ha usado.

Después de que haya iterado en el experimento y esté satisfecho con él:

1. Haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Retraining Web Service** (Servicio web de reentrenamiento): los nodos de entrada y salida se agregan automáticamente.
2. Haga clic en **Ejecutar**
3. Haga clic en **implementar el servicio de Web** y seleccione **implementar servicio Web [estándar]** o **implementar [New] servicio Web** función hello entorno toowhich desea toodeploy.

Hecho esto, el servicio web se habrá implementado, y puede acceder a él y a administrarlo como si fuera un servicio web predictivo.

## <a name="updating-your-web-service"></a>Actualización del servicio web
Ahora que ha implementado el experimento como un servicio Web, ¿qué ocurre si necesita tooupdate él?

Eso depende de lo que necesita tooupdate:

**Desea toochange Hola entrada o salida, o quiere toomodify cómo Hola servicio Web manipula datos**

Si no se está cambiando el modelo de hello, pero solo cambian cómo Hola servicio Web administra los datos, puede editar el experimento de predicción de hello y, a continuación, haga clic en **implementar el servicio de Web** y seleccione **implementar servicio Web [estándar]** o **implementar [New] servicio Web** nuevo. Hola servicio Web se detiene, hello experimento predictivo actualizada se implementa y se reinicia el servicio Web de Hola.

Este es un ejemplo: imagine que su experimento predictivo devuelve toda la fila de datos de entrada con Hola Hola predecir el resultado. Puede decidir que desea que el resultado del servicio de hello Web toojust Hola devuelto. Para poder agregar un **proyectar columnas** módulo en el experimento de predicción de hello, justo antes de puerto, de salida de hello tooexclude columnas que no sea de hello como resultado. Al hacer clic en **implementar el servicio de Web** y seleccione **implementar servicio Web [estándar]** o **implementar [New] servicio Web** nuevo, se actualiza Hola servicio Web.

**Desea tooretrain Hola modelo con nuevos datos**

Si desea que tookeep su modelo de aprendizaje automático, pero le gustaría tener tooretrain lo con nuevos datos, tiene dos opciones:

1. **Volver a entrenar el modelo de hello mientras se está ejecutando el servicio Web de hello** -si desea tooretrain el modelo mientras se ejecuta el servicio Web de la predicción hello, puede hacerlo mediante la realización de un par toomake de experimento de entrenamiento de toohello las modificaciones un *** reciclaje experimento***, a continuación, puede implementarlo como un  ***web reconversión* servicio**. Para obtener instrucciones sobre cómo toodo, vea [aprendizaje automático de volver a entrenar modelos mediante programación](machine-learning-retrain-models-programmatically.md).
2. **Volver atrás toohello experimento de entrenamiento original y utilizar su modelo de aprendizaje diferentes datos toodevelop** : su experimento predictivo está vinculado toohello servicio Web, pero experimento de entrenamiento de hello no está vinculada directamente de esta manera. Si modifica el experimento de entrenamiento original de Hola y haga clic en **configurar el servicio de Web**, creará un *nueva* predictivo experimentar que, cuando se implementa, creará un *nueva* Web servicio. No actualiza solo servicio Web original de Hola.
   
   Si necesita experimento de entrenamiento de hello toomodify, ábralo y haga clic en **Guardar como** toomake una copia. Esto dejará el experimento de entrenamiento original intacto hello y predicción experimento, servicio Web. Ahora puede crear un nuevo servicio web con los cambios. Una vez haya implementado Hola nuevo servicio Web de, a continuación, puede decidir si toostop Hola servicio Web anterior o mantenerlo ejecutándose junto con hello uno nuevo.

**Desea tootrain un modelo diferente**

Si desea toomake cambia experimento predictivo original tooyour, como la selección de un algoritmo de aprendizaje de automático diferentes tratando de un método de aprendizaje diferentes, etc., a continuación, se necesita toofollow Hola segundo procedimiento descrito anteriormente para volver a capacitar a su modelo de: Abra el experimento de entrenamiento de hello, haga clic en **Guardar como** toomake una copia y después iniciar hacia abajo de la nueva ruta de desarrollo de un modelo, crear experimento predictivo Hola e implementación de Hola Hola servicio web. Esto creará un nuevo servicio Web sin relación toohello original: puede decidir qué tookeep uno o ambos, que se ejecuta.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más detalles sobre el proceso de Hola de desarrollo y el experimento, vea Hola siguientes artículos:

* convertir el experimento de hello - [cómo tooprepare el modelo para la implementación en estudio de aprendizaje automático de Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* implementación de servicio Web de hello: [implementar un servicio web de aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md)
* modelo de hello reconversión - [aprendizaje automático de volver a entrenar modelos mediante programación](machine-learning-retrain-models-programmatically.md)

Para obtener ejemplos de proceso completo de hello, vea:

* [Tutorial de Aprendizaje automático: Creación del primer experimento en Estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md)
* [Tutorial: Desarrollo de una solución de análisis predictivo para la evaluación del riesgo de crédito en Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

