---
title: "Topologías de Apache Storm con Visual Studio y C# - Azure HDInsight | Microsoft Docs"
description: "Aprenda a crear topologías de Storm en C#. Cree una sencilla topología de recuento de palabras en Visual Studio con las herramientas de Hadoop para Visual Studio."
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
ms.openlocfilehash: 3ee89b6644ba395e0a6c28ecc2c082c2f7393ac8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d8207-104">Desarrollo de topologías de C# para Apache Storm con Herramientas de Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8207-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="d8207-105">Aprenda a crear una topología de Storm de C# con Herramientas de Azure Data Lake (Hadoop) para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8207-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="d8207-106">Este documento le guía a través del proceso para crear un proyecto de Storm en Visual Studio, probarlo localmente e implementarlo en un clúster de Apache Storm en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="d8207-107">También aprenderá a crear topologías híbridas que usan componentes de C# y Java.</span><span class="sxs-lookup"><span data-stu-id="d8207-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="d8207-108">Aunque los pasos descritos en este documento se basan en un entorno de desarrollo de Windows con Visual Studio, el proyecto compilado se puede enviar a un clúster de HDInsight basado en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="d8207-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="d8207-109">Solo los clústeres basados en Linux creados después del 28 de octubre de 2016 admiten topologías SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="d8207-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="d8207-110">Para usar una topología de C# con un clúster basado en Linux, debe actualizar el paquete NuGet Microsoft.SCP.Net.SDK usado en el proyecto a la versión 0.10.0.6 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d8207-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="d8207-111">La versión del paquete también debe coincidir con la versión principal de Storm instalada en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="d8207-112">Versión de HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8207-112">HDInsight version</span></span> | <span data-ttu-id="d8207-113">Versión de Storm</span><span class="sxs-lookup"><span data-stu-id="d8207-113">Storm version</span></span> | <span data-ttu-id="d8207-114">Versión de SCP.NET</span><span class="sxs-lookup"><span data-stu-id="d8207-114">SCP.NET version</span></span> | <span data-ttu-id="d8207-115">Versión de Mono predeterminada</span><span class="sxs-lookup"><span data-stu-id="d8207-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="d8207-116">3.3</span><span class="sxs-lookup"><span data-stu-id="d8207-116">3.3</span></span> |<span data-ttu-id="d8207-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="d8207-117">0.10.x</span></span> |<span data-ttu-id="d8207-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="d8207-118">0.10.x.x</span></span></br><span data-ttu-id="d8207-119">(solo en HDInsight basado en Windows)</span><span class="sxs-lookup"><span data-stu-id="d8207-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="d8207-120">N/D</span><span class="sxs-lookup"><span data-stu-id="d8207-120">NA</span></span> |
| <span data-ttu-id="d8207-121">3.4</span><span class="sxs-lookup"><span data-stu-id="d8207-121">3.4</span></span> | <span data-ttu-id="d8207-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="d8207-122">0.10.0.x</span></span> | <span data-ttu-id="d8207-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="d8207-123">0.10.0.x</span></span> | <span data-ttu-id="d8207-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="d8207-124">3.2.8</span></span> |
| <span data-ttu-id="d8207-125">3,5</span><span class="sxs-lookup"><span data-stu-id="d8207-125">3.5</span></span> | <span data-ttu-id="d8207-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="d8207-126">1.0.2.x</span></span> | <span data-ttu-id="d8207-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="d8207-127">1.0.0.x</span></span> | <span data-ttu-id="d8207-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="d8207-128">4.2.1</span></span> |
| <span data-ttu-id="d8207-129">3.6</span><span class="sxs-lookup"><span data-stu-id="d8207-129">3.6</span></span> | <span data-ttu-id="d8207-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="d8207-130">1.1.0.x</span></span> | <span data-ttu-id="d8207-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="d8207-131">1.0.0.x</span></span> | <span data-ttu-id="d8207-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="d8207-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d8207-133">Las topologías de C# en clústeres basados en Linux deben usar .NET 4.5, y emplear Mono para ejecutarse en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="d8207-134">Compruebe el documento de [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para ver las posibles incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="d8207-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="d8207-135">Instalación de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8207-135">Install Visual Studio</span></span>

<span data-ttu-id="d8207-136">Puede desarrollar topologías de C# con SCP.NET mediante una de las siguientes versiones de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d8207-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="d8207-137">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="d8207-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="d8207-138">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="d8207-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="d8207-139">Visual Studio 2015 o [Visual Studio Community 2015](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="d8207-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="d8207-140">Visual Studio 2017 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="d8207-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d8207-141">Instalación de Herramientas de Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8207-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="d8207-142">Para instalar Herramientas de Data Lake para Visual Studio, siga los pasos de [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) (Introducción al uso de Herramientas de Data Lake para Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d8207-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="d8207-143">Instalar Java</span><span class="sxs-lookup"><span data-stu-id="d8207-143">Install Java</span></span>

