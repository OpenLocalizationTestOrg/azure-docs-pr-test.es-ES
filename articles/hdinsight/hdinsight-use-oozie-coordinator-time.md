---
title: Coordinador basado en tiempo de Hadoop Oozie de aaaUse en HDInsight | Documentos de Microsoft
description: "Uso del coordinador de Oozie de Hadoop basado en tiempo en HDInsight, un servicio de big data. Obtenga información acerca de cómo toodefine Oozie flujos de trabajo y coordinadores de y enviar trabajos."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="2a170-104">Usar coordinador basado en tiempo de Oozie con Hadoop en flujos de trabajo de HDInsight toodefine y coordinar los trabajos</span><span class="sxs-lookup"><span data-stu-id="2a170-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="2a170-105">En este artículo, aprenderá cómo toodefine flujos de trabajo y los coordinadores, y cómo tootrigger Hola trabajos de coordinador, según el tiempo.</span><span class="sxs-lookup"><span data-stu-id="2a170-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="2a170-106">Resulta útil toogo a través de [Oozie de uso con HDInsight] [ hdinsight-use-oozie] antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="2a170-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="2a170-107">Además tooOozie, también puede programar trabajos mediante Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="2a170-108">toolearn Data Factory de Azure, consulte [uso de Pig y Hive con factoría de datos](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2a170-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2a170-109">En este artículo se requiere un clúster de HDInsight basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="2a170-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="2a170-110">Para obtener información sobre el uso de Oozie, incluidas las tareas basadas en tiempo, en un clúster basado en Linux, consulte [Oozie de uso con Hadoop toodefine y ejecutar un flujo de trabajo de HDInsight basados en Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="2a170-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="2a170-111">¿Qué es Oozie?</span><span class="sxs-lookup"><span data-stu-id="2a170-111">What is Oozie</span></span>
<span data-ttu-id="2a170-112">Oozie de Apache es un sistema de coordinación o flujo de trabajo que administra trabajos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2a170-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="2a170-113">Se integra con la pila de Hadoop de Hola y admite trabajos de Hadoop MapReduce Apache, Pig Apache, Apache Hive y Sqoop de Apache.</span><span class="sxs-lookup"><span data-stu-id="2a170-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="2a170-114">También puede ser tooschedule usado trabajos que el sistema tooa específico, como programas Java o secuencias de comandos de shell.</span><span class="sxs-lookup"><span data-stu-id="2a170-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="2a170-115">Hello siguiente imagen muestra flujo de trabajo de hello que implementará:</span><span class="sxs-lookup"><span data-stu-id="2a170-115">hello following image shows hello workflow you will implement:</span></span>

![Diagrama de flujo de trabajo][img-workflow-diagram]

