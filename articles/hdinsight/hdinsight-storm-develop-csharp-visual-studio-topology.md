---
title: "topologías de Storm aaaApache con Visual Studio y C# - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate topologías de Storm en C#. Crear una topología de recuento de palabras simple en Visual Studio mediante las herramientas de Hadoop de Hola para Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="79b30-104">Desarrollar topologías de C# para Apache Storm mediante las herramientas de Data Lake Hola para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79b30-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="79b30-105">Obtenga información acerca de cómo toocreate una topología de C# Storm mediante el uso de hello Azure Data Lake (Hadoop) de las herramientas de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79b30-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="79b30-106">Este documento le guía por el proceso de Hola de crear un proyecto de Storm en Visual Studio, pruebas de forma local e implementarla tooan Apache Storm en clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="79b30-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="79b30-107">También aprenderá cómo toocreate topologías de híbridas que utilizan los componentes de C# y Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="79b30-108">Aunque los pasos de hello en este documento se basan en un entorno de desarrollo de Windows con Visual Studio, proyecto compilado Hola puede ser tooeither enviado un clúster de HDInsight basados en Windows o de Linux.</span><span class="sxs-lookup"><span data-stu-id="79b30-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="79b30-109">Solo los clústeres basados en Linux creados después del 28 de octubre de 2016 admiten topologías SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="79b30-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="79b30-110">topología de toouse C# con un clúster basado en Linux, debe actualizar Hola paquete de Microsoft.SCP.Net.SDK NuGet utilizado por el tooversion proyecto 0.10.0.6 o posterior.</span><span class="sxs-lookup"><span data-stu-id="79b30-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="79b30-111">versión de Hola del paquete de hello también debe coincidir con la versión principal de Hola de Storm instalado en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79b30-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="79b30-112">Versión de HDInsight</span><span class="sxs-lookup"><span data-stu-id="79b30-112">HDInsight version</span></span> | <span data-ttu-id="79b30-113">Versión de Storm</span><span class="sxs-lookup"><span data-stu-id="79b30-113">Storm version</span></span> | <span data-ttu-id="79b30-114">Versión de SCP.NET</span><span class="sxs-lookup"><span data-stu-id="79b30-114">SCP.NET version</span></span> | <span data-ttu-id="79b30-115">Versión de Mono predeterminada</span><span class="sxs-lookup"><span data-stu-id="79b30-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="79b30-116">3.3</span><span class="sxs-lookup"><span data-stu-id="79b30-116">3.3</span></span> |<span data-ttu-id="79b30-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="79b30-117">0.10.x</span></span> |<span data-ttu-id="79b30-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="79b30-118">0.10.x.x</span></span></br><span data-ttu-id="79b30-119">(solo en HDInsight basado en Windows)</span><span class="sxs-lookup"><span data-stu-id="79b30-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="79b30-120">N/D</span><span class="sxs-lookup"><span data-stu-id="79b30-120">NA</span></span> |
| <span data-ttu-id="79b30-121">3.4</span><span class="sxs-lookup"><span data-stu-id="79b30-121">3.4</span></span> | <span data-ttu-id="79b30-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="79b30-122">0.10.0.x</span></span> | <span data-ttu-id="79b30-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="79b30-123">0.10.0.x</span></span> | <span data-ttu-id="79b30-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="79b30-124">3.2.8</span></span> |
| <span data-ttu-id="79b30-125">3,5</span><span class="sxs-lookup"><span data-stu-id="79b30-125">3.5</span></span> | <span data-ttu-id="79b30-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="79b30-126">1.0.2.x</span></span> | <span data-ttu-id="79b30-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="79b30-127">1.0.0.x</span></span> | <span data-ttu-id="79b30-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="79b30-128">4.2.1</span></span> |
| <span data-ttu-id="79b30-129">3.6</span><span class="sxs-lookup"><span data-stu-id="79b30-129">3.6</span></span> | <span data-ttu-id="79b30-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="79b30-130">1.1.0.x</span></span> | <span data-ttu-id="79b30-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="79b30-131">1.0.0.x</span></span> | <span data-ttu-id="79b30-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="79b30-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="79b30-133">Topologías de C# en clústeres basados en Linux deben usar .NET 4.5 y usar toorun Mono en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="79b30-134">Compruebe el documento de [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para ver las posibles incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="79b30-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="79b30-135">Instalación de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79b30-135">Install Visual Studio</span></span>

<span data-ttu-id="79b30-136">Puede desarrollar topologías de C# con SCP.NET mediante uno de hello después de versiones de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="79b30-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="79b30-137">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="79b30-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="79b30-138">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="79b30-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="79b30-139">Visual Studio 2015 o [Visual Studio Community 2015](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="79b30-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="79b30-140">Visual Studio 2017 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="79b30-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="79b30-141">Instalación de Herramientas de Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79b30-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="79b30-142">herramientas de Data Lake tooinstall para Visual Studio, siga los pasos de hello en [Introducción al uso de herramientas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="79b30-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="79b30-143">Instalar Java</span><span class="sxs-lookup"><span data-stu-id="79b30-143">Install Java</span></span>

