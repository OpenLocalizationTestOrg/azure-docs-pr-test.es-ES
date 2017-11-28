---
title: trabajos de MapReduce aaaSubmit con HDInsight .NET SDK - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosubmit MapReduce trabajos tooAzure Hadoop de HDInsight con HDInsight .NET SDK."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="45241-103">Envío de trabajos de MapReduce mediante el SDK .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="45241-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="45241-104">Obtenga información acerca de cómo toosubmit MapReduce trabajos usando HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="45241-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="45241-105">Los clústeres de HDInsight vienen con un archivo .jar con varios ejemplos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="45241-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="45241-106">es el archivo jar de Hello */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="45241-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="45241-107">Uno de los ejemplos de hello es *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="45241-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="45241-108">Desarrollar un toosubmit de aplicación de consola un trabajo wordcount de C#.</span><span class="sxs-lookup"><span data-stu-id="45241-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="45241-109">trabajo de Hello lee hello */example/data/gutenberg/davinci.txt* archivo y las salidas Hola resultados demasiado*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="45241-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="45241-110">Si desea que la aplicación de hello toorerun, debe limpiar la carpeta de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="45241-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="45241-111">pasos de Hello en este artículo deben realizarse desde un cliente de Windows.</span><span class="sxs-lookup"><span data-stu-id="45241-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="45241-112">Para obtener información sobre cómo usar un Linux, OS X o toowork de cliente de Unix con Hive, utilice tabulador Hola que se muestra en la parte superior de Hola de artículo Hola.</span><span class="sxs-lookup"><span data-stu-id="45241-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="45241-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="45241-113">Prerequisites</span></span>
<span data-ttu-id="45241-114">Antes de comenzar este artículo, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="45241-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="45241-115">**Un clúster de Hadoop en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="45241-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="45241-116">Consulte [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45241-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="45241-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="45241-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="45241-118">Envío de trabajos de MapReduce mediante el SDK .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="45241-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="45241-119">Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET.</span><span class="sxs-lookup"><span data-stu-id="45241-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="45241-120">**trabajos de tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="45241-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="45241-121">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45241-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="45241-122">Desde la consola de administrador de paquetes de Nuget hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="45241-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="45241-123">Usar hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="45241-123">Use hello following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="45241-124">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="45241-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="45241-125">trabajo de toorun Hola de nuevo, debe cambiar nombre de carpeta de salida de hello trabajo, en el ejemplo hello, es "/ datos de ejemplo/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="45241-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="45241-126">Cuando se completa correctamente el trabajo de hello, aplicación hello imprime el contenido de Hola Hola del archivo de salida "parte-r-00000".</span><span class="sxs-lookup"><span data-stu-id="45241-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="45241-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45241-127">Next steps</span></span>
<span data-ttu-id="45241-128">En este artículo, ha aprendido varias formas toocreate un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="45241-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="45241-129">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="45241-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="45241-130">Para enviar un trabajo de Hive, consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="45241-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="45241-131">Para obtener más información sobre cómo crear clústeres de HDInsight, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="45241-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="45241-132">Para administrar clústeres de HDInsight, consulte [Administración de clústeres en HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="45241-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="45241-133">Para obtener información sobre hello HDInsight .NET SDK, vea [referencia de SDK de HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="45241-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="45241-134">Para no interactivo autenticar tooAzure, consulte [crear aplicaciones de .NET HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="45241-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

