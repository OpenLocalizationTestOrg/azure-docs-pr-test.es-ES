---
title: hoja de referencia de algoritmo de aprendizaje de aaaMachine | Documentos de Microsoft
description: "Una hoja de referencia de algoritmo de aprendizaje de automático imprimible le ayuda a elegir el algoritmo correcto de hello para el modelo de predicción en estudio de aprendizaje automático de Azure."
keywords: algorithm cheat sheet,cheat sheet,machine learning algorithm
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Hoja de referencia rápida de algoritmos de aprendizaje automático de Estudio de aprendizaje automático de Microsoft Azure
Hola **hoja de referencia rápida de Microsoft Azure Machine Learning algoritmo** le ayuda a elegir el algoritmo correcto de Hola para un modelo de análisis predictivos.

[Estudio de aprendizaje automático de Azure](https://studio.azureml.net/) tiene una gran biblioteca de algoritmos de hello ***regresión***, ***clasificación***, ***de agrupación en clústeres***y ***detección de anomalías*** familias. Cada uno está diseñado tooaddress un tipo de problema de aprendizaje de máquina diferente.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>Descarga: Hoja de referencia rápida de algoritmos de aprendizaje automático
**Descargar aquí la hoja de referencia de hello: [hoja de referencia rápida de algoritmo de máquina aprendizaje (11 x 17.)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![Hoja de referencia del algoritmo de aprendizaje de máquina: Obtenga información acerca de cómo toochoose un algoritmo de aprendizaje automático.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

Descarga e impresión Hola hoja de referencia rápida de algoritmo de aprendizaje de máquina en tabloide tookeep práctica y obtenga ayudan a elegir un algoritmo de cambio de tamaño.

> [!NOTE]
> Vea el artículo de hello [cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md) para una guía detallada toousing esta hoja de referencia.
> 
> 

## <a name="more-help-with-algorithms"></a>Más ayuda con los algoritmos
* Para obtener ayuda sobre el uso de esta hoja de referencia para elegir el algoritmo correcto de hello, además de un análisis profundo de diferentes tipos de Hola de algoritmos de aprendizaje automático y cómo se utilizan, vea [cómo toochoose algoritmos de aprendizaje de Microsoft Azure máquina](machine-learning-algorithm-choice.md).
* Para una infografía descargable que describe los algoritmos y proporciona ejemplos, consulte [Infografía descargable: Conceptos básicos de aprendizaje automático con ejemplos de algoritmos](machine-learning-basics-infographic-with-algorithm-examples.md).
* Para obtener una lista por categoría de todos los algoritmos de aprendizaje Hola automático disponibles en estudio de aprendizaje automático, consulte [inicializar modelo] [ initialize-model] en hello Studio algoritmo de aprendizaje de máquina y la Ayuda del módulo.
* Para ver una lista completa de todos los algoritmos de Machine Learning Studio, consulte [Lista de la A a la Z de módulos de Machine Learning Studio][a-z-list] (Lista de la A a la Z de módulos de Machine Learning Studio) en la Ayuda de módulos y algoritmos de Machine Learning Studio.
* toodownload e imprimir un diagrama que ofrezca una visión general de las capacidades de Hola de estudio de aprendizaje automático, consulte [diagrama de información general de las capacidades de estudio de aprendizaje automático de Azure](machine-learning-studio-overview-diagram.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>Hoja de referencia rápida de notas y las definiciones de terminología de algoritmo de aprendizaje automático de Hola

* sugerencias de Hello ofrecidas en esta hoja de referencia de algoritmo son reglas de thumb aproximado. Algunas se pueden ignorar y otras se pueden infringir de forma fragante. Se trata de un punto de partida de toosuggest previsto. No ser toorun atreve una competición dos jugadores entre varios algoritmos en los datos. No hay simplemente no hay sustituto para entender los principios de Hola de cada algoritmo y descripción sistema Hola que genera los datos.

* Cada algoritmo de aprendizaje automático tiene su propio estilo o *sesgo inductivo*. Para un problema específico, varios algoritmos pueden ser apropiados y un algoritmo puede servir mejor que otros. Pero no siempre es posible tooknow con antelación que es mejor Hola. En estos casos, varios algoritmos aparecen juntos en la hoja de referencia de Hola. Una estrategia adecuada se tenga tootry un algoritmo y si los resultados de hello no son satisfactorios, vuelva a Hola otros. Este es un ejemplo de Hola [Galería de inteligencia de Cortana](http://gallery.cortanaintelligence.com/) de un experimento que intente varios algoritmos contra Hola mismos datos y compara Hola resultados: [comparación de clasificadores multiclase: reconocimiento de letra ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* Existen tres categorías principales de aprendizaje automático: **aprendizaje supervisado**, **aprendizaje sin supervisar** y **aprendizaje de refuerzo**.

  * En el **aprendizaje supervisado**, cada punto de datos está etiquetado o asociado con una categoría o valor de interés.  Un ejemplo de una etiqueta de categoría es asignar una imagen como un 'gato' o 'perro'.  Un ejemplo de una etiqueta de valor es precio de venta de hello asociado con un automóvil usado. objetivo de aprendizaje supervisado Hello es toostudy muchas etiquetadas como ejemplos de este tipo y, a continuación, toobe toomake capaz de predicciones acerca de los puntos de datos en el futuro. Por ejemplo, identificar nuevas fotografías con hello correcta animal o la asignación de tooother de los precios de venta precisa que se utiliza automóviles. Este es un tipo conocido y útil del aprendizaje automático. Todos los módulos de hello en el aprendizaje automático de Azure de supervisadas excepto para los algoritmos de aprendizaje [agrupación en clústeres K-Means][k-means-clustering].

  * En el **aprendizaje sin supervisar**, los puntos de datos no tienen etiquetas asociadas a ellos. Hola en su lugar, el objetivo de un algoritmo de aprendizaje supervisados son datos de Hola de tooorganize de alguna manera o toodescribe su estructura. Esto puede significar agruparlos en clústeres, como hace K-means, o buscar diferentes maneras de examinar datos complejos para que parezcan más simples.

  * En **aprendizaje de refuerzo**, algoritmo de hello obtiene toochoose una acción de punto de datos de respuesta tooeach. Es un enfoque común en robótica, donde hello conjunto de lecturas de sensor en un punto en el tiempo es un punto de datos y algoritmo de hello debe elegir la acción siguiente del robot Hola. También resulta perfecto para las aplicaciones de Internet de las cosas. algoritmo de aprendizaje de Hello también recibe una señal de recompensa era un poco más adelante, que indica la calidad decisión Hola. En función de esto, algoritmo de hello modifica su estrategia de recompensa más alto de orden tooachieve Hola. Actualmente no hay ningún módulo de algoritmo de aprendizaje de refuerzo en Aprendizaje automático de Azure.

* **Métodos Bayesianos** hacer suposición Hola de puntos de datos estadísticamente independientes. Esto significa que Hola no modelada variabilidad en un punto de datos es no correlacionado con otros usuarios, es decir, no se puede predecir. Por ejemplo, si los datos de Hola que se está registrados están el número de Hola de minutos hasta que se reciba de entrenar metro siguiente de hello, dos mediciones del día alejados son estadísticamente independientes. Sin embargo, dos mediciones desmontadas un minuto no son estadísticamente independientes; valor de Hola de uno es alta predicción del valor de Hola de hello otro.

* La **regresión del árbol de decisión incrementado** aprovecha la superposición de características o la interacción entre ellas. Que significa que, en cualquier dato determinado punto, Hola valor de una característica es un poco predicción del valor de Hola de otro. Por ejemplo, en los datos de alta y baja temperatura diaria, conocer baja temperatura de hello para el día de hello permite toomake una estimación razonable en hello alta. información de Hello contenida en dos características de hello es redundante en cierto modo.

* Se pueden clasificar los datos en más de una categoría, bien mediante un clasificador multiclase por naturaleza, o combinando un conjunto de clasificadores de dos clases en un **conjunto**. En el enfoque de "conjunto" Hola, hay un clasificador de dos clases independiente para cada clase: cada uno de ellos, separa los datos de hello en dos categorías: "esta clase" y "no esta clase." A continuación, estos clasificadores votan sobre asignación correcta de Hola Hola punto de datos. Este es Hola operativa principio detrás de [Multiclase uno contra todos][one-vs-all-multiclass].

* Varios métodos, incluyendo la regresión logística y máquina del punto de Bayes hello, suponen **los límites de clase lineal**. Es decir, adoptan ese Hola los límites entre las clases son aproximadamente líneas rectas (o hyperplanes en Hola caso más general). Con frecuencia, es una característica de datos de Hola que no conoce hasta después de que has intentado tooseparate, pero es algo que normalmente se puede aprender al visualizar con antelación. Si los límites de la clase de hello buscar muy irregulares, opte por los árboles de decisión, las selvas de decisión, admite las máquinas de vectores o redes neurales.

* Redes neurales pueden utilizarse con variables de categorías mediante la creación de un **variable ficticia** para cada categoría, si se establece too1 en casos donde se aplica categoría hello, que no es de 0.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
