---
title: tutoriales de Spark aaaHDInsight con PySpark y Scala en Azure | Documentos de Microsoft
description: "Ejemplos de hello proceso de ciencia de datos de equipo que guían a través de hello el uso de PySpark y Scala en un análisis predictivos de toodo de Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>Tutoriales de ciencia de datos de HDInsight Spark con PySpark y Scala en Azure

Estos tutoriales utiliza PySpark y Scala en un análisis predictivos de Azure Spark clúster toodo. Siguen pasos Hola descritos en hello proceso de ciencia de datos de equipo. Para obtener información general de hello proceso de ciencia de datos de equipo, consulte [proceso de ciencia de datos](data-science-process-overview.md). Para obtener información general de Spark en HDInsight, vea [tooSpark de introducción en HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).

Tutoriales de ciencia de datos adicionales que se ejecutan Hola proceso de ciencia de datos de equipo se agrupan por hello **plataforma** que utilizan: 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Predicción de propinas para taxis con PySpark en Azure Spark

Hola [usar Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md) tutorial usa datos de Nueva York taxis toopredict si se le paga una sugerencia y rango de Hola de cantidades espera toobe de pago. Usa Hola proceso de ciencia de datos de equipo en un escenario mediante un [clúster de Azure HDInsight Spark](https://azure.microsoft.com/services/hdinsight/) toostore, explorar y datos de ingeniería de hello disponible públicamente NYC taxi de ida y vuelta de características y resultados son el conjunto de datos. Este tema de introducción configura también con un clúster de HDInsight Spark y hello Jupyter PySpark utilizados en hello resto del tutorial de hello blocs de notas. Estos equipos portátiles mostrarán cómo tooexplore los datos y, a continuación, cómo toocreate y consumir los modelos. Hola avanzada de exploración de datos y modelado Bloc de notas muestra cómo tooinclude validación cruzada, un parámetro de hyper barrido y evaluación de modelos.

### <a name="data-exploration-and-modeling-with-spark"></a>Exploración y modelado de datos con Spark 
Explorar el conjunto de datos de Hola y crear, puntuación y evaluar modelos de aprendizaje automático de Hola por trabajar a través de hello [crear modelos de clasificación y regresión binarios para los datos con el Kit de herramientas de hello Spark MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) tema.

### <a name="model-consumption"></a>Consumo de modelos
toolearn cómo crean modelos de clasificación y regresión de hello tooscore en este tema, consulte [puntuación y evaluar modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Validación cruzada y barrido de hiperparámetros
Consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber cómo se pueden entrenar modelos con el barrido de hiperparámetros y la validación cruzada.


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Predicción de propinas para taxis mediante Scala en Azure Spark

Hola [Scala de uso con Spark en Azure](machine-learning-data-science-process-scala-walkthrough.md) tutorial usa datos de Nueva York taxis toopredict si se le paga una sugerencia y rango de Hola de cantidades espera toobe de pago. Muestra cómo toouse Scala para tareas de aprendizaje automático supervisado con la biblioteca de aprendizaje de máquina Hola Spark (MLlib) y SparkML paquetes en un clúster de Azure HDInsight Spark. Le guía a través de las tareas de Hola que constituyen hello [proceso de ciencia de datos](http://aka.ms/datascienceprocess): recopilación de datos y exploración, visualización, ingeniería de característica, modelado y consumo de modelo. modelos de Hello integrados incluyen regresión logística y lineal, los bosques aleatorios y los árboles impulsados degradados.


## <a name="next-steps"></a>Pasos siguientes

Para obtener una explicación de los componentes clave de Hola que componen Hola proceso de ciencia de datos de equipo, consulte [información general del proceso de ciencia de datos de equipo](data-science-process-overview.md).

Para obtener una descripción que se puede usar toostructure el ciclo de vida del proceso de ciencia de datos de equipo Hola de los proyectos de ciencia de datos, vea [ciclo de vida del proceso de ciencia de datos de equipo](data-science-process-lifecycle.md). ciclo de vida de Hello describe los pasos de hello, de toofinish de inicio, que los proyectos suelen seguir cuando se ejecutan. 

