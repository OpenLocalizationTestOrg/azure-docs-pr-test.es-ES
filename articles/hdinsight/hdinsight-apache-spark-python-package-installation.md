---
title: "acción de aaaScript: paquetes de instalar Python con Jupyter en HDInsight de Azure | Documentos de Microsoft"
description: "Instrucciones paso a paso sobre cómo toouse script acción tooconfigure Jupyter blocs de notas disponibles con HDInsight Spark clústeres paquetes de python externo toouse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Utilizar paquetes de Python externos de acción de secuencia de comandos tooinstall en blocs de notas de Jupyter en clústeres de Apache Spark en HDInsight
> [!div class="op_single_selector"]
> * [Uso de magic cell](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Uso de acciones de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Obtenga información acerca de cómo toouse acciones de Script tooconfigure un clúster de Apache Spark en HDInsight (Linux) toouse externa, Comunidad proporcionado **python** paquetes que no están incluyen de cuadro en clúster de Hola.

> [!NOTE]
> También puede configurar Jupyter notebook mediante `%%configure` mágico toouse los paquetes externos. Para obtener instrucciones, consulte [Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight Linux](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

Puede buscar hello [índice del paquete](https://pypi.python.org/pypi) para la lista completa de Hola de paquetes que están disponibles. También puede obtener una lista de paquetes disponibles de otras fuentes. Por ejemplo, puede instalar paquetes que están disponibles a través de [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) o [conda-forge](https://conda-forge.github.io/feedstocks.html).

En este artículo, aprenderá cómo hello tooinstall [TensorFlow](https://www.tensorflow.org/) empaquetar mediante Script Actoin en el clúster y usar mediante el Bloc de notas de hello Jupyter.

## <a name="prerequisites"></a>Requisitos previos
Debe disponer de hello siguiente:

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Si aún no tiene un clúster de Spark en HDInsight Linux, puede ejecutar acciones de script durante la creación del clúster. Visite la documentación de hello en [cómo toouse custom script acciones](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Uso de paquetes externos con cuadernos de Jupyter Notebook

1. De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.   

2. En la hoja de clúster de Spark hello, haga clic en **acciones de Script** en **uso**. Ejecutar la acción personalizada de Hola instala TensorFlow en nodos principales de Hola y nodos de trabajador de Hola. pueden hacer referencia a scripts de bash Hola desde: documentación de hello https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh visita en [cómo toouse custom script acciones](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Hay dos python instalaciones en clúster de Hola. Spark usará la instalación de python Anaconda Hola ubicado en `/usr/bin/anaconda/bin`. Haga referencia a esa instalación en sus acciones personalizadas mediante `/usr/bin/anaconda/bin/pip` y `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Abrir un cuaderno de Jupyter de PySpark

    ![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Crear un nuevo cuaderno de Jupyter")

4. Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.

    ![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "proporcione un nombre para el Bloc de notas de Hola")

5. Ahora realizará la acción `import tensorflow` y ejecutará un ejemplo de saludo (Hola mundo). 

    Toocopy de código:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    resultado de Hello tendrá un aspecto similar al siguiente:
    
    ![Ejecución de código de TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Ejecución de código de TensorFlow")



## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)
