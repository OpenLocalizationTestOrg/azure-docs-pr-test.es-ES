---
title: "aaaGuide toohello Red neuronal redes de lenguaje de especificación | Documentos de Microsoft"
description: "Sintaxis de hello Net # neuronal redes de lenguaje de especificación, junto con ejemplos de cómo toocreate una red neuronal personalizada del modelo de aprendizaje automático de Azure de Microsoft con Net #"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Guía de lenguaje de especificación de la red neuronal tooNet # para el aprendizaje automático de Azure
## <a name="overview"></a>Información general
NET # es un lenguaje desarrollado por Microsoft que es usado toodefine arquitecturas de red neuronal. Puede usar Net# en módulos de red neuronal de Microsoft Azure Machine Learning.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

En este artículo, aprenderá los conceptos básicos necesarios toodevelop una red neuronal personalizada: 

* Requisitos de red neuronal y cómo toodefine Hola componentes principales
* sintaxis de Hola y palabras clave del lenguaje de especificación de Net # Hola
* Ejemplos de redes neuronales personalizadas creadas mediante Net# 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>Conceptos básicos sobre redes neuronales
Formada por una estructura de red neuronal ***nodos*** que se organizan en ***capas***y ponderadas ***conexiones*** (o ***bordes***) entre nodos de Hola. conexiones de Hello son direccionales, y cada conexión tiene un ***origen*** nodo y un ***destino*** nodo.  

Cada una de las ***capas entrenables*** (una capa oculta o de salida) tiene uno o varios ***conjuntos de conexiones***. Una agrupación de conexiones está formada por una capa de origen y una especificación de las conexiones de Hola desde esa capa de origen. Todas las conexiones de hello en un recurso compartido de paquete determinada Hola mismo ***capa de origen*** y Hola mismo ***capa de destino***. En Net #, una agrupación de conexiones se considera como capa de destino del paquete toohello que pertenecen.  

NET # admite distintos tipos de paquetes de conexión, que le permite personalizar la forma hello las entradas son asignadas toohidden capas y salidas de toohello asignado.   

predeterminado de Hola o agrupación estándar es un **agrupación completa**, en el que cada nodo de hello capa de origen es nodo de tooevery conectado en la capa de destino de Hola.  

Además, Net # admite Hola después de cuatro tipos de agrupaciones avanzadas de conexión:  

* **Conjuntos filtrados**. usuario de Hello puede definir un predicado mediante ubicaciones Hola de nodo de nivel de origen de Hola y el nodo de nivel de destino de Hola. Los nodos están conectados siempre predicado hello es True.
* **Conjuntos convolucionales**. usuario de Hello puede definir grupos pequeños de nodos en la capa de origen de Hola. Cada nodo en la capa de destino de hello es conectado tooone entorno de nodos de nivel de origen de Hola.
* **Conjuntos de agrupación** y **conjuntos de normalización de respuesta**. Se trata de agrupaciones de tooconvolutional similar en ese Hola usuario define grupos pequeños de nodos de nivel de origen de Hola. diferencia de Hello es que pesos Hola de bordes de hello en estos paquetes no son trainable. En su lugar, se aplica una función predefinida nodo de origen toohello valores del valor de nodo de destino de toodetermine Hola.  

Con Net # toodefine Hola estructura de una red neuronal hace posible toodefine estructuras complejas, como redes neurales profundas o convoluciones de dimensiones arbitrarias, que se conocen el aprendizaje de tooimprove de datos, como imágenes, audio o vídeo.  

## <a name="supported-customizations"></a>Personalizaciones compatibles
arquitectura de Hola de modelos de red neuronal que cree en aprendizaje automático de Azure se puede personalizar ampliamente mediante Net #. Puede:  

* Cree niveles ocultos y control hello número de nodos en cada capa.
* Especifique cómo los niveles están toobe conectado tooeach otros.
* Definir estructuras de conectividad especial como convoluciones y conjuntos ponderados de uso compartido.
* Especificar diferentes funciones de activación.  

