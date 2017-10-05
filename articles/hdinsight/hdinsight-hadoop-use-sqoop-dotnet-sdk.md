---
title: "Ejecución de trabajos de Sqoop con .NET y HDInsight - Azure | Microsoft Docs"
description: "Obtenga información sobre cómo utilizar el SDK de .NET de HDInsight para ejecutar trabajos de Sqoop con el fin de llevar a cabo tareas de importación y exportación entre un clúster de Hadoop y una base de datos SQL de Azure."
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="753ad-104">Ejecución de trabajos de Sqoop con el SDK de .NET para Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="753ad-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="753ad-105">Obtenga información sobre cómo utilizar el SDK de .NET de HDInsight en HDInsight para ejecutar trabajos de Sqoop con el fin de llevar a cabo tareas de importación y exportación entre un clúster de HDInsight y una base de datos SQL de Azure o una de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="753ad-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="753ad-106">Los pasos de este artículo pueden usarse con un clúster de HDInsight basado en Windows o en Linux, aunque solo funcionan desde un cliente Windows.</span><span class="sxs-lookup"><span data-stu-id="753ad-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="753ad-107">Utilice el selector de pestañas de la parte superior de este artículo para elegir otros métodos.</span><span class="sxs-lookup"><span data-stu-id="753ad-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="753ad-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="753ad-108">Prerequisites</span></span>
<span data-ttu-id="753ad-109">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="753ad-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="753ad-110">**Un clúster de Hadoop en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="753ad-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="753ad-111">Consulte el artículo [Creación del clúster y la base de datos SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="753ad-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="753ad-112">Usar Sqoop en clústeres de HDInsight con el SDK. de .NET</span><span class="sxs-lookup"><span data-stu-id="753ad-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="753ad-113">El SDK .NET de HDInsight ofrece bibliotecas de cliente .NET que facilitan el trabajo con los clústeres de HDInsight de .NET.</span><span class="sxs-lookup"><span data-stu-id="753ad-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="753ad-114">En esta sección se crea una aplicación de consola de C# para exportar hivesampletable a la tabla de base de datos SQL creada anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="753ad-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="753ad-115">Enviar un trabajo de Sqoop</span><span class="sxs-lookup"><span data-stu-id="753ad-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="753ad-116">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="753ad-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="753ad-117">En la Consola del administrador de paquetes de Visual Studio, ejecute el siguiente comando de Nuget para importar el paquete.</span><span class="sxs-lookup"><span data-stu-id="753ad-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="753ad-118">Use el siguiente código en el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="753ad-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="753ad-119">Presione **F5** para ejecutar el programa.</span><span class="sxs-lookup"><span data-stu-id="753ad-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="753ad-120">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="753ad-120">Limitations</span></span>
* <span data-ttu-id="753ad-121">Exportación masiva: con HDInsight basado en Linux, el conector Sqoop que se utiliza para exportar datos a Microsoft SQL Server o Base de datos SQL Azure no es compatible actualmente con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="753ad-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="753ad-122">Procesamiento por lotes: con HDInsight basado en Linux, cuando se usa `-batch` al realizar inserciones, Sqoop realiza varias inserciones en lugar de procesar por lotes las operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="753ad-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="753ad-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="753ad-123">Next steps</span></span>
<span data-ttu-id="753ad-124">Ahora ya ha aprendido a usar Sqoop.</span><span class="sxs-lookup"><span data-stu-id="753ad-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="753ad-125">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="753ad-125">To learn more, see:</span></span>

* <span data-ttu-id="753ad-126">[Uso de Oozie con HDInsight](hdinsight-use-oozie.md): use la acción Sqoop en un flujo de trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="753ad-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="753ad-127">[Análisis de la información de retraso de vuelos con HDInsight](hdinsight-analyze-flight-delay-data.md): use Hive para analizar la información de retraso de los vuelos y luego use Sqoop para exportar los datos a una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="753ad-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="753ad-128">[Carga de datos en HDInsight](hdinsight-upload-data.md): busque otros métodos para cargar datos en HDInsight o el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="753ad-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

