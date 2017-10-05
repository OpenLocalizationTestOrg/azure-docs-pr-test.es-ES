---
title: "Ejecución de un trabajo de Hadoop con Azure Cosmos DB y HDInsight | Microsoft Docs"
description: "Obtenga información acerca de cómo ejecutar un trabajo de Hive, Pig y MapReduce simple con Azure Cosmos DB y Azure HDInsight."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="9f410-103"><a name="Azure Cosmos DB-HDInsight"></a>Ejecución de un trabajo de Apache Hive, Pig o Hadoop con Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f410-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="9f410-104">Este tutorial muestra cómo ejecutar trabajos de [Apache Hive][apache-hive], [Apache Pig][apache-pig] y [Apache Hadoop][apache-hadoop] MapReduce en HDInsight de Azure con el conector Hadoop de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f410-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="9f410-105">El conector de Hadoop de Cosmos DB permite a Cosmos DB actuar como punto de origen y recepción para trabajos de Hive, Pig y MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9f410-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="9f410-106">En este tutorial, se usará Cosmos DB como el origen de datos y el destino para trabajos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9f410-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="9f410-107">Después de completar este tutorial, podrá responder a las preguntas siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f410-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="9f410-108">¿Cómo se cargan datos desde Cosmos DB mediante un trabajo de MapReduce, Pig o Hive?</span><span class="sxs-lookup"><span data-stu-id="9f410-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="9f410-109">¿Cómo se almacenan datos en Cosmos DB mediante un trabajo de MapReduce, Pig o Hive?</span><span class="sxs-lookup"><span data-stu-id="9f410-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="9f410-110">Se recomienda comenzar con el vídeo siguiente, donde se realiza una ejecución a través de un trabajo de Hive usando Cosmos DB y HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="9f410-111">A continuación, vuelva a este artículo, donde recibirá información detallada sobre cómo ejecutar trabajos de análisis en los datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f410-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="9f410-112">Este tutorial presupone que se tiene experiencia previa con Apache Hadoop, Hive o Pig</span><span class="sxs-lookup"><span data-stu-id="9f410-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="9f410-113">Si no está familiarizado con Apache Hadoop, Hive y Pig, se recomienda consultar la [documentación de Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="9f410-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="9f410-114">Asimismo, el tutorial también presupone que se tiene experiencia previa con Cosmos DB además de una cuenta en este servicio.</span><span class="sxs-lookup"><span data-stu-id="9f410-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="9f410-115">Si no está familiarizado con Cosmos DB o no tiene una cuenta en este servicio, consulte nuestra página [Introducción][getting-started].</span><span class="sxs-lookup"><span data-stu-id="9f410-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="9f410-116">¿No tiene tiempo para completar el tutorial y solo desea obtener todos los scripts de PowerShell de ejemplo de Hive, Pig y MapReduce?</span><span class="sxs-lookup"><span data-stu-id="9f410-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="9f410-117">No hay problema, obténgalos [aquí][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="9f410-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="9f410-118">La descarga también contiene los archivos hpl, pig y java para estos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="9f410-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="9f410-119"><a name="NewestVersion"></a>Versión más reciente</span><span class="sxs-lookup"><span data-stu-id="9f410-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="9f410-120">Versión del conector de Hadoop</span><span class="sxs-lookup"><span data-stu-id="9f410-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="9f410-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9f410-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="9f410-122">URI de script</span><span class="sxs-lookup"><span data-stu-id="9f410-122">Script Uri</span></span></th>
        <td><span data-ttu-id="9f410-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="9f410-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="9f410-124">Fecha de modificación</span><span class="sxs-lookup"><span data-stu-id="9f410-124">Date Modified</span></span></th>
        <td><span data-ttu-id="9f410-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="9f410-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="9f410-126">Versiones compatibles de HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f410-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="9f410-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="9f410-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="9f410-128">Registro de cambios</span><span class="sxs-lookup"><span data-stu-id="9f410-128">Change Log</span></span></th>
        <td><span data-ttu-id="9f410-129">Actualización del SDK de Java para Azure Cosmos DB a 1.6.0</span><span class="sxs-lookup"><span data-stu-id="9f410-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="9f410-130">Se ha agregado compatibilidad con las colecciones divididas como origen y receptor.</span><span class="sxs-lookup"><span data-stu-id="9f410-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="9f410-131"><a name="Prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f410-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="9f410-132">Antes de seguir las instrucciones de este tutorial, asegúrese de contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9f410-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="9f410-133">Una cuenta de Cosmos DB, una base de datos y una colección con documentos dentro.</span><span class="sxs-lookup"><span data-stu-id="9f410-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="9f410-134">Para más información, consulte [Introducción a Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="9f410-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="9f410-135">Importe datos de ejemplo a su cuenta de Cosmos DB con la [herramienta de importación de Cosmos DB][import-data].</span><span class="sxs-lookup"><span data-stu-id="9f410-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="9f410-136">Capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="9f410-136">Throughput.</span></span> <span data-ttu-id="9f410-137">Las lecturas y escrituras de HDInsight se tienen en cuenta a la hora de calcular las unidades de solicitud asignadas a las colecciones.</span><span class="sxs-lookup"><span data-stu-id="9f410-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="9f410-138">Capacidad para un procedimiento almacenado adicional dentro de cada colección de salida.</span><span class="sxs-lookup"><span data-stu-id="9f410-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="9f410-139">Los procedimientos almacenados se utilizan para transferir los documentos resultantes.</span><span class="sxs-lookup"><span data-stu-id="9f410-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="9f410-140">Capacidad para los documentos resultantes desde los trabajos de MapReduce, Pig o Hive.</span><span class="sxs-lookup"><span data-stu-id="9f410-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="9f410-141">[*Opcional*] Capacidad para una colección adicional.</span><span class="sxs-lookup"><span data-stu-id="9f410-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="9f410-142">Para evitar que se cree una nueva colección mientras se está realizando cualquier trabajo, puede imprimir los resultados en stdout, guardar la salida en el contenedor WASB o especificar una colección existente.</span><span class="sxs-lookup"><span data-stu-id="9f410-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="9f410-143">En el caso de que desee especificar una colección existente, se crearán nuevos documentos dentro de la colección y los documentos existentes solo se verán afectados si se produce un conflicto entre los *identificadores*.</span><span class="sxs-lookup"><span data-stu-id="9f410-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="9f410-144">**El conector sobrescribirá automáticamente los documentos existentes con conflictos de identificador**.</span><span class="sxs-lookup"><span data-stu-id="9f410-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="9f410-145">Puede desactivar esta característica estableciendo la opción upsert en false.</span><span class="sxs-lookup"><span data-stu-id="9f410-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="9f410-146">Si upsert es false y se produce un conflicto, se producirá un error en el trabajo de Hadoop y se informará de un error a causa de conflicto de identificadores.</span><span class="sxs-lookup"><span data-stu-id="9f410-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="9f410-147"><a name="ProvisionHDInsight"></a>Paso 1: Creación de un nuevo clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f410-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="9f410-148">En este tutorial, se usa la acción de script de Azure Portal para personalizar el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="9f410-149">Así que usaremos Azure Portal para crear el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="9f410-150">Para obtener instrucciones sobre cómo usar los cmdlets de PowerShell o el SDK de .NET de HDInsight, consulte el artículo [Personalización de los clústeres de HDInsight mediante la acción de script][hdinsight-custom-provision].</span><span class="sxs-lookup"><span data-stu-id="9f410-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="9f410-151">Inicie sesión en [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f410-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="9f410-152">Haga clic en **+ Nuevo** en la parte superior del panel izquierdo y busque **HDInsight** en la barra de búsqueda superior de la hoja Nuevo.</span><span class="sxs-lookup"><span data-stu-id="9f410-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="9f410-153">Aparece **HDInsight** publicado por **Microsoft** en la parte superior de los resultados.</span><span class="sxs-lookup"><span data-stu-id="9f410-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="9f410-154">Haga clic en él y luego en **rear**.</span><span class="sxs-lookup"><span data-stu-id="9f410-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="9f410-155">En la hoja para crear un nuevo clúster de HDInsight, escriba su **nombre de clúster** y seleccione la **suscripción** con la que quiere aprovisionar este recurso.</span><span class="sxs-lookup"><span data-stu-id="9f410-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="9f410-156">Nombre del clúster</span><span class="sxs-lookup"><span data-stu-id="9f410-156">Cluster name</span></span></td><td><span data-ttu-id="9f410-157">Dé un nombre al clúster.</span><span class="sxs-lookup"><span data-stu-id="9f410-157">Name the cluster.</span></span><br/>
<span data-ttu-id="9f410-158">El nombre DNS debe empezar y terminar con un carácter alfanumérico y puede contener guiones.</span><span class="sxs-lookup"><span data-stu-id="9f410-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="9f410-159">El campo debe ser una cadena con una longitud que tenga entre 3 y 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f410-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="9f410-160">Subscription Name</span><span class="sxs-lookup"><span data-stu-id="9f410-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="9f410-161">Si tiene más de una suscripción de Azure, seleccione aquella que va a hospedar el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="9f410-162">
5. Haga clic en **Seleccionar tipo de clúster** y establezca las siguientes propiedades en los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="9f410-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="9f410-163">Tipo de clúster</span><span class="sxs-lookup"><span data-stu-id="9f410-163">Cluster type</span></span></td><td><span data-ttu-id="9f410-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="9f410-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="9f410-165">Nivel de clúster</span><span class="sxs-lookup"><span data-stu-id="9f410-165">Cluster tier</span></span></td><td><span data-ttu-id="9f410-166"><strong>Estándar</strong></span><span class="sxs-lookup"><span data-stu-id="9f410-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="9f410-167">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="9f410-167">Operating System</span></span></td><td><span data-ttu-id="9f410-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="9f410-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="9f410-169">Versión</span><span class="sxs-lookup"><span data-stu-id="9f410-169">Version</span></span></td><td><span data-ttu-id="9f410-170">Versión más reciente</span><span class="sxs-lookup"><span data-stu-id="9f410-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="9f410-171">Ahora, haga clic en **SELECCIONAR**.</span><span class="sxs-lookup"><span data-stu-id="9f410-171">Now, click **SELECT**.</span></span>

    ![Proporcionar detalles del clúster inicial de HDInsight de Hadoop][image-customprovision-page1]
6. <span data-ttu-id="9f410-173">Haga clic en **Credenciales** para establecer las credenciales de inicio de sesión y de acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="9f410-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="9f410-174">Elija su **nombre de usuario de inicio de sesión del clúster** y **contraseña de inicio de sesión del clúster**.</span><span class="sxs-lookup"><span data-stu-id="9f410-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="9f410-175">Si quiere tener acceso remoto al clúster, seleccione *Sí* en la parte inferior de la hoja y proporcione un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="9f410-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="9f410-176">Haga clic en **rigen de datos** para establecer la ubicación principal para el acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="9f410-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="9f410-177">Elija el **método de selección** y especifique una cuenta de almacenamiento ya existente o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="9f410-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="9f410-178">En la misma hoja, especifique un **contenedor predeterminado** y una **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="9f410-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="9f410-179">A continuación, haga clic en **SELECCIONAR**.</span><span class="sxs-lookup"><span data-stu-id="9f410-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f410-180">Seleccione una ubicación cercana a la región de la cuenta de Cosmos DB para mejorar el rendimiento</span><span class="sxs-lookup"><span data-stu-id="9f410-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="9f410-181">Haga clic en **recios** para seleccionar el número y el tipo de los nodos.</span><span class="sxs-lookup"><span data-stu-id="9f410-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="9f410-182">Puede mantener la configuración predeterminada y escalar el número de nodos de trabajo más adelante.</span><span class="sxs-lookup"><span data-stu-id="9f410-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="9f410-183">Haga clic en **Configuración opcional** y luego en **Acciones de script** en la hoja Configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="9f410-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="9f410-184">En Acciones de Script, escriba la siguiente información para personalizar el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="9f410-185">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9f410-185">Property</span></span></th><th><span data-ttu-id="9f410-186">Valor</span><span class="sxs-lookup"><span data-stu-id="9f410-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="9f410-187">Nombre</span><span class="sxs-lookup"><span data-stu-id="9f410-187">Name</span></span></td>
             <td><span data-ttu-id="9f410-188">Especifique un nombre para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="9f410-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="9f410-189">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="9f410-189">Script URI</span></span></td>
             <td><span data-ttu-id="9f410-190">Especifique el identificador URI al script que se ha invocado para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="9f410-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="9f410-191">Especifique esta información:</span><span class="sxs-lookup"><span data-stu-id="9f410-191">Please enter:</span></span> </br> <span data-ttu-id="9f410-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="9f410-193">Principal</span><span class="sxs-lookup"><span data-stu-id="9f410-193">Head</span></span></td>
             <td><span data-ttu-id="9f410-194">Haga clic en la casilla para ejecutar el script de PowerShell en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="9f410-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="9f410-195">
             <strong>Active esta casilla</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="9f410-196">Trabajo</span><span class="sxs-lookup"><span data-stu-id="9f410-196">Worker</span></span></td>
             <td><span data-ttu-id="9f410-197">Haga clic en la casilla para ejecutar el script de PowerShell en el nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9f410-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="9f410-198">
             <strong>Active esta casilla</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="9f410-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="9f410-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="9f410-200">Haga clic en la casilla para ejecutar el script de PowerShell en el Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="9f410-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="9f410-201">
             <strong>No es necesario</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="9f410-202">parameters</span><span class="sxs-lookup"><span data-stu-id="9f410-202">Parameters</span></span></td>
             <td><span data-ttu-id="9f410-203">Especifique los parámetros, si lo requiere el script.</span><span class="sxs-lookup"><span data-stu-id="9f410-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="9f410-204">
             <strong>No se necesita ningún parámetro</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="9f410-205">
11. Cree un **grupo de recursos** o use uno existente en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f410-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="9f410-206">12.</span><span class="sxs-lookup"><span data-stu-id="9f410-206">12.</span></span> <span data-ttu-id="9f410-207">Ahora, marque **Anclar al panel** para realizar un seguimiento de su implementación y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9f410-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="9f410-208"><a name="InstallCmdlets"></a>Paso 2: Instalación y configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f410-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="9f410-209">Instale Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f410-209">Install Azure PowerShell.</span></span> <span data-ttu-id="9f410-210">Puede encontrar instrucciones [aquí][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="9f410-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f410-211">En el caso de las consultas de Hive, use el Editor de Hive en línea de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="9f410-212">Para ello, inicie sesión en [Azure Portal][azure-portal] y haga clic en **HDInsight** en el panel izquierdo para ver una lista de los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="9f410-213">Haga clic en el clúster en el que desea ejecutar consultas de Hive y, a continuación, haga clic en **Consola de consultas**.</span><span class="sxs-lookup"><span data-stu-id="9f410-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="9f410-214">Abra el entorno de script integrado de Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9f410-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="9f410-215">Si el equipo dispone de Windows 8 o Windows Server 2012, o una versión posterior, puede utilizar la búsqueda integrada.</span><span class="sxs-lookup"><span data-stu-id="9f410-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="9f410-216">En la pantalla de inicio, escriba **powershell ise** y haga clic en **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="9f410-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="9f410-217">Si el equipo dispone de una versión anterior a Windows 8 o Windows Server 2012, use el menú Inicio.</span><span class="sxs-lookup"><span data-stu-id="9f410-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="9f410-218">En el menú Inicio, escriba **Símbolo del sistema** en el cuadro de búsqueda. A continuación, en la lista de resultados, haga clic en **Símbolo del sistema**.</span><span class="sxs-lookup"><span data-stu-id="9f410-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="9f410-219">En el Símbolo del sistema, escriba **powershell_ise** y haga clic en **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="9f410-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="9f410-220">Agregue su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f410-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="9f410-221">En el panel de consola, escriba **Add-AzureAccount** y haga clic en **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="9f410-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="9f410-222">Escriba la dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="9f410-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="9f410-223">Escriba la contraseña para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f410-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="9f410-224">Haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9f410-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="9f410-225">El diagrama siguiente identifica las partes importantes de su entorno de scripts de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f410-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagrama de Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="9f410-227"><a name="RunHive"></a>Paso 3: Ejecución de un trabajo de Hive con Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f410-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f410-228">Todas las variables indicadas con < > deben rellenarse con los valores de configuración adecuados.</span><span class="sxs-lookup"><span data-stu-id="9f410-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="9f410-229">Configure las siguientes variables en el panel de scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f410-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="9f410-230">Comencemos a construir la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="9f410-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="9f410-231">Se escribirá una consulta de Hive que tome las marcas de tiempo (_ts) generadas por el sistema de todos los documentos y los identificadores únicos (_rid) de una colección de Azure Cosmos DB, cuente todos los documentos por minuto y luego almacene de nuevo los resultados en una nueva colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f410-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="9f410-232">En primer lugar se crea una tabla de Hive a partir de la colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f410-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="9f410-233">Agregue el siguiente fragmento de código en el panel de scripts de PowerShell <strong>después</strong> del fragmento de código número 1.</span><span class="sxs-lookup"><span data-stu-id="9f410-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="9f410-234">Asegúrese de incluir el parámetro DocumentDB.query opcional para recortar nuestros documentos solo hasta _ts y _rid.</span><span class="sxs-lookup"><span data-stu-id="9f410-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="9f410-235">**La denominación de DocumentDB.inputCollections no era un error.**</span><span class="sxs-lookup"><span data-stu-id="9f410-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="9f410-236">Sí, se pueden agregar varias colecciones como una entrada:</span><span class="sxs-lookup"><span data-stu-id="9f410-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="9f410-237">A continuación, vamos a crear una tabla de Hive para la colección de salida.</span><span class="sxs-lookup"><span data-stu-id="9f410-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="9f410-238">Las propiedades del documento de salida serán el mes, el día, la hora, el minuto y el número total de apariciones.</span><span class="sxs-lookup"><span data-stu-id="9f410-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f410-239">**Una vez más, la denominación de DocumentDB.outputCollections no era un error.**</span><span class="sxs-lookup"><span data-stu-id="9f410-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="9f410-240">Sí, se pueden agregar varias colecciones como una salida:</span><span class="sxs-lookup"><span data-stu-id="9f410-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="9f410-241">"*DocumentDB.outputCollections*"="*\<Nombre de la colección de salida de DocumentDB 1\>*,*\<Nombre de la colección de salida de DocumentDB 2\>*"</span><span class="sxs-lookup"><span data-stu-id="9f410-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="9f410-242">Se separan los nombres de la colección sin espacios en blanco, con una sola coma.</span><span class="sxs-lookup"><span data-stu-id="9f410-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="9f410-243">Documentos se distribuirán en cadena en varias colecciones.</span><span class="sxs-lookup"><span data-stu-id="9f410-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="9f410-244">Un lote de documentos se almacenará en una colección. A continuación, un segundo lote de documentos se almacenará en la colección siguiente y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9f410-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="9f410-245">Por último, vamos realizar un recuento de los documentos por mes, día, hora y minuto, y vamos a insertar los resultados en la tabla de Hive de salida.</span><span class="sxs-lookup"><span data-stu-id="9f410-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="9f410-246">Agregue el siguiente fragmento de script para crear una definición de trabajo de Hive a partir de la consulta anterior.</span><span class="sxs-lookup"><span data-stu-id="9f410-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="9f410-247">También usará el conmutador -File para especificar un archivo de script de HiveQL en HDFS.</span><span class="sxs-lookup"><span data-stu-id="9f410-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="9f410-248">Agregue el siguiente fragmento para guardar la hora de inicio y enviar el trabajo de Hive.</span><span class="sxs-lookup"><span data-stu-id="9f410-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="9f410-249">Agregue lo siguiente para esperar a que el trabajo de Hive termine.</span><span class="sxs-lookup"><span data-stu-id="9f410-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="9f410-250">Agregue lo siguiente para imprimir la salida estándar y los tiempos de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="9f410-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="9f410-251">**Ejecute** el nuevo script.</span><span class="sxs-lookup"><span data-stu-id="9f410-251">**Run** your new script!</span></span> <span data-ttu-id="9f410-252">**Haga clic** en el botón verde para llevar a cabo la ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f410-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="9f410-253">Compruebe los resultados.</span><span class="sxs-lookup"><span data-stu-id="9f410-253">Check the results.</span></span> <span data-ttu-id="9f410-254">Inicie sesión en [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f410-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="9f410-255">Haga clic en <strong>Examinar</strong> en el panel de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="9f410-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="9f410-256">Haga clic en <strong>Todo</strong>, en la parte superior derecha del panel de exploración.</span><span class="sxs-lookup"><span data-stu-id="9f410-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="9f410-257">Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="9f410-258">Luego busque la <strong>cuenta de Azure Cosmos DB</strong>, la <strong>base de datos de Azure Cosmos DB</strong> y la <strong>colección de Azure Cosmos DB</strong> asociadas a la colección de salida especificada en la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="9f410-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="9f410-259">Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="9f410-260">Verá los resultados de la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="9f410-260">You will see the results of your Hive query.</span></span>

   ![Resultados de la consulta de Hive][image-hive-query-results]

## <span data-ttu-id="9f410-262"><a name="RunPig"></a>Paso 4: Ejecución de un trabajo de Pig con Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f410-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f410-263">Todas las variables indicadas con < > deben rellenarse con los valores de configuración adecuados.</span><span class="sxs-lookup"><span data-stu-id="9f410-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="9f410-264">Configure las siguientes variables en el panel de scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f410-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="9f410-265">Comencemos a construir la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="9f410-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="9f410-266">Se escribirá una consulta de Pig que tome las marcas de tiempo (_ts) generadas por el sistema de todos los documentos y los identificadores únicos (_rid) de una colección de Azure Cosmos DB, cuente todos los documentos por minuto y luego almacene de nuevo los resultados en una nueva colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f410-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="9f410-267">En primer lugar, cargue documentos de Cosmos DB en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="9f410-268">Agregue el siguiente fragmento de código en el panel de scripts de PowerShell <strong>después</strong> del fragmento de código número 1.</span><span class="sxs-lookup"><span data-stu-id="9f410-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="9f410-269">Asegúrese de agregar una consulta de DocumentDB para el parámetro de consulta de DocumentDB opcional para recortar los documentos a solo _ts y _rid.</span><span class="sxs-lookup"><span data-stu-id="9f410-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="9f410-270">Sí, se pueden agregar varias colecciones como una entrada:</span><span class="sxs-lookup"><span data-stu-id="9f410-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="9f410-271">"*\<Nombre de la colección de salida de DocumentDB 1\>*,*\<Nombre de la colección de salida de DocumentDB 2\>*"</span><span class="sxs-lookup"><span data-stu-id="9f410-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="9f410-272">Se separan los nombres de la colección sin espacios en blanco, con una sola coma.</span><span class="sxs-lookup"><span data-stu-id="9f410-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="9f410-273">Documentos se distribuirán en cadena en varias colecciones.</span><span class="sxs-lookup"><span data-stu-id="9f410-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="9f410-274">Un lote de documentos se almacenará en una colección. A continuación, un segundo lote de documentos se almacenará en la colección siguiente y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9f410-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="9f410-275">A continuación, vamos realizar un recuento de los documentos por mes, día, hora, minuto y el número total de apariciones.</span><span class="sxs-lookup"><span data-stu-id="9f410-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="9f410-276">Por último, vamos a almacenar los resultados en nuestra nueva colección de salida.</span><span class="sxs-lookup"><span data-stu-id="9f410-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f410-277">Sí, se pueden agregar varias colecciones como una salida:</span><span class="sxs-lookup"><span data-stu-id="9f410-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="9f410-278">"\<Nombre de la colección de salida de DocumentDB 1\>,\<Nombre de la colección de salida de DocumentDB 2\>"</span><span class="sxs-lookup"><span data-stu-id="9f410-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="9f410-279">Se separan los nombres de la colección sin espacios en blanco, con una sola coma.</span><span class="sxs-lookup"><span data-stu-id="9f410-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="9f410-280">Documentos se distribuirán en cadena por las distintas colecciones.</span><span class="sxs-lookup"><span data-stu-id="9f410-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="9f410-281">Un lote de documentos se almacenará en una colección. A continuación, un segundo lote de documentos se almacenará en la colección siguiente y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9f410-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="9f410-282">Agregue el siguiente fragmento de script para crear una definición de trabajo de Pig a partir de la consulta anterior.</span><span class="sxs-lookup"><span data-stu-id="9f410-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="9f410-283">También usará el modificador -File para especificar un archivo de script de Pig en HDFS.</span><span class="sxs-lookup"><span data-stu-id="9f410-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="9f410-284">Agregue el siguiente fragmento para guardar la hora de inicio y enviar el trabajo de Pig.</span><span class="sxs-lookup"><span data-stu-id="9f410-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="9f410-285">Agregue lo siguiente para esperar a que el trabajo de Pig termine.</span><span class="sxs-lookup"><span data-stu-id="9f410-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="9f410-286">Agregue lo siguiente para imprimir la salida estándar y los tiempos de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="9f410-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="9f410-287">**Ejecute** el nuevo script.</span><span class="sxs-lookup"><span data-stu-id="9f410-287">**Run** your new script!</span></span> <span data-ttu-id="9f410-288">**Haga clic** en el botón verde para llevar a cabo la ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f410-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="9f410-289">Compruebe los resultados.</span><span class="sxs-lookup"><span data-stu-id="9f410-289">Check the results.</span></span> <span data-ttu-id="9f410-290">Inicie sesión en [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f410-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="9f410-291">Haga clic en <strong>Examinar</strong> en el panel de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="9f410-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="9f410-292">Haga clic en <strong>Todo</strong>, en la parte superior derecha del panel de exploración.</span><span class="sxs-lookup"><span data-stu-id="9f410-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="9f410-293">Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="9f410-294">Luego busque la <strong>cuenta de Azure Cosmos DB</strong>, la <strong>base de datos de Azure Cosmos DB</strong> y la <strong>colección de Azure Cosmos DB</strong> asociadas a la colección de salida especificada en la consulta de Pig.</span><span class="sxs-lookup"><span data-stu-id="9f410-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="9f410-295">Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="9f410-296">Verá los resultados de la consulta de Pig.</span><span class="sxs-lookup"><span data-stu-id="9f410-296">You will see the results of your Pig query.</span></span>

    ![Resultados de la consulta de Pig][image-pig-query-results]

## <span data-ttu-id="9f410-298"><a name="RunMapReduce"></a>Paso 5: Ejecución de un trabajo de MapReduce con Azure Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f410-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="9f410-299">Configure las siguientes variables en el panel de scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f410-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="9f410-300">Se va a ejecutar un trabajo de MapReduce que cuenta el número de repeticiones de cada propiedad de documento de la colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f410-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="9f410-301">Agregue este fragmento de script **después** del fragmento de código anterior.</span><span class="sxs-lookup"><span data-stu-id="9f410-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="9f410-302">TallyProperties-v01.jar incluye la instalación personalizada del conector de Hadoop de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f410-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="9f410-303">Agregue el siguiente comando para enviar el trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9f410-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="9f410-304">Además de la definición de trabajo de MapReduce, también debe proporcionar el nombre del clúster de HDInsight en el que desea ejecutar el trabajo de MapReduce y las credenciales.</span><span class="sxs-lookup"><span data-stu-id="9f410-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="9f410-305">Start-AzureHDInsightJob es una llamada no sincronizada.</span><span class="sxs-lookup"><span data-stu-id="9f410-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="9f410-306">Para comprobar la finalización del trabajo, use el cmdlet *Wait-AzureHDInsightJob* .</span><span class="sxs-lookup"><span data-stu-id="9f410-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="9f410-307">Agregue el siguiente comando para comprobar posibles errores al ejecutar el trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9f410-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="9f410-308">**Ejecute** el nuevo script.</span><span class="sxs-lookup"><span data-stu-id="9f410-308">**Run** your new script!</span></span> <span data-ttu-id="9f410-309">**Haga clic** en el botón verde para llevar a cabo la ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f410-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="9f410-310">Compruebe los resultados.</span><span class="sxs-lookup"><span data-stu-id="9f410-310">Check the results.</span></span> <span data-ttu-id="9f410-311">Inicie sesión en [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f410-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="9f410-312">Haga clic en <strong>Examinar</strong> en el panel de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="9f410-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="9f410-313">Haga clic en <strong>Todo</strong>, en la parte superior derecha del panel de exploración.</span><span class="sxs-lookup"><span data-stu-id="9f410-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="9f410-314">Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="9f410-315">Luego busque la <strong>cuenta de Azure Cosmos DB</strong>, la <strong>base de datos de Azure Cosmos DB</strong> y la <strong>colección de Azure Cosmos DB</strong> asociadas a la colección de salida especificada en el trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9f410-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="9f410-316">Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</span><span class="sxs-lookup"><span data-stu-id="9f410-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="9f410-317">Verá los resultados de su trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9f410-317">You will see the results of your MapReduce job.</span></span>

      ![Resultados de la consulta de MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="9f410-319"><a name="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f410-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="9f410-320">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="9f410-320">Congratulations!</span></span> <span data-ttu-id="9f410-321">Acaba de ejecutar sus primeros trabajos de Hive, Pig y MapReduce con Azure Cosmos DB y HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f410-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="9f410-322">El conector de Hadoop tiene el código abierto.</span><span class="sxs-lookup"><span data-stu-id="9f410-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="9f410-323">Si le interesa, puede contribuir en [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="9f410-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="9f410-324">Para obtener más información, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f410-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="9f410-325">[Desarrollo de una aplicación Java con DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="9f410-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="9f410-326">[Desarrollo de programas MapReduce de Java para Hadoop en HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9f410-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="9f410-327">[Introducción al uso de Hadoop con Hive en HDInsight para analizar el uso de datos móviles][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="9f410-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="9f410-328">[Uso de MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9f410-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="9f410-329">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9f410-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9f410-330">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9f410-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9f410-331">[Personalización de los clústeres de HDInsight mediante la acción de script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="9f410-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
