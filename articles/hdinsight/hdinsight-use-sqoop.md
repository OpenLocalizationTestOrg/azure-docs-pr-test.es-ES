---
title: "Ejecución de trabajos de Apache Sqoop con Azure HDInsight (Hadoop) | Microsoft Docs"
description: "Aprenda a utilizar Azure PowerShell desde una estación de trabajo para ejecutar la importación y exportación en Sqoop entre un clúster de Hadoop y una base de datos SQL de Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="cf0d3-103">Uso de Sqoop con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf0d3-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="cf0d3-104">Aprenda a utilizar Sqoop en HDInsight  para importar y exportar entre un clúster de HDInsight y una base de datos de SQL Server o la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="cf0d3-105">A pesar de que Hadoop es una opción natural para procesar datos no estructurados y datos semiestructurados, como registros y archivos, es posible que también sea necesario procesar datos estructurados almacenados en bases de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="cf0d3-106">[Sqoop][sqoop-user-guide-1.4.4] es una herramienta diseñada para transferir datos entre clústeres de Hadoop y las bases de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="cf0d3-107">Puede usarla para importar datos desde un sistema de administración de bases de datos relacionales (RDBMS) como SQL Server, MySQL u Oracle en el sistema de archivos distribuidos Hadoop (HDFS), transformar los datos de Hadoop con MapReduce o Hive y, a continuación, exportar los datos en un RDBMS.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="cf0d3-108">En este tutorial, usará una base de datos de SQL Server como base de datos relacional.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="cf0d3-109">Para ver las versiones de Sqoop compatibles con los clústeres de HDInsight, consulte [Novedades en las versiones de clústeres proporcionadas por HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="cf0d3-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="cf0d3-110">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cf0d3-110">Understand the scenario</span></span>

<span data-ttu-id="cf0d3-111">El clúster de HDInsight incluye algunos datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="cf0d3-112">Utilice los dos ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-112">You use the following two samples:</span></span>

* <span data-ttu-id="cf0d3-113">Un archivo registro log4j, ubicado en */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="cf0d3-114">Los registros siguientes se extraen del archivo:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="cf0d3-115">Una tabla de Hive denominada *hivesampletable* que hace referencia al archivo de datos ubicado en */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="cf0d3-116">La tabla contiene algunos datos del dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="cf0d3-117">Campo</span><span class="sxs-lookup"><span data-stu-id="cf0d3-117">Field</span></span> | <span data-ttu-id="cf0d3-118">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="cf0d3-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="cf0d3-119">clientid</span><span class="sxs-lookup"><span data-stu-id="cf0d3-119">clientid</span></span> |<span data-ttu-id="cf0d3-120">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-120">string</span></span> |
  | <span data-ttu-id="cf0d3-121">querytime</span><span class="sxs-lookup"><span data-stu-id="cf0d3-121">querytime</span></span> |<span data-ttu-id="cf0d3-122">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-122">string</span></span> |
  | <span data-ttu-id="cf0d3-123">market</span><span class="sxs-lookup"><span data-stu-id="cf0d3-123">market</span></span> |<span data-ttu-id="cf0d3-124">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-124">string</span></span> |
  | <span data-ttu-id="cf0d3-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="cf0d3-125">deviceplatform</span></span> |<span data-ttu-id="cf0d3-126">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-126">string</span></span> |
  | <span data-ttu-id="cf0d3-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="cf0d3-127">devicemake</span></span> |<span data-ttu-id="cf0d3-128">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-128">string</span></span> |
  | <span data-ttu-id="cf0d3-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="cf0d3-129">devicemodel</span></span> |<span data-ttu-id="cf0d3-130">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-130">string</span></span> |
  | <span data-ttu-id="cf0d3-131">state</span><span class="sxs-lookup"><span data-stu-id="cf0d3-131">state</span></span> |<span data-ttu-id="cf0d3-132">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-132">string</span></span> |
  | <span data-ttu-id="cf0d3-133">country</span><span class="sxs-lookup"><span data-stu-id="cf0d3-133">country</span></span> |<span data-ttu-id="cf0d3-134">string</span><span class="sxs-lookup"><span data-stu-id="cf0d3-134">string</span></span> |
  | <span data-ttu-id="cf0d3-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="cf0d3-135">querydwelltime</span></span> |<span data-ttu-id="cf0d3-136">double</span><span class="sxs-lookup"><span data-stu-id="cf0d3-136">double</span></span> |
  | <span data-ttu-id="cf0d3-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="cf0d3-137">sessionid</span></span> |<span data-ttu-id="cf0d3-138">bigint</span><span class="sxs-lookup"><span data-stu-id="cf0d3-138">bigint</span></span> |
  | <span data-ttu-id="cf0d3-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="cf0d3-139">sessionpagevieworder</span></span> |<span data-ttu-id="cf0d3-140">bigint</span><span class="sxs-lookup"><span data-stu-id="cf0d3-140">bigint</span></span> |

