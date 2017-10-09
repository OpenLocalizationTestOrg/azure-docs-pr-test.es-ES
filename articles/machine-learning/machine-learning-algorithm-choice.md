---
title: "algoritmos de aprendizaje automático de toochoose de aaaHow | Documentos de Microsoft"
description: "¿Cómo toochoose aprendizaje algoritmos de aprendizaje supervisado y de agrupación en clústeres, clasificación o regresión experimentos."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>¿Cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure
Hola responder toohello pregunta "¿qué máquina algoritmo de aprendizaje debo usar?" siempre es "Depende". Depende en tamaño hello, la calidad y la naturaleza de los datos de Hola. Depende de lo que desee toodo con respuesta Hola. Depende de cómo se traducen matemáticas Hola del algoritmo de hello en las instrucciones de equipo de Hola que está utilizando. Y también depende del tiempo de que disponga. Incluso los científicos de datos más experimentado de hello no pueden determinar qué algoritmo llevará a cabo mejor antes de intentar ellos.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>Hola hoja de referencia rápida de algoritmo de aprendizaje de máquina
Hola **Microsoft Azure Machine Learning algoritmo referencia rápida hoja** le ayuda a elegir derecha Hola máquina algoritmo de aprendizaje para las soluciones de análisis predictivos de biblioteca de aprendizaje automático de Microsoft Azure Hola de algoritmos.
En este artículo se explica cómo toouse lo.

> [!NOTE]
> hoja de referencia de toodownload hello y siga a lo largo de este artículo, vaya demasiado[máquina hoja de referencia de algoritmo de aprendizaje para estudio de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-cheat-sheet.md).
> 
> 

Esta hoja de referencia tiene una audiencia concreta muy en cuenta: principio científico de datos con aprendizaje automático de nivel superiores, intentar toochoose un toostart algoritmo con en estudio de aprendizaje automático de Azure. Eso significa que en ella se hacen algunas generalizaciones y simplificaciones exageradas, pero le sirve para orientarse bien. También significa que hay muchos algoritmos que no están incluidos aquí. A medida que aprendizaje automático de Azure aumenta tooencompass un conjunto más completo de métodos disponibles, vamos a agregar.

Estas recomendaciones son una recopilación de los comentarios y las sugerencias de muchos científicos de datos y expertos en aprendizaje automático. Se no coincidir con todo, pero he probado tooharmonize nuestra opinión en un consenso aproximado. La mayoría de las instrucciones de Hola de desacuerdo comienzan por "Depende..."

### <a name="how-toouse-hello-cheat-sheet"></a>La hoja de referencia toouse Hola rápida
Leer las etiquetas de ruta de acceso y el algoritmo de Hola de gráfico de hello como "para  *&lt;etiqueta de la ruta de acceso&gt;*, use  *&lt;algoritmo&gt;*." Por ejemplo, "Para *velocidad*, use la *regresión logística de dos clases*". Ciertas veces, se aplica más de una rama.
Otras, ninguna de ellas es la ideal. Está previsto toobe de regla recomendaciones, por lo que no se preocupe que sea exacto.
Varios científicos de datos describe con dice que solo seguro hasta encontrar el mejor algoritmo de hello es tootry Hola todas ellas.

