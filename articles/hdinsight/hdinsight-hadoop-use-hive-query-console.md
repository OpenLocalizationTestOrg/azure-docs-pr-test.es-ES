---
title: aaaUse Hive de Hadoop en la consola de consultas en HDInsight - Azure Hola | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola basada en web consola de consultas toorun consultas de Hive en un Hadoop de HDInsight de clúster desde el explorador."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Ejecutar consultas de Hive con hello consola de consultas
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

En este artículo, aprenderá cómo consultas de Hive toouse Hola consola de consultas de HDInsight toorun en un Hadoop de HDInsight de clúster desde el explorador.

> [!IMPORTANT]
> Hola HDInsight consulta consola sólo está disponible en clústeres de HDInsight basados en Windows. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 o superior, consulte [Ejecución de consultas de Hive en la vista Hive de Ambari](hdinsight-hadoop-use-hive-ambari-view.md) para más información sobre cómo ejecutar consultas de Hive desde un explorador web.

## <a id="prereq"></a>Requisitos previos
pasos de hello toocomplete en este artículo, deberá siguiente Hola.

* Un clúster de Hadoop para HDInsight basado en Windows
* Un explorador web moderno

## <a id="run"></a>Ejecutar consultas de Hive con hello consola de consultas
1. Abra un explorador web y navegue demasiado**https://CLUSTERNAME.azurehdinsight.net**, donde **CLUSTERNAME** es Hola nombre de su clúster de HDInsight. Si se le solicite, escriba nombre de usuario de Hola y la contraseña que utilizó cuando creó el clúster de Hola.
2. En los vínculos de hello al principio de Hola de página de hello, seleccione **Editor de Hive**. Esto muestra un formulario que puede ser usado tooenter hello HiveQL instrucciones que desea toorun en clúster de HDInsight de Hola.

    ![editor de subárboles Hola](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Reemplazar texto hello `Select * from hivesampletable` con hello siguiendo las instrucciones de HiveQL:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Estas instrucciones realizan Hola siguientes acciones:

   * **DROP TABLE**: elimina la tabla de Hola y archivo de datos de hello si Hola tabla ya existe.
   * **CREATE EXTERNAL TABLE**: crea una tabla "externa" nueva en Hive. Tablas externas almacenan definición única de la tabla de hello en el subárbol; Hola datos permanecen en la ubicación original de Hola.

     > [!NOTE]
     > Tablas externas deben utilizarse cuando creas Hola subyacente toobe datos actualizado por un origen externo (por ejemplo, un proceso de carga de datos automatizado) o por otra operación de MapReduce, pero desea siempre que datos más recientes de toouse Hola de consulta de Hive.
     >
     > Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.
     >
     >
   * **FORMATO de fila**: indica cómo se da formato a los datos de Hola de Hive. En este caso, los campos de hello en cada registro están separados por un espacio.
   * **UBICACIÓN de archivo de texto de AS almacenados**: indica Hive donde están Hola datos almacenados (directorio de datos del ejemplo de Hola) y que se almacena como texto
   * **Seleccione**: seleccionar un recuento de todas las filas donde columna **t4** contienen el valor de hello **[ERROR]**. Esto debe devolver un valor de **3** porque hay tres filas que contienen este valor.
   * **INPUT__FILE__NAME LIKE '%.log'**: indica a Hive que solo deberíamos devolver datos de archivos que terminan en .log. Así restringe hello toohello sample.log archivo de búsqueda contiene datos de Hola y mantiene devuelvan datos del ejemplo de otro archivos de datos que no coinciden con el esquema de Hola que se define.
3. Haga clic en **Enviar**. Hola **sesión de trabajo** en hello parte inferior de la página de hello debe mostrar detalles de trabajo de Hola.
4. Cuando Hola **estado** cambia de campo demasiado**completado**, seleccione **ver detalles** trabajo Hola. En la página de detalles de Hola Hola **salida del trabajo** contiene `[ERROR]    3`. Puede usar hello **descargar** situado bajo este toodownload de campo de un archivo que contiene la salida de hello de trabajo de Hola.

## <a id="summary"></a>Resumen
Como puede ver, Hola consola de consultas proporciona una manera sencilla de toorun consultas de Hive en un clúster de HDInsight, supervisar el estado del trabajo de Hola y recuperar la salida de hello.

Seleccione toolearn más sobre el uso de trabajos de Hive de consola de consultas de Hive toorun, **Introducción** Hola parte superior de hello consola de consultas, a continuación, utilice los ejemplos de hello que se proporcionan. Cada ejemplo recorre de proceso de hello consiste en utilizar datos de Hive tooanalyze, incluidas explicaciones acerca de las instrucciones de HiveQL Hola utilizadas en el ejemplo de Hola.

## <a id="nextsteps"></a>Pasos siguientes
Para obtener información general acerca de Hive en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)

Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

Si usas Tez con Hive, vea Hola después de documentos para información de depuración:

* [Usar hello Tez UI en HDInsight basados en Windows](hdinsight-debug-tez-ui.md)
* [Usar hello vista Ambari Tez en HDInsight basados en Linux](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
