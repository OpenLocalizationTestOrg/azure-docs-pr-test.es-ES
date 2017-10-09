---
title: aaaAnalyze Application Insight registra con Spark - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooexport Application Insight registros de almacenamiento de tooblob y, a continuación, analizar registros de hello con Spark en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Análisis de registros de telemetría de Application Insights con Spark en HDInsight

Obtenga información acerca de cómo toouse inspirará en HDInsight tooanalyze los datos de telemetría de Application Insight.

[Application Insights de Visual Studio](../application-insights/app-insights-overview.md) es un servicio de análisis que supervisa sus aplicaciones web. Datos de telemetría generados por Application Insights pueden ser exportado tooAzure almacenamiento. Una vez que los datos de hello están en el almacenamiento de Azure, HDInsight puede ser usado tooanalyze lo.

## <a name="prerequisites"></a>Requisitos previos

* Una aplicación que está había configurado toouse Application Insights.

* Experiencia en la creación de un clúster de HDInsight basado en Linux. Para obtener más información, consulte el artículo sobre [creación de un clúster de Apache Spark en HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un navegador web.

Hello siguientes se utilizan los recursos en desarrollar y probar este documento:

* Los datos de telemetría de visión de aplicación se ha generado mediante una [aplicación web de Node.js configurado toouse Application Insights](../application-insights/app-insights-nodejs.md).

* Un Spark basados en Linux en la versión de clúster de HDInsight 3.5 era tooanalyze usado Hola datos.

## <a name="architecture-and-planning"></a>Arquitectura y planeación

Hola siguiente diagrama ilustra la arquitectura de servicio de Hola de este ejemplo:

![diagrama que muestra los datos que fluyen desde el almacenamiento de tooblob de Application Insights, a continuación, que son procesadas por Spark en HDInsight](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Almacenamiento de Azure

Visión de la aplicación puede ser tooblobs de información de telemetría de exportación toocontinuously configurado. HDInsight, a continuación, puede leer los datos almacenados en blobs de Hola. Sin embargo, hay algunos requisitos que se deben seguir:

* **Ubicación**: si hello cuenta de almacenamiento y HDInsight se encuentran en distintas ubicaciones, puede aumentar la latencia. También incrementa el costo y cargos de salida sea aplicada toodata mover entre regiones.

    > [!WARNING]
    > No se puede usar una cuenta de almacenamiento en una ubicación diferente a la de HDInsight.

* **Tipo de blob**: HDInsight solo es compatible con blobs en bloques. Visión de la aplicación tiene como valor predeterminado de blobs en bloques toousing, por lo que debería funcionar de forma predeterminada con HDInsight.

Para obtener información sobre cómo agregar existente de clúster de HDInsight de tooan de almacenamiento adicional, vea hello [agregar cuentas de almacenamiento adicionales](hdinsight-hadoop-add-storage.md) documento.

### <a name="data-schema"></a>Esquema de datos

Proporciona información de la aplicación [Exportar modelo de datos](../application-insights/app-insights-export-data-model.md) información de formato de datos de telemetría de hello exportado tooblobs. pasos de Hello en este documento usan toowork Spark SQL con datos de Hola. Spark SQL puede generar automáticamente un esquema para la estructura de datos JSON Hola registrado por Application Insights.

## <a name="export-telemetry-data"></a>Exportación de datos de telemetría

Siga los pasos de hello en [configurar exportar continua](../application-insights/app-insights-export-telemetry.md) tooconfigure su tooan de información de telemetría de Application Insights tooexport almacenamiento de Azure blob.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>Configurar datos de saludo de tooaccess de HDInsight

Si va a crear un clúster de HDInsight, agregar la cuenta de almacenamiento de Hola durante la creación del clúster.

Hola tooadd clúster existente de tooan de cuenta de almacenamiento de Azure, use la información de Hola Hola [agregar cuentas de almacenamiento adicionales](hdinsight-hadoop-add-storage.md) documento.

## <a name="analyze-hello-data-pyspark"></a>Analizar datos de hello: PySpark

1. De hello [portal de Azure](https://portal.azure.com), seleccione su Spark en clúster de HDInsight. De hello **vínculos rápidos** sección, seleccione **paneles de clúster**y, a continuación, seleccione **Jupyter Notebook** de hoja de hello Dashboard__ de clúster.

    ![paneles de clúster de Hola](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. En hello esquina superior derecha de la página de Jupyter hello, seleccione **New**y, a continuación, **PySpark**. Se abre una nueva pestaña en el explorador con un cuaderno de Jupyter Notebook basado en Python.

3. En el primer campo de hello (denominado un **celda**) en la página de hello, escriba Hola después de texto:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Este código configura la estructura de directorios de hello Spark toorecursively acceso de datos de entrada de Hola. La telemetría de visión de aplicación es registrado tooa directory estructura similar toohello `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Use **MAYÚS+ENTRAR** código de hello toorun. En hello parte izquierda de la celda de hello, una '\*' aparece entre Hola corchetes tooindicate que se está ejecutando código de hello en esta celda. Una vez que se complete, hello '\*' cambia número tooa y toohello similar después de texto se muestra por debajo de la celda de Hola de salida:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Se crea una nueva celda por debajo de hello primero. Escriba Hola después de texto en la nueva celda de Hola. Reemplace `CONTAINER` y `STORAGEACCOUNT` con nombre de cuenta de almacenamiento de Azure de Hola y el nombre de contenedor de blob que contiene los datos de Application Insights.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Use **MAYÚS+ENTRAR** tooexecute esta celda. Vea un toohello similar de resultados siguiente texto:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    ruta de acceso de Hello wasb devuelta es la ubicación de Hola de hello datos de telemetría de Application Insights. Hola de cambio `hdfs dfs -ls` en hello celda toouse hello wasb ruta devuelta de línea y, a continuación, usar **MAYÚS+ENTRAR** celda de hello toorun nuevo. Este tiempo, resultados de hello deberían mostrar directorios de Hola que contienen los datos de telemetría.

   > [!NOTE]
   > Para los pasos restantes de Hola de hello en esta sección, Hola `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` se usó el directorio. La estructura de sus directorios puede ser diferente.

6. En la siguiente celda hello, escriba Hola siguiente código: reemplazar `WASB_PATH` con ruta de acceso de saludo del paso anterior Hola.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Este código crea una trama de datos de archivos JSON de hello exportados por el proceso de exportación continua de Hola. Use **MAYÚS+ENTRAR** toorun esta celda.
7. En la siguiente celda hello, escriba y ejecute hello después de esquema de hello tooview que Spark creado para los archivos JSON hello:

   ```python
   jsonData.printSchema()
   ```

    esquema de Hola para cada tipo de telemetría es diferente. el ejemplo siguiente se Hello es esquema Hola que se genera para las solicitudes web (datos almacenados en hello `Requests` subdirectorio):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Usar hello después tooregister Hola trama de datos como una tabla temporal y ejecutar una consulta con los datos de hello:

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    Esta consulta devuelve información de la ciudad de Hola para superior 20 registros de Hola donde context.location.city no es null.

   > [!NOTE]
   > estructura de contexto de Hello está presente en todos los telemetría registrado por Application Insights. elemento de la ciudad de Hello no puede llenarse en los registros. Utilice Hola esquema tooidentify otros elementos que puede consultar y que pueden contener datos para sus registros.

    Esta consulta devuelve información toohello similar siguiente texto:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Analizar datos de hello: Scala

1. De hello [portal de Azure](https://portal.azure.com), seleccione su Spark en clúster de HDInsight. De hello **vínculos rápidos** sección, seleccione **paneles de clúster**y, a continuación, seleccione **Jupyter Notebook** de hoja de hello Dashboard__ de clúster.

    ![paneles de clúster de Hola](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. En hello esquina superior derecha de la página de Jupyter hello, seleccione **New**y, a continuación, **Scala**. Se abre una nueva pestaña en el explorador con un cuaderno de Jupyter Notebook basado en Scala.
3. En el primer campo de hello (denominado un **celda**) en la página de hello, escriba Hola después de texto:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Este código configura la estructura de directorios de hello Spark toorecursively acceso de datos de entrada de Hola. Application Insights la telemetría es iniciado tooa estructura de directorios similar demasiado`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Use **MAYÚS+ENTRAR** código de hello toorun. En hello parte izquierda de la celda de hello, una '\*' aparece entre Hola corchetes tooindicate que se está ejecutando código de hello en esta celda. Una vez que se complete, hello '\*' cambia número tooa y toohello similar después de texto se muestra por debajo de la celda de Hola de salida:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Se crea una nueva celda por debajo de hello primero. Escriba Hola después de texto en la nueva celda de Hola. Reemplace `CONTAINER` y `STORAGEACCOUNT` con el nombre de cuenta de almacenamiento de Azure de Hola y el nombre del contenedor de blob que contiene información de la aplicación inicia sesión.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Use **MAYÚS+ENTRAR** tooexecute esta celda. Vea un toohello similar de resultados siguiente texto:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    ruta de acceso de Hello wasb devuelta es la ubicación de Hola de hello datos de telemetría de Application Insights. Hola de cambio `hdfs dfs -ls` en hello celda toouse hello wasb ruta devuelta de línea y, a continuación, usar **MAYÚS+ENTRAR** celda de hello toorun nuevo. Este tiempo, resultados de hello deberían mostrar directorios de Hola que contienen los datos de telemetría.

   > [!NOTE]
   > Para los pasos restantes de Hola de hello en esta sección, Hola `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` se usó el directorio. Este directorio podría no existir, a menos que los datos de telemetría sean de una aplicación web.

6. En la siguiente celda hello, escriba Hola siguiente código: reemplazar `WASB\_PATH` con ruta de acceso de saludo del paso anterior Hola.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Este código crea una trama de datos de archivos JSON de hello exportados por el proceso de exportación continua de Hola. Use **MAYÚS+ENTRAR** toorun esta celda.

7. En la siguiente celda hello, escriba y ejecute hello después de esquema de hello tooview que Spark creado para los archivos JSON hello:

   ```scala
   jsonData.printSchema
   ```

    esquema de Hola para cada tipo de telemetría es diferente. el ejemplo siguiente se Hello es esquema Hola que se genera para las solicitudes web (datos almacenados en hello `Requests` subdirectorio):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Usar hello después tooregister Hola trama de datos como una tabla temporal y ejecutar una consulta con los datos de hello:

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    Esta consulta devuelve información de la ciudad de Hola para superior 20 registros de Hola donde context.location.city no es null.

   > [!NOTE]
   > estructura de contexto de Hello está presente en todos los telemetría registrado por Application Insights. elemento de la ciudad de Hello no puede llenarse en los registros. Utilice Hola esquema tooidentify otros elementos que puede consultar y que pueden contener datos para sus registros.
   >
   >

    Esta consulta devuelve información toohello similar siguiente texto:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Pasos siguientes

Para obtener más ejemplos del uso de Spark toowork con los datos y los servicios de Azure, vea Hola siguientes documentos:

* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

Para obtener información sobre cómo crear y ejecutar aplicaciones de Spark, vea Hola siguientes documentos:

* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)
