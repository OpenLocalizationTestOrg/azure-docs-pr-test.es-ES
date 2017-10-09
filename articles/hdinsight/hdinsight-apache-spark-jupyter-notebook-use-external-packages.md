---
title: aaaUse paquetes personalizados de Maven con Jupyter de Spark en HDInsight de Azure | Documentos de Microsoft
description: "Instrucciones paso a paso sobre cómo tooconfigure Jupyter portátiles disponibles con HDInsight Spark clústeres toouse paquetes de Maven personalizados."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight
> [!div class="op_single_selector"]
> * [Uso de magic cell](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Uso de acciones de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Obtenga información acerca de cómo tooconfigure Jupyter notebook en clústeres de Apache Spark en HDInsight toouse externa, Comunidad proporcionado **maven** paquetes que no están incluyen de cuadro en clúster de Hola. 

Puede buscar hello [repositorio Maven](http://search.maven.org/) para la lista completa de Hola de paquetes que están disponibles. También puede obtener una lista de paquetes disponibles de otras fuentes. Por ejemplo, dispone de la lista completa de los paquetes externos aportados por la comunidad en [Spark Packages](http://spark-packages.org/)(Paquetes Spark).

En este artículo, aprenderá cómo hello toouse [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paquete con el Bloc de notas de hello Jupyter.



## <a name="prerequisites"></a>Requisitos previos
Debe disponer de hello siguiente:

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Uso de paquetes externos con cuadernos de Jupyter Notebook
1. De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.   
2. En la hoja de clúster de Spark hello, haga clic en **vínculos rápidos**y, a continuación, desde hello **panel clúster** hoja, haga clic en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.

    > [!NOTE]
    > También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Cree un nuevo notebook. Haga clic en **Nuevo** y luego en **Spark**.
   
    ![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Crear un nuevo cuaderno de Jupyter")

4. Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.
   
    ![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "proporcione un nombre para el Bloc de notas de Hola")

5. Va a usar hello `%%configure` tooconfigure mágico Hola Bloc de notas toouse un paquete externo. En los equipos portátiles que utilizan los paquetes externos, asegúrese de que se llama a hello `%%configure` mágico en la primera celda de código de hello. Esto garantiza que kernel Hola paquete de hello toouse configurado antes de inicia sesión de Hola.

    >[!IMPORTANT] 
    >Si olvida tooconfigure kernel de hello en la primera celda de hello, puede usar hello `%%configure` con hello `-f` parámetro, pero que se reiniciará la sesión de Hola y se perderá todos los progreso.

    | Versión de HDInsight | Comando |
    |-------------------|---------|
    |Para HDInsight 3.3 y HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Para HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. fragmento de código de Hello anterior espera hello maven coordenadas para el paquete externo de hello en el repositorio Central de Maven. En este fragmento de código, `com.databricks:spark-csv_2.10:1.4.0` es hello maven coordenada para **spark-csv** paquete. Le mostramos cómo construir Hola coordenadas para un paquete.
   
    a. Busque el paquete de Hola Hola Maven repositorio. En este tutorial, utilizamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Repositorio de hello, recopilar los valores de hello de **GroupId**, **ArtifactId**, y **versión**. Asegúrese de que haya recopilado de valores de hello coinciden con el clúster. En este caso, estamos usando un Scala 2.10 y un paquete de Spark 1.4.0, pero puede tener tooselect distintas versiones para la versión adecuada de Scala o Spark hello en el clúster. Puede averiguar Hola Scala versión en el clúster mediante la ejecución de `scala.util.Properties.versionString` en el kernel de Spark Jupyter Hola o en enviar Spark. Puede averiguar Hola Spark versión en el clúster mediante la ejecución de `sc.version` en Jupyter blocs de notas.
   
    ![Uso de paquetes externos con cuadernos de Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Uso de paquetes externos con cuadernos de Jupyter")
   
    c. Concatenar valores de hello tres, separados por dos puntos (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Ejecutar la celda de código de hello con hello `%%configure` magia. Esto configurará Hola subyacente Livio sesión toouse Hola paquete proporcionado. En las celdas subsiguientes hello en el Bloc de notas de hello, ahora puede usar el paquete de hello, tal y como se muestra a continuación.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. A continuación, puede ejecutar fragmentos de código de hello, como se muestra a continuación, tooview hello los datos de trama de datos de Hola crean en el paso anterior de Hola.
   
        df.show()
   
        df.select("Time").count()

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

* [Uso de paquetes externos de Python con cuadernos de Jupyter Notebook en clústeres de Apache Spark en HDInsight Linux](hdinsight-apache-spark-python-package-installation.md)
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

