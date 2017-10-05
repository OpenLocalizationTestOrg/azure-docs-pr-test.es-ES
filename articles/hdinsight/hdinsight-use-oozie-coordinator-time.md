---
title: Uso del coordinador de Oozie de Hadoop basado en tiempo en HDInsight | Microsoft Docs
description: "Uso del coordinador de Oozie de Hadoop basado en tiempo en HDInsight, un servicio de big data. Aprenda a definir flujos de trabajo y coordinadores de Oozie y envíe trabajos."
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
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="307fd-104">Uso del coordinador de Oozie basado en tiempo con Hadoop en HDInsight para definir flujos de trabajo y coordinar trabajos</span><span class="sxs-lookup"><span data-stu-id="307fd-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="307fd-105">En este artículo, obtenga información sobre cómo definir los flujos de trabajo y los coordinadores, así como el modo de desencadenar los trabajos del coordinador basados en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="307fd-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="307fd-106">Le resultará útil repasar el artículo [Uso de Oozie con HDInsight][hdinsight-use-oozie] antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="307fd-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="307fd-107">Además de con Oozie, también puede programar trabajos usando Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="307fd-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="307fd-108">Para obtener información sobre la factoría de datos de Azure, consulte [Uso de Pig y Hive con la factoría de datos](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="307fd-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="307fd-109">En este artículo se requiere un clúster de HDInsight basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="307fd-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="307fd-110">Para obtener información sobre el uso de Oozie, incluidos los trabajos basados en tiempo, en un clúster basado en Linux, consulte [Uso de Oozie con Hadoop para definir y ejecutar un flujo de trabajo en HDInsight basado en Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="307fd-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="307fd-111">¿Qué es Oozie?</span><span class="sxs-lookup"><span data-stu-id="307fd-111">What is Oozie</span></span>
<span data-ttu-id="307fd-112">Oozie de Apache es un sistema de coordinación o flujo de trabajo que administra trabajos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="307fd-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="307fd-113">Se integra con la pila de Hadoop y es compatible con los trabajos de Hadoop para MapReduce, Pig, Hive y Sqoop de Apache.</span><span class="sxs-lookup"><span data-stu-id="307fd-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="307fd-114">También puede usarse para programar trabajos específicos de un sistema, como scripts de shell o programas Java.</span><span class="sxs-lookup"><span data-stu-id="307fd-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="307fd-115">En la siguiente imagen se muestra el flujo de trabajo que se va a implementar:</span><span class="sxs-lookup"><span data-stu-id="307fd-115">The following image shows the workflow you will implement:</span></span>

![Diagrama de flujo de trabajo][img-workflow-diagram]

<span data-ttu-id="307fd-117">El flujo de trabajo contiene dos acciones:</span><span class="sxs-lookup"><span data-stu-id="307fd-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="307fd-118">Una acción de Hive ejecuta un script de HiveQL para contar las apariciones de cada tipo de nivel de registro en un archivo de registro log4j.</span><span class="sxs-lookup"><span data-stu-id="307fd-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="307fd-119">Cada registro log4j consta de una línea de campos que contiene uno llamado [LOG LEVEL] que muestra el tipo y la gravedad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="307fd-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="307fd-120">El resultado del script de Hive será parecido al siguiente:</span><span class="sxs-lookup"><span data-stu-id="307fd-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="307fd-121">Para más información sobre Hive, consulte [Uso de Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="307fd-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="307fd-122">Una acción de Sqoop exporta el resultado de la acción de HiveQL a una tabla en una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="307fd-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="307fd-123">Para obtener más información sobre Sqoop, consulte [Uso de Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="307fd-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="307fd-124">Para ver las versiones de Oozie compatibles en los clústeres de HDInsight, consulte [Novedades en las versiones de clústeres proporcionadas por HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="307fd-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="307fd-125">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="307fd-125">Prerequisites</span></span>
<span data-ttu-id="307fd-126">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="307fd-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="307fd-127">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="307fd-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="307fd-128">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y desaparecerá por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="307fd-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="307fd-129">En los pasos descritos en este documento, se usan los nuevos cmdlets de HDInsight que funcionan con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="307fd-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="307fd-130">Para instalar la versión más reciente, siga los pasos descritos en [Cómo instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) .</span><span class="sxs-lookup"><span data-stu-id="307fd-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="307fd-131">Si tiene scripts que se deben modificar para usar los nuevos cmdlets que funcionan con Azure Resource Manager, consulte [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) (Migración a herramientas de desarrollo basadas en Azure Resource Manager para clústeres de HDInsight) para más información.</span><span class="sxs-lookup"><span data-stu-id="307fd-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="307fd-132">**Un clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="307fd-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="307fd-133">Para obtener más información sobre cómo crear un clúster de HDInsight, consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight][hdinsight-provision] o [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="307fd-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="307fd-134">Para completar el tutorial, necesitará los datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="307fd-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="307fd-135">Propiedad del clúster</span><span class="sxs-lookup"><span data-stu-id="307fd-135">Cluster property</span></span></th><th><span data-ttu-id="307fd-136">Nombre de variable de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="307fd-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="307fd-137">Valor</span><span class="sxs-lookup"><span data-stu-id="307fd-137">Value</span></span></th><th><span data-ttu-id="307fd-138">Description</span><span class="sxs-lookup"><span data-stu-id="307fd-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="307fd-139">Nombre del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="307fd-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="307fd-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="307fd-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="307fd-141">El clúster de HDInsight al que aplicará este tutorial.</span><span class="sxs-lookup"><span data-stu-id="307fd-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-142">Nombre de usuario del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="307fd-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="307fd-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="307fd-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="307fd-144">El nombre del usuario del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="307fd-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="307fd-145">Contraseña del usuario del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="307fd-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="307fd-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="307fd-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="307fd-147">La contraseña de usuario del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="307fd-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-148">Nombre de la cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="307fd-148">Azure storage account name</span></span></td><td><span data-ttu-id="307fd-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="307fd-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="307fd-150">Cuenta de almacenamiento de Azure disponible para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="307fd-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="307fd-151">Para este tutorial, use la cuenta de almacenamiento predeterminada especificada durante el proceso de aprovisionamiento del clúster.</span><span class="sxs-lookup"><span data-stu-id="307fd-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-152">Nombre del contenedor de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="307fd-152">Azure Blob container name</span></span></td><td><span data-ttu-id="307fd-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="307fd-153">$containerName</span></span></td><td></td><td><span data-ttu-id="307fd-154">Para este ejemplo, use el contenedor de almacenamiento de blobs de Azure que se usa para el sistema de archivos predeterminado del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="307fd-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="307fd-155">De manera predeterminada, tiene el mismo nombre que el del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="307fd-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="307fd-156">
* **Una base de datos SQL de Azure**.</span><span class="sxs-lookup"><span data-stu-id="307fd-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="307fd-157">Debe configurar una regla de firewall para que el servidor de Base de datos SQL permita el acceso desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="307fd-158">Para obtener instrucciones sobre cómo crear una base de datos de Azure SQL y configurar el firewall, consulte [Introducción al uso de Azure SQL Database][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="307fd-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="307fd-159">En este artículo se proporciona un script de Windows PowerShell para crear la tabla de base de datos SQL de Azure requerida para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="307fd-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="307fd-160">Propiedad de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="307fd-160">SQL database property</span></span></th><th><span data-ttu-id="307fd-161">Nombre de variable de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="307fd-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="307fd-162">Valor</span><span class="sxs-lookup"><span data-stu-id="307fd-162">Value</span></span></th><th><span data-ttu-id="307fd-163">Description</span><span class="sxs-lookup"><span data-stu-id="307fd-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="307fd-164">Nombre del servidor de base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="307fd-164">SQL database server name</span></span></td><td><span data-ttu-id="307fd-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="307fd-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="307fd-166">El servidor de base de datos SQL en el que Sqoop exportará los datos.</span><span class="sxs-lookup"><span data-stu-id="307fd-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="307fd-167">Nombre de inicio de sesión de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="307fd-167">SQL database login name</span></span></td><td><span data-ttu-id="307fd-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="307fd-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="307fd-169">Nombre de inicio de sesión de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="307fd-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-170">Contraseña de inicio de sesión de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="307fd-170">SQL database login password</span></span></td><td><span data-ttu-id="307fd-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="307fd-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="307fd-172">Contraseña de inicio de sesión de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="307fd-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-173">Nombre de la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="307fd-173">SQL database name</span></span></td><td><span data-ttu-id="307fd-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="307fd-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="307fd-175">La base de datos SQL de Azure en la que Sqoop exportará los datos.</span><span class="sxs-lookup"><span data-stu-id="307fd-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="307fd-176">De forma predeterminada, una base de datos SQL de Azure permite realizar conexiones desde servicios de Azure, como HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="307fd-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="307fd-177">Si la configuración del firewall está deshabilitada, debe habilitarla en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="307fd-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="307fd-178">Para obtener instrucciones sobre la creación de una base de datos SQL y la configuración de las reglas de firewall, consulte [Creación y configuración de una base de datos SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="307fd-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="307fd-179">Rellene los valores de las tablas.</span><span class="sxs-lookup"><span data-stu-id="307fd-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="307fd-180">Le resultará útil para completar el tutorial.</span><span class="sxs-lookup"><span data-stu-id="307fd-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="307fd-181">Definición del flujo de trabajo de Oozie y el script de HiveQL relacionado</span><span class="sxs-lookup"><span data-stu-id="307fd-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="307fd-182">Las definiciones de los flujos de trabajo de Oozie se escriben en hPDL (un lenguaje de definición de procesos XML).</span><span class="sxs-lookup"><span data-stu-id="307fd-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="307fd-183">El nombre de archivo de flujo de trabajo predeterminado es *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="307fd-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="307fd-184">Guardará el archivo de flujo de trabajo localmente y lo implementará en el clúster de HDInsight con Azure PowerShell posteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="307fd-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="307fd-185">La acción de Hive en el flujo de trabajo llama a un archivo de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="307fd-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="307fd-186">El archivo de script contiene tres instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="307fd-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="307fd-187">**La instrucción DROP TABLE** elimina la tabla de Hive log4j en caso de que exista.</span><span class="sxs-lookup"><span data-stu-id="307fd-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="307fd-188">**La instrucción CREATE TABLE** crea una tabla externa de Hive log4j Hive que apunta a la ubicación del archivo de registro log4j.</span><span class="sxs-lookup"><span data-stu-id="307fd-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="307fd-189">**La ubicación del archivo de registro log4j**.</span><span class="sxs-lookup"><span data-stu-id="307fd-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="307fd-190">El delimitador de campo es ",".</span><span class="sxs-lookup"><span data-stu-id="307fd-190">The field delimiter is ",".</span></span> <span data-ttu-id="307fd-191">El delimitador de línea predeterminado es "\n".</span><span class="sxs-lookup"><span data-stu-id="307fd-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="307fd-192">Una tabla externa de Hive se usa para evitar que el archivo de datos se quite de la ubicación original, en el caso de que desee ejecutar el flujo de trabajo de Oozie varias veces.</span><span class="sxs-lookup"><span data-stu-id="307fd-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="307fd-193">**La instrucción INSERT OVERWRITE** cuenta las apariciones de cada tipo de nivel de registro desde la tabla de Hive log4j y guarda el resultado en una ubicación de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="307fd-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="307fd-194">Hay un problema conocido de la ruta de acceso de Hive.</span><span class="sxs-lookup"><span data-stu-id="307fd-194">There is a known Hive path issue.</span></span> <span data-ttu-id="307fd-195">Se producirá este problema cuando envíe un trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="307fd-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="307fd-196">Las instrucciones para corregir el problema pueden encontrarse en Wiki de TechNet: [Error de Hive de HDInsight: No se puede cambiar de nombre][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="307fd-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="307fd-197">**Para definir el archivo de script de HiveQL para que lo llame el flujo de trabajo**</span><span class="sxs-lookup"><span data-stu-id="307fd-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="307fd-198">Cree un archivo de texto con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="307fd-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="307fd-199">Existen tres variables que se usan en el script:</span><span class="sxs-lookup"><span data-stu-id="307fd-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="307fd-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="307fd-200">${hiveTableName}</span></span>
   * <span data-ttu-id="307fd-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="307fd-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="307fd-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="307fd-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="307fd-203">El archivo de definición de flujo de trabajo (workflow.xml en este tutorial) pasará estos valores al script de HiveQL en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="307fd-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="307fd-204">Guarde el archivo como **C:\Tutorials\UseOozie\useooziewf.hql** mediante la codificación ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="307fd-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="307fd-205">(Use el Bloc de notas si el editor de texto no proporciona esta opción.) Este archivo de script se implementará en el clúster de HDInsight más tarde en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="307fd-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="307fd-206">**Para definir un flujo de trabajo**</span><span class="sxs-lookup"><span data-stu-id="307fd-206">**To define a workflow**</span></span>

1. <span data-ttu-id="307fd-207">Cree un archivo de texto con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="307fd-207">Create a text file with the following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>

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

    <span data-ttu-id="307fd-208">Existen dos acciones definidas en el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="307fd-209">La acción de inicio es *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="307fd-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="307fd-210">Si la acción ejecuta *OK*, la acción siguiente es *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="307fd-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="307fd-211">RunHiveScript tiene distintas variables.</span><span class="sxs-lookup"><span data-stu-id="307fd-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="307fd-212">Pasará los valores cuando envíe el trabajo de Oozie desde la estación de trabajo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="307fd-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="307fd-213">Variables de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="307fd-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="307fd-214">Variables de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="307fd-214">Workflow variables</span></span></th><th><span data-ttu-id="307fd-215">Description</span><span class="sxs-lookup"><span data-stu-id="307fd-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="307fd-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="307fd-216">${jobTracker}</span></span></td><td><span data-ttu-id="307fd-217">Especifique la dirección URL del seguimiento de trabajo de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="307fd-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="307fd-218">Use <strong>jobtrackerhost:9010</strong> en la versión del clúster de HDInsight 3.0 y 2.0.</span><span class="sxs-lookup"><span data-stu-id="307fd-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="307fd-219">${nameNode}</span></span></td><td><span data-ttu-id="307fd-220">Especifique la dirección URL del nombre de nodo de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="307fd-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="307fd-221">Use el sistema de archivos predeterminado wasb:// dirección, por ejemplo, <i>wasb://&lt;nombreDelContenedor&gt;@&lt;nombreDeLaCuentaDeAlmacenamiento&gt;.blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="307fd-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="307fd-222">${queueName}</span></span></td><td><span data-ttu-id="307fd-223">Especifica el nombre de cola al que se enviará el trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="307fd-224">Use el <strong>valor predeterminado</strong>.</span><span class="sxs-lookup"><span data-stu-id="307fd-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="307fd-225">Variables de acción de Hive</span><span class="sxs-lookup"><span data-stu-id="307fd-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="307fd-226">Variable de acción de Hive</span><span class="sxs-lookup"><span data-stu-id="307fd-226">Hive action variable</span></span></th><th><span data-ttu-id="307fd-227">Description</span><span class="sxs-lookup"><span data-stu-id="307fd-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="307fd-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="307fd-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="307fd-229">El directorio de origen para el comando Create Table de Hive.</span><span class="sxs-lookup"><span data-stu-id="307fd-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="307fd-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="307fd-231">La carpeta de salida para la instrucción INSERT OVERWRITE.</span><span class="sxs-lookup"><span data-stu-id="307fd-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="307fd-232">${hiveTableName}</span></span></td><td><span data-ttu-id="307fd-233">El nombre de la tabla de Hive que hace referencia a los archivos de datos log4j.</span><span class="sxs-lookup"><span data-stu-id="307fd-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="307fd-234">Variables de acción de Sqoop</span><span class="sxs-lookup"><span data-stu-id="307fd-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="307fd-235">Variable de acción de Sqoop</span><span class="sxs-lookup"><span data-stu-id="307fd-235">Sqoop action variable</span></span></th><th><span data-ttu-id="307fd-236">Description</span><span class="sxs-lookup"><span data-stu-id="307fd-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="307fd-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="307fd-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="307fd-238">Cadena de conexión de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="307fd-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="307fd-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="307fd-240">La tabla de base de datos SQL de Azure donde se exportarán los datos.</span><span class="sxs-lookup"><span data-stu-id="307fd-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="307fd-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="307fd-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="307fd-242">La carpeta de salida para la instrucción INSERT OVERWRITE de Hive.</span><span class="sxs-lookup"><span data-stu-id="307fd-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="307fd-243">Se trata de la misma carpeta para la exportación de Sqoop (export-dir).</span><span class="sxs-lookup"><span data-stu-id="307fd-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="307fd-244">Para obtener más información sobre el flujo de trabajo de Oozie y el uso de acciones de flujo de trabajo, consulte la [documentación de Oozie 4.0 de Apache (en inglés)][apache-oozie-400] (para la versión del clúster de HDInsight 3.0) o la documentación de [Oozie 3.3.2 de Apache (en inglés)][apache-oozie-332] (para la versión del clúster de HDInsight 2.1).</span><span class="sxs-lookup"><span data-stu-id="307fd-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="307fd-245">Guarde el archivo como **C:\Tutorials\UseOozie\workflow.xml** mediante la codificación ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="307fd-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="307fd-246">(Use el Bloc de notas si el editor de texto no proporciona esta opción.)</span><span class="sxs-lookup"><span data-stu-id="307fd-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="307fd-247">**Para definir el coordinador**</span><span class="sxs-lookup"><span data-stu-id="307fd-247">**To define coordinator**</span></span>

1. <span data-ttu-id="307fd-248">Cree un archivo de texto con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="307fd-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="307fd-249">En el archivo de definición se usan cinco variables:</span><span class="sxs-lookup"><span data-stu-id="307fd-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="307fd-250">Variable</span><span class="sxs-lookup"><span data-stu-id="307fd-250">Variable</span></span> | <span data-ttu-id="307fd-251">Description</span><span class="sxs-lookup"><span data-stu-id="307fd-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="307fd-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="307fd-252">${coordFrequency}</span></span> |<span data-ttu-id="307fd-253">Hora de pausa del trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-253">Job pause time.</span></span> <span data-ttu-id="307fd-254">La frecuencia se expresa siempre en minutos.</span><span class="sxs-lookup"><span data-stu-id="307fd-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="307fd-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="307fd-255">${coordStart}</span></span> |<span data-ttu-id="307fd-256">Hora de inicio del trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-256">Job start time.</span></span> |
   | <span data-ttu-id="307fd-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="307fd-257">${coordEnd}</span></span> |<span data-ttu-id="307fd-258">Hora de finalización del trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-258">Job end time.</span></span> |
   | <span data-ttu-id="307fd-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="307fd-259">${coordTimezone}</span></span> |<span data-ttu-id="307fd-260">Oozie procesa los trabajos del coordinador en una zona horaria fija sin horario de verano (representado normalmente mediante UTC).</span><span class="sxs-lookup"><span data-stu-id="307fd-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="307fd-261">Esta zona horaria se conoce como la "zona de horaria de procesamiento de Oozie".</span><span class="sxs-lookup"><span data-stu-id="307fd-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="307fd-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="307fd-262">${wfPath}</span></span> |<span data-ttu-id="307fd-263">La ruta de acceso de workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="307fd-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="307fd-264">Si el nombre del archivo del flujo de trabajo no es el del archivo predeterminado (workflow.xml), debe especificarlo.</span><span class="sxs-lookup"><span data-stu-id="307fd-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="307fd-265">Guarde el archivo como **C:\Tutorials\UseOozie\coordinator.xml** mediante la codificación ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="307fd-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="307fd-266">(Use el Bloc de notas si el editor de texto no proporciona esta opción.)</span><span class="sxs-lookup"><span data-stu-id="307fd-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="307fd-267">Implementación del proyecto de Oozie y preparación del tutorial</span><span class="sxs-lookup"><span data-stu-id="307fd-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="307fd-268">Ejecutará el script de Azure PowerShell para realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="307fd-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="307fd-269">Copie el script de HiveQL (useoozie.hql) en Azure Blob Storage, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="307fd-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="307fd-270">Copie workflow.xml en wasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="307fd-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="307fd-271">Copie coordinator.xml en wasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="307fd-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="307fd-272">Copie el archivo de datos (/example/data/sample.log) en wasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="307fd-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="307fd-273">Cree una tabla de base de datos SQL de Azure para el almacenamiento de datos de exportación de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="307fd-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="307fd-274">El nombre de la tabla es *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="307fd-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="307fd-275">**Descripción del almacenamiento de HDInsight**</span><span class="sxs-lookup"><span data-stu-id="307fd-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="307fd-276">HDInsight usa el almacenamiento de blobs de Azure para almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="307fd-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="307fd-277">wasb:// es la implementación de Microsoft del sistema de archivos distribuido de Hadoop (HDFS) en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="307fd-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="307fd-278">Para obtener más información, consulte [Uso de Azure Blob Storage con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="307fd-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="307fd-279">Cuando se aprovisiona un clúster de HDInsight, se designan una cuenta de almacenamiento de blobs de Azure y un contenedor específico de dicha cuenta como el sistema de archivos predeterminado, de la misma forma que en HDFS.</span><span class="sxs-lookup"><span data-stu-id="307fd-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="307fd-280">Además de esta cuenta de almacenamiento, puede agregar más cuentas de almacenamiento desde la misma suscripción de Azure o desde otras diferentes durante el proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="307fd-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="307fd-281">Para obtener instrucciones sobre cómo agregar más cuentas de almacenamiento, consulte [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="307fd-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="307fd-282">Para simplificar el script de Azure PowerShell que se usa en este tutorial, todos los archivos se almacenan en el contenedor del sistema de archivos predeterminado, que se encuentra en */tutorials/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="307fd-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="307fd-283">De forma predeterminada, este contenedor tiene el mismo nombre que el del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="307fd-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="307fd-284">La sintaxis es:</span><span class="sxs-lookup"><span data-stu-id="307fd-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="307fd-285">Solo se admite la sintaxis *wasb://* con el clúster de HDInsight, versión 3.0.</span><span class="sxs-lookup"><span data-stu-id="307fd-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="307fd-286">La antigua sintaxis *asv://* es compatible con los clústeres de HDInsight 2.1 y 1.6, pero no es compatible con los clústeres de HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="307fd-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="307fd-287">La ruta de acceso wasb:// es una ruta de acceso virtual.</span><span class="sxs-lookup"><span data-stu-id="307fd-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="307fd-288">Para obtener más información, consulte [Uso de Azure Blob Storage con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="307fd-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="307fd-289">Para acceder a un archivo almacenado en el contenedor del sistema de archivos predeterminado desde HDInsight se puede usar cualquiera de los URI siguientes (uso workflow.xml como ejemplo):</span><span class="sxs-lookup"><span data-stu-id="307fd-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="307fd-290">Si desea obtener acceso al archivo directamente desde la cuenta de almacenamiento, el nombre de blob del archivo es:</span><span class="sxs-lookup"><span data-stu-id="307fd-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="307fd-291">**Descripción de las tablas internas y externas de Hive**</span><span class="sxs-lookup"><span data-stu-id="307fd-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="307fd-292">Existen determinados aspectos que debe conocer en relación con las tablas internas y externas de Hive:</span><span class="sxs-lookup"><span data-stu-id="307fd-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="307fd-293">El comando CREATE TABLE crea una tabla interna, también conocida como tabla administrada.</span><span class="sxs-lookup"><span data-stu-id="307fd-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="307fd-294">El archivo de datos debe ubicarse en el contenedor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="307fd-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="307fd-295">El comando CREATE TABLE mueve el archivo de datos a la carpeta /hive/warehouse/<TableName> en el contenedor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="307fd-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="307fd-296">El comando CREATE EXTERNAL TABLE crea una tabla externa.</span><span class="sxs-lookup"><span data-stu-id="307fd-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="307fd-297">El archivo de datos puede estar ubicado fuera del contenedor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="307fd-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="307fd-298">El comando CREATE EXTERNAL TABLE no mueve el archivo de datos.</span><span class="sxs-lookup"><span data-stu-id="307fd-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="307fd-299">El comando CREATE EXTERNAL TABLE no permite a las subcarpetas en la carpeta especificada en la cláusula LOCATION.</span><span class="sxs-lookup"><span data-stu-id="307fd-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="307fd-300">Este es el motivo por el que el tutorial hace una copia del archivo sample.log.</span><span class="sxs-lookup"><span data-stu-id="307fd-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="307fd-301">Para obtener más información, consulte [HDInsight: introducción de tablas internas y externas de Hive][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="307fd-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="307fd-302">**Para preparar el tutorial**</span><span class="sxs-lookup"><span data-stu-id="307fd-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="307fd-303">Abra Windows PowerShell ISE (en la pantalla Inicio de Windows 8, escriba **PowerShell_ISE** y luego haga clic en **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="307fd-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="307fd-304">Consulte [Iniciar Windows PowerShell en Windows 8 y Windows][powershell-start] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="307fd-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="307fd-305">En el panel inferior, ejecute el comando siguiente para conectarse a su suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="307fd-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="307fd-306">Se le pedirá que escriba las credenciales de la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="307fd-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="307fd-307">Este método de agregar una conexión de suscripción expira y, transcurridas 12 horas, tendrá que volver a ejecutar el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="307fd-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="307fd-308">Si tiene varias suscripciones de Azure y no desea usar la predeterminada, use el cmdlet <strong>Select-AzureSubscription</strong> para seleccionar una suscripción.</span><span class="sxs-lookup"><span data-stu-id="307fd-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="307fd-309">Copie el siguiente script en el panel de scripts y, a continuación, establezca las seis primeras variables:</span><span class="sxs-lookup"><span data-stu-id="307fd-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

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

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="307fd-310">Para ver más descripciones de las variables, consulte la sección [Requisitos previos](#prerequisites) de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="307fd-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="307fd-311">Agregue lo siguiente al script en el panel de scripts:</span><span class="sxs-lookup"><span data-stu-id="307fd-311">Append the following to the script in the script pane:</span></span>

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
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
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

        #Create the log4jLogsCount table
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

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="307fd-312">Haga clic en **Ejecutar script** o presione **F5** para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="307fd-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="307fd-313">La salida debe ser similar a:</span><span class="sxs-lookup"><span data-stu-id="307fd-313">The output will be similar to:</span></span>

    ![Resultado de preparación del tutorial][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="307fd-315">Ejecución del proyecto de Oozie</span><span class="sxs-lookup"><span data-stu-id="307fd-315">Run the Oozie project</span></span>
<span data-ttu-id="307fd-316">Azure PowerShell no proporciona actualmente cmdlets para la definición de trabajos de Oozie.</span><span class="sxs-lookup"><span data-stu-id="307fd-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="307fd-317">Puede usar el cmdlet **Invoke-RestMethod** para invocar los servicios web de Oozie.</span><span class="sxs-lookup"><span data-stu-id="307fd-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="307fd-318">La API de servicios web de Oozie es una API HTTP REST JSON.</span><span class="sxs-lookup"><span data-stu-id="307fd-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="307fd-319">Para obtener más información sobre la API de servicios web de Oozie, consulte la [documentación de Oozie 4.0 de Apache (en inglés)][apache-oozie-400] (para la versión del clúster de HDInsight 3.0) o la [documentación de Oozie 3.3.2 de Apache (en inglés)][apache-oozie-332] (para la versión del clúster de HDInsight 2.1).</span><span class="sxs-lookup"><span data-stu-id="307fd-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="307fd-320">**Para enviar un trabajo de Oozie**</span><span class="sxs-lookup"><span data-stu-id="307fd-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="307fd-321">Abra Windows PowerShell ISE (en la pantalla Inicio de Windows 8, escriba **PowerShell_ISE** y luego haga clic en **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="307fd-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="307fd-322">Consulte [Iniciar Windows PowerShell en Windows 8 y Windows][powershell-start] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="307fd-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="307fd-323">Copie el siguiente script en el panel de scripts y, a continuación, configure las catorce primeras variables (pero omita **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="307fd-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
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

    <span data-ttu-id="307fd-324">Para ver más descripciones de las variables, consulte la sección [Requisitos previos](#prerequisites) de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="307fd-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="307fd-325">$coordstart y $coordend son las horas de inicio y fin del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="307fd-326">Para saber la hora UTC y GMT, busque "hora utc" en bing.com. $coordFrequency es la frecuencia minutos con la que desea ejecutar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="307fd-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="307fd-327">Agregue lo siguiente al script.</span><span class="sxs-lookup"><span data-stu-id="307fd-327">Append the following to the script.</span></span> <span data-ttu-id="307fd-328">Esta parte define la carga de Oozie:</span><span class="sxs-lookup"><span data-stu-id="307fd-328">This part defines the Oozie payload:</span></span>

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
   > <span data-ttu-id="307fd-329">La principal diferencia que se aprecia al comparar con el archivo de carga de envío de flujos de trabajo es la variable **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="307fd-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="307fd-330">Al enviar una tarea de flujo de trabajo, se usa **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="307fd-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="307fd-331">Agregue lo siguiente al script.</span><span class="sxs-lookup"><span data-stu-id="307fd-331">Append the following to the script.</span></span> <span data-ttu-id="307fd-332">En esta parte se comprueba el estado del servicio web de Oozie:</span><span class="sxs-lookup"><span data-stu-id="307fd-332">This part checks the Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="307fd-333">Agregue lo siguiente al script.</span><span class="sxs-lookup"><span data-stu-id="307fd-333">Append the following to the script.</span></span> <span data-ttu-id="307fd-334">En esta parte se crea un trabajo de Oozie:</span><span class="sxs-lookup"><span data-stu-id="307fd-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="307fd-335">Al enviar una tarea del flujo de trabajo, debe realizar otra llamada de servicio web para iniciar la tarea una vez que esta se haya creado.</span><span class="sxs-lookup"><span data-stu-id="307fd-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="307fd-336">En este caso, el trabajo de coordinador se desencadena por tiempo.</span><span class="sxs-lookup"><span data-stu-id="307fd-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="307fd-337">El trabajo se iniciará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="307fd-337">The job will start automatically.</span></span>

6. <span data-ttu-id="307fd-338">Agregue lo siguiente al script.</span><span class="sxs-lookup"><span data-stu-id="307fd-338">Append the following to the script.</span></span> <span data-ttu-id="307fd-339">En esta parte se comprueba el estado del trabajo de Oozie:</span><span class="sxs-lookup"><span data-stu-id="307fd-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
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

7. <span data-ttu-id="307fd-340">(Opcional) Agregue lo siguiente al script.</span><span class="sxs-lookup"><span data-stu-id="307fd-340">(Optional) Append the following to the script.</span></span>

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
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="307fd-341">Agregue lo siguiente al script:</span><span class="sxs-lookup"><span data-stu-id="307fd-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="307fd-342">Elimine el signo # si desea ejecutar las funciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="307fd-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="307fd-343">Si el clúster de HDinsight es la versión 2.1, reemplace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" por "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="307fd-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="307fd-344">La versión del clúster de HDInsight 2.1 no es compatible con la versión 2 de los servicios web.</span><span class="sxs-lookup"><span data-stu-id="307fd-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="307fd-345">Haga clic en **Ejecutar script** o presione **F5** para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="307fd-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="307fd-346">La salida debe ser similar a:</span><span class="sxs-lookup"><span data-stu-id="307fd-346">The output will be similar to:</span></span>

     ![Resultado del flujo de trabajo de ejecución del tutorial][img-runworkflow-output]
11. <span data-ttu-id="307fd-348">Conéctese a la Base de datos SQL para ver los datos exportados.</span><span class="sxs-lookup"><span data-stu-id="307fd-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="307fd-349">**Para comprobar el registro de errores del trabajo**</span><span class="sxs-lookup"><span data-stu-id="307fd-349">**To check the job error log**</span></span>

<span data-ttu-id="307fd-350">Para solucionar los problemas de un flujo de trabajo, puede encontrar el archivo de registro de Oozie en C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log en el nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="307fd-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="307fd-351">Para obtener más información sobre RDP, consulte [Administración de clústeres de Hadoop en HDInsight mediante Azure Portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="307fd-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="307fd-352">**Para volver a ejecutar el tutorial**</span><span class="sxs-lookup"><span data-stu-id="307fd-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="307fd-353">Para volver a ejecutar el flujo de trabajo, debe realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="307fd-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="307fd-354">Elimine el archivo de salida del script de Hive.</span><span class="sxs-lookup"><span data-stu-id="307fd-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="307fd-355">Eliminar los datos de la tabla log4jLogsCount.</span><span class="sxs-lookup"><span data-stu-id="307fd-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="307fd-356">Aquí tiene un script de Windows PowerShell de ejemplo que puede usar:</span><span class="sxs-lookup"><span data-stu-id="307fd-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="307fd-357">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="307fd-357">Next steps</span></span>
<span data-ttu-id="307fd-358">En este tutorial ha aprendido a definir un flujo de trabajo de Oozie y un coordinador de Oozie, y a ejecutar un trabajo de coordinador de Oozie mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="307fd-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="307fd-359">Para obtener más información, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="307fd-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="307fd-360">[Introducción a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="307fd-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="307fd-361">[Uso de Azure Blob Storage con HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="307fd-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="307fd-362">[Administración de HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="307fd-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="307fd-363">[Carga de datos en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="307fd-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="307fd-364">[Uso de Sqoop con HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="307fd-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="307fd-365">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="307fd-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="307fd-366">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="307fd-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="307fd-367">[Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="307fd-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