<span data-ttu-id="79b30-144">Cuando se envía una topología de Storm desde Visual Studio, SCP.NET genera un archivo zip que contiene las dependencias y la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="79b30-145">Java es toocreate usa estos archivos, zip porque utiliza un formato que sea más compatible con clústeres basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="79b30-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="79b30-146">Instalar Hola Kit de desarrollador de Java (JDK) 7 o posterior en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="79b30-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="79b30-147">Puede obtener Hola Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="79b30-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="79b30-148">También puede usar [otras distribuciones de Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="79b30-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="79b30-149">Hola `JAVA_HOME` entorno debe variable punto toohello el directorio que contiene Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="79b30-150">Hola `PATH` variable de entorno debe incluir hello `%JAVA_HOME%\bin` directory.</span><span class="sxs-lookup"><span data-stu-id="79b30-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="79b30-151">Puede usar Hola después de C# consola los tooverify de aplicación que se han instalado correctamente hello JDK y Java:</span><span class="sxs-lookup"><span data-stu-id="79b30-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="79b30-152">Plantillas de Storm</span><span class="sxs-lookup"><span data-stu-id="79b30-152">Storm templates</span></span>

<span data-ttu-id="79b30-153">herramientas de Data Lake de Hola para Visual Studio proporcionan Hola siguientes plantillas:</span><span class="sxs-lookup"><span data-stu-id="79b30-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="79b30-154">Tipo de proyecto</span><span class="sxs-lookup"><span data-stu-id="79b30-154">Project type</span></span> | <span data-ttu-id="79b30-155">Muestra</span><span class="sxs-lookup"><span data-stu-id="79b30-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="79b30-156">Storm Application</span><span class="sxs-lookup"><span data-stu-id="79b30-156">Storm Application</span></span> |<span data-ttu-id="79b30-157">Un proyecto vacío de topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="79b30-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="79b30-158">Storm Azure SQL Writer Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="79b30-159">Cómo toowrite tooAzure base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="79b30-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="79b30-160">Storm Azure Cosmos DB Reader Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="79b30-161">¿Cómo tooread de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79b30-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="79b30-162">Storm Azure Cosmos DB Writer Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="79b30-163">Cómo toowrite tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79b30-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="79b30-164">Storm EventHub Reader Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="79b30-165">¿Cómo tooread desde los centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="79b30-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="79b30-166">Storm EventHub Writer Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="79b30-167">Cómo toowrite tooAzure centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="79b30-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="79b30-168">Storm HBase Reader Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="79b30-169">¿Cómo tooread de HBase en HDInsight de clústeres.</span><span class="sxs-lookup"><span data-stu-id="79b30-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="79b30-170">Storm HBase Writer Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="79b30-171">Cómo toowrite tooHBase en HDInsight de clústeres.</span><span class="sxs-lookup"><span data-stu-id="79b30-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="79b30-172">Storm Hybrid Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="79b30-173">¿Cómo toouse un componente de Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="79b30-174">Storm Sample</span><span class="sxs-lookup"><span data-stu-id="79b30-174">Storm Sample</span></span> |<span data-ttu-id="79b30-175">Una topología de recuento de palabras básica.</span><span class="sxs-lookup"><span data-stu-id="79b30-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="79b30-176">No todas las plantillas funcionará con HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="79b30-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="79b30-177">Paquetes de NuGet utilizados plantillas de hello no pueden ser compatibles con Mono.</span><span class="sxs-lookup"><span data-stu-id="79b30-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="79b30-178">Comprobar hello [compatibilidad Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documentos y usar hello [analizador de portabilidad de .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="79b30-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="79b30-179">En los pasos de hello en este documento, use hello básico Storm aplicación proyecto tipo toocreate una topología.</span><span class="sxs-lookup"><span data-stu-id="79b30-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="79b30-180">Notas de plantillas de HBase</span><span class="sxs-lookup"><span data-stu-id="79b30-180">HBase templates notes</span></span>

