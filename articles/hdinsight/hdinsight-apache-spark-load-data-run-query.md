---
title: "realizar consultas interactivas en un clúster de Azure HDInsight Spark aaaRun | Documentos de Microsoft"
description: "Inicio rápido de HDInsight Spark en forma de clúster toocreate un Apache Spark en HDInsight."
keywords: "inicio rápido para spark,spark interactivo,consulta interactiva,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Ejecución de consultas interactivas en un clúster Spark de HDInsight

En este artículo, use un Jupyter notebook toorun Spark SQL las consultas interactivas en un clúster de Spark. Jupyter notebook es una aplicación basada en explorador que extiende Hola experiencia interactiva basada en consola toohello Web. Para obtener más información, consulte [Bloc de notas de hello Jupyter](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

Para este tutorial, utilice hello **PySpark** kernel en hello Jupyter notebook toorun una consulta de Spark SQL interactiva. Los notebooks de Jupyter en clústeres de HDInsight también admiten dos kernels: **PySpark3** y **Spark**. Para obtener más información acerca de los kernels de Hola y Hola ventajas del uso de **PySpark**, consulte [clústeres de núcleos de Bloc de notas de uso Jupyter con Apache Spark en HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Requisitos previos

* **Clúster Spark de Azure HDInsight**. Para obtener instrucciones, consulte [Creación de un clúster de Apache Spark en Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Crear Jupyter notebook toorun realizar consultas interactivas

consultas de toorun, utilizamos datos de ejemplo que está disponible en almacenamiento de hello asociada Hola clúster de forma predeterminada. Sin embargo, primero debe cargar esos datos en Spark como una trama de datos. Una vez que tenga la trama de datos de hello, puede ejecutar consultas en ella con el Bloc de notas de hello Jupyter. En esta sección, puede aprender a:

* Registrar un conjunto de datos de ejemplo como una trama de datos de Spark.
* Ejecutar consultas en la trama de datos de Hola.

1. Abra hello [portal de Azure](https://portal.azure.com/). Si ha elegido el panel de toohello de toopin Hola clúster, haga clic en icono de clúster de Hola desde la hoja de clúster de hello panel toolaunch Hola.

    Si no ancla panel Hola clúster toohello, desde el panel izquierdo de hello, haga clic en **clústeres de HDInsight**y, a continuación, haga clic en clúster de Hola que creó.

3. En **Quick links** (Vínculos rápidos), haga clic en **Cluster dashboards** (Paneles de clúster) y después en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.

   ![Abrir Jupyter notebook toorun interactivo Spark SQL consulta](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "consultas Jupyter Abrir Bloc de notas toorun interactivo Spark SQL")

   > [!NOTE]
   > También puede tener acceso a Jupyter notebook de hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Cree un cuaderno. Haga clic en **Nuevo** y, luego, en **PySpark**.

   ![Crear una consulta de Spark SQL interactiva de Jupyter notebook toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "crear una consulta Jupyter notebook toorun interactiva Spark SQL")

   Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled(Untitled.pynb).

4. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo si desea.

    ![Proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva de](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva desde")

5. Siguiente de Hola de pegar código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR** código de hello toorun. código de Hello importa tipos de hello necesarios en este escenario:

        from pyspark.sql.types import *

    Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente. contextos de Spark y Hive Hola se crean automáticamente cuando se ejecuta la primera celda de código de hello.

    ![Estado de consulta Spark SQL interactiva](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Estado de consulta Spark SQL interactiva")

    Cada vez que ejecute una consulta interactiva en Jupyter, el título de ventana de explorador web muestra un **(estado ocupado)** estado junto con el título de hello Bloc de notas. También verá un toohello siguiente círculo sólido **PySpark** texto en la esquina superior derecha de Hola. Una vez completado el trabajo de hello, cambia el círculo hueco tooa.

6. Antes de cargar datos de hello en un clúster de Spark, nos permiten buscar una instantánea de él. Hello datos de ejemplo utilizados en este tutorial están disponibles como un archivo CSV en todos los clústeres de HDInsight Spark en **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. datos de Hello captura las variaciones de temperatura de Hola de un edificio. Presentamos hello en las primeras filas de datos de Hola.

    ![Instantánea de los datos de consulta SQL interactiva de Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Instantánea de los datos de consultas SQL interactivas de Spark")

6. Crear una trama de datos y una tabla temporal (**hvac**) ejecutando el siguiente código de hello. Para este tutorial, no creamos todas las columnas de hello en tabla temporal de hello como toohello comparados columnas de datos sin procesar de CSV de Hola. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Tras crea tabla hello, ejecutar consultas interactivas de datos de hello, utilice Hola siguiente código.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Porque utiliza un núcleo de PySpark, ahora puede ejecutar directamente una consulta SQL interactiva en la tabla temporal de hello **hvac** que crean mediante hello `%%sql` magia. Para obtener más información acerca de hello `%%sql` mágico y otros magics disponibles con kernel PySpark de hello, vea [núcleos disponibles en los equipos portátiles Jupyter con clústeres de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Hola siguiendo la salida tabular se muestra de forma predeterminada.

     ![Tabla de salida de resultados de consultas Spark interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabla de salida de resultados de consultas Spark interactivas")

    También puede ver los resultados de hello en otras visualizaciones. Por ejemplo, un gráfico de áreas para hello misma salida sería Hola siguiente.

    ![Gráfico de área de resultados de consultas Spark interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gráfico de área de resultados de consultas Spark interactivas")

9. Apagar los recursos de clúster de hello Bloc de notas toorelease Hola después de que haya terminado de ejecutar la aplicación hello. toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.

## <a name="next-step"></a>Paso siguiente

En este artículo se habrá aprendido cómo realizar consultas interactivas toorun en Spark con Jupyter notebook. Avanzar toohello siguiente artículo toosee cómo se pueden extraer datos de hello registrado en Spark en una herramienta de análisis de BI como Power BI y Tableau. 

> [!div class="nextstepaction"]
>[Spark BI mediante herramientas de visualización de datos con Azure HDInsight](hdinsight-apache-spark-use-bi-tools.md)