<span data-ttu-id="2a170-117">flujo de trabajo de Hello contiene dos acciones:</span><span class="sxs-lookup"><span data-stu-id="2a170-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="2a170-118">Una acción de subárbol ejecuta un hello toocount de script de HiveQL apariciones de cada tipo de nivel de registro en un archivo de registro log4j.</span><span class="sxs-lookup"><span data-stu-id="2a170-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="2a170-119">Cada registro log4j consta de una línea de campos que contenga una [nivel de registro] campo tooshow Hola hello y tipo de gravedad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2a170-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="2a170-120">es similar a la salida del script de Hive Hola:</span><span class="sxs-lookup"><span data-stu-id="2a170-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="2a170-121">Para más información sobre Hive, consulte [Uso de Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="2a170-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="2a170-122">Una acción de Sqoop exporta hello HiveQL acción salida tooa tabla en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="2a170-123">Para obtener más información sobre Sqoop, consulte [Uso de Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="2a170-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="2a170-124">Para versiones compatibles de Oozie en clústeres de HDInsight, vea [cuáles son las novedades en las versiones de clúster Hola proporcionadas por HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="2a170-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2a170-125">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a170-125">Prerequisites</span></span>
<span data-ttu-id="2a170-126">Antes de comenzar este tutorial, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="2a170-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="2a170-127">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2a170-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2a170-128">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y desaparecerá por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="2a170-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="2a170-129">Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2a170-130">Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="2a170-131">Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2a170-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="2a170-132">**Un clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2a170-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="2a170-133">Para obtener más información sobre cómo crear un clúster de HDInsight, consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight][hdinsight-provision] o [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="2a170-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="2a170-134">Necesitará Hola después toogo datos tutorial Hola:</span><span class="sxs-lookup"><span data-stu-id="2a170-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a170-135">Propiedad del clúster</span><span class="sxs-lookup"><span data-stu-id="2a170-135">Cluster property</span></span></th><th><span data-ttu-id="2a170-136">Nombre de variable de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a170-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2a170-137">Valor</span><span class="sxs-lookup"><span data-stu-id="2a170-137">Value</span></span></th><th><span data-ttu-id="2a170-138">Description</span><span class="sxs-lookup"><span data-stu-id="2a170-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a170-139">Nombre del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a170-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="2a170-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="2a170-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="2a170-141">clúster de HDInsight de Hello en el que se ejecutará este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a170-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-142">Nombre de usuario del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a170-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="2a170-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="2a170-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="2a170-144">nombre de usuario de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2a170-145">Contraseña del usuario del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a170-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="2a170-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="2a170-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="2a170-147">contraseña de usuario de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-148">Nombre de la cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="2a170-148">Azure storage account name</span></span></td><td><span data-ttu-id="2a170-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="2a170-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="2a170-150">Un clúster de HDInsight toohello disponibles de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="2a170-151">Para este tutorial, utilice cuenta de almacenamiento predeterminada de Hola que haya especificado durante el proceso de aprovisionamiento de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-152">Nombre del contenedor de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="2a170-152">Azure Blob container name</span></span></td><td><span data-ttu-id="2a170-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="2a170-153">$containerName</span></span></td><td></td><td><span data-ttu-id="2a170-154">En este ejemplo, utilice el contenedor de almacenamiento de blobs de Azure de Hola que se usa para el sistema de archivos de clúster de HDInsight de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="2a170-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="2a170-155">De manera predeterminada, tiene Hola mismo nombre como clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="2a170-156">
* **Una base de datos SQL de Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a170-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="2a170-157">Debe configurar una regla de firewall para hello tooallow acceso de base de datos de SQL server desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2a170-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="2a170-158">Para obtener instrucciones sobre cómo crear una base de datos de SQL Azure y cómo configurar firewall de hello, consulte [empezar a usar la base de datos de SQL Azure] [sqldatabase get-iniciado].</span><span class="sxs-lookup"><span data-stu-id="2a170-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="2a170-159">En este artículo se proporciona un script de Windows PowerShell para crear la tabla de base de datos de SQL Azure Hola que necesite para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a170-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a170-160">Propiedad de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="2a170-160">SQL database property</span></span></th><th><span data-ttu-id="2a170-161">Nombre de variable de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a170-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2a170-162">Valor</span><span class="sxs-lookup"><span data-stu-id="2a170-162">Value</span></span></th><th><span data-ttu-id="2a170-163">Description</span><span class="sxs-lookup"><span data-stu-id="2a170-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a170-164">Nombre del servidor de base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="2a170-164">SQL database server name</span></span></td><td><span data-ttu-id="2a170-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="2a170-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="2a170-166">toowhich de servidor de base de datos SQL de Hello Sqoop exportará los datos.</span><span class="sxs-lookup"><span data-stu-id="2a170-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2a170-167">Nombre de inicio de sesión de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="2a170-167">SQL database login name</span></span></td><td><span data-ttu-id="2a170-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="2a170-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="2a170-169">Nombre de inicio de sesión de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2a170-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-170">Contraseña de inicio de sesión de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="2a170-170">SQL database login password</span></span></td><td><span data-ttu-id="2a170-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="2a170-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="2a170-172">Contraseña de inicio de sesión de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2a170-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-173">Nombre de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="2a170-173">SQL database name</span></span></td><td><span data-ttu-id="2a170-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="2a170-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="2a170-175">toowhich de base de datos de SQL Azure Hello Sqoop exportará los datos.</span><span class="sxs-lookup"><span data-stu-id="2a170-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="2a170-176">De forma predeterminada, una base de datos SQL de Azure permite realizar conexiones desde servicios de Azure, como HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="2a170-177">Si se deshabilita esta configuración de firewall, debe habilitarla de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="2a170-178">Para obtener instrucciones sobre la creación de una base de datos SQL y la configuración de las reglas de firewall, consulte [Creación y configuración de una base de datos SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2a170-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="2a170-179">Valores de hello de rellenar en las tablas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="2a170-180">Le resultará útil para completar el tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a170-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="2a170-181">Definir el flujo de trabajo de Oozie y Hola relacionados con script de HiveQL</span><span class="sxs-lookup"><span data-stu-id="2a170-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="2a170-182">Las definiciones de los flujos de trabajo de Oozie se escriben en hPDL (un lenguaje de definición de procesos XML).</span><span class="sxs-lookup"><span data-stu-id="2a170-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="2a170-183">es el nombre de archivo de flujo de trabajo predeterminado de Hello *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="2a170-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="2a170-184">Se guardar archivo de flujo de trabajo de hello localmente y, a continuación, implementarlo clúster de HDInsight toohello mediante Azure PowerShell más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a170-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="2a170-185">acción de Hive en el flujo de trabajo de Hola Hola llama a un archivo de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="2a170-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="2a170-186">El archivo de script contiene tres instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="2a170-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="2a170-187">**instrucción DROP TABLE de Hello** eliminaciones Hola log4j Hive tabla si existe.</span><span class="sxs-lookup"><span data-stu-id="2a170-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="2a170-188">**instrucción CREATE TABLE de Hello** crea una tabla externa de Hive log4j, que señala toohello ubicación del archivo de registro de hello log4j;</span><span class="sxs-lookup"><span data-stu-id="2a170-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="2a170-189">**Hola ubicación del archivo de registro de hello log4j**.</span><span class="sxs-lookup"><span data-stu-id="2a170-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="2a170-190">delimitador de campo de Hello es ",".</span><span class="sxs-lookup"><span data-stu-id="2a170-190">hello field delimiter is ",".</span></span> <span data-ttu-id="2a170-191">delimitador de línea de saludo predeterminado es "\n".</span><span class="sxs-lookup"><span data-stu-id="2a170-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="2a170-192">Una tabla externa de subárbol es el archivo de datos de Hola de tooavoid utilizado que se va a quitar de la ubicación original de hello, en caso de que desea que el flujo de trabajo de toorun hello Oozie varias veces.</span><span class="sxs-lookup"><span data-stu-id="2a170-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="2a170-193">**Hola instrucción INSERT SOBRESCRIBIR** recuentos de apariciones de Hola de cada tipo de nivel de registro de hello log4j tabla de Hive y guarda ubicación de almacenamiento de blobs de Azure de hello salida tooan.</span><span class="sxs-lookup"><span data-stu-id="2a170-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="2a170-194">Hay un problema conocido de la ruta de acceso de Hive.</span><span class="sxs-lookup"><span data-stu-id="2a170-194">There is a known Hive path issue.</span></span> <span data-ttu-id="2a170-195">Se producirá este problema cuando envíe un trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a170-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="2a170-196">Hola instrucciones para corregir el problema de hello puede encontrarse en hello Wiki de TechNet: [Hive de HDInsight de error: no se puede toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="2a170-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="2a170-197">**llamado por el flujo de trabajo de hello toodefine hello HiveQL script archivo toobe**</span><span class="sxs-lookup"><span data-stu-id="2a170-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="2a170-198">Cree un archivo de texto con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="2a170-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="2a170-199">Hay tres variables utilizadas en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="2a170-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="2a170-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2a170-200">${hiveTableName}</span></span>
   * <span data-ttu-id="2a170-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2a170-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="2a170-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2a170-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="2a170-203">archivo de definición de flujo de trabajo de Hello (workflow.xml en este tutorial) pasará estos toothis valores script de HiveQL en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2a170-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="2a170-204">Guardar archivo de hello como **C:\Tutorials\UseOozie\useooziewf.hql** usando la codificación ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2a170-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2a170-205">(Use el Bloc de notas si el editor de texto no proporciona esta opción.) El archivo de script será clúster de HDInsight implementado toohello más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="2a170-206">**toodefine un flujo de trabajo**</span><span class="sxs-lookup"><span data-stu-id="2a170-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="2a170-207">Cree un archivo de texto con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="2a170-207">Create a text file with hello following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="2a170-208">Hay dos acciones definidas en el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="2a170-209">Hola inicio-tooaction es *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="2a170-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="2a170-210">Si se ejecuta la acción de hello *Aceptar*, la acción siguiente hello es *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="2a170-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="2a170-211">Hola RunHiveScript tiene varias variables.</span><span class="sxs-lookup"><span data-stu-id="2a170-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="2a170-212">Valores de hello pasará al enviar trabajo de Oozie Hola desde su estación de trabajo mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="2a170-213">Variables de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="2a170-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a170-214">Variables de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="2a170-214">Workflow variables</span></span></th><th><span data-ttu-id="2a170-215">Description</span><span class="sxs-lookup"><span data-stu-id="2a170-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a170-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="2a170-216">${jobTracker}</span></span></td><td><span data-ttu-id="2a170-217">Especifique la dirección URL de Hola de seguimiento de trabajo de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="2a170-218">Use <strong>jobtrackerhost:9010</strong> en la versión del clúster de HDInsight 3.0 y 2.0.</span><span class="sxs-lookup"><span data-stu-id="2a170-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="2a170-219">${nameNode}</span></span></td><td><span data-ttu-id="2a170-220">Especifique la dirección URL de hello del nodo de nombre de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="2a170-221">Usar wasb de sistema de archivos de hello predeterminado: / / dirección, por ejemplo, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="2a170-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="2a170-222">${queueName}</span></span></td><td><span data-ttu-id="2a170-223">Especifica el nombre de la cola de Hola que Hola trabajo se enviarán a.</span><span class="sxs-lookup"><span data-stu-id="2a170-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="2a170-224">Use el <strong>valor predeterminado</strong>.</span><span class="sxs-lookup"><span data-stu-id="2a170-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="2a170-225">Variables de acción de Hive</span><span class="sxs-lookup"><span data-stu-id="2a170-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a170-226">Variable de acción de Hive</span><span class="sxs-lookup"><span data-stu-id="2a170-226">Hive action variable</span></span></th><th><span data-ttu-id="2a170-227">Description</span><span class="sxs-lookup"><span data-stu-id="2a170-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a170-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2a170-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="2a170-229">directorio de origen de Hola de hello comando Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="2a170-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2a170-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2a170-231">carpeta de salida de Hello de hello instrucción INSERT SOBRESCRIBIR.</span><span class="sxs-lookup"><span data-stu-id="2a170-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2a170-232">${hiveTableName}</span></span></td><td><span data-ttu-id="2a170-233">nombre de Hola de tabla de Hive de Hola que hace referencia a archivos de datos de log4j Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="2a170-234">Variables de acción de Sqoop</span><span class="sxs-lookup"><span data-stu-id="2a170-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a170-235">Variable de acción de Sqoop</span><span class="sxs-lookup"><span data-stu-id="2a170-235">Sqoop action variable</span></span></th><th><span data-ttu-id="2a170-236">Description</span><span class="sxs-lookup"><span data-stu-id="2a170-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a170-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="2a170-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="2a170-238">Cadena de conexión de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2a170-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="2a170-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="2a170-240">se exportarán Hello Azure base de datos tabla toowhere Hola de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="2a170-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a170-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2a170-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2a170-242">carpeta de salida de Hello de hello instrucción Hive insertar SOBRESCRIBIR.</span><span class="sxs-lookup"><span data-stu-id="2a170-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="2a170-243">Se trata de hello misma carpeta para la exportación de Sqoop Hola (export-dir).</span><span class="sxs-lookup"><span data-stu-id="2a170-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="2a170-244">Para obtener más información sobre el flujo de trabajo de Oozie y el uso de las acciones de flujo de trabajo de hello, consulte [documentación de Apache Oozie 4.0] [ apache-oozie-400] (con la versión de clúster de HDInsight 3.0) o [Apache Oozie 3.3.2 documentación] [ apache-oozie-332] (para la versión 2.1 del clúster de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="2a170-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="2a170-245">Guardar archivo de hello como **C:\Tutorials\UseOozie\workflow.xml** usando la codificación ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2a170-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2a170-246">(Use el Bloc de notas si el editor de texto no proporciona esta opción.)</span><span class="sxs-lookup"><span data-stu-id="2a170-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="2a170-247">**toodefine coordinador**</span><span class="sxs-lookup"><span data-stu-id="2a170-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="2a170-248">Cree un archivo de texto con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="2a170-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="2a170-249">Hay cinco variables utilizadas en el archivo de definición de hello:</span><span class="sxs-lookup"><span data-stu-id="2a170-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="2a170-250">Variable</span><span class="sxs-lookup"><span data-stu-id="2a170-250">Variable</span></span> | <span data-ttu-id="2a170-251">Description</span><span class="sxs-lookup"><span data-stu-id="2a170-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="2a170-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="2a170-252">${coordFrequency}</span></span> |<span data-ttu-id="2a170-253">Hora de pausa del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2a170-253">Job pause time.</span></span> <span data-ttu-id="2a170-254">La frecuencia se expresa siempre en minutos.</span><span class="sxs-lookup"><span data-stu-id="2a170-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="2a170-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="2a170-255">${coordStart}</span></span> |<span data-ttu-id="2a170-256">Hora de inicio del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2a170-256">Job start time.</span></span> |
   | <span data-ttu-id="2a170-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="2a170-257">${coordEnd}</span></span> |<span data-ttu-id="2a170-258">Hora de finalización del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2a170-258">Job end time.</span></span> |
   | <span data-ttu-id="2a170-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="2a170-259">${coordTimezone}</span></span> |<span data-ttu-id="2a170-260">Oozie procesa los trabajos del coordinador en una zona horaria fija sin horario de verano (representado normalmente mediante UTC).</span><span class="sxs-lookup"><span data-stu-id="2a170-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="2a170-261">Esta zona horaria se conoce como Hola "Oozie procesamiento timezone."</span><span class="sxs-lookup"><span data-stu-id="2a170-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="2a170-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="2a170-262">${wfPath}</span></span> |<span data-ttu-id="2a170-263">ruta de acceso de Hola para workflow.xml Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="2a170-264">Si el nombre de archivo de flujo de trabajo de hello no es nombre de archivo predeterminado de hello (workflow.xml), debe especificarlo.</span><span class="sxs-lookup"><span data-stu-id="2a170-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="2a170-265">Guardar archivo de hello como **C:\Tutorials\UseOozie\coordinator.xml** usando la codificación de hello ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2a170-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2a170-266">(Use el Bloc de notas si el editor de texto no proporciona esta opción.)</span><span class="sxs-lookup"><span data-stu-id="2a170-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="2a170-267">Implementar proyecto de Oozie hello y preparar el tutorial Hola</span><span class="sxs-lookup"><span data-stu-id="2a170-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="2a170-268">Se ejecutará una siguiente de hello Azure PowerShell tooperform de secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="2a170-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="2a170-269">Copia Hola almacenamiento de blobs de HiveQL (useoozie.hql) de la secuencia de comandos tooAzure, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="2a170-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="2a170-270">Copie el archivo workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2a170-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="2a170-271">Copie coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="2a170-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="2a170-272">Archivo de datos de copia hello (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="2a170-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="2a170-273">Cree una tabla de base de datos SQL de Azure para el almacenamiento de datos de exportación de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2a170-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="2a170-274">es el nombre de la tabla de Hello *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="2a170-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="2a170-275">**Descripción del almacenamiento de HDInsight**</span><span class="sxs-lookup"><span data-stu-id="2a170-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="2a170-276">HDInsight usa el almacenamiento de blobs de Azure para almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="2a170-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="2a170-277">wasb: / / es la implementación de sistema de archivos distribuido de Hadoop Hola (HDFS) en almacenamiento de blobs de Azure de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2a170-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="2a170-278">Para obtener más información, consulte [Uso de Azure Blob Storage con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="2a170-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2a170-279">Cuando se aprovisiona un clúster de HDInsight, una cuenta de almacenamiento de blobs de Azure y un contenedor específico de esa cuenta se designa como sistema de archivos predeterminado de hello, al igual que en HDFS.</span><span class="sxs-lookup"><span data-stu-id="2a170-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="2a170-280">Además toothis cuenta de almacenamiento, puede agregar cuentas de almacenamiento adicional de hello misma suscripción de Azure o desde diferentes suscripciones de Azure durante el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="2a170-281">Para obtener instrucciones sobre cómo agregar más cuentas de almacenamiento, consulte [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="2a170-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="2a170-282">script de PowerShell de Azure de toosimplify Hola usado en este tutorial, todos de hello archivos se almacenan en el contenedor de sistema de archivos de hello predeterminado se encuentran en */tutoriales/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="2a170-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="2a170-283">De forma predeterminada, este contenedor tiene Hola mismo nombre como nombre de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="2a170-284">Hola sintaxis es:</span><span class="sxs-lookup"><span data-stu-id="2a170-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="2a170-285">Hola solo *wasb: / /* la sintaxis es compatible con la versión 3.0 del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a170-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="2a170-286">Hola anterior *asv: / /* se admiten la sintaxis de 1.6 clústeres y 2.1 de HDInsight, pero no se admite en clústeres de HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="2a170-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="2a170-287">Hola wasb: / / ruta de acceso es una ruta de acceso virtual.</span><span class="sxs-lookup"><span data-stu-id="2a170-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="2a170-288">Para obtener más información, consulte [Uso de Azure Blob Storage con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="2a170-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2a170-289">Un archivo que se almacena en el contenedor de sistema de archivos de hello predeterminado puede tener acceso desde HDInsight mediante cualquiera de hello después a URI (utilizo workflow.xml como ejemplo):</span><span class="sxs-lookup"><span data-stu-id="2a170-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="2a170-290">Si desea tooaccess Hola archivo directamente desde la cuenta de almacenamiento de hello, nombre de blob de hello para el archivo hello es:</span><span class="sxs-lookup"><span data-stu-id="2a170-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="2a170-291">**Descripción de las tablas internas y externas de Hive**</span><span class="sxs-lookup"><span data-stu-id="2a170-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="2a170-292">Hay algunas cosas que debe tooknow acerca de las tablas internas y externas de Hive:</span><span class="sxs-lookup"><span data-stu-id="2a170-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="2a170-293">Hola comando CREATE TABLE crea una tabla interna, también conocido como una tabla administrada.</span><span class="sxs-lookup"><span data-stu-id="2a170-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="2a170-294">archivo de datos de Hello debe estar ubicado en el contenedor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="2a170-295">Hola comando CREATE TABLE mueve datos Hola archivotoohello/hive/almacenamiento/<TableName> carpeta en el contenedor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="2a170-296">Hola comando CREATE TABLE externo crea una tabla externa.</span><span class="sxs-lookup"><span data-stu-id="2a170-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="2a170-297">archivo de datos de Hello puede encontrarse fuera del contenedor predeterminado Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="2a170-298">Hola comando CREATE TABLE externo no mueve los archivos de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="2a170-299">Hola comando CREATE TABLE externo no permite que las subcarpetas de la carpeta de Hola que se especifica en la cláusula de ubicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="2a170-300">Se trata de motivo Hola ¿por qué tutorial Hola realiza una copia del archivo de hello sample.log.</span><span class="sxs-lookup"><span data-stu-id="2a170-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="2a170-301">Para obtener más información, consulte [HDInsight: introducción de tablas internas y externas de Hive][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="2a170-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="2a170-302">**tutorial de hello tooprepare**</span><span class="sxs-lookup"><span data-stu-id="2a170-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="2a170-303">Hola abrir Windows PowerShell ISE (en la pantalla de inicio de Windows 8 de bienvenida, escriba **PowerShell_ISE**y, a continuación, haga clic en **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="2a170-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2a170-304">Consulte [Iniciar Windows PowerShell en Windows 8 y Windows][powershell-start] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2a170-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2a170-305">En el panel de la parte inferior de hello, ejecute hello después comando tooconnect tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="2a170-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="2a170-306">También será tooenter solicitada sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="2a170-307">Este método para agregar una conexión a una suscripción expire y después de 12 horas, tendrá toorun Hola cmdlet nuevo.</span><span class="sxs-lookup"><span data-stu-id="2a170-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2a170-308">Si tiene varias suscripciones de Azure y suscripción predeterminada de hello no es hello uno desea toouse, usar hello <strong>Select-AzureSubscription</strong> tooselect cmdlet una suscripción.</span><span class="sxs-lookup"><span data-stu-id="2a170-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="2a170-309">Copie Hola siguiente secuencia de comandos en el panel de scripts de hello y, a continuación, establezca las variables de seis primeros hello:</span><span class="sxs-lookup"><span data-stu-id="2a170-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="2a170-310">Para obtener más descripciones de las variables de hello, vea hello [requisitos previos](#prerequisites) sección en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a170-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="2a170-311">Anexar Hola siguiente secuencia de comandos toohello en el panel de scripts de hello:</span><span class="sxs-lookup"><span data-stu-id="2a170-311">Append hello following toohello script in hello script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="2a170-312">Haga clic en **ejecutar Script** o presione **F5** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="2a170-313">salida de Hello será similar al:</span><span class="sxs-lookup"><span data-stu-id="2a170-313">hello output will be similar to:</span></span>

    ![Resultado de preparación del tutorial][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="2a170-315">Ejecute hello Oozie proyecto</span><span class="sxs-lookup"><span data-stu-id="2a170-315">Run hello Oozie project</span></span>
<span data-ttu-id="2a170-316">Azure PowerShell no proporciona actualmente cmdlets para la definición de trabajos de Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a170-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="2a170-317">Puede usar hello **Invoke-RestMethod** servicios web de cmdlet tooinvoke Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a170-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="2a170-318">Hola Oozie API para servicios web es una API de JSON de REST de HTTP.</span><span class="sxs-lookup"><span data-stu-id="2a170-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="2a170-319">Para obtener más información sobre los servicios web de Oozie Hola API, consulte [documentación de Apache Oozie 4.0] [ apache-oozie-400] (con la versión de clúster de HDInsight 3.0) o [documentación de Apache Oozie 3.3.2] [ apache-oozie-332] (para la versión 2.1 del clúster de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="2a170-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="2a170-320">**toosubmit un trabajo de Oozie**</span><span class="sxs-lookup"><span data-stu-id="2a170-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="2a170-321">Hola abrir Windows PowerShell ISE (en la pantalla de inicio de Windows 8, escriba **PowerShell_ISE**y, a continuación, haga clic en **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="2a170-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2a170-322">Consulte [Iniciar Windows PowerShell en Windows 8 y Windows][powershell-start] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2a170-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2a170-323">Script siguiente de Hola de copia en el panel de scripts de hello y, a continuación, conjunto Hola variables primero catorce (sin embargo, omitir **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="2a170-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="2a170-324">Para obtener más descripciones de las variables de hello, vea hello [requisitos previos](#prerequisites) sección en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a170-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="2a170-325">$coordstart y $coordend son de flujo de trabajo a partir de Hola y hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="2a170-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="2a170-326">toofind hora UTC/GMT de hello, busque "hora utc" en bing.com. Hola $coordFrequency es la frecuencia en minutos que desea que el flujo de trabajo de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="2a170-327">Anexar Hola siguiente secuencia de comandos de toohello.</span><span class="sxs-lookup"><span data-stu-id="2a170-327">Append hello following toohello script.</span></span> <span data-ttu-id="2a170-328">Este elemento define la carga de Oozie Hola:</span><span class="sxs-lookup"><span data-stu-id="2a170-328">This part defines hello Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="2a170-329">archivo de carga de envío de flujo de trabajo de diferencia importante en comparación con toohello Hello es variable hello **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="2a170-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="2a170-330">Al enviar una tarea de flujo de trabajo, se usa **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="2a170-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="2a170-331">Anexar Hola siguiente secuencia de comandos de toohello.</span><span class="sxs-lookup"><span data-stu-id="2a170-331">Append hello following toohello script.</span></span> <span data-ttu-id="2a170-332">Esta parte comprueba el estado del servicio de hello Oozie web:</span><span class="sxs-lookup"><span data-stu-id="2a170-332">This part checks hello Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="2a170-333">Anexar Hola siguiente secuencia de comandos de toohello.</span><span class="sxs-lookup"><span data-stu-id="2a170-333">Append hello following toohello script.</span></span> <span data-ttu-id="2a170-334">En esta parte se crea un trabajo de Oozie:</span><span class="sxs-lookup"><span data-stu-id="2a170-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="2a170-335">Cuando se envía un trabajo de flujo de trabajo, debe realizar otro trabajo web servicio llamada toostart Hola después de que se crea el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="2a170-336">En este caso, el trabajo de coordinador de Hola se desencadena por tiempo.</span><span class="sxs-lookup"><span data-stu-id="2a170-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="2a170-337">trabajo de Hola se iniciará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2a170-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="2a170-338">Anexar Hola siguiente secuencia de comandos de toohello.</span><span class="sxs-lookup"><span data-stu-id="2a170-338">Append hello following toohello script.</span></span> <span data-ttu-id="2a170-339">Este elemento comprueba el estado del trabajo de Hola Oozie:</span><span class="sxs-lookup"><span data-stu-id="2a170-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="2a170-340">(Opcional) Anexar Hola siguiente secuencia de comandos de toohello.</span><span class="sxs-lookup"><span data-stu-id="2a170-340">(Optional) Append hello following toohello script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="2a170-341">Anexar Hola siguiente secuencia de comandos de toohello:</span><span class="sxs-lookup"><span data-stu-id="2a170-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="2a170-342">Quitar signos de hello # si desea que las funciones adicionales de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="2a170-343">Si el clúster de HDinsight es la versión 2.1, reemplace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" por "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="2a170-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="2a170-344">Versión de clúster de HDInsight 2.1 no no admite la versión 2 de servicios web de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="2a170-345">Haga clic en **ejecutar Script** o presione **F5** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="2a170-346">salida de Hello será similar al:</span><span class="sxs-lookup"><span data-stu-id="2a170-346">hello output will be similar to:</span></span>

     ![Resultado del flujo de trabajo de ejecución del tutorial][img-runworkflow-output]
11. <span data-ttu-id="2a170-348">Conectar tooyour hello que exporta datos de base de datos SQL toosee.</span><span class="sxs-lookup"><span data-stu-id="2a170-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="2a170-349">**registro de errores de trabajo de hello toocheck**</span><span class="sxs-lookup"><span data-stu-id="2a170-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="2a170-350">tootroubleshoot un flujo de trabajo, archivo de registro de hello Oozie puede encontrarse en C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log desde el nodo principal del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="2a170-351">Para obtener información acerca de RDP, consulte [clústeres de HDInsight de administración con Hola portal de Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="2a170-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="2a170-352">**tutorial de hello toorerun**</span><span class="sxs-lookup"><span data-stu-id="2a170-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="2a170-353">flujo de trabajo de toorerun hello, debe realizar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="2a170-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="2a170-354">Elimine el archivo de salida de script de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="2a170-355">Eliminar datos de hello en la tabla de log4jLogsCount Hola.</span><span class="sxs-lookup"><span data-stu-id="2a170-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="2a170-356">Aquí tiene un script de Windows PowerShell de ejemplo que puede usar:</span><span class="sxs-lookup"><span data-stu-id="2a170-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="2a170-357">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a170-357">Next steps</span></span>
<span data-ttu-id="2a170-358">En este tutorial, se habrá aprendido cómo toodefine un flujo de trabajo de Oozie y un coordinador de Oozie y cómo toorun un coordinador de Oozie de trabajo mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a170-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="2a170-359">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="2a170-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="2a170-360">[Introducción a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2a170-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="2a170-361">[Uso de Azure Blob Storage con HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="2a170-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="2a170-362">[Administración de HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="2a170-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="2a170-363">[Cargar datos tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="2a170-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="2a170-364">[Uso de Sqoop con HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="2a170-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="2a170-365">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2a170-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2a170-366">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2a170-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2a170-367">[Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2a170-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