Para obtener detalles de la sintaxis del lenguaje de especificación de hello, consulte [especificación de la estructura](#Structure-specifications).  

Para obtener ejemplos de definir redes neurales para algunas tareas, desde toocomplex símplex, de aprendizaje de automático comunes vea [ejemplos](#Examples-of-Net#-usage).  

## <a name="general-requirements"></a>Requisitos generales
* Debe haber exactamente una capa de salida, al menos una capa de entrada y ninguna o varias capas ocultas. 
* Cada capa tiene un número fijo de nodos, ordenados conceptualmente en una matriz rectangular de dimensiones arbitrarias. 
* Capas entradas no tienen asociados entrenados parámetros y representan punto Hola donde los datos de instancia entra en la red de Hola. 
* Trainable capas (Hola niveles ocultos y salidas) tienen asociados parámetros entrenados, que se conocen como pesos e inclinaciones. 
* los nodos de origen y destino de Hello deben estar en capas independientes. 
* Las conexiones deben ser acíclicas; en otras palabras, no puede ser una cadena de conexiones iniciales toohello back-nodo de origen inicial.
* nivel de salida de Hello no puede ser una capa de origen de una agrupación de conexiones.  

## <a name="structure-specifications"></a>Especificación de estructura
Una especificación de la estructura de red neuronal se compone de tres secciones: Hola **declaración de constante**, hello **capas declaración**, hello **declaración de conexión**. También hay una sección de **declaración de uso compartido** opcional. secciones de Hello pueden especificarse en cualquier orden.  

## <a name="constant-declaration"></a>Declaración constante
Una declaración de constante es opcional. Proporciona un medio toodefine valores utilizados en otra parte en la definición de red neuronal de Hola. instrucción de declaración de Hello consta de un identificador seguido por un signo igual y una expresión de valor.   

Por ejemplo, hello sigue instrucción define una constante **x**:  

    Const X = 28;  

toodefine dos o más constantes simultáneamente, incluya los nombres de identificador hello y los valores entre llaves y sepárelas con punto y coma. Por ejemplo:  

    Const { X = 28; Y = 4; }  

lado derecho de Hola de cada expresión de asignación puede ser un entero, un número real, un valor booleano (True o False) o una expresión matemática. Por ejemplo:  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>Declaración de capas
se requiere la declaración de la capa de Hola. Define el tamaño de Hola y el origen de capa de hello, incluidas sus agrupaciones de conexión y los atributos. Hola empieza de instrucción de declaración con nombre de Hola de capa de hello (de entrada, oculto o de salida), a continuación, las dimensiones de Hola de capa de hello (una tupla de números enteros positivos). Por ejemplo:  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* producto de Hola de dimensiones de hello es número Hola de nodos de nivel de Hola. En este ejemplo, hay dos dimensiones [5,20], lo que significa que hay 100 nodos de capa de Hola.
* las capas de Hola se pueden declarar en cualquier orden, con una excepción: si se define más de un nivel de entrada, Hola orden en que se declaran debe coincidir con hello de características de los datos de entrada de Hola.  

toospecify que el número de nodos en una capa de hello ser determina automáticamente, use hello **automática** palabra clave. Hola **automática** palabra clave tiene efectos diferentes, dependiendo del nivel de hello:  

* En una declaración de nivel de entrada, el número de Hola de nodos es número Hola de características de los datos de entrada de Hola.
* En una declaración de nivel oculto, número de Hola de nodos es número Hola especificado por el valor del parámetro hello para **número de nodos ocultos**. 
* En una declaración de nivel de salida, número de Hola de nodos es 2 para la clasificación de dos clases, 1 de regresión y toohello igual número de nodos de salida para la clasificación multiclase.   

Por ejemplo, hello siguiente definición de red permite Hola tamaño de todos los toobe capas determina automáticamente:  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


Una declaración de capa de una capa trainable (Hola niveles ocultos o de salida) puede incluir opcionalmente la función de salida de hello (también denominada una función de activación), cuyo valor predeterminado es demasiado**sigmoidea** para los modelos de clasificación y **lineal** para los modelos de regresión. (Incluso si utiliza Hola predeterminado, se debe indicar explícitamente función de activación de hello, si lo desea para mayor claridad.)

Hello salida funciones siguientes se admiten:  

* sigmoid
* linear
* softmax
* rlinear
* square
* sqrt
* srlinear
* abs
* tanh 
* brlinear  

Por ejemplo, hello siguiente declaración usa hello **softmax** función:  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>Declaración de conexiones
Inmediatamente después de definir capa trainable hello, debe declarar las conexiones entre las capas de Hola que ha definido. declaración de agrupación de conexiones de Hello comienza con la palabra clave de hello **de**, seguido del nombre de Hola de los tipo de hello y capa de origen de agrupación de Hola de toocreate de agrupación de conexiones.   

Actualmente se admiten cinco tipos de conjuntos de conexiones:  

* **Completa** agrupaciones, indicados por la palabra clave de hello **todos**
* **Filtrar** agrupaciones, indicados por la palabra clave de hello **donde**, seguido de una expresión de predicado
* **Convolutional** agrupaciones, indicados por la palabra clave de hello **convolve**, seguido de los atributos de circunvolución Hola
* **Agrupación de** agrupaciones, indicados por palabras clave de hello **max pool** o **significa grupo**
* **Normalización de respuesta** agrupaciones, indicados por la palabra clave de hello **norma de respuesta**      

## <a name="full-bundles"></a>Conjuntos completos
Un paquete de conexión completa incluye una conexión de cada nodo en nodo de tooeach de nivel de origen de hello en la capa de destino de Hola. Se trata de un tipo de conexión de red de hello predeterminado.  

## <a name="filtered-bundles"></a>Conjuntos filtrados
Una especificación de conjunto de conexiones filtrado incluye un predicado, expresado sintácticamente de manera muy similar a una expresión lambda de C#. Hello en el ejemplo siguiente se define dos paquetes de filtrado:  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* En el predicado de Hola para *ByRow*, **s** es un parámetro que representa un índice en una matriz rectangular de Hola de nodos de nivel de entrada de hello, *píxeles*, y **d.**  es un parámetro que representa un índice en una matriz de Hola de nodos del nivel oculto de hello, *ByRow*. Hola tipo de ambos **s** y **d.** es una tupla de enteros de longitud de dos. Conceptualmente, **s** intervalos sobre todos los pares de enteros con *0 <= s[0] < 10* y *0 <= s[1] < 20* y **d** intervalos de todos los pares de enteros con *0 <= d[0] < 10* y *0 <= d[1] < 12*. 
* En el lado derecho de Hola de expresión de predicado de hello, hay una condición. En este ejemplo, para cada valor de **s** y **d.** esa condición hello es True, hay un borde Hola capa nodo toohello destino capa del nodo de origen. Por lo tanto, esta expresión de filtro indica ese paquete Hola incluye una conexión desde el nodo de hello definido por **s** definido por el nodo de toohello **d.** en todos los casos donde s [0] es igual tood [0].  

También tiene la posibilidad de especificar un conjunto de ponderaciones para un conjunto filtrado. Hola valor para hello **pesos** atributo debe ser una tupla de los valores de punto con una longitud que coincida con el número de Hola de conexiones definidos por la agrupación de Hola flotante. De manera predeterminada, las ponderaciones se generan de manera aleatoria.  

Los valores de peso se agrupan por su índice de nodo de destino de Hola. Es decir, si está conectado el primer nodo de destino Hola tardó nodos de origen, Hola primero *K* elementos de hello **pesos** tupla son pesos de hello para el nodo de destino primera hello, en el orden de índice de origen. Hola que mismo se aplica a Hola restantes nodos de destino.  

Es posible toospecify pesos directamente como valores constantes. Por ejemplo, si ha aprendido pesos Hola anteriormente, puede especificarlos como constantes con esta sintaxis:

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>Conjuntos convolucionales
Cuando los datos de entrenamiento de hello tienen una estructura homogénea, conexiones convolutional son características de alto nivel de uso frecuente toolearn de datos de Hola. Por ejemplo, en datos de imagen, audio o vídeo, la dimensionalidad espacial o temporal puede ser bastante homogénea.  

Agrupaciones de convolutional emplean rectangular **kernels** que son Deslizar las dimensiones de Hola. Básicamente, cada núcleo define un conjunto de pesos que se aplican en los grupos locales, que se hace referencia tooas **aplicaciones de kernel**. Cada aplicación de kernel corresponde tooa nodo en la capa de origen de hello, que es lo que se conoce tooas hello **nodo central**. pesos de Hola de un núcleo se comparten entre muchas conexiones. En un paquete convolutional, cada núcleo es rectangular y todas las aplicaciones de kernel son Hola mismo tamaño.  

Hola de soporte técnico de agrupaciones convolutional siguientes atributos:

**InputShape** define la dimensionalidad de Hola de capa de origen de Hola para fines de Hola de este paquete convolutional. valor de Hello debe ser una tupla de números enteros positivos. producto de Hola de enteros de hello debe ser igual a número Hola de nodos de nivel de origen de hello, pero en caso contrario, no es necesario dimensionalidad de hello toomatch declarado para el nivel del origen de Hola. longitud de Hola de esta tupla se convierte en hello **aridad** valor para agrupación convolutional Hola. (Normalmente aridad hace referencia toohello número de argumentos o los operandos que puede llevar a cabo una función.)  

forma de hello toodefine y ubicaciones de los kernels de hello, utilice atributos de hello **KernelShape**, **Stride**, **relleno**, **LowerPad**, y **UpperPad**:   

* **KernelShape**: dimensionalidad de hello define (obligatorio) de cada núcleo para agrupación convolutional Hola. valor de Hello debe ser una tupla de enteros positivos con una longitud igual a aridad Hola de agrupación de Hola. Cada componente de este tupla debe ser no mayor que el componente correspondiente de Hola de **InputShape**. 
* **STRIDE**: (opcional) Hola define deslizante tamaños de paso de circunvolución hello (tamaño de un paso para cada dimensión), que es la distancia de hello entre nodos central Hola. valor de Hello debe ser una tupla de enteros positivos con una longitud de aridad Hola de agrupación de Hola. Cada componente de este tupla debe ser no mayor que el componente correspondiente de Hola de **KernelShape**. valor predeterminado de Hello es una tupla con tooone igual de todos los componentes. 
* **Uso compartido**: (opcional) peso de hello define para cada dimensión de circunvolución Hola de uso compartido. Hola valor puede ser una tupla de valores booleanos con una longitud de aridad Hola de agrupación de Hola o de un solo valor booleano. Un solo valor booleano es extendido toobe una tupla de longitud correcta de Hola a todos los componentes toohello igual valor especificado. valor predeterminado de Hello es una tupla que consta de todos los valores True. 
* **MapCount**: (opcional) número de hello define la desviación de la característica de mapas de agrupación convolutional Hola. Hola valor puede ser un número entero positivo o una tupla de enteros positivos con una longitud de aridad Hola de agrupación de Hola. Un valor entero único se ha ampliado toobe una tupla de longitud correcta de hello con hello primera componentes igual toohello especifica el valor y todos Hola restantes tooone igual de componentes. valor predeterminado de Hello es uno. número total de Hola de asignaciones de función es producto Hola de componentes de Hola de tupla Hola. Hola factorización de este número total en componentes de hello determina cómo se agrupan los valores de asignación de características de hello en nodos de destino de Hola. 
* **Pesos**: (opcional) define Hola inicial los pesos para agrupación Hola. valor de Hello debe ser una tupla de los valores de punto con una longitud Hola número de núcleos veces Hola pesos por núcleo, tal como se define más adelante en este artículo flotante. pesos de Hello predeterminado se generan de forma aleatoria.  

Hay dos conjuntos de propiedades que controlan el relleno, propiedades de hello son mutuamente excluyentes:

* **Relleno**: (opcional) determina si Hola de entrada se debe controlar mediante el uso de un **esquema de relleno predeterminado**. valor de Hello puede ser un solo valor booleano, o puede ser una tupla de valores booleanos con una longitud de aridad Hola de agrupación de Hola. Un solo valor booleano es extendido toobe una tupla de longitud correcta de Hola a todos los componentes toohello igual valor especificado. Si el valor de Hola para una dimensión es True, origen Hola lógicamente se rellena en esa dimensión con aplicaciones de kernel adicional de toosupport celdas con valor cero, tal que Hola central nodos de kernels primeros y últimos de hello en esa dimensión son Hola primero y último en la dimensión en la capa de origen de Hola. Por lo tanto, número de Hola de nodos "ficticios" en cada dimensión es determina automáticamente, toofit exactamente *(InputShape [d] - 1) / Stride [d] + 1* kernels en la capa de origen de hello rellenado. Si el valor de Hola para una dimensión es False, Hola kernels se definen para que sea el número de Hola de nodos en cada lado que se dejan fuera igual Hola (arriba tooa diferencia de 1). valor predeterminado de Hola de este atributo es una tupla con tooFalse igual de todos los componentes.
* **UpperPad** y **LowerPad**: (opcional) proporcionar mayor control sobre la cantidad de Hola de toouse de relleno. **Importante:** estos atributos se pueden definir si y solo si hello **relleno** propiedad anterior es ***no*** definido. valores de Hello deberían tuplas con valor entero con longitudes de aridad Hola de agrupación de Hola. Cuando se especifican estos atributos, se agregan nodos "ficticios" toohello inferior y extremos superiores de cada dimensión del programa Hola a nivel de entrada. número de nodos Hello agregado toohello inferior y superior termina en cada dimensión viene determinado por **LowerPad**[i] y **UpperPad**[i] respectivamente. debe cumplirse tooensure que kernels corresponden nodos solo demasiado "reales" y no demasiado de "ficticio", hello condiciones siguientes:
  * Cada componente de **LowerPad** debe ser estrictamente inferior a KernelShape[d]/2. 
  * Ningún componente de **UpperPad** puede ser superior a KernelShape[d]/2. 
  * valor predeterminado de Hola de estos atributos es una tupla con too0 igual de todos los componentes. 

configuración de Hello **relleno** = true, se permiten como el relleno sea necesario tookeep Hola "center" del kernel de hello dentro de Hola "real" de entrada. Esto cambia matemáticas Hola un poco para calcular el tamaño de la salida de hello. Por lo general, el tamaño de la salida de hello *d.* se calcula como *d. = (I - K) / S + 1*, donde *I* tamaño de entrada de hello, *K* tamaño de kernel hello, *S* es stride hello, y  */*  es la división de enteros (redondear hacia cero). Si establece UpperPad = [1, 1], tamaño de la entrada de hello *I* es efectivamente 29 y, por tanto, *d. = (29-5) / 2 + 1 = 13*. Sin embargo, cuando **Padding** = true, esencialmente *I* aumenta en *K - 1*; por lo tanto, *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*. Al especificar valores para **UpperPad** y **LowerPad** obtener un mayor control sobre Hola relleno que if acabas de configurar **relleno** = true.

Para obtener más información acerca de las redes convolucionales y sus aplicaciones, consulte estos artículos:  

* [http://deeplearning.net/tutorial/lenet.html ](http://deeplearning.net/tutorial/lenet.html)
* [http://research.microsoft.com/pubs/68920/icdar03.pdf](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>Conjuntos de agrupación
A **agrupación agrupación** aplica conectividad tooconvolutional similar de geometría, pero usa funciones predefinidas toosource nodo valores tooderive Hola nodo valor de destino. Por tanto, los conjuntos de agrupación no tienen estado entrenable (ponderaciones o sesgos). Agrupación de soporte técnico de agrupaciones Hola a todos los atributos convolutional excepto **compartir**, **MapCount**, y **pesos**.  

Por lo general, no se superponen los kernels de hello resumidos por unidades de agrupación adyacentes. Si Stride [d] es igual tooKernelShape [d] en cada dimensión, nivel de hello obtenido es Hola tradicional local agrupación capa, que normalmente se emplea en redes neurales convolutional. Cada nodo de destino calcula Hola máximo o promedio de Hola de actividades de Hola de su kernel en la capa de origen de Hola.  

Hola de ejemplo siguiente muestra un paquete de agrupación: 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* Hola aridad de agrupación de hello es 3 (Hola longitud de tuplas de hello **InputShape**, **KernelShape**, y **Stride**). 
* Hola número de nodos de nivel de origen de hello es *5 * 24 * 24 = 2880*. 
* Esto es un nivel de agrupación local tradicional porque **KernelShape** y **Stride** son iguales. 
* Hola número de nodos de nivel de destino de hello es *5 * 12 * 12 = 1440*.  

Para obtener más información acerca de las capas de agrupación, consulte estos artículos:  

* [http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Sección 3.4)
* [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>Conjuntos de normalización de respuesta
**Normalización de respuesta** es un esquema de normalización local que apareció por primera vez por Geoffrey Hinton, et al., en papel de hello [ImageNet Classiﬁcation con profundidad redes neurales Convolutional](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf). Normalización de respuesta es generalización tooaid usado en las redes neurales. Cuando se genera una neurona en un nivel muy alto de activación, una capa de normalización de respuesta local suprime el nivel de activación de Hola de Hola que rodean las neuronas. Esto se realiza mediante tres parámetros (***α***, ***β*** y ***k***) y una estructura convolutional (o forma de entorno). Cada neurona de capa de destino de hello ***y*** corresponde tooa neurona ***x*** en la capa de origen de Hola. Hola a nivel de activación de ***y*** viene dado por hello después de la fórmula, donde ***f*** es Hola de nivel de activación de una neurona y ***Nx*** es kernel hello (o conjunto de Hola que contiene Hola neuronas en el entorno de Hola de ***x***), tal como se define por hello siguiendo convolutional estructura:  

![][1]  

Agrupaciones de normalización de respuesta compatible con todos los atributos de hello convolutional excepto **compartir**, **MapCount**, y **pesos**.  

* Si kernel hello contiene neuronas de hello mismo asignar como ***x***, esquema de normalización de hello es que se hace referencia tooas **mismo mapa normalización**. toodefine mismo mapa normalización, primera coordenada de hello en **InputShape** debe tener el valor de hello 1.
* Si el núcleo de hello contiene neuronas de Hola misma posición espacial que ***x***, pero neuronas Hola están en otros mapas, se denomina esquema de normalización de hello **asigna a través de normalización**. Este tipo de normalización de respuesta implementa un formulario de inhibición lateral inspirado en hello encontró un tipo de neuronas reales, crear la competición por los niveles de activación grande entre salidas neurona calculadas en diferentes asignaciones. toodefine a través de normalización asigna, primera coordenada de hello debe ser un entero mayor que uno y no mayor que el número de Hola de mapas y, rest Hola de coordenadas de hello debe tener el valor de hello 1.  

Dado que los paquetes de normalización de respuesta aplican un valor de nodo función predefinida toosource nodo valores toodetermine Hola destino, no tienen ningún estado trainable (pesos o inclinaciones).   

**Alerta**: nodos de hello en la capa de destino de hello corresponden tooneurons que son nodos central Hola kernels Hola. Por ejemplo, si KernelShape [d] es impar, a continuación, *KernelShape [d] / 2* corresponde toohello nodo de kernel central. Si *KernelShape [d]* es par, es el nodo central hello en *KernelShape [d] / 2-1*. Por lo tanto, si **relleno**[d] es False, Hola primero y último Hola *KernelShape [d] / 2* nodos no tienen nodos correspondientes en la capa de destino de Hola. tooavoid esta situación, definir **relleno** como [es true, true,..., true].  

Además toohello cuatro atributos describen anteriormente, agrupaciones de normalización de respuesta también Hola de compatibilidad siguientes atributos:  

* **Alfa**: (obligatorio) especifica un valor de punto flotante que corresponde demasiado***α*** en la fórmula anterior Hola. 
* **Beta**: (obligatorio) especifica un valor de punto flotante que corresponde demasiado***β*** en la fórmula anterior Hola. 
* **Desplazamiento**: (opcional) especifica un valor de punto flotante que corresponde demasiado***k*** en la fórmula anterior Hola. El valor predeterminado es too1.  

Hello en el ejemplo siguiente se define una agrupación de normalización de respuesta con estos atributos:  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* capa de origen de Hello incluye cinco asignaciones, cada uno con la dimensión de aof de 12 x 12, calcular los totales en nodos de 1440. 
* Hola valo **KernelShape** indica que se trata de una misma capa de normalización de mapa, donde el entorno de hello es un rectángulo de 3 x 3. 
* Hola valor predeterminado de **relleno** es False, lo que capa de destino de hello tiene solo 10 nodos en cada dimensión. tooinclude un nodo de capa de destino de hello correspondiente nodo tooevery en la capa de origen de hello, agregar relleno = [true, true, true]; y cambiar el tamaño de Hola de RN1 demasiado [5, 12, 12].  

## <a name="share-declaration"></a>Declaración de uso compartido
Net# admite opcionalmente la definición de varios conjuntos con ponderaciones compartidas. pesos de Hola de los dos paquetes pueden compartirse Si sus estructuras son Hola igual. Hola sintaxis define agrupaciones con pesos compartidos:  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

Por ejemplo, hello siguiente declaración de recurso compartido especifica nombres de las capas hello, que indica que se deben compartir pesos e inclinaciones:  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* características de entrada de Hola se dividen en dos niveles de entrada con tamaño iguales. 
* capas de Hello ocultado, a continuación, calculan las características de nivel superior en dos niveles de entrada Hola. 
* declaración de recurso compartido de Hello especifica que *H1* y *H2* debe calcularse en hello igual de sus respectivas entradas.  

Es posible también especificarlo con dos declaraciones de uso compartido independientes, del modo siguiente:  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

Puede usar la forma abreviada de hello cuando las capas de hello contienen un único lote. En general, es posible compartir sólo cuando la estructura relevante hello es idéntica, lo que significa que tienen Hola mismo tamaño, misma geometría convolutional y así sucesivamente.  

## <a name="examples-of-net-usage"></a>Ejemplos de uso de Net#
En esta sección se proporciona algunos ejemplos de cómo puede usar Net # capas tooadd oculta, definir la manera en que Hola que interactúan con otras capas niveles ocultos y crear redes convolutional.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>Definición de una red neuronal sencilla personalizada: ejemplo "Hello World"
Este ejemplo demuestra cómo toocreate un neural network modelo que tiene una sola capa oculta.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

ejemplo de Hola muestra algunos comandos básicos como sigue:  

* primera línea Hello define nivel de entrada de hello (denominado *datos*). Cuando usas hello **automática** palabra clave, Red neuronal de hello incluye automáticamente todas las columnas de característica en los ejemplos de entrada de Hola. 
* Hola segunda línea crea capa oculta Hola. nombre de Hello *H* se asigna el nivel oculto toohello, que tiene 200 nodos. Este nivel es el nivel de entrada de toohello conectados de forma continua.
* tercera línea de Hello define el nivel de salida de hello (denominado *O*), que contiene 10 nodos de salida. Si se usa la red neuronal de hello para la clasificación, hay un nodo de salida por clase. Hola palabra clave **sigmoidea** indica que la función de salida de hello es nivel de salida de toohello aplicado.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>Definición de varias capas ocultas: ejemplo de visión de equipo
Hello ejemplo siguiente se muestra cómo toodefine una red neuronal ligeramente más compleja, con varios niveles ocultos personalizados.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

En este ejemplo se muestra varias características del lenguaje de especificación de redes neurales hello:  

* estructura de Hello tiene dos niveles de entrada, *píxeles* y *metadatos*.
* Hola *píxeles* capa es una capa de origen para dos paquetes de conexión, con capas de destino, *ByRow* y *ByCol*.
* Hola capas *recopilar* y *resultado* son capas de destino en varios paquetes de conexión.
* nivel de salida de Hello, *resultado*, es una capa de destino en dos agrupaciones de conexión, uno con hello de segundo nivel oculto (recopilación) como una capa de destino y otro con el nivel de entrada de Hola (MetaData) Hola como una capa de destino.
* Hola niveles ocultos, *ByRow* y *ByCol*, especificar la conectividad filtrado mediante expresiones de predicado. Más concretamente, el nodo de hello en *ByRow* en [x, y] está conectado toohello nodos *píxeles* que tienen x de coordenadas, primer Hola índice toohello igual coordenadas del primer nodo. De forma similar, el nodo de hello en *ByCol en [x, y] es nodos conectados toohello _Pixels* que tienen coordenadas de hello segundo índice dentro de una segunda coordenada del nodo de hello, y.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>Defina una red de circunvolución para la clasificación multiclass: ejemplo de reconocimiento de dígitos
definición de Hola de hello después de la red es números toorecognize diseñada e ilustra algunas técnicas avanzadas para personalizar una red neuronal.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* estructura de Hello tiene un único nivel de entrada, *imagen*.
* Hola palabra clave **convolve** indica que las capas de hello denominen *Conv1* y *Conv2* son capas convolutional. Cada una de estas declaraciones capa va seguida de una lista de atributos de circunvolución Hola.
* Hola net tiene una tercera ocultas capa, *Hid3*, que está completamente conectado toohello segunda capa oculta, *Conv2*.
* nivel de salida de Hello, *dígitos*, está conectado toohello solo tercera capa oculta, *Hid3*. Hola palabra clave **todos los** indica dicho nivel de salida de hello esté conectada totalmente demasiado*Hid3*.
* Hello aridad de circunvolución hello es tres (Hola longitud de tuplas de hello **InputShape**, **KernelShape**, **Stride**, y **compartir**). 
* número de Hola de pesos por núcleo es *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26. o bien 26 * 50 = 1300*.
* Puede calcular nodos hello en cada capa oculta como sigue:
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[1] = (13 - 5) / 2 + 1 = 5. 
  * **NodeCount**\[2] = (13 - 5) / 2 + 1 = 5. 
* Hello número total de nodos puede calcularse mediante el uso de hello declarado dimensionalidad de hello las capas, [50, 5, 5], como se indica a continuación:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*
* Porque **compartir**[d] es False solo para *d. == 0*, número de Hola de kernels es  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*. 

## <a name="acknowledgements"></a>Agradecimientos
Hola lenguaje Net # para personalizar la arquitectura de Hola de las redes neurales fue desarrollado en Microsoft por Shon Katzenberger (arquitecto, aprendizaje automático) y Alexey Kamenev (ingeniero de Software, Microsoft Research). Se usa internamente para proyectos y aplicaciones que abarcan desde el análisis de tootext de detección de imagen de aprendizaje automático. Para obtener más información, vea [redes neurales en Azure ML - Introducción tooNet #](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