<span data-ttu-id="d8207-144">Cuando se envía una topología de Storm desde Visual Studio, SCP.NET genera un archivo zip que contiene la topología y las dependencias.</span><span class="sxs-lookup"><span data-stu-id="d8207-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="d8207-145">Java se usa para crear estos archivos zip, ya que emplea un formato más compatible con los clústeres basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="d8207-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="d8207-146">Instale Java Development Kit (JDK) 7 o posterior en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d8207-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="d8207-147">Puede obtener el JDK de Oracle en [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="d8207-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="d8207-148">También puede usar [otras distribuciones de Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="d8207-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="d8207-149">La variable de entorno `JAVA_HOME` debe apuntar al directorio que contiene Java.</span><span class="sxs-lookup"><span data-stu-id="d8207-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="d8207-150">La variable de entorno `PATH` debe incluir el directorio `%JAVA_HOME%\bin`.</span><span class="sxs-lookup"><span data-stu-id="d8207-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="d8207-151">Puede usar la aplicación de consola de C# siguiente para comprobar que Java y el JDK se han instalado correctamente:</span><span class="sxs-lookup"><span data-stu-id="d8207-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

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

## <a name="storm-templates"></a><span data-ttu-id="d8207-152">Plantillas de Storm</span><span class="sxs-lookup"><span data-stu-id="d8207-152">Storm templates</span></span>

<span data-ttu-id="d8207-153">Herramientas de Data Lake para Visual Studio proporciona las siguientes plantillas:</span><span class="sxs-lookup"><span data-stu-id="d8207-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="d8207-154">Tipo de proyecto</span><span class="sxs-lookup"><span data-stu-id="d8207-154">Project type</span></span> | <span data-ttu-id="d8207-155">Muestra</span><span class="sxs-lookup"><span data-stu-id="d8207-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="d8207-156">Storm Application</span><span class="sxs-lookup"><span data-stu-id="d8207-156">Storm Application</span></span> |<span data-ttu-id="d8207-157">Un proyecto vacío de topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="d8207-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="d8207-158">Storm Azure SQL Writer Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="d8207-159">Cómo escribir en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d8207-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="d8207-160">Storm Azure Cosmos DB Reader Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="d8207-161">Cómo leer desde Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8207-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="d8207-162">Storm Azure Cosmos DB Writer Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="d8207-163">Cómo escribir en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8207-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="d8207-164">Storm EventHub Reader Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="d8207-165">Cómo leer desde Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d8207-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="d8207-166">Storm EventHub Writer Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="d8207-167">Cómo escribir en Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d8207-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="d8207-168">Storm HBase Reader Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="d8207-169">Cómo leer desde HBase en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="d8207-170">Storm HBase Writer Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="d8207-171">Cómo escribir en HBase en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="d8207-172">Storm Hybrid Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="d8207-173">Cómo usar un componente de Java.</span><span class="sxs-lookup"><span data-stu-id="d8207-173">How to use a Java component.</span></span> |
| <span data-ttu-id="d8207-174">Storm Sample</span><span class="sxs-lookup"><span data-stu-id="d8207-174">Storm Sample</span></span> |<span data-ttu-id="d8207-175">Una topología de recuento de palabras básica.</span><span class="sxs-lookup"><span data-stu-id="d8207-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="d8207-176">No todas las plantillas funcionará con HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="d8207-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="d8207-177">Es posible que los paquetes NuGet que las plantillas usan no sean compatibles con Mono.</span><span class="sxs-lookup"><span data-stu-id="d8207-177">Nuget packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="d8207-178">Revise el documento sobre la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/) y use el [Analizador de portabilidad de .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) para identificar potenciales problemas.</span><span class="sxs-lookup"><span data-stu-id="d8207-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="d8207-179">En los pasos de este documento, usará el tipo de proyecto Storm Application básico para crear una topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="d8207-180">Notas de plantillas de HBase</span><span class="sxs-lookup"><span data-stu-id="d8207-180">HBase templates notes</span></span>

