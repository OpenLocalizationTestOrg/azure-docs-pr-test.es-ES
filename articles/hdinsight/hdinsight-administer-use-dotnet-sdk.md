---
title: "clústeres de aaaManage Hadoop en HDInsight con .NET SDK - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform administrativa tareas para hello clústeres de Hadoop en HDInsight con HDInsight .NET SDK."
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
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="d996e-103">Administración de clústeres de Hadoop en HDInsight con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="d996e-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="d996e-104">Obtenga información acerca de cómo usar los clústeres de toomanage HDInsight [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="d996e-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="d996e-105">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="d996e-105">**Prerequisites**</span></span>

<span data-ttu-id="d996e-106">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="d996e-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="d996e-107">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="d996e-107">**An Azure subscription**.</span></span> <span data-ttu-id="d996e-108">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d996e-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="d996e-109">Conectar tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d996e-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="d996e-110">Necesita Hola siguientes paquetes de Nuget:</span><span class="sxs-lookup"><span data-stu-id="d996e-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="d996e-111">Hello ejemplo de código siguiente muestra cómo tooconnect tooAzure antes de poder administrar HDInsight clústeres en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d996e-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
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
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="d996e-112">Al ejecutar este programa, verá un mensaje.</span><span class="sxs-lookup"><span data-stu-id="d996e-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="d996e-113">Si no desea que el símbolo del sistema de toosee hello, consulte [crear aplicaciones de .NET HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d996e-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="d996e-114">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="d996e-114">Create clusters</span></span>
<span data-ttu-id="d996e-115">Vea [basados en Linux crear clústeres de HDInsight utilizando Hola SDK para .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="d996e-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="d996e-116">Enumeración de clústeres</span><span class="sxs-lookup"><span data-stu-id="d996e-116">List clusters</span></span>
<span data-ttu-id="d996e-117">Hello fragmento de código siguiente enumera los clústeres y algunas propiedades:</span><span class="sxs-lookup"><span data-stu-id="d996e-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="d996e-118">Eliminación de clústeres</span><span class="sxs-lookup"><span data-stu-id="d996e-118">Delete clusters</span></span>
<span data-ttu-id="d996e-119">Usar hello siguiente fragmento de código toodelete un clúster de forma sincrónica o asincrónica:</span><span class="sxs-lookup"><span data-stu-id="d996e-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="d996e-120">Escalado de clústeres</span><span class="sxs-lookup"><span data-stu-id="d996e-120">Scale clusters</span></span>
<span data-ttu-id="d996e-121">característica de ajuste de escala de clúster de Hola permite toochange número de Hola de nodos de trabajador usado por un clúster que se ejecuta en HDInsight de Azure sin necesidad de toore-crear clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="d996e-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d996e-122">Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior.</span><span class="sxs-lookup"><span data-stu-id="d996e-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="d996e-123">Si no está seguro de la versión de Hola del clúster, puede comprobar la página de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="d996e-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="d996e-124">Consulte [Enumeración y visualización de clústeres](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="d996e-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="d996e-125">impacto de Hola de cambiar el número de Hola de nodos de datos para cada tipo de clúster compatible con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d996e-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="d996e-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="d996e-126">Hadoop</span></span>
  
    <span data-ttu-id="d996e-127">Perfectamente puede aumentar el número de Hola de nodos de trabajador en un clúster de Hadoop que se ejecuta sin afectar a los trabajos pendientes o en ejecución.</span><span class="sxs-lookup"><span data-stu-id="d996e-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="d996e-128">También se pueden enviar trabajos nuevos mientras Hola operación está en curso.</span><span class="sxs-lookup"><span data-stu-id="d996e-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="d996e-129">Errores en una operación de ajuste de escala se controlan correctamente para que hello clúster siempre se deja en un estado funcional.</span><span class="sxs-lookup"><span data-stu-id="d996e-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="d996e-130">Cuando un clúster de Hadoop es reducido reduciendo el número de Hola de nodos de datos, algunos de los servicios de hello en clúster de Hola se reinician.</span><span class="sxs-lookup"><span data-stu-id="d996e-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="d996e-131">Esto hace que ejecutan todos y pendiente de trabajos toofail al término de Hola Hola la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="d996e-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="d996e-132">Sin embargo, puede volver a enviar trabajos de hello una vez completada la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d996e-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="d996e-133">HBase</span><span class="sxs-lookup"><span data-stu-id="d996e-133">HBase</span></span>
  
    <span data-ttu-id="d996e-134">Sin problemas, puede agregar o quitar el clúster de HBase tooyour nodos mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="d996e-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="d996e-135">Los servidores regionales se equilibran automáticamente dentro de unos pocos minutos después de completar la operación de escalado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d996e-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="d996e-136">No obstante, puede equilibrar manualmente servidores regionales Hola iniciando sesión en el nodo principal de hello del clúster y ejecución Hola siguientes comandos de una ventana del símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="d996e-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="d996e-137">Storm</span><span class="sxs-lookup"><span data-stu-id="d996e-137">Storm</span></span>
  
    <span data-ttu-id="d996e-138">Sin problemas, puede agregar o quitar el clúster de Storm de tooyour de nodos de datos mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="d996e-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="d996e-139">Sin embargo, tras finalizar correctamente la operación de escalado de hello, debe topología de hello toorebalance.</span><span class="sxs-lookup"><span data-stu-id="d996e-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="d996e-140">Esto se puede realizar de dos formas:</span><span class="sxs-lookup"><span data-stu-id="d996e-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="d996e-141">La interfaz de usuario web de Storm</span><span class="sxs-lookup"><span data-stu-id="d996e-141">Storm web UI</span></span>
  * <span data-ttu-id="d996e-142">La herramienta de la interfaz de línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="d996e-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="d996e-143">Consulte toohello [documentación de Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="d996e-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="d996e-144">interfaz de usuario de web de Storm Hola está disponible en el clúster de HDInsight de hello:</span><span class="sxs-lookup"><span data-stu-id="d996e-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![Reequilibrio de escalado de HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="d996e-146">Este es un ejemplo cómo toouse Hola CLI comando topología de Storm Hola toorebalance:</span><span class="sxs-lookup"><span data-stu-id="d996e-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="d996e-147">Hola código fragmento siguiente muestra cómo tooresize un clúster de forma sincrónica o asincrónica:</span><span class="sxs-lookup"><span data-stu-id="d996e-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="d996e-148">Concesión o revocación del acceso</span><span class="sxs-lookup"><span data-stu-id="d996e-148">Grant/revoke access</span></span>
<span data-ttu-id="d996e-149">Clústeres de HDInsight tienen Hola después de servicios web HTTP (todos estos servicios tienen extremos RESTful):</span><span class="sxs-lookup"><span data-stu-id="d996e-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="d996e-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="d996e-150">ODBC</span></span>
* <span data-ttu-id="d996e-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="d996e-151">JDBC</span></span>
* <span data-ttu-id="d996e-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="d996e-152">Ambari</span></span>
* <span data-ttu-id="d996e-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="d996e-153">Oozie</span></span>
* <span data-ttu-id="d996e-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="d996e-154">Templeton</span></span>

<span data-ttu-id="d996e-155">De manera predeterminada, estos servicios se conceden para el acceso.</span><span class="sxs-lookup"><span data-stu-id="d996e-155">By default, these services are granted for access.</span></span> <span data-ttu-id="d996e-156">Puede revocar y conceder acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d996e-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="d996e-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="d996e-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="d996e-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="d996e-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="d996e-159">Por conceder o revocar el acceso de hello, se restablecerá la contraseña y el nombre de usuario del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d996e-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="d996e-160">Esto puede hacerse a través de hello Portal.</span><span class="sxs-lookup"><span data-stu-id="d996e-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="d996e-161">Vea [HDInsight administrar mediante el uso de Hola portal de Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="d996e-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="d996e-162">Actualización de las credenciales de usuario HTTP</span><span class="sxs-lookup"><span data-stu-id="d996e-162">Update HTTP user credentials</span></span>
<span data-ttu-id="d996e-163">Es Hola mismo procedimiento como [HTTP conceder o revocar acceso](#grant/revoke-access). Si se concedió clúster Hola Hola acceso HTTP, debe revocar primero.</span><span class="sxs-lookup"><span data-stu-id="d996e-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="d996e-164">Y, a continuación, conceder acceso de hello con nuevas credenciales de usuario HTTP.</span><span class="sxs-lookup"><span data-stu-id="d996e-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="d996e-165">Busque la cuenta de almacenamiento predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="d996e-165">Find hello default storage account</span></span>
<span data-ttu-id="d996e-166">Hola siguiente fragmento de código muestra cómo tooget nombre de cuenta de almacenamiento predeterminado de Hola y Hola clave de cuenta de almacenamiento predeterminada para un clúster.</span><span class="sxs-lookup"><span data-stu-id="d996e-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="d996e-167">Envío de trabajos</span><span class="sxs-lookup"><span data-stu-id="d996e-167">Submit jobs</span></span>
<span data-ttu-id="d996e-168">**trabajos de MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="d996e-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="d996e-169">Consulte [Ejecución de ejemplos de Hadoop en HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d996e-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="d996e-170">**trabajos de Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="d996e-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="d996e-171">Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d996e-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="d996e-172">**trabajos de Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="d996e-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="d996e-173">Consulte [Ejecución de trabajos de Pig con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d996e-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="d996e-174">**trabajos de Sqoop toosubmit**</span><span class="sxs-lookup"><span data-stu-id="d996e-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="d996e-175">Consulte [Uso de Sqoop con HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d996e-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="d996e-176">**trabajos de Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="d996e-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="d996e-177">Vea [Oozie de uso con Hadoop toodefine y ejecutar un flujo de trabajo en HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="d996e-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="d996e-178">Cargar el almacenamiento de blobs de datos tooAzure</span><span class="sxs-lookup"><span data-stu-id="d996e-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="d996e-179">Vea [cargar datos tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="d996e-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="d996e-180">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d996e-180">See Also</span></span>
* [<span data-ttu-id="d996e-181">Documentación de referencia del SDK de HDInsight</span><span class="sxs-lookup"><span data-stu-id="d996e-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="d996e-182">[Administrar HDInsight mediante Hola portal de Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="d996e-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="d996e-183">[Administración de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="d996e-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="d996e-184">[Creación de clústeres de HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="d996e-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="d996e-185">[Cargar datos tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d996e-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d996e-186">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d996e-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


