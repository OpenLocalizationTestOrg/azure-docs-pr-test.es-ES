---
title: los trabajos de aaaRun Sqoop de Apache con Azure HDInsight (Hadoop) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse PowerShell de Azure desde un toorun de estación de trabajo Sqoop importar y exportar entre un clúster de Hadoop y una base de datos de SQL Azure."
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
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="a245e-103">Uso de Sqoop con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="a245e-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="a245e-104">Obtenga información acerca de cómo toouse Sqoop en HDInsight tooimport y exportación entre el clúster de HDInsight y la base de datos SQL de Azure o la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a245e-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="a245e-105">Aunque Hadoop es una opción natural para el procesamiento de datos no estructurados y semiestructurados, como registros y los archivos, también puede haber una necesidad de datos tooprocess estructurado que se almacenan en bases de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="a245e-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="a245e-106">[Sqoop] [ sqoop-user-guide-1.4.4] es una herramienta diseñada tootransfer datos entre clústeres de Hadoop y bases de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="a245e-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="a245e-107">Puede usar lo tooimport datos desde un sistema de administración de bases de datos relacionales (RDBMS), como SQL Server, MySQL u Oracle en el sistema de archivos distribuido de Hadoop de hello (HDFS), transforme datos hello Hadoop MapReduce o subárbol y, a continuación, exportar datos de hello en un RDBMS.</span><span class="sxs-lookup"><span data-stu-id="a245e-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="a245e-108">En este tutorial, usará una base de datos de SQL Server como base de datos relacional.</span><span class="sxs-lookup"><span data-stu-id="a245e-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="a245e-109">¿Para las versiones de Sqoop que son compatibles con clústeres de HDInsight, consulte [cuáles son las novedades en las versiones de clúster Hola proporcionadas por HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="a245e-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="a245e-110">Comprender el escenario de Hola</span><span class="sxs-lookup"><span data-stu-id="a245e-110">Understand hello scenario</span></span>

<span data-ttu-id="a245e-111">El clúster de HDInsight incluye algunos datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a245e-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="a245e-112">Use Hola siguiendo dos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="a245e-112">You use hello following two samples:</span></span>

* <span data-ttu-id="a245e-113">Un archivo registro log4j, ubicado en */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="a245e-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="a245e-114">Hola después de registros extraído de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="a245e-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="a245e-115">Una tabla de Hive denominada *hivesampletable*, que las referencias Hola ubicado en el archivo de datos */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="a245e-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="a245e-116">Hola tabla contiene algunos datos de dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="a245e-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="a245e-117">Campo</span><span class="sxs-lookup"><span data-stu-id="a245e-117">Field</span></span> | <span data-ttu-id="a245e-118">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="a245e-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="a245e-119">clientid</span><span class="sxs-lookup"><span data-stu-id="a245e-119">clientid</span></span> |<span data-ttu-id="a245e-120">string</span><span class="sxs-lookup"><span data-stu-id="a245e-120">string</span></span> |
  | <span data-ttu-id="a245e-121">querytime</span><span class="sxs-lookup"><span data-stu-id="a245e-121">querytime</span></span> |<span data-ttu-id="a245e-122">string</span><span class="sxs-lookup"><span data-stu-id="a245e-122">string</span></span> |
  | <span data-ttu-id="a245e-123">market</span><span class="sxs-lookup"><span data-stu-id="a245e-123">market</span></span> |<span data-ttu-id="a245e-124">string</span><span class="sxs-lookup"><span data-stu-id="a245e-124">string</span></span> |
  | <span data-ttu-id="a245e-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="a245e-125">deviceplatform</span></span> |<span data-ttu-id="a245e-126">string</span><span class="sxs-lookup"><span data-stu-id="a245e-126">string</span></span> |
  | <span data-ttu-id="a245e-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="a245e-127">devicemake</span></span> |<span data-ttu-id="a245e-128">string</span><span class="sxs-lookup"><span data-stu-id="a245e-128">string</span></span> |
  | <span data-ttu-id="a245e-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="a245e-129">devicemodel</span></span> |<span data-ttu-id="a245e-130">string</span><span class="sxs-lookup"><span data-stu-id="a245e-130">string</span></span> |
  | <span data-ttu-id="a245e-131">state</span><span class="sxs-lookup"><span data-stu-id="a245e-131">state</span></span> |<span data-ttu-id="a245e-132">string</span><span class="sxs-lookup"><span data-stu-id="a245e-132">string</span></span> |
  | <span data-ttu-id="a245e-133">country</span><span class="sxs-lookup"><span data-stu-id="a245e-133">country</span></span> |<span data-ttu-id="a245e-134">string</span><span class="sxs-lookup"><span data-stu-id="a245e-134">string</span></span> |
  | <span data-ttu-id="a245e-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="a245e-135">querydwelltime</span></span> |<span data-ttu-id="a245e-136">double</span><span class="sxs-lookup"><span data-stu-id="a245e-136">double</span></span> |
  | <span data-ttu-id="a245e-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="a245e-137">sessionid</span></span> |<span data-ttu-id="a245e-138">bigint</span><span class="sxs-lookup"><span data-stu-id="a245e-138">bigint</span></span> |
  | <span data-ttu-id="a245e-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="a245e-139">sessionpagevieworder</span></span> |<span data-ttu-id="a245e-140">bigint</span><span class="sxs-lookup"><span data-stu-id="a245e-140">bigint</span></span> |

