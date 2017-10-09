---
title: consultas de Hive aaaRun con HDInsight .NET SDK - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosubmit Hadoop trabajos tooAzure Hadoop de HDInsight con HDInsight .NET SDK."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="ddb3b-103">Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ddb3b-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ddb3b-104">Obtenga información acerca de cómo las consultas que utilizan el SDK de HDInsight .NET toosubmit Hive.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-104">Learn how toosubmit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="ddb3b-105">Escribir un programa de C# toosubmit una consulta de Hive para enumerar tablas de Hive y mostrar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-105">You write a C# program toosubmit a Hive query for listing Hive tables, and display hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="ddb3b-106">pasos de Hello en este artículo deben realizarse desde un cliente de Windows.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-106">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="ddb3b-107">Para obtener información sobre cómo usar un Linux, OS X o toowork de cliente de Unix con Hive, utilice tabulador Hola que se muestra en la parte superior de Hola de artículo Hola.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-107">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ddb3b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ddb3b-108">Prerequisites</span></span>
<span data-ttu-id="ddb3b-109">Antes de comenzar este artículo, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ddb3b-109">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="ddb3b-110">**Un clúster de Hadoop en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="ddb3b-111">Consulte [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ddb3b-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="ddb3b-112">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="ddb3b-113">Envío de trabajos de Hive mediante el SDK de .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ddb3b-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="ddb3b-114">Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-114">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="ddb3b-115">**trabajos de tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="ddb3b-115">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="ddb3b-116">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="ddb3b-117">Desde la consola de administrador de paquetes de Nuget hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ddb3b-117">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="ddb3b-118">Usar hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="ddb3b-118">Use hello following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="ddb3b-119">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-119">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="ddb3b-120">salida de Hello de aplicación hello será similar al:</span><span class="sxs-lookup"><span data-stu-id="ddb3b-120">hello output of hello application shall be similar to:</span></span>

![Salida de trabajo de Hive para Hadoop en HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="ddb3b-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ddb3b-122">Next steps</span></span>
<span data-ttu-id="ddb3b-123">En este artículo, ha aprendido varias formas toocreate un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ddb3b-123">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="ddb3b-124">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="ddb3b-124">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="ddb3b-125">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="ddb3b-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="ddb3b-126">[Creación de clústeres de Hadoop en HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="ddb3b-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="ddb3b-127">Administrar clústeres de Hadoop en HDInsight con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ddb3b-127">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="ddb3b-128">Referencia del SDK de .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ddb3b-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="ddb3b-129">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="ddb3b-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ddb3b-130">Uso de Sqoop con HDInsight</span><span class="sxs-lookup"><span data-stu-id="ddb3b-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="ddb3b-131">Crear aplicaciones .NET para HDInsight de autenticación no interactiva</span><span class="sxs-lookup"><span data-stu-id="ddb3b-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


