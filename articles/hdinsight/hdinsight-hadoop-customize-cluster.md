---
title: "uso de clústeres de HDInsight de aaaCustomize script acciones - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize HDInsight clústeres utilizando la acción de secuencia de comandos."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>Personalización de clústeres de HDInsight mediante la acción de scripts (Windows)
**Acción de secuencia de comandos** puede ser usado tooinvoke [scripts personalizados](hdinsight-hadoop-script-actions.md) durante el proceso de creación de clúster de Hola para instalar software adicional en un clúster.

información de Hello en este artículo es específicos clústeres de HDInsight basados en tooWindows. Para obtener más información sobre clústeres basados en Linux, vea [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Clústeres de HDInsight pueden personalizarse en una variedad de otras maneras, como la inclusión de las cuentas de almacenamiento de Azure adicionales, cambiar hello Hadoop (core-site.xml, hive-site.xml, etc.) de los archivos de configuración o agregar compartidas bibliotecas (p. ej., Hive y Oozie) en ubicaciones comunes en clúster de Hola. Estas personalizaciones pueden hacerse a través de PowerShell de Azure, hello Azure HDInsight .NET SDK, u Hola portal de Azure. Para obtener más información, consulte [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Acción de secuencia de comandos en el proceso de creación de clúster de Hola
Generar script de acción solo se usa cuando un clúster está en proceso de Hola de que se está creando. Hello siguiente diagrama se muestra cuando se ejecuta la acción de secuencia de comandos durante el proceso de creación de hello:

![Fases y personalización de clústeres de HDInsight durante la creación de clústeres][img-hdi-cluster-states]

Cuando se ejecuta el script de Hola, clúster de hello entra en hello **ClusterCustomization** fase. En esta fase, Hola script se ejecuta bajo la cuenta de administrador del sistema de hello, en paralelo en todos los Hola especificado nodos de clúster de Hola y proporciona privilegios de administrador total en nodos de Hola.

> [!NOTE]
> Dado que tiene privilegios de administrador en los nodos de clúster de Hola durante el **ClusterCustomization** fase, puede utilizar operaciones de tooperform de script de Hola como detener e iniciar servicios, incluidos los servicios relacionados con Hadoop. Por lo tanto, como parte del script de Hola, debe asegurarse de esa hello Ambari servicios y otros servicios relacionados con Hadoop están activados y ejecutándose antes de que finaliza la ejecución de script de Hola. Estos servicios son necesarios toosuccessfully determinar Hola mantenimiento y el estado del clúster de hello mientras se está creando. Si cambia cualquier configuración en el clúster que afecta a estos servicios, debe utilizar las funciones de aplicación auxiliar de Hola que se proporcionan. Para obtener más información sobre las funciones auxiliares, consulte [Desarrollo de la acción de script con HDInsight][hdinsight-write-script].
>
>

salida de Hello y registros de errores de Hola para script de Hola se almacenan en la cuenta de almacenamiento predeterminada de Hola que especificó para el clúster de Hola. Hello registros almacenan en una tabla con nombre de hello **u < \cluster-name-fragment >< \time-stamp > setuplog**. Se trata de registros agregados desde un script de Hola ejecutar en todos los nodos de hello (nodo principal y nodos de trabajador) en clúster de Hola.

Cada clúster puede aceptar varias acciones de script que se invocan en orden de hello en el que se especifican. Una secuencia de comandos se pueda ejecutar en el nodo principal de hello, nodos de trabajador de Hola o ambos.

HDInsight proporciona varios Hola de tooinstall de secuencias de comandos de los componentes siguientes en clústeres de HDInsight:

| Nombre | Script |
| --- | --- |
| **Instalar Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Vea [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]. |
| **Instalar R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Consulte [Instalación y uso de R en clústeres de HDInsight][hdinsight-install-r]. |
| **Instalar Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Vea [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Instalar Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Vea [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md). |
| **Carga previa de las bibliotecas de Hive** |https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1. Vea [Incorporación de bibliotecas de Hive durante la creación de clústeres de HDInsight](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Llamar a secuencias de comandos mediante Hola portal de Azure
**De hello portal de Azure**

1. Comience a crear un clúster, tal y como se describe en [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
2. En configuración opcional para hello **acciones de Script** hoja, haga clic en **Agregar acción de secuencia de comandos** tooprovide detalles sobre la acción de secuencia de comandos de hello, tal y como se muestra a continuación:

    ![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize de acción de secuencia de comandos de uso un clúster")

    <table border='1'>
        <tr><th>Propiedad</th><th>Valor</th></tr>
        <tr><td>Nombre</td>
            <td>Especifique un nombre para la acción de secuencia de comandos de Hola.</td></tr>
        <tr><td>Identificador URI de script</td>
            <td>Especifique Hola URI toohello script que es invocado toocustomize Hola clúster. s</td></tr>
        <tr><td>Head/Worker</td>
            <td>Especifique los nodos de hello (**Head** o **trabajo**) en qué personalización Hola se ejecuta el script.</b>.
        <tr><td>parameters</td>
            <td>Especificar parámetros de hello, si así lo requiere el script de Hola.</td></tr>
    </table>

    Presione ENTRAR tooadd más de una secuencia de comandos acción tooinstall varios componentes de clúster de Hola.
3. Haga clic en **seleccione** toosave Hola configuración de acción de secuencia de comandos y continuar con la creación del clúster.

## <a name="call-scripts-using-azure-powershell"></a>Llamada a scripts con Azure PowerShell
Este script de PowerShell siguiente muestra cómo tooinstall Spark en Windows en la función de clúster de HDInsight.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall otro software, deberá tooreplace archivo de script de Hola en script de Hola:

Cuando se le solicite, escriba credenciales de hello para el clúster de Hola. Puede tardar varios minutos antes de que se crea un clúster Hola.

## <a name="call-scripts-using-net-sdk"></a>Llamada a scripts mediante .NET SDK
Hello en el ejemplo siguiente se muestra cómo tooinstall Spark en Windows en la función de clúster de HDInsight. tooinstall otro software, deberá tooreplace archivo de script de hello en el código de hello.

**un clúster de HDInsight con Spark toocreate**

1. Cree una aplicación de consola en C# mediante Visual Studio.
2. Desde la consola de administrador de paquetes de Nuget hello, ejecute hello siguiente comando.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Hola de uso después de usar las instrucciones en el archivo Program.cs de hello:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Coloque el código de hello en clase hello con siguiente hello:

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. Presione **F5** aplicación de hello toorun.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Soporte técnico para el software de código abierto utilizado en clústeres de HDInsight
Hola servicio HDInsight de Azure de Microsoft es una plataforma flexible que permite toobuild aplicaciones de grandes cantidades de datos en la nube de hello mediante el uso de un ecosistema de tecnologías de código abierto formado alrededor de Hadoop. Microsoft Azure proporciona un nivel de compatibilidad general para las tecnologías de código abierto, como se describe en hello **admite ámbito** sección de hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">sitio Web de preguntas frecuentes de soporte de Azure</a>. Hola servicio HDInsight proporciona un nivel adicional de compatibilidad con algunos componentes de hello, tal y como se describe a continuación.

Hay dos tipos de componentes de código abierto que están disponibles en hello servicio HDInsight:

* **Componentes integrados** -estos componentes se instalan previamente en clústeres de HDInsight y proporcionan la funcionalidad básica de clúster de Hola. Por ejemplo, ResourceManager hilo, lenguaje de consulta de Hive hello (HiveQL) y biblioteca de Mahout Hola pertenecen toothis categoría. Una lista completa de componentes del clúster está disponible en [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?](hdinsight-component-versioning.md) </a>.
* **Componentes personalizados** -, como un usuario del clúster hello, puede instalar o usar en la carga de trabajo cualquier componente disponible en la Comunidad de Hola o creado por el usuario.

Componentes integrados son totalmente compatibles, y Microsoft Support le ayudarán tooisolate y resolver los problemas relacionados toothese componentes.

> [!WARNING]
> Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles y Microsoft Support le ayudarán tooisolate y resolver los problemas relacionados toothese componentes.
>
> Componentes personalizados reciben soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola. Esto podría producir en resolver el problema de hello ni pedir que tooengage canales disponibles para hello abrir tecnologías de origen donde se encuentra la amplia experiencia para que la tecnología. Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Además, los proyectos de Apache tienen sitios del proyecto en [http://apache.org](http://apache.org), por ejemplo, [Hadoop](http://hadoop.apache.org/) y [Spark](http://spark.apache.org/).
>
>

Hola servicio HDInsight proporciona varias maneras de componentes personalizados de toouse. Independientemente de cómo un componente se utiliza o instalado en el clúster de hello, hello mismo nivel de compatibilidad se aplica. A continuación se muestra una lista de las maneras más habituales de Hola que los componentes personalizados pueden utilizarse en clústeres de HDInsight:

1. Envío de trabajos - Hadoop u otros tipos de trabajos que se ejecutan o utilizan componentes personalizados pueden clúster toohello enviado.
2. Personalización de clúster - durante la creación del clúster, puede especificar opciones de configuración adicionales y componentes personalizados que se instalarán en los nodos de clúster de Hola.
3. Ejemplos: para componentes personalizados populares, Microsoft y otros elementos pueden proporcionar ejemplos de cómo se pueden usar estos componentes en clústeres de HDInsight Hola. Estas muestras se proporcionan sin soporte técnico.

## <a name="develop-script-action-scripts"></a>Desarrollo de scripts de acción de script
Consulte [Desarrollo de scripts de acciones de script con HDInsight][hdinsight-write-script].

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
