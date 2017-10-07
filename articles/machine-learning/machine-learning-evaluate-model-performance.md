---
title: "rendimiento de los modelos aaaEvaluate en aprendizaje automático | Documentos de Microsoft"
description: "Explica cómo tooevaluate modelo rendimiento aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>¿Cómo tooevaluate modelo rendimiento aprendizaje automático de Azure
Este artículo demuestra cómo tooevaluate Hola de rendimiento de un modelo en estudio de aprendizaje automático de Azure y proporciona una breve explicación de las métricas de hello disponibles para esta tarea. Se presentan tres escenarios comunes de aprendizaje supervisado: 

* regresión
* clasificación binaria 
* clasificación multiclase

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Evaluar el rendimiento de Hola de un modelo es uno de etapas principales de hello en el proceso de ciencia de datos Hola. Indica éxito Hola puntuación (predicciones) de un conjunto de datos ha sido mediante un modelo entrenado. 

Azure Machine Learning admite la evaluación de modelos a través de dos de sus módulos principales de aprendizaje automático: [Evaluar modelo][evaluate-model] y [Validar modelo de forma cruzada][cross-validate-model]. Estos módulos le permiten toosee cómo realiza el modelo en cuanto a un número de métricas que se usan habitualmente en las estadísticas y el aprendizaje automático.

## <a name="evaluation-vs-cross-validation"></a>Evaluación frente a Validación cruzada
Evaluación y validación cruzada son rendimiento de hello toomeasure de forma estándar del modelo. Ambos generan métricas de evaluación que puede inspeccionar o comparar con las de otros modelos.

[Evaluar el modelo de] [ evaluate-model] espera un conjunto de datos con puntuación como entrada (o 2 caso en que desea que el rendimiento de hello toocompare de 2 modelos diferentes). Esto significa que necesita tootrain el modelo usando hello [entrenar modelo] [ train-model] módulo y realizar predicciones sobre algún conjunto de datos mediante hello [puntuar modelo] [ score-model] módulo, para poder evaluar los resultados de Hola. Hello evaluación se basa Hola puntuado etiquetas/probabilidades junto con etiquetas de hello es true, todos los cuales son salida Hola [puntuar modelo] [ score-model] módulo.

Como alternativa, puede usar la validación cruzada tooperform una serie de puntuación de entrenar evaluar operaciones (10 subconjuntos) automáticamente en distintos subconjuntos de datos de entrada de Hola. datos de entrada de Hola se dividen en partes de 10, que está reservado para las pruebas y Hola otros 9 para el entrenamiento. Este proceso se repite 10 veces y se calcula el promedio de las métricas de evaluación de Hola. Esto ayuda a determinar el grado en que un modelo podría extrapolarse toonew conjuntos de datos. Hola [modelo de validación cruzada] [ cross-validate-model] módulo toma en un modelo no entrenado y algunos resultados de evaluación de Hola de conjunto de datos y los resultados de cada uno de Hola la etiqueta 10 subconjuntos, además toohello Promediar resultados.

Hola siguientes secciones, se generar modelos de regresión y de clasificación simples y evaluar su rendimiento, con ambos hello [evaluar modelo] [ evaluate-model] hello y [realizar una validación cruzada Modelo] [ cross-validate-model] módulos.

## <a name="evaluating-a-regression-model"></a>Evaluación de un modelo de regresión
Supongamos que desea toopredict precio del automóvil mediante algunas características, como dimensiones, potencia, las especificaciones de motor y así sucesivamente. Se trata de un problema de regresión típicos, donde Hola variable de destino (*precio*) es un valor numérico continuo. Podemos incluir un modelo de regresión lineal simple que, dada la característica de hello valores de un automóvil determinado, puede predecir precio Hola de ese automóvil. Este modelo de regresión se puede utilizar tooscore Hola se entrenó en mismo conjunto de datos. Una vez que nos hemos hello predichos precios de automóviles Hola todos, se podemos evaluar el rendimiento de Hola de modelo de hello examinando cuánto predicciones Hola se desvían de precios reales de hello en promedio. tooillustrate, usamos hello *conjunto de datos (Raw) de precios de automóviles* disponibles en hello **conjuntos de datos guardados** sección en estudio de aprendizaje automático de Azure.

### <a name="creating-hello-experiment"></a>Creación de hello experimento
Agregue Hola después de área de trabajo de tooyour de módulos de estudio de aprendizaje automático de Azure:

