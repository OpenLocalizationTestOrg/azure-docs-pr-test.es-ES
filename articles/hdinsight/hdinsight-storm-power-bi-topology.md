---
title: aaaUse Apache Storm con Power BI - HDInsight de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="98237-103">Usar datos de Power BI toovisualize de una topología de Apache Storm</span><span class="sxs-lookup"><span data-stu-id="98237-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="98237-104">Power BI permite toovisually mostrar datos como informes.</span><span class="sxs-lookup"><span data-stu-id="98237-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="98237-105">Este documento proporciona un ejemplo de cómo toouse Apache Storm en HDInsight toogenerate datos para Power BI.</span><span class="sxs-lookup"><span data-stu-id="98237-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="98237-106">Hello pasos de este documento se basan en un entorno de desarrollo de Windows con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98237-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="98237-107">proyecto compilado Hola puede ser enviado tooa clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="98237-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="98237-108">Solo los clústeres basados en Linux creados con posterioridad al 28/10/2016 admiten topologías SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="98237-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="98237-109">toouse una topología de C# con un clúster basado en Linux, Hola de actualización de paquetes de Microsoft.SCP.Net.SDK NuGet utilizado por el tooversion proyecto 0.10.0.6 o superior.</span><span class="sxs-lookup"><span data-stu-id="98237-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="98237-110">versión de Hola del paquete de hello también debe coincidir con la versión principal de Hola de Storm instalado en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98237-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="98237-111">Por ejemplo, en las versiones de HDInsight 3.3 y 3.4 se usa Storm 0.10.x, mientras que en HDInsight 3.5 se usa Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="98237-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="98237-112">Topologías de C# en clústeres basados en Linux deben usar .NET 4.5 y usar toorun Mono en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="98237-113">La mayoría funcionará.</span><span class="sxs-lookup"><span data-stu-id="98237-113">Most things work.</span></span> <span data-ttu-id="98237-114">Sin embargo debe comprobar hello [Mono compatibilidad](http://www.mono-project.com/docs/about-mono/compatibility/) documento para detectar posibles incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="98237-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="98237-115">Para obtener una versión de Java de este proyecto que funciona con HDInsight basado en Windows o en Linux, vea [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="98237-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98237-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="98237-116">Prerequisites</span></span>

* <span data-ttu-id="98237-117">Un usuario de Azure Active Directory con acceso a [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="98237-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="98237-118">Un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98237-118">An HDInsight cluster.</span></span> <span data-ttu-id="98237-119">Para más información, vea [Introducción a los ejemplos de Storm Starter para análisis de macrodatos en HDInsight basado en Linux](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="98237-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="98237-120">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="98237-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="98237-121">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="98237-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="98237-122">Visual Studio (uno de hello siguiendo las versiones)</span><span class="sxs-lookup"><span data-stu-id="98237-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="98237-123">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="98237-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="98237-124">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="98237-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="98237-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="98237-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="98237-126">Visual Studio 2017 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="98237-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="98237-127">Hola HDInsight Tools para Visual Studio: vea [Introducción al uso de hello HDInsight Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obtener información sobre la información de instalación.</span><span class="sxs-lookup"><span data-stu-id="98237-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="98237-128">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="98237-128">How it works</span></span>

<span data-ttu-id="98237-129">Este ejemplo contiene una topología de Storm en C# que genera de forma aleatoria los datos de registro de Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="98237-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="98237-130">Estos datos se escriben tooa base de datos SQL y, a partir de ahí es toogenerate usa informes de Power BI.</span><span class="sxs-lookup"><span data-stu-id="98237-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="98237-131">Hola después de implementar archivos Hola funcionalidad principal de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98237-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="98237-132">**SqlAzureBolt.cs**: escribe la información que se produce en hello Storm topología tooSQL base de datos.</span><span class="sxs-lookup"><span data-stu-id="98237-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="98237-133">**IISLogsTable.sql**: Hola Transact-SQL instrucciones que se utilizan toogenerate Hola base de datos que Hola datos se almacenan en.</span><span class="sxs-lookup"><span data-stu-id="98237-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="98237-134">Crear tabla de hello en la base de datos SQL antes de iniciar la topología de hello en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98237-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="98237-135">Descargar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="98237-135">Download hello example</span></span>

<span data-ttu-id="98237-136">Descargar hello [ejemplo HDInsight C# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="98237-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="98237-137">toodownload, ya sea bifurcar/clone mediante [git](http://git-scm.com/), o usar hello **descargar** toodownload vínculo .zip archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="98237-138">Crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="98237-138">Create a database</span></span>

1. <span data-ttu-id="98237-139">toocreate una base de datos, siga los pasos de Hola Hola [tutorial de base de datos SQL](../sql-database/sql-database-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="98237-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="98237-140">Conectar toohello base de datos Hola siguiente pasos de hello [conectar tooa base de datos SQL con Visual Studio](../sql-database/sql-database-connect-query.md) documento.</span><span class="sxs-lookup"><span data-stu-id="98237-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="98237-141">En el Explorador de objetos, haga clic en la base de datos de Hola y seleccione **nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="98237-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="98237-142">Pegar contenido Hola de hello **IISLogsTable.sql** archivo incluido en hello descargaste el proyecto en la ventana de consulta de hello y, a continuación, utilice Ctrl + Mayús + E tooexecute Hola consulta.</span><span class="sxs-lookup"><span data-stu-id="98237-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="98237-143">Debería recibir un mensaje que Hola comandos que se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="98237-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="98237-144">Configurar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="98237-144">Configure hello sample</span></span>

1. <span data-ttu-id="98237-145">De hello [portal de Azure](https://portal.azure.com), seleccione la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="98237-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="98237-146">De hello **Essentials** sección de hoja de base de datos SQL hello, seleccione **mostrar cadenas de conexión de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="98237-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="98237-147">De la lista de Hola que aparece, copie hello **ADO.NET (autenticación de SQL)** información.</span><span class="sxs-lookup"><span data-stu-id="98237-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="98237-148">Ejemplo de Hola abierta en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98237-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="98237-149">De **el Explorador de soluciones**, abra hello **App.config** de archivos y, a continuación, busque Hola siguiente entrada:</span><span class="sxs-lookup"><span data-stu-id="98237-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="98237-150">Reemplace hello **TOBEFILLED ##** valor con la cadena de conexión de base de datos de Hola se copió en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="98237-151">Reemplace **{su\_username}** y **{su\_contraseña}** con hello username y password para base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="98237-152">Guarde y cierre los archivos de saludo.</span><span class="sxs-lookup"><span data-stu-id="98237-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="98237-153">Implementar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="98237-153">Deploy hello sample</span></span>

1. <span data-ttu-id="98237-154">De **el Explorador de soluciones**, contextual hello **StormToSQL** de proyecto y seleccione **enviar tooStorm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="98237-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="98237-155">Clúster de HDInsight seleccione Hola de hello **clúster de Storm** cuadro de diálogo de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="98237-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="98237-156">Puede tardar unos segundos hello **clúster de Storm** toopopulate de lista desplegable con nombres de servidor.</span><span class="sxs-lookup"><span data-stu-id="98237-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="98237-157">Si se le solicite, escriba las credenciales de inicio de sesión de hello para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="98237-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="98237-158">Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98237-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="98237-159">Cuando se ha enviado la topología de hello, Hola __Visor de la topología__ aparece.</span><span class="sxs-lookup"><span data-stu-id="98237-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="98237-160">tooview esta topología, entrada de SqlAzureWriterTopology Hola seleccione de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![topologías de Hello, con la topología de hello seleccionado](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="98237-162">Puede usar esta información de toosee de vista en la topología de hello, o haga doble clic en un componente de tooa específico de entrada (por ejemplo, hello SqlAzureBolt) toosee información de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="98237-163">Después de hello topología se ejecutó durante unos minutos, ventana de consulta SQL toohello devuelto usar base de datos de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="98237-164">Reemplace las instrucciones existentes de hello con hello después de consulta:</span><span class="sxs-lookup"><span data-stu-id="98237-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="98237-165">Utilice Ctrl + Mayús + E tooexecute Hola de consultas y se debe recibir resultados toohello similar datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="98237-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="98237-166">Estos datos se ha escrito de topología de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="98237-167">Creación de un informe</span><span class="sxs-lookup"><span data-stu-id="98237-167">Create a report</span></span>

1. <span data-ttu-id="98237-168">Conectar toohello [conector de base de datos de SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para Power BI.</span><span class="sxs-lookup"><span data-stu-id="98237-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="98237-169">Dentro de **Bases de datos**, seleccione **Obtener**.</span><span class="sxs-lookup"><span data-stu-id="98237-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="98237-170">Seleccione **Azure SQL Database** y luego **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="98237-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="98237-171">Se le pedirá toodownload Hola Power BI Desktop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="98237-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="98237-172">Si es así, utilice Hola siguiendo los pasos tooconnect:</span><span class="sxs-lookup"><span data-stu-id="98237-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="98237-173">Abra Power BI Desktop y seleccione __Obtener datos__.</span><span class="sxs-lookup"><span data-stu-id="98237-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="98237-174">2  Seleccione __Azure__ y luego __Azure SQL Database__.</span><span class="sxs-lookup"><span data-stu-id="98237-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="98237-175">Escriba Hola información tooconnect tooyour base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="98237-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="98237-176">Puede encontrar esta información visitando hello [portal de Azure](https://portal.azure.com) y seleccione la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="98237-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="98237-177">También puede establecer intervalo de actualización de Hola y filtros personalizados mediante **habilitar opciones avanzadas** de hello el diálogo de conexión.</span><span class="sxs-lookup"><span data-stu-id="98237-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="98237-178">Una vez conectado, verá un nuevo conjunto de datos con hello que mismo nombre como base de datos de Hola que se ha conectado.</span><span class="sxs-lookup"><span data-stu-id="98237-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="98237-179">Seleccione toobegin de conjunto de datos de hello diseñar un informe.</span><span class="sxs-lookup"><span data-stu-id="98237-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="98237-180">De **campos**, expanda hello **IISLOGS** entrada.</span><span class="sxs-lookup"><span data-stu-id="98237-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="98237-181">toocreate proviene de un informe que enumera Hola URI, active la casilla de verificación de Hola para **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="98237-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Creación de un informe](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="98237-183">A continuación, arrastre **método** toohello informes.</span><span class="sxs-lookup"><span data-stu-id="98237-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="98237-184">Hola de Hello informe actualizaciones toolist proviene y método HTTP correspondiente de hello usa para hello solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="98237-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![agregar datos sobre métodos Hola](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="98237-186">De hello **visualizaciones** columna, seleccione hello **campos** icono y, a continuación, seleccione Hola flecha abajo junto demasiado**método** en hello **valores**sección.</span><span class="sxs-lookup"><span data-stu-id="98237-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="98237-187">Seleccione toodisplay se accedió a un recuento de cuántas veces un URI, **recuento**.</span><span class="sxs-lookup"><span data-stu-id="98237-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Cambiar el número de tooa de métodos](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="98237-189">A continuación, seleccione hello **gráfico de columnas apiladas** toochange cómo se muestra información de Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Variación tooa series apiladas](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="98237-191">informe de toosave hello, seleccione **guardar** y escriba un nombre para el informe de Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="98237-192">Detener la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="98237-192">Stop hello topology</span></span>

<span data-ttu-id="98237-193">topología de Hello continúa toorun hasta que lo detenga o eliminar Hola Storm en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98237-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="98237-194">toostop Hola topología, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98237-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="98237-195">En Visual Studio, devolver Visor de la topología de toohello y seleccione la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="98237-196">Seleccione hello **Kill** topología de botón toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="98237-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill botón en la topología de hello resumen](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="98237-198">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="98237-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="98237-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98237-199">Next steps</span></span>

<span data-ttu-id="98237-200">En este documento, aprendió cómo toosend datos desde un tooSQL de topología de Storm base de datos, a continuación, visualizar los datos de hello con Power BI.</span><span class="sxs-lookup"><span data-stu-id="98237-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="98237-201">Para obtener información acerca de cómo toowork con otras tecnologías de Azure con Storm en HDInsight, vea Hola siguiente documento:</span><span class="sxs-lookup"><span data-stu-id="98237-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="98237-202">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="98237-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
