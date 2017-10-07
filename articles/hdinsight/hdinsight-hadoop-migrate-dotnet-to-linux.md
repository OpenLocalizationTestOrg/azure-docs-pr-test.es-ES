---
title: aaaUse .NET con Hadoop MapReduce en HDInsight basados en Linux - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de .NET toouse de transmisión por secuencias MapReduce en HDInsight basados en Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="e6699-103">Migrar soluciones de .NET para HDInsight basados en Windows-based tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6699-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="e6699-104">Uso de clústeres de HDInsight basados en Linux [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicaciones. NET.</span><span class="sxs-lookup"><span data-stu-id="e6699-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="e6699-105">Mono permite toouse componentes de .NET como las aplicaciones de MapReduce con HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="e6699-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="e6699-106">En este documento, obtenga información acerca de cómo se crean soluciones de .NET toomigrate para toowork de clústeres de HDInsight basados en Windows con Mono en HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="e6699-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="e6699-107">Compatibilidad de Mono con .NET</span><span class="sxs-lookup"><span data-stu-id="e6699-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="e6699-108">La versión 4.2.1 de Mono está incluida en la versión 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6699-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="e6699-109">Para obtener más información sobre la versión de Hola de Mono incluido con HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e6699-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="e6699-110">tooinstall una versión específica de Mono, vea hello [instalación o una actualización Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e6699-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="e6699-111">Para obtener información detallada sobre la compatibilidad entre Mono y. NET, vea hello [compatibilidad Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) documento.</span><span class="sxs-lookup"><span data-stu-id="e6699-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6699-112">el marco de trabajo de Hello SCP.NET es compatible con Mono.</span><span class="sxs-lookup"><span data-stu-id="e6699-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="e6699-113">Para obtener más información sobre el uso de SCP.NET con Mono, consulte [topologías de toodevelop C# utilice Visual Studio para Apache Storm en HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e6699-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="e6699-114">Análisis de portabilidad automatizado</span><span class="sxs-lookup"><span data-stu-id="e6699-114">Automated portability analysis</span></span>

<span data-ttu-id="e6699-115">Hola [analizador de portabilidad de .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) puede ser usado toogenerate un informe de las incompatibilidades entre la aplicación y Mono.</span><span class="sxs-lookup"><span data-stu-id="e6699-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="e6699-116">Usar hello siguiendo los pasos tooconfigure Hola analizador toocheck la aplicación para la portabilidad Mono:</span><span class="sxs-lookup"><span data-stu-id="e6699-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="e6699-117">Instalar hello [analizador de portabilidad de .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="e6699-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="e6699-118">Durante la instalación, seleccione la versión de Hola de toouse de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6699-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="e6699-119">En Visual Studio 2015, seleccione __analizar__ > __configuración de analizador de portabilidad__y asegúrese de que __4.5__ está activada en hello __Mono__  sección.</span><span class="sxs-lookup"><span data-stu-id="e6699-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![4.5 activadas en la sección Mono para la configuración del analizador de Hola](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="e6699-121">Seleccione __Aceptar__ configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="e6699-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="e6699-122">Seleccione __Analyze__ > __Analyze Assembly Portability__ (Analizar > Analizar portabilidad de ensamblado).</span><span class="sxs-lookup"><span data-stu-id="e6699-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="e6699-123">Seleccionar ensamblado de Hola que contiene la solución y, a continuación, seleccione __abiertos__ toobegin analysis.</span><span class="sxs-lookup"><span data-stu-id="e6699-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="e6699-124">Una vez completado el análisis, seleccione __Analyze__ > __View analysis reports__ (Analizar > Ver informes de análisis).</span><span class="sxs-lookup"><span data-stu-id="e6699-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="e6699-125">En __resultados del análisis de portabilidad__, seleccione __abrir informe__ tooopen un informe.</span><span class="sxs-lookup"><span data-stu-id="e6699-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Cuadro de diálogo de resultados del analizador de portabilidad](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="e6699-127">Analizador de Hello no puede detectar todos los problemas con la solución.</span><span class="sxs-lookup"><span data-stu-id="e6699-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="e6699-128">Por ejemplo, una ruta de archivo de `c:\temp\file.txt` se considera correcto porque Mono se ejecuta en Windows y la ruta de acceso de hello es válido en ese contexto.</span><span class="sxs-lookup"><span data-stu-id="e6699-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="e6699-129">Sin embargo, la ruta de acceso de hello no es válido en una plataforma de Linux.</span><span class="sxs-lookup"><span data-stu-id="e6699-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="e6699-130">Análisis de portabilidad manual</span><span class="sxs-lookup"><span data-stu-id="e6699-130">Manual portability analysis</span></span>

<span data-ttu-id="e6699-131">Realizar una auditoría manual del código utilizando información de Hola Hola [portabilidad de aplicación (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) documento.</span><span class="sxs-lookup"><span data-stu-id="e6699-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="e6699-132">Modificación y compilación</span><span class="sxs-lookup"><span data-stu-id="e6699-132">Modify and build</span></span>

<span data-ttu-id="e6699-133">Puede continuar toouse Visual Studio toobuild sus soluciones de .NET para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6699-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="e6699-134">Sin embargo, debe asegurarse de que ese proyecto Hola está configurado toouse .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e6699-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="e6699-135">Implementación y prueba</span><span class="sxs-lookup"><span data-stu-id="e6699-135">Deploy and test</span></span>

<span data-ttu-id="e6699-136">Una vez que haya modificado la solución con las recomendaciones de Hola de hello analizador de portabilidad de .NET o de un análisis manual, debe probarla con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6699-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="e6699-137">Probar la solución de hello en un clúster de HDInsight basados en Linux puede revelar problemas sutiles que requieren toobe que se ha corregido.</span><span class="sxs-lookup"><span data-stu-id="e6699-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="e6699-138">Se recomienda que habilite el registro adicional en la aplicación durante la prueba.</span><span class="sxs-lookup"><span data-stu-id="e6699-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="e6699-139">Para obtener más información sobre cómo acceder a los registros, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="e6699-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="e6699-140">Acceso a registros de aplicación de YARN en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="e6699-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="e6699-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6699-141">Next steps</span></span>

* [<span data-ttu-id="e6699-142">Uso de MapReduce en C# en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6699-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="e6699-143">Uso de funciones definidas por el usuario de C# con Hive y Pig</span><span class="sxs-lookup"><span data-stu-id="e6699-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="e6699-144">Desarrollo de topologías de C# para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6699-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)