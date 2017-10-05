---
title: Uso de Apache Storm con Power BI - Azure HDInsight | Microsoft Docs
description: "Creación de un informe de Power BI usando datos de una topología de C# que se ejecuta en un clúster de Apache Storm en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="9b16d-103">Uso de Power BI para visualizar datos de una topología de Apache Storm</span><span class="sxs-lookup"><span data-stu-id="9b16d-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="9b16d-104">Power BI permite mostrar visualmente los datos como informes.</span><span class="sxs-lookup"><span data-stu-id="9b16d-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="9b16d-105">Este documento proporciona un ejemplo de cómo usar Apache Storm en HDInsight para generar datos para Power BI.</span><span class="sxs-lookup"><span data-stu-id="9b16d-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="9b16d-106">Los pasos descritos en este documento se basan en un entorno de desarrollo de Windows con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b16d-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="9b16d-107">El proyecto compilado se puede enviar a un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="9b16d-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9b16d-108">Solo los clústeres basados en Linux creados con posterioridad al 28/10/2016 admiten topologías SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="9b16d-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="9b16d-109">Para usar una topología de C# con un clúster basado en Linux, actualice el paquete de NuGet Microsoft.SCP.Net.SDK usado en el proyecto a la versión 0.10.0.6 o superior.</span><span class="sxs-lookup"><span data-stu-id="9b16d-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="9b16d-110">La versión del paquete también debe coincidir con la versión principal de Storm instalada en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b16d-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="9b16d-111">Por ejemplo, en las versiones de HDInsight 3.3 y 3.4 se usa Storm 0.10.x, mientras que en HDInsight 3.5 se usa Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="9b16d-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="9b16d-112">Las topologías de C# en clústeres basados en Linux deben usar .NET 4.5, y emplear Mono para ejecutarse en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b16d-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="9b16d-113">La mayoría funcionará.</span><span class="sxs-lookup"><span data-stu-id="9b16d-113">Most things work.</span></span> <span data-ttu-id="9b16d-114">No obstante, compruebe el documento de [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para ver las posibles incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="9b16d-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="9b16d-115">Para obtener una versión de Java de este proyecto que funciona con HDInsight basado en Windows o en Linux, vea [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9b16d-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b16d-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b16d-116">Prerequisites</span></span>

* <span data-ttu-id="9b16d-117">Un usuario de Azure Active Directory con acceso a [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="9b16d-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="9b16d-118">Un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b16d-118">An HDInsight cluster.</span></span> <span data-ttu-id="9b16d-119">Para más información, vea [Introducción a los ejemplos de Storm Starter para análisis de macrodatos en HDInsight basado en Linux](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9b16d-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9b16d-120">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="9b16d-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9b16d-121">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9b16d-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9b16d-122">Visual Studio (una de las siguientes versiones)</span><span class="sxs-lookup"><span data-stu-id="9b16d-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="9b16d-123">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="9b16d-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="9b16d-124">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="9b16d-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="9b16d-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="9b16d-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="9b16d-126">Visual Studio 2017 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="9b16d-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="9b16d-127">Herramientas de HDInsight para Visual Studio: vea [Introducción al uso de Herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obtener información acerca de la instalación.</span><span class="sxs-lookup"><span data-stu-id="9b16d-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="9b16d-128">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="9b16d-128">How it works</span></span>

<span data-ttu-id="9b16d-129">Este ejemplo contiene una topología de Storm en C# que genera de forma aleatoria los datos de registro de Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="9b16d-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="9b16d-130">Estos datos se escriben en una Base de datos SQL y desde allí se utilizan para generar informes en Power BI.</span><span class="sxs-lookup"><span data-stu-id="9b16d-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="9b16d-131">Los siguientes archivos implementan la funcionalidad principal de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9b16d-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="9b16d-132">**SqlAzureBolt.cs**: escribe la información generada en la topología de Storm para Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9b16d-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="9b16d-133">**IISLogsTable.sql**: las instrucciones Transact-SQL usadas para generar la base de datos en la que se almacenan los datos.</span><span class="sxs-lookup"><span data-stu-id="9b16d-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="9b16d-134">Cree la tabla en SQL Database antes de iniciar la topología en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b16d-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="9b16d-135">Descarga del ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b16d-135">Download the example</span></span>

<span data-ttu-id="9b16d-136">Descargue el [ejemplo de Power BI de Storm en C# de HDInsight](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="9b16d-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="9b16d-137">Para descargarlo, bifúrquelo o clónelo mediante [git](http://git-scm.com/), o use el vínculo **Descargar** para descargar un archivo .zip del archivo.</span><span class="sxs-lookup"><span data-stu-id="9b16d-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="9b16d-138">Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="9b16d-138">Create a database</span></span>

1. <span data-ttu-id="9b16d-139">Para crear una base de datos, siga los pasos del documento [Tutorial de SQL Database](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9b16d-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="9b16d-140">Para conectarse a la base de datos, siga los pasos del documento [Conexión a una base de datos SQL con Visual Studio](../sql-database/sql-database-connect-query.md).</span><span class="sxs-lookup"><span data-stu-id="9b16d-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="9b16d-141">En el Explorador de objetos, haga clic con el botón derecho en la base de datos y seleccione **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="9b16d-142">Pegue el contenido del archivo **IISLogsTable.sql** incluido en el proyecto descargado en la ventana de consulta, y use Ctrl + Mayús + E para ejecutar la consulta.</span><span class="sxs-lookup"><span data-stu-id="9b16d-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="9b16d-143">Debería recibir un mensaje informándole de que los comandos se completaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="9b16d-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="9b16d-144">Configuración del ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b16d-144">Configure the sample</span></span>

1. <span data-ttu-id="9b16d-145">En el [Portal de Azure](https://portal.azure.com), seleccione la Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9b16d-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="9b16d-146">Desde la sección **Aspectos básicos** de la hoja Base de datos SQL, seleccione **Mostrar las cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="9b16d-147">En la lista que aparece, copie la información **ADO.NET (autenticación de SQL)** .</span><span class="sxs-lookup"><span data-stu-id="9b16d-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="9b16d-148">Abra el ejemplo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b16d-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="9b16d-149">Desde el **Explorador de soluciones**, abra el archivo **App.config** y luego busque la siguiente entrada:</span><span class="sxs-lookup"><span data-stu-id="9b16d-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="9b16d-150">Reemplace el valor **TOBEFILLED ##** con la cadena de conexión de base de datos copiada en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="9b16d-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="9b16d-151">Reemplace **{your\_username}** y **{your\_password}** por el nombre de usuario y la contraseña de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="9b16d-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="9b16d-152">Guarde y cierre los archivos.</span><span class="sxs-lookup"><span data-stu-id="9b16d-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="9b16d-153">Implementación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b16d-153">Deploy the sample</span></span>

1. <span data-ttu-id="9b16d-154">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **StormToSQL** y seleccione **Submit to Storm on HDInsight** (Enviar a Storm en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="9b16d-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="9b16d-155">Seleccione el clúster de HDInsight desde el cuadro desplegable **Clúster de Storm** .</span><span class="sxs-lookup"><span data-stu-id="9b16d-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9b16d-156">El cuadro desplegable **Storm clúster** puede tardar unos segundos en rellenarse con los nombres de servidor.</span><span class="sxs-lookup"><span data-stu-id="9b16d-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="9b16d-157">Si se le solicita, introduzca las credenciales de inicio de sesión de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b16d-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="9b16d-158">Si tiene más de una suscripción, inicie sesión en la que contenga el clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b16d-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="9b16d-159">Cuando se haya enviado la topología, aparecerá el __Visor de topología__.</span><span class="sxs-lookup"><span data-stu-id="9b16d-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="9b16d-160">Para ver esta topología, seleccione la entrada SqlAzureWriterTopology en la lista.</span><span class="sxs-lookup"><span data-stu-id="9b16d-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![Las topologías, con la topología seleccionada](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="9b16d-162">Puede usar esta vista para ver información de la topología o hacer doble clic en una entrada (como SqlAzureBolt) para ver información específica de un componente de la topología.</span><span class="sxs-lookup"><span data-stu-id="9b16d-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="9b16d-163">Después de que la topología se haya ejecutado durante unos minutos, vuelva a la ventana de consulta SQL que usó para crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="9b16d-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="9b16d-164">Sustituya las instrucciones existentes por la consulta siguiente:</span><span class="sxs-lookup"><span data-stu-id="9b16d-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="9b16d-165">Use Ctrl + Mayús + E para ejecutar la consulta, debería recibir resultados similares a los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="9b16d-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="9b16d-166">Estos datos se escribieron a partir de la topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="9b16d-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="9b16d-167">Creación de un informe</span><span class="sxs-lookup"><span data-stu-id="9b16d-167">Create a report</span></span>

1. <span data-ttu-id="9b16d-168">Conectarse al [conector de Base de datos SQL de Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para Power BI.</span><span class="sxs-lookup"><span data-stu-id="9b16d-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="9b16d-169">Dentro de **Bases de datos**, seleccione **Obtener**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="9b16d-170">Seleccione **Azure SQL Database** y luego **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b16d-171">Se le pedirá que descargue Power BI Desktop para continuar.</span><span class="sxs-lookup"><span data-stu-id="9b16d-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="9b16d-172">En ese caso, siga estos pasos para conectarse:</span><span class="sxs-lookup"><span data-stu-id="9b16d-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="9b16d-173">Abra Power BI Desktop y seleccione __Obtener datos__.</span><span class="sxs-lookup"><span data-stu-id="9b16d-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="9b16d-174">2  Seleccione __Azure__ y luego __Azure SQL Database__.</span><span class="sxs-lookup"><span data-stu-id="9b16d-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="9b16d-175">Escriba la información para conectarse a la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b16d-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="9b16d-176">Puede encontrar esta información si visita [Azure Portal](https://portal.azure.com) y selecciona la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9b16d-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9b16d-177">También puede establecer el intervalo de actualización y los filtros personalizados con **Habilitar opciones avanzadas** en el cuadro de diálogo Conectar.</span><span class="sxs-lookup"><span data-stu-id="9b16d-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="9b16d-178">Una vez que haya conectado, verá un nuevo conjunto de datos con el mismo nombre que la base de datos a la que está conectado.</span><span class="sxs-lookup"><span data-stu-id="9b16d-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="9b16d-179">Seleccione el conjunto de datos para comenzar a diseñar un informe.</span><span class="sxs-lookup"><span data-stu-id="9b16d-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="9b16d-180">En **Campos**, expanda la entrada **IISLOGS**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="9b16d-181">Para crear un informe que enumere los recursos de identificador URI, seleccione la casilla **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Creación de un informe](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="9b16d-183">A continuación, arrastre **METHOD** al informe.</span><span class="sxs-lookup"><span data-stu-id="9b16d-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="9b16d-184">El informe se actualiza para mostrar los recursos y el método HTTP correspondiente que se utiliza para la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b16d-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![incorporación de los datos de método](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="9b16d-186">En la columna **Visualizaciones**, seleccione el icono **Campos** y luego seleccione la flecha hacia abajo junto a **METHOD** en la sección **Valores**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="9b16d-187">Para mostrar un recuento de cuántas veces se ha accedido a un identificador URI, seleccione **Recuento**.</span><span class="sxs-lookup"><span data-stu-id="9b16d-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Cambio a un recuento de métodos](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="9b16d-189">A continuación, seleccione **Gráfico de columnas apiladas** para cambiar la forma en la que se muestra la información.</span><span class="sxs-lookup"><span data-stu-id="9b16d-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Cambio a un gráfico apilado](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="9b16d-191">Para guardar el informe, haga clic en **Guardar** y escriba un nombre para el informe.</span><span class="sxs-lookup"><span data-stu-id="9b16d-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="9b16d-192">Detención de la topología</span><span class="sxs-lookup"><span data-stu-id="9b16d-192">Stop the topology</span></span>

<span data-ttu-id="9b16d-193">La topología continúa ejecutándose hasta que la detenga o elimine el clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b16d-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="9b16d-194">Para detener la topología, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b16d-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="9b16d-195">En Visual Studio, vuelva al visor de topologías y seleccione la topología.</span><span class="sxs-lookup"><span data-stu-id="9b16d-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="9b16d-196">Seleccione el botón **Cerrar** para detener la topología.</span><span class="sxs-lookup"><span data-stu-id="9b16d-196">Select the **Kill** button to stop the topology.</span></span>

    ![Botón Cerrar en el resumen de la topología](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="9b16d-198">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="9b16d-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="9b16d-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b16d-199">Next steps</span></span>

<span data-ttu-id="9b16d-200">En este documento ha aprendido a enviar datos de una topología de Storm a Base de datos SQL, y a visualizar los datos después usando Power BI.</span><span class="sxs-lookup"><span data-stu-id="9b16d-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="9b16d-201">Para más información sobre cómo trabajar con otras tecnologías de Azure usando Storm en HDInsight, consulte el siguiente documento:</span><span class="sxs-lookup"><span data-stu-id="9b16d-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="9b16d-202">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b16d-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
