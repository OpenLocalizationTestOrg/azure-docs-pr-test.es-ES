---
title: "¿aaaWhat es estudio de aprendizaje automático de Azure? | Microsoft Docs"
description: "Información general de Machine Learning Studio, una herramienta de arrastrar y colocar para crear rápidamente modelos desde una biblioteca lista para usar de algoritmos y módulos."
keywords: azure machine learning, machine learning studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>¿Qué es Azure Machine Learning Studio?
Estudio de aprendizaje automático de Microsoft Azure es una herramienta de colaboración y de arrastrar y colocar puede usar toobuild, probar e implementar soluciones de análisis predictivo en los datos. Machine Learning Studio publica modelos como servicios web que pueden utilizarse fácilmente en aplicaciones personalizadas o herramientas de BI como Excel.

Machine Learning Studio es el lugar en el que confluyen la ciencia de datos, el análisis predictivo, los recursos en la nube y sus datos.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>área de trabajo interactiva de Hello estudio de aprendizaje automático
toodevelop un modelo de análisis predictivos, se utilizan normalmente datos de uno o más orígenes, transformar y analizar datos a través de varias de las funciones estadísticas y manipulación de datos y generar un conjunto de resultados. Desarrollar un modelo como este es un proceso iterativo: Mientras modificas Hola distintas funciones y sus parámetros, los resultados convergen hasta que esté satisfecho que tienen un modelo entrenado y eficaz.

**Estudio de aprendizaje automático de Azure** proporciona un área de trabajo interactivos, visual tooeasily compilar, probar y establecer una iteración en un modelo de análisis predictivos. Que arrastrar y colocar ***conjuntos de datos*** y análisis ***módulos*** en un lienzo interactivo conectándolos tooform junto un ***experimentar***, que se ejecutan en el aprendizaje automático Studio. tooiterate en el diseño del modelo, editar experimento hello, guarde una copia si lo desea y vuelva a ejecutarlo. Cuando esté listo, podrá convertir su ***experimento de entrenamiento*** tooa ***experimento predictivo***y, a continuación, publicarlo como un ***servicio web*** para que el modelo puede tener acceso a otros usuarios.

No hay ninguna programación necesaria, simplemente visualmente conectarse tooconstruct módulos y conjuntos de datos el modelo de análisis predictivos.

> [!TIP]
> toodownload e imprimir un diagrama que ofrezca una visión general de las capacidades de Hola de estudio de aprendizaje automático, consulte [diagrama de información general de las capacidades de estudio de aprendizaje automático de Azure](machine-learning-studio-overview-diagram.md).
> 
> 

