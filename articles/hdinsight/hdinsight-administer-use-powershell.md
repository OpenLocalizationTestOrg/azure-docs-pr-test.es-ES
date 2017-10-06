---
title: "clústeres de aaaManage Hadoop en HDInsight con PowerShell, Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform administrativa tareas para hello clústeres de Hadoop en HDInsight con Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Administración de clústeres de Hadoop en HDInsight con PowerShell de Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell es un entorno de scripting eficaz que puede usar toocontrol y automatizar la implementación de Hola y administración de las cargas de trabajo en Azure. En este artículo, aprenderá cómo toomanage clústeres de Hadoop en HDInsight de Azure mediante una consola de PowerShell de Azure local a través de hello el uso de Windows PowerShell. Para lista de Hola de hello HDInsight PowerShell cmdlets, consulte [referencia de cmdlets de HDInsight][hdinsight-powershell-reference].

**Requisitos previos**

Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Azure PowerShell
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Si ha instalado la versión 0.9 x de Azure PowerShell, debe desinstalarla antes de instalar una versión más reciente.

versión de hello toocheck de hello había instalado PowerShell:

    Get-Module *azure*

toouninstall Hola versión anterior, ejecutar programas y características en el panel de control de Hola.

## <a name="create-clusters"></a>Creación de clústeres
Consulte [Crear clústeres basados en Linux en HDInsight con Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Enumeración de clústeres
Usar hello después a toolist comando todos los clústeres en la suscripción actual de hello:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Presentación de clústeres
Usar hello comando tooshow detalles de un clúster concreto en la suscripción actual de hello siguientes:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Eliminación de clústeres
Usar hello después comando toodelete un clúster:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

También puede eliminar un clúster mediante la eliminación de grupo de recursos de Hola que contiene el clúster de Hola. Tenga en cuenta, se eliminarán todos los recursos de hello en grupo de hello incluidas cuenta de almacenamiento predeterminada de Hola.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Escalado de clústeres
característica de ajuste de escala de clúster de Hola permite toochange número de Hola de nodos de trabajador usado por un clúster que se ejecuta en HDInsight de Azure sin necesidad de toore-crear clúster Hola.

> [!NOTE]
> Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior. Si no está seguro de la versión de Hola del clúster, puede comprobar la página de propiedades de Hola.  Consulte [Enumeración y visualización de clústeres](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

impacto de Hola de cambiar el número de Hola de nodos de datos para cada tipo de clúster compatible con HDInsight:

* Hadoop

    Perfectamente puede aumentar el número de Hola de nodos de trabajador en un clúster de Hadoop que se ejecuta sin afectar a los trabajos pendientes o en ejecución. También se pueden enviar trabajos nuevos mientras Hola operación está en curso. Errores en una operación de ajuste de escala se controlan correctamente para que hello clúster siempre se deja en un estado funcional.

    Cuando un clúster de Hadoop es reducido reduciendo el número de Hola de nodos de datos, algunos de los servicios de hello en clúster de Hola se reinician. Esto hace que ejecutan todos y pendiente de trabajos toofail al término de Hola Hola la operación de escalado. Sin embargo, puede volver a enviar trabajos de hello una vez completada la operación de Hola.
* HBase

    Sin problemas, puede agregar o quitar el clúster de HBase tooyour nodos mientras se está ejecutando. Los servidores regionales se equilibran automáticamente dentro de unos pocos minutos después de completar la operación de escalado de Hola. No obstante, puede equilibrar manualmente servidores regionales Hola al iniciar sesión en el nodo principal de toohello del clúster y ejecución Hola siguientes comandos de una ventana del símbolo del sistema:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    Sin problemas, puede agregar o quitar el clúster de Storm de tooyour de nodos de datos mientras se está ejecutando. Sin embargo, tras finalizar correctamente la operación de escalado de hello, debe topología de hello toorebalance.

    Esto se puede realizar de dos formas:

  * La interfaz de usuario web de Storm
  * La herramienta de la interfaz de línea de comandos (CLI)

    Consulte toohello [documentación de Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obtener más detalles.

    interfaz de usuario de web de Storm Hola está disponible en el clúster de HDInsight de hello:

    ![reequilibrio de escalado de storm de HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Este es un ejemplo cómo toouse Hola CLI comando topología de Storm Hola toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Hola toochange tamaño de clúster de Hadoop mediante Azure PowerShell, ejecute hello siguiente comando desde un equipo cliente:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Concesión o revocación del acceso
Clústeres de HDInsight tienen Hola después de servicios web HTTP (todos estos servicios tienen extremos RESTful):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

De manera predeterminada, estos servicios se conceden para el acceso. Puede revocar y conceder acceso de Hola. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> Por conceder o revocar el acceso de hello, se restablecerá la contraseña y el nombre de usuario del clúster de Hola.
>
>

Esto puede hacerse a través de hello Portal. Vea [HDInsight administrar mediante el uso de Hola portal de Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Actualización de las credenciales de usuario HTTP
Es Hola mismo procedimiento como [HTTP conceder o revocar acceso](#grant/revoke-access). Si se concedió clúster Hola Hola acceso HTTP, debe revocar primero.  Y, a continuación, conceder acceso de hello con nuevas credenciales de usuario HTTP.

## <a name="find-hello-default-storage-account"></a>Busque la cuenta de almacenamiento predeterminada de Hola
Hola siguiente script de Powershell muestra cómo tooget nombre de cuenta de almacenamiento predeterminado de Hola y Hola clave de cuenta de almacenamiento predeterminada para un clúster.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Encontrar el grupo de recursos de Hola
En el modo de administrador de recursos de hello, cada clúster de HDInsight pertenece tooan grupo de recursos de Azure.  grupo de recursos de Hola toofind:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Envío de trabajos
**trabajos de MapReduce toosubmit**

Vea [Ejecución de ejemplos de Hadoop MapReduce en HDInsight basado en Windows](hdinsight-run-samples.md).

**trabajos de Hive toosubmit**

Vea [Ejecución de consultas de Hive con PowerShell](hdinsight-hadoop-use-hive-powershell.md).

**trabajos de Pig toosubmit**

Vea [Ejecución de trabajos de Pig mediante PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**trabajos de Sqoop toosubmit**

Consulte [Uso de Sqoop con HDInsight](hdinsight-use-sqoop.md).

**trabajos de Oozie toosubmit**

Vea [Oozie de uso con Hadoop toodefine y ejecutar un flujo de trabajo en HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Cargar el almacenamiento de blobs de datos tooAzure
Vea [cargar datos tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Otras referencias
* [Documentación de referencia de los cmdlets de HDInsight][hdinsight-powershell-reference]
* [Administrar HDInsight mediante Hola portal de Azure][hdinsight-admin-portal]
* [Administración de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]
* [Creación de clústeres de HDInsight][hdinsight-provision]
* [Cargar datos tooHDInsight][hdinsight-upload-data]
* [Envío de trabajos de Hadoop mediante programación][hdinsight-submit-jobs]
* [Introducción a Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
