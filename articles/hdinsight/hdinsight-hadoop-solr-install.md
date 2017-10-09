---
title: "Acción de secuencia de comandos tooinstall Solr de aaaUse en clúster de Hadoop - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toocustomize HDInsight con Solr mediante la acción de secuencia de comandos."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Instalación y uso de Solr en clústeres de HDInsight basados en Windows

Obtenga información acerca de cómo toocustomize HDInsight basados en Windows de clúster con Solr mediante la acción de secuencia de comandos y cómo toouse Solr toosearch datos.

> [!IMPORTANT]
> Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows. HDInsight solo está disponible en Windows en versiones inferiores a la 3.4. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obtener información sobre el uso de Solr con un clúster basado en Linux, consulte [Instalación y uso de Solr en clústeres de Hadoop para HDinsight (Linux)](hdinsight-hadoop-solr-install-linux.md)


Puede instalar R en cualquier tipo de clúster (Hadoop, Storm, HBase, Spark) en HDInsight de Azure mediante la *acción de script*. Tooinstall de secuencia de comandos de ejemplo Solr en un clúster de HDInsight está disponible en un blob de almacenamiento de Azure de solo lectura en [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

script de ejemplo de Hola solo funciona con la versión de clúster de HDInsight 3.1. Para obtener más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).

script de ejemplo de Hola utilizado en este tema crea un clúster basado en Windows Solr con una configuración concreta. Si desea que el clúster de Solr tooconfigure Hola con diferentes recopilaciones, particiones, esquemas, las réplicas, etc., debe modificar el script de Hola y archivos binarios de Solr en consecuencia.

**Artículos relacionados**

