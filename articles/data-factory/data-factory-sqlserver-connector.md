---
title: aaaMove tooand de datos de SQL Server | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de SQL Server de base de datos que es local o en una máquina virtual de Azure mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="e4f90-103">Mover tooand de datos de SQL Server local o en IaaS (VM de Azure) mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="e4f90-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="e4f90-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="e4f90-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="e4f90-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="e4f90-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="e4f90-106">Supported scenarios</span></span>
<span data-ttu-id="e4f90-107">Puede copiar datos **desde una base de datos de SQL Server** toohello siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="e4f90-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="e4f90-108">Puede copiar los datos de hello siguientes almacenes de datos **base de datos de SQL Server tooa**:</span><span class="sxs-lookup"><span data-stu-id="e4f90-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="e4f90-109">Versiones admitidas de SQL Server</span><span class="sxs-lookup"><span data-stu-id="e4f90-109">Supported SQL Server versions</span></span>
<span data-ttu-id="e4f90-110">Esta compatibilidad del conector de SQL Server copian datos de / toohello después de las versiones de instancia hospedada en local o en IaaS de Azure mediante la autenticación de Windows y autenticación de SQL: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="e4f90-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="e4f90-111">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="e4f90-111">Enabling connectivity</span></span>
<span data-ttu-id="e4f90-112">conceptos de Hola y los pasos necesarios para conectar con SQL Server hospedado en local o en Azure IaaS (infraestructura como-servicio) las máquinas virtuales se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="e4f90-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="e4f90-113">En ambos casos, debe toouse Data Management Gateway para la conectividad.</span><span class="sxs-lookup"><span data-stu-id="e4f90-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="e4f90-114">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="e4f90-115">La configuración de una instancia de puerta de enlace es un requisito previo para conectarse con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="e4f90-116">Durante la instalación de puerta de enlace en hello mismo local instancia de máquina virtual de máquina o en la nube como Hola SQL Server para mejorar el rendimiento, se recomienda instalarlos en equipos diferentes.</span><span class="sxs-lookup"><span data-stu-id="e4f90-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="e4f90-117">Tener puerta de enlace de Hola y SQL Server en equipos diferentes reduce la contención de recursos.</span><span class="sxs-lookup"><span data-stu-id="e4f90-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e4f90-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="e4f90-118">Getting started</span></span>
<span data-ttu-id="e4f90-119">Puede crear una canalización con actividad de copia que mueva los datos desde una base de datos de SQL Server local o hacia ella mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="e4f90-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="e4f90-120">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e4f90-121">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="e4f90-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="e4f90-122">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e4f90-123">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="e4f90-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e4f90-124">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="e4f90-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="e4f90-125">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-125">Create a **data factory**.</span></span> <span data-ttu-id="e4f90-126">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="e4f90-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="e4f90-127">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="e4f90-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="e4f90-128">Por ejemplo, si va a copiar datos desde un tooan de base de datos de SQL Server almacenamiento de blobs de Azure, cree dos toolink servicios vinculados su base de datos de SQL Server y la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f90-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="e4f90-129">Para las propiedades de servicio vinculado que son la base de datos de servidor tooSQL específicos, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="e4f90-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="e4f90-130">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="e4f90-131">En el ejemplo de Hola mencionado en el último paso de hello, cree una tabla SQL de conjunto de datos toospecify hello en la base de datos de SQL Server que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="e4f90-132">Crear contenedor de blobs Hola de otro conjunto de datos toospecify y carpeta Hola que contiene datos de hello copiados de Hola de base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="e4f90-133">Para las propiedades de conjunto de datos que son la base de datos de servidor tooSQL específicos, consulte [propiedades de conjunto de datos](#dataset-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="e4f90-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="e4f90-134">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="e4f90-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="e4f90-135">En el ejemplo de Hola que se ha mencionado anteriormente, use SqlSource como un origen y BlobSink como un receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="e4f90-136">De forma similar, si va a copiar desde el almacenamiento de blobs de Azure tooSQL base de datos del servidor, usar BlobSource y SqlSink de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="e4f90-137">Para copiar propiedades de actividad que son específico tooSQL base de datos de servidor, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="e4f90-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="e4f90-138">Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="e4f90-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="e4f90-139">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="e4f90-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e4f90-140">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e4f90-141">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde una base de datos de SQL Server local, vea [ejemplos JSON](#json-examples-for-copying-data-from-and-to-sql-server) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="e4f90-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="e4f90-142">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooSQL Server:</span><span class="sxs-lookup"><span data-stu-id="e4f90-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e4f90-143">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="e4f90-143">Linked service properties</span></span>
<span data-ttu-id="e4f90-144">Crear un servicio vinculado de tipo **onpremisessqlserver** toolink una factoría de datos local tooa de base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="e4f90-145">Hello en la tabla siguiente proporciona la descripción del servicio de SQL Server vinculado de JSON elementos tooon local específico.</span><span class="sxs-lookup"><span data-stu-id="e4f90-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="e4f90-146">Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSQL servicio del servidor vinculado.</span><span class="sxs-lookup"><span data-stu-id="e4f90-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="e4f90-147">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e4f90-147">Property</span></span> | <span data-ttu-id="e4f90-148">Descripción</span><span class="sxs-lookup"><span data-stu-id="e4f90-148">Description</span></span> | <span data-ttu-id="e4f90-149">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e4f90-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e4f90-150">type</span><span class="sxs-lookup"><span data-stu-id="e4f90-150">type</span></span> |<span data-ttu-id="e4f90-151">propiedad de tipo Hello debe establecerse en: **onpremisessqlserver**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="e4f90-152">Sí</span><span class="sxs-lookup"><span data-stu-id="e4f90-152">Yes</span></span> |
| <span data-ttu-id="e4f90-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="e4f90-153">connectionString</span></span> |<span data-ttu-id="e4f90-154">Especificar información de connectionString necesaria tooconnect toohello en SQL Server base de datos local con autenticación de SQL o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="e4f90-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="e4f90-155">Sí</span><span class="sxs-lookup"><span data-stu-id="e4f90-155">Yes</span></span> |
| <span data-ttu-id="e4f90-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e4f90-156">gatewayName</span></span> |<span data-ttu-id="e4f90-157">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de SQL Server de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="e4f90-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="e4f90-158">Sí</span><span class="sxs-lookup"><span data-stu-id="e4f90-158">Yes</span></span> |
| <span data-ttu-id="e4f90-159">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="e4f90-159">username</span></span> |<span data-ttu-id="e4f90-160">Especifique el nombre de usuario si usa la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="e4f90-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="e4f90-161">Ejemplo: **nombreDeDominio\\nombreDeUsuario**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="e4f90-162">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-162">No</span></span> |
| <span data-ttu-id="e4f90-163">Contraseña</span><span class="sxs-lookup"><span data-stu-id="e4f90-163">password</span></span> |<span data-ttu-id="e4f90-164">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e4f90-165">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-165">No</span></span> |

<span data-ttu-id="e4f90-166">Puede cifrar las credenciales con hello **New-AzureRmDataFactoryEncryptValue** cmdlet y usarlos en la cadena de conexión de hello tal y como se muestra en el siguiente ejemplo de Hola (**EncryptedCredential** propiedad):</span><span class="sxs-lookup"><span data-stu-id="e4f90-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="e4f90-167">Muestras</span><span class="sxs-lookup"><span data-stu-id="e4f90-167">Samples</span></span>
<span data-ttu-id="e4f90-168">**JSON para usar autenticación de SQL**</span><span class="sxs-lookup"><span data-stu-id="e4f90-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="e4f90-169">**JSON para usar autenticación de Windows**</span><span class="sxs-lookup"><span data-stu-id="e4f90-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="e4f90-170">Data Management Gateway suplantará Hola especificada base de datos de usuario cuenta tooconnect toohello local SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="e4f90-171">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="e4f90-171">Dataset properties</span></span>
<span data-ttu-id="e4f90-172">En los ejemplos de hello, ha utilizado un conjunto de datos de tipo **SqlServerTable** toorepresent una tabla en una base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="e4f90-173">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="e4f90-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e4f90-174">Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (SQL Server, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="e4f90-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e4f90-175">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="e4f90-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e4f90-176">Hola **typeProperties** sección Hola conjunto de datos de tipo **SqlServerTable** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4f90-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="e4f90-177">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e4f90-177">Property</span></span> | <span data-ttu-id="e4f90-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="e4f90-178">Description</span></span> | <span data-ttu-id="e4f90-179">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e4f90-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e4f90-180">tableName</span><span class="sxs-lookup"><span data-stu-id="e4f90-180">tableName</span></span> |<span data-ttu-id="e4f90-181">Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Server de Hola que servicio vinculado hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="e4f90-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="e4f90-182">Sí</span><span class="sxs-lookup"><span data-stu-id="e4f90-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e4f90-183">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="e4f90-183">Copy activity properties</span></span>
<span data-ttu-id="e4f90-184">Si va a mover datos desde una base de datos de SQL Server, configure tipo de origen de hello en la actividad de copia de hello demasiado**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="e4f90-185">De forma similar, si va a mover la base de datos de SQL Server de tooa de datos, Establece el tipo de receptor de hello en actividad de copia de hello demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="e4f90-186">Esta sección proporciona una lista de propiedades admitidas por SqlSource y SqlSink.</span><span class="sxs-lookup"><span data-stu-id="e4f90-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="e4f90-187">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="e4f90-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e4f90-188">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="e4f90-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="e4f90-189">Hola actividad de copia toma solo una entrada y produce un único resultado.</span><span class="sxs-lookup"><span data-stu-id="e4f90-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="e4f90-190">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="e4f90-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="e4f90-191">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="e4f90-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="e4f90-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="e4f90-192">SqlSource</span></span>
<span data-ttu-id="e4f90-193">Cuando el origen de una actividad de copia es del tipo **SqlSource**, Hola propiedades siguientes está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="e4f90-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e4f90-194">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e4f90-194">Property</span></span> | <span data-ttu-id="e4f90-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="e4f90-195">Description</span></span> | <span data-ttu-id="e4f90-196">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="e4f90-196">Allowed values</span></span> | <span data-ttu-id="e4f90-197">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e4f90-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e4f90-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e4f90-198">sqlReaderQuery</span></span> |<span data-ttu-id="e4f90-199">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="e4f90-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e4f90-200">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="e4f90-200">SQL query string.</span></span> <span data-ttu-id="e4f90-201">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="e4f90-201">For example: select * from MyTable.</span></span> <span data-ttu-id="e4f90-202">Puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="e4f90-203">Si no se especifica, Hola instrucción SQL ejecutada: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="e4f90-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="e4f90-204">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-204">No</span></span> |
| <span data-ttu-id="e4f90-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e4f90-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="e4f90-206">Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="e4f90-207">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="e4f90-207">Name of hello stored procedure.</span></span> <span data-ttu-id="e4f90-208">Hola última instrucción de SQL debe ser una instrucción SELECT en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="e4f90-209">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-209">No</span></span> |
| <span data-ttu-id="e4f90-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e4f90-210">storedProcedureParameters</span></span> |<span data-ttu-id="e4f90-211">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="e4f90-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="e4f90-212">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="e4f90-212">Name/value pairs.</span></span> <span data-ttu-id="e4f90-213">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="e4f90-214">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-214">No</span></span> |

<span data-ttu-id="e4f90-215">Si hello **sqlReaderQuery** se especifica para hello SqlSource, hello actividad de copia ejecuta esta consulta en datos de Hola de hello base de datos de SQL Server origen tooget.</span><span class="sxs-lookup"><span data-stu-id="e4f90-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="e4f90-216">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="e4f90-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="e4f90-217">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="e4f90-218">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="e4f90-219">Cuando usas **sqlReaderStoredProcedureName**, seguirá necesitando toospecify un valor para hello **tableName** propiedad Hola de conjunto de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="e4f90-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="e4f90-220">Pero no se ha realizado ninguna validación en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="e4f90-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="e4f90-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="e4f90-221">SqlSink</span></span>
<span data-ttu-id="e4f90-222">**SqlSink** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4f90-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="e4f90-223">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e4f90-223">Property</span></span> | <span data-ttu-id="e4f90-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="e4f90-224">Description</span></span> | <span data-ttu-id="e4f90-225">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="e4f90-225">Allowed values</span></span> | <span data-ttu-id="e4f90-226">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e4f90-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e4f90-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e4f90-227">writeBatchTimeout</span></span> |<span data-ttu-id="e4f90-228">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="e4f90-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="e4f90-229">timespan</span><span class="sxs-lookup"><span data-stu-id="e4f90-229">timespan</span></span><br/><br/> <span data-ttu-id="e4f90-230">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="e4f90-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e4f90-231">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-231">No</span></span> |
| <span data-ttu-id="e4f90-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e4f90-232">writeBatchSize</span></span> |<span data-ttu-id="e4f90-233">Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="e4f90-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="e4f90-234">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="e4f90-234">Integer (number of rows)</span></span> |<span data-ttu-id="e4f90-235">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="e4f90-235">No (default: 10000)</span></span> |
| <span data-ttu-id="e4f90-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e4f90-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e4f90-237">Especificar la consulta para tooexecute de actividad de copia que se limpian los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="e4f90-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="e4f90-238">Para más información, consulte la sección [copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="e4f90-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="e4f90-239">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="e4f90-239">A query statement.</span></span> |<span data-ttu-id="e4f90-240">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-240">No</span></span> |
| <span data-ttu-id="e4f90-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="e4f90-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="e4f90-242">Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="e4f90-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="e4f90-243">Para más información, consulte la sección [copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="e4f90-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="e4f90-244">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="e4f90-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="e4f90-245">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-245">No</span></span> |
| <span data-ttu-id="e4f90-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e4f90-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="e4f90-247">Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="e4f90-248">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="e4f90-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="e4f90-249">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-249">No</span></span> |
| <span data-ttu-id="e4f90-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e4f90-250">storedProcedureParameters</span></span> |<span data-ttu-id="e4f90-251">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="e4f90-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="e4f90-252">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="e4f90-252">Name/value pairs.</span></span> <span data-ttu-id="e4f90-253">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="e4f90-254">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-254">No</span></span> |
| <span data-ttu-id="e4f90-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="e4f90-255">sqlWriterTableType</span></span> |<span data-ttu-id="e4f90-256">Especifique toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="e4f90-257">Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="e4f90-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="e4f90-258">Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="e4f90-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="e4f90-259">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="e4f90-259">A table type name.</span></span> |<span data-ttu-id="e4f90-260">No</span><span class="sxs-lookup"><span data-stu-id="e4f90-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="e4f90-261">Ejemplos JSON para copiar datos desde y tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="e4f90-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="e4f90-262">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e4f90-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e4f90-263">Hola siguientes ejemplos muestran cómo toocopy tooand de datos de SQL Server y el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f90-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="e4f90-264">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f90-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="e4f90-265">Ejemplo: Copiar los datos de SQL Server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e4f90-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="e4f90-266">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="e4f90-266">hello following sample shows:</span></span>

1. <span data-ttu-id="e4f90-267">Un servicio vinculado de tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="e4f90-268">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="e4f90-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e4f90-269">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="e4f90-270">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e4f90-271">Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e4f90-272">ejemplo de Hola copia datos de serie temporal de un tooan de tabla de SQL Server blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="e4f90-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="e4f90-273">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="e4f90-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e4f90-274">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="e4f90-275">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="e4f90-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="e4f90-276">**Servicio vinculado de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="e4f90-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="e4f90-277">**Servicio vinculado de almacenamiento de blobs de Azure**</span><span class="sxs-lookup"><span data-stu-id="e4f90-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="e4f90-278">**Conjunto de datos de entrada de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="e4f90-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="e4f90-279">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Server y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="e4f90-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="e4f90-280">Puede consultar a través de varias tablas dentro de hello misma mediante un único conjunto de datos, pero una sola tabla de base de datos debe utilizarse para typeProperty de nombre de tabla del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="e4f90-281">Establecer "externo": "true" informa a servicio de factoría de datos ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="e4f90-282">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="e4f90-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="e4f90-283">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="e4f90-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e4f90-284">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="e4f90-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e4f90-285">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="e4f90-286">**Canalización con actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="e4f90-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="e4f90-287">canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="e4f90-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e4f90-288">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="e4f90-289">consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="e4f90-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
<span data-ttu-id="e4f90-290">En este ejemplo, **sqlReaderQuery** se especifica para hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="e4f90-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="e4f90-291">Hola actividad de copia ejecuta esta consulta contra Hola datos de saludo de tooget de origen de base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="e4f90-292">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="e4f90-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="e4f90-293">Hola sqlReaderQuery puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="e4f90-294">No es limitado tooonly Hola tabla establecido como Hola typeProperty de nombre de tabla del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="e4f90-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="e4f90-295">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="e4f90-296">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="e4f90-297">Vea hello [origen Sql](#sqlsource) sección y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de Hola de propiedades admitidas por SqlSource y BlobSink.</span><span class="sxs-lookup"><span data-stu-id="e4f90-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="e4f90-298">Ejemplo: Copiar los datos de Blob de Azure tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="e4f90-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="e4f90-299">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="e4f90-299">hello following sample shows:</span></span>

1. <span data-ttu-id="e4f90-300">Hola vinculado servicio del tipo [onpremisessqlserver](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="e4f90-301">Hola vinculado servicio del tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e4f90-302">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e4f90-303">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e4f90-304">Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="e4f90-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="e4f90-305">ejemplo de Hola copia datos de series temporales de una tabla de SQL Server tooa de blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="e4f90-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="e4f90-306">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="e4f90-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e4f90-307">**Servicio vinculado de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="e4f90-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="e4f90-308">**Servicio vinculado de almacenamiento de blobs de Azure**</span><span class="sxs-lookup"><span data-stu-id="e4f90-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="e4f90-309">**Conjunto de datos de entrada de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="e4f90-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="e4f90-310">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="e4f90-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e4f90-311">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="e4f90-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e4f90-312">ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="e4f90-313">"externo": "true" configuración informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="e4f90-314">**Conjunto de datos de salida de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="e4f90-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="e4f90-315">ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4f90-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="e4f90-316">Crear tabla de hello en SQL Server con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="e4f90-317">Se agregan nuevas filas toohello tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="e4f90-317">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="e4f90-318">**Canalización con actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="e4f90-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="e4f90-319">canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="e4f90-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e4f90-320">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="e4f90-321">Solución de problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="e4f90-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="e4f90-322">Configurar las conexiones remotas de SQL Server tooaccept.</span><span class="sxs-lookup"><span data-stu-id="e4f90-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="e4f90-323">Inicie **SQL Server Management Studio**, haga clic con el botón derecho en **Servidor** y después en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="e4f90-324">Seleccione **conexiones** en lista de Hola y verificación **server toohello de permitir conexiones remotas**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Habilitar conexiones remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="e4f90-326">Vea [configurar la opción de configuración de servidor de acceso remoto de hello](https://msdn.microsoft.com/library/ms191464.aspx) para obtener pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="e4f90-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="e4f90-327">Inicie el **Administrador de configuración de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="e4f90-328">Expanda **configuración de red de SQL Server** para saludo de la instancia desee y seleccione **protocolos para MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="e4f90-329">Debería ver los protocolos en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="e4f90-330">Para habilitar TCP/IP, haga clic con el botón derecho en **TCP/IP** y haga clic en **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="e4f90-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Habilitar TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="e4f90-332">Consulte [Habilitar o deshabilitar un protocolo de red de servidor](https://msdn.microsoft.com/library/ms191294.aspx) para ver información y maneras alternativas de habilitar el protocolo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e4f90-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="e4f90-333">En la consulta Hola la misma ventana, haga doble clic en **TCP/IP** toolaunch **propiedades TCP/IP** ventana.</span><span class="sxs-lookup"><span data-stu-id="e4f90-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="e4f90-334">Cambiar toohello **direcciones IP** ficha. Desplácese hacia abajo toosee **IPAll** sección.</span><span class="sxs-lookup"><span data-stu-id="e4f90-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="e4f90-335">Tome nota de Hola ** el puerto TCP ** (valor predeterminado es **1433**).</span><span class="sxs-lookup"><span data-stu-id="e4f90-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="e4f90-336">Crear un **regla de Firewall de Windows hello** en hello máquina tooallow el tráfico entrante a través de este puerto.</span><span class="sxs-lookup"><span data-stu-id="e4f90-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="e4f90-337">**Compruebe la conexión**: tooconnect toohello SQL Server con el nombre completo, use SQL Server Management Studio desde un equipo diferente.</span><span class="sxs-lookup"><span data-stu-id="e4f90-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="e4f90-338">Por ejemplo: <machine><domain>.corp<company>.com,1433.</span><span class="sxs-lookup"><span data-stu-id="e4f90-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="e4f90-339">Vea [mover datos entre orígenes locales y en la nube Hola con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="e4f90-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="e4f90-340">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e4f90-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="e4f90-341">Columnas de identidad en la base de datos de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="e4f90-341">Identity columns in hello target database</span></span>
<span data-ttu-id="e4f90-342">En esta sección se proporciona un ejemplo que copia datos de una tabla de origen con ninguna tabla de destino de tooa de columna de identidad con una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="e4f90-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="e4f90-343">**Tabla de origen:**</span><span class="sxs-lookup"><span data-stu-id="e4f90-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="e4f90-344">**Tabla de destino:**</span><span class="sxs-lookup"><span data-stu-id="e4f90-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="e4f90-345">Tenga en cuenta que esa tabla de destino de hello tiene una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="e4f90-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="e4f90-346">**Definición de JSON del conjunto de datos de origen**</span><span class="sxs-lookup"><span data-stu-id="e4f90-346">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="e4f90-347">**Definición de JSON del conjunto de datos de destino**</span><span class="sxs-lookup"><span data-stu-id="e4f90-347">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="e4f90-348">Tenga en cuenta que la tabla de origen y de destino tienen un esquema diferente (el destino tiene una columna adicional con identidad).</span><span class="sxs-lookup"><span data-stu-id="e4f90-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="e4f90-349">En este escenario, necesita toospecify **estructura** propiedad en la definición de conjunto de datos de destino de hello, que no incluye la columna de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="e4f90-350">Invocación del procedimiento almacenado desde el receptor de SQL</span><span class="sxs-lookup"><span data-stu-id="e4f90-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="e4f90-351">Para ver un ejemplo de invocación de un procedimiento almacenado desde el receptor de SQL en una actividad de copia de una canalización, consulte el artículo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocación de un procedimiento almacenado desde el receptor de SQL en la actividad de copia).</span><span class="sxs-lookup"><span data-stu-id="e4f90-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="e4f90-352">Asignación de tipos para SQL Server</span><span class="sxs-lookup"><span data-stu-id="e4f90-352">Type mapping for SQL server</span></span>
<span data-ttu-id="e4f90-353">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, Hola actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="e4f90-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="e4f90-354">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="e4f90-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="e4f90-355">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="e4f90-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="e4f90-356">Al mover datos demasiado & de SQL server, Hola siguientes asignaciones se usan del tipo de too.NET de tipo SQL y viceversa.</span><span class="sxs-lookup"><span data-stu-id="e4f90-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="e4f90-357">asignación de Hello es igual a la asignación de tipo de datos de SQL Server para ADO.NET Hola.</span><span class="sxs-lookup"><span data-stu-id="e4f90-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="e4f90-358">Tipo de motor de base de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="e4f90-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="e4f90-359">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e4f90-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="e4f90-360">bigint</span><span class="sxs-lookup"><span data-stu-id="e4f90-360">bigint</span></span> |<span data-ttu-id="e4f90-361">Int64</span><span class="sxs-lookup"><span data-stu-id="e4f90-361">Int64</span></span> |
| <span data-ttu-id="e4f90-362">binary</span><span class="sxs-lookup"><span data-stu-id="e4f90-362">binary</span></span> |<span data-ttu-id="e4f90-363">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-363">Byte[]</span></span> |
| <span data-ttu-id="e4f90-364">bit</span><span class="sxs-lookup"><span data-stu-id="e4f90-364">bit</span></span> |<span data-ttu-id="e4f90-365">Booleano</span><span class="sxs-lookup"><span data-stu-id="e4f90-365">Boolean</span></span> |
| <span data-ttu-id="e4f90-366">char</span><span class="sxs-lookup"><span data-stu-id="e4f90-366">char</span></span> |<span data-ttu-id="e4f90-367">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-367">String, Char[]</span></span> |
| <span data-ttu-id="e4f90-368">fecha</span><span class="sxs-lookup"><span data-stu-id="e4f90-368">date</span></span> |<span data-ttu-id="e4f90-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="e4f90-369">DateTime</span></span> |
| <span data-ttu-id="e4f90-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="e4f90-370">Datetime</span></span> |<span data-ttu-id="e4f90-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="e4f90-371">DateTime</span></span> |
| <span data-ttu-id="e4f90-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="e4f90-372">datetime2</span></span> |<span data-ttu-id="e4f90-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="e4f90-373">DateTime</span></span> |
| <span data-ttu-id="e4f90-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="e4f90-374">Datetimeoffset</span></span> |<span data-ttu-id="e4f90-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="e4f90-375">DateTimeOffset</span></span> |
| <span data-ttu-id="e4f90-376">Decimal</span><span class="sxs-lookup"><span data-stu-id="e4f90-376">Decimal</span></span> |<span data-ttu-id="e4f90-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="e4f90-377">Decimal</span></span> |
| <span data-ttu-id="e4f90-378">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="e4f90-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="e4f90-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-379">Byte[]</span></span> |
| <span data-ttu-id="e4f90-380">Float</span><span class="sxs-lookup"><span data-stu-id="e4f90-380">Float</span></span> |<span data-ttu-id="e4f90-381">Doble</span><span class="sxs-lookup"><span data-stu-id="e4f90-381">Double</span></span> |
| <span data-ttu-id="e4f90-382">imagen</span><span class="sxs-lookup"><span data-stu-id="e4f90-382">image</span></span> |<span data-ttu-id="e4f90-383">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-383">Byte[]</span></span> |
| <span data-ttu-id="e4f90-384">int</span><span class="sxs-lookup"><span data-stu-id="e4f90-384">int</span></span> |<span data-ttu-id="e4f90-385">Int32</span><span class="sxs-lookup"><span data-stu-id="e4f90-385">Int32</span></span> |
| <span data-ttu-id="e4f90-386">money</span><span class="sxs-lookup"><span data-stu-id="e4f90-386">money</span></span> |<span data-ttu-id="e4f90-387">Decimal</span><span class="sxs-lookup"><span data-stu-id="e4f90-387">Decimal</span></span> |
| <span data-ttu-id="e4f90-388">nchar</span><span class="sxs-lookup"><span data-stu-id="e4f90-388">nchar</span></span> |<span data-ttu-id="e4f90-389">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-389">String, Char[]</span></span> |
| <span data-ttu-id="e4f90-390">ntext</span><span class="sxs-lookup"><span data-stu-id="e4f90-390">ntext</span></span> |<span data-ttu-id="e4f90-391">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-391">String, Char[]</span></span> |
| <span data-ttu-id="e4f90-392">numeric</span><span class="sxs-lookup"><span data-stu-id="e4f90-392">numeric</span></span> |<span data-ttu-id="e4f90-393">Decimal</span><span class="sxs-lookup"><span data-stu-id="e4f90-393">Decimal</span></span> |
| <span data-ttu-id="e4f90-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="e4f90-394">nvarchar</span></span> |<span data-ttu-id="e4f90-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-395">String, Char[]</span></span> |
| <span data-ttu-id="e4f90-396">real</span><span class="sxs-lookup"><span data-stu-id="e4f90-396">real</span></span> |<span data-ttu-id="e4f90-397">Single</span><span class="sxs-lookup"><span data-stu-id="e4f90-397">Single</span></span> |
| <span data-ttu-id="e4f90-398">rowversion</span><span class="sxs-lookup"><span data-stu-id="e4f90-398">rowversion</span></span> |<span data-ttu-id="e4f90-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-399">Byte[]</span></span> |
| <span data-ttu-id="e4f90-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="e4f90-400">smalldatetime</span></span> |<span data-ttu-id="e4f90-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="e4f90-401">DateTime</span></span> |
| <span data-ttu-id="e4f90-402">smallint</span><span class="sxs-lookup"><span data-stu-id="e4f90-402">smallint</span></span> |<span data-ttu-id="e4f90-403">Int16</span><span class="sxs-lookup"><span data-stu-id="e4f90-403">Int16</span></span> |
| <span data-ttu-id="e4f90-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="e4f90-404">smallmoney</span></span> |<span data-ttu-id="e4f90-405">Decimal</span><span class="sxs-lookup"><span data-stu-id="e4f90-405">Decimal</span></span> |
| <span data-ttu-id="e4f90-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="e4f90-406">sql_variant</span></span> |<span data-ttu-id="e4f90-407">Object *</span><span class="sxs-lookup"><span data-stu-id="e4f90-407">Object *</span></span> |
| <span data-ttu-id="e4f90-408">text</span><span class="sxs-lookup"><span data-stu-id="e4f90-408">text</span></span> |<span data-ttu-id="e4f90-409">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-409">String, Char[]</span></span> |
| <span data-ttu-id="e4f90-410">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="e4f90-410">time</span></span> |<span data-ttu-id="e4f90-411">timespan</span><span class="sxs-lookup"><span data-stu-id="e4f90-411">TimeSpan</span></span> |
| <span data-ttu-id="e4f90-412">timestamp</span><span class="sxs-lookup"><span data-stu-id="e4f90-412">timestamp</span></span> |<span data-ttu-id="e4f90-413">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-413">Byte[]</span></span> |
| <span data-ttu-id="e4f90-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="e4f90-414">tinyint</span></span> |<span data-ttu-id="e4f90-415">Byte</span><span class="sxs-lookup"><span data-stu-id="e4f90-415">Byte</span></span> |
| <span data-ttu-id="e4f90-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="e4f90-416">uniqueidentifier</span></span> |<span data-ttu-id="e4f90-417">Guid</span><span class="sxs-lookup"><span data-stu-id="e4f90-417">Guid</span></span> |
| <span data-ttu-id="e4f90-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="e4f90-418">varbinary</span></span> |<span data-ttu-id="e4f90-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-419">Byte[]</span></span> |
| <span data-ttu-id="e4f90-420">varchar</span><span class="sxs-lookup"><span data-stu-id="e4f90-420">varchar</span></span> |<span data-ttu-id="e4f90-421">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="e4f90-421">String, Char[]</span></span> |
| <span data-ttu-id="e4f90-422">xml</span><span class="sxs-lookup"><span data-stu-id="e4f90-422">xml</span></span> |<span data-ttu-id="e4f90-423">xml</span><span class="sxs-lookup"><span data-stu-id="e4f90-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="e4f90-424">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="e4f90-424">Mapping source toosink columns</span></span>
<span data-ttu-id="e4f90-425">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e4f90-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="e4f90-426">Copia repetible</span><span class="sxs-lookup"><span data-stu-id="e4f90-426">Repeatable copy</span></span>
<span data-ttu-id="e4f90-427">Cuando se copian datos tooSQL base de datos de servidor, actividad de copia de hello anexa la tabla de datos toohello receptor de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e4f90-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="e4f90-428">en su lugar, vea tooperform un UPSERT [tooSqlSink escritura repetible](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artículo.</span><span class="sxs-lookup"><span data-stu-id="e4f90-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="e4f90-429">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="e4f90-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="e4f90-430">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="e4f90-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e4f90-431">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="e4f90-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e4f90-432">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="e4f90-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e4f90-433">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="e4f90-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e4f90-434">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="e4f90-434">Performance and Tuning</span></span>
<span data-ttu-id="e4f90-435">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="e4f90-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
