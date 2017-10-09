---
title: "aaaDebug Apache Spark trabajos se están ejecutando en HDInsight de Azure | Documentos de Microsoft"
description: "Usar la interfaz de usuario de hilo, interfaz de usuario de Spark e historial de Spark server tootrack y depuración trabajos que se ejecutan en un clúster de Spark en HDInsight de Azure"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Depuración de trabajos de Apache Spark que se ejecutan en Azure HDInsight

En este artículo, aprenderá cómo tootrack y depuración inspirará trabajos que se ejecutan en clústeres de HDInsight con hello YARN de interfaz de usuario, interfaz de usuario de Spark y Hola Spark historial de servidor. En este artículo, se iniciará un trabajo de Spark utilizando un bloc de notas disponible con clúster de Spark hello, **aprendizaje automático: análisis predictivos en datos de la inspección de alimentos mediante MLLib**. Puede usar estos pasos hello tootrack una aplicación que envió utilizando cualquier otro enfoque así, por ejemplo, **spark-submit**.

## <a name="prerequisites"></a>Requisitos previos
Debe disponer de hello siguiente:

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).
* Debería haberse iniciado ejecutando Bloc de notas de hello,  **[aprendizaje automático: análisis predictivos en datos de la inspección de alimentos con MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Para obtener instrucciones sobre cómo toorun este bloc de notas, siga Hola vínculo.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Realizar un seguimiento de una aplicación Hola interfaz de usuario de hilo
1. Inicie hello YARN interfaz de usuario. En la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **YARN**.
   
    ![Iniciar interfaz de usuario de YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > Como alternativa, también puede iniciar hello YARN UI de hello Ambari UI. Hola toolaunch Ambari UI, desde la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **panel de clúster de HDInsight**. En hello Ambari UI, haga clic en **YARN**, haga clic en **vínculos rápidos**, haga clic en Administrador de recursos activos de hello y, a continuación, haga clic en **ResourceManager UI**.    
   > 
   > 
2. Dado que se inició el trabajo de Spark de hello mediante Jupyter blocs de notas, aplicación hello tiene el nombre de hello **remotesparkmagics** (es decir, nombre de Hola para todas las aplicaciones que se inician desde blocs de notas de hello). Haga clic en Id. de aplicación Hola contra Hola aplicación nombre tooget obtener más información sobre el trabajo de Hola. Se abre la vista de la aplicación hello.
   
    ![Buscar identificador de aplicación Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Para estas aplicaciones que se inicien desde blocs de notas de hello Jupyter, estado de hello es siempre **EJECUTANDO** hasta que salga de Bloc de notas de Hola.
3. Hola desde vista de aplicación, puede explorar en profundidad más toofind contenedores Hola asociados con la aplicación hello y registros de hello (stdout y stderr). También puede iniciar Hola Spark UI haciendo clic en hello vinculación correspondiente toohello **dirección URL de seguimiento**, tal y como se muestra a continuación. 
   
    ![Descargar registros de contenedor](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Realizar un seguimiento de una aplicación Hola Spark UI
Hola Spark interfaz de usuario, puede profundizar en los trabajos de Spark Hola que son generados por la aplicación hello que inició anteriormente.

1. Hola toolaunch Spark de interfaz de usuario, desde la vista de la aplicación hello, haga clic en vínculo Hola contra Hola **dirección URL de seguimiento**, tal y como se muestra en la captura de pantalla de hello anterior. Puede ver todos los trabajos de Spark Hola iniciados por aplicación Hola que se ejecuta en el Bloc de notas de hello Jupyter.
   
    ![Ver trabajos de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Haga clic en hello **ejecutor** toosee información de procesamiento y almacenamiento para cada elemento de ejecución de la ficha. También puede recuperar la pila de llamadas de hello haciendo clic en hello **subprocesos volcar** vínculo.
   
    ![Ver ejecutores de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Haga clic en hello **fases** ficha fases de hello toosee asociados a la aplicación hello.
   
    ![Ver fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Cada fase puede tener varias tareas de las que puede ver las estadísticas de ejecución, como se muestra a continuación.
   
    ![Ver fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Desde la página de detalles de la fase de hello, puede iniciar la visualización de DAG. Expanda hello **DAG visualización** vincular al principio de Hola de página de hello, tal y como se muestra a continuación.
   
    ![Ver visualización DAG de las fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG o un gráfico de Aclyic directo representa las distintas fases de hello en la aplicación hello. Cada cuadro azul en el gráfico de hello representa una operación de Spark invocada desde aplicación Hola.
5. Desde la página de detalles de la fase de hello, también puede iniciar la vista de escala de tiempo de aplicación Hola. Expanda hello **escala de tiempo del evento** vincular al principio de Hola de página de hello, tal y como se muestra a continuación.
   
    ![Ver escala de tiempo de eventos de fases de Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Esto muestra eventos de Spark hello en forma de Hola de una escala de tiempo. vista de escala de tiempo de Hello está disponible en tres niveles, en los trabajos, en un trabajo y, en una fase. imagen de Hello anterior captura la vista de escala de tiempo de Hola para una determinada fase.
   
   > [!TIP]
   > Si selecciona hello **habilitar Zoom** casilla de verificación, puede desplazarse a la izquierda y derecha en la vista de escala de tiempo de Hola.
   > 
   > 
6. Otras fichas de hello Spark UI proporcionan información útil acerca de la instancia de Spark Hola así.
   
   * Pestaña de almacenamiento: si la aplicación crea un RDDs, puede encontrar información sobre los agentes en la pestaña de almacenamiento de Hola.
   * Ficha entorno - esta pestaña proporciona mucha información útil sobre la instancia de Spark como Hola 
     * La versión de la escala
     * Directorio de registro de eventos asociado con el clúster de Hola
     * Número de núcleos de ejecutor para la aplicación hello
     * Etc.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Buscar información acerca de los trabajos completados con hello Spark historial de servidor
Una vez que se completa un trabajo, información de hello sobre trabajo Hola se mantiene en hello Spark historial de servidor.

1. Hola toolaunch Spark historial de servidor, de hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **Spark historial Server**.
   
    ![Iniciar servidor de historial de Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > Como alternativa, también puede iniciar Hola interfaz de usuario del servidor de historial de Spark de hello Ambari UI. Hola toolaunch Ambari UI, desde la hoja de clúster de hello, haga clic en **panel clúster**y, a continuación, haga clic en **panel de clúster de HDInsight**. En hello Ambari UI, haga clic en **Spark**, haga clic en **vínculos rápidos**y, a continuación, haga clic en **interfaz de usuario del servidor de historial de Spark**.
   > 
   > 
2. Verá todas las aplicaciones de hello completado enumeradas. Haga clic en un toodrill de Id. de aplicación hacia abajo en una aplicación para obtener más información.
   
    ![Iniciar servidor de historial de Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Otras referencias
*  [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Para analistas de datos

* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Análisis de datos de telemetría de Application Insights con Spark en HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Uso de Caffe en Azure HDInsight Spark para el aprendizaje profundo distribuido](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Para desarrolladores de Spark

* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


