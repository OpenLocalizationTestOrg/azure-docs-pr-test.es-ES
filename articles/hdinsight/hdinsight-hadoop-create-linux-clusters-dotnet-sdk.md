---
title: "Creación de clústeres de Hadoop con NET - Azure HDInsight | Microsoft Docs"
description: "Aprenda a crear clústeres de Hadoop, HBase, Storm o Spark en Linux para HDInsight con el SDK .NET de HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9c74e3dc-837f-4c90-bbb1-489bc7124a3d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: ccd3a0c777510e0694170b2f9acc8da0e7dcde9b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-the-net-sdk"></a><span data-ttu-id="dfbe4-103">Crear clústeres basados en Linux en HDInsight con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="dfbe4-103">Create Linux-based clusters in HDInsight using the .NET SDK</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]


<span data-ttu-id="dfbe4-104">Aprenda a crear un clúster de Hadoop en un clúster de HDInsight de Azure mediante el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-104">Learn how to create a Hadoop cluster in Azure HDInsight cluster using the .NET SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfbe4-105">Los pasos descritos en este documento crean un clúster con un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-105">The steps in this document create a cluster with one worker node.</span></span> <span data-ttu-id="dfbe4-106">Si piensa crear más de 32 nodos de trabajo, ya sea al crear el clúster o al escalar el clúster después de crearlo, debe seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-106">If you plan on more than 32 worker nodes, either at cluster creation or by scaling the cluster after creation, you need to select a head node size with at least 8 cores and 14GB ram.</span></span>
>
> <span data-ttu-id="dfbe4-107">Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="dfbe4-107">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfbe4-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dfbe4-108">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="dfbe4-109">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-109">**An Azure subscription**.</span></span> <span data-ttu-id="dfbe4-110">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="dfbe4-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="dfbe4-111">Una **cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-111">**An Azure storage account**.</span></span> <span data-ttu-id="dfbe4-112">Vea [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="dfbe4-112">See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="dfbe4-113">**Visual Studio 2013, Visual Studio 2015 o Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-113">**Visual Studio 2013, Visual Studio 2015 or Visual Studio 2017**.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="dfbe4-114">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="dfbe4-114">Create clusters</span></span>

1. <span data-ttu-id="dfbe4-115">Abra Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-115">Open Visual Studio 2017.</span></span>
2. <span data-ttu-id="dfbe4-116">Cree una aplicación de consola nueva de Visual C#.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-116">Create a new Visual C# console application.</span></span>
3. <span data-ttu-id="dfbe4-117">En el menú **Herramientas**, haga clic en **Administrador de paquetes NuGet** y luego en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-117">From the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="dfbe4-118">Ejecute el siguiente comando en la consola para instalar los paquetes:</span><span class="sxs-lookup"><span data-stu-id="dfbe4-118">Run the following command in the console to install the packages:</span></span>

    ```powershell
    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight
    ```

    <span data-ttu-id="dfbe4-119">Estos comandos agregan las bibliotecas y referencias .NET al proyecto de Visual Studio actual.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-119">These commands add .NET libraries and references to them to the current Visual Studio project.</span></span>
5. <span data-ttu-id="dfbe4-120">En el Explorador de soluciones, haga doble clic en **Program.cs** para abrirlo, pegue el siguiente código y proporcione valores para las variables:</span><span class="sxs-lookup"><span data-stu-id="dfbe4-120">From Solution Explorer, double-click **Program.cs** to open it, paste the following code, and provide values for the variables:</span></span>

    ```csharp
    using System;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    namespace CreateHDInsightCluster
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;

            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            private const string ExistingResourceGroupName = "<Enter Resource Group Name>";
            private const string ExistingStorageName = "<Enter Default Storage Account Name>.blob.core.windows.net";
            private const string ExistingStorageKey = "<Enter Default Storage Account Key>";
            private const string ExistingBlobContainer = "<Enter Default Bob Container Name>";

            private const string NewClusterName = "<Enter HDInsight Cluster Name>";
            private const int NewClusterNumNodes = 2;
            private const string NewClusterLocation = "EAST US 2";     // Must be the same as the default Storage account
            private const OSType NewClusterOSType = OSType.Linux;
            private const string NewClusterType = "Hadoop";
            private const string NewClusterVersion = "3.5";
            private const string NewClusterUsername = "admin";
            private const string NewClusterPassword = "<Enter HTTP User Password>";
            private const string NewClusterSshUserName = "sshuser";

            // You can use eitehr password or public key. See https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix
            private const string NewClusterSshPassword = "<Enter SSH User Password>";
            private const string NewClusterSshPublicKey = @"---- BEGIN SSH2 PUBLIC KEY ----
                Comment: ""rsa-key-20150731""
                AAAAB3NzaC1yc2EAAAABJQAAAQEA4QiCRLqT7fnmUA5OhYWZNlZo6lLaY1c+IRsp
                gmPCsJVGQLu6O1wqcxRqiKk7keYq8bP5s30v6bIljsLZYTnyReNUa5LtFw7eauGr
                yVt3Pve6ejfWELhbVpi0iq8uJNFA9VvRkz8IP1JmjC5jsdnJhzQZtgkIrdn3w0e6
                WVfu15kKyY8YAiynVbdV51EB0SZaSLdMZkZQ81xi4DDtCZD7qvdtWEFwLa+EHdkd
                pzO36Mtev5XvseLQqzXzZ6aVBdlXoppGHXkoGHAMNOtEWRXpAUtEccjpATsaZhQR
                zZdZlzHduhM10ofS4YOYBADt9JohporbQVHM5w6qUhIgyiPo7w==
                ---- END SSH2 PUBLIC KEY ----"; //replace the public key with your own

            static void Main(string[] args)
            {
                System.Console.WriteLine("Creating a cluster.  The process takes 10 to 20 minutes ...");

                // Authenticate and get a token
                var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // Set parameters for the new cluster
                var parameters = new ClusterCreateParameters
                {
                    ClusterSizeInNodes = NewClusterNumNodes,
                    UserName = NewClusterUsername,
                    ClusterType = NewClusterType,
                    OSType = NewClusterOSType,
                    Version = NewClusterVersion,

                    // Use an Azure storage account as the default storage
                    DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

                    // Is the cluster type RServer? If so, you can set the EdgeNodeSize.
                    // Otherwise, the default VM size is used.
                    //EdgeNodeSize = "Standard_D12_v2",

                    Password = NewClusterPassword,
                    Location = NewClusterLocation,

                    SshUserName = NewClusterSshUserName,
                    SshPassword = NewClusterSshPassword,
                    //SshPublicKey = NewClusterSshPublicKey
                };

                // Is the cluster type RServer? If so, add the RStudio configuration option.
                /*
                parameters.Configurations.Add(
                    "rserver",
                    new Dictionary<string, string>()
                    {
                        { "rstudio", "true" }
                    }
                );
                */

                // Create the cluster
                _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

                System.Console.WriteLine("The cluster has been created. Press ENTER to continue ...");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials GetTokenCloudCredentials(string TenantId, string ClientId, string SubscriptionId)
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
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }
    ```

6. <span data-ttu-id="dfbe4-121">Reemplace los valores de miembro de clase.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-121">Replace the class member values.</span></span>
7. <span data-ttu-id="dfbe4-122">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-122">Press **F5** to run the application.</span></span> <span data-ttu-id="dfbe4-123">Una ventana de consola se abrirá y mostrará el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-123">A console window should open and display the status of the application.</span></span> <span data-ttu-id="dfbe4-124">Se le pedirá que escriba las credenciales de la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-124">You are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="dfbe4-125">La creación del clúster de HDInsight puede durar varios minutos, normalmente unos 15.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-125">It can take several minutes to create an HDInsight cluster, normally around 15.</span></span>

## <a name="use-bootstrap"></a><span data-ttu-id="dfbe4-126">Uso de bootstrap</span><span class="sxs-lookup"><span data-stu-id="dfbe4-126">Use bootstrap</span></span>

<span data-ttu-id="dfbe4-127">Mediante bootstrap puede configurar opciones adicionales durante las operaciones de creación de clúster.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-127">Using bootstrap, you can configure addition settings during the cluster creations.</span></span>  <span data-ttu-id="dfbe4-128">Para más información, consulte [Personalización de los clústeres de HDInsight con Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span><span class="sxs-lookup"><span data-stu-id="dfbe4-128">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

<span data-ttu-id="dfbe4-129">Modifique el ejemplo para [crear clústeres](#create-clusters) a fin de configurar un valor de Hive:</span><span class="sxs-lookup"><span data-stu-id="dfbe4-129">Modify the sample in [Create clusters](#create-clusters) to configure a Hive setting:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  The process takes 10 to 20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for the new cluster
    var extendedParameters = new ClusterCreateParametersExtended
    {
        Location = NewClusterLocation,
        Properties = new ClusterCreateProperties
        {
            ClusterDefinition = new ClusterDefinition
            {
                ClusterType = NewClusterType.ToString()
            },
            ClusterVersion = NewClusterVersion,
            OperatingSystemType = NewClusterOSType
        }
    };

    var coreConfigs = new Dictionary<string, string>
    {
        {"fs.defaultFS", string.Format("wasb://{0}@{1}", ExistingBlobContainer, ExistingStorageName)},
        {
            string.Format("fs.azure.account.key.{0}", ExistingStorageName),
            ExistingStorageKey
        }
    };

    // bootstrap
    var hiveConfigs = new Dictionary<string, string>
    {
        { "hive.metastore.client.socket.timeout", "90"}
    };

    var gatewayConfigs = new Dictionary<string, string>
    {
        {"restAuthCredential.isEnabled", "true"},
        {"restAuthCredential.username", NewClusterUsername},
        {"restAuthCredential.password", NewClusterPassword}
    };

    var configurations = new Dictionary<string, Dictionary<string, string>>
    {
        {"core-site", coreConfigs},
        {"gateway", gatewayConfigs},
        {"hive-site", hiveConfigs}
    };

    var serializedConfig = JsonConvert.SerializeObject(configurations);
    extendedParameters.Properties.ClusterDefinition.Configurations = serializedConfig;

    var sshPublicKeys = new List<SshPublicKey>();
    var sshPublicKey = new SshPublicKey
    {
        CertificateData =
            string.Format("ssh-rsa {0}", NewClusterSshPublicKey)
    };
    sshPublicKeys.Add(sshPublicKey);

    var headNode = new Role
    {
        Name = "headnode",
        TargetInstanceCount = 2,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                // When use a SSH pulbic key, make sure to remove comments, headers and trailers, and concatenate the key into one line 
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    var workerNode = new Role
    {
        Name = "workernode",
        TargetInstanceCount = NewClusterNumNodes,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    extendedParameters.Properties.ComputeProfile = new ComputeProfile();
    extendedParameters.Properties.ComputeProfile.Roles.Add(headNode);
    extendedParameters.Properties.ComputeProfile.Roles.Add(workerNode);

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, extendedParameters);

    System.Console.WriteLine("The cluster has been created. Press ENTER to continue ...");
    System.Console.ReadLine();
}
```

## <a name="use-script-action"></a><span data-ttu-id="dfbe4-130">Uso de la acción de scripts</span><span class="sxs-lookup"><span data-stu-id="dfbe4-130">Use Script Action</span></span>

<span data-ttu-id="dfbe4-131">Con la acción de scripts puede configurar opciones adicionales durante las operaciones de creación de clúster.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-131">Using Script Action, you can configure additional settings during cluster creations.</span></span>  <span data-ttu-id="dfbe4-132">Para más información, vea [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dfbe4-132">For more information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="dfbe4-133">Modifique el ejemplo para [crear clústeres](#create-clusters) a fin de llamar a una acción de scripts para instalar R:</span><span class="sxs-lookup"><span data-stu-id="dfbe4-133">Modify the sample in [Create clusters](#create-clusters) to call a Script Action to install R:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  The process takes 10 to 20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for the new cluster
    var parameters = new ClusterCreateParameters
    {
        ClusterSizeInNodes = NewClusterNumNodes,
        Location = NewClusterLocation,
        ClusterType = NewClusterType,
        OSType = NewClusterOSType,
        Version = NewClusterVersion,

        DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

        UserName = NewClusterUsername,
        Password = NewClusterPassword,
        SshUserName = NewClusterSshUserName,
        SshPublicKey = NewClusterSshPublicKey
    };

    ScriptAction rScriptAction = new ScriptAction("Install R",
        new Uri("https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh"), "");

    parameters.ScriptActions.Add(ClusterNodeType.HeadNode,new System.Collections.Generic.List<ScriptAction> { rScriptAction});
    parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { rScriptAction });

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

    System.Console.WriteLine("The cluster has been created. Press ENTER to continue ...");
    System.Console.ReadLine();
}
```

## <a name="troubleshoot"></a><span data-ttu-id="dfbe4-134">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="dfbe4-134">Troubleshoot</span></span>

<span data-ttu-id="dfbe4-135">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="dfbe4-135">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfbe4-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dfbe4-136">Next steps</span></span>
<span data-ttu-id="dfbe4-137">Ahora que ya creó un clúster de HDInsight correctamente, use lo siguiente para aprender a trabajar con el clúster.</span><span class="sxs-lookup"><span data-stu-id="dfbe4-137">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span> 

### <a name="hadoop-clusters"></a><span data-ttu-id="dfbe4-138">Clústeres Hadoop</span><span class="sxs-lookup"><span data-stu-id="dfbe4-138">Hadoop clusters</span></span>
* [<span data-ttu-id="dfbe4-139">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-139">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="dfbe4-140">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-140">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="dfbe4-141">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-141">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="dfbe4-142">Clústeres HBase</span><span class="sxs-lookup"><span data-stu-id="dfbe4-142">HBase clusters</span></span>
* [<span data-ttu-id="dfbe4-143">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-143">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="dfbe4-144">Desarrollo de aplicaciones de Java para HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-144">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="dfbe4-145">Clústeres Storm</span><span class="sxs-lookup"><span data-stu-id="dfbe4-145">Storm clusters</span></span>
* [<span data-ttu-id="dfbe4-146">Desarrollo de topologías de Java para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-146">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="dfbe4-147">Uso de componentes de Python en Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-147">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="dfbe4-148">Implementación y supervisión de topologías con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfbe4-148">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="dfbe4-149">Clústeres de Spark</span><span class="sxs-lookup"><span data-stu-id="dfbe4-149">Spark clusters</span></span>
* [<span data-ttu-id="dfbe4-150">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="dfbe4-150">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="dfbe4-151">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="dfbe4-151">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="dfbe4-152">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="dfbe4-152">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="dfbe4-153">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="dfbe4-153">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="dfbe4-154">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="dfbe4-154">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="run-jobs"></a><span data-ttu-id="dfbe4-155">Ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="dfbe4-155">Run jobs</span></span>
* [<span data-ttu-id="dfbe4-156">Run Hive jobs in HDInsight using .NET SDK (Ejecución de trabajos de Hive en HDInsight mediante el SDK de .NET)</span><span class="sxs-lookup"><span data-stu-id="dfbe4-156">Run Hive jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="dfbe4-157">Run Pig jobs in HDInsight using .NET SDK (Ejecución de trabajos de Pig en HDInsight mediante el SDK de .NET)</span><span class="sxs-lookup"><span data-stu-id="dfbe4-157">Run Pig jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
* [<span data-ttu-id="dfbe4-158">Run Sqoop jobs in HDInsight using .NET SDK (Ejecución de trabajos de Sqoop en HDInsight mediante el SDK de .NET)</span><span class="sxs-lookup"><span data-stu-id="dfbe4-158">Run Sqoop jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
* [<span data-ttu-id="dfbe4-159">Run Oozie jobs in HDInsightt (Ejecución de trabajos de Oozie en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="dfbe4-159">Run Oozie jobs in HDInsight</span></span>](hdinsight-use-oozie.md)