<span data-ttu-id="a245e-141">En primer lugar, exportar *sample.log* y *hivesampletable* toohello base de datos de SQL Azure o tooSQL Server y, a continuación, importar Hola que contenga datos de dispositivos móviles de hello hacer copia tooHDInsight mediante Hola ruta de acceso siguiente:</span><span class="sxs-lookup"><span data-stu-id="a245e-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="a245e-142">Creación del clúster y la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a245e-142">Create cluster and SQL database</span></span>
<span data-ttu-id="a245e-143">Esta sección muestra cómo toocreate un clúster, una base de datos de SQL y esquemas de base de datos SQL de Hola para ejecución Hola tutorial mediante Hola portal de Azure y una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a245e-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="a245e-144">Hola plantilla puede encontrarse en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="a245e-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="a245e-145">plantilla de administrador de recursos de Hello llama a un bacpac paquete toodeploy Hola tabla esquemas tooSQL base de datos.</span><span class="sxs-lookup"><span data-stu-id="a245e-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="a245e-146">paquete de Hello bacpac se encuentra en un contenedor de blobs públicos, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="a245e-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="a245e-147">Si desea toouse un contenedor privado para los archivos de bacpac de hello, utilice Hola después de valores de hello plantilla:</span><span class="sxs-lookup"><span data-stu-id="a245e-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="a245e-148">Si prefiere hello base de datos SQL y clúster de hello toocreate de toouse PowerShell de Azure, consulte [Apéndice A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="a245e-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="a245e-149">Haga clic en hello después imagen tooopen una plantilla de administrador de recursos en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="a245e-150">Escriba Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="a245e-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="a245e-151">**Suscripción**: escriba su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="a245e-152">**Grupo de recursos**: cree un nuevo grupo de recursos de Azure o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="a245e-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="a245e-153">Un grupo de recursos tiene fines administrativos.</span><span class="sxs-lookup"><span data-stu-id="a245e-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="a245e-154">Es un contenedor de objetos.</span><span class="sxs-lookup"><span data-stu-id="a245e-154">It is a container for objects.</span></span>
    - <span data-ttu-id="a245e-155">**Ubicación**: seleccione una región.</span><span class="sxs-lookup"><span data-stu-id="a245e-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="a245e-156">**ClusterName**: escriba un nombre para el clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="a245e-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="a245e-157">**Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es administrador.</span><span class="sxs-lookup"><span data-stu-id="a245e-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="a245e-158">**Nombre de usuario y contraseña de SSH**.</span><span class="sxs-lookup"><span data-stu-id="a245e-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="a245e-159">**Nombre y contraseña de inicio de sesión en el servidor de la base de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="a245e-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="a245e-160">**_artifacts ubicación**: usar el valor predeterminado de Hola a menos que desee toouse su propio archivo lo en una ubicación diferente.</span><span class="sxs-lookup"><span data-stu-id="a245e-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="a245e-161">**_artifacts Location Sas Token** (Token Sas de ubicación de _artefactos): deje este valor en blanco.</span><span class="sxs-lookup"><span data-stu-id="a245e-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="a245e-162">**Nombre de archivo de Bacpac**: usar el valor predeterminado de Hola a menos que desee toouse su propio archivo lo.</span><span class="sxs-lookup"><span data-stu-id="a245e-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="a245e-163">Hola después valores está codificados en la sección de variables de hello:</span><span class="sxs-lookup"><span data-stu-id="a245e-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="a245e-164">Nombre de la cuenta de almacenamiento predeterminada</span><span class="sxs-lookup"><span data-stu-id="a245e-164">Default storage account name</span></span> | <span data-ttu-id="a245e-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="a245e-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="a245e-166">Nombre del servidor de base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="a245e-166">Azure SQL database server name</span></span> |<span data-ttu-id="a245e-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="a245e-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="a245e-168">Nombre de la base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="a245e-168">Azure SQL database name</span></span> |<span data-ttu-id="a245e-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="a245e-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="a245e-170">Escriba estos valores.</span><span class="sxs-lookup"><span data-stu-id="a245e-170">Please write down these values.</span></span>  <span data-ttu-id="a245e-171">Se necesita más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="a245e-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="a245e-172">3. Haga clic en **Aceptar** parámetros de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="a245e-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="a245e-173">4. de hello **implementación personalizada** hoja, haga clic en **grupo de recursos** desplegable cuadro y, a continuación, haga clic en **New** toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a245e-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="a245e-174">grupo de recursos de Hello es un contenedor que agrupa los clúster de hello, cuenta de almacenamiento dependientes de hello y otro recurso vinculado.</span><span class="sxs-lookup"><span data-stu-id="a245e-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="a245e-175">5. Haga clic en **Términos legales** y en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a245e-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="a245e-176">6. Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a245e-176">6.Click **Create**.</span></span> <span data-ttu-id="a245e-177">Verá un icono nuevo llamado Envío de implementación para la implementación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="a245e-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="a245e-178">Se tarda aproximadamente clúster de aproximadamente 20 minutos toocreate hello y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a245e-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="a245e-179">Si elige toouse de base de datos SQL de Azure existente o Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="a245e-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="a245e-180">**La base de datos SQL Azure**: debe configurar una regla de firewall para hello acceso de tooallow de servidor de base de datos de SQL Azure desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a245e-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="a245e-181">Para obtener instrucciones sobre cómo crear una base de datos de SQL Azure y cómo configurar firewall de hello, consulte [Introducción al uso de la base de datos SQL de Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="a245e-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="a245e-182">De forma predeterminada, una base de datos SQL de Azure permite realizar conexiones desde servicios de Azure, como HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="a245e-183">Si se deshabilita esta configuración de firewall, necesita tooenable desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="a245e-184">Para obtener instrucciones sobre la creación de una base de datos de Azure SQL Database y la configuración de las reglas de firewall, consulte [Creación y configuración de SQL Database][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="a245e-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="a245e-185">**SQL Server**: si el clúster de HDInsight está en hello misma red virtual en Azure como SQL Server, puede usar los pasos de hello en este artículo tooimport y exportación tooa SQL Server base de datos.</span><span class="sxs-lookup"><span data-stu-id="a245e-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a245e-186">HDInsight solo admite redes virtuales basadas en la ubicación y actualmente no funciona con redes virtuales basadas en grupos de afinidad.</span><span class="sxs-lookup"><span data-stu-id="a245e-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="a245e-187">toocreate y configurar una red virtual, consulte [crear una red virtual con el portal de Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="a245e-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="a245e-188">Cuando se utiliza SQL Server en el centro de datos, debe configurar la red virtual de hello como *sitio a sitio* o *point-to-site*.</span><span class="sxs-lookup"><span data-stu-id="a245e-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="a245e-189">Para **point-to-site** redes virtuales, SQL Server deben disponer de cliente VPN Hola aplicación de configuración, que está disponible en hello **panel** de la configuración de red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="a245e-190">Cuando se utiliza SQL Server en una máquina virtual de Azure, se puede utilizar cualquier configuración de red virtual si la máquina virtual de hello hospeda SQL Server es miembro del programa Hola a misma red virtual que HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a245e-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="a245e-191">toocreate un clúster de HDInsight en una red virtual, vea [Hadoop crear clústeres de HDInsight con opciones personalizadas](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="a245e-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a245e-192">SQL Server también debe permitir la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a245e-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="a245e-193">Debe usar un servidor de SQL Server hello toocomplete de inicio de sesión de los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="a245e-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="a245e-194">Ejecución de trabajos de Sqoop</span><span class="sxs-lookup"><span data-stu-id="a245e-194">Run Sqoop jobs</span></span>
<span data-ttu-id="a245e-195">HDInsight puede ejecutar trabajos de Sqoop mediante una variedad de métodos.</span><span class="sxs-lookup"><span data-stu-id="a245e-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="a245e-196">Usar hello después toodecide tabla qué método es adecuado para usted, a continuación, siga el vínculo de Hola para ver un tutorial.</span><span class="sxs-lookup"><span data-stu-id="a245e-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="a245e-197">**Utilícelo** si desea...</span><span class="sxs-lookup"><span data-stu-id="a245e-197">**Use this** if you want...</span></span> | <span data-ttu-id="a245e-198">...un shell **interactivo**</span><span class="sxs-lookup"><span data-stu-id="a245e-198">...an **interactive** shell</span></span> | <span data-ttu-id="a245e-199">...procesamiento por**lotes**</span><span class="sxs-lookup"><span data-stu-id="a245e-199">...**batch** processing</span></span> | <span data-ttu-id="a245e-200">...con este **sistema operativo de clúster**</span><span class="sxs-lookup"><span data-stu-id="a245e-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="a245e-201">...desde este **sistema operativo de cliente**</span><span class="sxs-lookup"><span data-stu-id="a245e-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="a245e-202">SSH</span><span class="sxs-lookup"><span data-stu-id="a245e-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="a245e-203">✔</span><span class="sxs-lookup"><span data-stu-id="a245e-203">✔</span></span> |<span data-ttu-id="a245e-204">✔</span><span class="sxs-lookup"><span data-stu-id="a245e-204">✔</span></span> |<span data-ttu-id="a245e-205">Linux</span><span class="sxs-lookup"><span data-stu-id="a245e-205">Linux</span></span> |<span data-ttu-id="a245e-206">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="a245e-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a245e-207">.NET SDK para Hadoop</span><span class="sxs-lookup"><span data-stu-id="a245e-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="a245e-208">✔</span><span class="sxs-lookup"><span data-stu-id="a245e-208">✔</span></span> |<span data-ttu-id="a245e-209">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="a245e-209">Linux or Windows</span></span> |<span data-ttu-id="a245e-210">Windows (por ahora)</span><span class="sxs-lookup"><span data-stu-id="a245e-210">Windows (for now)</span></span> |
| [<span data-ttu-id="a245e-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a245e-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="a245e-212">✔</span><span class="sxs-lookup"><span data-stu-id="a245e-212">✔</span></span> |<span data-ttu-id="a245e-213">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="a245e-213">Linux or Windows</span></span> |<span data-ttu-id="a245e-214">Windows</span><span class="sxs-lookup"><span data-stu-id="a245e-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="a245e-215">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="a245e-215">Limitations</span></span>
* <span data-ttu-id="a245e-216">La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="a245e-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="a245e-217">Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop varias inserciones en lugar de procesamiento por lotes las operaciones de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="a245e-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a245e-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a245e-218">Next steps</span></span>
<span data-ttu-id="a245e-219">Ahora que ha aprendido cómo toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a245e-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="a245e-220">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="a245e-220">toolearn more, see:</span></span>

* [<span data-ttu-id="a245e-221">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a245e-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a245e-222">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a245e-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="a245e-223">[Uso de Oozie con HDInsight][hdinsight-use-oozie]: use la acción de Sqoop en un flujo de trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="a245e-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="a245e-224">[Analizar datos de retrasos de vuelos con HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze flight retrasar datos y, a continuación, usar base de datos de Sqoop tooexport datos tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="a245e-225">[Cargar datos tooHDInsight][hdinsight-upload-data]: dar con otros métodos para cargar el almacenamiento de blobs de datos tooHDInsight o SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="a245e-226">Apéndice A - un ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a245e-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="a245e-227">ejemplo de Hola a PowerShell realiza Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a245e-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="a245e-228">Conectar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a245e-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="a245e-229">Cree un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-229">Create an Azure resource group.</span></span> <span data-ttu-id="a245e-230">Para obtener más información, consulte [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="a245e-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="a245e-231">Cree un servidor de Base de datos SQL de Azure, una base de datos SQL de Azure y dos tablas.</span><span class="sxs-lookup"><span data-stu-id="a245e-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="a245e-232">Si utiliza SQL Server en su lugar, use hello las instrucciones toocreate Hola tablas siguientes:</span><span class="sxs-lookup"><span data-stu-id="a245e-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
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
   
    <span data-ttu-id="a245e-233">tablas y base de datos de hello más fácil manera tooexamine hello es toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a245e-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="a245e-234">servidor de base de datos de Hola y base de datos de Hola se pueden examinar con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="a245e-235">Cree un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a245e-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="a245e-236">clúster de hello tooexamine, puede usar Hola portal de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a245e-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="a245e-237">Preprocesar archivo de datos de origen de hello.</span><span class="sxs-lookup"><span data-stu-id="a245e-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="a245e-238">En este tutorial, exporte un archivo de registro log4j (un archivo delimitado) y una base de datos de Hive tabla tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="a245e-239">Hello archivo delimitado se denomina */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="a245e-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="a245e-240">Anteriormente en el tutorial de hello, ha visto algunos ejemplos de log4j registros.</span><span class="sxs-lookup"><span data-stu-id="a245e-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="a245e-241">En el archivo de registro de hello, hay algunas líneas vacías y algunos toothese similar de líneas:</span><span class="sxs-lookup"><span data-stu-id="a245e-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="a245e-242">Esto es correcto para obtener ejemplos que utilizan estos datos, pero debemos eliminar estas excepciones antes de que podemos importar en la base de datos de SQL Azure de Hola o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a245e-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="a245e-243">Se produce un error en la exportación de Sqoop si se produce una cadena vacía o una línea con un menor elementos que número Hola de campos definidos en la tabla de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="a245e-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="a245e-244">tabla de Hello log4jlogs tiene 7 campos de tipo de cadena.</span><span class="sxs-lookup"><span data-stu-id="a245e-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="a245e-245">Este procedimiento crea un nuevo archivo en clúster de hello: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="a245e-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="a245e-246">archivo de datos modificados de hello tooexamine, puede usar Hola portal de Azure, una herramienta de explorador de almacenamiento de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a245e-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="a245e-247">[Empezar a trabajar con HDInsight] [ hdinsight-get-started] tiene un código de ejemplo para usar Azure PowerShell toodownload un archivo y mostrar el contenido del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a245e-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="a245e-248">Exportar una base de datos de SQL Azure de datos archivo toohello.</span><span class="sxs-lookup"><span data-stu-id="a245e-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="a245e-249">archivo de código fuente de Hello es tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="a245e-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="a245e-250">tabla de Hola donde datos hello están toois exportados denomina log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="a245e-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a245e-251">Distinto de información de la cadena de conexión, deberían funcionar pasos hello en esta sección para una base de datos de SQL Azure o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a245e-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="a245e-252">Estos pasos se han probado con hello siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="a245e-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="a245e-253">**Configuración de red virtual de Azure point-to-site**: una red virtual conectado hello HDInsight clúster tooa SQL Server en un centro de datos privado.</span><span class="sxs-lookup"><span data-stu-id="a245e-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="a245e-254">Vea [configurar una VPN de punto a sitio en el Portal de administración de Hola](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a245e-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="a245e-255">**HDInsight de Azure 3.1:**consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener más información sobre cómo crear un clúster en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="a245e-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="a245e-256">**SQL Server 2014**: configurar autenticación tooallow y tooconnect de paquete de configuración cliente VPN de hello ejecución segura toohello de red virtual.</span><span class="sxs-lookup"><span data-stu-id="a245e-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="a245e-257">Exportar una base de datos de Hive tabla toohello SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a245e-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="a245e-258">Importe el clúster de HDInsight de hello mobiledata tabla toohello.</span><span class="sxs-lookup"><span data-stu-id="a245e-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="a245e-259">archivo de datos modificados de hello tooexamine, puede usar Hola portal de Azure, una herramienta de explorador de almacenamiento de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a245e-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="a245e-260">[Empezar a trabajar con HDInsight] [ hdinsight-get-started] tiene un código de ejemplo sobre el uso de PowerShell de Azure toodownload un archivo y mostrar el contenido del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a245e-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="a245e-261">ejemplo de Hola a PowerShell</span><span class="sxs-lookup"><span data-stu-id="a245e-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
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
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
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

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

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