<span data-ttu-id="cf0d3-141">En primer lugar, exporte tanto *sample.log* como *hivesampletable* a la base de datos de Azure SQL o a SQL Server y luego importe la tabla que contiene los datos del dispositivo móvil de nuevo a HDInsight con la ruta de acceso siguiente:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="cf0d3-142">Creación del clúster y la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cf0d3-142">Create cluster and SQL database</span></span>
<span data-ttu-id="cf0d3-143">En esta sección se muestra cómo crear un clúster, una instancia de SQL Database y los esquemas de SQL Database para ejecutar el tutorial con Azure Portal y una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="cf0d3-144">La plantilla se puede encontrar en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="cf0d3-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="cf0d3-145">La plantilla de Resource Manager llama a un paquete de bacpac para que implemente los esquemas de tabla en SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="cf0d3-146">El paquete de bacpac se encuentra en un contenedor de blobs público, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="cf0d3-147">Si desea usar un contenedor privado para los archivos bacpac, utilice los siguientes valores en la plantilla:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="cf0d3-148">Si prefiere usar Azure PowerShell para crear el clúster y la base de datos SQL; consulte el [Apéndice A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="cf0d3-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="cf0d3-149">Haga clic en la imagen siguiente para abrir una plantilla de Resource Manager en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="cf0d3-150">Especifique las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-150">Enter the following properties:</span></span>

    - <span data-ttu-id="cf0d3-151">**Suscripción**: escriba su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="cf0d3-152">**Grupo de recursos**: cree un nuevo grupo de recursos de Azure o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="cf0d3-153">Un grupo de recursos tiene fines administrativos.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="cf0d3-154">Es un contenedor de objetos.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-154">It is a container for objects.</span></span>
    - <span data-ttu-id="cf0d3-155">**Ubicación**: seleccione una región.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="cf0d3-156">**Nombre del clúster**: escriba el nombre del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="cf0d3-157">**Nombre de inicio de sesión y contraseña de clúster**: el nombre de inicio de sesión predeterminado es admin.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="cf0d3-158">**Nombre de usuario y contraseña de SSH**.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="cf0d3-159">**Nombre y contraseña de inicio de sesión en el servidor de la base de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="cf0d3-160">**_artifacts Location** (Ubicación de _artefactos): use el valor predeterminado a no ser que quiera usar su propio archivo backpac en una ubicación diferente.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="cf0d3-161">**_artifacts Location Sas Token** (Token Sas de ubicación de _artefactos): deje este valor en blanco.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="cf0d3-162">**Bacpac File Name** (Nombre de archivo bacpac): use el valor predeterminado a no ser que quiera usar su propio archivo backpac.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="cf0d3-163">Los siguientes valores están codificados de forma rígida en la sección de variables:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="cf0d3-164">Nombre de la cuenta de almacenamiento predeterminada</span><span class="sxs-lookup"><span data-stu-id="cf0d3-164">Default storage account name</span></span> | <span data-ttu-id="cf0d3-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="cf0d3-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="cf0d3-166">Nombre del servidor de base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="cf0d3-166">Azure SQL database server name</span></span> |<span data-ttu-id="cf0d3-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="cf0d3-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="cf0d3-168">Nombre de la base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="cf0d3-168">Azure SQL database name</span></span> |<span data-ttu-id="cf0d3-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="cf0d3-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="cf0d3-170">Escriba estos valores.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-170">Please write down these values.</span></span>  <span data-ttu-id="cf0d3-171">Los necesitará más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="cf0d3-172">3. Haga clic en **Aceptar** para guardar los parámetros.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="cf0d3-173">4. En la hoja **Implementación personalizada**, haga clic en el cuadro desplegable **Grupo de recursos** y, después, en **Nuevo** para crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="cf0d3-174">El grupo de recursos es un contenedor que agrupa al clúster, a la cuenta de almacenamiento dependiente y a otros recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="cf0d3-175">5. Haga clic en **Términos legales** y en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="cf0d3-176">6. Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-176">6.Click **Create**.</span></span> <span data-ttu-id="cf0d3-177">Verá un icono nuevo llamado Envío de implementación para la implementación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="cf0d3-178">Tarda aproximadamente 20 minutos en crear un clúster y la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="cf0d3-179">Si opta por usar la base de datos SQL de Azure existente o Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="cf0d3-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="cf0d3-180">**Base de datos SQL de Azure**: debe configurar una regla de firewall para que el servidor de base de datos SQL de Azure permita el acceso desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="cf0d3-181">Para obtener instrucciones sobre cómo crear una base de datos SQL de Azure y configurar el firewall, consulte [Introducción al uso de Azure SQL Database][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="cf0d3-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="cf0d3-182">De forma predeterminada, una base de datos SQL de Azure permite realizar conexiones desde servicios de Azure, como HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="cf0d3-183">Si la configuración del firewall está deshabilitada, debe habilitarla en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="cf0d3-184">Para obtener instrucciones sobre la creación de una base de datos de Azure SQL Database y la configuración de las reglas de firewall, consulte [Creación y configuración de SQL Database][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="cf0d3-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="cf0d3-185">**SQL Server**: si el clúster de HDInsight se encuentra en la misma red virtual de Azure que un SQL Server, puede seguir los pasos indicados en este artículo para importar y exportar datos a una base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cf0d3-186">HDInsight solo admite redes virtuales basadas en la ubicación y actualmente no funciona con redes virtuales basadas en grupos de afinidad.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="cf0d3-187">Para crear y configurar una red virtual, consulte [Creación de una red virtual mediante Azure Portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="cf0d3-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="cf0d3-188">Cuando use SQL Server en el centro de datos, debe configurar la red virtual como de *sitio a sitio* o de *punto a sitio*.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="cf0d3-189">En el caso de las redes virtuales de **punto a sitio**, SQL Server debe ejecutarse en la aplicación de configuración de clientes VPN, que se encuentra disponible en el **Panel** de la configuración de red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="cf0d3-190">Si usa SQL Server en una máquina virtual de Azure, se puede usar cualquier configuración de red virtual si la máquina virtual que hospeda SQL Server es miembro de la misma red virtual que HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="cf0d3-191">Para crear un clúster de HDInsight en una red virtual, consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="cf0d3-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cf0d3-192">SQL Server también debe permitir la autenticación.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="cf0d3-193">Debe usar un inicio de sesión de SQL Server para completar los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="cf0d3-194">Ejecución de trabajos de Sqoop</span><span class="sxs-lookup"><span data-stu-id="cf0d3-194">Run Sqoop jobs</span></span>
<span data-ttu-id="cf0d3-195">HDInsight puede ejecutar trabajos de Sqoop mediante una variedad de métodos.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="cf0d3-196">Use la tabla siguiente para decidir cuál es el método adecuado para usted luego siga el vínculo para ver un tutorial.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="cf0d3-197">**Utilícelo** si desea...</span><span class="sxs-lookup"><span data-stu-id="cf0d3-197">**Use this** if you want...</span></span> | <span data-ttu-id="cf0d3-198">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="cf0d3-198">...an **interactive** shell</span></span> | <span data-ttu-id="cf0d3-199">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="cf0d3-199">...**batch** processing</span></span> | <span data-ttu-id="cf0d3-200">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="cf0d3-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="cf0d3-201">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="cf0d3-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="cf0d3-202">SSH</span><span class="sxs-lookup"><span data-stu-id="cf0d3-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="cf0d3-203">✔</span><span class="sxs-lookup"><span data-stu-id="cf0d3-203">✔</span></span> |<span data-ttu-id="cf0d3-204">✔</span><span class="sxs-lookup"><span data-stu-id="cf0d3-204">✔</span></span> |<span data-ttu-id="cf0d3-205">Linux</span><span class="sxs-lookup"><span data-stu-id="cf0d3-205">Linux</span></span> |<span data-ttu-id="cf0d3-206">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="cf0d3-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cf0d3-207">.NET SDK para Hadoop</span><span class="sxs-lookup"><span data-stu-id="cf0d3-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="cf0d3-208">✔</span><span class="sxs-lookup"><span data-stu-id="cf0d3-208">✔</span></span> |<span data-ttu-id="cf0d3-209">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cf0d3-209">Linux or Windows</span></span> |<span data-ttu-id="cf0d3-210">Windows (por ahora)</span><span class="sxs-lookup"><span data-stu-id="cf0d3-210">Windows (for now)</span></span> |
| [<span data-ttu-id="cf0d3-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf0d3-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="cf0d3-212">✔</span><span class="sxs-lookup"><span data-stu-id="cf0d3-212">✔</span></span> |<span data-ttu-id="cf0d3-213">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="cf0d3-213">Linux or Windows</span></span> |<span data-ttu-id="cf0d3-214">Windows</span><span class="sxs-lookup"><span data-stu-id="cf0d3-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="cf0d3-215">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="cf0d3-215">Limitations</span></span>
* <span data-ttu-id="cf0d3-216">Exportación masiva: con HDInsight basado en Linux, el conector Sqoop que se utiliza para exportar datos a Microsoft SQL Server o Base de datos SQL Azure no es compatible actualmente con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="cf0d3-217">Procesamiento por lotes: con HDInsight basado en Linux, cuando se usa `-batch` al realizar inserciones, Sqoop realiza varias inserciones en lugar de procesar por lotes las operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf0d3-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf0d3-218">Next steps</span></span>
<span data-ttu-id="cf0d3-219">Ahora ya ha aprendido a usar Sqoop.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="cf0d3-220">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-220">To learn more, see:</span></span>

* [<span data-ttu-id="cf0d3-221">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf0d3-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cf0d3-222">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf0d3-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="cf0d3-223">[Uso de Oozie con HDInsight][hdinsight-use-oozie]: use la acción de Sqoop en un flujo de trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="cf0d3-224">[Análisis de la información de retraso de vuelos con HDInsight][hdinsight-analyze-flight-data]: use Hive para analizar la información de retraso de los vuelos y luego use Sqoop para exportar los datos a una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="cf0d3-225">[Carga de datos en HDInsight][hdinsight-upload-data]: busque otros métodos para cargar datos en HDInsight o en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="cf0d3-226">Apéndice A - un ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf0d3-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="cf0d3-227">El ejemplo de PowerShell lleva a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="cf0d3-228">Conéctese a Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-228">Connect to Azure.</span></span>
2. <span data-ttu-id="cf0d3-229">Cree un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-229">Create an Azure resource group.</span></span> <span data-ttu-id="cf0d3-230">Para obtener más información, consulte [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="cf0d3-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="cf0d3-231">Cree un servidor de Base de datos SQL de Azure, una base de datos SQL de Azure y dos tablas.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="cf0d3-232">Si usa SQL Server en su lugar, use las siguientes instrucciones para crear las tablas:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="cf0d3-233">La manera más sencilla de examinar la base de datos y las tablas es usar Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="cf0d3-234">El servidor de bases de datos y la base de datos se pueden examinar con el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="cf0d3-235">Cree un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="cf0d3-236">Para examinar el clúster, puede usar el portal de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="cf0d3-237">Preprocese el archivo de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="cf0d3-238">En este tutorial, se exporta un archivo de registro log4j (un archivo delimitado) y una tabla de Hive a una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="cf0d3-239">El archivo delimitado se llama */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="cf0d3-240">Anteriormente en este tutorial, se han mostrado algunos ejemplos de registros log4j.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="cf0d3-241">El archivo de registro tiene algunas líneas vacías y otras similares a las siguientes:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="cf0d3-242">Esto es válido para otros ejemplos que usan estos datos, pero debemos quitar estas excepciones para poder importarlos a la base de datos SQL de Azure o a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="cf0d3-243">La exportación de Sqoop produce un error si hay una cadena vacía o una línea con menos elementos inferior al número de campos definido en la tabla de base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="cf0d3-244">La tabla log4jlogs tiene 7 campos de tipo cadena.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="cf0d3-245">Este procedimiento crea un archivo nuevo en el clúster: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="cf0d3-246">Para examinar el archivo de datos modificado, puede usar el portal de Azure, una herramienta del explorador de almacenamiento de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="cf0d3-247">[Introducción a HDInsight][hdinsight-get-started] incluye código de ejemplo para usar Azure PowerShell para descargar un archivo y mostrar su contenido.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="cf0d3-248">Exportar un archivo de datos a la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="cf0d3-249">El archivo de origen es tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="cf0d3-250">La tabla donde se exportan los datos se denomina log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cf0d3-251">Aparte de la información de la cadena de conexión, los pasos indicados en esta sección deben funcionar para una base de datos SQL de Azure o para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="cf0d3-252">Estos pasos se probaron con la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="cf0d3-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="cf0d3-253">**Configuración de punto a sitio de la red virtual de Azure**: red virtual que conecta el clúster de HDInsight a SQL Server en un centro privado de datos.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="cf0d3-254">Para obtener más información, consulte [Configuración de una VPN de punto a sitio en el Portal de administración](../vpn-gateway/vpn-gateway-point-to-site-create.md) .</span><span class="sxs-lookup"><span data-stu-id="cf0d3-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="cf0d3-255">**HDInsight de Azure 3.1:**consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener más información sobre cómo crear un clúster en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="cf0d3-256">**SQL Server 2014**: configurado para permitir la autenticación y la ejecución del paquete de configuración de clientes VPN para conectarse de forma segura a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="cf0d3-257">Exportar una tabla de Hive a la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="cf0d3-258">Importe la tabla mobiledata al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="cf0d3-259">Para examinar el archivo de datos modificado, puede usar el portal de Azure, una herramienta del explorador de almacenamiento de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="cf0d3-260">[Introducción a HDInsight][hdinsight-get-started] incluye código de ejemplo para usar Azure PowerShell para descargar un archivo y mostrar su contenido.</span><span class="sxs-lookup"><span data-stu-id="cf0d3-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="cf0d3-261">El ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf0d3-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
