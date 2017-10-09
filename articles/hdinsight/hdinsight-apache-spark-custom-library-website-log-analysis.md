---
title: registros del sitio Web de aaaAnalyze con bibliotecas de Python en Spark - Azure | Documentos de Microsoft
description: "Este bloc de notas, muestra cómo tooanalyze registrar datos de uso de una biblioteca personalizada con Spark en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>Análisis de registros de sitios web mediante una biblioteca Python personalizada con un clúster Apache Spark en HDInsight

Este bloc de notas, muestra cómo tooanalyze registrar datos de uso de una biblioteca personalizada con Spark en HDInsight. se utiliza la biblioteca personalizada Hello es una biblioteca de Python llama **iislogparser.py**.

> [!TIP]
> Este tutorial también está disponible como un cuaderno de Jupyter en un clúster Spark (Linux) que se crea en HDInsight. experiencia de Bloc de notas de Hello le permite ejecutar fragmentos de código de Python Hola desde Bloc de notas de hello propio. tutorial de hello tooperform desde dentro de un bloc de notas, cree un clúster de Spark, inicie Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), y, a continuación, ejecutar el Bloc de notas de hello **analizar registros con Spark mediante un library.ipynb personalizado** en hello  **PySpark** carpeta.
>
>

**Requisitos previos:**

Debe disponer de hello siguiente:

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="save-raw-data-as-an-rdd"></a>Almacenamiento de datos sin procesar como RDD
En esta sección, se utiliza hello [Jupyter](https://jupyter.org) Bloc de notas asociada a un clúster de Apache Spark en HDInsight toorun trabajos que procesan los datos de ejemplo sin formato y guardarla como una tabla de Hive. datos de ejemplo de Hola están un archivo .csv (hvac.csv) disponible en todos los clústeres de forma predeterminada.

Una vez que los datos se guardan como una tabla de Hive, en la sección siguiente Hola se conectará toohello tabla de Hive con herramientas de BI como Power BI y Tableau.

1. De hello [portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.   
2. En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.

   > [!NOTE]
   > También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Cree un nuevo notebook. Haga clic en **Nuevo** y, luego, en **PySpark**.

    ![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Crear un nuevo cuaderno de Jupyter")
4. Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.

    ![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "proporcione un nombre para el Bloc de notas de Hola")
5. Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente. contextos de Spark y Hive Hola se crearán automáticamente automáticamente cuando se ejecuta la primera celda de código de hello. Puede iniciar mediante la importación de tipos de Hola que son necesarios para este escenario. Pegue Hola siguiente fragmento de código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR**.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. Crear un diseño dirigido por responsabilidades mediante datos de registro de ejemplo de Hola ya están disponibles en el clúster de Hola. Puede tener acceso a datos de hello en hello cuenta de almacenamiento predeterminado asociado con el clúster de hello en **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. Recuperar un tooverify de conjunto de registros de ejemplo que Hola paso anterior que se completó correctamente.

        logs.take(5)

    Debería ver un siguiente toohello similar de salida:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>Análisis de datos de registro mediante una biblioteca personalizada de Python
1. En la salida de hello anterior, primeras líneas del par Hola incluyen información de encabezado de Hola y cada línea restante coincide con esquema de hello descrito en ese encabezado. Analizar dichos registros podría ser complicado. Por lo tanto, utilizamos una biblioteca personalizada de Python (**iislogparser.py**) que ayuda a analizar estos registros de manera más fácil. De forma predeterminada, esta biblioteca se incluye con el clúster Spark en HDInsight en **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.

    Sin embargo, esta biblioteca no está en hello `PYTHONPATH` por lo que no podemos usar mediante una instrucción de importación como `import iislogparser`. toouse esta biblioteca, debemos distribuirla nodos de trabajador de tooall Hola. Ejecute hello siguiente fragmento de código.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`Proporciona una función `parse_log_line` que devuelve `None` si una línea de registro es una fila de encabezado y devuelve una instancia de hello `LogLine` clase si encuentra una línea de registro. Hola de uso `LogLine` clase tooextract Hola solo líneas de registro de hello RDD:

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. Recuperar un par de líneas de registro extraídos tooverify que Hola paso se ha completado correctamente.

       logLines.take(2)

   salida de Hello debe ser similar siguiente toohello:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. Hola `LogLine` (clase), a su vez, tiene algunos métodos útiles, como `is_error()`, que se devuelve si una entrada del registro tiene un código de error. Usar este número de hello toocompute de errores en las líneas de registro de hello extraído y, a continuación, todos los Hola errores tooa otro archivo de registro.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Debería ver una salida similar Hola siguiente:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. También puede usar **Matplotlib** tooconstruct una visualización de datos de Hola. Por ejemplo, si desea que la causa de hello tooisolate de solicitudes que se ejecutan durante mucho tiempo, podría desea toofind Hola archivos que toman Hola mayoría tooserve de tiempo promedio.
   siguiente fragmento de Hello recupera Hola top 25 recursos que realizó una solicitud de mayoría tooserve de tiempo.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Debería ver una salida similar Hola siguiente:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. También se puede presentar esta información en forma de Hola de trazado. Como un primer paso toocreate un trazado, permítanos primero crea una tabla temporal **AverageTime**. Hola Hola de grupos de tabla se registra por tiempo toosee si hubiera los picos de latencia inusuales en un momento dado.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. A continuación, puede ejecutar todos los registros de Hola de Hola después tooget de consultas SQL en Hola **AverageTime** tabla.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   Hola `%%sql` mágico seguido `-o averagetime` garantiza que la salida de hello de consulta de Hola se conserva localmente en el servidor de Jupyter Hola (normalmente Hola nodo principal del clúster de hello). salida de Hello se almacena como un [Pandas](http://pandas.pydata.org/) trama de datos con hello especificado nombre **averagetime**.

   Debería ver una salida similar Hola siguiente:

   ![Salida de la consulta SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Salida de la consulta SQL")

   Para obtener más información acerca de hello `%%sql` mágico, vea [admiten parámetros con hello %% magia sql](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
7. Ahora puede usar Matplotlib, una biblioteca usa tooconstruct visualización de datos, toocreate un gráfico. Porque se debe crear trazado de Hola de hello localmente conservan **averagetime** trama de datos, el fragmento de código de hello debe comienzan con hello `%%local` magia. Esto garantiza que el código de hello se ejecuta localmente en el servidor de Jupyter Hola.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Debería ver una salida similar Hola siguiente:

   ![Salida de Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Salida de Matplotlib")
8. Una vez haya terminado de ejecutar la aplicación hello, debería recursos de hello toorelease de apagado Hola Bloc de notas. toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**. Este se apagará y portátil de hello cerrar.

## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)

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
