---
title: "modelos de análisis de texto aaaCreate en estudio de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Cómo los modelos de análisis de texto toocreate de estudio de aprendizaje automático de Azure mediante módulos de preprocesamiento de texto, N gramos o hash de características"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Creación de modelos de análisis de texto en Azure Machine Learning Studio
Puede usar toobuild de aprendizaje automático de Azure y hacer operativos los modelos de análisis de texto. Estos modelos pueden ayudarle a resolver, por ejemplo, problemas de clasificación de documentos o de análisis de opinión.

En un experimento de análisis de texto, normalmente debería:

1. Limpiar y preprocesar el conjunto de datos de texto
2. Extraer vectores numéricos de características del texto preprocesado
3. Entrenar un modelo de clasificación o regresión
4. Puntuación y validar el modelo de Hola
5. Implementar Hola modelo tooproduction

En este tutorial, aprenderá estos pasos a medida que se explique un modelo de análisis de opinión mediante el conjunto de datos de Amazon Book Reviews (consulte el trabajo de investigación, “Biographies, Bollywood, Boom-boxes and Blenders: Domain Adaptation for Sentiment Classification” ("Biografías, Bollywoood, equipos de sonido y licuadoras") de John Blitzer, Mark Dredze y Fernando Pereira; Asociación de Lingüística Informática (ACL), 2007. Este conjunto de datos consta de las puntuaciones de revisión (1-2 o 4-5) y un texto de forma libre. Hello objetivo es puntuación de revisión de Hola toopredict: baja (1 - 2) o high (4-5).

Puede encontrar los experimentos descritos en este tutorial en la Galería de Cortana Intelligence:

[Predict Book Reviews](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Predict Book Reviews - Predictive Experiment](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>Paso 1: Limpiar y preprocesar el conjunto de datos de texto
Empezaremos Hola experimento dividiendo las puntuaciones de revisión de hello en categorías depósitos inferior y superior problema de hello tooformulate como clasificación de dos clases. Se utilizarán los módulos [Editar metadatos](https://msdn.microsoft.com/library/azure/dn905986.aspx) y [Agrupar valores categóricos](https://msdn.microsoft.com/library/azure/dn906014.aspx).

![Crear etiqueta](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

A continuación, se limpia Hola texto mediante [texto de preprocesamiento](https://msdn.microsoft.com/library/azure/mt762915.aspx) módulo. limpieza de Hello reduce el ruido de hello en el conjunto de datos de hello, Hola a ayudan a encontrar Hola características más importantes y mejorar la precisión del modelo final de Hola. Se eliminan las palabras irrelevantes: palabras comunes como "el" o "un", y números, caracteres especiales, caracteres duplicados, direcciones de correo electrónico y direcciones URL. Se también convertir Hola texto toolowercase, lemmatize palabras hello y detectar los límites de oración, a continuación, se indican mediante "|" símbolo de texto preprocesada.

![preprocesamiento de texto](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

¿Qué ocurre si desea toouse una lista de palabras irrelevantes personalizada? Puede pasarla como entrada opcional. También puede usar personalizado C# sintaxis de la expresión regular tooreplace subcadenas y quitar palabras por parte de la oración: sustantivos, verbos o adjetivos.

Una vez completada la Hola preprocesamiento, se dividir los datos de hello en el entrenamiento y conjuntos de pruebas.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>Paso 2: Extraer vectores numéricos de características del texto preprocesado
toobuild un modelo de datos de texto, normalmente tiene texto de forma libre de tooconvert en vectores de característica numéricos. En este ejemplo, utilizamos [extraer características de N-gramas de texto](https://msdn.microsoft.com/library/azure/mt762916.aspx) formato de toosuch de datos de texto de módulo tootransform Hola. Este módulo toma una columna de palabras separadas por espacios en blanco y procesa un diccionario de palabras, o n-gramas de palabras, que aparecerán en el conjunto de datos. A continuación, cuenta cuántas veces aparece cada palabra, o n-grama, en cada registro y crea los vectores de características a partir de los recuentos. En este tutorial, establecemos too2 de tamaño de n-gramas, por lo que nuestro vectores de característica incluyen palabras o combinaciones de dos o más palabras posteriores.

![Extraer n-gramas](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

Se aplica TF * IDF (término frecuencia inversa documento frecuencia) ponderación tooN grama recuentos. Este método agrega el peso de palabras que aparecen frecuentemente en un único registro pero poco frecuentes a través de hello todo el conjunto de datos. Otras opciones incluyen la ponderación binaria, de TF y de gráfico.

A menudo, estas características de texto tienen una alta dimensionalidad. Por ejemplo, si el conjunto tiene 100 000 palabras únicas, el espacio de características tendrá 100 000 dimensiones o incluso más si se usan n-gramas. módulo de extraer características de N-gramas Hola proporciona un conjunto de dimensionalidad de hello tooreduce de opciones. Puede elegir tooexclude palabras que son el valor de predicción significativo toohave corto o largo, o demasiado frecuente o demasiado frecuente. En este tutorial, se excluyen los n-gramas que aparecen en menos de 5 registros o en más del 80 % de los registros.

Además, puede utilizar la característica selección tooselect solo aquellas características que son más Hola correlacionadas con el destino de la predicción. Utilizamos tooselect 1000 características de selección de características chi cuadrado. Puede ver vocabulario Hola de palabras seleccionadas o N gramos haciendo clic en la salida de hello derecho del módulo de extracción N gramos.

Como un enfoque alternativo se toousing extraer características de N-gramas, puede usar el módulo hash de características. Tenga en cuenta que el módulo de [hash de características](https://msdn.microsoft.com/library/azure/dn906018.aspx) no tiene funcionalidades de selección de características de compilación ni ponderación TF*IDF.

## <a name="step-3-train-classification-or-regression-model"></a>Paso 3: Entrenar un modelo de clasificación o regresión
Ahora el texto hello ha sido transformado toonumeric columnas de característica. conjunto de datos de Hello todavía contiene columnas de cadena de fases anteriores, por lo que usamos seleccionar columnas de conjunto de datos tooexclude ellos.

A continuación, utilizamos [regresión logística de dos clases](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict nuestro objetivo: puntuación de revisión alta o baja. En este momento, problema de análisis de texto hello se ha convertido en un problema de clasificación normales. Puede usar herramientas de hello disponibles en el modelo de aprendizaje automático de Azure tooimprove Hola. Por ejemplo, puede experimentar con distintos clasificadores toofind los resultados de grado de precisión que dé o usar hyperparameter tooimprove precisión de hello para la optimización.

![Entrenar y puntuar](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>Paso 4: Puntuación y validar el modelo de Hola
¿Cómo se validará entrenado Hola? Hemos puntuar en conjunto de datos de prueba de Hola y evaluar la precisión de Hola. Sin embargo, el modelo de Hola había aprendido vocabulario Hola de n-gramas y sus pesos de conjunto de datos de entrenamiento de Hola. Por lo tanto, debemos usar ese vocabulario y los pesos al extraer las características de datos de prueba, como opone vocabulario de hello toocreating como nueva. Por lo tanto, se agrega extraer características de N-gramas módulo toohello puntuación rama del experimento de hello, conectar vocabulario de salida de hello de bifurcación de entrenamiento y establecer el modo de vocabulario de hello solo tooread. También deshabilitar el filtrado de Hola de n-gramas por frecuencia por configuración de instancia de too1 mínima de Hola y too100 máximo % y desactivar la selección de características de Hola.

Después de hello columna de texto de la prueba de datos ha sido transformado toonumeric columnas de característica, excluimos cadena hello como columnas de fases anteriores de bifurcación de entrenamiento. A continuación, usamos predicciones de toomake de módulo de modelo de puntuación y la precisión de Hola de evaluar modelo módulo tooevaluate.

## <a name="step-5-deploy-hello-model-tooproduction"></a>Paso 5: Implementar Hola modelo tooproduction
modelo de Hello está casi listo toobe implementa tooproduction. Cuando se implementa como servicio web, toma la cadena de texto de forma libre como entrada y devuelve una predicción de puntuación "alta" o "baja". Usa Hola aprendido n-gramas vocabulario tootransform Hola texto toofeatures y entrenar el modelo de regresión logística toomake una predicción de esas características. 

tooset seguridad experimento predictivo hello, se guarda primero vocabulario de n-gramas hello como conjunto de datos, y Hola entrena el modelo de regresión logística de bifurcación de entrenamiento de hello del experimento de Hola. A continuación, guardamos experimento de hello mediante "Guardar como" toocreate un gráfico de experimento para predicción experimento. Quitamos el módulo de dividir datos de Hola y bifurcación de entrenamiento de Hola de experimento Hola. A continuación, conectamos Hola guardado previamente n-gramas vocabulario y modelo tooExtract N-gramas características y módulos de modelo de puntuación, respectivamente. También Quitamos el módulo de evaluar modelo Hola.

Se seleccione columnas de inserción en el módulo de conjunto de datos antes de la columna de etiqueta de texto de preprocesamiento módulo tooremove hello y anule la selección de opción de "Toodataset de columna de puntuación de anexar" en el módulo de puntuación. De este modo, servicio web de hello no solicita etiqueta de Hola que está tratando de toopredict y no de eco características de entrada de Hola en respuesta.

![Experimento predictivo](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Ahora tenemos un experimento que se puede publicar como servicio web y al que se puede llamar mediante las API de request-response (solicitud-respuesta) o batch excution (ejecución por lotes).

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de los módulos de análisis de texto mediante la [documentación de MSDN](https://msdn.microsoft.com/library/azure/dn905886.aspx).

