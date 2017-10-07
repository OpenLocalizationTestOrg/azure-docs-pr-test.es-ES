---
title: 'aaaHive con herramientas de Data Lake (Hadoop) para Visual Studio: HDInsight de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toouse Hola Data Lake tools para toorun de Visual Studio Apache Hive consultas con Apache Hadoop en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Ejecutar consultas de Hive con herramientas de Data Lake Hola para Visual Studio

Obtenga información acerca de cómo toouse Hola Data Lake tools para Apache Hive de tooquery de Visual Studio. herramientas de Data Lake Hello tooeasily podrá crear, enviar y supervisar tooHadoop de las consultas de Hive en HDInsight de Azure.

## <a id="prereq"></a>Requisitos previos

* Un clúster de Azure HDInsight (Hadoop en HDInsight).

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (uno de hello siguiendo las versiones):

    * Visual Studio 2013 Community/Professional/Premium/Ultimate con la actualización 4

    * Visual Studio 2015 (cualquier edición)

    * Visual Studio 2017 (cualquier edición)

* Herramientas de HDInsight para Visual Studio o Azure Data Lake Tools for Visual Studio. Vea [Introducción al uso de Hadoop de Visual Studio tools para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) para obtener información sobre cómo instalar y configurar las herramientas de Hola.

## <a id="run"></a>Ejecutar consultas de Hive con hello Visual Studio

1. Abra **Visual Studio** y seleccione **Nuevo** > **Proyecto** > **Azure Data Lake** > **HIVE** > **Hive Application** (Aplicación de Hive). Indique un nombre para este proyecto.

2. Abra hello **Script.hql** archivo que se crea con este proyecto y pegar en hello siguiendo las instrucciones de HiveQL:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Estas instrucciones realizan Hola siguientes acciones:

   * `DROP TABLE`: Si existe en la tabla de hello, esta instrucción elimina.

   * `CREATE EXTERNAL TABLE`: Crea una tabla 'externa' en Hive. Tablas externas solo almacenan definición de la tabla de hello en el subárbol (Hola datos permanecen en la ubicación original de hello).

     > [!NOTE]
     > Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo. Por ejemplo, un trabajo de MapReduce o un servicio de Azure.
     >
     > Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.

   * `ROW FORMAT`: Indica cómo se da formato a los datos de Hola de Hive. En este caso, los campos de hello en cada registro están separados por un espacio.

   * `STORED AS TEXTFILE LOCATION`: Indica Hive donde hello se almacenan los datos (directorio de datos del ejemplo de Hola) y que se almacena como texto.

   * `SELECT`: Seleccionar un recuento de todas las filas donde columna `t4` contiene el valor de hello `[ERROR]`. Esta instrucción devuelve un valor de `3` porque hay tres filas que contienen este valor.

   * `INPUT__FILE__NAME LIKE '%.log'`: Indica a Hive que solo deberíamos devolver datos de archivos que terminan en .log. Esta cláusula restringe hello toohello sample.log archivo de búsqueda contiene datos de Hola.

3. En la barra de herramientas de hello, seleccione hello **clúster de HDInsight** que desea toouse para esta consulta. Seleccione **enviar** instrucciones de hello toorun como un trabajo de Hive.

   ![Barra Enviar](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Hola **resumen del trabajo de Hive** aparece y muestra información acerca de hello ejecutar trabajo. Hola de uso **actualizar** vincular toorefresh Hola información sobre el trabajo, hasta hello **estado del trabajo** cambia demasiado**completado**.

   ![resumen de trabajos que muestra un trabajo completado](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Hola de uso **salida del trabajo** vincular la salida de hello tooview de este trabajo. Muestra `[ERROR] 3`, que es el valor de hello devuelto por esta consulta.

6. También puede ejecutar consultas de Hive sin crear un proyecto. Con el **Explorador de servidores**, expanda **Azure** > **HDInsight**, haga clic con el botón derecho en el servidor de HDInsight y luego seleccione **Escribir una consulta de Hive**.

7. Hola **temp.hql** documento que aparece, agregue Hola siguiendo las instrucciones de HiveQL:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Estas instrucciones realizan Hola siguientes acciones:

   * `CREATE TABLE IF NOT EXISTS`: Crea una tabla, si todavía no existe. Dado que hello `EXTERNAL` no se utiliza la palabra clave, esta instrucción crea una tabla interna. Las tablas internas se almacenan en el almacén de datos de Hive de Hola y administradas por el subárbol.

     > [!NOTE]
     > A diferencia de `EXTERNAL` tablas, quitar una tabla interna también elimina Hola datos subyacentes.

   * `STORED AS ORC`: Almacena Hola datos en formato de fila optimizado columnas (ORC). ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.

   * `INSERT OVERWRITE ... SELECT`: Selecciona las filas de hello `log4jLogs` tabla que contenga `[ERROR]`, a continuación, inserta Hola datos en hello `errorLogs` tabla.

8. En la barra de herramientas de hello, seleccione **enviar** trabajo de hello toorun. Hola de uso **estado del trabajo** toodetermine ese trabajo Hola se completó correctamente.

9. tooverify que Hola trabajo creado tabla hello, utilice **Explorador de servidores** y expanda **Azure** > **HDInsight** > su clúster de HDInsight > **Bases de datos de hive** > **predeterminado**. Hola **registros de errores de** hello y tabla **log4jLogs** tabla se enumeran.

## <a id="nextsteps"></a>Pasos siguientes

Como puede ver, las herramientas de HDInsight de Hola para Visual Studio proporcionan una toowork fácilmente con consultas de Hive en HDInsight.

Para obtener información general acerca de Hive en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)

Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)

* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

Para obtener más información acerca de hello HDInsight tools para Visual Studio:

* [Introducción a las herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
