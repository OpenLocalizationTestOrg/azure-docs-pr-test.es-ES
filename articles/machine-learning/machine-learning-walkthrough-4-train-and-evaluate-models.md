---
title: "Paso 4: Entrenar y evaluar modelos de análisis predictivos de hello | Documentos de Microsoft"
description: "Paso 4 de hello desarrollar un tutorial de solución de predicción: entrenar, puntuarlos y evaluar varios modelos en estudio de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Paso 4 del tutorial: Entrenar y evaluar modelos de análisis predictivos de Hola
Este tema contiene el cuarto paso del tutorial de hello, de hello [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creación de un área de trabajo de Aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carga de los datos existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Crear un experimento nuevo](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Entrenar y evaluar modelos de Hola**
5. [Implementar el servicio Web de Hola](machine-learning-walkthrough-5-publish-web-service.md)
6. [Acceder al servicio Web Hola](machine-learning-walkthrough-6-access-web-service.md)

- - -
Una de las ventajas de hello del uso de estudio de aprendizaje automático de Azure para crear modelos de aprendizaje automático está Hola capacidad tootry más de un tipo de modelo a la vez en un experimento único y comparar resultados de Hola. Este tipo de experimentación le ayuda a encontrar Hola mejor solución para su problema.

En el experimento de hello desarrollamos en este tutorial, se creará dos tipos diferentes de modelos y, a continuación, comparar su puntuación toodecide resultados qué algoritmo queremos toouse en nuestro experimento final.  

Existen varios modelos entre los que se puede elegir. modelos de hello toosee disponibles, expanda hello **aprendizaje automático** nodo en la paleta de módulo de hello y, a continuación, expanda **inicializar modelo** y nodos de hello situado debajo de él. Para fines de Hola de este experimento, se seleccionará hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] (SVM) hello y [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulos.    

> [!TIP]
> tooget decidir qué algoritmo de aprendizaje automático mejor se adapte a problema concreto de Hola que está tratando de toosolve, consulte [cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Entrenar modelos de Hola

Vamos a agregar ambos hello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulo y [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo en este experimentar.

### <a name="two-class-boosted-decision-tree"></a>Árbol de decisión ampliado de dos clases

En primer lugar, vamos a configurar el modelo de árbol de decisión impulsado de Hola.

1. Buscar hello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulo en la paleta de módulo de Hola y lo arrastra al lienzo de Hola.

2. Buscar hello [entrenar modelo] [ train-model] módulo, arrástrelo al lienzo de Hola y, a continuación, conecte la salida de hello de hello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree]toohello módulo deja el puerto de entrada de hello [entrenar modelo] [ train-model] módulo.
   
   Hola [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulo inicializa modelo genérico de hello, y [entrenar modelo] [ train-model] utiliza datos de entrenamiento modelo de hello tootrain. 

3. Conecte Hola salida izquierdo de la izquierda de hello [ejecutar Script de R] [ execute-r-script] puerto de Hola de entrada de módulo toohello derecha [entrenar modelo] [ train-model] módulo (se decidió en [paso 3](machine-learning-walkthrough-3-create-new-experiment.md) de tutorial toouse Hola los datos procedentes de la parte izquierda de módulo de dividir datos de hello para el entrenamiento de hello).
   
   > [!TIP]
   > No se necesita dos entradas de hello y otro de salidas de Hola de hello [ejecutar Script de R] [ execute-r-script] módulo para este experimento, por lo que podemos o dejarlos adjuntas. 
   > 
   > 

Esta parte del experimento de hello ahora es algo parecido a esto:  

![Training a model][1]

Ahora necesitamos hello tootell [entrenar modelo] [ train-model] módulo que queremos que cada valor de riesgo de crédito Hola modelo toopredict Hola.

1. Seleccione hello [entrenar modelo] [ train-model] módulo. Hola **propiedades** panel, haga clic en **selector de columna de inicio**.

2. Hola **seleccionar una sola columna** cuadro de diálogo, escriba "riesgo de crédito" en el campo de búsqueda de hello en **columnas disponibles**, seleccione "Riesgo de crédito" a continuación y haga clic en el botón de flecha derecha de hello ( **>** ) toomove "Del crédito riesgo" demasiado**columnas seleccionadas**. 

    ![Seleccionar columna de riesgo del crédito de hello para el módulo entrenar modelo de Hola][0]

3. Haga clic en hello **Aceptar** marca de verificación.

### <a name="two-class-support-vector-machine"></a>Máquina de vectores de soporte de dos clases

A continuación, configuramos modelo SVM de Hola.  

En primer lugar, una breve explicación sobre SVM. Los árboles de decisión ampliados funcionan bien con características de todo tipo. Sin embargo, puesto que el módulo SVM de hello genera un clasificador lineal, modelo de Hola que genera tiene error de prueba recomendado hello cuando todas las características numéricas tienen Hola misma escala. tooconvert numérico todas las características toohello mismo escalar, se usa una transformación de "Tanh" (con hello [Normalizar datos] [ normalize-data] módulo). Esto transforma los números en el intervalo [0,1] Hola. módulo SVM de Hello convierte la cadena características toocategorical características y, a continuación, toobinary 0/1, por lo que no necesita transformar toomanually funciones de cadena. Además, no es aconsejable columna riesgo del crédito de hello tootransform (columna 21): es numérico, pero es valor Hola nos estamos entrenamiento Hola toopredict de modelo, por lo que necesitamos tooleave por su cuenta.  

tooset modelo de SVM de hello, Hola siguientes:

1. Buscar hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo en la paleta de módulo de Hola y lo arrastra al lienzo de Hola.

2. Menú contextual hello [entrenar modelo] [ train-model] módulo, seleccione **copia**y, a continuación, haga clic en el lienzo de Hola y seleccione **pegar**. Hola copia de hello [entrenar modelo] [ train-model] módulo tiene Hola misma selección de columna como Hola original.

3. Conecte la salida de hello de hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] toohello módulo izquierdo puerto de entrada de hello segundo [entrenar modelo] [ train-model] módulo.

4. Buscar hello [Normalizar datos] [ normalize-data] módulo y lo arrastra al lienzo de Hola.

5. Conecte Hola salida izquierdo de la izquierda de hello [ejecutar Script de R] [ execute-r-script] entrada toohello de módulo de este módulo (Observe que Hola de puerto de salida de un módulo puede ser toomore conectado a un módulo de otro).

6. Conectar Hola dejado el puerto de salida de hello [Normalizar datos] [ normalize-data] módulo toohello derecha de entrada de puerto de hello en segundo lugar [entrenar modelo] [ train-model] módulo.

Esta parte de nuestro experimento debería tener ahora un aspecto similar al siguiente:  

![Modelo de entrenamiento Hola segundo][2]  

Configurar ahora hello [Normalizar datos] [ normalize-data] módulo:

1. Haga clic en hello tooselect [Normalizar datos] [ normalize-data] módulo. Hola **propiedades** panel, seleccione **Tanh** para hello **método de transformación** parámetro.

2. Haga clic en **selector de columna de inicio**, seleccione "No hay columnas" para **comenzar con**, seleccione **Include** en la primera lista desplegable de hello, seleccione **el tipo de columna**en Hola segunda lista desplegable y seleccione **numérico** en lista desplegable terceros de Hola. Especifica que todas las columnas numéricas de hello (y numérico único) se transforman.

3. Haga clic en Hola toohello de signo más (+) derecha de esta fila - Esto crea una fila de listas desplegables. Seleccione **excluir** en la primera lista desplegable de hello, seleccione **nombres de columna** en Hola segunda lista desplegable y escriba "Riesgo de crédito" en el campo de texto hello. Esto especifica que se debe omitir esa columna de riesgo de crédito hello (necesitamos toodo esto porque esta columna es numérica y así se transformaría si no excluirla).

4. Haga clic en hello **Aceptar** marca de verificación.  

    ![Seleccione las columnas para el módulo de hello Normalizar datos][5]

Hola [Normalizar datos] [ normalize-data] módulo ahora es conjunto tooperform una transformación Tanh en todas las columnas numéricas excepto Hola riesgo de crédito.  

## <a name="score-and-evaluate-hello-models"></a>Puntuar y evaluar modelos de Hola

Usamos Hola comprobación de datos que se distinguiendo entre hello [dividir datos] [ split] tooscore módulo nuestros modelos entrenados. A continuación, se puedan comparar resultados de Hola de hello dos modelos toosee que genera los mejores resultados.  

### <a name="add-hello-score-model-modules"></a>Agregar módulos de modelo de puntuación de Hola

1. Buscar hello [puntuar modelo] [ score-model] módulo y lo arrastra al lienzo de Hola.

2. Conectar hello [entrenar modelo] [ train-model] módulo que se ha conectado toohello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] entrada izquierda de módulo toohello puerto de hello [puntuar modelo] [ score-model] módulo.

3. Conectar derecha hello [ejecutar Script de R] [ execute-r-script] puerto de Hola de entrada de módulo (nuestros datos de prueba) toohello derecha [puntuar modelo] [ score-model] módulo.

    ![Módulo Score Model (Puntuar modelo) conectado][6]
   
   Hola [puntuar modelo] [ score-model] módulo ahora puede aprovechar la información de crédito de Hola de hello datos, se debe ejecutar utilizando el modelo de hello, de prueba y comparar las predicciones de hello genera el modelo de hello con hello real riesgo de crédito columna de datos de prueba de Hola.

4. Copie y pegue hello [puntuar modelo] [ score-model] toocreate módulo una segunda copia.

5. Conecte la salida de hello de modelo SVM de hello (es decir, el puerto de hello de la salida de hello [entrenar modelo] [ train-model] módulo que se ha conectado toohello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo) toohello de entrada de puerto de hello en segundo lugar [puntuar modelo] [ score-model] módulo.

6. Para el modelo de SVM de hello, tenemos toodo Hola los mismos datos de prueba de toohello de transformación igual que hicimos toohello datos de entrenamiento. Por lo tanto, copiar y pegar hello [Normalizar datos] [ normalize-data] toocreate módulo una segunda copia y conéctelo derecha toohello [ejecutar Script de R] [ execute-r-script] módulo.

7. Conecte la salida de izquierdo de Hola de hello en segundo lugar [Normalizar datos] [ normalize-data] módulo toohello derecha de entrada de puerto de hello en segundo lugar [puntuar modelo] [ score-model] módulo.

    ![Ambos módulos Score Model (Puntuar modelo) conectados][7]

### <a name="add-hello-evaluate-model-module"></a>Agregar módulo de hello evaluar modelo

tooevaluate Hola dos resultados de puntuación y compararlos, usamos un [evaluar modelo] [ evaluate-model] módulo.  

1. Buscar hello [evaluar modelo] [ evaluate-model] módulo y lo arrastra al lienzo de Hola.

2. Conecte los puertos de salida de hello de hello [puntuar modelo] [ score-model] módulo asociado Hola impulsado puerto de hello de entrada izquierda toohello de modelo de árbol de decisión [evaluar modelo] [ evaluate-model] módulo.

3. Conectar Hola otro [puntuar modelo] [ score-model] puerto de entrada de módulo toohello derecha.  

    ![Módulo Evaluate Model (Evaluar modelo) conectado][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Ejecute el experimento de Hola y comprobar los resultados de Hola

toorun Hola experimento, haga clic en hello **ejecutar** botón a continuación lienzo Hola. Esto puede tardar unos minutos. Se muestra un indicador de giro en cada módulo que se está ejecutando y, a continuación, una marca de verificación verde muestra cuando finalice el módulo de Hola. Cuando todos los módulos de hello tienen una marca de verificación, experimento Hola ha terminado de ejecutarse.

el experimento de Hello ahora debería ser similar al siguiente:  

![Evaluating both models][3]

resultados de hello toocheck, haga clic en puerto de salida de hello de hello [evaluar modelo] [ evaluate-model] módulo y seleccione **visualizar**.  

Hola [evaluar modelo] [ evaluate-model] módulo genera un par de curvas y las métricas que le permiten resultados de Hola de toocompare de hello dos modelos de puntuación. Puede ver los resultados de hello como característica de operador de receptor (ROC) curvas, curvas de precisión/recuperación o curvas de elevación. Datos adicionales que se muestra incluyen una matriz de confusión, valores acumulativos de área de hello en curva de hello (AUC) y otras métricas. Puede cambiar el valor de umbral de Hola por móvil control deslizante izquierdo o derecho de Hola y ver cómo afecta al conjunto de Hola de métricas.  

toohello derecha del gráfico de hello, haga clic en **conjunto de datos puntuado** o **puntúan toocompare de conjunto de datos** toohighlight Hola asociado curva y toodisplay Hola asociados métricas a continuación. En la leyenda de Hola para curvas de hello, "Conjunto de datos puntuado" corresponde toohello dejado el puerto de entrada de hello [evaluar modelo] [ evaluate-model] módulo - en nuestro caso, este es el modelo de árbol de decisión impulsado de Hola. "Toocompare de conjunto de datos de puntuación" corresponde toohello puerto de entrada derecha - modelo SVM de hello en nuestro caso. Al hacer clic en una de estas etiquetas, se resalta la curva de Hola para dicho modelo y se muestran las métricas de hello correspondiente, tal y como se muestra en el siguiente gráfico de Hola.  

![ROC curves for models][4]

Mediante el examen de estos valores, puede decidir qué modelo es más cercano toogiving que Hola resultados que está buscando. Puede volver atrás y repita el experimento cambiando los valores de parámetro en modelos diferentes de Hola. 

Hola y ciencia de interpretar estos resultados y optimizar el rendimiento del modelo hello es ámbito de hello fuera de este tutorial. Para obtener ayuda adicional, puede leer Hola siguientes artículos:
- [¿Cómo tooevaluate modelo rendimiento aprendizaje automático de Azure](machine-learning-evaluate-model-performance.md)
- [Elegir parámetros toooptimize sus algoritmos de aprendizaje automático de Azure](machine-learning-algorithm-parameters-optimize.md)
- [Cómo interpretar los resultados del modelo de Azure Machine Learning](machine-learning-interpret-model-results.md)

> [!TIP]
> Cada vez que ejecute el experimento de hello un registro de esa iteración se mantiene en hello historial de ejecución. Puede ver estas iteraciones y devolver tooany de ellos, haciendo clic en **ver el historial de ejecución** por debajo del lienzo de Hola. También puede hacer clic en **ejecutar anterior** en hello **propiedades** Hola de iteración de panel tooreturn toohello inmediatamente anterior a uno que tenga abiertos.
> 
> Puede realizar una copia de alguna iteración del experimento, haga clic en **SAVE AS** por debajo del lienzo de Hola. 
> Usar del experimento de hello **resumen** y **descripción** propiedades tookeep un registro de lo que probó en las iteraciones de experimento.
> 
> Consulte [Administración de iteraciones de experimentos en Estudio de aprendizaje automático de Azure](machine-learning-manage-experiment-iterations.md)para obtener más detalles.  
> 
> 

- - -
**Siguiente: [implementar el servicio web de Hola](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
