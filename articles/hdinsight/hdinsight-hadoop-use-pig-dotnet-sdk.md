---
title: aaaRun Apache Pig trabajos con el SDK de .NET de Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola .NET SDK para tooHadoop de trabajos de Hadoop toosubmit Pig en HDInsight."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Ejecutar trabajos de Pig con hello .NET SDK para Hadoop en HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Obtenga información acerca de cómo toouse hello .NET SDK para toosubmit Hadoop Pig Apache trabajos tooHadoop en HDInsight de Azure.

Hola HDInsight .NET SDK proporciona bibliotecas de cliente de .NET que resulta más fácil toowork con clústeres de HDInsight desde. NET. Pig permite operaciones de MapReduce toocreate al modelar una serie de transformaciones de datos. En este documento, aprenderá cómo toouse un básico de C# aplicación toosubmit un Pig trabajo tooan clúster de HDInsight.

## <a name="prerequisites"></a>Requisitos previos

pasos de hello toocomplete en este artículo, necesita siguiente de Hola.

* Un clúster de HDInsight de Azure (Hadoop en HDInsight) (Windows o Linux)

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio 2012, 2013, 2015 o 2017.

## <a name="create-hello-application"></a>Crear aplicación hello

Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET.

1. De hello **archivo** menú en Visual Studio, seleccione **New** y, a continuación, seleccione **proyecto**.

2. Para nuevo proyecto de hello, tipo o seleccione hello siguientes valores:

   | Propiedad | Valor |
   | ------ | ------ |
   | Categoría | Plantillas/Visual C#/Windows |
   | Plantilla | Aplicación de consola |
   | Nombre | SubmitPigJob |

3. Haga clic en **Aceptar** proyecto de hello toocreate.

4. De hello **herramientas** menú, seleccione **Administrador de paquetes de biblioteca** o **Administrador de paquetes de Nuget**y, a continuación, seleccione **Package Manager Console**.

5. paquetes de tooinstall Hola .NET SDK, use Hola siguiente comando:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. En el Explorador de soluciones, haga doble clic en **Program.cs** tooopen lo. Reemplace el código existente de hello con hello siguiente.

    ```csharp
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

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. aplicación de hello toostart, presione **F5**.

8. aplicación de hello tooexit, presione **ENTRAR**.

## <a name="summary"></a>Resumen

Como puede ver, Hola .NET SDK para Hadoop le permite toocreate las aplicaciones de .NET que enviar el clúster de HDInsight de tooan de trabajos de Pig y supervisar el estado del trabajo Hola.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre Pig en HDInsight, vea [Usar Pig con Hadoop en HDInsight](hdinsight-use-pig.md).

Para obtener más información sobre el uso de Hadoop en HDInsight, vea Hola siguientes documentos:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
