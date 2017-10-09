---
title: trabajos de Sqoop aaaRun utiliza .NET y HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse HDInsight .NET SDK toorun Sqoop importar y exportar entre un clúster de Hadoop y una base de datos de SQL Azure."
keywords: trabajo de Sqoop
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="d01e0-104">Ejecución de trabajos de Sqoop con el SDK de .NET para Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d01e0-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="d01e0-105">Obtenga información acerca de cómo trabajos toouse HDInsight .NET SDK toorun Sqoop en HDInsight tooimport y exportar entre el clúster de HDInsight y la base de datos SQL de Azure o la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d01e0-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="d01e0-106">pasos de Hello en este artículo se pueden utilizar con cualquier un clúster basado en Windows o Linux de HDInsight; Sin embargo, estos pasos sólo funcionan desde un cliente de Windows.</span><span class="sxs-lookup"><span data-stu-id="d01e0-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="d01e0-107">Utilizar tabulador hello en la parte superior de Hola de este artículo toochoose otros métodos.</span><span class="sxs-lookup"><span data-stu-id="d01e0-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="d01e0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d01e0-108">Prerequisites</span></span>
<span data-ttu-id="d01e0-109">Antes de comenzar este tutorial, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d01e0-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="d01e0-110">**Un clúster de Hadoop en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d01e0-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="d01e0-111">Consulte el artículo [Creación del clúster y la base de datos SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="d01e0-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="d01e0-112">Usar Sqoop en clústeres de HDInsight con el SDK. de .NET</span><span class="sxs-lookup"><span data-stu-id="d01e0-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="d01e0-113">Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET.</span><span class="sxs-lookup"><span data-stu-id="d01e0-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="d01e0-114">En esta sección, creará una tabla C# consola aplicación tooexport hello hivesampletable toohello base de datos SQL que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d01e0-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="d01e0-115">Enviar un trabajo de Sqoop</span><span class="sxs-lookup"><span data-stu-id="d01e0-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="d01e0-116">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d01e0-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d01e0-117">Desde Hola consola de administrador de paquetes de Visual Studio, ejecute hello después el paquete de Nuget command tooimport Hola.</span><span class="sxs-lookup"><span data-stu-id="d01e0-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="d01e0-118">Usar hello siguiente código en el archivo Program.cs de hello:</span><span class="sxs-lookup"><span data-stu-id="d01e0-118">Use hello following code in hello Program.cs file:</span></span>
   
        using System.Collections.Generic;
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
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="d01e0-119">Presione **F5** programa Hola de toorun.</span><span class="sxs-lookup"><span data-stu-id="d01e0-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="d01e0-120">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="d01e0-120">Limitations</span></span>
* <span data-ttu-id="d01e0-121">La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="d01e0-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="d01e0-122">Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop varias inserciones en lugar de procesamiento por lotes las operaciones de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="d01e0-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d01e0-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d01e0-123">Next steps</span></span>
<span data-ttu-id="d01e0-124">Ahora que ha aprendido cómo toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="d01e0-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="d01e0-125">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="d01e0-125">toolearn more, see:</span></span>

* <span data-ttu-id="d01e0-126">[Uso de Oozie con HDInsight](hdinsight-use-oozie.md): use la acción Sqoop en un flujo de trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="d01e0-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="d01e0-127">[Analizar datos de retrasos de vuelos con HDInsight](hdinsight-analyze-flight-delay-data.md): usar Hive tooanalyze flight retrasar datos y, a continuación, usar base de datos de Sqoop tooexport datos tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d01e0-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="d01e0-128">[Cargar datos tooHDInsight](hdinsight-upload-data.md): dar con otros métodos para cargar el almacenamiento de blobs de datos tooHDInsight o SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d01e0-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