* Información sobre los precios de los automóviles (datos sin procesar)
* [Regresión lineal][linear-regression]
* [Train Model][train-model] (Entrenar modelo)
* [Puntuar modelo][score-model]
* [Evaluar modelo][evaluate-model]

Conectar puertos de hello tal y como se muestra a continuación en la figura 1 y la columna de etiqueta de Hola de conjunto de hello [entrenar modelo] [ train-model] módulo demasiado*precio*.

![Evaluación de un modelo de regresión](media/machine-learning-evaluate-model-performance/1.png)

Figura 1. Evaluación de un modelo de regresión.

### <a name="inspecting-hello-evaluation-results"></a>Inspeccionar los resultados de la evaluación de Hola
Después de la ejecución experimento de hello, puede hacer clic en puerto de salida de hello de hello [evaluar modelo] [ evaluate-model] módulo y seleccione *visualizar* toosee resultados de la evaluación de Hola. Hola métricas de evaluación disponibles para los modelos de regresión son: *desviación significa*, *Error absoluto medio raíz significa*, *Error absoluto relativo*, * Error cuadrático relativo*, hello y *coeficiente de determinación*.

término de Hola "error" representa la diferencia de hello entre Hola valor predicho y el valor de true Hola. valor absoluto de Hola o hello cuadrado de esta diferencia son normalmente calculada toocapture Hola total magnitud de los errores en todas las instancias, como diferencia de hello entre Hola predecir y valor true puede ser negativo en algunos casos. las métricas de error de Hola medir el rendimiento de predicción de Hola de un modelo de regresión en términos de la desviación media de Hola de sus predicciones a partir de valores true Hola. Los valores más bajos de error significan modelo hello es más precisa para realizar predicciones. Una métrica de error general de 0 significa que Hola modelo se adapta perfectamente a datos de Hola.

coeficiente de Hola de determinación, que también se conoce como R cuadrado, también es una manera estándar de medir el grado en que modelo Hola se adapta a los datos de Hola. Se puede interpretar como proporción de hello de la variación explicado el modelo de Hola. Una mayor proporción es mejor en este caso, donde 1 indica un ajuste perfecto.

![Métricas de evaluación de regresión lineal](media/machine-learning-evaluate-model-performance/2.png)

Ilustración 2. Métricas de evaluación de regresión lineal.

### <a name="using-cross-validation"></a>Uso de la validación cruzada
Tal y como se mencionó anteriormente, puede realizar entrenamiento repetido, puntuación y las evaluaciones de forma automática utilizando Hola [modelo de validación cruzada] [ cross-validate-model] módulo. Lo único que necesita en este caso es un conjunto de datos, un modelo sin entrenar y un módulo [Validar modelo de forma cruzada][cross-validate-model] (consulte la ilustración siguiente). Tenga en cuenta que necesita demasiado columna de etiqueta de hello tooset*precio* en hello [modelo de validación cruzada] [ cross-validate-model] propiedades del módulo.

![Validación cruzada de un modelo de regresión](media/machine-learning-evaluate-model-performance/3.png)

Figura 3. Validación cruzada de un modelo de regresión.

Después de la ejecución experimento de hello, puede inspeccionar resultados de la evaluación de hello haciendo clic en el puerto de salida derecha Hola de hello [modelo de validación cruzada] [ cross-validate-model] módulo. Esto le dará una vista detallada de las métricas de Hola para cada iteración (subconjunto) y Hola Promediar resultados de cada una de las métricas de hello (ilustración 4).

![Resultados de la validación cruzada de un modelo de regresión](media/machine-learning-evaluate-model-performance/4.png)

Figura 4. Resultados de la validación cruzada de un modelo de regresión.

