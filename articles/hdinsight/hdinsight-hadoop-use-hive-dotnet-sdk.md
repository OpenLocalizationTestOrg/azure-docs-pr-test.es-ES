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
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Obtenga información acerca de cómo las consultas que utilizan el SDK de HDInsight .NET toosubmit Hive. Escribir un programa de C# toosubmit una consulta de Hive para enumerar tablas de Hive y mostrar los resultados de Hola.

> [!NOTE]
> pasos de Hello en este artículo deben realizarse desde un cliente de Windows. Para obtener información sobre cómo usar un Linux, OS X o toowork de cliente de Unix con Hive, utilice tabulador Hola que se muestra en la parte superior de Hola de artículo Hola.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener Hola siguientes elementos:

* **Un clúster de Hadoop en HDInsight**. Consulte [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>Envío de trabajos de Hive mediante el SDK de .NET de HDInsight
Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET. 

**trabajos de tooSubmit**

1. Cree una aplicación de consola en C# mediante Visual Studio.
2. Desde la consola de administrador de paquetes de Nuget hello, ejecute hello siguiente comando:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Usar hello siguiente código:

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
4. Presione **F5** aplicación de hello toorun.

salida de Hello de aplicación hello será similar al:

![Salida de trabajo de Hive para Hadoop en HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido varias formas toocreate un clúster de HDInsight. toolearn más información, vea Hola siguientes artículos:

* [Introducción a Azure HDInsight][hdinsight-get-started]
* [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision]
* [Administrar clústeres de Hadoop en HDInsight con hello portal de Azure](hdinsight-administer-use-management-portal.md)
* [Referencia del SDK de .NET de HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de Sqoop con HDInsight](hdinsight-use-sqoop-mac-linux.md)
* [Crear aplicaciones .NET para HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