Este es un ejemplo de Hola [Galería de inteligencia de Cortana](http://gallery.cortanaintelligence.com/) de un experimento que intente varios algoritmos contra Hola mismos datos y compara Hola resultados: [comparación de clasificadores multiclase: reconocimiento de letra ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> toodownload e imprimir un diagrama que ofrezca una visión general de las capacidades de Hola de estudio de aprendizaje automático, consulte [diagrama de información general de las capacidades de estudio de aprendizaje automático de Azure](machine-learning-studio-overview-diagram.md).
> 
> 

## <a name="flavors-of-machine-learning"></a>Variantes del aprendizaje automático
### <a name="supervised"></a>Supervisado
Los algoritmos de aprendizaje supervisado hacen predicciones basadas en un conjunto de ejemplos. Por ejemplo, cotizaciones históricos pueden ser estimaciones toohazard usados en los precios de futuras. Cada ejemplo que se usa para el entrenamiento se etiqueta con el valor de Hola de interés: en este caso Hola precio de las acciones. Un algoritmo de aprendizaje supervisado busca patrones en esas etiquetas de valor. Puede usar cualquier información que podría ser pertinente: día de Hola de semana de hello, temporada de hello, datos financieros de la compañía de hello, tipo hello del sector, presencia de Hola de acontecimientos geopolíticos interrumpen el funcionamiento, y cada algoritmo examina para diferentes tipos de patrones. Una vez que el algoritmo de hello encuentra patrón mejor Hola puede, usa que las predicciones de toomake de patrón de sin etiqueta de datos de prueba, los precios de mañana.

El aprendizaje supervisado es un tipo conocido y útil de aprendizaje automático. Con una excepción, todos los módulos de hello en el aprendizaje automático de Azure supervisados algoritmos de aprendizaje. Hay varios tipos específicos de aprendizaje supervisado representados en Aprendizaje automático de Azure: la clasificación, la regresión y la detección de anomalías.

* **Clasificación**. Cuando los datos de Hola se toopredict usa una categoría, aprendizaje supervisado también se denomina clasificación. Este es el caso de hello al asignar una imagen como una imagen de un 'cat' o "dog". Cuando hay solo dos opciones, se denomina clasificación **de dos clases** o **binomial**. Cuando hay más categorías, como cuando se predicen ganador Hola de torneo de NCAA marzo Madness hello, este problema se conoce como **clasificación multiclase**.
* **Regresión**. Cuando se predice un valor, como el precio de las acciones, el aprendizaje supervisado se denomina regresión.
* **Detección de anomalías**. A veces hello objetivo es tooidentify puntos de datos que no son simplemente habituales. En la detección de fraudes, por ejemplo, los patrones de gasto de tarjeta de crédito muy poco habituales son sospechosos. las posibles variaciones de Hello son tan numerosas y Hola ejemplos de entrenamiento tan pocos, que es no es posible toolearn aspecto qué actividades fraudulentas. El enfoque que toma la detección de anomalías es toosimply Obtenga información acerca de qué actividades normales aspecto (con las transacciones no fraudulentas un historial) e identificar cualquier cosa que es significativamente diferente.

### <a name="unsupervised"></a>Sin supervisar
En el aprendizaje sin supervisar, los puntos de datos no tienen etiquetas asociadas a ellos. En su lugar, el objetivo Hola de un supervisados aprendizaje algoritmo consiste en organizar los datos de Hola de alguna manera o toodescribe su estructura. Esto puede significar agruparlos en clústeres o buscar diferentes maneras de examinar datos complejos para que parezcan más simples o más organizados.

### <a name="reinforcement-learning"></a>Aprendizaje de refuerzo
En el aprendizaje de refuerzo, algoritmo de hello obtiene toochoose una acción de punto de datos de respuesta tooeach. algoritmo de aprendizaje de Hello también recibe una señal de recompensa era un poco más adelante, que indica la calidad decisión Hola.
En función de esto, algoritmo de hello modifica su estrategia de recompensa más alto de orden tooachieve Hola. Actualmente no hay ningún módulo de algoritmo de aprendizaje de refuerzo en Aprendizaje automático de Azure. Aprendizaje de refuerzo es habitual en robótica, donde hello conjunto de lecturas de sensor en un punto en el tiempo es un punto de datos y algoritmo de hello debe elegir la acción siguiente del robot Hola. También resulta perfecto para las aplicaciones de Internet de las cosas.

## <a name="considerations-when-choosing-an-algorithm"></a>Consideraciones al elegir un algoritmo
### <a name="accuracy"></a>Precisión
Obtener respuesta sean más preciso de hello posibles no siempre es necesario.
A veces, una aproximación ya es útil, según para qué se la desee usar. Si ese es el caso de hello, es posible que pueda toocut el tiempo de procesamiento considerablemente por quede con más métodos aproximados. Otra ventaja de los métodos más aproximados es que tienden naturalmente a evitar el [sobreajuste](https://youtu.be/DQWI1kvmwRg).

### <a name="training-time"></a>Tiempo de entrenamiento
Hola número de minutos u horas tootrain es necesario que un modelo de un gran ahorro varía entre los algoritmos. Tiempo de entrenamiento es a menudo estrechamente relacionada con la precisión, uno normalmente acompaña Hola otro. Además, algunos algoritmos son más sensible toohello número de puntos de datos que otras personas.
Cuando se limita el tiempo puede controlar elegir Hola algoritmo, especialmente cuando el conjunto de datos de hello es grande.

### <a name="linearity"></a>Linealidad
Muchos algoritmos de aprendizaje automático hacen uso de la linealidad. Los algoritmos de clasificación lineal suponen que las clases pueden estar separadas mediante una línea recta (o su análogo de mayores dimensiones). Entre ellos, se encuentran la regresión logística y las máquinas de vectores de soporte (como las que se implementan en Aprendizaje automático de Azure).
Los algoritmos de regresión lineal suponen que las tendencias de datos siguen una línea recta. Estas suposiciones no son incorrectas para algunos problemas, pero en otros disminuyen la precisión.

![Límite de clase no lineal][1]

***Límite de clase no lineal****: la dependencia de un algoritmo de clasificación lineal se traduciría en baja precisión*.

![Datos con tendencia no lineal][2]

***Datos con tendencia no lineal****: el uso de un método de regresión lineal generaría errores mucho mayores que los necesarios*

A pesar de los riesgos, los algoritmos lineales son muy populares como primera línea de ataque. Suelen toobe forma algorítmica simple y rápida para entrenar.

### <a name="number-of-parameters"></a>Cantidad de parámetros
Los parámetros son botones de hello científico de datos obtiene tooturn al configurar un algoritmo. Únicamente son números que afectan al comportamiento del algoritmo de hello, como tolerancia a errores o el número de iteraciones u opciones entre las variantes de funcionamiento del algoritmo de Hola. tiempo de entrenamiento de Hola y la precisión del algoritmo de Hola a veces pueden ser muy confidenciales toogetting configuración de derechos de hello solo. Normalmente, los algoritmos con parámetros de grandes cantidades requieren hello más prueba y error toofind una combinación válida.

También puede haber un bloque de módulos de [barrido de parámetros](machine-learning-algorithm-parameters-optimize.md) en Aprendizaje automático de Azure que prueba automáticamente todas las combinaciones de parámetros en cualquier granularidad que se elija. Aunque esto es una excelente manera toomake seguro de que ha ocupa espacio paramétrico de Hola, Hola tiempo necesario tootrain un modelo aumenta exponencialmente con número de Hola de parámetros.

Hello ventaja es que tiene muchos parámetros normalmente indica que un algoritmo tiene mayor flexibilidad. A menudo, puede lograr una precisión muy alta. Proporciona que puede encontrar la combinación correcta de Hola de configuración de parámetros.

### <a name="number-of-features"></a>Cantidad de características
Para determinados tipos de datos, el número de Hola de características puede ser toohello en comparación con un gran número de puntos de datos. Suele ser el caso de hello genetics o datos de texto. gran número de características de Hello puede perjudicar algunos algoritmos de aprendizaje, realizar el entrenamiento unfeasibly largos de tiempo. Máquinas de vectores de soporte técnico son especialmente adecuada toothis caso (ver abajo).

### <a name="special-cases"></a>Casos especiales
Algunos algoritmos de aprendizaje suposiciones determinado sobre estructura Hola de datos de Hola o los resultados de hello deseado. Si encuentra uno que se ajuste a sus necesidades, este puede ofrecerle resultados más útiles, predicciones más precisas o tiempos de entrenamiento más cortos.

| **Algoritmo** | **Precisión** | **Tiempo de entrenamiento** | **Linealidad** | **Parámetros** | **Notas** |
| --- |:---:|:---:|:---:|:---:| --- |
| **Clasificación multiclase** | | | | | |
| [regresión logística](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [bosque de decisión](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [selva de decisión](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |Uso de memoria bajo |
| [árbol de decisión impulsado](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |Uso de memoria grande |
| [red neuronal](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[La personalización adicional es posible](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [perceptrón promedio](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [máquina de vectores de soporte](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |Útil para conjuntos de características de gran tamaño |
| [máquina de vectores de soporte localmente profunda](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |Útil para conjuntos de características de gran tamaño |
| [máquina del punto de Bayes](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **Clasificación multiclase** | | | | | |
| [regresión logística](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [bosque de decisión](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [selva de decisión ](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |Uso de memoria bajo |
| [red neuronal](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[La personalización adicional es posible](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [uno frente a todos](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |Ver propiedades del método de dos clases de hello seleccionado |
| **Regresión** | | | | | |
| [lineal](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [Bayesiano lineal](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [bosque de decisión](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [árbol de decisión impulsado](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |Uso de memoria grande |
| [cuantil de bosque rápido](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |Distribuciones en lugar de predicciones de puntos |
| [red neuronal](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[La personalización adicional es posible](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |Logarítmico lineal técnicamente. Para la predicción de recuentos |
| [ordinal](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |Para la predicción de ordenación de clasificaciones |
| **Detección de anomalías** | | | | | |
| [máquina de vectores de soporte](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |Especialmente útil para conjuntos de características de gran tamaño |
| [Detección de anomalías basada en PCA](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-Means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |Un algoritmo de agrupación en clústeres |

**Propiedades de algoritmo:**

**●** -muestra una precisión excelente, períodos de formación rápida y el uso de Hola de linealidad

**○** : muestra buena precisión y tiempos de entrenamiento moderados

## <a name="algorithm-notes"></a>Notas sobre los algoritmos
### <a name="linear-regression"></a>Regresión lineal
Como se mencionó anteriormente, [regresión lineal](https://msdn.microsoft.com/library/azure/dn905978.aspx) se ajuste a un conjunto de datos de toohello de línea (o plano o hiperplano). Es potente, simple y rápida, pero puede ser demasiado simple para algunos problemas.
Entre aquí para ver un [tutorial sobre regresión lineal](machine-learning-linear-regression-in-azure.md).

![Datos con tendencia lineal][3]

***Datos con tendencia lineal***

### <a name="logistic-regression"></a>Regresión logística
Aunque confusa incluye 'regresión' en nombre de hello, la regresión logística es realmente una herramienta eficaz para [dos clases](https://msdn.microsoft.com/library/azure/dn905994.aspx) y [multiclase](https://msdn.microsoft.com/library/azure/dn905853.aspx) clasificación. Es rápida y sencilla. Hola el hecho de que usa de una '-facilita una opción natural para dividir los datos en grupos de forma curva en lugar de una línea recta. La regresión logística proporciona límites de clase lineal. Por lo tanto, cuando la use, asegúrese de que la aproximación lineal le es útil.

![Datos de la clase tootwo de regresión logística con una sola característica][4]

***Una regresión logística tootwo clases de datos con una sola característica*** *-el límite de la clase es el punto de hello en qué Hola curva logística se cierre simplemente como clases tooboth*

### <a name="trees-forests-and-jungles"></a>Árboles, bosques y selvas
Los bosques de decisión ([regresión](https://msdn.microsoft.com/library/azure/dn905862.aspx), [dos clases](https://msdn.microsoft.com/library/azure/dn906008.aspx) y [multiclase](https://msdn.microsoft.com/library/azure/dn906015.aspx)), las selvas de decisión ([dos clases](https://msdn.microsoft.com/library/azure/dn905976.aspx) y [multiclase](https://msdn.microsoft.com/library/azure/dn905963.aspx)) y los árboles de decisión impulsados ([regresión](https://msdn.microsoft.com/library/azure/dn905801.aspx) y [dos clases](https://msdn.microsoft.com/library/azure/dn906025.aspx)) se basan en árboles de decisión, un concepto fundamental del aprendizaje automático. Hay muchas variantes de árboles de decisión, pero todas ellas hacen lo mismo: subdivide espacio de características de hello en regiones con principalmente hello misma etiqueta. Estas pueden ser regiones de la misma categoría o de un valor constante, según si se está realizando una clasificación o una regresión.

![El árbol de decisión subdivide un espacio de características][5]

***Un árbol de decisión subdivide un espacio de características en regiones de valores más o menos uniformes***

Dado que un espacio de características puede dividirse en zonas arbitrariamente pequeñas, es fácil tooimagine dividiéndolo con precisión suficiente toohave un punto de datos por región. Se trata de un ejemplo extremo de sobreajuste. En orden tooavoid esto, un conjunto grande de árboles se construyen con especial cuidado matemático realizado que no están correlacionados árboles Hola. promedio de Hola de "bosque de decisión" es un árbol que evita el sobreajuste. Los bosques de decisión pueden llegar a usar demasiada memoria. Las selvas de decisión son una variante que consume menos memoria en gastos de Hola de ligeramente más tiempo de entrenamiento.

Los árboles de decisión impulsados evitan el sobreajuste al limitar la cantidad de veces que pueden subdividir y la cantidad de puntos de datos que se permiten en cada región. El algoritmo genera una secuencia de árboles, cada uno de los cuales aprende para compensar el error Hola árbol Hola antes de la izquierda. resultado de Hello es un aprendiz muy preciso que tiende toouse una gran cantidad de memoria. Para la descripción técnica completa de Hola, eche un vistazo [papel original de experiencia](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[El rápido regresión de bosque por cuantiles](https://msdn.microsoft.com/library/azure/dn913093.aspx) es una variación de árboles de decisión para caso especial de Hola donde desea saber no sólo hello (medio) valor típico de datos de hello dentro de una región, sino también su distribución en forma de Hola de cuantiles.

### <a name="neural-networks-and-perceptrons"></a>Redes neuronales y perceptrones
Las redes neuronales son algoritmos de aprendizaje inspirados en el cerebro que abarcan problemas [multiclase](https://msdn.microsoft.com/library/azure/dn906030.aspx), [de dos clases](https://msdn.microsoft.com/library/azure/dn905947.aspx) y [de regresión](https://msdn.microsoft.com/library/azure/dn905924.aspx). Provienen de una variedad infinita, pero las redes neuronales hello en aprendizaje automático de Azure son todas del formato de Hola de gráficos acíclicos dirigidos. Esto significa que las características de entrada se adelantan (nunca se atrasan) en una secuencia de capas antes convertirse en salidas. En cada capa se ponderan entradas en diversas combinaciones, sumada y pasará al siguiente nivel de Hola. Esta combinación de resultados de cálculos sencillos en el toolearn de capacidad de una sofisticada tendencias de los límites y los datos de la clase, aparentemente por arte de magia. Redes de varios niveles de este tipo realizan Hola "aprendizaje profundo" que impulsa tanta tech reporting y ciencia ficción.

Sin embargo, el alto rendimiento no es gratuito. Redes neurales pueden tardar un tootrain mucho tiempo, especialmente para grandes conjuntos de datos con una gran cantidad de características. También tienen más parámetros que la mayoría de los algoritmos, lo que significa que barrido de parámetros expande el tiempo de entrenamiento Hola mucho.
Y para esos overachievers que deseen demasiado[especificar su propia estructura de red](http://go.microsoft.com/fwlink/?LinkId=402867), las posibilidades son inexhaustible.

![Los límites aprendido por redes neurales][6]
***los límites de hello aprendidos por redes neurales pueden ser complejos e irregulares***

Hola [perceptrón promedio de dos clases](https://msdn.microsoft.com/library/azure/dn906036.aspx) es períodos de formación de redes neurales respuesta tooskyrocketing. Este perceptrón usa una estructura de red que proporciona límites de clase lineal. Es casi primitivo por los estándares de hoy en día, pero tiene una larga historia de trabajar con solidez y es lo suficientemente pequeño toolearn rápidamente.

### <a name="svms"></a>SVM
Las máquinas de vector de soporte (SVM) buscar los límites de Hola que separa las clases como todo un margen como sea posible. Cuando no se pueden separar con claridad dos clases de hello, algoritmos de hello encontrar límites recomendados Hola pueden. Hola a medida que se escriben en aprendizaje automático de Azure, [SVM de dos clases](https://msdn.microsoft.com/library/azure/dn905835.aspx) realiza esto con solo una línea recta. (En el idioma de SVM, usa un kernel lineal). Porque hace que esta aproximación lineal, es capaz de toorun con bastante rapidez. Donde realmente se destaca, es con datos de muchas características, como texto o genómica. En estos casos SVM es clases puede tooseparate más rápidamente y con menos el sobreajuste que otros algoritmos, además toorequiring sólo una pequeña cantidad de memoria.

![Límite de clase de máquina de vectores de soporte][7]

***Un límite de clase de máquina de vector de soporte típico maximiza el margen de hello separar dos clases***

Otro producto de Microsoft Research, Hola [SVM de dos clases localmente profunda](https://msdn.microsoft.com/library/azure/dn913070.aspx) es una variante de SVM que mantiene la mayor parte de la eficacia de velocidad y la memoria de Hola de versión lineal hello no lineal. Es ideal para los casos donde enfoque lineal hello no le ofrece respuestas suficientemente precisas. los desarrolladores de Hola mantienen rápido al dividir problema hello en una serie de problemas SVM lineales pequeños. Hola de lectura [completa descripción](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) para obtener detalles de hello sobre cómo saca de este truco.

Utiliza una extensión inteligente de SVM no lineal, Hola [SVM de una clase](https://msdn.microsoft.com/library/azure/dn913103.aspx) dibuja un límite que describe totalmente Hola todo el conjunto de datos. Es útil para la detección de anomalías. Los nuevos puntos de datos que se encuentran ahora fuera de ese límite son lo suficientemente inusual toobe merece la pena comentar.

### <a name="bayesian-methods"></a>Métodos bayesianos
Los métodos bayesianos tienen una calidad muy deseable: evitan el sobreajuste. Para hacerlo con algunas suposiciones con antelación acerca de la distribución probabilidad Hola de respuesta de Hola. Otra característica de este enfoque es que tienen muy pocos parámetros. Azure Machine Learning tiene dos algoritmos bayesianos tanto para la clasificación ([automática de puntos de Bayes de dos clases](https://msdn.microsoft.com/library/azure/dn905930.aspx)) como para la regresión ([regresión lineal bayesiana](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Tenga en cuenta que estos se supone que los datos de Hola se pueden dividir o encaja con una línea recta.

Como nota histórica, se desarrollaron las máquinas de puntos de Bayes en Microsoft Research. Presentan un trabajo teórico excepcional. estudiante interesado Hello es dirigido toohello [artículo original en JMLR](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) y un [detalle blog de Chris Bishop](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx).

### <a name="specialized-algorithms"></a>Algoritmos especializados
Si tiene un objetivo muy específico, puede que sea su día de suerte. Dentro de hello colección de aprendizaje automático de Azure, hay algoritmos que se especializan en:

- predicción de rangos ([regresión ordinal](https://msdn.microsoft.com/library/azure/dn906029.aspx)),
- predicción de totales ([regresión de Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx)),
- detección de anomalías (uno basado en el [análisis de componentes principales](https://msdn.microsoft.com/library/azure/dn913102.aspx) y otro en [máquinas de vectores de soporte](https://msdn.microsoft.com/library/azure/dn913103.aspx))
- agrupación en clústeres ([K-Means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![Detección de anomalías basada en PCA][8]

***Detección de anomalías basado en PCA*** *-gran mayoría de los datos de Hola de hello entra en una distribución stereotypical; puntos que difieran considerablemente de distribución están sospechoso*

![Conjunto de datos agrupados mediante K-Means][9]

***Un conjunto de datos se agrupa en 5 clústeres mediante K-Means***

También hay un conjunto [clasificador multiclase uno v todos](https://msdn.microsoft.com/library/azure/dn905887.aspx), qué problema de clasificación de saltos Hola clase N problemas de clasificación de dos clases de n-1. precisión de Hello, el tiempo de entrenamiento y linealidad propiedades dependen de clasificadores de dos clases de hello usa.

![Clasificadores de dos clases combinan tooform un clasificador tres clases][10]

***Un par de clasificadores de dos clases combinar tooform un clasificador tres clases***

Aprendizaje de automático de Azure también incluye marco de aprendizaje de máquina potente de tooa de acceso en el título de Hola de [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
VW es un reto a la categorización, ya que puede aprender problemas tanto de clasificación como de regresión, e incluso puede aprender a partir de datos parcialmente etiquetados. Se puede configurar toouse cualquiera de una serie de algoritmos, funciones de pérdida y optimización de aprendizaje. Que se diseñó desde Hola masa seguridad toobe eficaz, en paralelo y extremadamente rápida. Administra enormes conjuntos de características con mucha facilidad.
VW, iniciado y liderado por el propio John Langford de Microsoft Research, es una entrada de Fórmula Uno en un campo de algoritmos de coches de línea. No todos los problemas ajusta VW, pero si el suyo tiene, es posible la pena tooclimb la curva de aprendizaje en su interfaz. También está disponible como [código fuente abierto independiente](https://github.com/JohnLangford/vowpal_wabbit) en varios idiomas.

## <a name="more-help-with-algorithms"></a>Más ayuda con los algoritmos
* Para una infografía descargable que describe los algoritmos y proporciona ejemplos, consulte [Infografía descargable: Conceptos básicos de aprendizaje automático con ejemplos de algoritmos](machine-learning-basics-infographic-with-algorithm-examples.md).
* Para obtener una lista por categoría de aprendizaje automático de hello todos los algoritmos disponibles en estudio de aprendizaje automático de Azure, consulte [inicializar modelo] [ initialize-model] en hello Studio algoritmo de aprendizaje de máquina y la Ayuda del módulo.
* Para ver una lista completa de todos los algoritmos de Machine Learning Studio, consulte [A-Z list of Machine Learning Studio modules][a-z-list] (Lista de la A a la Z de módulos de Machine Learning Studio) en la Ayuda de módulos y algoritmos de Machine Learning Studio.
* toodownload e imprimir un diagrama que ofrezca una visión general de las capacidades de Hola de estudio de aprendizaje automático de Azure, consulte [diagrama de información general de las capacidades de estudio de aprendizaje automático de Azure](machine-learning-studio-overview-diagram.md).


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
