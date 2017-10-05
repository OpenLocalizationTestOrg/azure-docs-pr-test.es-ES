---
title: "Envío de trabajos de MapReduce mediante el SDK .NET de HDInsight (Azure) | Microsoft Docs"
description: "Obtenga información sobre cómo enviar trabajos de MapReduce a HDInsight Hadoop de Azure mediante el SDK de .NET de HDInsight."
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
ms.openlocfilehash: 015435270c31bafea0ebf5303b459338755c1410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="f0bd8-103">Envío de trabajos de MapReduce mediante el SDK .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0bd8-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="f0bd8-104">Aprenda a enviar trabajos de MapReduce mediante el SDK .NET de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="f0bd8-105">Los clústeres de HDInsight vienen con un archivo .jar con varios ejemplos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="f0bd8-106">El archivo .jar se encuentra en */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="f0bd8-107">Uno de los ejemplos es *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="f0bd8-108">Desarrollará una aplicación de consola de C# para enviar un trabajo de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="f0bd8-109">El trabajo lee el archivo */example/data/gutenberg/davinci.txt* y guarda el resultado en */example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="f0bd8-110">Si desea volver a ejecutar la aplicación, deberá limpiar la carpeta de salida.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="f0bd8-111">Los pasos de este artículo deben realizarse desde un cliente de Windows.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="f0bd8-112">Para obtener información sobre cómo usar un cliente Linux, OS X o Unix para trabajar con Hive, utilice el selector de pestañas que se muestra en la parte superior del artículo.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f0bd8-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f0bd8-113">Prerequisites</span></span>
<span data-ttu-id="f0bd8-114">Antes de empezar este artículo, debe tener los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f0bd8-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="f0bd8-115">**Un clúster de Hadoop en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="f0bd8-116">Consulte [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd8-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="f0bd8-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="f0bd8-118">Envío de trabajos de MapReduce mediante el SDK .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0bd8-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="f0bd8-119">El SDK .NET de HDInsight ofrece bibliotecas de cliente .NET que facilitan el trabajo con los clústeres de HDInsight de .NET.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="f0bd8-120">**Para enviar trabajos**</span><span class="sxs-lookup"><span data-stu-id="f0bd8-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="f0bd8-121">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="f0bd8-122">En la Consola del Administrador de paquetes NuGet, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f0bd8-122">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="f0bd8-123">Use el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="f0bd8-123">Use the following code:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
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
                        // Create the storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create the blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference to a previously created container.
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
4. <span data-ttu-id="f0bd8-124">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="f0bd8-125">Para ejecutar el trabajo de nuevo, debe cambiar el nombre de la carpeta de salida del trabajo que, en el ejemplo, es "/example/data/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="f0bd8-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="f0bd8-126">Cuando el trabajo se completa correctamente, la aplicación imprime el contenido del archivo de salida "part-r-00000".</span><span class="sxs-lookup"><span data-stu-id="f0bd8-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0bd8-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0bd8-127">Next steps</span></span>
<span data-ttu-id="f0bd8-128">En este artículo, ha aprendido varias maneras de crear un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0bd8-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="f0bd8-129">Para obtener más información, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f0bd8-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="f0bd8-130">Para enviar un trabajo de Hive, consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd8-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="f0bd8-131">Para obtener más información sobre cómo crear clústeres de HDInsight, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd8-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="f0bd8-132">Para administrar clústeres de HDInsight, consulte [Administración de clústeres en HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd8-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="f0bd8-133">Para obtener información sobre el SDK .NET de HDInsight, consulte ka [referencia del SDK de .NET de HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0bd8-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="f0bd8-134">Para usar la autenticación no interactiva en Azure, consulte [Creación de aplicaciones .NET para HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd8-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

