---
title: "aaaInstall y el uso de clústeres de Giraph en Hadoop en HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toocustomize HDInsight con Giraph y cómo toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Instalación y uso de Giraph en clústeres de HDInsight basados en Linux

Obtenga información acerca de cómo toocustomize Windows en función de clúster de HDInsight con Giraph mediante la acción de secuencia de comandos y cómo toouse Giraph tooprocess a gran escala gráficos. Para obtener información sobre el uso de Giraph con un clúster basado en Linux, consulte [Instalación de Giraph en clústeres Hadoop de HDinsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)

> [!IMPORTANT]
> Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows. HDInsight solo está disponible en Windows en versiones inferiores a la 3.4. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obtener información acerca de cómo tooinstall Giraph en un clúster de HDInsight basados en Linux, consulte [Giraph instalar en clústeres de Hadoop de HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).


Puede instalar Giraph en cualquier tipo de clúster (Hadoop, Storm, HBase, Spark) en HDInsight de Azure mediante la *acción de script*. Tooinstall de secuencia de comandos de ejemplo Giraph en un clúster de HDInsight está disponible en un blob de almacenamiento de Azure de solo lectura en [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). script de ejemplo de Hola solo funciona con la versión de clúster de HDInsight 3.1. Para obtener más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).

**Artículos relacionados**