![Diagrama de Azure Machine Learning Studio: crear experimentos, leer datos de muchos orígenes, escribir datos puntuados, modelos de escritura.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>Introducción a Machine Learning Studio
Cuando escriba [estudio de aprendizaje automático](https://studio.azureml.net) vea hello **inicio** página. Desde aquí puede ver documentación, vídeos y seminarios web, y encontrar otros recursos valiosos.

Haga clic en el menú de la parte superior izquierda de Hola ![Menú](media/machine-learning-what-is-ml-studio/menu.png) y verá varias opciones.

### <a name="cortana-intelligence"></a>Cortana Intelligence
Haga clic en **Cortana Intelligence** y se le dirigirá toohello portada de hello [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite). Hola Cortana Intelligence Suite es una grande de datos totalmente administrado y advanced analytics suite tootransform los datos en acción inteligente. Consulte la página de inicio de conjunto de Hola para obtener documentación completa, incluidos los casos de usuario de cliente.

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Hay dos opciones en este caso, **inicio**, página Hola donde ha comenzado, y **Studio**.

Haga clic en **Studio** y se le dirigirá toohello **estudio de aprendizaje automático de Azure**. En primer lugar se le preguntará toosign en con su cuenta de Microsoft o su cuenta profesional o educativa. Una vez iniciado sesión, podrá ver Hola siguiendo las pestañas de hello izquierda:

* **PROYECTOS** : colecciones de experimentos, conjuntos de datos, cuadernos y otros recursos que representan un proyecto individual
* **EXPERIMENTOS**: experimentos que ha creado y ejecutado, o que ha guardado como borrador.
* **SERVICIOS WEB** : servicios web que implementó a partir de los experimentos
* **CUADERNOS** : cuadernos de Jupyter que creó
* **CONJUNTOS DE DATOS** : conjuntos de datos que cargó en Estudio
* **MODELOS ENTRENADOS** : modelos que entrenó en experimentos y guardó en Estudio
* **CONFIGURACIÓN de** -una colección de los valores que puede usar tooconfigure su cuenta y sus recursos.

### <a name="gallery"></a>Galería
Haga clic en **galería** y se le dirigirá toohello  **[Galería de inteligencia de Cortana](http://gallery.cortanaintelligence.com/)**. Hola galería es un lugar donde una comunidad de científicos de datos y a los desarrolladores compartir las soluciones creadas con componentes de hello Cortana Intelligence Suite.

Para obtener más información acerca de la Galería de hello, consulte [recurso compartido y descubra soluciones Hola Galería de inteligencia de Cortana](machine-learning-gallery-how-to-use-contribute-publish.md).

## <a name="components-of-an-experiment"></a>Componentes de un experimento
Consta de un experimento de conjuntos de datos que proporcionan los módulos de tooanalytical de datos, que conectan juntos tooconstruct un modelo de análisis predictivos. En concreto, un experimento válido tiene estas características:

* el experimento de Hello tiene al menos un conjunto de datos y un módulo
* Conjuntos de datos pueden ser toomodules solo conectado
* Módulos pueden ser conjuntos de datos conectado tooeither u otros módulos
* Todos los puertos de entrada para los módulos deben tener algunos datos de conexión toohello flujo
* Deben establecerse todos los parámetros necesarios para cada módulo.

Puede crear un experimento desde cero, o puede usar un experimento de ejemplo existente como plantilla. Para obtener más información, consulte [experimentos de ejemplo copia experimentos de aprendizaje automático nuevo toocreate](machine-learning-sample-experiments.md).

Para obtener un ejemplo de creación de un experimento simple, consulte [Creación de un experimento sencillo en Azure Machine Learning Studio](machine-learning-create-experiment.md).

Para obtener un tutorial más completo de la creación de una solución de análisis predictivos, consulte [Desarrollo de una solución predictiva con Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="datasets"></a>CONJUNTOS DE DATOS
Un conjunto de datos es de datos que se ha cargan tooMachine estudio de aprendizaje para que se puede utilizar en el proceso de modelado de Hola. Se incluye con estudio de aprendizaje automático para tooexperiment con una serie de conjuntos de datos de ejemplo y puede cargar varios conjuntos de datos según sea necesario. A continuación se muestran algunos ejemplos de los conjuntos de datos incluidos:

* **Datos sobre consumo de combustible por distancia recorrida para varios automóviles** : valores sobre consumo de combustible por distancia recorrida para automóviles identificados por el número de cilindros, los caballos de potencia, etc.
* **Datos sobre cáncer de mama** : datos de diagnóstico de cáncer de mama.
* **Datos de incendios forestales** : magnitud de los incendios forestales en el noreste de Portugal.

Al crear un experimento puede elegir entre lista Hola de conjuntos de datos disponibles toohello izquierda del lienzo de Hola.

Para obtener una lista de conjuntos de datos de ejemplo incluido en estudio de aprendizaje automático, consulte [utilizar conjuntos de datos de ejemplo de Hola en estudio de aprendizaje automático de Azure](machine-learning-use-sample-datasets.md).

### <a name="modules"></a>Módulos
Un módulo es un algoritmo que puede aplicar sobre sus datos. Estudio de aprendizaje automático tiene un número de módulos que van desde los datos de entrada funciones tootraining, puntuación y validación de los procesos. A continuación se muestran algunos ejemplos de los módulos incluidos:

* [Convertir tooARFF] [ convert-to-arff] -formato de archivo convierte una conjunto de datos serializados. NET tooAttribute-relación (ARFF).
* [Estadísticas elementales de procesos][elementary-statistics]: calcula estadísticas elementales como la media, la desviación estándar, etc.
* [Regresión lineal][linear-regression]: crea un modelo de regresión lineal basado en un descenso de gradiente en línea.
* [Puntuar modelo][score-model]: puntúa un modelo entrenado de clasificación o regresión.

Al crear un experimento puede elegir entre lista Hola de módulos disponibles toohello izquierda del lienzo de Hola.  

Un módulo puede tener un conjunto de parámetros que puede usar algoritmos internos del módulo de tooconfigure Hola. Cuando se selecciona un módulo en el lienzo de hello, los parámetros del módulo de Hola se muestran en hello **propiedades** toohello del panel derecho del lienzo de Hola. Puede modificar los parámetros de hello en ese panel tootune el modelo.

Para algunos ayuda navegar por los gran biblioteca de Hola de algoritmos de aprendizaje automático disponibles, consulte [cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md).

## <a name="deploying-a-predictive-analytics-web-service"></a>Implementación del servicio web de análisis predictivo
Cuando el modelo de análisis predictivo esté listo, puede implementarlo como servicio web directamente desde Machine Learning Studio. Para obtener más información vea [Implementación de un servicio web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
