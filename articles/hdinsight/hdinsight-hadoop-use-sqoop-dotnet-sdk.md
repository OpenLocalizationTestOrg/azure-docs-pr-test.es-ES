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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Ejecución de trabajos de Sqoop con el SDK de .NET para Hadoop en HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Obtenga información acerca de cómo trabajos toouse HDInsight .NET SDK toorun Sqoop en HDInsight tooimport y exportar entre el clúster de HDInsight y la base de datos SQL de Azure o la base de datos de SQL Server.

> [!NOTE]
> pasos de Hello en este artículo se pueden utilizar con cualquier un clúster basado en Windows o Linux de HDInsight; Sin embargo, estos pasos sólo funcionan desde un cliente de Windows. Utilizar tabulador hello en la parte superior de Hola de este artículo toochoose otros métodos.
> 
> 

### <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener Hola siguientes elementos:

* **Un clúster de Hadoop en HDInsight**. Consulte el artículo [Creación del clúster y la base de datos SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>Usar Sqoop en clústeres de HDInsight con el SDK. de .NET
Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET. En esta sección, creará una tabla C# consola aplicación tooexport hello hivesampletable toohello base de datos SQL que creó anteriormente en este tutorial.

## <a name="submit-a-sqoop-job"></a>Enviar un trabajo de Sqoop

1. Cree una aplicación de consola en C# mediante Visual Studio.
2. Desde Hola consola de administrador de paquetes de Visual Studio, ejecute hello después el paquete de Nuget command tooimport Hola.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Usar hello siguiente código en el archivo Program.cs de hello:
   
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
4. Presione **F5** programa Hola de toorun. 

## <a name="limitations"></a>Limitaciones
* La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.
* Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop varias inserciones en lugar de procesamiento por lotes las operaciones de inserción de Hola.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido cómo toouse Sqoop. toolearn más información, vea:

* [Uso de Oozie con HDInsight](hdinsight-use-oozie.md): use la acción Sqoop en un flujo de trabajo de Oozie.
* [Analizar datos de retrasos de vuelos con HDInsight](hdinsight-analyze-flight-delay-data.md): usar Hive tooanalyze flight retrasar datos y, a continuación, usar base de datos de Sqoop tooexport datos tooan SQL Azure.
* [Cargar datos tooHDInsight](hdinsight-upload-data.md): dar con otros métodos para cargar el almacenamiento de blobs de datos tooHDInsight o SQL Azure.

