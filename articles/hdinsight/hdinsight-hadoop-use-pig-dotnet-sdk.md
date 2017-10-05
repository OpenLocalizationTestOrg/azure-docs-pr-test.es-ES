---
title: "Ejecución de trabajos de Apache Pig con el SDK de .NET para Hadoop - Azure HDInsight | Microsoft Docs"
description: Aprenda a usar el SDK de .NET de Hadoop para enviar trabajos de Pig a Hadoop en HDInsight.
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
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="75648-103">Ejecución de trabajos de Pig con el SDK de .NET para Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="75648-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="75648-104">Aprenda a usar el SDK de .NET de Hadoop para enviar trabajos de Apache Pig a Hadoop en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75648-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="75648-105">El SDK .NET de HDInsight proporciona bibliotecas de cliente .NET que facilitan el trabajo con los clústeres de HDInsight en .NET.</span><span class="sxs-lookup"><span data-stu-id="75648-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="75648-106">Pig le permite crear operaciones de MapReduce al modelar una serie de transformaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="75648-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="75648-107">En este documento, aprenderá a utilizar una aplicación básica de C# para enviar un trabajo de Pig para un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75648-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75648-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="75648-108">Prerequisites</span></span>

<span data-ttu-id="75648-109">Necesitará lo siguiente para completar los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="75648-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="75648-110">Un clúster de HDInsight de Azure (Hadoop en HDInsight) (Windows o Linux)</span><span class="sxs-lookup"><span data-stu-id="75648-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="75648-111">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="75648-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="75648-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="75648-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="75648-113">Visual Studio 2012, 2013, 2015 o 2017.</span><span class="sxs-lookup"><span data-stu-id="75648-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="75648-114">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="75648-114">Create the application</span></span>

<span data-ttu-id="75648-115">El SDK .NET de HDInsight ofrece bibliotecas de cliente .NET que facilitan el trabajo con los clústeres de HDInsight de .NET.</span><span class="sxs-lookup"><span data-stu-id="75648-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="75648-116">En Visual Studio, en el menú **Archivo**, seleccione **Nuevo** y, luego, **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="75648-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="75648-117">Para el nuevo proyecto, escriba o seleccione los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="75648-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="75648-118">Propiedad</span><span class="sxs-lookup"><span data-stu-id="75648-118">Property</span></span> | <span data-ttu-id="75648-119">Valor</span><span class="sxs-lookup"><span data-stu-id="75648-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="75648-120">Categoría</span><span class="sxs-lookup"><span data-stu-id="75648-120">Category</span></span> | <span data-ttu-id="75648-121">Plantillas/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="75648-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="75648-122">Plantilla</span><span class="sxs-lookup"><span data-stu-id="75648-122">Template</span></span> | <span data-ttu-id="75648-123">Aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="75648-123">Console Application</span></span> |
   | <span data-ttu-id="75648-124">Nombre</span><span class="sxs-lookup"><span data-stu-id="75648-124">Name</span></span> | <span data-ttu-id="75648-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="75648-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="75648-126">Haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="75648-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="75648-127">En el menú **Herramientas**, seleccione **Administrador de paquetes de biblioteca** o **Administrador de paquetes de Nuget** y, a continuación, seleccione **Consola del administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="75648-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="75648-128">Use el siguiente comando para instalar los paquetes de SDK de .NET:</span><span class="sxs-lookup"><span data-stu-id="75648-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="75648-129">En el Explorador de soluciones, haga doble clic en **Program.cs** para abrirlo.</span><span class="sxs-lookup"><span data-stu-id="75648-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="75648-130">Reemplace el código existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="75648-130">Replace the existing code with the following.</span></span>

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
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
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

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="75648-131">Presione **F5** para iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="75648-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="75648-132">Presione **ENTRAR** para salir de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="75648-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="75648-133">Resumen</span><span class="sxs-lookup"><span data-stu-id="75648-133">Summary</span></span>

<span data-ttu-id="75648-134">Como puede observar, el SDK de .NET para Hadoop le permite crear aplicaciones .NET que envíen trabajos de Pig a un clúster de HDInsight y supervisar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="75648-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75648-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75648-135">Next steps</span></span>

<span data-ttu-id="75648-136">Para obtener información sobre Pig en HDInsight, vea [Usar Pig con Hadoop en HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="75648-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="75648-137">Para más información sobre el uso de Hadoop con HDInsight, vea los documentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="75648-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="75648-138">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="75648-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="75648-139">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="75648-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
