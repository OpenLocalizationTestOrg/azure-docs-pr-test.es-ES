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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Envío de trabajos de MapReduce mediante el SDK .NET de HDInsight
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Obtenga información acerca de cómo toosubmit MapReduce trabajos usando HDInsight .NET SDK. Los clústeres de HDInsight vienen con un archivo .jar con varios ejemplos de MapReduce. es el archivo jar de Hello */example/jars/hadoop-mapreduce-examples.jar*.  Uno de los ejemplos de hello es *wordcount*. Desarrollar un toosubmit de aplicación de consola un trabajo wordcount de C#.  trabajo de Hello lee hello */example/data/gutenberg/davinci.txt* archivo y las salidas Hola resultados demasiado*/example/data/davinciwordcount*.  Si desea que la aplicación de hello toorerun, debe limpiar la carpeta de salida de hello.

> [!NOTE]
> pasos de Hello en este artículo deben realizarse desde un cliente de Windows. Para obtener información sobre cómo usar un Linux, OS X o toowork de cliente de Unix con Hive, utilice tabulador Hola que se muestra en la parte superior de Hola de artículo Hola.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener Hola siguientes elementos:

* **Un clúster de Hadoop en HDInsight**. Consulte [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Envío de trabajos de MapReduce mediante el SDK .NET de HDInsight
Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET. 

**trabajos de tooSubmit**

1. Cree una aplicación de consola en C# mediante Visual Studio.
2. Desde la consola de administrador de paquetes de Nuget hello, ejecute hello siguiente comando:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Usar hello siguiente código:
   
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
4. Presione **F5** aplicación de hello toorun.

trabajo de toorun Hola de nuevo, debe cambiar nombre de carpeta de salida de hello trabajo, en el ejemplo hello, es "/ datos de ejemplo/davinciwordcount".

Cuando se completa correctamente el trabajo de hello, aplicación hello imprime el contenido de Hola Hola del archivo de salida "parte-r-00000".

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido varias formas toocreate un clúster de HDInsight. toolearn más información, vea Hola siguientes artículos:

* Para enviar un trabajo de Hive, consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Para obtener más información sobre cómo crear clústeres de HDInsight, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Para administrar clústeres de HDInsight, consulte [Administración de clústeres en HDInsight](hdinsight-administer-use-portal-linux.md).
* Para obtener información sobre hello HDInsight .NET SDK, vea [referencia de SDK de HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx).
* Para no interactivo autenticar tooAzure, consulte [crear aplicaciones de .NET HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