* [Instalación y uso de Solr en clústeres de Hadoop para HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.
* [Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.
* [Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-solr"></a>¿Qué es Solr?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> es una plataforma de búsqueda empresarial que permite una eficaz búsqueda de texto completo en los datos. Mientras Hadoop permite almacenar y administrar grandes cantidades de datos, Apache Solr proporciona capacidades de búsqueda de hello tooquickly recuperar datos de Hola.

## <a name="install-solr-using-portal"></a>Instalación de Solr mediante el portal
1. Empezar a crear un clúster mediante el uso de hello **creación personalizada** opción, como se describe en [Hadoop crear clústeres de HDInsight](hdinsight-provision-clusters.md).
2. En hello **acciones de Script** página del Asistente de hello, haga clic en **Agregar acción de secuencia de comandos** tooprovide detalles sobre la acción de secuencia de comandos de hello, tal y como se muestra a continuación:

    ![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize de acción de secuencia de comandos de uso un clúster")

    <table border='1'>
        <tr><th>Propiedad</th><th>Valor</th></tr>
        <tr><td>Nombre</td>
            <td>Especifique un nombre para la acción de secuencia de comandos de Hola. Por ejemplo, <b>Instalar Solr</b>.</td></tr>
        <tr><td>Identificador URI de script</td>
            <td>Especificar una secuencia toohello de hello identificador uniforme de recursos (URI) que es invocado toocustomize Hola clúster. Por ejemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>.</td></tr>
        <tr><td>Tipo de nodo</td>
            <td>Especifique los nodos de hello en el que se ejecuta el script de personalización de Hola. Puede elegir <b>Todos los nodos</b>, <b>Solo nodos principales</b> o <b>Solo nodos de trabajo</b>.
        <tr><td>parameters</td>
            <td>Especificar parámetros de hello, si así lo requiere el script de Hola. Hola script tooinstall Solr no requiere ningún parámetro, por lo que puede dejar en blanco.</td></tr>
    </table>

    Puede agregar más de una secuencia de comandos acción tooinstall varios componentes en clúster de Hola. Después de haber agregado las secuencias de comandos de hello, haga clic en toostart de marca de verificación de hello crear clúster Hola.

## <a name="use-solr"></a>Uso de Solr
Debe comenzar con la indización de Solr con algunos archivos de datos. A continuación, puede usar consultas de búsqueda de Solr toorun en hello indizado datos. Lleve a cabo Hola siguiendo los pasos toouse Solr en un clúster de HDInsight:

1. **Usar tooremote de protocolo de escritorio remoto (RDP) en clúster de HDInsight de hello con Solr instalado**. Desde el portal de Azure hello, habilitar Escritorio remoto para clúster Hola creadas con clúster de hello instalado y, a continuación, remoto en Solr. Para obtener instrucciones, consulte [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Indexe Solr mediante la carga de archivos de datos**. Al indizar Solr, coloque documentos en el que puede que necesite toosearch. tooindex Solr, utilice RDP tooremote en clúster de hello, navegue toohello escritorio, abra la línea de comandos de Hadoop de Hola y navegar demasiado**C:\apps\dist\solr-4.7.2\example\exampledocs**. Ejecute el siguiente comando de hello:

        java -jar post.jar solr.xml monitor.xml

    Verá Hola siguiente salida de consola hello:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    utilidad de Hello post.jar indiza Solr con dos documentos de ejemplo, **solr.xml** y **monitor.xml**. utilidad de post.jar Hello y documentos de ejemplo de Hola están disponibles con la instalación de Solr.
3. **Use hello Solr panel toosearch dentro de hello indizar documentos**. Hola RDP sesión toohello HDInsight clúster, abra Internet Explorer e iniciar panel de Solr hello en **http://headnodehost:8983/solr / #/**. En panel izquierdo de Hola y de hello **Core Selector** lista desplegable, seleccione **collection1**y dentro de ella, haga clic en **consulta**. Como un ejemplo, tooselect y se devuelven todos los documentos de hello en Solr, proporcionar Hola siguientes valores:

   * Hola **preguntas** texto cuadro, escriba  **\*:**\*. Esto devolverá todos los documentos de Hola que están indizados en Solr. Si desea toosearch una cadena específica dentro de los documentos de hello, puede especificar esa cadena aquí.
   * Hola **wt** cuadro de texto, formato de salida de hello select. El valor predeterminado es **json**. Haga clic en **Ejecutar consulta**.

     ![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "ejecutar una consulta en el panel de Solr")

     salida de Hello devuelve Hola dos documentos que hemos usado para indización Solr. salida de Hello es similar a la siguiente hello:

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
4. **Recomendado: Copia de seguridad Hola indizar los datos de Solr tooAzure almacenamiento de blobs asociado con clúster de HDInsight de Hola**. Como una buena práctica, debe realizar una copia Hola indizado datos desde los nodos del clúster de Solr hello en almacenamiento de blobs de Azure. Lleve a cabo Hola siguiendo los pasos toodo así:

   1. Desde la sesión RDP de hello, abra Internet Explorer y toohello punto después de la dirección URL:

           http://localhost:8983/solr/replication?command=backup

       Debería obtener una respuesta similar a la siguiente:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. En la sesión remota de hello, navegue demasiado {SOLR_HOME}\{colección} \data. Para el clúster de hello creado mediante un script de ejemplo de Hola, debe ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. En esta ubicación, verá una carpeta de instantáneas que se crea con un nombre similar demasiado**instantánea.* marca de tiempo***.
   3. Comprima la carpeta de instantáneas de Hola y cargarlo en el almacenamiento de blobs de tooAzure. Desde la línea de comandos de Hadoop de hello, navegar toohello ubicación de carpeta de instantáneas de hello mediante Hola siguiente comando:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Este comando copias instantáneas demasiado / / datos de ejemplo de Hola/contenedor hello en predeterminado Hola almacenamiento cuenta asociada con el clúster de Hola.

## <a name="install-solr-using-aure-powershell"></a>Instalación de Solr mediante Azure PowerShell
Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  ejemplo de Hola se muestra cómo tooinstall Spark con Azure PowerShell. Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Instalación de Solr con el SDK de .NET
Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). ejemplo de Hola se muestra cómo tooinstall Spark utilizando Hola .NET SDK. Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Otras referencias
* [Instalación y uso de Solr en clústeres de Hadoop para HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.
* [Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.
* [Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).
* [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]: ejemplo de acción de script sobre la instalación de Spark.
* [Instalación de R en clústeres de HDInsight][hdinsight-install-r]: ejemplo de acción de script sobre la instalación de R.
* [Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md): ejemplo de acción de script sobre la instalación de Giraph.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