<span data-ttu-id="d8207-181">Las plantillas de lector y escritor de HBase usan la API de REST de HBase, no la API de Java de HBase, para comunicarse con un HBase en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="d8207-182">Notas de plantillas de EventHub</span><span class="sxs-lookup"><span data-stu-id="d8207-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8207-183">Es posible que el componente de spout de EventHub basado en Java incluido en la plantilla de lector de EventHub no funcione con Storm en HDInsight versión 3.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d8207-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="d8207-184">Hay una versión actualizada de este componente disponible en [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="d8207-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="d8207-185">Para obtener una topología de ejemplo que usa este componente y funciona con Storm en HDInsight 3.5, vea [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="d8207-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="d8207-186">Creación de una topología de C#</span><span class="sxs-lookup"><span data-stu-id="d8207-186">Create a C# topology</span></span>

1. <span data-ttu-id="d8207-187">Abra Visual Studio, seleccione **Archivo** > **Nuevo** y luego seleccione **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d8207-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="d8207-188">En la ventana **Nuevo proyecto**, expanda **Instalado** > **Plantillas** y seleccione **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="d8207-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="d8207-189">En la lista de plantillas, seleccione **Aplicación de Storm**.</span><span class="sxs-lookup"><span data-stu-id="d8207-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="d8207-190">En la parte inferior de la pantalla, escriba **WordCount** como nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8207-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![Captura de pantalla de la ventana Nuevo proyecto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="d8207-192">Después de crear el proyecto, debe tener los siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="d8207-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="d8207-193">**Program.cs**: este archivo define la topología del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d8207-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="d8207-194">Una topología predeterminada que consta de un spout y un bolt se crea de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d8207-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="d8207-195">**Spout.cs**: un spout de ejemplo que emite números aleatorios</span><span class="sxs-lookup"><span data-stu-id="d8207-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="d8207-196">**Bolt.cs**: un bolt de ejemplo que mantiene un recuento de los números emitidos por el spout.</span><span class="sxs-lookup"><span data-stu-id="d8207-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="d8207-197">Cuando se crea el proyecto, NuGet descarga el [paquete SCP.NET](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/) más reciente.</span><span class="sxs-lookup"><span data-stu-id="d8207-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="d8207-198">Implementación del spout</span><span class="sxs-lookup"><span data-stu-id="d8207-198">Implement the spout</span></span>

1. <span data-ttu-id="d8207-199">Abra **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="d8207-199">Open **Spout.cs**.</span></span> <span data-ttu-id="d8207-200">Los spouts se usan para leer los datos en una topología de un origen externo.</span><span class="sxs-lookup"><span data-stu-id="d8207-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="d8207-201">Los componentes principales de un spout son:</span><span class="sxs-lookup"><span data-stu-id="d8207-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="d8207-202">**NextTuple**: llamado por Storm cuando se permite que el spout emita nuevas tuplas</span><span class="sxs-lookup"><span data-stu-id="d8207-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="d8207-203">**Ack** (solo topología transaccional): controla las confirmaciones iniciadas por otros componentes de la topología para tuplas enviadas desde el spout.</span><span class="sxs-lookup"><span data-stu-id="d8207-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="d8207-204">La confirmación de una tupla permite que el spout conozca que se ha procesado correctamente por componentes de bajada.</span><span class="sxs-lookup"><span data-stu-id="d8207-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="d8207-205">**Fail** (solo topología transaccional): controla las tuplas que producen un error al procesar otros componentes de la topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="d8207-206">Implementar un método Fail le permite volver a emitir la tupla para que se pueda procesar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="d8207-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="d8207-207">Reemplace el contenido de la clase **Spout** por el texto siguiente.</span><span class="sxs-lookup"><span data-stu-id="d8207-207">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="d8207-208">Este spout emite aleatoriamente una frase en la topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-208">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
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

### <a name="implement-the-bolts"></a><span data-ttu-id="d8207-209">Implementación de los bolts</span><span class="sxs-lookup"><span data-stu-id="d8207-209">Implement the bolts</span></span>

1. <span data-ttu-id="d8207-210">Elimine el archivo **Bolt.cs** existente del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d8207-210">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="d8207-211">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Agregar** > **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="d8207-211">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="d8207-212">En la lista, seleccione **Bolt de Storm** y escriba **Splitter.cs** como nombre.</span><span class="sxs-lookup"><span data-stu-id="d8207-212">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="d8207-213">Repita este proceso para crear un segundo bolt denominado **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="d8207-213">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="d8207-214">**Splitter.cs**: implementa un bolt que divide la frase en palabras individuales y emite una nueva secuencia de palabras.</span><span class="sxs-lookup"><span data-stu-id="d8207-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="d8207-215">**Counter.cs**: implementa un bolt que cuenta cada palabra y emite una nueva secuencia de palabras y el recuento de cada palabra.</span><span class="sxs-lookup"><span data-stu-id="d8207-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d8207-216">Estos bolts leen y escriben en las secuencias, pero también se puede usar un bolt para comunicarse con orígenes como una base de datos o un servicio.</span><span class="sxs-lookup"><span data-stu-id="d8207-216">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="d8207-217">Abra **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="d8207-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="d8207-218">Solo tiene un método de forma predeterminada: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="d8207-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="d8207-219">El método Execute se llama cuando el bolt recibe una tupla para el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="d8207-219">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="d8207-220">En este caso, puede leer y procesar las tuplas entrantes y emitir tuplas salientes.</span><span class="sxs-lookup"><span data-stu-id="d8207-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="d8207-221">Reemplace el contenido de la clase **Splitter** por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d8207-221">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
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

5. <span data-ttu-id="d8207-222">Abra **Counter.cs** y sustituya el contenido de la clase por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d8207-222">Open **Counter.cs**, and replace the class contents with the following:</span></span>

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
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
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

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-the-topology"></a><span data-ttu-id="d8207-223">Definición de la topología</span><span class="sxs-lookup"><span data-stu-id="d8207-223">Define the topology</span></span>

<span data-ttu-id="d8207-224">Los spouts y bolts se organizan en un gráfico, que define cómo fluyen los datos entre componentes.</span><span class="sxs-lookup"><span data-stu-id="d8207-224">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="d8207-225">Para esta topología, el gráfico es como sigue:</span><span class="sxs-lookup"><span data-stu-id="d8207-225">For this topology, the graph is as follows:</span></span>

![Diagrama de cómo se organizan los componentes](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="d8207-227">Las frases se emiten desde el spout y se distribuyen a las instancias del bolt divisor.</span><span class="sxs-lookup"><span data-stu-id="d8207-227">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="d8207-228">El bolt divisor divide las frases en palabras, que se distribuyen en el bolt contador.</span><span class="sxs-lookup"><span data-stu-id="d8207-228">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="d8207-229">Dado que el recuento de palabras se guarda localmente en la instancia del contador, queremos asegurarnos de que determinadas palabras fluyan a la misma instancia del bolt contador.</span><span class="sxs-lookup"><span data-stu-id="d8207-229">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="d8207-230">Cada instancia realiza el seguimiento de palabras específicas.</span><span class="sxs-lookup"><span data-stu-id="d8207-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="d8207-231">Dado que el bolt divisor no mantiene ningún estado, realmente no importa qué instancia del divisor recibe cada frase.</span><span class="sxs-lookup"><span data-stu-id="d8207-231">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="d8207-232">Abra **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="d8207-232">Open **Program.cs**.</span></span> <span data-ttu-id="d8207-233">El método importante aquí es **GetTopologyBuilder**, que se usa para definir la topología que se envía a Storm.</span><span class="sxs-lookup"><span data-stu-id="d8207-233">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="d8207-234">Reemplace el contenido de **GetTopologyBuilder** por el código siguiente para implementar la topología descrita anteriormente:</span><span class="sxs-lookup"><span data-stu-id="d8207-234">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
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

## <a name="submit-the-topology"></a><span data-ttu-id="d8207-235">Envío de la topología</span><span class="sxs-lookup"><span data-stu-id="d8207-235">Submit the topology</span></span>

1. <span data-ttu-id="d8207-236">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Submit to Storm on HDInsight** (Enviar a Storm en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="d8207-236">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d8207-237">Si se le solicita, introduzca las credenciales de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8207-237">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="d8207-238">Si tiene más de una suscripción, inicie sesión en la que contenga el clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-238">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="d8207-239">Seleccione el clúster de Storm en HDInsight desde el menú desplegable **Storm Cluster**  (Clúster de Storm y seleccione **Submit** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="d8207-239">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="d8207-240">Puede supervisar si el envío es correcto mediante la ventana **Salida** .</span><span class="sxs-lookup"><span data-stu-id="d8207-240">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="d8207-241">Cuando la topología se envíe correctamente, debe aparecer **topologías de Storm** del clúster.</span><span class="sxs-lookup"><span data-stu-id="d8207-241">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="d8207-242">Seleccione la topología **WordCount** en la lista para consultar la información acerca de la topología en ejecución.</span><span class="sxs-lookup"><span data-stu-id="d8207-242">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d8207-243">También puede ver **topologías de Storm** desde el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="d8207-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="d8207-244">Expanda **Azure** > **HDInsight**, haga clic con el botón derecho en un clúster de Storm en HDInsight y luego seleccione **Ver topologías de Storm**.</span><span class="sxs-lookup"><span data-stu-id="d8207-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="d8207-245">Para ver información sobre los componentes de la topología, haga doble clic en el componente en el diagrama.</span><span class="sxs-lookup"><span data-stu-id="d8207-245">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="d8207-246">Desde la vista **Resumen de la topología**, haga clic en **Eliminar** para detener la topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-246">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d8207-247">Las topologías de Storm continúan ejecutándose hasta que se desactiven o se elimine el clúster.</span><span class="sxs-lookup"><span data-stu-id="d8207-247">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="d8207-248">Topología transaccional</span><span class="sxs-lookup"><span data-stu-id="d8207-248">Transactional topology</span></span>

<span data-ttu-id="d8207-249">La topología anterior no es transaccional.</span><span class="sxs-lookup"><span data-stu-id="d8207-249">The previous topology is non-transactional.</span></span> <span data-ttu-id="d8207-250">Los componentes de la topología no implementan la funcionalidad para reproducir los mensajes.</span><span class="sxs-lookup"><span data-stu-id="d8207-250">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="d8207-251">Para ver un ejemplo de una topología transaccional, cree un proyecto y seleccione **Muestra de Storm** como tipo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="d8207-251">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="d8207-252">Las topologías transaccionales implementan lo siguiente para que admitan la reproducción de datos:</span><span class="sxs-lookup"><span data-stu-id="d8207-252">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="d8207-253">**Almacenamiento en caché de metadatos**: el spout debe almacenar metadatos sobre los datos emitidos para que los datos puedan recuperarse y volver a emitirse si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="d8207-253">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="d8207-254">Dado que los datos que emite la muestra son pequeños, los datos sin procesar de cada tupla se almacenan en un diccionario para la reproducción.</span><span class="sxs-lookup"><span data-stu-id="d8207-254">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="d8207-255">**Ack**: cada bolt de la topología puede llamar a `this.ctx.Ack(tuple)` para confirmar que ha procesado una tupla correctamente.</span><span class="sxs-lookup"><span data-stu-id="d8207-255">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="d8207-256">Una vez que todos los bolts han confirmado la tupla, se llama al método `Ack` del spout.</span><span class="sxs-lookup"><span data-stu-id="d8207-256">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="d8207-257">El método `Ack` permite al spout quitar los datos que se almacenaron en caché para la reproducción.</span><span class="sxs-lookup"><span data-stu-id="d8207-257">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="d8207-258">**Fail**: cada bolt puede llamar a `this.ctx.Fail(tuple)` para indicar que se produjo un error al procesar una tupla.</span><span class="sxs-lookup"><span data-stu-id="d8207-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="d8207-259">El error se propaga al método `Fail` del spout, donde la tupla puede reproducirse mediante metadatos almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="d8207-259">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="d8207-260">**Id. de secuencia**: al emitir una tupla, se puede especificar un identificador de secuencia único.</span><span class="sxs-lookup"><span data-stu-id="d8207-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="d8207-261">Este valor identifica la tupla para el procesamiento de reproducción (Ack y Fail).</span><span class="sxs-lookup"><span data-stu-id="d8207-261">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="d8207-262">Por ejemplo, el spout del proyecto **Muestra de Storm** utiliza los siguiente al emitir datos:</span><span class="sxs-lookup"><span data-stu-id="d8207-262">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="d8207-263">Este código emite una tupla que contiene una frase a la secuencia predeterminada, con el valor de identificador de secuencia contenido en **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="d8207-263">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="d8207-264">En este ejemplo, **lastSeqId** se incrementa con cada tupla emitida.</span><span class="sxs-lookup"><span data-stu-id="d8207-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="d8207-265">Como se muestra en el proyecto **Muestra de Storm**, se puede establecer si un componente es transaccional en runtime, según la configuración.</span><span class="sxs-lookup"><span data-stu-id="d8207-265">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="d8207-266">Topología híbrida con C# y Java</span><span class="sxs-lookup"><span data-stu-id="d8207-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="d8207-267">También puede usar Herramientas de Data Lake para Visual Studio para crear topologías híbridas, donde algunos componentes son de C# y otros de Java.</span><span class="sxs-lookup"><span data-stu-id="d8207-267">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="d8207-268">Para ver un ejemplo de una topología híbrida, cree un proyecto y seleccione **Muestra híbrida de Storm**.</span><span class="sxs-lookup"><span data-stu-id="d8207-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="d8207-269">Este tipo de ejemplo ilustra los conceptos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d8207-269">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="d8207-270">**Spout de Java** y **bolt de C#**: definidos en **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="d8207-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="d8207-271">Una versión transaccional se define en **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="d8207-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="d8207-272">**Spout de C#** y **bolt de Java**: definidos en **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="d8207-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="d8207-273">Una versión transaccional se define en **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="d8207-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d8207-274">Esta versión también muestra cómo usar código de Clojure desde un archivo de texto como un componente de Java.</span><span class="sxs-lookup"><span data-stu-id="d8207-274">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="d8207-275">Para cambiar la topología que se usa cuando se envía el proyecto, simplemente mueva la instrucción `[Active(true)]` a la topología que quiere usar antes de enviarla al clúster.</span><span class="sxs-lookup"><span data-stu-id="d8207-275">To switch the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d8207-276">Todos los archivos de Java necesarios se ofrecen como parte de este proyecto en la carpeta **JavaDependency** .</span><span class="sxs-lookup"><span data-stu-id="d8207-276">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="d8207-277">Tenga en cuenta lo siguiente al crear y enviar una topología híbrida:</span><span class="sxs-lookup"><span data-stu-id="d8207-277">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="d8207-278">Debe usar **JavaComponentConstructor** para crear una instancia de la clase de Java para un spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="d8207-278">You must use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="d8207-279">Debe usar **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** para serializar datos hacia y desde los componentes de Java a partir de objetos de Java a JSON.</span><span class="sxs-lookup"><span data-stu-id="d8207-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="d8207-280">Al enviar la topología al servidor, debe usar la opción **Configuraciones adicionales** para especificar las **rutas de acceso del archivo Java**.</span><span class="sxs-lookup"><span data-stu-id="d8207-280">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="d8207-281">La ruta especificada debe ser el directorio que contiene los archivos JAR que contienen las clases de Java.</span><span class="sxs-lookup"><span data-stu-id="d8207-281">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="d8207-282">Centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="d8207-282">Azure Event Hubs</span></span>

<span data-ttu-id="d8207-283">La versión 0.9.4.203 de SCP.NET presenta una nueva clase y un nuevo método específicos para trabajar con el spout del centro de eventos (un spout de Java que lee desde Event Hubs).</span><span class="sxs-lookup"><span data-stu-id="d8207-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="d8207-284">Al crear una topología que usa un spout del centro de eventos, emplee los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d8207-284">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="d8207-285">Clase **EventHubSpoutConfig**: crea un objeto que contiene la configuración del componente de spout.</span><span class="sxs-lookup"><span data-stu-id="d8207-285">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="d8207-286">Método **TopologyBuilder.SetEventHubSpout**: agrega el componente de spout del centro de eventos a la topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-286">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="d8207-287">Debe seguir usando **CustomizedInteropJSONSerializer** para serializar los datos generados por el spout.</span><span class="sxs-lookup"><span data-stu-id="d8207-287">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <span data-ttu-id="d8207-288"><a id="configurationmanager"></a>Uso de ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="d8207-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="d8207-289">No use **ConfigurationManager** para recuperar valores de configuración de los componentes de bolt y spout.</span><span class="sxs-lookup"><span data-stu-id="d8207-289">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="d8207-290">Si lo hace, puede generar una excepción de puntero nulo.</span><span class="sxs-lookup"><span data-stu-id="d8207-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="d8207-291">En su lugar, la configuración del proyecto se pasa a la topología de Storm como un par de clave y valor en el contexto de la topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-291">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="d8207-292">Cada componente que se basa en los valores de configuración debe recuperarlos del contexto durante la inicialización.</span><span class="sxs-lookup"><span data-stu-id="d8207-292">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="d8207-293">El código siguiente muestra cómo recuperar estos valores:</span><span class="sxs-lookup"><span data-stu-id="d8207-293">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="d8207-294">Si usa un método `Get` para devolver una instancia de su componente, debe asegurarse de que pasa los parámetros `Context` y `Dictionary<string, Object>` al constructor.</span><span class="sxs-lookup"><span data-stu-id="d8207-294">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="d8207-295">El ejemplo siguiente es un método `Get` básico que pasa estos valores correctamente:</span><span class="sxs-lookup"><span data-stu-id="d8207-295">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="d8207-296">Cómo actualizar SCP.NET</span><span class="sxs-lookup"><span data-stu-id="d8207-296">How to update SCP.NET</span></span>

<span data-ttu-id="d8207-297">Las versiones recientes de SCP.NET admiten la actualización de paquetes a través de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d8207-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="d8207-298">Cuando está disponible una nueva actualización, recibirá una notificación de actualización.</span><span class="sxs-lookup"><span data-stu-id="d8207-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="d8207-299">Para comprobar manualmente si hay una actualización, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d8207-299">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="d8207-300">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d8207-300">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="d8207-301">En el administrador de paquetes, seleccione **Actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="d8207-301">From the package manager, select **Updates**.</span></span> <span data-ttu-id="d8207-302">Si hay disponible una actualización, se mostrará una lista.</span><span class="sxs-lookup"><span data-stu-id="d8207-302">If an update is available, it is listed.</span></span> <span data-ttu-id="d8207-303">Haga clic en **Actualizar** para que el paquete la instale.</span><span class="sxs-lookup"><span data-stu-id="d8207-303">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8207-304">Si el proyecto se creó con una versión anterior de SCP.NET que no usó NuGet, debe realizar los pasos siguientes para actualizar a una versión más reciente:</span><span class="sxs-lookup"><span data-stu-id="d8207-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="d8207-305">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d8207-305">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="d8207-306">Mediante el campo **Búsqueda**, busque **Microsoft.SCP.Net.SDK** y agréguelo al proyecto.</span><span class="sxs-lookup"><span data-stu-id="d8207-306">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="d8207-307">Solución de problemas comunes de las topologías</span><span class="sxs-lookup"><span data-stu-id="d8207-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="d8207-308">Excepciones de puntero nulo</span><span class="sxs-lookup"><span data-stu-id="d8207-308">Null pointer exceptions</span></span>

<span data-ttu-id="d8207-309">Al usar una topología de C# con un clúster de HDInsight basado en Linux, los componentes de bolt y spout que usan **ConfigurationManager** para leer los valores de configuración en runtime pueden devolver excepciones de puntero nulo.</span><span class="sxs-lookup"><span data-stu-id="d8207-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="d8207-310">La configuración del proyecto se pasa a la topología de Storm como un par de clave y valor en el contexto de la topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-310">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="d8207-311">Se puede recuperar del objeto de diccionario que se pasó a los componentes cuando se inicializaron.</span><span class="sxs-lookup"><span data-stu-id="d8207-311">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="d8207-312">Para más información, vea la sección [ConfigurationManager](#configurationmanager) de este documento.</span><span class="sxs-lookup"><span data-stu-id="d8207-312">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="d8207-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="d8207-313">System.TypeLoadException</span></span>

<span data-ttu-id="d8207-314">Al usar una topología de C# con un clúster de HDInsight basado en Linux, puede aparecer el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="d8207-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="d8207-315">Este error se produce cuando se usa un archivo binario que no es compatible con la versión de .NET que admite Mono.</span><span class="sxs-lookup"><span data-stu-id="d8207-315">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="d8207-316">En el caso de los clústeres de HDInsight basados en Linux, debe asegurarse de que el proyecto use archivos binarios compilados para .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d8207-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="d8207-317">Prueba de una topología localmente</span><span class="sxs-lookup"><span data-stu-id="d8207-317">Test a topology locally</span></span>

<span data-ttu-id="d8207-318">Aunque es fácil implementar una topología en un clúster, en algunos casos puede que deba probar localmente una topología.</span><span class="sxs-lookup"><span data-stu-id="d8207-318">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="d8207-319">Siga los pasos que se muestran a continuación para ejecutar y probar localmente la topología de ejemplo de este tutorial en su entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d8207-319">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="d8207-320">Las pruebas locales solo funcionan para topologías básicas de C#.</span><span class="sxs-lookup"><span data-stu-id="d8207-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="d8207-321">No se pueden usar pruebas locales para las topologías híbridas o para las topologías que usan varias secuencias.</span><span class="sxs-lookup"><span data-stu-id="d8207-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="d8207-322">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="d8207-322">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="d8207-323">En las propiedades del proyecto, cambie el **tipo de salida** a **Aplicación de consola**.</span><span class="sxs-lookup"><span data-stu-id="d8207-323">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![Captura de pantalla de las propiedades del proyecto con Tipo de salida resaltado](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="d8207-325">No olvide cambiar el **tipo de salida** de nuevo a **Biblioteca de clases** antes de implementar la topología en un clúster.</span><span class="sxs-lookup"><span data-stu-id="d8207-325">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="d8207-326">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Agregar** > **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="d8207-326">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="d8207-327">Seleccione **Clase** y escriba **LocalTest.cs** como nombre de clase.</span><span class="sxs-lookup"><span data-stu-id="d8207-327">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="d8207-328">Por último, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d8207-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="d8207-329">Abra **LocalTest.cs** y agregue la siguiente instrucción **using** en la parte superior:</span><span class="sxs-lookup"><span data-stu-id="d8207-329">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="d8207-330">Use el código siguiente como contenido de la clase **LocalTest**:</span><span class="sxs-lookup"><span data-stu-id="d8207-330">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="d8207-331">Dedique un momento para leer los comentarios del código.</span><span class="sxs-lookup"><span data-stu-id="d8207-331">Take a moment to read through the code comments.</span></span> <span data-ttu-id="d8207-332">Este código usa **LocalContext** para ejecutar los componentes en el entorno de desarrollo y conserva la secuencia de datos entre componentes de los archivos de texto en la unidad local.</span><span class="sxs-lookup"><span data-stu-id="d8207-332">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="d8207-333">Abra **Program.cs** y agregue lo siguiente al método **Main**:</span><span class="sxs-lookup"><span data-stu-id="d8207-333">Open **Program.cs**, and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
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

2. <span data-ttu-id="d8207-334">Guarde los cambios y luego haga clic en **F5** o seleccione **Depurar** > **Iniciar depuración** para iniciar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d8207-334">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="d8207-335">Debe aparecer una ventana de consola y el estado del registro a medida que progresen las pruebas.</span><span class="sxs-lookup"><span data-stu-id="d8207-335">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="d8207-336">Cuando se muestre **Pruebas finalizadas** , presione cualquier tecla para cerrar la ventana.</span><span class="sxs-lookup"><span data-stu-id="d8207-336">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="d8207-337">Use el **Explorador de Windows** para buscar el directorio que contiene el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d8207-337">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="d8207-338">Por ejemplo: **C:\Usuarios\<su_nombre_de_usuario>\Documentos\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="d8207-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="d8207-339">En este directorio, abra **Bin** y haga clic en **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="d8207-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="d8207-340">Debería ver los archivos de texto que se generaron cuando se ejecutaron las pruebas: sentences.txt, counter.txt y splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="d8207-340">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="d8207-341">Abra cada archivo de texto e inspeccione los datos.</span><span class="sxs-lookup"><span data-stu-id="d8207-341">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d8207-342">Los datos de cadena se guardan como persistentes como una matriz de valores decimales en estos archivos.</span><span class="sxs-lookup"><span data-stu-id="d8207-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="d8207-343">Por ejemplo, \[[97,103,111]] en el archivo **splitter.txt** es la palabra *and*.</span><span class="sxs-lookup"><span data-stu-id="d8207-343">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="d8207-344">Asegúrese de volver a establecer el **tipo de proyecto** en **Biblioteca de clases** antes de implementarlo en un clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-344">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="d8207-345">Información del registro</span><span class="sxs-lookup"><span data-stu-id="d8207-345">Log information</span></span>

<span data-ttu-id="d8207-346">Puede registrar fácilmente información de los componentes de la topología mediante `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="d8207-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="d8207-347">Por ejemplo, lo siguiente creará una entrada del registro informativo:</span><span class="sxs-lookup"><span data-stu-id="d8207-347">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="d8207-348">Se puede ver la información registrada desde el **registro del servicio Hadoop**, que se encuentra en el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="d8207-348">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="d8207-349">Expanda la entrada del clúster de Storm en HDInsight y luego expanda **Registro del servicio Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="d8207-349">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="d8207-350">Por último, seleccione el archivo de registro que desea consultar.</span><span class="sxs-lookup"><span data-stu-id="d8207-350">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="d8207-351">Los registros se almacenan en la cuenta de Azure Storage que usa el clúster.</span><span class="sxs-lookup"><span data-stu-id="d8207-351">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="d8207-352">Para ver los registros en Visual Studio, debe iniciar sesión en la suscripción de Azure a la que pertenece la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d8207-352">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="d8207-353">Visualización de la información del error</span><span class="sxs-lookup"><span data-stu-id="d8207-353">View error information</span></span>

<span data-ttu-id="d8207-354">Para ver los errores que se han producido en una topología en ejecución, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d8207-354">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="d8207-355">En el **Explorador de servidores**, haga clic con el botón derecho en el clúster de Storm en HDInsight y seleccione **Ver topologías de Storm**.</span><span class="sxs-lookup"><span data-stu-id="d8207-355">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="d8207-356">En los componentes de **spout** y **bolt**, la columna **Último error** contiene información sobre el último error.</span><span class="sxs-lookup"><span data-stu-id="d8207-356">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="d8207-357">Seleccione el **id. de spout** o el **id. de bolt** del componente del que se muestra un error.</span><span class="sxs-lookup"><span data-stu-id="d8207-357">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="d8207-358">En la página de detalles que se muestra, se enumerará información adicional sobre el error en la sección **Errores** de la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="d8207-358">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="d8207-359">Para más información, seleccione un **puerto** en la sección **Executors** (Ejecutores) de la página para ver el registro de trabajo de Storm de los últimos minutos.</span><span class="sxs-lookup"><span data-stu-id="d8207-359">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="d8207-360">Errores en el envío de topologías</span><span class="sxs-lookup"><span data-stu-id="d8207-360">Errors submitting topologies</span></span>

<span data-ttu-id="d8207-361">Si se producen errores al enviar una topología a HDInsight, puede encontrar registros para los componentes de servidor que controlan el envío de la topología en su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-361">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="d8207-362">Para recuperar estos registros, utilice el siguiente comando desde una línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="d8207-362">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="d8207-363">Reemplace __sshuser__ por la cuenta de usuario SSH del clúster.</span><span class="sxs-lookup"><span data-stu-id="d8207-363">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="d8207-364">Reemplace __clustername__ por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8207-364">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="d8207-365">Para más información sobre cómo usar `scp` y `ssh` con HDInsight, vea [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d8207-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="d8207-366">Se pueden producir errores en los envíos por varios motivos:</span><span class="sxs-lookup"><span data-stu-id="d8207-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="d8207-367">JDK no está instalado o no está en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="d8207-367">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="d8207-368">Las dependencias de Java necesarias no se incluyen en el envío.</span><span class="sxs-lookup"><span data-stu-id="d8207-368">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="d8207-369">Dependencias no compatibles.</span><span class="sxs-lookup"><span data-stu-id="d8207-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="d8207-370">Nombres de topologías duplicados.</span><span class="sxs-lookup"><span data-stu-id="d8207-370">Duplicate topology names.</span></span>

<span data-ttu-id="d8207-371">Si el registro `hdinsight-scpwebapi.out` contiene un `FileNotFoundException`, puede deberse a las siguientes condiciones:</span><span class="sxs-lookup"><span data-stu-id="d8207-371">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="d8207-372">El JDK no está en la ruta de acceso en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d8207-372">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="d8207-373">Compruebe que el JDK está instalado en el entorno de desarrollo y que `%JAVA_HOME%/bin` está en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="d8207-373">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="d8207-374">Falta una dependencia de Java.</span><span class="sxs-lookup"><span data-stu-id="d8207-374">You are missing a Java dependency.</span></span> <span data-ttu-id="d8207-375">Asegúrese de incluir todos los archivos .jar necesarios como parte del envío.</span><span class="sxs-lookup"><span data-stu-id="d8207-375">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8207-376">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8207-376">Next steps</span></span>

<span data-ttu-id="d8207-377">Para obtener un ejemplo de procesamiento de datos desde Event Hubs, vea [Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d8207-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="d8207-378">Para ver un ejemplo de una topología de C# que divide los datos de una secuencia en varias secuencias, consulte [Ejemplo de Storm en C#](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="d8207-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="d8207-379">Para más información sobre cómo crear topologías de C#, vea [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="d8207-379">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="d8207-380">Para conocer más formas de trabajar con HDInsight y obtener más ejemplos de Storm en HDInsight, vea los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="d8207-380">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="d8207-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="d8207-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="d8207-382">Guía de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="d8207-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="d8207-383">**Apache Storm en HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d8207-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="d8207-384">Implementación y supervisión de topologías con Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8207-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="d8207-385">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8207-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="d8207-386">**Apache Hadoop en HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d8207-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="d8207-387">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8207-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d8207-388">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8207-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d8207-389">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8207-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="d8207-390">**Apache HBase en HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d8207-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="d8207-391">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8207-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
