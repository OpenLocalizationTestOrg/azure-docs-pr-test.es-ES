---
title: aaaRun un Hadoop de trabajo utilizando la base de datos de Azure Cosmos y HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo toorun un simple Hive, Pig y MapReduce de trabajo con la base de datos de Azure Cosmos y HDInsight de Azure."
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
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="6e986-103"><a name="Azure Cosmos DB-HDInsight"></a>Ejecución de un trabajo de Apache Hive, Pig o Hadoop con Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e986-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="6e986-104">Este tutorial muestra cómo toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], y [Apache Hadoop] [ apache-hadoop] Trabajos MapReduce en HDInsight de Azure con el conector de Hadoop de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6e986-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="6e986-105">Conector de Hadoop de COSMOS de DB permite tooact de base de datos de Cosmos como un origen y un receptor para trabajos de Hive, Pig y MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6e986-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="6e986-106">Este tutorial usará DB Cosmos como origen de datos de Hola y de destino para trabajos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6e986-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="6e986-107">Después de completar este tutorial, estará hello tooanswer pueda siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="6e986-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="6e986-108">¿Cómo se cargan datos desde Cosmos DB mediante un trabajo de MapReduce, Pig o Hive?</span><span class="sxs-lookup"><span data-stu-id="6e986-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="6e986-109">¿Cómo se almacenan datos en Cosmos DB mediante un trabajo de MapReduce, Pig o Hive?</span><span class="sxs-lookup"><span data-stu-id="6e986-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="6e986-110">Se recomienda introducción, inspeccionando Hola después de vídeo, donde se ejecuta a través de un trabajo de Hive mediante DB Cosmos y HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="6e986-111">A continuación, devolver artículo toothis, donde recibirá Hola información detallada sobre cómo ejecutar trabajos de análisis en los datos de la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6e986-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="6e986-112">Este tutorial presupone que se tiene experiencia previa con Apache Hadoop, Hive o Pig</span><span class="sxs-lookup"><span data-stu-id="6e986-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="6e986-113">Si es nuevo tooApache Hadoop, Hive y Pig, recomendamos visitar hello [documentación de Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="6e986-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="6e986-114">Asimismo, el tutorial también presupone que se tiene experiencia previa con Cosmos DB además de una cuenta en este servicio.</span><span class="sxs-lookup"><span data-stu-id="6e986-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="6e986-115">Si usted es tooCosmos nueva base de datos o no tiene una cuenta de base de datos de Cosmos, consulte nuestro [Introducción] [ getting-started] página.</span><span class="sxs-lookup"><span data-stu-id="6e986-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="6e986-116">¿No tiene tiempo toocomplete Hola tutorial y sólo desea scripts de PowerShell de ejemplo completo de tooget Hola de Hive, Pig y MapReduce?</span><span class="sxs-lookup"><span data-stu-id="6e986-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="6e986-117">No hay problema, obténgalos [aquí][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="6e986-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="6e986-118">descarga de Hello también contiene archivos de hql, pig y java de Hola para estos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="6e986-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="6e986-119"><a name="NewestVersion"></a>Versión más reciente</span><span class="sxs-lookup"><span data-stu-id="6e986-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="6e986-120">Versión del conector de Hadoop</span><span class="sxs-lookup"><span data-stu-id="6e986-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="6e986-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="6e986-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="6e986-122">URI de script</span><span class="sxs-lookup"><span data-stu-id="6e986-122">Script Uri</span></span></th>
        <td><span data-ttu-id="6e986-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="6e986-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="6e986-124">Fecha de modificación</span><span class="sxs-lookup"><span data-stu-id="6e986-124">Date Modified</span></span></th>
        <td><span data-ttu-id="6e986-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="6e986-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="6e986-126">Versiones compatibles de HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e986-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="6e986-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="6e986-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="6e986-128">Registro de cambios</span><span class="sxs-lookup"><span data-stu-id="6e986-128">Change Log</span></span></th>
        <td><span data-ttu-id="6e986-129">Actualizar base de datos de Azure Cosmos Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="6e986-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="6e986-130">Se ha agregado compatibilidad con las colecciones divididas como origen y receptor.</span><span class="sxs-lookup"><span data-stu-id="6e986-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="6e986-131"><a name="Prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6e986-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="6e986-132">Antes de seguir las instrucciones de hello en este tutorial, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="6e986-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="6e986-133">Una cuenta de Cosmos DB, una base de datos y una colección con documentos dentro.</span><span class="sxs-lookup"><span data-stu-id="6e986-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="6e986-134">Para más información, consulte [Introducción a Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="6e986-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="6e986-135">Importar datos de ejemplo a la cuenta de base de datos de Cosmos con hello [herramienta de importación de base de datos de Cosmos][import-data].</span><span class="sxs-lookup"><span data-stu-id="6e986-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="6e986-136">Capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="6e986-136">Throughput.</span></span> <span data-ttu-id="6e986-137">Las lecturas y escrituras de HDInsight se tienen en cuenta a la hora de calcular las unidades de solicitud asignadas a las colecciones.</span><span class="sxs-lookup"><span data-stu-id="6e986-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="6e986-138">Capacidad para un procedimiento almacenado adicional dentro de cada colección de salida.</span><span class="sxs-lookup"><span data-stu-id="6e986-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="6e986-139">procedimientos almacenado de Hola se usan para transferir los documentos resultantes.</span><span class="sxs-lookup"><span data-stu-id="6e986-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="6e986-140">Capacidad para documentos resultantes de Hola de trabajos de Hive, Pig y MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="6e986-141">[*Opcional*] Capacidad para una colección adicional.</span><span class="sxs-lookup"><span data-stu-id="6e986-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="6e986-142">En orden tooavoid Hola la creación de una nueva colección durante alguno de los trabajos de hello, puede imprimir Hola resultados toostdout, guardar el contenedor de hello salida tooyour WASB o especifique una recopilación ya existente.</span><span class="sxs-lookup"><span data-stu-id="6e986-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="6e986-143">En caso de hello de especificar una colección existente, se crearán nuevos documentos dentro de la colección de Hola y documentos ya existentes solo se verán afectados si se produce un conflicto en *identificadores*.</span><span class="sxs-lookup"><span data-stu-id="6e986-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="6e986-144">**Conector de Hello sobrescribirá automáticamente documentos existentes con los conflictos de identificador**.</span><span class="sxs-lookup"><span data-stu-id="6e986-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="6e986-145">Puede desactivar esta característica estableciendo Hola upsert opción toofalse.</span><span class="sxs-lookup"><span data-stu-id="6e986-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="6e986-146">Si es false upsert y se produce un conflicto, se producirá un error de trabajo de Hadoop de hello; informar de un error de conflicto de identificador.</span><span class="sxs-lookup"><span data-stu-id="6e986-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="6e986-147"><a name="ProvisionHDInsight"></a>Paso 1: Creación de un nuevo clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e986-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="6e986-148">Este tutorial usa la acción de secuencia de comandos de hello Azure Portal toocustomize su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="6e986-149">En este tutorial, usaremos hello Azure Portal toocreate su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="6e986-150">Para obtener instrucciones sobre cómo los cmdlets de PowerShell de toouse o hello HDInsight .NET SDK, visite la [HDInsight personalizar clústeres mediante la acción de secuencia de comandos] [ hdinsight-custom-provision] artículo.</span><span class="sxs-lookup"><span data-stu-id="6e986-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="6e986-151">Inicie sesión en toohello [Portal de Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6e986-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="6e986-152">Haga clic en **+ nuevo** en la parte superior de Hola de hello barra de navegación izquierda, busque **HDInsight** en la barra de búsqueda superior hello en la nueva hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="6e986-153">**HDInsight** publicados por **Microsoft** aparecerá en la parte superior de Hola de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="6e986-154">Haga clic en él y luego en **rear**.</span><span class="sxs-lookup"><span data-stu-id="6e986-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="6e986-155">En el nuevo HDInsight clúster Hola Crear hoja, escriba su **nombre del clúster** y seleccione hello **suscripción** desea tooprovision este recurso en.</span><span class="sxs-lookup"><span data-stu-id="6e986-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="6e986-156">Nombre del clúster</span><span class="sxs-lookup"><span data-stu-id="6e986-156">Cluster name</span></span></td><td><span data-ttu-id="6e986-157">Clúster de Hola de nombre.</span><span class="sxs-lookup"><span data-stu-id="6e986-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="6e986-158">El nombre DNS debe empezar y terminar con un carácter alfanumérico y puede contener guiones.</span><span class="sxs-lookup"><span data-stu-id="6e986-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="6e986-159">campo de Hello debe ser una cadena comprendida entre 3 y 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6e986-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="6e986-160">Subscription Name</span><span class="sxs-lookup"><span data-stu-id="6e986-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="6e986-161">Si tiene más de una suscripción de Azure, seleccione la suscripción de Hola que va a hospedar el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="6e986-162">
5.Haga clic en **Seleccionar tipo de clúster** y Hola conjunto después propiedades toohello los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="6e986-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="6e986-163">Tipo de clúster</span><span class="sxs-lookup"><span data-stu-id="6e986-163">Cluster type</span></span></td><td><span data-ttu-id="6e986-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="6e986-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="6e986-165">Nivel de clúster</span><span class="sxs-lookup"><span data-stu-id="6e986-165">Cluster tier</span></span></td><td><span data-ttu-id="6e986-166"><strong>Estándar</strong></span><span class="sxs-lookup"><span data-stu-id="6e986-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="6e986-167">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="6e986-167">Operating System</span></span></td><td><span data-ttu-id="6e986-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="6e986-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="6e986-169">Versión</span><span class="sxs-lookup"><span data-stu-id="6e986-169">Version</span></span></td><td><span data-ttu-id="6e986-170">Versión más reciente</span><span class="sxs-lookup"><span data-stu-id="6e986-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="6e986-171">Ahora, haga clic en **SELECCIONAR**.</span><span class="sxs-lookup"><span data-stu-id="6e986-171">Now, click **SELECT**.</span></span>

    ![Proporcionar detalles del clúster inicial de HDInsight de Hadoop][image-customprovision-page1]
6. <span data-ttu-id="6e986-173">Haga clic en **credenciales** tooset su inicio de sesión y credenciales de acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="6e986-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="6e986-174">Elija su **nombre de usuario de inicio de sesión del clúster** y **contraseña de inicio de sesión del clúster**.</span><span class="sxs-lookup"><span data-stu-id="6e986-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="6e986-175">Si desea tooremote en el clúster, seleccione *Sí* final Hola de hoja de Hola y proporcione un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="6e986-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="6e986-176">Haga clic en **origen de datos** tooset acceso de la ubicación principal para los datos.</span><span class="sxs-lookup"><span data-stu-id="6e986-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="6e986-177">Elija hello **método de selección de** y especificar una cuenta de almacenamiento ya existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="6e986-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="6e986-178">Hola la misma hoja en, especifique un **contenedor predeterminado** y un **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="6e986-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="6e986-179">A continuación, haga clic en **SELECCIONAR**.</span><span class="sxs-lookup"><span data-stu-id="6e986-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e986-180">Seleccione una región de la cuenta de base de datos de Cosmos para mejorar el rendimiento de ubicación cerrar tooyour</span><span class="sxs-lookup"><span data-stu-id="6e986-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="6e986-181">Haga clic en **precios** tooselect Hola número y tipo de nodos.</span><span class="sxs-lookup"><span data-stu-id="6e986-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="6e986-182">Puede mantener configuración predeterminada de Hola y escala Hola número de nodos de trabajo más adelante.</span><span class="sxs-lookup"><span data-stu-id="6e986-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="6e986-183">Haga clic en **configuración opcional**, a continuación, **acciones de Script** Hola hoja de configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="6e986-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="6e986-184">En acciones de secuencia de comandos, escriba Hola después información toocustomize su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="6e986-185">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6e986-185">Property</span></span></th><th><span data-ttu-id="6e986-186">Valor</span><span class="sxs-lookup"><span data-stu-id="6e986-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="6e986-187">Nombre</span><span class="sxs-lookup"><span data-stu-id="6e986-187">Name</span></span></td>
             <td><span data-ttu-id="6e986-188">Especifique un nombre para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="6e986-189">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="6e986-189">Script URI</span></span></td>
             <td><span data-ttu-id="6e986-190">Especifique Hola URI toohello script que es invocado toocustomize Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="6e986-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="6e986-191">Especifique esta información:</span><span class="sxs-lookup"><span data-stu-id="6e986-191">Please enter:</span></span> </br> <span data-ttu-id="6e986-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="6e986-193">Principal</span><span class="sxs-lookup"><span data-stu-id="6e986-193">Head</span></span></td>
             <td><span data-ttu-id="6e986-194">Haga clic en Hola casilla toorun Hola script de PowerShell en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="6e986-195">
             <strong>Active esta casilla</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="6e986-196">Trabajo</span><span class="sxs-lookup"><span data-stu-id="6e986-196">Worker</span></span></td>
             <td><span data-ttu-id="6e986-197">Haga clic en el script de PowerShell de hello casilla toorun hello en el nodo de trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="6e986-198">
             <strong>Active esta casilla</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="6e986-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="6e986-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="6e986-200">Haga clic en el script de PowerShell de hello casilla toorun hello en hello Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="6e986-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="6e986-201">
             <strong>No es necesario</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="6e986-202">parameters</span><span class="sxs-lookup"><span data-stu-id="6e986-202">Parameters</span></span></td>
             <td><span data-ttu-id="6e986-203">Especificar parámetros de hello, si así lo requiere el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="6e986-204">
             <strong>No se necesita ningún parámetro</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="6e986-205">
11. Cree un **grupo de recursos** o use uno existente en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e986-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="6e986-206">12.</span><span class="sxs-lookup"><span data-stu-id="6e986-206">12.</span></span> <span data-ttu-id="6e986-207">Ahora, compruebe **Pin toodashboard** tootrack su implementación y haga clic en **crear**!</span><span class="sxs-lookup"><span data-stu-id="6e986-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="6e986-208"><a name="InstallCmdlets"></a>Paso 2: Instalación y configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e986-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="6e986-209">Instale Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e986-209">Install Azure PowerShell.</span></span> <span data-ttu-id="6e986-210">Puede encontrar instrucciones [aquí][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="6e986-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e986-211">En el caso de las consultas de Hive, use el Editor de Hive en línea de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="6e986-212">toodo por lo tanto, inicie sesión en toohello [Portal de Azure][azure-portal], haga clic en **HDInsight** tooview de panel izquierdo hello en una lista de los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="6e986-213">Haga clic en el clúster de Hola que desea que las consultas de Hive toorun en y, a continuación, haga clic en **consola de consultas**.</span><span class="sxs-lookup"><span data-stu-id="6e986-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="6e986-214">Abra hello Azure PowerShell Integrated Scripting Environment:</span><span class="sxs-lookup"><span data-stu-id="6e986-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="6e986-215">En un equipo que ejecute Windows 8 o Windows Server 2012 o posterior, también puede usar integrada de hello búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6e986-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="6e986-216">En la pantalla de inicio de bienvenida, escriba **powershell ise** y haga clic en **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="6e986-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="6e986-217">En un equipo que ejecuta una versión anterior a Windows 8 o Windows Server 2012, utilice el menú de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="6e986-218">En el menú de inicio de hello, escriba **símbolo** en el cuadro de búsqueda de hello, luego, en lista de Hola de resultados, haga clic en **símbolo**.</span><span class="sxs-lookup"><span data-stu-id="6e986-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="6e986-219">Hola símbolo del sistema, escriba **powershell_ise** y haga clic en **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="6e986-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="6e986-220">Agregue su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e986-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="6e986-221">Hola panel de consola, escriba **Add-AzureAccount** y haga clic en **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="6e986-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="6e986-222">Escriba Hola dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="6e986-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="6e986-223">Escribir contraseña de hello para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e986-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="6e986-224">Haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="6e986-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="6e986-225">Hola después diagrama identifica partes importantes de Hola de su entorno de Scripting de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e986-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagrama de Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="6e986-227"><a name="RunHive"></a>Paso 3: Ejecución de un trabajo de Hive con Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e986-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6e986-228">Todas las variables indicadas con < > deben rellenarse con los valores de configuración adecuados.</span><span class="sxs-lookup"><span data-stu-id="6e986-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="6e986-229">Establecer Hola después de las variables en el panel de scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e986-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="6e986-230">Comencemos a construir la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="6e986-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="6e986-231">Escribiremos una consulta de Hive que toma las marcas de hora generada por el sistema (_ts) y los identificadores únicos (_rid) de una colección de base de datos de Azure Cosmos todos los documentos, cuenta todos los documentos por minuto de hello y, a continuación, vuelve a almacenar resultados de hello en una nueva colección de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6e986-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="6e986-232">En primer lugar se crea una tabla de Hive a partir de la colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6e986-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="6e986-233">Agregar Hola siguiente fragmento de código toohello panel de scripts de PowerShell <strong>después</strong> fragmento de código de hello de #1.</span><span class="sxs-lookup"><span data-stu-id="6e986-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="6e986-234">Asegúrese de que incluir Hola opcional DocumentDB.query parámetro t recorte nuestros documentos toojust _ts y _rid.</span><span class="sxs-lookup"><span data-stu-id="6e986-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="6e986-235">**La denominación de DocumentDB.inputCollections no era un error.**</span><span class="sxs-lookup"><span data-stu-id="6e986-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="6e986-236">Sí, se pueden agregar varias colecciones como una entrada:</span><span class="sxs-lookup"><span data-stu-id="6e986-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="6e986-237">A continuación, vamos a crear una tabla de Hive para la recopilación de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="6e986-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="6e986-238">propiedades de documento de salida de Hello será mes hello, día, hora, minuto y número total de Hola de repeticiones.</span><span class="sxs-lookup"><span data-stu-id="6e986-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e986-239">**Una vez más, la denominación de DocumentDB.outputCollections no era un error.**</span><span class="sxs-lookup"><span data-stu-id="6e986-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="6e986-240">Sí, se pueden agregar varias colecciones como una salida:</span><span class="sxs-lookup"><span data-stu-id="6e986-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="6e986-241">"*DocumentDB.outputCollections*"="*\<Nombre de la colección de salida de DocumentDB 1\>*,*\<Nombre de la colección de salida de DocumentDB 2\>*"</span><span class="sxs-lookup"><span data-stu-id="6e986-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="6e986-242">nombres de la colección de Hola se separan sin espacios en blanco, con solo una sola coma.</span><span class="sxs-lookup"><span data-stu-id="6e986-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="6e986-243">Documentos se distribuirán en cadena en varias colecciones.</span><span class="sxs-lookup"><span data-stu-id="6e986-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="6e986-244">Un lote de documentos se almacenará en una colección y, a continuación, un segundo lote de documentos se almacenará en la recolección siguiente de Hola y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="6e986-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="6e986-245">Por último, vamos a documentos de hello recuento por mes, día, hora y minuto e insertar resultados hello en hello habían salida tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="6e986-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="6e986-246">Agregar Hola siguientes toocreate de fragmento de script una definición de trabajo de Hive de consulta anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="6e986-247">También puede usar hello - archivo cambiar toospecify un archivo de script de HiveQL en HDFS.</span><span class="sxs-lookup"><span data-stu-id="6e986-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="6e986-248">Agregue Hola después de la hora de inicio de fragmento de código toosave hello y enviar el trabajo de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="6e986-249">Agregar Hola después toowait para toocomplete de trabajo de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="6e986-250">Agregue Hola siguientes tooprint Hola estándar hello y salida de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="6e986-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="6e986-251">**Ejecute** el nuevo script.</span><span class="sxs-lookup"><span data-stu-id="6e986-251">**Run** your new script!</span></span> <span data-ttu-id="6e986-252">**Haga clic en** verde Hola ejecutar botón.</span><span class="sxs-lookup"><span data-stu-id="6e986-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="6e986-253">Hola resultados de la comprobación.</span><span class="sxs-lookup"><span data-stu-id="6e986-253">Check hello results.</span></span> <span data-ttu-id="6e986-254">Inicio de sesión en hello [Portal de Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6e986-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="6e986-255">Haga clic en <strong>examinar</strong> en el panel del lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="6e986-256">Haga clic en <strong>todo</strong> en hello superior derecha del panel de exploración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="6e986-257">Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="6e986-258">A continuación, busque su <strong>cuenta de base de datos de Azure Cosmos</strong>, a continuación, <strong>base de datos de base de datos de Azure Cosmos</strong> y su <strong>colección de base de datos de Azure Cosmos</strong> asociados con la colección de salida de hello especificada en la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="6e986-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="6e986-259">Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="6e986-260">Verá los resultados de saludo de la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="6e986-260">You will see hello results of your Hive query.</span></span>

   ![Resultados de la consulta de Hive][image-hive-query-results]

## <span data-ttu-id="6e986-262"><a name="RunPig"></a>Paso 4: Ejecución de un trabajo de Pig con Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e986-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6e986-263">Todas las variables indicadas con < > deben rellenarse con los valores de configuración adecuados.</span><span class="sxs-lookup"><span data-stu-id="6e986-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="6e986-264">Establecer Hola después de las variables en el panel de scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e986-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="6e986-265">Comencemos a construir la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="6e986-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="6e986-266">Escribiremos una consulta de Pig que toma las marcas de hora generada por el sistema (_ts) y los identificadores únicos (_rid) de una colección de base de datos de Azure Cosmos todos los documentos, cuenta todos los documentos por minuto de hello y, a continuación, vuelve a almacenar resultados de hello en una nueva colección de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6e986-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="6e986-267">En primer lugar, cargue documentos de Cosmos DB en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="6e986-268">Agregar Hola siguiente fragmento de código toohello panel de scripts de PowerShell <strong>después</strong> fragmento de código de hello de #1.</span><span class="sxs-lookup"><span data-stu-id="6e986-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="6e986-269">Asegúrese de que tooadd una DocumentDB de consulta toohello opcional documentos consulta parámetro tootrim nuestros documentos toojust _ts y _rid.</span><span class="sxs-lookup"><span data-stu-id="6e986-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="6e986-270">Sí, se pueden agregar varias colecciones como una entrada:</span><span class="sxs-lookup"><span data-stu-id="6e986-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="6e986-271">"*\<Nombre de la colección de salida de DocumentDB 1\>*,*\<Nombre de la colección de salida de DocumentDB 2\>*"</span><span class="sxs-lookup"><span data-stu-id="6e986-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="6e986-272">nombres de la colección de Hola se separan sin espacios en blanco, con solo una sola coma.</span><span class="sxs-lookup"><span data-stu-id="6e986-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="6e986-273">Documentos se distribuirán en cadena en varias colecciones.</span><span class="sxs-lookup"><span data-stu-id="6e986-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="6e986-274">Un lote de documentos se almacenará en una colección y, a continuación, un segundo lote de documentos se almacenará en la recolección siguiente de Hola y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="6e986-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="6e986-275">A continuación, vamos a concuerdan documentos Hola por mes de hello, día, hora, minuto y número total de Hola de repeticiones.</span><span class="sxs-lookup"><span data-stu-id="6e986-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="6e986-276">Por último, vamos a almacenar resultados de hello en nuestra nueva colección de salida.</span><span class="sxs-lookup"><span data-stu-id="6e986-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e986-277">Sí, se pueden agregar varias colecciones como una salida:</span><span class="sxs-lookup"><span data-stu-id="6e986-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="6e986-278">"\<Nombre de la colección de salida de DocumentDB 1\>,\<Nombre de la colección de salida de DocumentDB 2\>"</span><span class="sxs-lookup"><span data-stu-id="6e986-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="6e986-279">nombres de la colección de Hola se separan sin espacios en blanco, con solo una sola coma.</span><span class="sxs-lookup"><span data-stu-id="6e986-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="6e986-280">Documenta will ser distribuida round robin en hello varias colecciones.</span><span class="sxs-lookup"><span data-stu-id="6e986-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="6e986-281">Un lote de documentos se almacenará en una colección y, a continuación, un segundo lote de documentos se almacenará en la recolección siguiente de Hola y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="6e986-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="6e986-282">Agregar Hola siguientes toocreate de fragmento de script una definición de trabajo de Pig de consulta anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="6e986-283">También puede usar hello - archivo cambiar toospecify un archivo de script de Pig en HDFS.</span><span class="sxs-lookup"><span data-stu-id="6e986-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="6e986-284">Agregue Hola después de la hora de inicio de fragmento de código toosave hello y enviar el trabajo de Pig Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="6e986-285">Agregar Hola después toowait para toocomplete de trabajo de Pig Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="6e986-286">Agregue Hola siguientes tooprint Hola estándar hello y salida de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="6e986-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="6e986-287">**Ejecute** el nuevo script.</span><span class="sxs-lookup"><span data-stu-id="6e986-287">**Run** your new script!</span></span> <span data-ttu-id="6e986-288">**Haga clic en** verde Hola ejecutar botón.</span><span class="sxs-lookup"><span data-stu-id="6e986-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="6e986-289">Hola resultados de la comprobación.</span><span class="sxs-lookup"><span data-stu-id="6e986-289">Check hello results.</span></span> <span data-ttu-id="6e986-290">Inicio de sesión en hello [Portal de Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6e986-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="6e986-291">Haga clic en <strong>examinar</strong> en el panel del lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="6e986-292">Haga clic en <strong>todo</strong> en hello superior derecha del panel de exploración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="6e986-293">Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="6e986-294">A continuación, busque su <strong>cuenta de base de datos de Azure Cosmos</strong>, a continuación, <strong>base de datos de base de datos de Azure Cosmos</strong> y su <strong>colección de base de datos de Azure Cosmos</strong> asociados con la colección de salida de hello especificada en la consulta de Pig.</span><span class="sxs-lookup"><span data-stu-id="6e986-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="6e986-295">Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="6e986-296">Verá los resultados de saludo de la consulta de Pig.</span><span class="sxs-lookup"><span data-stu-id="6e986-296">You will see hello results of your Pig query.</span></span>

    ![Resultados de la consulta de Pig][image-pig-query-results]

## <span data-ttu-id="6e986-298"><a name="RunMapReduce"></a>Paso 5: Ejecución de un trabajo de MapReduce con Azure Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e986-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="6e986-299">Establecer Hola después de las variables en el panel de scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e986-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="6e986-300">Se deberá ejecutar un trabajo de MapReduce que cuenta Hola número de repeticiones de cada propiedad de documento de la colección de la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6e986-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="6e986-301">Agregue este fragmento de script **después** fragmento Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="6e986-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="6e986-302">TallyProperties v01.jar incluye instalación personalizada de Hola de hello Cosmos conector de Hadoop de base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e986-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="6e986-303">Agregar Hola siguiendo el trabajo de MapReduce de comando toosubmit Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="6e986-304">Además toohello definición del trabajo MapReduce, también proporcionar nombre del clúster de HDInsight de Hola donde desee trabajo de MapReduce toorun hello y credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="6e986-305">Hola Start-AzureHDInsightJob es una llamada desincronizada.</span><span class="sxs-lookup"><span data-stu-id="6e986-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="6e986-306">finalización de hello toocheck de trabajo de hello, use hello *Wait-AzureHDInsightJob* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6e986-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="6e986-307">Agregar Hola después toocheck comando producido algún error en el trabajo en ejecución Hola MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6e986-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="6e986-308">**Ejecute** el nuevo script.</span><span class="sxs-lookup"><span data-stu-id="6e986-308">**Run** your new script!</span></span> <span data-ttu-id="6e986-309">**Haga clic en** verde Hola ejecutar botón.</span><span class="sxs-lookup"><span data-stu-id="6e986-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="6e986-310">Hola resultados de la comprobación.</span><span class="sxs-lookup"><span data-stu-id="6e986-310">Check hello results.</span></span> <span data-ttu-id="6e986-311">Inicio de sesión en hello [Portal de Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="6e986-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="6e986-312">Haga clic en <strong>examinar</strong> en el panel del lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="6e986-313">Haga clic en <strong>todo</strong> en hello superior derecha del panel de exploración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e986-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="6e986-314">Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="6e986-315">A continuación, busque su <strong>cuenta de base de datos de Azure Cosmos</strong>, a continuación, <strong>base de datos de base de datos de Azure Cosmos</strong> y su <strong>colección de base de datos de Azure Cosmos</strong> asociados con la colección de salida de hello especificada en el trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6e986-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="6e986-316">Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</span><span class="sxs-lookup"><span data-stu-id="6e986-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="6e986-317">Verá resultados Hola de su trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6e986-317">You will see hello results of your MapReduce job.</span></span>

      ![Resultados de la consulta de MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="6e986-319"><a name="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e986-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="6e986-320">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="6e986-320">Congratulations!</span></span> <span data-ttu-id="6e986-321">Acaba de ejecutar sus primeros trabajos de Hive, Pig y MapReduce con Azure Cosmos DB y HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e986-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="6e986-322">El conector de Hadoop tiene el código abierto.</span><span class="sxs-lookup"><span data-stu-id="6e986-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="6e986-323">Si le interesa, puede contribuir en [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="6e986-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="6e986-324">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="6e986-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="6e986-325">[Desarrollo de una aplicación Java con DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="6e986-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="6e986-326">[Desarrollo de programas MapReduce de Java para Hadoop en HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6e986-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="6e986-327">[Empezar a trabajar con Hadoop Hive en el uso de auriculares móviles de tooanalyze de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6e986-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="6e986-328">[Uso de MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6e986-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="6e986-329">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6e986-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="6e986-330">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6e986-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="6e986-331">[Personalización de los clústeres de HDInsight mediante la acción de script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="6e986-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
