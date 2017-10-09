---
title: "aaaUse R en clústeres de HDInsight toocustomize - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar tooinstall R Script acción y use R en clústeres de HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Instalación y uso de R en clústeres de Hadoop para HDInsight

Obtenga información acerca de cómo toocustomize Windows según el clúster de HDInsight con R mediante la acción de secuencia de comandos y cómo los clústeres de toouse R en HDInsight. Hola [HDInsight oferta](https://azure.microsoft.com/pricing/details/hdinsight/) incluye R Server como parte de su clúster de HDInsight. Esto permite a los scripts de R cálculos de toouse MapReduce y Spark toorun distribuida. Para obtener más información, consulte [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md)(Introducción a R Server en HDInsight). Para obtener información sobre el uso de R con un clúster basado en Linux, consulte [Instalación y uso de R en clústeres de Hadoop para HDinsight (Linux)](hdinsight-hadoop-r-scripts-linux.md)

Puede instalar R en cualquier tipo de clúster (Hadoop, Storm, HBase, Spark) en HDInsight de Azure mediante la *acción de script*. Tooinstall de secuencia de comandos de ejemplo R en un clúster de HDInsight está disponible en un blob de almacenamiento de Azure de solo lectura en [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Artículos relacionados**

* [Instalación y uso de R en clústeres de Hadoop para HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md): información general sobre la creación de clústeres de HDInsight.
* [Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.
* [Desarrollo de la acción de script con HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>¿Qué es R?
Hola <a href="http://www.r-project.org/" target="_blank">proyecto de R para la computación estadística</a> es un lenguaje de código abierto y un entorno de computación estadística. R proporciona cientos de de funciones estadísticas integradas y su propio lenguaje de programación que combina aspectos de la programación funcional y orientada a objetos. También proporciona amplias capacidades gráficas. R es el entorno de programación preferido de Hola para profesionales más estadísticos y científicos en una amplia variedad de campos.

R es compatible con el almacenamiento de blobs de Azure (WASB) para que los datos que se almacenan allí se puedan procesar mediante R en HDInsight.  

## <a name="install-r"></a>Instalar R
A [secuencia de comandos de ejemplo](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R en un clúster de HDInsight está disponible en un blob de solo lectura en el almacenamiento de Azure. Esta sección proporciona instrucciones sobre cómo toouse Hola script de ejemplo al crear el clúster de hello mediante Hola Portal de Azure.

> [!NOTE]
> script de ejemplo de Hola se introdujo con la versión 3.1 del clúster de HDInsight. Para más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).
>
>

1. Cuando se crea un clúster de HDInsight de hello Portal, haga clic en **configuración opcional**y, a continuación, haga clic en **acciones de Script**.
2. En hello **acciones de Script** escriba Hola siguientes valores:

    ![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize de acción de secuencia de comandos de uso un clúster")

    <table border='1'>
        <tr><th>Propiedad</th><th>Valor</th></tr>
        <tr><td>Nombre</td>
            <td>Especifique un nombre para la acción de secuencia de comandos de hello, por ejemplo, <b>instalar R</b>.</td></tr>
        <tr><td>Identificador URI de script</td>
            <td>Especificar Hola URI toohello script clúster de hello toocustomize invocado, por ejemplo, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Tipo de nodo</td>
            <td>Especifique los nodos de hello en el que se ejecuta el script de personalización de Hola. Puede elegir <b>Todos los nodos</b>, <b>Solo nodos principales</b> o <b>Solo nodos de trabajo</b>.
        <tr><td>parameters</td>
            <td>Especificar parámetros de hello, si así lo requiere el script de Hola. Sin embargo, Hola script tooinstall R no requiere ningún parámetro, por lo que puede dejar en blanco.</td></tr>
    </table>

    Puede agregar más de una secuencia de comandos acción tooinstall varios componentes en clúster de Hola. Después de haber agregado las secuencias de comandos de hello, haga clic en toostart de marca de verificación de hello empaquetamiento clúster Hola.

También puede utilizar Hola script tooinstall R en HDInsight con Azure PowerShell o hello HDInsight .NET SDK. Más adelante en este artículo se proporcionan instrucciones para estos procedimientos.

## <a name="run-r-scripts"></a>Ejecutar scripts de R
Esta sección describe cómo toorun una R script en Hadoop Hola clúster con HDInsight.

1. **Establecer un clúster de toohello de conexión de escritorio remoto**: desde Hola Portal habilitar Escritorio remoto para el clúster de hello creadas con R instalado y, a continuación, conecte el clúster toohello. Para obtener instrucciones, consulte [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Consola de hello abierto R**: programa de instalación de hello R coloca una consola de R toohello de vínculo en el escritorio de hello del nodo principal de Hola. Haga clic en ella consola de hello R tooopen.
3. **Ejecutar script de Hola R**: script de Hola R se puede ejecutar directamente desde la consola de hello R por pegándola, selecciónelo y presione ENTRAR. Este es un script de ejemplo sencillo que genera Hola números 1 too100 y, a continuación, multiplica por 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Hola dos primeras líneas llamada hello RHadoop bibliotecas que se instalan con R. Hola línea final imprime Hola resultados toohello consola. salida de Hello debería tener este aspecto:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Instalación de R mediante Azure PowerShell
Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  ejemplo de Hola se muestra cómo tooinstall Spark con Azure PowerShell. Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>Instalación de R con .NET SDK
Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). ejemplo de Hola se muestra cómo tooinstall Spark utilizando Hola .NET SDK. Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Otras referencias
* [Instalación y uso de R en clústeres de Hadoop para HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md): información general sobre la creación de clústeres de HDInsight.
* [Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.
* [Desarrollo de la acción de script con HDInsight](hdinsight-hadoop-script-actions.md)
* [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]: ejemplo de acción de script sobre la instalación de Spark.
* [Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md): ejemplo de acción de script sobre la instalación de Giraph.
* [Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md): ejemplo de acción de script sobre la instalación de Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
