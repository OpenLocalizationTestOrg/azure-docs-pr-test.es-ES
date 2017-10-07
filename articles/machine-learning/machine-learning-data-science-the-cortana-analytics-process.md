---
title: "¿aaaWhat es el proceso de ciencia de datos de equipo?  | Microsoft Docs"
description: "Hola proceso de ciencia de datos de equipo es un método sistemático para la creación de aplicaciones inteligentes que aprovechen las funciones analíticas avanzadas."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>¿Qué es hello proceso de ciencia de datos de equipo (TDSP)?
Hola [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md) proporciona un enfoque sistemático toobuilding aplicaciones inteligentes que permite que los equipos de los datos científicos toocollaborate eficazmente a través de un ciclo de vida completo de Hola de actividades necesarias tooturn estas aplicaciones en productos. Hola TDSP describe una secuencia de pasos que proporcionan **instrucciones** en cómo problema de hello toodefine, configurar las herramientas de Hola y el entorno es necesario, analizar los datos pertinentes, compilar y evaluar modelos de predicción y, a continuación, implementar los modelos en aplicaciones empresariales. 

Estos son los pasos de hello en **proceso de ciencia de datos de equipo**:  

![Flujo de trabajo del proceso de análisis de Cortana](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

proceso de Hello **iterativo**: Hola comprensión de nuevos y existentes o mejoras en el modelo de hello evoluciona y requiere revisión pasos completados anteriormente en la secuencia de Hola. Desarrollo de la organización existente y procesos de planeación del proyecto son **adaptan fácilmente** toowork con hello secuencia definida por el TDSP de pasos. 

Hello pasos de proceso de hello son diagrama y vinculadas en hello [ruta de acceso de aprendizaje de TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y se describe más abajo.  

## <a name="preparation-steps"></a>Pasos de preparación
## <a name="p1-plan-hello-analytics-project"></a>P1. Plan de proyecto de análisis de Hola
Inicie un proyecto de análisis mediante la definición de los objetivos de negocio y los problemas. Se especifican en términos de **requisitos empresariales**. Un objetivo central de este paso es tooidentify Hola empresariales clave variables (ventas previsión u Hola probabilidad de que un pedido que se va a fraudulentas, por ejemplo) que Hola analysis necesidades toopredict toosatisfy estos requisitos. Planeación adicional, a continuación, es esencial normalmente toodevelop una descripción del programa Hola a **orígenes de datos** necesarios tooaddress Hola objetivos del proyecto de Hola desde una perspectiva analítica. No es raro, por ejemplo, toofind que los sistemas existentes otros tipos de datos tooaddress de registro y necesitan toocollect Hola problema y lograr los objetivos del proyecto Hola. Para obtener instrucciones, consulte [planear su entorno para hello proceso de ciencia de datos de equipo](machine-learning-data-science-plan-your-environment.md) y [escenarios para análisis avanzado en aprendizaje automático de Azure](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Configuración del entorno de análisis
Un entorno de análisis para hello proceso de ciencia de datos de equipo implica varios componentes: 

* **áreas de trabajo de datos** donde datos Hola están almacenado provisionalmente para su análisis y modelado, 
* un **infraestructura de procesamiento** para procesamiento previo, explorar y modelado de datos de Hola
* un **infraestructura en tiempo de ejecución** toooperationalize Hola modelos analíticos y ejecutar aplicaciones de cliente inteligente de Hola que usan modelos de Hola.  

infraestructura de análisis de Hola que necesita el programa de instalación de toobe suele ser parte de un entorno que es independiente de los sistemas operativos principales. Pero normalmente aprovecha datos desde varios sistemas dentro de empresa de Hola y de empresa de orígenes externos toohello. infraestructura de análisis de Hello puede ser puramente basado en la nube o una instalación local o una combinación de dos Hola. Para las opciones, consulte [configurar entornos de ciencia de datos para su uso en hello proceso de ciencia de datos de equipo](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Pasos del análisis:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Introducir datos en el entorno analíticos Hola
Hola primer paso es datos relevantes de hello toobring de varios orígenes, ya sea desde dentro o de enterprise Hola fuera, en un análisis entornos donde se pueden procesar los datos de Hola. Hola **formato** de hello datos en origen pueden diferir de formato de hello requerido por el destino de Hola. Por lo que alguna transformación de datos también podrían tener toobe realizarla herramientas de ingesta de Hola. Para ver las opciones, consulte [Carga de datos en entornos de almacenamiento para el análisis](machine-learning-data-science-ingest-data.md)

En suma toohello inicial procesos de recopilación de datos, muchas aplicaciones inteligentes son necesarios toorefresh Hola datos periódicamente como parte de un proceso de aprendizaje en curso. Puede llevarse a cabo mediante la configuración de una **canalización de datos** o un flujo de trabajo. Esto forma parte del elemento iterativo de Hola de proceso de Hola que incluye volver a generar y volver a evaluar modelos analíticos Hola Hola aplicación inteligente implementar soluciones de hello usados. Ver, por ejemplo, [mover datos desde un servidor SQL local tooSQL Azure con Data Factory de Azure](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Exploración y procesamiento previo de los datos
Hola siguiente paso es tooobtain una comprensión más profunda de los datos de hello mediante la investigación su **estadísticas de resumen** , relaciones y mediante el uso de técnicas tales **visualización**. Aquí también es en donde se tratan los problemas de **calidad de datos** y de su integridad, como la inexistencia de valores, las diferencias de tipos de datos y las relaciones de datos incoherentes. Transformaciones previas al procesamiento son tooclean usa los datos sin procesar de hello antes de análisis adicional y modelado puede tener lugar. Para obtener una descripción, consulte [tooprepare datos para el aprendizaje automático mejorada de tareas](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Desarrollo de características
Los científicos de datos, en colaboración con expertos de dominio, deben identificar las características de Hola que captura hello más destacadas propiedades del conjunto de datos de Hola y mejor pueden ser variables de clave del negocio de Hola de toopredict usado identificadas durante la planeación. Estas nuevas características se pueden derivar de los datos existentes o pueden requerir toobe de datos adicionales que se recopilan. Este proceso se conoce como **característica ingeniería** y es uno de hello pasos clave en la creación de un sistema eficaz de análisis predictivos. Este paso requiere una combinación creativa de visión de hello y experiencia de dominio obtenida en el paso de exploración de datos de Hola. Para obtener instrucciones, consulte [ingeniería Hola proceso de ciencia de datos de equipo de características](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Creación de modelos de predicción
Los científicos de datos generación modelos analíticos identificadas por los requisitos de negocios de hello definidos en hello planeación paso utilizando los datos que se ha limpiado y caracterizará variables toopredict Hola clave. Sistemas de aprendizaje de máquina admitan varias **modelado algoritmos** que son aplicables tooa gran variedad de casos. Para obtener instrucciones, consulte [cómo toochoose algoritmos de aprendizaje automático de Azure de equipo](machine-learning-algorithm-choice.md).

Los científicos de datos deben elegir el modelo de hello más adecuado para su tarea de predicción y no es raro que los resultados de varios modelos necesitan toobe combinan tooobtain Hola obtener los mejores resultados. Hello datos de entrada para el modelado es normalmente divide aleatoriamente en tres partes:

* un conjunto de datos de aprendizaje 
* un conjunto de datos de validación 
* un conjunto de datos de prueba 

se generan los modelos de Hello mediante hello **conjunto de datos de entrenamiento**. la combinación óptima de modelos (con parámetros optimizados) Hello está activada de forma ejecutando modelos de Hola y medición de errores de predicción de Hola para hello **conjunto de datos de validación**. Por último Hola **conjunto de datos de prueba** es tooevaluate usado Hola rendimiento del modelo de hello elegido en datos independientes que no ha usado tootrain o validar el modelo de Hola.  Para conocer los procedimientos, consulte [cómo tooevaluate modelo rendimiento aprendizaje automático de Azure](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Implementación y consumo de modelos
Una vez que tenemos un conjunto de modelos que funcionan bien, pueden ser **operaciones** para otro tooconsume de aplicaciones. Dependiendo de los requisitos empresariales hello, se crean las predicciones en **tiempo real** o en un **lote** base. toobe operaciones, los modelos de hello tienen toobe que se exponen a través de un **abrir la interfaz API** que puedan usar fácilmente desde diversas aplicaciones tales sitio Web en línea, hojas de cálculo, paneles o en línea de aplicaciones empresariales y de back-end. Consulte [Implementar un servicio web de Aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Resumen y pasos siguientes
Hola [proceso de ciencia de datos de equipo](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) se modela como una secuencia de pasos iteradas que **proporcionan instrucciones** en tareas de hello toouse necesario avanzado análisis toobuild un aplicaciones inteligentes. Cada paso también proporciona detalles sobre lo toouse diversas tareas de Hola de toocomplete de tecnologías de Microsoft que describe. 

Mientras TDSP no prescribir tipos específicos de **documentación** artefactos, se tiene una mejor práctica toodocument hello como resultado de exploración de datos de hello, modelado y evaluación y toosave Hola código pertinente para que análisis de Hola Puede que se itera cuando sea necesario. Esto también permite la reutilización de hello análisis funcionan cuando se trabaja en otras aplicaciones que implican datos similares y tareas de predicción.

Completa-to-end tutoriales que muestran todos los pasos de hello en proceso de Hola para **escenarios concretos** también se proporcionan. Por ejemplo, consulte:

* [Hola proceso de ciencia de datos de equipo en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Hola proceso de ciencia de datos de equipo en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md).
* [Información general sobre la ciencia de los datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md)
* [Ciencia de datos escalables en Azure Data Lake: tutorial completo](machine-learning-data-science-process-data-lake-walkthrough.md)

