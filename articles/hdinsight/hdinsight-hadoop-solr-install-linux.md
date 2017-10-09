---
title: "Acción de secuencia de comandos de aaaUse tooinstall Solr en HDInsight basados en Linux - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar acciones de Script de clústeres de tooinstall Solr en Hadoop de HDInsight basados en Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Instalación y uso de Solr en clústeres de Hadoop de HDInsight

Obtenga información acerca de cómo tooinstall Solr en HDInsight de Azure mediante la acción de secuencia de comandos. Solr es una eficaz plataforma de búsqueda eficaz y proporciona capacidades de búsqueda de nivel empresarial en datos administrados por Hadoop.

> [!IMPORTANT]
    > pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!IMPORTANT]
> script de ejemplo de Hola usado en este documento instala Solr 4.9 con una configuración concreta. Si desea que el clúster de Solr tooconfigure Hola con diferentes recopilaciones, particiones, esquemas, las réplicas, etc., debe modificar el script de Hola y archivos binarios de Solr.

## <a name="whatis"></a>¿Qué es Solr?

[Apache Solr](http://lucene.apache.org/solr/features.html) es una plataforma de búsqueda empresarial que permite una eficaz búsqueda de texto completo en los datos. Mientras Hadoop permite almacenar y administrar grandes cantidades de datos, Apache Solr proporciona capacidades de búsqueda de hello tooquickly recuperar datos de Hola.

> [!WARNING]
> Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles con Microsoft.
>
> Componentes personalizados, como Solr, reciban soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola. Soporte técnico de Microsoft puede no ser capaz de tooresolve problemas con componentes personalizados. Puede que tenga las Comunidades de código abierto de hello tooengage para obtener ayuda. Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).

## <a name="what-hello-script-does"></a>El script de Hola hace

Este script realiza Hola después de clúster de HDInsight de toohello de cambios:

* Instala Solr 4.9 en `/usr/hdp/current/solr`
* Crea un usuario, **solrusr**, que es usado toorun hello Solr servicio
* Conjuntos de **solruser** como propietario de Hola de`/usr/hdp/current/solr`
* Agrega una configuración [Upstart](http://upstart.ubuntu.com/) que inicia Solr automáticamente.

## <a name="install"></a>Instalación de Solr mediante acciones de script

Tooinstall de secuencia de comandos de ejemplo Solr en un clúster de HDInsight está disponible en hello ubicación siguiente:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate un clúster que tenga instalado el Solr, Hola de uso de los pasos de hello [HDInsight crear clústeres](hdinsight-hadoop-create-linux-clusters-portal.md) documento. Durante el proceso de creación de hello, utilice Hola siguiendo los pasos tooinstall Solr:

1. De hello __resumen de clúster__ hoja, settings__ select__Advanced, a continuación, __acciones de Script__. Usar hello después de formulario de información de Hola toopopulate:

   * **NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.
   * **URI DE SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **PRINCIPAL**: active esta opción.
   * **TRABAJADOR**: active esta opción.
   * **ZOOKEEPER**: comprobar este tooinstall opción en el nodo de hello Zookeeper
   * **PARÁMETROS**: deje este campo en blanco.

2. En parte inferior de Hola de hello **acciones de Script** hoja, use hello **seleccione** configuración del botón toosave Hola. Por último, utilice hello **siguiente** botón tooreturn toohello __resumen de clúster__

3. De hello __resumen de clúster__ página, seleccione __crear__ clúster de hello toocreate.

## <a name="usesolr"></a>Cómo usar Solr en HDInsight

> [!IMPORTANT]
> pasos de Hello en esta sección demuestran la funcionalidad básica de Solr. Para obtener más información sobre cómo usar Solr, vea hello [Solr Apache sitio](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Datos de índice

Usar hello siguiendo los pasos tooadd ejemplo datos tooSolr y, a continuación, realizar consultas sobre él:

1. Conecte el clúster de HDInsight de toohello mediante SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

     > [!IMPORTANT]
     > Pasos más adelante en este documento utiliza un SSL túnel tooconnect toohello Solr interfaz de usuario web. toouse estos pasos, debe establecer una SSL de túnel y, a continuación, configurar su explorador toouse lo.
     >
     > Para obtener más información, vea hello [uso SSH túnel con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

2. Usar hello después de datos de ejemplo de comandos toohave Solr índice:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Hello siguiente resultado se devuelve toohello consola:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Hola `post.jar` utilidad agrega hello **solr.xml** y **monitor.xml** índice toohello de documentos.
  
3. Usar hello después comando tooquery hello Solr API de REST:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    Este comando busca **collection1** para los documentos que coinciden con  **\*:\***  (codificado como \*% 3A\* en la cadena de consulta de hello). Hola siguiendo el documento JSON es un ejemplo de Hola respuesta:

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>Con hello Solr panel

panel de Hello Solr es una interfaz de usuario que le permite toowork con Solr a través del explorador web de web. panel de Hello Solr no se expone directamente en hello Internet desde el clúster de HDInsight. Puede usar un tooaccess de túnel SSH se. Para obtener más información sobre el uso de un túnel SSH, vea hello [uso SSH túnel con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

Una vez que haya establecido un túnel SSH, use Hola siguiente panel de pasos toouse Hola Solr:

1. Determinar el nombre de host de hello para el nodo principal de hello principal:

   1. Utilice el nodo principal del clúster de toohello tooconnect SSH. Por ejemplo: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Para obtener más información sobre el uso de SSH, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Usar hello siguiente comando tooget Hola nombre de host completo:

        ```bash
        hostname -f
        ```

        Este comando devuelve un toohello similar valor después de nombre de host:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Guardar valor Hola devuelve, tal como se utiliza más adelante.

2. En el explorador, conéctese demasiado**http://HOSTNAME:8983/solr / #/**, donde **HOSTNAME** es nombre hello que determinó en pasos anteriores Hola.

    solicitud de saludo se enruta a través de hello SSH túnel toohello Solr interfaz de usuario web en el clúster. página de Hello aparece toohello similar después de imagen:

    ![Imagen del panel de Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. Desde el panel izquierdo de hello, use hello **Core Selector** desplegable tooselect **collection1**. Deberían aparecer varias entradas debajo de **collection1**.

4. En las entradas de hello debajo de **collection1**, seleccione **consulta**. Usar hello después de la página de búsqueda de valores toopopulate hello:

   * Hola **preguntas** texto cuadro, escriba  **\*:**\*. Esta consulta devuelve todos los documentos de Hola que están indizados en Solr. Si desea toosearch una cadena específica dentro de los documentos de hello, puede especificar esa cadena aquí.
   * Hola **wt** cuadro de texto, formato de salida de hello select. El valor predeterminado es **json**.

     Por último, seleccione hello **Ejecutar consulta** situado en parte inferior de Hola de y patentes de búsqueda de Hola.

     ![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     salida de Hello devuelve Hola dos documentos que ha agregado toohello índice anteriormente. Hola de salida es similar toohello posterior documento JSON:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Inicio y detención de Solr

Usar hello siga los comandos toomanually detener e iniciar Solr:

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Copia de seguridad de los datos indizados

Usar hello siguiendo los pasos tooback el almacenamiento de Solr datos toohello predeterminado para el clúster:

1. Conectar el clúster toohello mediante SSH, utilice Hola después de nombre de host de comando tooget hello para el nodo principal de hello:

    ```bash
    hostname -f
    ```

2. Usar hello después comando toocreate una instantánea de hello indizado datos. Reemplace **HOSTNAME** con nombre hello devuelto por el comando anterior hello:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    respuesta de Hello es similar toohello continuación de XML:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Cambie los directorios demasiado`/usr/hdp/current/solr/example/solr`. Hay un subdirectorio aquí para cada colección. Cada directorio de la colección contiene un `data` directorio que contiene la instantánea de hello para la recopilación de Hola.

4. toocreate un archivo comprimido de la carpeta de instantáneas Hola Hola de uso siguiente comando:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Reemplace hello `snapshot.20150806185338855` valores con el nombre de Hola de instantánea de hello para la colección.

    Este comando crea un archivo denominado **snapshot.20150806185338855.tgz**, que contiene el contenido de Hola de hello **snapshot.20150806185338855** directory.

5. A continuación, puede almacenar almacenamiento principal del clúster de hello archivo toohello con hello siguiente comando:

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Para más información sobre cómo trabajar con copia de seguridad y restauraciones de Solr, vea [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Pasos siguientes

* [Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilice tooinstall de personalización de clúster de clústeres de Giraph en Hadoop de HDInsight. Giraph permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure.

* [Instalación de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md). Utilice matiz de tooinstall de personalización de clúster en clústeres de Hadoop de HDInsight. El matiz es que un conjunto de aplicaciones Web utiliza toointeract con un clúster de Hadoop.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
