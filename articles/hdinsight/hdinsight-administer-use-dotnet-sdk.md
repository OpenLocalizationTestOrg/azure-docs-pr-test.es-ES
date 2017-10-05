---
title: "Administración de clústeres de Hadoop en HDInsight con el SDK de .NET: Azure | Microsoft Docs"
description: "Aprenda a realizar tareas administrativas para clústeres de Hadoop en HDInsight mediante el SDK de .NET en HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="75546-103">Administración de clústeres de Hadoop en HDInsight con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="75546-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="75546-104">Más información sobre cómo administrar los clústeres de HDInsight con el [SDK de .NET de HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="75546-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="75546-105">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="75546-105">**Prerequisites**</span></span>

<span data-ttu-id="75546-106">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="75546-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="75546-107">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="75546-107">**An Azure subscription**.</span></span> <span data-ttu-id="75546-108">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="75546-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="75546-109">Conexión a HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="75546-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="75546-110">Necesita los siguientes paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="75546-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="75546-111">El ejemplo de código siguiente muestra cómo conectarse a Azure antes de poder administrar clústeres de HDInsight con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="75546-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
            /// </summary>
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
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="75546-112">Al ejecutar este programa, verá un mensaje.</span><span class="sxs-lookup"><span data-stu-id="75546-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="75546-113">Si no desea ver el mensaje, consulte [Crear aplicaciones .NET para HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="75546-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="75546-114">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="75546-114">Create clusters</span></span>
<span data-ttu-id="75546-115">Vea [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="75546-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="75546-116">Enumeración de clústeres</span><span class="sxs-lookup"><span data-stu-id="75546-116">List clusters</span></span>
<span data-ttu-id="75546-117">El fragmento de código siguiente enumera los clústeres y algunas propiedades:</span><span class="sxs-lookup"><span data-stu-id="75546-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="75546-118">Eliminación de clústeres</span><span class="sxs-lookup"><span data-stu-id="75546-118">Delete clusters</span></span>
<span data-ttu-id="75546-119">Use el siguiente fragmento de código para eliminar un clúster de forma sincrónica o asincrónica:</span><span class="sxs-lookup"><span data-stu-id="75546-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="75546-120">Escalado de clústeres</span><span class="sxs-lookup"><span data-stu-id="75546-120">Scale clusters</span></span>
<span data-ttu-id="75546-121">La característica de escalado de clústeres permite cambiar la cantidad de nodos de trabajo que usa un clúster que se ejecuta en HDInsight de Azure sin necesidad de volver a crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="75546-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="75546-122">Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior.</span><span class="sxs-lookup"><span data-stu-id="75546-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="75546-123">Si no está seguro de la versión del clúster, puede comprobar la página de propiedades.</span><span class="sxs-lookup"><span data-stu-id="75546-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="75546-124">Vea [Enumeración y visualización de clústeres](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="75546-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="75546-125">A continuación se muestra el efecto que tiene cambiar la cantidad de nodos de datos de cada tipo de clúster compatible con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="75546-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="75546-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="75546-126">Hadoop</span></span>
  
    <span data-ttu-id="75546-127">Puede aumentar sin ningún problema la cantidad de nodos de trabajo en un clúster de Hadoop que se encuentre en ejecución, sin que afecte a ningún trabajo pendiente o en ejecución.</span><span class="sxs-lookup"><span data-stu-id="75546-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="75546-128">También se pueden enviar trabajos nuevos mientras la operación está en curso.</span><span class="sxs-lookup"><span data-stu-id="75546-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="75546-129">Los errores que puedan surgir en una operación de escalado se enfrentan oportunamente, por lo que el clúster siempre queda en estado funcional.</span><span class="sxs-lookup"><span data-stu-id="75546-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="75546-130">Cuando se realiza la reducción vertical de un clúster de Hadoop al disminuir la cantidad de nodos de datos, se reinician algunos de los servicios del clúster.</span><span class="sxs-lookup"><span data-stu-id="75546-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="75546-131">Esto provoca que todos los trabajos pendientes y en ejecución fallen al completarse la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="75546-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="75546-132">Sin embargo, puede volver a enviar los trabajos una vez finalizada la operación.</span><span class="sxs-lookup"><span data-stu-id="75546-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="75546-133">HBase</span><span class="sxs-lookup"><span data-stu-id="75546-133">HBase</span></span>
  
    <span data-ttu-id="75546-134">Puede agregar nodos sin problemas al clúster de HBase mientras se encuentra en ejecución, así como eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="75546-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="75546-135">Los servidores regionales se equilibran automáticamente en unos pocos minutos tras completar la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="75546-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="75546-136">Sin embargo, puede equilibrar manualmente los servidores regionales iniciando sesión en el nodo principal del clúster y ejecutando los comandos siguientes desde una ventana del símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="75546-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="75546-137">Storm</span><span class="sxs-lookup"><span data-stu-id="75546-137">Storm</span></span>
  
    <span data-ttu-id="75546-138">Puede agregar o quitar sin problemas nodos de datos de su clúster de Storm mientras se encuentra en ejecución.</span><span class="sxs-lookup"><span data-stu-id="75546-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="75546-139">Sin embargo, después de finalizar correctamente la operación de escalado, deberá volver a equilibrar la topología.</span><span class="sxs-lookup"><span data-stu-id="75546-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="75546-140">Esto se puede realizar de dos formas:</span><span class="sxs-lookup"><span data-stu-id="75546-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="75546-141">La interfaz de usuario web de Storm</span><span class="sxs-lookup"><span data-stu-id="75546-141">Storm web UI</span></span>
  * <span data-ttu-id="75546-142">La herramienta de la interfaz de línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="75546-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="75546-143">Consulte la [documentación de Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="75546-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="75546-144">La interfaz de usuario web de Storm se encuentra disponible en el clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="75546-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![Reequilibrio de escalado de HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="75546-146">El siguiente es un ejemplo de cómo usar el comando CLI para volver a equilibrar la topología de Storm:</span><span class="sxs-lookup"><span data-stu-id="75546-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="75546-147">El fragmento de código siguiente muestra cómo cambiar el tamaño de un clúster de forma sincrónica o asincrónica:</span><span class="sxs-lookup"><span data-stu-id="75546-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="75546-148">Concesión o revocación del acceso</span><span class="sxs-lookup"><span data-stu-id="75546-148">Grant/revoke access</span></span>
<span data-ttu-id="75546-149">Los clústeres de HDInsight tienen los siguientes servicios web HTTP (todos estos servicios tienen extremos RESTful):</span><span class="sxs-lookup"><span data-stu-id="75546-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="75546-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="75546-150">ODBC</span></span>
* <span data-ttu-id="75546-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="75546-151">JDBC</span></span>
* <span data-ttu-id="75546-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="75546-152">Ambari</span></span>
* <span data-ttu-id="75546-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="75546-153">Oozie</span></span>
* <span data-ttu-id="75546-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="75546-154">Templeton</span></span>

<span data-ttu-id="75546-155">De manera predeterminada, estos servicios se conceden para el acceso.</span><span class="sxs-lookup"><span data-stu-id="75546-155">By default, these services are granted for access.</span></span> <span data-ttu-id="75546-156">Puede revocar/conceder el acceso.</span><span class="sxs-lookup"><span data-stu-id="75546-156">You can revoke/grant the access.</span></span> <span data-ttu-id="75546-157">Para revocar:</span><span class="sxs-lookup"><span data-stu-id="75546-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="75546-158">Para conceder:</span><span class="sxs-lookup"><span data-stu-id="75546-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="75546-159">Al conceder/revocar el acceso, restablecerá el nombre de usuario y la contraseña del clúster.</span><span class="sxs-lookup"><span data-stu-id="75546-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="75546-160">Esto también se puede hacer a través del Portal.</span><span class="sxs-lookup"><span data-stu-id="75546-160">This can also be done via the Portal.</span></span> <span data-ttu-id="75546-161">Consulte [Administración de HDInsight mediante Azure Portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="75546-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="75546-162">Actualización de las credenciales de usuario HTTP</span><span class="sxs-lookup"><span data-stu-id="75546-162">Update HTTP user credentials</span></span>
<span data-ttu-id="75546-163">Es el mismo procedimiento que [Concesión o revocación del acceso HTTP](#grant/revoke-access). Si al clúster se le ha concedido el acceso HTTP, primero debe revocarlo.</span><span class="sxs-lookup"><span data-stu-id="75546-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="75546-164">Y después conceda el acceso con nuevas credenciales de usuario HTTP.</span><span class="sxs-lookup"><span data-stu-id="75546-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="75546-165">Búsqueda de la cuenta de almacenamiento predeterminada</span><span class="sxs-lookup"><span data-stu-id="75546-165">Find the default storage account</span></span>
<span data-ttu-id="75546-166">El siguiente fragmento de código muestra cómo obtener el nombre y la clave de la cuenta de almacenamiento predeterminada para un clúster.</span><span class="sxs-lookup"><span data-stu-id="75546-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="75546-167">Envío de trabajos</span><span class="sxs-lookup"><span data-stu-id="75546-167">Submit jobs</span></span>
<span data-ttu-id="75546-168">**Para enviar trabajos de MapReduce**</span><span class="sxs-lookup"><span data-stu-id="75546-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="75546-169">Consulte [Ejecución de ejemplos de Hadoop en HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="75546-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="75546-170">**Para enviar trabajos de Hive**</span><span class="sxs-lookup"><span data-stu-id="75546-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="75546-171">Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="75546-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="75546-172">**Para enviar trabajos de Pigs**</span><span class="sxs-lookup"><span data-stu-id="75546-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="75546-173">Consulte [Ejecución de trabajos de Pig con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="75546-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="75546-174">**Para enviar trabajos de Sqoop**</span><span class="sxs-lookup"><span data-stu-id="75546-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="75546-175">Consulte [Uso de Sqoop con HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="75546-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="75546-176">**Para enviar trabajos de Oozie**</span><span class="sxs-lookup"><span data-stu-id="75546-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="75546-177">Vea [Uso de Oozie con Hadoop para definir y ejecutar un flujo de trabajo en HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="75546-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="75546-178">Carga de archivos de datos al almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="75546-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="75546-179">Consulte [Carga de datos en HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="75546-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="75546-180">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="75546-180">See Also</span></span>
* [<span data-ttu-id="75546-181">Documentación de referencia del SDK de HDInsight</span><span class="sxs-lookup"><span data-stu-id="75546-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="75546-182">[Administración de HDInsight mediante Azure Portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="75546-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="75546-183">[Administración de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="75546-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="75546-184">[Creación de clústeres de HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="75546-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="75546-185">[Carga de datos en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="75546-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="75546-186">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="75546-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


