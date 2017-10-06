---
title: aaaUse Hive de Hadoop y el escritorio remoto en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooHadoop de clúster de HDInsight mediante Escritorio remoto y, a continuación, ejecutar consultas de Hive mediante Hola Hive interfaz de línea de comandos."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Uso de Hive con Hadoop en HDInsight con el escritorio remoto
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

En este artículo, aprenderá cómo las consultas tooconnect tooan HDInsight clúster mediante Escritorio remoto y, a continuación, ejecute subárbol mediante el uso de hello Hive interfaz de línea de comandos (CLI).

> [!IMPORTANT]
> Escritorio remoto sólo está disponible en los clústeres de HDInsight que usa Windows como sistema operativo de Hola. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 o superior, consulte [uso de Hive con HDInsight y Beeline](hdinsight-hadoop-use-hive-beeline.md) para obtener información acerca de cómo ejecutar consultas de Hive directamente en el clúster de Hola desde una línea de comandos.

## <a id="prereq"></a>Requisitos previos
pasos de hello toocomplete en este artículo, se necesita Hola siguiente:

* Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)
* Un equipo cliente con Windows 10, Window 8 o Windows 7

## <a id="connect"></a>Conexión con el Escritorio remoto
Habilitar Escritorio remoto para el clúster de HDInsight de Hola y conéctela tooit siguiendo las instrucciones de hello en [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Usar comandos de Hive Hola
Cuando se ha conectado el escritorio de toohello para el clúster de HDInsight de hello, utilice Hola siguiendo los pasos toowork con Hive:

1. Desde el escritorio de HDInsight de hello, inicie hello **línea de comandos de Hadoop**.
2. Escriba Hola después comando toostart hello Hive CLI:

        %hive_home%\bin\hive

    Cuando se ha iniciado Hola CLI, verá el símbolo del sistema de hello Hive CLI: `hive>`.
3. Hola CLI, escriba Hola siguiendo las instrucciones toocreate una nueva tabla denominada **log4jLogs** con datos de ejemplo:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Estas instrucciones realizan Hola siguientes acciones:

   * **DROP TABLE**: elimina la tabla de Hola y archivo de datos de hello si Hola tabla ya existe.
   * **CREATE EXTERNAL TABLE**: crea una tabla "externa" nueva en Hive. Tablas externas almacenan definición única de la tabla de hello en el subárbol (Hola datos permanecen en la ubicación original de hello).

     > [!NOTE]
     > Tablas externas deben utilizarse cuando creas Hola subyacente toobe datos actualizado por un origen externo (por ejemplo, un proceso de carga de datos automatizado) o por otra operación de MapReduce, pero desea siempre que datos más recientes de toouse Hola de consulta de Hive.
     >
     > Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.
     >
     >
   * **FORMATO de fila**: indica cómo se da formato a los datos de Hola de Hive. En este caso, los campos de hello en cada registro están separados por un espacio.
   * **UBICACIÓN de archivo de texto de AS almacenados**: indica Hive donde están Hola datos almacenados (directorio de datos del ejemplo de Hola) y que se almacena como texto.
   * **Seleccione**: selecciona un recuento de todas las filas donde columna **t4** contiene el valor de hello **[ERROR]**. Esto debe devolver un valor de **3** porque hay tres filas que contienen este valor.
   * **INPUT__FILE__NAME LIKE '%.log'**: indica a Hive que solo deberíamos devolver datos de archivos que terminan en .log. Así restringe hello toohello sample.log archivo de búsqueda contiene datos de Hola y mantiene devuelvan datos del ejemplo de otro archivos de datos que no coinciden con el esquema de Hola que se define.
4. Hola uso siguiendo las instrucciones toocreate una nueva tabla 'interna' denominada **registros de errores de**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Estas instrucciones realizan Hola siguientes acciones:

   * **CREATE TABLE IF NOT EXISTS**: crea una tabla, si todavía no existe. Dado que hello **externo** no se utiliza la palabra clave, se trata de una tabla interna, que se almacena en el almacén de datos de Hive de Hola y Hive administra completamente.

     > [!NOTE]
     > A diferencia de **externo** tablas, quitar una tabla interna también elimina Hola datos subyacentes.
     >
     >
   * **ALMACENA AS ORC**: almacena los datos de hello en formato de fila optimizado columnas (ORC). Se trata de un formato altamente optimizado y eficiente para almacenar datos de Hive.
   * **INSERT OVERWRITE ... Seleccione**: selecciona las filas de hello **log4jLogs** tabla que contenga **[ERROR]**, a continuación, inserta Hola datos en hello **registros de errores de** tabla.

     tooverify que solo las filas que contienen **[ERROR]** en columna t4 estaban almacenado toohello **registros de errores de** tablas, utilice Hola después tooreturn instrucción todos Hola filas de **registros de errores de**:

       SELECT * de errorLogs;

     Se deben devolver tres filas de datos y todas ellas deben contener **[ERROR]** en la columna t4.

## <a id="summary"></a>Resumen
Como puede ver, Hola Hola comando Hive proporciona un toointeractively fácilmente ejecutar consultas de Hive en un clúster de HDInsight, Hola monitor Estado del trabajo y recuperar la salida de hello.

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