## <a name="evaluating-a-binary-classification-model"></a>Evaluación de un modelo de clasificación binaria
En un escenario de clasificación binaria, variable de destino de hello tiene solo dos resultados posibles, por ejemplo: {0, 1} o {false, true}, {negativo, positivo}. Suponga que tiene un conjunto de datos de empleados para adultos con algunos demográficos y variables de empleo y que se le pide el nivel de ingresos toopredict hello, una variable binaria con valores de hello {"< = 50K", "> 50K"}. En otras palabras, clase negativo de hello representa los empleados de Hola que menor o igual que too50K por año y Hola positivo clase representa todos los demás empleados. Como en el escenario de regresión de hello, se podría entrenar un modelo, puntuación algunos datos y evaluar los resultados de Hola. Hola principal diferencia es la opción de Hola de métricas de que aprendizaje automático de Azure calcula y salidas. escenario de predicción de nivel de ingresos de hello tooillustrate, usaremos hello [para adultos](http://archive.ics.uci.edu/ml/datasets/Adult) toocreate de conjunto de datos un aprendizaje automático de Azure experimentar y evaluar el rendimiento de Hola de un modelo de regresión logística de dos clases, un archivo binario usado clasificador.

### <a name="creating-hello-experiment"></a>Creación de hello experimento
Agregue Hola después de área de trabajo de tooyour de módulos de estudio de aprendizaje automático de Azure:

* Conjunto de datos de clasificación binaria de ingresos en el censo de adultos
* [Regresión logística de dos clases][two-class-logistic-regression]
* [Train Model][train-model] (Entrenar modelo)
* [Puntuar modelo][score-model]
* [Evaluar modelo][evaluate-model]

Conectar puertos de hello tal y como se muestra a continuación en la figura 5 y la columna de etiqueta de Hola de conjunto de hello [entrenar modelo] [ train-model] módulo demasiado*ingresos*.

![Evaluación de un modelo de clasificación binaria](media/machine-learning-evaluate-model-performance/5.png)

Figura 5. Evaluación de un modelo de clasificación binaria.

### <a name="inspecting-hello-evaluation-results"></a>Inspeccionar los resultados de la evaluación de Hola
Después de la ejecución experimento de hello, puede hacer clic en puerto de salida de hello de hello [evaluar modelo] [ evaluate-model] módulo y seleccione *visualizar* resultados de evaluación de hello toosee (Ilustración 7). Hola métricas de evaluación disponibles para los modelos de clasificación binaria son: *precisión*, *precisión*, *recuerde*, *F1 puntuación*, y *AUC*. Además, el módulo de hello genera una matriz de confusión que muestra el número de Hola de verdaderos positivos, falsos negativos, falsos positivos y negativos es true, así como *ROC*, *precisión/recuperación*y *Elevación* curvas.

Precisión es simplemente un Hola proporción de instancias clasificadas correctamente. Suele ser métrica primera Hola que mirar al evaluar un clasificador. Sin embargo, cuando los datos de prueba de hello están asimétrica (donde la mayoría de las instancias de hello pertenecen tooone de clases de hello) o está más interesado en el rendimiento de hello en cualquiera de las clases de hello, precisión realmente no captura eficacia Hola de un clasificador. En el escenario de nivel de clasificación de ingresos hello, suponga que está probando en algunos datos donde 99% de las instancias de hello representan usuarios disfrutar de menor o igual too50K por año. Es posible tooachieve una exactitud 0,99 por predecir clase hello "< = 50K" para todas las instancias. Clasificador de Hello en este caso aparece toobe haciendo un buen trabajo global, pero en realidad, se produce un error tooclassify cualquiera de las personas con ingresos elevados de hello (Hola 1%) correctamente.

Por esta razón, resulta útil toocompute otras métricas que capturen los aspectos más específicos de evaluación de Hola. Antes de entrar en detalles de Hola de esas métricas, es importante toounderstand matriz de confusión Hola supone una evaluación de clasificación binaria. clase Hello las etiquetas en el conjunto de entrenamiento de hello pueden tardar en solo 2 posibles valores, que se suele hacer referencia tooas positivo o negativo. instancias positivos y negativos de Hola que un clasificador predice correctamente se denominan (TP) de verdaderos positivos y negativos true (TN), respectivamente. De igual forma, se denominan instancias Hola clasificado incorrectamente (FP) de falsos positivos y falsos negativos (FN). matriz de confusión Hello es simplemente una tabla que muestra el número de Hola de instancias que se encuentran en cada una de estas 4 categorías. Aprendizaje automático de Azure automáticamente decide cuál de las dos clases de hello en el conjunto de datos de hello es clase positivo de hello. Si las etiquetas de clase de hello son un valor booleano o enteros, Hola instancias con la etiqueta 'true' o '1' se asignan clase positivo Hola. Si las etiquetas de hello son cadenas, como en caso de hello del conjunto de datos de ingresos hello, las etiquetas de Hola se ordenan alfabéticamente y primer nivel de Hola se elige clase negativo de hello toobe mientras Hola segundo nivel es clase positivo Hola.

![Matriz de confusión de la clasificación binaria](media/machine-learning-evaluate-model-performance/6a.png)

Figura 6. Matriz de confusión de la clasificación binaria.

Si vuelve toohello problema de clasificación de ingresos, sería aconsejable tooask varias cuestiones de evaluación que nos ayudan a comprender el rendimiento de Hola de clasificador Hola utilizado. Una pregunta muy natural es: ' fuera de usuarios de Hola que Hola modelo toobe predicho ganar > 50 K (TP + FP), cuántos se han clasificado correctamente (TP)? " Puede responder esta pregunta examinando hello **precisión** de modelo de hello, que es la proporción de Hola de positivos que se han clasificado correctamente: TP/(TP+FP). Otra pregunta común es "fuera de todos los Hola alta ganancias empleados con ingresos > 50 k (TP + FN), cuántos Hola clasificador clasificar correctamente (TP)". Esto es realmente hello **recuerde**, u Hola verdadero positivo tasa: TP/(TP+FN) de clasificador Hola. Observará que hay una evidente compensación entre la precisión y la recuperación. Por ejemplo, dado un conjunto de datos relativamente equilibrada, un clasificador que predice principalmente positivos instancias, tendría una recuperación alta, pero ¿se clasifican incorrectamente una precisión baja en su lugar tantas instancias negativo Hola resultante en un gran número de falsos positivos. toosee un gráfico de cómo modificar estos dos métricas, puede hacer clic en la curva de hello ' Precisión/recuperación' en la página de salida de resultados de evaluación de hello (parte superior izquierda de la figura 7).

![Resultados de la evaluación de clasificación binaria](media/machine-learning-evaluate-model-performance/7.png)

 Ilustración 7. Resultados de la evaluación de clasificación binaria.

Otro relacionados con la métrica que se utiliza a menudo es hello **F1 puntuación**, que toma la precisión y la recuperación en consideración. Es la media armónica de Hola de estas métricas de 2 y se calcula como tal: F1 = 2 (recuerde precisión x) / (precisión + recuperación). puntuación de F1 de Hello es una evaluación de buena forma toosummarize hello en un número único, pero siempre es una toolook buenas prácticas en precisión y recuperación toobetter junto comprender cómo se comporta un clasificador.

Asimismo, uno puede inspeccionar tasa positivo true de hello frente a Hola de falsos positivos en hello **característica de funcionamiento de receptor (ROC)** curva y Hola correspondiente **área en hello curva (AUC)** valor. Hello más cerca esta curve toohello superior izquierda de la esquina, el rendimiento del clasificador del Hola de mejor hello es (es decir maximizar Hola true positivo velocidad y reduce su índice de falsos positivos hello). Curvas de toohello cerrar diagonal de Hola trazado, resultado de clasificadores que suelen toomake predicciones cerrar toorandom adivinanzas.

### <a name="using-cross-validation"></a>Uso de la validación cruzada
Como en el ejemplo de regresión de hello, podemos realizar la validación cruzada toorepeatedly entrenar, puntuación y evaluar diferentes subconjuntos de datos de hello automáticamente. De forma similar, podemos usar hello [modelo de validación cruzada] [ cross-validate-model] módulo, un modelo de regresión logística no entrenado y un conjunto de datos. columna de etiqueta de Hello debe establecerse demasiado*ingresos* en hello [modelo de validación cruzada] [ cross-validate-model] propiedades del módulo. Después de puerto de hello de salida ejecutan experimentación hello y haciendo clic en hello derecho [modelo de validación cruzada] [ cross-validate-model] módulo, podemos ver valores de métrica de clasificación binaria de Hola para cada subconjunto, además toohello Media y desviación estándar de cada uno de ellos. 

![Validación cruzada de un modelo de clasificación binaria](media/machine-learning-evaluate-model-performance/8.png)

Figura 8. Validación cruzada de un modelo de clasificación binaria.

![Resultados de la validación cruzada de un clasificador binario](media/machine-learning-evaluate-model-performance/9.png)

Figura 9. Resultados de la validación cruzada de un clasificador binario.

## <a name="evaluating-a-multiclass-classification-model"></a>Evaluación de un modelo de clasificación multiclase
En este experimento usaremos Hola popular [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") conjunto de datos que contiene las instancias de 3 diferentes tipos (clases) de planta de iris Hola. Hay 4 valores de características (longitud y ancho del sépalo y del pétalo) para cada instancia. En los experimentos anteriores Hola se entrena y modelos probados hello mediante Hola mismos conjuntos de datos. En este caso, usaremos hello [dividir datos] [ split] subconjuntos de toocreate 2 de módulo de datos de hello, entrene en hello en primer lugar y puntuación y evalúe en hello segundo. Hello conjunto de datos de Iris esté disponible públicamente en hello [repositorio de aprendizaje automático UCI](http://archive.ics.uci.edu/ml/index.html)y puede descargarse con un [importar datos] [ import-data] módulo.

### <a name="creating-hello-experiment"></a>Creación de hello experimento
Agregue Hola después de área de trabajo de tooyour de módulos de estudio de aprendizaje automático de Azure:

* [Importar datos][import-data]
* [Bosque de decisión multiclase][multiclass-decision-forest]
* [Split Data][split] (Dividir datos)
* [Train Model][train-model] (Entrenar modelo)
* [Puntuar modelo][score-model]
* [Evaluar modelo][evaluate-model]

Conectar puertos de hello tal y como se muestra a continuación en la figura 10.

Establece el índice de columna de etiqueta de Hola de hello [entrenar modelo] [ train-model] too5 de módulo. conjunto de datos de Hello no tiene ninguna fila de encabezado pero sabemos que esa clase hello las etiquetas son en hello quinta columna.

Haga clic en hello [importar datos] [ import-data] módulo conjunto hello y *origen de datos* propiedad demasiado*dirección URL Web a través de HTTP*, hello y *dirección URL * toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Fracción de Hola de conjunto de toobe de instancias que se usa para el entrenamiento en hello [dividir datos] [ split] módulo (0,7 por ejemplo).

![Evaluar un clasificador multiclase](media/machine-learning-evaluate-model-performance/10.png)

Figura 10. Evaluar un clasificador multiclase

### <a name="inspecting-hello-evaluation-results"></a>Inspeccionar los resultados de la evaluación de Hola
Ejecute el experimento de Hola y haga clic en puerto de salida de hello de [evaluar modelo][evaluate-model]. resultados de la evaluación de Hola se presentan en forma de Hola de una matriz de confusión, en este caso. matriz de Hello muestra hello real frente a instancias de predicción para todas las clases de 3.

![Resultados de la evaluación de clasificación multiclase](media/machine-learning-evaluate-model-performance/11.png)

Figura 11. Resultados de la evaluación de clasificación multiclase.

### <a name="using-cross-validation"></a>Uso de la validación cruzada
Tal y como se mencionó anteriormente, puede realizar entrenamiento repetido, puntuación y las evaluaciones de forma automática utilizando Hola [modelo de validación cruzada] [ cross-validate-model] módulo. Necesitaría un conjunto de datos, un modelo sin entrenar y un módulo [Validar modelo de forma cruzada][cross-validate-model] (consulte la ilustración siguiente). Vuelva a necesario columna de etiqueta de hello tooset de hello [modelo de validación cruzada] [ cross-validate-model] módulo (índice de columna 5 en este caso). Después de puerto de hello de salida ejecutan experimentación hello y haga clic en el derecho de Hola [modelo de validación cruzada][cross-validate-model], puede inspeccionar los valores de métrica de Hola para cada subconjunto como Hola Media y desviación estándar. métricas de Hello mostradas aquí están Hola similar toohello que se han tratado en caso de clasificación binaria de Hola. Sin embargo, tenga en cuenta que en la clasificación multiclase, informática Hola verdaderos positivos o negativos y falsos positivos o negativos contando en forma de clase por clase, ya que no existe ninguna clase general positiva o negativa. Por ejemplo, cuando informático precisión de Hola o recuperación de hello 'Iris setosa' clase, se supone que es clase positivo de hello y todos los demás como negativo.

![Validación cruzada de un modelo de clasificación multiclase](media/machine-learning-evaluate-model-performance/12.png)

Ilustración 12. Validación cruzada de un modelo de clasificación multiclase.

![Resultados de una validación cruzada de un modelo de clasificación multiclase](media/machine-learning-evaluate-model-performance/13.png)

Ilustración 13. Resultados de una validación cruzada de un modelo de clasificación multiclase.

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