* [Instalación de Giraph en clústeres de Hadoop de HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.
* [Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.
* [Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-giraph"></a>¿Qué es Giraph?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure. Gráficos de modelar las relaciones entre objetos, como las conexiones de hello entre enrutadores de una red de gran tamaño como Hola Internet, o las relaciones entre las personas en las redes sociales (en ocasiones denominado tooas un gráfico sociales). Procesamiento de gráficos le permite tooreason acerca de las relaciones de hello entre los objetos en un gráfico, como:

* Identificar los posibles amigos según las relaciones actuales.
* Identifica la ruta más corta de hello entre dos equipos en una red.
* Calcular la clasificación de la página de Hola de páginas Web.

## <a name="install-giraph-using-portal"></a>Instalación de Giraph mediante el portal
1. Empezar a crear un clúster mediante el uso de hello **creación personalizada** opción, como se describe en [Hadoop crear clústeres de HDInsight](hdinsight-provision-clusters.md).
2. En hello **acciones de Script** página del Asistente de hello, haga clic en **Agregar acción de secuencia de comandos** tooprovide detalles sobre la acción de secuencia de comandos de hello, tal y como se muestra a continuación:

    ![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize de acción de secuencia de comandos de uso un clúster")

    <table border='1'>
        <tr><th>Propiedad</th><th>Valor</th></tr>
        <tr><td>Nombre</td>
            <td>Especifique un nombre para la acción de secuencia de comandos de Hola. Por ejemplo, <b>Instalar Giraph</b>.</td></tr>
        <tr><td>Identificador URI de script</td>
            <td>Especificar una secuencia toohello de hello identificador uniforme de recursos (URI) que es invocado toocustomize Hola clúster. Por ejemplo, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i>.</td></tr>
        <tr><td>Tipo de nodo</td>
            <td>Especifique los nodos de hello en el que se ejecuta el script de personalización de Hola. Puede elegir <b>Todos los nodos</b>, <b>Solo nodos principales</b> o <b>Solo nodos de trabajo</b>.
        <tr><td>parameters</td>
            <td>Especificar parámetros de hello, si así lo requiere el script de Hola. Hola script tooinstall Giraph no requiere ningún parámetro, por lo que puede dejar en blanco.</td></tr>
    </table>

    Puede agregar más de una secuencia de comandos acción tooinstall varios componentes en clúster de Hola. Después de haber agregado las secuencias de comandos de hello, haga clic en toostart de marca de verificación de hello crear clúster Hola.

## <a name="use-giraph"></a>Uso de Giraph
Usamos hello SimpleShortestPathsComputation ejemplo toodemonstrate Hola basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementación para buscar la ruta de acceso más corta de hello entre los objetos de un gráfico. Usar hello siguiendo los pasos tooupload Hola ejemplo hello y datos de ejemplo jar, ejecute un trabajo mediante el uso de ejemplo de Hola a SimpleShortestPathsComputation y, a continuación, ver los resultados de Hola.

1. Cargar un archivo de datos ejemplo tooAzure almacenamiento de blobs. En la estación de trabajo local, cree un archivo nuevo llamado **tiny_graph.txt**. Debe contener Hola siguientes líneas:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Cargar hello tiny_graph.txt archivo toohello almacenamiento principal para el clúster de HDInsight. Para obtener instrucciones sobre cómo ver datos tooupload, [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).

    Estos datos describen una relación entre los objetos de un gráfico dirigido, con formato de hello [origen\_Id., origen\_valor, [[dest\_id], [borde\_valor],...]]. Cada línea representa una relación entre un objeto **source\_id** y uno más objetos **dest\_id**. Hola **borde\_valor** (o peso) puede considerarse como la intensidad de Hola o distancia de conexión de hello entre **source_id** y **dest\_identificador**.

    Dibujar, y con el valor de hello (o peso) como la distancia de hello entre objetos, Hola por encima de los datos podría ser similar a esto:

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Ejecutar el ejemplo de Hola a SimpleShortestPathsComputation. Usar hello después toorun cmdlets de PowerShell de Azure, hello (ejemplo) mediante el uso de archivo de hello tiny_graph.txt como entrada.

    > [!IMPORTANT]
    > La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017. Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.
    >
    > Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure. Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    Hola ejemplo anterior, reemplace **clustername** con el nombre de Hola de su clúster de HDInsight con Giraph instalado.
3. Ver los resultados de Hola. Una vez que haya finalizado el trabajo de hello, resultados de Hola se almacenarán en dos archivos de salida de hello **wasb: / / / ejemplo/out/shotestpaths** carpeta. se denominan archivos Hello **parte-m-00001** y **parte-m-00002**. Lleve a cabo Hola siguiendo la salida de hello toodownload y vista de pasos:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Esto creará hello **ejemplo/salida/shortestpaths** estructura de directorios en el directorio actual de hello en la estación de trabajo y archivos toothat ubicación de descarga Hola dos resultados.

    Hola de uso **Cat** contenido de Hola de cmdlet toodisplay de los archivos de hello:

        Cat example/output/shortestpaths/part*

    salida de Hello debe aparecer toohello similar a continuación:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    ejemplo de Hola a SimpleShortestPathComputation es toostart codificado con objeto de identificador 1 y buscar objetos de tooother de ruta de acceso más cortos de Hola. Por lo que debe leerse la salida de hello como `destination_id distance`, donde la distancia es valor hello (o peso) de los bordes de hello recorridos entre objeto identificador 1 y Hola Id. de destino.

    Visualizar esto, puede comprobar los resultados de Hola por las rutas de acceso más cortas de hello en viaje entre el identificador 1 y todos los demás objetos. Tenga en cuenta que Hola ruta más corta entre el identificador 1 y 4 de identificador es 5. Se trata de la distancia total de hello entre <span style="color:orange">identificador 1 y 3</span>y, a continuación, <span style="color:red">identificador 3 y 4</span>.

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Instalación de Giraph con Aure PowerShell
Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  ejemplo de Hola se muestra cómo tooinstall Spark con Azure PowerShell. Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Instalación de Giraph mediante .NET SDK
Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). ejemplo de Hola se muestra cómo tooinstall Spark utilizando Hola .NET SDK. Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>Otras referencias
* [Instalación de Giraph en clústeres de Hadoop de HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.
* [Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.
* [Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).
* [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]: ejemplo de acción de script sobre la instalación de Spark.
* [Instalación de R en clústeres de HDInsight][hdinsight-install-r]: ejemplo de acción de script sobre la instalación de R.
* [Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install.md): ejemplo de acción de script sobre la instalación de Solr.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
