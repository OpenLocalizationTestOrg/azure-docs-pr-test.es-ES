---
title: aaaMigrate tooAzure el Administrador de recursos de las herramientas de HDInsight | Documentos de Microsoft
description: "Cómo las herramientas toomigrate tooAzure desarrollo del Administrador de recursos para clústeres de HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>Herramientas de desarrollo basado en el Administrador de recursos tooAzure migrar para clústeres de HDInsight

HDInsight está abandonando el uso de herramientas basadas en Azure Service Manager (ASM) para HDInsight. Si se ha usando Azure PowerShell, CLI de Azure o hello HDInsight .NET SDK toowork con clústeres de HDInsight, son toouse recomienda Hola basado en ARM de administrador de recursos de Azure versiones de PowerShell, CLI y .NET SDK en el futuro. Este artículo proporciona punteros acerca de cómo toomigrate toohello nuevo basado en ARM enfoque. Siempre que sea aplicable, este artículo también señala las diferencias de hello entre los enfoques ASM y ARM de Hola para HDInsight.

> [!IMPORTANT]
> soporte de Hola para ASM basada en PowerShell, CLI, y dejará de SDK de .NET en **del 1 de enero de 2017**.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>Migrar tooAzure de CLI de Azure Resource Manager
Hola CLI de Azure ahora tiene como valor predeterminado el modo de tooAzure Resource Manager (ARM), a menos que se va a actualizar desde una instalación anterior; en este caso, deberá toouse hello `azure config mode arm` modo de comando tooswitch tooARM.

comandos básicos de Hola que Hola CLI de Azure proporciona toowork con HDInsight con la administración de servicio de Azure (ASM) se Hola igual al usar ARM; Sin embargo algunos parámetros y modificadores de pueden tener nombres nuevos, y hay muchos nuevos parámetros disponibles cuando se usa ARM. Por ejemplo, ahora puede usar `azure hdinsight cluster create` toospecify Hola red Virtual de Azure que deben crearse en un clúster, o subárbol e información de la tienda de metadatos de Oozie.

Los comandos básicos para trabajar con HDInsight a través de Azure Resource Manager son:

* `azure hdinsight cluster create` : crea un clúster de HDInsight
* `azure hdinsight cluster delete` : elimina un clúster de HDInsight que ya existe
* `azure hdinsight cluster show` : muestra información acerca de un clúster que ya existe
* `azure hdinsight cluster list` : enumera los clústeres de HDInsight para la suscripción de Azure

Hola de uso `-h` cambiar los parámetros de hello tooinspect y modificadores disponibles para cada comando.

### <a name="new-commands"></a>Nuevos comandos
Los nuevos comandos disponibles con Azure Resource Manager son:

* `azure hdinsight cluster resize`-dinámicamente cambios Hola número de nodos de trabajador del clúster Hola
* `azure hdinsight cluster enable-http-access`-permite HTTPs acceso toohello clúster (de forma predeterminada)
* `azure hdinsight cluster disable-http-access`-deshabilita el clúster de toohello de acceso de HTTPs
* `azure hdinsight script-action` : proporciona comandos para crear y administrar las acciones de script en un clúster
* `azure hdinsight config`-proporciona comandos para crear un archivo de configuración que se puede usar con hello `hdinsight cluster create` comando tooprovide la información de configuración.

### <a name="deprecated-commands"></a>Comandos en desuso
Si usas hello `azure hdinsight job` clúster de HDInsight de comandos toosubmit trabajos tooyour, estos no están disponibles a través de los comandos de hello ARM. Si necesita tooprogrammatically enviar trabajos tooHDInsight desde secuencias de comandos, debe usar en su lugar hello las API de REST proporcionada por HDInsight. Para obtener más información sobre cómo enviar trabajos mediante las API de REST, vea Hola después de documentos.

* [Ejecución de trabajos de MapReduce con Hadoop en HDInsight con Curl](hdinsight-hadoop-use-mapreduce-curl.md)
* [Ejecución de consultas de Hive con Hadoop en HDInsight con cURL](hdinsight-hadoop-use-hive-curl.md)
* [Ejecución de trabajos de Pig con Hadoop en HDInsight con Curl](hdinsight-hadoop-use-pig-curl.md)