<span data-ttu-id="79b30-181">Hola HBase lector y plantillas de escritor usan hello API de REST de HBase, no Hola API de Java de HBase, toocommunicate con un HBase en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79b30-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="79b30-182">Notas de plantillas de EventHub</span><span class="sxs-lookup"><span data-stu-id="79b30-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79b30-183">Hola EventHub basados en Java apetezca charlar un componente incluido con hello plantilla de lector de EventHub no funcionen con Storm en HDInsight versión 3.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="79b30-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="79b30-184">Hay una versión actualizada de este componente disponible en [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="79b30-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="79b30-185">Para obtener una topología de ejemplo que usa este componente y funciona con Storm en HDInsight 3.5, vea [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="79b30-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="79b30-186">Creación de una topología de C#</span><span class="sxs-lookup"><span data-stu-id="79b30-186">Create a C# topology</span></span>

1. <span data-ttu-id="79b30-187">Abra Visual Studio, seleccione **Archivo** > **Nuevo** y luego seleccione **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="79b30-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="79b30-188">De hello **nuevo proyecto** ventana, expanda **instalado** > **plantillas**y seleccione **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="79b30-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="79b30-189">En la lista Hola de plantillas, seleccione **aluvión de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="79b30-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="79b30-190">En la parte inferior de Hola de pantalla de bienvenida, escriba **WordCount** como nombre de Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="79b30-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Captura de pantalla de la ventana Nuevo proyecto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="79b30-192">Una vez haya creado el proyecto de hello, debe tener Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="79b30-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="79b30-193">**Program.cs**: este archivo define la topología de hello para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="79b30-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="79b30-194">Una topología predeterminada que consta de un spout y un bolt se crea de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="79b30-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="79b30-195">**Spout.cs**: un spout de ejemplo que emite números aleatorios</span><span class="sxs-lookup"><span data-stu-id="79b30-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="79b30-196">**Bolt.cs**: un rayo de ejemplo que mantiene un recuento de números emitidos por pitorro Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="79b30-197">Cuando se crea el proyecto de hello, descargas de NuGet Hola más reciente [SCP.NET paquete](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="79b30-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="79b30-198">Pitorro de hello implemente</span><span class="sxs-lookup"><span data-stu-id="79b30-198">Implement hello spout</span></span>

1. <span data-ttu-id="79b30-199">Abra **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="79b30-199">Open **Spout.cs**.</span></span> <span data-ttu-id="79b30-200">Spouts son datos tooread usado en una topología de un origen externo.</span><span class="sxs-lookup"><span data-stu-id="79b30-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="79b30-201">componentes principales de Hola para un pitorro son:</span><span class="sxs-lookup"><span data-stu-id="79b30-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="79b30-202">**NextTuple**: llama Storm cuando pitorro Hola se permite tooemit nuevas tuplas.</span><span class="sxs-lookup"><span data-stu-id="79b30-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="79b30-203">**Confirmación** (solo topología transaccional): controla confirmaciones iniciadas por otros componentes de la topología de Hola para tuplas enviados desde pitorro Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="79b30-204">Confirmación de una tupla, podrá pitorro Hola saber que se procesó correctamente por componentes de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="79b30-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="79b30-205">**Un error** (solo topología transaccional): controla tuplas que se producirá un error-procesamiento de otros componentes de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="79b30-206">Implementa un método por error permite toore-emitir tupla Hola para que se pueda procesar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="79b30-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="79b30-207">Reemplazar contenido Hola de hello **apetezca charlar** clase con hello después de texto.</span><span class="sxs-lookup"><span data-stu-id="79b30-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="79b30-208">Este pitorro aleatoriamente emite una frase en la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="79b30-209">Implementar Hola tornillos</span><span class="sxs-lookup"><span data-stu-id="79b30-209">Implement hello bolts</span></span>

1. <span data-ttu-id="79b30-210">Eliminar Hola existente **Bolt.cs** archivo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="79b30-211">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **agregar** > **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="79b30-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="79b30-212">En la lista de hello, seleccione **aluvión de rayo**y escriba **Splitter.cs** como nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="79b30-213">Repita este toocreate proceso denominado un rayo segundo **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="79b30-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="79b30-214">**Splitter.cs**: implementa un bolt que divide la frase en palabras individuales y emite una nueva secuencia de palabras.</span><span class="sxs-lookup"><span data-stu-id="79b30-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="79b30-215">**Counter.cs**: implementa un rayo que cuenta cada palabra y emite una nueva secuencia de palabras y el recuento de Hola de cada palabra.</span><span class="sxs-lookup"><span data-stu-id="79b30-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="79b30-216">Estos tornillos de lectura y escritura toostreams, pero también puede utilizar un rayo toocommunicate con orígenes, como una base de datos o un servicio.</span><span class="sxs-lookup"><span data-stu-id="79b30-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="79b30-217">Abra **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="79b30-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="79b30-218">Solo tiene un método de forma predeterminada: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="79b30-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="79b30-219">Hola método Execute se llama cuando el rayo de Hola recibe una tupla para el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="79b30-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="79b30-220">En este caso, puede leer y procesar las tuplas entrantes y emitir tuplas salientes.</span><span class="sxs-lookup"><span data-stu-id="79b30-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="79b30-221">Reemplazar contenido Hola de hello **divisor** clase con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="79b30-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="79b30-222">Abra **Counter.cs**y reemplace el contenido de la clase hello con siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="79b30-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="79b30-223">Definir la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="79b30-223">Define hello topology</span></span>

<span data-ttu-id="79b30-224">Spouts y tornillos se organizan en un gráfico, que define cómo fluyen los datos de hello entre los componentes.</span><span class="sxs-lookup"><span data-stu-id="79b30-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="79b30-225">Para esta topología, el gráfico de hello es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="79b30-225">For this topology, hello graph is as follows:</span></span>

![Diagrama de cómo se organizan los componentes](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="79b30-227">Las frases se emiten desde pitorro hello y son tooinstances distribuida de rayo divisor de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="79b30-228">tornillo del divisor de Hola divide las frases de Hola palabras, lo cual están distribuidas toohello rayo de contador.</span><span class="sxs-lookup"><span data-stu-id="79b30-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="79b30-229">Debido a número de palabras se conservan localmente en la instancia del contador de hello, queremos toomake seguro de que las palabras específicas fluyan toohello misma instancia del contador rayo.</span><span class="sxs-lookup"><span data-stu-id="79b30-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="79b30-230">Cada instancia realiza el seguimiento de palabras específicas.</span><span class="sxs-lookup"><span data-stu-id="79b30-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="79b30-231">Puesto que el rayo de hello divisor no mantiene ningún estado, realmente no importa qué instancia del divisor de hello recibe qué frase.</span><span class="sxs-lookup"><span data-stu-id="79b30-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="79b30-232">Abra **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="79b30-232">Open **Program.cs**.</span></span> <span data-ttu-id="79b30-233">Hola método en importancia es **GetTopologyBuilder**, que es la topología de hello toodefine utilizado que es envían tooStorm.</span><span class="sxs-lookup"><span data-stu-id="79b30-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="79b30-234">Reemplace el contenido de Hola de **GetTopologyBuilder** con hello después de la topología de hello tooimplement de código se ha descrito anteriormente:</span><span class="sxs-lookup"><span data-stu-id="79b30-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="79b30-235">Enviar Hola topología</span><span class="sxs-lookup"><span data-stu-id="79b30-235">Submit hello topology</span></span>

1. <span data-ttu-id="79b30-236">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="79b30-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="79b30-237">Si se le pide, escriba credenciales de hello para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="79b30-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="79b30-238">Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79b30-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="79b30-239">Seleccione el aluvión en clúster de HDInsight de hello **clúster de Storm** lista desplegable y, a continuación, seleccione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="79b30-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="79b30-240">Puede supervisar si el envío de hello es correcto mediante hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="79b30-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="79b30-241">Cuando se ha enviado correctamente la topología de hello, Hola **aluvión de topologías** para clúster Hola debería aparecer.</span><span class="sxs-lookup"><span data-stu-id="79b30-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="79b30-242">Seleccione hello **WordCount** topología de hello mostrar tooview información acerca de hello ejecutando topología.</span><span class="sxs-lookup"><span data-stu-id="79b30-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="79b30-243">También puede ver **topologías de Storm** desde el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="79b30-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="79b30-244">Expanda **Azure** > **HDInsight**, haga clic con el botón derecho en un clúster de Storm en HDInsight y luego seleccione **Ver topologías de Storm**.</span><span class="sxs-lookup"><span data-stu-id="79b30-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="79b30-245">tooview información sobre los componentes de Hola de topología de hello, haga doble clic en el componente de hello en el diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="79b30-246">De hello **resumen de la topología** ver, haga clic en **Kill** topología de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="79b30-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="79b30-247">Topologías de Storm continuar toorun hasta que están desactivadas o clúster de Hola se elimina.</span><span class="sxs-lookup"><span data-stu-id="79b30-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="79b30-248">Topología transaccional</span><span class="sxs-lookup"><span data-stu-id="79b30-248">Transactional topology</span></span>

<span data-ttu-id="79b30-249">topología anterior Hello es no transaccional.</span><span class="sxs-lookup"><span data-stu-id="79b30-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="79b30-250">componentes de Hola de topología de hello implementar mensajes tooreplaying de funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="79b30-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="79b30-251">Para obtener un ejemplo de una topología transaccional, cree un proyecto y seleccione **aluvión de ejemplo** como tipo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="79b30-252">Topologías transaccionales implementan Hola después de reproducción de toosupport de datos:</span><span class="sxs-lookup"><span data-stu-id="79b30-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="79b30-253">**Almacenamiento en caché de metadatos**: pitorro Hola debe almacenar metadatos sobre los datos de hello emitidos, por lo que pueden recuperar datos de Hola y emitir nuevo si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="79b30-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="79b30-254">Como datos de hello emitidos por el ejemplo hello están pequeños, datos sin procesar de hello en cada tupla se almacenan en un diccionario para la reproducción.</span><span class="sxs-lookup"><span data-stu-id="79b30-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="79b30-255">**Confirmación**: pueden llamar todos los tornillos de topología de hello `this.ctx.Ack(tuple)` tooacknowledge que ha procesado correctamente una tupla.</span><span class="sxs-lookup"><span data-stu-id="79b30-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="79b30-256">Cuando todos los tornillos tienen realizados Hola tupla, Hola `Ack` se invoca el método de pitorro Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="79b30-257">Hola `Ack` método permite que los datos de tooremove de pitorro Hola que se almacenó en caché para la reproducción.</span><span class="sxs-lookup"><span data-stu-id="79b30-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="79b30-258">**Un error**: pueden llamar todos los tornillos `this.ctx.Fail(tuple)` tooindicate que el procesamiento no se pudo realizar una tupla.</span><span class="sxs-lookup"><span data-stu-id="79b30-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="79b30-259">Error de Hello propaga toohello `Fail` método de pitorro hello, donde se pueden reproducir Hola tupla mediante el uso de metadatos que están almacenados.</span><span class="sxs-lookup"><span data-stu-id="79b30-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="79b30-260">**Id. de secuencia**: al emitir una tupla, se puede especificar un identificador de secuencia único.</span><span class="sxs-lookup"><span data-stu-id="79b30-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="79b30-261">Este valor identifica tupla hello para el procesamiento de reproducción (confirmación y error).</span><span class="sxs-lookup"><span data-stu-id="79b30-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="79b30-262">Por ejemplo, Hola pitorro en hello **aluvión de ejemplo** utiliza el proyecto siguiente Hola al emitir los datos:</span><span class="sxs-lookup"><span data-stu-id="79b30-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="79b30-263">Este código emite una tupla que contiene una secuencia predeterminada de toohello de oración, con valor de identificador de secuencia de hello contenido en **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="79b30-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="79b30-264">En este ejemplo, **lastSeqId** se incrementa con cada tupla emitida.</span><span class="sxs-lookup"><span data-stu-id="79b30-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="79b30-265">Como se muestra en hello **aluvión de ejemplo** proyecto de equipo y si un componente es transaccional pueden establecerse en tiempo de ejecución, en función de la configuración.</span><span class="sxs-lookup"><span data-stu-id="79b30-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="79b30-266">Topología híbrida con C# y Java</span><span class="sxs-lookup"><span data-stu-id="79b30-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="79b30-267">También puede usar herramientas de Data Lake para Visual Studio toocreate híbrida las topologías, donde algunos componentes estén C# y otras son Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="79b30-268">Para ver un ejemplo de una topología híbrida, cree un proyecto y seleccione **Muestra híbrida de Storm**.</span><span class="sxs-lookup"><span data-stu-id="79b30-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="79b30-269">Este tipo de ejemplo muestra hello siguientes conceptos:</span><span class="sxs-lookup"><span data-stu-id="79b30-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="79b30-270">**Spout de Java** y **bolt de C#**: definidos en **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="79b30-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="79b30-271">Una versión transaccional se define en **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="79b30-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="79b30-272">**Spout de C#** y **bolt de Java**: definidos en **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="79b30-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="79b30-273">Una versión transaccional se define en **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="79b30-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="79b30-274">Esta versión también muestra cómo toouse Clojure código de un archivo de texto como un componente de Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="79b30-275">topología de hello tooswitch que se usa cuando se envía el proyecto de hello, basta con mover hello `[Active(true)]` topología de toohello de instrucción que desea utilizar toouse, antes de enviar toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="79b30-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="79b30-276">Todos los archivos de Java de hello necesarios se proporcionan como parte de este proyecto en hello **JavaDependency** carpeta.</span><span class="sxs-lookup"><span data-stu-id="79b30-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="79b30-277">Tenga en cuenta los siguiente de hello cuando está creando y enviando una topología híbrida:</span><span class="sxs-lookup"><span data-stu-id="79b30-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="79b30-278">Debe usar **JavaComponentConstructor** toocreate una instancia de clase de Java para un pitorro o rayo Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="79b30-279">Debe usar **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON los objetos de datos de tooserialize entre o salga de componentes de Java en Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="79b30-280">Al enviar el servidor de toohello de topología de hello, debe usar hello **configuraciones adicionales** Hola de opción toospecify **las rutas de acceso de Java**.</span><span class="sxs-lookup"><span data-stu-id="79b30-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="79b30-281">ruta de acceso de Hello especificada debe ser el directorio de Hola que contiene los archivos JAR de Hola que contienen las clases de Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="79b30-282">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="79b30-282">Azure Event Hubs</span></span>

<span data-ttu-id="79b30-283">Versión SCP.NET 0.9.4.203 presenta una nueva clase y método específicamente para trabajar con pitorro de concentrador de eventos de hello (pitorro Java que lee los centros de eventos).</span><span class="sxs-lookup"><span data-stu-id="79b30-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="79b30-284">Cuando se crea una topología que utiliza un pitorro concentrador de eventos, use Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="79b30-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="79b30-285">**EventHubSpoutConfig** clase: crea un objeto que contiene la configuración de Hola de componente de pitorro Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="79b30-286">**TopologyBuilder.SetEventHubSpout** método: agrega topología de hello concentrador de eventos pitorro componente toohello.</span><span class="sxs-lookup"><span data-stu-id="79b30-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="79b30-287">Deberá seguir usando hello **CustomizedInteropJSONSerializer** tooserialize datos producidos por pitorro Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="79b30-288"><a id="configurationmanager"></a>Uso de ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="79b30-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="79b30-289">No utilice **ConfigurationManager** tooretrieve configuración de valores comprendidos entre el tornillo y apetezca charlar componentes.</span><span class="sxs-lookup"><span data-stu-id="79b30-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="79b30-290">Si lo hace, puede generar una excepción de puntero nulo.</span><span class="sxs-lookup"><span data-stu-id="79b30-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="79b30-291">En su lugar, configuración de hello para el proyecto se pasó a topología aluvión de Hola como un par de clave y valor en el contexto de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="79b30-292">Cada componente que se basa en valores de configuración debe recuperarlos desde el contexto de Hola durante la inicialización.</span><span class="sxs-lookup"><span data-stu-id="79b30-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="79b30-293">Hello código siguiente se muestra cómo tooretrieve estos valores:</span><span class="sxs-lookup"><span data-stu-id="79b30-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="79b30-294">Si utiliza un `Get` método tooreturn una instancia del componente, debe asegurarse de que pasa tanto hello `Context` y `Dictionary<string, Object>` constructor toohello de parámetros.</span><span class="sxs-lookup"><span data-stu-id="79b30-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="79b30-295">el ejemplo siguiente se Hello es básico `Get` método que pasa correctamente estos valores:</span><span class="sxs-lookup"><span data-stu-id="79b30-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="79b30-296">Cómo tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="79b30-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="79b30-297">Las versiones recientes de SCP.NET admiten la actualización de paquetes a través de NuGet.</span><span class="sxs-lookup"><span data-stu-id="79b30-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="79b30-298">Cuando está disponible una nueva actualización, recibirá una notificación de actualización.</span><span class="sxs-lookup"><span data-stu-id="79b30-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="79b30-299">comprobación de toomanually para realizar una actualización, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="79b30-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="79b30-300">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="79b30-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="79b30-301">En el Administrador de paquetes de saludo, seleccione **actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="79b30-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="79b30-302">Si hay disponible una actualización, se mostrará una lista.</span><span class="sxs-lookup"><span data-stu-id="79b30-302">If an update is available, it is listed.</span></span> <span data-ttu-id="79b30-303">Haga clic en **actualización** para tooinstall de paquetes de saludo se.</span><span class="sxs-lookup"><span data-stu-id="79b30-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79b30-304">Si el proyecto se creó con una versión anterior de SCP.NET que no utilizan NuGet, debe realizar Hola después de la versión más reciente de pasos tooupdate tooa:</span><span class="sxs-lookup"><span data-stu-id="79b30-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="79b30-305">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="79b30-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="79b30-306">Con hello **búsqueda** campo, busque y, a continuación, agregar, **Microsoft.SCP.Net.SDK** toohello proyecto.</span><span class="sxs-lookup"><span data-stu-id="79b30-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="79b30-307">Solución de problemas comunes de las topologías</span><span class="sxs-lookup"><span data-stu-id="79b30-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="79b30-308">Excepciones de puntero nulo</span><span class="sxs-lookup"><span data-stu-id="79b30-308">Null pointer exceptions</span></span>

<span data-ttu-id="79b30-309">Cuando se utiliza una topología de C# con un clúster de HDInsight basados en Linux, el tornillo y apetezca charlar componentes que usan **ConfigurationManager** tooread opciones de configuración en tiempo de ejecución pueden devolver las excepciones de puntero nulo.</span><span class="sxs-lookup"><span data-stu-id="79b30-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="79b30-310">configuración de Hello para el proyecto se pasó a topología aluvión de Hola como un par de clave y valor en el contexto de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="79b30-311">Se puede recuperar del objeto de diccionario de Hola que se pasa tooyour componentes cuando se inicializan.</span><span class="sxs-lookup"><span data-stu-id="79b30-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="79b30-312">Para obtener más información, vea hello [ConfigurationManager](#configurationmanager) sección de este documento.</span><span class="sxs-lookup"><span data-stu-id="79b30-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="79b30-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="79b30-313">System.TypeLoadException</span></span>

<span data-ttu-id="79b30-314">Cuando se utiliza una topología de C# con un clúster de HDInsight basados en Linux, puede encontrar Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="79b30-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="79b30-315">Este error se produce cuando se usa un archivo binario que no es compatible con la versión de Hola de .NET que admita Mono.</span><span class="sxs-lookup"><span data-stu-id="79b30-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="79b30-316">En el caso de los clústeres de HDInsight basados en Linux, debe asegurarse de que el proyecto use archivos binarios compilados para .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="79b30-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="79b30-317">Prueba de una topología localmente</span><span class="sxs-lookup"><span data-stu-id="79b30-317">Test a topology locally</span></span>

<span data-ttu-id="79b30-318">Aunque es fácil toodeploy un clúster de tooa topología, en algunos casos, puede que tenga tootest una topología localmente.</span><span class="sxs-lookup"><span data-stu-id="79b30-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="79b30-319">Usar hello siguiendo los pasos toorun y pruebe la topología de ejemplo de Hola en este tutorial localmente en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="79b30-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="79b30-320">Las pruebas locales solo funcionan para topologías básicas de C#.</span><span class="sxs-lookup"><span data-stu-id="79b30-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="79b30-321">No se pueden usar pruebas locales para las topologías híbridas o para las topologías que usan varias secuencias.</span><span class="sxs-lookup"><span data-stu-id="79b30-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="79b30-322">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="79b30-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="79b30-323">En Propiedades del proyecto hello, cambie hello **tipo de salida** demasiado**aplicación de consola**.</span><span class="sxs-lookup"><span data-stu-id="79b30-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Captura de pantalla de las propiedades del proyecto con Tipo de salida resaltado](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="79b30-325">Recuerde hello toochange **tipo de salida** realizar copia demasiado**biblioteca de clases** antes de implementar el clúster de hello topología tooa.</span><span class="sxs-lookup"><span data-stu-id="79b30-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="79b30-326">En **el Explorador de soluciones**, haga clic en proyecto de hello y, a continuación, seleccione **agregar** > **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="79b30-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="79b30-327">Seleccione **clase**y escriba **LocalTest.cs** como nombre de la clase hello.</span><span class="sxs-lookup"><span data-stu-id="79b30-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="79b30-328">Por último, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="79b30-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="79b30-329">Abra **LocalTest.cs**y agregue Hola siguiente **con** declaración en la parte superior de hello:</span><span class="sxs-lookup"><span data-stu-id="79b30-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="79b30-330">Use Hola siguiente de código como contenido de Hola de hello **LocalTest** clase:</span><span class="sxs-lookup"><span data-stu-id="79b30-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="79b30-331">Tomar una tooread momento a través de comentarios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="79b30-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="79b30-332">Este código usa **LocalContext** toorun componentes de hello en el entorno de desarrollo de Hola y continúa el flujo de datos de hello entre los archivos de tootext de componentes en la unidad local Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="79b30-333">Abra **Program.cs**y agregue Hola después toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="79b30-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="79b30-334">Guardar los cambios de hello y, a continuación, haga clic en **F5** o seleccione **depurar** > **Iniciar depuración** proyecto de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="79b30-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="79b30-335">Debe aparecer una ventana de consola y registrar el estado del progreso de las pruebas de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="79b30-336">Cuando **terminado las pruebas** aparece, presione cualquier ventana de hello tooclose clave.</span><span class="sxs-lookup"><span data-stu-id="79b30-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="79b30-337">Use **el Explorador de Windows** directorio de hello toolocate que contiene el proyecto.</span><span class="sxs-lookup"><span data-stu-id="79b30-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="79b30-338">Por ejemplo: **C:\Usuarios\<su_nombre_de_usuario>\Documentos\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="79b30-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="79b30-339">En este directorio, abra **Bin** y haga clic en **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="79b30-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="79b30-340">Debería ver los archivos de texto hello que se producen cuando se ejecutó hello: sentences.txt, counter.txt y splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="79b30-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="79b30-341">Abra cada archivo de texto e inspeccionar los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="79b30-342">Los datos de cadena se guardan como persistentes como una matriz de valores decimales en estos archivos.</span><span class="sxs-lookup"><span data-stu-id="79b30-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="79b30-343">Por ejemplo, \[[97,103,111]] Hola **splitter.txt** archivo es palabra Hola *y*.</span><span class="sxs-lookup"><span data-stu-id="79b30-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="79b30-344">Estar seguro de hello tooset **tipo de proyecto** realizar copia demasiado**biblioteca de clases** antes de implementar tooa Storm en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79b30-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="79b30-345">Información del registro</span><span class="sxs-lookup"><span data-stu-id="79b30-345">Log information</span></span>

<span data-ttu-id="79b30-346">Puede registrar fácilmente información de los componentes de la topología mediante `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="79b30-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="79b30-347">Por ejemplo, la siguiente Hola crea una entrada de registro informativo:</span><span class="sxs-lookup"><span data-stu-id="79b30-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="79b30-348">Puede verse información registrada de hello **registro del servicio de Hadoop**, que se encuentra en **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="79b30-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="79b30-349">Expanda la entrada de Hola para su Storm en clúster de HDInsight y, a continuación, expanda **registro del servicio de Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="79b30-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="79b30-350">Por último, seleccione tooview de archivo de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="79b30-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="79b30-351">Hola registros se almacenan en hello cuenta de almacenamiento de Azure que es utilizada por el clúster.</span><span class="sxs-lookup"><span data-stu-id="79b30-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="79b30-352">registros de hello tooview en Visual Studio, debe iniciar sesión en toohello suscripción de Azure que pertenece la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="79b30-353">Visualización de la información del error</span><span class="sxs-lookup"><span data-stu-id="79b30-353">View error information</span></span>

<span data-ttu-id="79b30-354">errores de tooview que se han producido en una topología de ejecución, utilice Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="79b30-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="79b30-355">De **Explorador de servidores**, haga clic en hello Storm en clúster de HDInsight y seleccione **topologías aluvión de vista**.</span><span class="sxs-lookup"><span data-stu-id="79b30-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="79b30-356">Para hello **apetezca charlar** y **tornillos**, hello **último Error** columna contiene información sobre el último error de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="79b30-357">Seleccione hello **apetezca charlar un identificador** o **Id. de rayo** para el componente de Hola que tiene un error que aparece.</span><span class="sxs-lookup"><span data-stu-id="79b30-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="79b30-358">En página de detalles de hello es error adicional, muestra información aparece en hello **errores** sección final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="79b30-359">tooobtain obtener más información, seleccione un **puerto** de hello **ejecutor** sección de página de hello, registro de trabajo de toosee Hola aluvión de hello últimos minutos.</span><span class="sxs-lookup"><span data-stu-id="79b30-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="79b30-360">Errores en el envío de topologías</span><span class="sxs-lookup"><span data-stu-id="79b30-360">Errors submitting topologies</span></span>

<span data-ttu-id="79b30-361">Si se producen errores al enviar un tooHDInsight topología, puede encontrar registros para los componentes de servidor de Hola que controlan la presentación de la topología en su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79b30-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="79b30-362">tooretrieve estos registros, Hola de uso siguiente comando desde una línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="79b30-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="79b30-363">Reemplace __sshuser__ con la cuenta de usuario SSH para clúster Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="79b30-364">Reemplace __clustername__ con el nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79b30-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="79b30-365">Para más información sobre cómo usar `scp` y `ssh` con HDInsight, vea [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="79b30-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="79b30-366">Se pueden producir errores en los envíos por varios motivos:</span><span class="sxs-lookup"><span data-stu-id="79b30-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="79b30-367">JDK no está instalado o no está en la ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="79b30-368">Dependencias de Java necesarias no se incluyen en el envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="79b30-369">Dependencias no compatibles.</span><span class="sxs-lookup"><span data-stu-id="79b30-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="79b30-370">Nombres de topologías duplicados.</span><span class="sxs-lookup"><span data-stu-id="79b30-370">Duplicate topology names.</span></span>

<span data-ttu-id="79b30-371">Si hello `hdinsight-scpwebapi.out` registro contiene un `FileNotFoundException`, esto podría deberse a Hola condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="79b30-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="79b30-372">Hola JDK no está en la ruta de acceso de hello en el entorno de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="79b30-373">Compruebe que Hola JDK está instalado en el entorno de desarrollo de Hola y que `%JAVA_HOME%/bin` está en la ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="79b30-374">Falta una dependencia de Java.</span><span class="sxs-lookup"><span data-stu-id="79b30-374">You are missing a Java dependency.</span></span> <span data-ttu-id="79b30-375">Asegúrese de que va a incluir los archivos .jar necesarios como parte del envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="79b30-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79b30-376">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79b30-376">Next steps</span></span>

<span data-ttu-id="79b30-377">Para obtener un ejemplo de procesamiento de datos desde Event Hubs, vea [Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="79b30-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="79b30-378">Para ver un ejemplo de una topología de C# que divide los datos de una secuencia en varias secuencias, consulte [Ejemplo de Storm en C#](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="79b30-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="79b30-379">toodiscover obtener más información acerca de cómo crear topologías de C#, vea [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="79b30-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="79b30-380">Para más toowork maneras con HDInsight y Storm más muestras de HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="79b30-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="79b30-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="79b30-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="79b30-382">Guía de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="79b30-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="79b30-383">**Apache Storm en HDInsight**</span><span class="sxs-lookup"><span data-stu-id="79b30-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="79b30-384">Implementación y supervisión de topologías con Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="79b30-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="79b30-385">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="79b30-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="79b30-386">**Apache Hadoop en HDInsight**</span><span class="sxs-lookup"><span data-stu-id="79b30-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="79b30-387">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="79b30-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="79b30-388">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="79b30-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="79b30-389">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="79b30-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="79b30-390">**Apache HBase en HDInsight**</span><span class="sxs-lookup"><span data-stu-id="79b30-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="79b30-391">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="79b30-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
