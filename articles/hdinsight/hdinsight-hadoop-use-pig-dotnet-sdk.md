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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="d6aa0-103">Ejecutar trabajos de Pig con hello .NET SDK para Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6aa0-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="d6aa0-104">Obtenga información acerca de cómo toouse hello .NET SDK para toosubmit Hadoop Pig Apache trabajos tooHadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="d6aa0-105">Hola HDInsight .NET SDK proporciona bibliotecas de cliente de .NET que resulta más fácil toowork con clústeres de HDInsight desde. NET.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="d6aa0-106">Pig permite operaciones de MapReduce toocreate al modelar una serie de transformaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="d6aa0-107">En este documento, aprenderá cómo toouse un básico de C# aplicación toosubmit un Pig trabajo tooan clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6aa0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d6aa0-108">Prerequisites</span></span>

<span data-ttu-id="d6aa0-109">pasos de hello toocomplete en este artículo, necesita siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="d6aa0-110">Un clúster de HDInsight de Azure (Hadoop en HDInsight) (Windows o Linux)</span><span class="sxs-lookup"><span data-stu-id="d6aa0-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d6aa0-111">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d6aa0-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d6aa0-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d6aa0-113">Visual Studio 2012, 2013, 2015 o 2017.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="d6aa0-114">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="d6aa0-114">Create hello application</span></span>

<span data-ttu-id="d6aa0-115">Hola HDInsight .NET SDK proporciona bibliotecas de cliente. NET, lo que hace más fácil toowork con clústeres de HDInsight desde. NET.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="d6aa0-116">De hello **archivo** menú en Visual Studio, seleccione **New** y, a continuación, seleccione **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="d6aa0-117">Para nuevo proyecto de hello, tipo o seleccione hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="d6aa0-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="d6aa0-118">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d6aa0-118">Property</span></span> | <span data-ttu-id="d6aa0-119">Valor</span><span class="sxs-lookup"><span data-stu-id="d6aa0-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="d6aa0-120">Categoría</span><span class="sxs-lookup"><span data-stu-id="d6aa0-120">Category</span></span> | <span data-ttu-id="d6aa0-121">Plantillas/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="d6aa0-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="d6aa0-122">Plantilla</span><span class="sxs-lookup"><span data-stu-id="d6aa0-122">Template</span></span> | <span data-ttu-id="d6aa0-123">Aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="d6aa0-123">Console Application</span></span> |
   | <span data-ttu-id="d6aa0-124">Nombre</span><span class="sxs-lookup"><span data-stu-id="d6aa0-124">Name</span></span> | <span data-ttu-id="d6aa0-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="d6aa0-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="d6aa0-126">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="d6aa0-127">De hello **herramientas** menú, seleccione **Administrador de paquetes de biblioteca** o **Administrador de paquetes de Nuget**y, a continuación, seleccione **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="d6aa0-128">paquetes de tooinstall Hola .NET SDK, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d6aa0-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="d6aa0-129">En el Explorador de soluciones, haga doble clic en **Program.cs** tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="d6aa0-130">Reemplace el código existente de hello con hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-130">Replace hello existing code with hello following.</span></span>

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

7. <span data-ttu-id="d6aa0-131">aplicación de hello toostart, presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="d6aa0-132">aplicación de hello tooexit, presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="d6aa0-133">Resumen</span><span class="sxs-lookup"><span data-stu-id="d6aa0-133">Summary</span></span>

<span data-ttu-id="d6aa0-134">Como puede ver, Hola .NET SDK para Hadoop le permite toocreate las aplicaciones de .NET que enviar el clúster de HDInsight de tooan de trabajos de Pig y supervisar el estado del trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="d6aa0-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6aa0-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6aa0-135">Next steps</span></span>

<span data-ttu-id="d6aa0-136">Para obtener información sobre Pig en HDInsight, vea [Usar Pig con Hadoop en HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="d6aa0-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="d6aa0-137">Para obtener más información sobre el uso de Hadoop en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="d6aa0-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="d6aa0-138">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6aa0-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d6aa0-139">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6aa0-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
