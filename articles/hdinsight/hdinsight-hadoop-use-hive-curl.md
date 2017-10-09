---
title: aaaUse Hive de Hadoop con doblez en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo enviar tooremotely Pig trabajos tooHDInsight mediante Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Ejecución de consultas de Hive con Hadoop en HDInsight con REST

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Obtenga información acerca de cómo las consultas toouse Hola API de REST de WebHCat toorun Hive con Hadoop en clúster de HDInsight de Azure.

[CURL](http://curl.haxx.se/) es usado toodemonstrate cómo pueden interactuar con HDInsight mediante el uso de las solicitudes HTTP sin formato. Hola [jq](http://stedolan.github.io/jq/) utilidad incluye datos JSON de hello tooprocess usado devueltos desde solicitudes REST.

> [!NOTE]
> Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea hello [lo que necesita tooknow acerca de Hadoop en HDInsight basados en Linux](hdinsight-hadoop-linux-information.md) documento.

## <a id="curl"></a>Ejecución de consultas de Hive

> [!NOTE]
> Al usar cURL o cualquier otro tipo de comunicación REST con WebHCat, debe autenticar solicitudes de hello proporcionando el nombre de usuario de Hola y la contraseña de administrador de clústeres de HDInsight Hola.
>
> Para los comandos de hello en esta sección, reemplace **nombre de usuario** por clúster de hello usuario tooauthenticate toohello y **contraseña** con contraseña hello para la cuenta de usuario de Hola. Reemplace **CLUSTERNAME** con nombre hello del clúster.
>
> API de REST de Hello se protege una a través de [la autenticación básica](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp Asegúrese de que las credenciales de forma segura siempre envía toohello servidor, realizar solicitudes mediante HTTP seguro (HTTPS).

1. Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Recibirá un toohello similar de respuesta siguiente texto:

        {"status":"ok","version":"v1"}

    parámetros de Hello utilizados en este comando son los siguientes:

   * **-u** -Hola nombre de usuario y una contraseña usan tooauthenticate solicitud de saludo.
   * **-G**: indica que esta es una solicitud de operación GET.

     Hola a partir de la dirección URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Hola iguales para todas las solicitudes. ruta de acceso de Hello, **/Status**, indica esa solicitud hello es tooreturn un estado de WebHCat (también conocido como Templeton) para servidor de Hola. También puede solicitar versión Hola del subárbol mediante Hola siguiente comando:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     Esta solicitud devuelve un toohello similar de respuesta siguiente texto:

       {"module":"hive","version":"0.13.0.2.1.6.0-2103"}

2. Hola de uso después de una tabla denominada toocreate **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Hola después de parámetros que se utilizan con esta solicitud:

   * **-d** : desde `-G` no se utiliza, solicitud de hello tiene como valor predeterminado el método POST de toohello. `-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.

     * **User.nombre** -usuario Hola que se ejecuta el comando Hola.
     * **ejecutar** -Hola tooexecute de instrucciones de HiveQL.
     * **statusdir** -se escribió en el directorio de Hola que Hola estado para este trabajo.

     Estas instrucciones realizan Hola siguientes acciones:
   * **DROP TABLE** -si ya existe una tabla de hello, se elimina.
   * **CREATE EXTERNAL TABLE** : crea una tabla "externa" nueva en Hive. Tablas externas almacenan solo la definición de tabla hello en el subárbol. Hola datos permanecen en la ubicación original de Hola.

     > [!NOTE]
     > Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo. Por ejemplo, un proceso de carga de datos automatizado u otra operación de MapReduce.
     >
     > Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.

   * **FORMATO de fila** : cómo Hola datos tienen el formato. los campos de Hello en cada registro están separados por un espacio.
   * **UBICACIÓN de archivo de texto de AS almacenados** : donde se almacenan los datos de hello (directorio de datos del ejemplo de Hola) y que se almacena como texto.
   * **Seleccione** -selecciona un recuento de todas las filas donde columna **t4** contiene el valor de hello **[ERROR]**. Esta instrucción devuelve un valor de **3** porque hay tres filas que contienen este valor.

     > [!NOTE]
     > Tenga en cuenta que los espacios de hello entre las instrucciones de HiveQL se reemplazan por hello `+` caracteres cuando se usa con el doblez. Los valores entre comillas que contengan un espacio, como delimitador de hello, no deben ser reemplazados por `+`.

   * **INPUT__FILE__NAME como '% 25.log'** : esta instrucción límites Hola búsqueda tooonly use archivos de. registro.

     > [!NOTE]
     > Hola `%25` es la forma de codificación de dirección URL de Hola de %, por lo que es la condición real hello `like '%.log'`. Hola % tiene codificada, la dirección URL toobe tal y como se trata como un carácter especial en las direcciones URL.

     Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de Hola.

       {"id":"job_1415651640909_0026"}

3. estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Reemplace **JOBID** con valor Hola devuelta en el paso anterior de Hola. Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, **JOBID** sería `job_1415651640909_0026`.

    Si ha terminado el trabajo de hello, estado de hello es **correcto**.

   > [!NOTE]
   > Esta solicitud Curl devuelve un documento de JavaScript Object Notation (JSON) con información sobre el trabajo de Hola. Se utiliza Jq tooretrieve Hola solo el valor de estado.

4. Una vez que el estado de Hola de trabajo de hello ha cambiado demasiado**correcto**, se pueden recuperar resultados de Hola de trabajo de Hola desde el almacenamiento de blobs de Azure. Hola `statusdir` parámetro pasado con hello consulta contiene ubicación de Hola Hola del archivo de salida; en este caso, **/ejemplo/curl**. Esta dirección almacena los resultados de Hola Hola **ejemplo/curl** directory Hola clústeres de almacenamiento predeterminado.

    Puede enumerar y descargar estos archivos mediante el uso de hello [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Para obtener más información sobre el uso de hello CLI de Azure con el almacenamiento de Azure, vea hello [usar Azure CLI 2.0 con el almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) documento.

5. Hola uso siguiendo las instrucciones toocreate una nueva tabla 'interna' denominada **registros de errores de**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Estas instrucciones realizan Hola siguientes acciones:

   * **CREATE TABLE IF NOT EXISTS** : crea una tabla, si todavía no existe. Esta instrucción crea una tabla interna, que se almacena en el almacén de datos de Hive de Hola y Hive administra completamente.

     > [!NOTE]
     > A diferencia de las tablas externas, al quitar una tabla interna, eliminan datos subyacente de saludo.

   * **ALMACENA AS ORC** -almacena los datos de hello en formato optimizado fila columnas (ORC). ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.
   * **INSERT OVERWRITE ... Seleccione** -selecciona las filas de hello **log4jLogs** tabla que contenga **[ERROR]**, a continuación, inserta Hola datos en hello **registros de errores de** tabla.
   * **Seleccione** -selecciona todas las filas de hello nueva **registros de errores de** tabla.

6. Usar Id. de trabajo de hello devolvió el estado de hello toocheck de trabajo de Hola. Una vez que se ha realizado correctamente, utilice Hola CLI de Azure como se describió anteriormente toodownload y ver resultados de Hola. salida de Hello debe contener tres líneas, todas las cuales contienen **[ERROR]**.

## <a id="nextsteps"></a>Pasos siguientes

Si desea obtener información general sobre Hive con HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)

Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

Si usas Tez con Hive, vea Hola después de documentos para información de depuración:

* [Usar hello vista Ambari Tez en HDInsight basados en Linux](hdinsight-debug-ambari-tez-view.md)

Para obtener más información sobre Hola API de REST que se utiliza en este documento, vea hello [WebHCat referencia](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) documento.

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


