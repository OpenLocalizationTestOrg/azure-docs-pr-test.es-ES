---
title: "Clústeres de HDInsight con arranque: Azure aaaCustomize | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize HDInsight clústeres utilizando el arranque."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a>Personalización de los clústeres de HDInsight con Bootstrap

A veces, desea que los archivos de configuración de tooconfigure hello, que incluyen:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Hay tres toouse métodos arranque:

* Uso de Azure PowerShell
* Uso del SDK de .NET
* Usar plantillas de Azure Resource Manager

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Para obtener información acerca de cómo instalar componentes adicionales en el clúster de HDInsight durante el tiempo de creación de hello, vea:

* [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a>Uso de Azure PowerShell
Hola siguiente código de PowerShell personaliza una configuración de Hive:

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

En el [Anexo A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)aparece un script de PowerShell completamente en uso.

**cambio de Hola tooverify:**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Hola menú izquierdo, haga clic en **clústeres de HDInsight**. Si no lo ve, haga clic primero en **Más servicios**.
3. Haga clic en el clúster de Hola que acaba de crear mediante script de PowerShell de Hola.
4. Haga clic en **panel** de arriba Hola de hello hoja tooopen Hola Ambari UI.
5. Haga clic en **Hive** desde el menú de la izquierda Hola.
6. Haga clic en **HiveServer2** en **Summary** (Resumen).
7. Haga clic en hello **configuraciones** ficha.
8. Haga clic en **Hive** desde el menú de la izquierda Hola.
9. Haga clic en hello **avanzadas** ficha.
10. Desplácese hacia abajo y expanda **Advanced hive-site**(Sitio de Hive avanzado).
11. Busque **hive.metastore.client.socket.timeout** en la sección de Hola.

Otros ejemplos de cómo personalizar otros archivos de configuración:

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

Para más información, vea el blog de Azim Uddin titulado [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx)(Personalización de la creación de clústeres de HDInsight).

## <a name="use-net-sdk"></a>Uso del SDK de .NET
Vea [basados en Linux crear clústeres de HDInsight utilizando Hola .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).

## <a name="use-resource-manager-template"></a>Uso de plantillas de Resource Manager
Puede usar Bootstrap en la plantilla de Resource Manager:

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop personaliza la plantilla de Azure Resource Manager de Bootstrap del clúster](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a>Otras referencias
* [Crear clústeres de Hadoop en HDInsight] [ hdinsight-provision-cluster] proporciona instrucciones sobre cómo toocreate una HDInsight de clúster mediante el uso de otras opciones personalizadas.
* [Desarrollo de acciones de script con HDInsight][hdinsight-write-script]
* [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]
* [Instalación y uso de R en clústeres de Hadoop de HDInsight][hdinsight-install-r]
* [Instalación y uso de Solr en clústeres de Hadoop de HDInsight](hdinsight-hadoop-solr-install.md).
* [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fases durante la creación del clúster"

## <a name="appx-a-powershell-sample"></a>Anexo A: ejemplo de PowerShell
Este script de PowerShell crea un clúster de HDInsight y personaliza una configuración de Hive:

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
