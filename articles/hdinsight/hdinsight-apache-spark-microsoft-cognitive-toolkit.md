---
title: aaaMicrosoft cognitivos Toolkit con Azure HDInsight Spark para aprendizaje profundo | Documentos de Microsoft
description: "Obtenga información acerca de cómo un entrenado cognitivos Kit de herramientas Microsoft profundo modelo de aprendizaje puede ser el conjunto de datos de tooa aplicada mediante Hola Spark Python API en un clúster de Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Uso del modelo de aprendizaje profundo de Microsoft Cognitive Toolkit con un clúster de Azure HDInsight Spark

En este artículo, Hola lo siguiente.

1. Ejecutar un tooinstall de secuencia de comandos personalizada cognitivos Kit de herramientas de Microsoft en un clúster de Azure HDInsight Spark.

2. Cargar un toosee Jupyter notebook toohello Spark clúster cómo tooapply un entrenado cognitivos Kit de herramientas Microsoft profundo aprendizaje toofiles de modelo en una cuenta de almacenamiento de blobs de Azure con hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Antes de comenzar este tutorial, debe tener una suscripción a Azure. Consulte la página [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free).

* **Clúster de Azure HDInsight Spark**. Para este artículo, cree un clúster de Spark 2.0. Para obtener instrucciones, consulte [Creación de un clúster de Apache Spark en Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>¿Cómo funciona esta solución?

Esta solución se divide entre este artículo y un cuaderno de Jupyter que se carga como parte de este tutorial. En este artículo, se realizará Hola pasos:

* Ejecutar una acción de secuencia de comandos en un clúster de HDInsight Spark tooinstall paquetes de Microsoft cognitivos Toolkit y Python.
* Cargue el Bloc de notas de Jupyter de Hola que se ejecuta la solución de hello toohello clúster de HDInsight Spark.

Hola se tratan estos pasos restantes en el Bloc de notas de hello Jupyter.

- Carga de imágenes de ejemplo en un conjunto de datos distribuido resistente o RDD de Spark
   - Carga de los módulos y definición de los valores preestablecidos
   - Descargar conjunto de datos de hello localmente en el clúster de Spark Hola
   - Convertir el conjunto de datos de hello en un diseño dirigido por responsabilidades
- Imágenes de puntuación hello mediante un Kit de herramientas cognitivos entrenado
   - Descargar Hola entrenado Toolkit cognitivos modelo toohello Spark clúster
   - Definir toobe funciones utilizado por los nodos de trabajador
   - Imágenes de puntuación hello en los nodos de trabajador
   - Evaluación de la precisión del modelo


## <a name="install-microsoft-cognitive-toolkit"></a>Instalación de Microsoft Cognitive Toolkit

Puede instalar Microsoft Cognitive Toolkit en un clúster de Spark mediante la acción de scripts. Acción de secuencia de comandos usa componentes de tooinstall scripts personalizados en clúster de Hola que no están disponibles de forma predeterminada. Puede usar secuencias de comandos personalizadas Hola de hello Portal de Azure, mediante el SDK de HDInsight .NET o mediante el uso de PowerShell de Azure. También puede usar el Kit de herramientas de hello script tooinstall hello como parte de la creación del clúster, o después de que el clúster de hello está en funcionamiento. 

En este artículo, usamos hello tooinstall portal Hola toolkit, una vez creado el clúster de Hola. Para otra formas toorun hello secuencia de comandos personalizada, consulte [HDInsight personalizar clústeres mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>Uso de hello Portal de Azure

Para obtener instrucciones sobre cómo toouse hello Azure Portal toorun secuencia de comandos de acción, vea [HDInsight personalizar clústeres mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Asegúrese de que proporcionar Hola después entradas tooinstall cognitivos Kit de herramientas de Microsoft.

* Proporcione un valor para el nombre de acción de secuencia de comandos de Hola.

* Para el **URI de script de Bash**, escriba `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Asegúrese de que ejecuta el script de Hola solo en hello nodos principal y de trabajo y desactive todos Hola otras casillas de verificación.

* Haga clic en **Crear**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Cargar hello Jupyter notebook tooAzure clúster de HDInsight Spark

Hola toouse Microsoft cognitivos Toolkit con clúster de Azure HDInsight Spark hello, debe cargar el Bloc de notas de hello Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello clúster de Azure HDInsight Spark. Este cuaderno está disponible en GitHub en [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Repositorio de GitHub de clon hello [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Para obtener instrucciones tooclone, consulte [clonación de un repositorio](https://help.github.com/articles/cloning-a-repository/).

2. Desde el Portal de Azure hello, abrir la hoja de clúster de Spark de Hola que ya ha aprovisionado, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter notebook**.

    También puede iniciar el Bloc de notas de hello Jupyter yendo toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`. Reemplace \<clustername > con el nombre de Hola de su clúster de HDInsight.

3. En el Bloc de notas de Jupyter hello, haga clic en **cargar** en Hola esquina superior derecha y, a continuación, navegue ubicación toohello donde clonó repositorio de GitHub de Hola.

    ![Cargar Jupyter notebook tooAzure clúster de HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "cargar Jupyter notebook tooAzure clúster de HDInsight Spark")

4. Haga clic en **Cargar** de nuevo.

5. Después de carga el Bloc de notas de hello, haga clic en nombre Hola de Bloc de notas de Hola y, a continuación, siga las instrucciones de hello en Bloc de notas de hello propio acerca de cómo tooload Hola conjunto de datos y realizar el tutorial Hola.

## <a name="see-also"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Análisis de datos de telemetría de Application Insights con Spark en HDInsight](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