Para obtener información sobre otro toorun formas MapReduce, Hive, Pig de forma interactiva, consulte [MapReduce de uso con Hadoop en HDInsight](hdinsight-use-mapreduce.md), [uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md), y [uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md).

### <a name="examples"></a>Ejemplos
**Creación de un clúster**

* Comando anterior (ASM): `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* Nuevo comando (ARM): `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**Eliminación de un cluster**

* Comando anterior (ASM): `azure hdinsight cluster delete myhdicluster`
* Nuevo comando (ARM): `azure hdinsight cluster delete mycluster -g myresourcegroup`

**Enumeración de clústeres**

* Comando anterior (ASM): `azure hdinsight cluster list`
* Nuevo comando (ARM): `azure hdinsight cluster list`

> [!NOTE]
> Comando de lista de hello, especificar Hola grupo de recursos mediante `-g` devolverá solo los clústeres de hello en el grupo de recursos especificado Hola.
> 
> 

**Presentación de la información de clúster**

* Comando anterior (ASM): `azure hdinsight cluster show myhdicluster`
* Nuevo comando (ARM): `azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>Migrar tooAzure de PowerShell de Azure Resource Manager
Hola obtener información general acerca de PowerShell de Azure en el modo de hello Azure Resource Manager (ARM) puede encontrarse en [con Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).

Hola cmdlets de ARM de PowerShell de Azure puede ser instalado en paralelo con hello ASM cmdlets. cmdlets de Hola de dos modos de Hola se pueden distinguir por sus nombres.  el modo de Hello ARM tiene *AzureRmHDInsight* en nombres de cmdlet de hello comparar demasiado*AzureHDInsight* en modo ASM de Hola.  Por ejemplo, *AzureRmHDInsightCluster New* frente a *New-AzureHDInsightCluster*. Parámetros y conmutadores pueden tener nombres nuevos y hay muchos parámetros nuevos disponibles si utiliza ARM.  Por ejemplo, varios cmdlets requieren un nuevo modificador llamado *- ResourceGroupName*. 

Antes de poder usar cmdlets de HDInsight de hello, debe conectarse tooyour cuenta de Azure y crear un nuevo grupo de recursos:

* Login-AzureRmAccount o [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx). Consulte [Autenticación de una entidad de servicio con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>Cmdlets cuyo nombre ha cambiado
Hola toolist cmdlets de HDInsight ASM en la consola de Windows PowerShell:

    help *azurermhdinsight*

Hello tabla siguiente enumeran Hola ASM cmdlets y sus nombres en el modo de hello ARM:

| Cmdlets de ASM | Cmdlets de ARM |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Add-AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Add-AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Add-AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Grant-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Grant-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Invoke-AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[New-AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[New-AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[New-AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[New-AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[New-AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[New-AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Revoke-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Revoke-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Use-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Wait-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>Nuevos cmdlets
los siguientes Hola son Hola nuevos cmdlets que solo están disponibles en el modo de hello ARM. 

**Cmdlets relacionados con acciones de script:**

* **Get-AzureRmHDInsightPersistedScriptAction**: Hola obtiene conserva las acciones de script para un clúster y muestra los resultados en orden cronológico u obtiene detalles de una acción de script persistentes especificado. 
* **Get-AzureRmHDInsightScriptActionHistory**: Obtiene el historial de acciones de script de Hola para un clúster y se enumeran en orden cronológico inverso u obtiene detalles de una acción de secuencia de comandos ejecutada anteriormente. 
* **Remove-AzureRmHDInsightPersistedScriptAction**: quita una acción de script persistente de un clúster de HDInsight.
* **Conjunto AzureRmHDInsightPersistedScriptAction**: establece un toobe de acción de secuencia de comandos ejecutada con anterioridad una acción de script persistentes.
* **AzureRmHDInsightScriptAction enviar**: envía un nuevo clúster de HDInsight de Azure de tooan de acción de secuencia de comandos. 

Para más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).

**Cmdlets relacionados con la identidad del clúster:**

* **AzureRmHDInsightClusterIdentity agregar**: agrega un objeto de configuración de clúster de clúster identidad tooa de modo que hello clúster de HDInsight puede tener acceso a almacenes de datos Lake de Azure. Consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).

### <a name="examples"></a>Ejemplos
**Crear clúster**

Comando anterior (ASM): 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

Nuevo comando (ARM):

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**Eliminación de clúster**

Comando anterior (ASM):

    Remove-AzureHDInsightCluster -name $clusterName 

Nuevo comando (ARM):

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**Enumeración de clústeres**

Comando anterior (ASM):

    Get-AzureHDInsightCluster

Nuevo comando (ARM):

    Get-AzureRmHDInsightCluster 

**Presentación de clústeres**

Comando anterior (ASM):

    Get-AzureHDInsightCluster -Name $clusterName

Nuevo comando (ARM):

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>Otros ejemplos
* [Creación de clústeres de HDInsight](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Envío de trabajos de Hive](hdinsight-hadoop-use-hive-powershell.md)
* [Envío de trabajos de Pig](hdinsight-hadoop-use-pig-powershell.md)
* [Envío de trabajos de Sqoop](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>Migrar toohello basado en ARM HDInsight .NET SDK
Hola basado en administración de servicios de Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) ahora está en desuso. Son toouse recomienda Hola basado en administración de recursos de Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx). Hello siguientes paquetes de HDInsight basados en ASM están en desuso.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

Esta sección proporciona punteros toomore información acerca de cómo tooperform determinada tareas mediante Hola SDK basado en ARM.

| Cómo... utilizando Hola basado en ARM SDK de HDInsight | Vínculos |
| --- | --- |
| Crear clústeres basados en Linux en HDInsight con el SDK de .NET |Consulte [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| Personalizar un clúster mediante una acción de script con el SDK de .NET |Consulte [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| Autenticar interactivamente aplicaciones mediante Azure Active Directory con el SDK de .NET |Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md). fragmento de código de Hello en este artículo utiliza el método de autenticación interactiva de Hola. |
| Autenticar aplicaciones de forma no interactiva mediante Azure Active Directory con el SDK de .NET |Consulte [Crear aplicaciones .NET para HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| Enviar un trabajo de Hive mediante el SDK de .NET |Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| Enviar un trabajo de Pig mediante el SDK de .NET |Consulte [Ejecución de trabajos de Pig con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| Enviar un trabajo de Sqoop mediante el SDK de .NET |Consulte [Ejecución de trabajos de Sqoop con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| Enumerar clústeres de HDInsight con el SDK. de .NET. |Consulte [Enumeración de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| Escalar clústeres de HDInsight con el SDK. de .NET. |Consulte [Escalamiento de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| Conceder o revocar acceso tooHDInsight clústeres con el SDK de .NET |Vea [tooHDInsight clústeres de conceder o revocar acceso](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| Actualizar las credenciales de usuario HTTP para clústeres de HDInsight mediante el SDK de .NET |Consulte [Actualización de las credenciales de usuario HTTP para clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| Buscar la cuenta de almacenamiento predeterminada de Hola para clústeres de HDInsight con el SDK de .NET |Vea [encontrar la cuenta de almacenamiento predeterminada de Hola para clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| Eliminar clústeres de HDInsight con el SDK de .NET. |Consulte [Eliminación de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>Ejemplos
Estos son algunos ejemplos de cómo es una operación efectúa a través de fragmento de código equivalentes de Hola y de saludo SDK de ASM de hello SDK basado en ARM.

**Creación de un cliente CRUD de clúster**

* Comando anterior (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* Nuevo comando (ARM) (autorización de la entidad de servicio)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* Nuevo comando (ARM) (autorización de usuario)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**Creación de un clúster**

* Comando anterior (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* Nuevo comando (ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**Habilitación del acceso HTTP**

* Comando anterior (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* Nuevo comando (ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**Eliminación de un cluster**

* Comando anterior (ASM)
  
        client.DeleteCluster(dnsName);
* Nuevo comando (ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

