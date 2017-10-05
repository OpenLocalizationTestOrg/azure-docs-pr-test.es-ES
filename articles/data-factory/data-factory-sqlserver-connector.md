---
title: Traslado de datos con SQL Server como origen y destino | Microsoft Docs
description: "Aprenda a mover los datos hacia y desde una base de datos SQL Server en un entorno local o en una máquina virtual de Azure mediante Factoría de datos de Azure."
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
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="f2808-103">Movimiento de los datos entre entornos locales de SQL Server o en IaaS (máquina virtual de Azure) mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="f2808-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="f2808-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos de una base de datos SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="f2808-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="f2808-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f2808-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="f2808-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="f2808-106">Supported scenarios</span></span>
<span data-ttu-id="f2808-107">Puede copiar datos **de una base de datos SQL Server** a los siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="f2808-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="f2808-108">Puede copiar datos de los siguientes almacenes de datos **a una base de datos SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="f2808-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="f2808-109">Versiones admitidas de SQL Server</span><span class="sxs-lookup"><span data-stu-id="f2808-109">Supported SQL Server versions</span></span>
<span data-ttu-id="f2808-110">Este conector de SQL Server admite la copia de datos hacia y desde las siguientes versiones de la instancia hospedada local o en Azure IaaS mediante autenticación de SQL y autenticación de Windows: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="f2808-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="f2808-111">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="f2808-111">Enabling connectivity</span></span>
<span data-ttu-id="f2808-112">Los conceptos y los pasos necesarios para conectar con SQL Server hospedado de forma local o en máquinas virtuales de IaaS de Azure (infraestructura como servicio) son los mismos.</span><span class="sxs-lookup"><span data-stu-id="f2808-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="f2808-113">En ambos casos, tendrá que utilizar Data Management Gateway para establecer la conectividad.</span><span class="sxs-lookup"><span data-stu-id="f2808-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="f2808-114">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f2808-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="f2808-115">La configuración de una instancia de puerta de enlace es un requisito previo para conectarse con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2808-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="f2808-116">Aunque puede instalar la puerta de enlace en la misma máquina local o una instancia de máquina virtual en la nube, como SQL Server, para mejorar el rendimiento, se recomienda instalarlos en máquinas independientes.</span><span class="sxs-lookup"><span data-stu-id="f2808-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="f2808-117">Tener la puerta de enlace y SQL Server en máquinas diferentes reduce la contención de recursos.</span><span class="sxs-lookup"><span data-stu-id="f2808-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f2808-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="f2808-118">Getting started</span></span>
<span data-ttu-id="f2808-119">Puede crear una canalización con actividad de copia que mueva los datos desde una base de datos de SQL Server local o hacia ella mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="f2808-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="f2808-120">La manera más fácil de crear una canalización es usar el **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="f2808-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f2808-121">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="f2808-122">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="f2808-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f2808-123">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="f2808-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f2808-124">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="f2808-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="f2808-125">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="f2808-125">Create a **data factory**.</span></span> <span data-ttu-id="f2808-126">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="f2808-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="f2808-127">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="f2808-128">Por ejemplo, si va a copiar datos de una base de datos de SQL Server a una instancia de Azure Blob Storage, cree dos servicios vinculados para vincular su base de datos de SQL Server y su cuenta de Azure Storage a su fábrica de datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="f2808-129">Para información sobre las propiedades de los servicios vinculados que son específicas de la base de datos de SQL Server, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="f2808-130">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="f2808-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="f2808-131">En el ejemplo mencionado en el último paso, se crea un conjunto de datos para especificar la tabla SQL en la base de datos SQL Server que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2808-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="f2808-132">Además, se crea otro conjunto de datos para especificar el contenedor de blobs y la carpeta que contiene los datos copiados desde la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2808-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="f2808-133">Para información sobre las propiedades del conjunto de datos que son específicas de la base de datos de SQL Server, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="f2808-134">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="f2808-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="f2808-135">En el ejemplo mencionado anteriormente, se usa SqlSource como origen y BlobSink como receptor para la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="f2808-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="f2808-136">De igual forma, si va a copiar de Azure Blob Storage a una base de datos de SQL Server, usará BlobSource y SqlSink en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="f2808-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="f2808-137">Para información sobre las propiedades de actividad de copia que son específicas de la base de datos de SQL Server, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="f2808-138">Para más información sobre cómo usar un almacén de datos como origen o receptor, haga clic en el vínculo de la sección anterior para su almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="f2808-139">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="f2808-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f2808-140">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f2808-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f2808-141">Para ver ejemplos con definiciones JSON de entidades de Data Factory que se usan para copiar datos a/desde una base de datos SQL Server local, consulte la sección [Ejemplos de JSON](#json-examples-for-copying-data-from-and-to-sql-server) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f2808-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="f2808-142">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de SQL Server:</span><span class="sxs-lookup"><span data-stu-id="f2808-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="f2808-143">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="f2808-143">Linked service properties</span></span>
<span data-ttu-id="f2808-144">Se crea un servicio vinculado de tipo **OnPremisesSqlServer** para vincular una base de datos SQL Server local a una instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f2808-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="f2808-145">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="f2808-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="f2808-146">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio SQL Server vinculado.</span><span class="sxs-lookup"><span data-stu-id="f2808-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="f2808-147">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f2808-147">Property</span></span> | <span data-ttu-id="f2808-148">Descripción</span><span class="sxs-lookup"><span data-stu-id="f2808-148">Description</span></span> | <span data-ttu-id="f2808-149">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f2808-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2808-150">type</span><span class="sxs-lookup"><span data-stu-id="f2808-150">type</span></span> |<span data-ttu-id="f2808-151">La propiedad type se debe establecer en **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="f2808-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="f2808-152">Sí</span><span class="sxs-lookup"><span data-stu-id="f2808-152">Yes</span></span> |
| <span data-ttu-id="f2808-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="f2808-153">connectionString</span></span> |<span data-ttu-id="f2808-154">Especifique la información de connectionString necesaria para conectarse a la Base de datos SQL Server local mediante autenticación de SQL o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="f2808-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="f2808-155">Sí</span><span class="sxs-lookup"><span data-stu-id="f2808-155">Yes</span></span> |
| <span data-ttu-id="f2808-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f2808-156">gatewayName</span></span> |<span data-ttu-id="f2808-157">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la Base de datos SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="f2808-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="f2808-158">Sí</span><span class="sxs-lookup"><span data-stu-id="f2808-158">Yes</span></span> |
| <span data-ttu-id="f2808-159">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f2808-159">username</span></span> |<span data-ttu-id="f2808-160">Especifique el nombre de usuario si usa la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="f2808-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="f2808-161">Ejemplo: **nombreDeDominio\\nombreDeUsuario**.</span><span class="sxs-lookup"><span data-stu-id="f2808-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="f2808-162">No</span><span class="sxs-lookup"><span data-stu-id="f2808-162">No</span></span> |
| <span data-ttu-id="f2808-163">contraseña</span><span class="sxs-lookup"><span data-stu-id="f2808-163">password</span></span> |<span data-ttu-id="f2808-164">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="f2808-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="f2808-165">No</span><span class="sxs-lookup"><span data-stu-id="f2808-165">No</span></span> |

<span data-ttu-id="f2808-166">Puede cifrar las credenciales con el cmdlet **New-AzureRmDataFactoryEncryptValue** y usarlas en la cadena de conexión, como se muestra en el ejemplo siguiente (propiedad **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="f2808-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="f2808-167">Muestras</span><span class="sxs-lookup"><span data-stu-id="f2808-167">Samples</span></span>
<span data-ttu-id="f2808-168">**JSON para usar autenticación de SQL**</span><span class="sxs-lookup"><span data-stu-id="f2808-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="f2808-169">**JSON para usar autenticación de Windows**</span><span class="sxs-lookup"><span data-stu-id="f2808-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="f2808-170">Data Management Gateway suplantará la cuenta de usuario especificada para conectarse a la base de datos de SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="f2808-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="f2808-171">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="f2808-171">Dataset properties</span></span>
<span data-ttu-id="f2808-172">En los ejemplos se ha usado un conjunto de datos de tipo **SqlServerTable** para representar una tabla en una base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2808-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="f2808-173">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f2808-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f2808-174">Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (SQL Server, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="f2808-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f2808-175">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f2808-176">La sección **typeProperties** del conjunto de datos de tipo **SqlServerTable** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="f2808-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="f2808-177">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f2808-177">Property</span></span> | <span data-ttu-id="f2808-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="f2808-178">Description</span></span> | <span data-ttu-id="f2808-179">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f2808-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2808-180">tableName</span><span class="sxs-lookup"><span data-stu-id="f2808-180">tableName</span></span> |<span data-ttu-id="f2808-181">Nombre de la tabla en la instancia de base de datos de SQL Server a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="f2808-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="f2808-182">Sí</span><span class="sxs-lookup"><span data-stu-id="f2808-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f2808-183">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="f2808-183">Copy activity properties</span></span>
<span data-ttu-id="f2808-184">Si va a mover datos desde una base de datos de SQL Server, establezca el tipo de origen en la actividad de copia en **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="f2808-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="f2808-185">De igual forma, si va a mover datos a una base de datos de SQL Server, establezca el tipo de receptor en la actividad de copia en **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="f2808-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="f2808-186">Esta sección proporciona una lista de propiedades admitidas por SqlSource y SqlSink.</span><span class="sxs-lookup"><span data-stu-id="f2808-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="f2808-187">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f2808-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f2808-188">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="f2808-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="f2808-189">La actividad de copia toma solo una entrada y genera una única salida.</span><span class="sxs-lookup"><span data-stu-id="f2808-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="f2808-190">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="f2808-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="f2808-191">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="f2808-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="f2808-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="f2808-192">SqlSource</span></span>
<span data-ttu-id="f2808-193">Cuando el origen es una actividad de copia de tipo **SqlSource**, están disponibles las propiedades siguientes en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="f2808-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="f2808-194">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f2808-194">Property</span></span> | <span data-ttu-id="f2808-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="f2808-195">Description</span></span> | <span data-ttu-id="f2808-196">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f2808-196">Allowed values</span></span> | <span data-ttu-id="f2808-197">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f2808-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2808-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="f2808-198">sqlReaderQuery</span></span> |<span data-ttu-id="f2808-199">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-199">Use the custom query to read data.</span></span> |<span data-ttu-id="f2808-200">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="f2808-200">SQL query string.</span></span> <span data-ttu-id="f2808-201">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="f2808-201">For example: select * from MyTable.</span></span> <span data-ttu-id="f2808-202">Es posible hacer referencia a varias tablas de la base de datos a la que hace referencia el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2808-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="f2808-203">Si no se especifica, la instrucción SQL que se ejecuta: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="f2808-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="f2808-204">No</span><span class="sxs-lookup"><span data-stu-id="f2808-204">No</span></span> |
| <span data-ttu-id="f2808-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="f2808-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="f2808-206">Nombre del procedimiento almacenado que lee datos de la tabla de origen.</span><span class="sxs-lookup"><span data-stu-id="f2808-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="f2808-207">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2808-207">Name of the stored procedure.</span></span> <span data-ttu-id="f2808-208">La última instrucción SQL debe ser una instrucción SELECT del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2808-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="f2808-209">No</span><span class="sxs-lookup"><span data-stu-id="f2808-209">No</span></span> |
| <span data-ttu-id="f2808-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="f2808-210">storedProcedureParameters</span></span> |<span data-ttu-id="f2808-211">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2808-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="f2808-212">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="f2808-212">Name/value pairs.</span></span> <span data-ttu-id="f2808-213">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2808-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="f2808-214">No</span><span class="sxs-lookup"><span data-stu-id="f2808-214">No</span></span> |

<span data-ttu-id="f2808-215">Si se especifica **sqlReaderQuery** para SqlSource, la actividad de copia ejecuta la consulta en el origen de Base de datos SQL de Azure para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="f2808-216">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="f2808-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="f2808-217">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura se usan para crear una consulta Select para ejecutarla en Base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2808-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="f2808-218">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="f2808-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="f2808-219">Cuando use **sqlReaderStoredProcedureName**, necesitará especificar un valor para la propiedad **tableName** del conjunto de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="f2808-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="f2808-220">Pero no se ha realizado ninguna validación en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="f2808-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="f2808-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="f2808-221">SqlSink</span></span>
<span data-ttu-id="f2808-222">**SqlSink** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="f2808-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="f2808-223">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f2808-223">Property</span></span> | <span data-ttu-id="f2808-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="f2808-224">Description</span></span> | <span data-ttu-id="f2808-225">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f2808-225">Allowed values</span></span> | <span data-ttu-id="f2808-226">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f2808-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2808-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="f2808-227">writeBatchTimeout</span></span> |<span data-ttu-id="f2808-228">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="f2808-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="f2808-229">timespan</span><span class="sxs-lookup"><span data-stu-id="f2808-229">timespan</span></span><br/><br/> <span data-ttu-id="f2808-230">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="f2808-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="f2808-231">No</span><span class="sxs-lookup"><span data-stu-id="f2808-231">No</span></span> |
| <span data-ttu-id="f2808-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f2808-232">writeBatchSize</span></span> |<span data-ttu-id="f2808-233">Inserta datos en la tabla SQL cuando el tamaño del búfer alcanza el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="f2808-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="f2808-234">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="f2808-234">Integer (number of rows)</span></span> |<span data-ttu-id="f2808-235">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="f2808-235">No (default: 10000)</span></span> |
| <span data-ttu-id="f2808-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="f2808-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="f2808-237">Especifique la consulta para que la actividad de copia se ejecute de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="f2808-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="f2808-238">Para más información, consulte la sección [copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="f2808-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="f2808-239">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="f2808-239">A query statement.</span></span> |<span data-ttu-id="f2808-240">No</span><span class="sxs-lookup"><span data-stu-id="f2808-240">No</span></span> |
| <span data-ttu-id="f2808-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="f2808-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="f2808-242">Especifique el nombre de columna para que la rellene la actividad de copia con un identificador de segmentos generado automáticamente, que se usará para limpiar los datos de un segmento específico cuando se vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="f2808-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="f2808-243">Para más información, consulte la sección [copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="f2808-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="f2808-244">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="f2808-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="f2808-245">No</span><span class="sxs-lookup"><span data-stu-id="f2808-245">No</span></span> |
| <span data-ttu-id="f2808-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="f2808-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="f2808-247">Nombre del procedimiento almacenado que actualiza e inserta (operación de upsert) datos en la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="f2808-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="f2808-248">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2808-248">Name of the stored procedure.</span></span> |<span data-ttu-id="f2808-249">No</span><span class="sxs-lookup"><span data-stu-id="f2808-249">No</span></span> |
| <span data-ttu-id="f2808-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="f2808-250">storedProcedureParameters</span></span> |<span data-ttu-id="f2808-251">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2808-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="f2808-252">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="f2808-252">Name/value pairs.</span></span> <span data-ttu-id="f2808-253">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2808-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="f2808-254">No</span><span class="sxs-lookup"><span data-stu-id="f2808-254">No</span></span> |
| <span data-ttu-id="f2808-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="f2808-255">sqlWriterTableType</span></span> |<span data-ttu-id="f2808-256">Especifique el nombre del tipo de tabla que se usará en el procedimiento almacenado anterior.</span><span class="sxs-lookup"><span data-stu-id="f2808-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="f2808-257">La actividad de copia dispone que los datos que se mueven estén disponibles en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="f2808-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="f2808-258">El código de procedimiento almacenado puede combinar los datos copiados con datos existentes.</span><span class="sxs-lookup"><span data-stu-id="f2808-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="f2808-259">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="f2808-259">A table type name.</span></span> |<span data-ttu-id="f2808-260">No</span><span class="sxs-lookup"><span data-stu-id="f2808-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="f2808-261">Ejemplos JSON para copiar datos desde y hacia SQL Server</span><span class="sxs-lookup"><span data-stu-id="f2808-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="f2808-262">En los siguientes ejemplos se proporcionan definiciones JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f2808-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f2808-263">En los siguientes ejemplos, se muestra cómo copiar datos entre SQL Server y Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2808-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="f2808-264">Sin embargo, los datos se pueden copiar **directamente** de cualquiera de los orígenes a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2808-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="f2808-265">Ejemplo: Copia de datos de SQL Server a Blob de Azure</span><span class="sxs-lookup"><span data-stu-id="f2808-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="f2808-266">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="f2808-266">The following sample shows:</span></span>

1. <span data-ttu-id="f2808-267">Un servicio vinculado de tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="f2808-268">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="f2808-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f2808-269">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="f2808-270">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f2808-271">La [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f2808-272">El ejemplo copia los datos de la serie temporal desde una tabla de SQL Server a un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="f2808-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="f2808-273">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="f2808-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f2808-274">En primer lugar, configure Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f2808-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="f2808-275">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="f2808-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f2808-276">**Servicio vinculado de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="f2808-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="f2808-277">**Servicio vinculado de almacenamiento de blobs de Azure**</span><span class="sxs-lookup"><span data-stu-id="f2808-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="f2808-278">**Conjunto de datos de entrada de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="f2808-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="f2808-279">El ejemplo supone que ha creado una tabla "MyTable" en SQL Server y que contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="f2808-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="f2808-280">Puede consultar en varias tablas dentro de la misma base de datos mediante un único conjunto de datos, pero se debe utilizar una única tabla para typeProperty tableName del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="f2808-281">Si se establece external: true, se informa al servicio Data Factory de que el conjunto de datos es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="f2808-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="f2808-282">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="f2808-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="f2808-283">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f2808-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f2808-284">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="f2808-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f2808-285">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="f2808-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="f2808-286">**Canalización con actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="f2808-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="f2808-287">La canalización contiene una actividad de copia que está configurada para usar estos conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="f2808-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f2808-288">En la definición de la canalización JSON, el tipo **source** se establece en **SqlSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f2808-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f2808-289">La consulta SQL especificada para la propiedad **SqlReaderQuery** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="f2808-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="f2808-290">En este ejemplo, **sqlReaderQuery** se especifica para SqlSource.</span><span class="sxs-lookup"><span data-stu-id="f2808-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="f2808-291">La actividad de copia ejecuta esta consulta en el origen de Base de datos de SQL Server para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="f2808-292">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="f2808-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="f2808-293">sqlReaderQuery puede hacer referencia a varias tablas de la base de datos a la que hace referencia el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2808-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="f2808-294">No se limita exclusivamente a la tabla establecida como typeProperty tableName del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f2808-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="f2808-295">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura se usan para crear una consulta Select para ejecutarla en Base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2808-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="f2808-296">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="f2808-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="f2808-297">Vea la sección [Sql Source](#sqlsource) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para obtener la lista de propiedades admitidas por SqlSource y BlobSink.</span><span class="sxs-lookup"><span data-stu-id="f2808-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="f2808-298">Ejemplo: Copia de datos de Blob de Azure a SQL Server</span><span class="sxs-lookup"><span data-stu-id="f2808-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="f2808-299">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="f2808-299">The following sample shows:</span></span>

1. <span data-ttu-id="f2808-300">El servicio vinculado de tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="f2808-301">El servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f2808-302">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f2808-303">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f2808-304">La [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="f2808-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="f2808-305">El ejemplo copia los datos de la serie temporal desde un blob de Azure a una tabla de SQL Server cada hora.</span><span class="sxs-lookup"><span data-stu-id="f2808-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="f2808-306">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="f2808-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f2808-307">**Servicio vinculado de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="f2808-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="f2808-308">**Servicio vinculado de almacenamiento de blobs de Azure**</span><span class="sxs-lookup"><span data-stu-id="f2808-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="f2808-309">**Conjunto de datos de entrada de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="f2808-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="f2808-310">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f2808-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f2808-311">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="f2808-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f2808-312">La ruta de acceso de la carpeta usa la parte year, month y day de la hora de inicio y el nombre de archivo, la parte hour.</span><span class="sxs-lookup"><span data-stu-id="f2808-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="f2808-313">El valor external: true informa al servicio Data Factory de que el conjunto de datos es externo a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="f2808-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="f2808-314">**Conjunto de datos de salida de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="f2808-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="f2808-315">El ejemplo copia los datos a una tabla denominada "MyTable" en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2808-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="f2808-316">Cree la tabla en SQL Server con el mismo número de columnas que espera que contenga el archivo CSV de blob.</span><span class="sxs-lookup"><span data-stu-id="f2808-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="f2808-317">Se agregan nuevas filas a la tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="f2808-317">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="f2808-318">**Canalización con actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="f2808-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="f2808-319">La canalización contiene una actividad de copia que está configurada para usar estos conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="f2808-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f2808-320">En la definición de JSON de canalización, el tipo **source** se establece en **BlobSource** y el tipo **sink**, en **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="f2808-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="f2808-321">Solución de problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="f2808-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="f2808-322">Configure su SQL Server para que acepte conexiones remotas.</span><span class="sxs-lookup"><span data-stu-id="f2808-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="f2808-323">Inicie **SQL Server Management Studio**, haga clic con el botón derecho en **Servidor** y después en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="f2808-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="f2808-324">Seleccione **Conexiones** en la lista y active **Permitir conexiones remotas con este servidor**.</span><span class="sxs-lookup"><span data-stu-id="f2808-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Habilitar conexiones remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="f2808-326">Consulte los pasos detallados de [Configurar la opción de configuración del servidor Acceso remoto](https://msdn.microsoft.com/library/ms191464.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f2808-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="f2808-327">Inicie el **Administrador de configuración de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f2808-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="f2808-328">Expanda **Configuración de red de SQL Server** para la instancia que desee y seleccione **Protocols for MSSQLSERVER** (Protocolos para MSSQLSERVER).</span><span class="sxs-lookup"><span data-stu-id="f2808-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="f2808-329">Debería ver protocolos en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="f2808-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="f2808-330">Para habilitar TCP/IP, haga clic con el botón derecho en **TCP/IP** y haga clic en **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="f2808-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Habilitar TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="f2808-332">Consulte [Habilitar o deshabilitar un protocolo de red de servidor](https://msdn.microsoft.com/library/ms191294.aspx) para ver información y maneras alternativas de habilitar el protocolo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="f2808-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="f2808-333">En la misma ventana, haga doble clic en **TCP/IP** para abrir la ventana **TCP/IP Properties** (Propiedades de TCP/IP).</span><span class="sxs-lookup"><span data-stu-id="f2808-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="f2808-334">Cambie a la pestaña **Direcciones IP** .</span><span class="sxs-lookup"><span data-stu-id="f2808-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="f2808-335">Desplácese hacia abajo hasta la sección **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="f2808-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="f2808-336">Anote el valor de **Puerto TCP** (el valor predeterminado es **1433**).</span><span class="sxs-lookup"><span data-stu-id="f2808-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="f2808-337">Cree una **regla del Firewall de Windows** en la máquina para permitir el tráfico entrante a través de este puerto.</span><span class="sxs-lookup"><span data-stu-id="f2808-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="f2808-338">**Compruebe la conexión**: use SQL Server Management Studio en una máquina diferente para conectarse a SQL Server con el nombre completo.</span><span class="sxs-lookup"><span data-stu-id="f2808-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="f2808-339">Por ejemplo: <machine><domain>.corp<company>.com,1433.</span><span class="sxs-lookup"><span data-stu-id="f2808-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="f2808-340">Consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="f2808-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="f2808-341">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f2808-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="f2808-342">Columnas de identidad en la base de datos de destino</span><span class="sxs-lookup"><span data-stu-id="f2808-342">Identity columns in the target database</span></span>
<span data-ttu-id="f2808-343">En esta sección se proporciona un ejemplo para copiar datos de una tabla de origen sin una columna de identidad en una tabla de destino con una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="f2808-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="f2808-344">**Tabla de origen:**</span><span class="sxs-lookup"><span data-stu-id="f2808-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="f2808-345">**Tabla de destino:**</span><span class="sxs-lookup"><span data-stu-id="f2808-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="f2808-346">Observe que la tabla de destino tiene una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="f2808-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="f2808-347">**Definición de JSON del conjunto de datos de origen**</span><span class="sxs-lookup"><span data-stu-id="f2808-347">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="f2808-348">**Definición de JSON del conjunto de datos de destino**</span><span class="sxs-lookup"><span data-stu-id="f2808-348">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="f2808-349">Tenga en cuenta que la tabla de origen y de destino tienen un esquema diferente (el destino tiene una columna adicional con identidad).</span><span class="sxs-lookup"><span data-stu-id="f2808-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="f2808-350">En este escenario, debe especificar la propiedad **structure** de la definición del conjunto de datos de destino, que no incluye la columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="f2808-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="f2808-351">Invocación del procedimiento almacenado desde el receptor de SQL</span><span class="sxs-lookup"><span data-stu-id="f2808-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="f2808-352">Para ver un ejemplo de invocación de un procedimiento almacenado desde el receptor de SQL en una actividad de copia de una canalización, consulte el artículo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocación de un procedimiento almacenado desde el receptor de SQL en la actividad de copia).</span><span class="sxs-lookup"><span data-stu-id="f2808-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="f2808-353">Asignación de tipos para SQL Server</span><span class="sxs-lookup"><span data-stu-id="f2808-353">Type mapping for SQL server</span></span>
<span data-ttu-id="f2808-354">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="f2808-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="f2808-355">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="f2808-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f2808-356">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="f2808-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f2808-357">Al mover datos a SQL Server y desde este, se usan las siguientes asignaciones del tipo SQL al tipo .NET, y viceversa.</span><span class="sxs-lookup"><span data-stu-id="f2808-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="f2808-358">La asignación es igual que la asignación de tipo de datos de SQL Server para ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="f2808-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="f2808-359">Tipo de motor de base de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="f2808-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="f2808-360">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f2808-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="f2808-361">bigint</span><span class="sxs-lookup"><span data-stu-id="f2808-361">bigint</span></span> |<span data-ttu-id="f2808-362">Int64</span><span class="sxs-lookup"><span data-stu-id="f2808-362">Int64</span></span> |
| <span data-ttu-id="f2808-363">binary</span><span class="sxs-lookup"><span data-stu-id="f2808-363">binary</span></span> |<span data-ttu-id="f2808-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f2808-364">Byte[]</span></span> |
| <span data-ttu-id="f2808-365">bit</span><span class="sxs-lookup"><span data-stu-id="f2808-365">bit</span></span> |<span data-ttu-id="f2808-366">Booleano</span><span class="sxs-lookup"><span data-stu-id="f2808-366">Boolean</span></span> |
| <span data-ttu-id="f2808-367">char</span><span class="sxs-lookup"><span data-stu-id="f2808-367">char</span></span> |<span data-ttu-id="f2808-368">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f2808-368">String, Char[]</span></span> |
| <span data-ttu-id="f2808-369">fecha</span><span class="sxs-lookup"><span data-stu-id="f2808-369">date</span></span> |<span data-ttu-id="f2808-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="f2808-370">DateTime</span></span> |
| <span data-ttu-id="f2808-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="f2808-371">Datetime</span></span> |<span data-ttu-id="f2808-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="f2808-372">DateTime</span></span> |
| <span data-ttu-id="f2808-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="f2808-373">datetime2</span></span> |<span data-ttu-id="f2808-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="f2808-374">DateTime</span></span> |
| <span data-ttu-id="f2808-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f2808-375">Datetimeoffset</span></span> |<span data-ttu-id="f2808-376">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f2808-376">DateTimeOffset</span></span> |
| <span data-ttu-id="f2808-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="f2808-377">Decimal</span></span> |<span data-ttu-id="f2808-378">Decimal</span><span class="sxs-lookup"><span data-stu-id="f2808-378">Decimal</span></span> |
| <span data-ttu-id="f2808-379">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="f2808-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="f2808-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f2808-380">Byte[]</span></span> |
| <span data-ttu-id="f2808-381">Float</span><span class="sxs-lookup"><span data-stu-id="f2808-381">Float</span></span> |<span data-ttu-id="f2808-382">Doble</span><span class="sxs-lookup"><span data-stu-id="f2808-382">Double</span></span> |
| <span data-ttu-id="f2808-383">imagen</span><span class="sxs-lookup"><span data-stu-id="f2808-383">image</span></span> |<span data-ttu-id="f2808-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f2808-384">Byte[]</span></span> |
| <span data-ttu-id="f2808-385">int</span><span class="sxs-lookup"><span data-stu-id="f2808-385">int</span></span> |<span data-ttu-id="f2808-386">Int32</span><span class="sxs-lookup"><span data-stu-id="f2808-386">Int32</span></span> |
| <span data-ttu-id="f2808-387">money</span><span class="sxs-lookup"><span data-stu-id="f2808-387">money</span></span> |<span data-ttu-id="f2808-388">Decimal</span><span class="sxs-lookup"><span data-stu-id="f2808-388">Decimal</span></span> |
| <span data-ttu-id="f2808-389">nchar</span><span class="sxs-lookup"><span data-stu-id="f2808-389">nchar</span></span> |<span data-ttu-id="f2808-390">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f2808-390">String, Char[]</span></span> |
| <span data-ttu-id="f2808-391">ntext</span><span class="sxs-lookup"><span data-stu-id="f2808-391">ntext</span></span> |<span data-ttu-id="f2808-392">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f2808-392">String, Char[]</span></span> |
| <span data-ttu-id="f2808-393">numeric</span><span class="sxs-lookup"><span data-stu-id="f2808-393">numeric</span></span> |<span data-ttu-id="f2808-394">Decimal</span><span class="sxs-lookup"><span data-stu-id="f2808-394">Decimal</span></span> |
| <span data-ttu-id="f2808-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="f2808-395">nvarchar</span></span> |<span data-ttu-id="f2808-396">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f2808-396">String, Char[]</span></span> |
| <span data-ttu-id="f2808-397">real</span><span class="sxs-lookup"><span data-stu-id="f2808-397">real</span></span> |<span data-ttu-id="f2808-398">Single</span><span class="sxs-lookup"><span data-stu-id="f2808-398">Single</span></span> |
| <span data-ttu-id="f2808-399">rowversion</span><span class="sxs-lookup"><span data-stu-id="f2808-399">rowversion</span></span> |<span data-ttu-id="f2808-400">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f2808-400">Byte[]</span></span> |
| <span data-ttu-id="f2808-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="f2808-401">smalldatetime</span></span> |<span data-ttu-id="f2808-402">DateTime</span><span class="sxs-lookup"><span data-stu-id="f2808-402">DateTime</span></span> |
| <span data-ttu-id="f2808-403">smallint</span><span class="sxs-lookup"><span data-stu-id="f2808-403">smallint</span></span> |<span data-ttu-id="f2808-404">Int16</span><span class="sxs-lookup"><span data-stu-id="f2808-404">Int16</span></span> |
| <span data-ttu-id="f2808-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="f2808-405">smallmoney</span></span> |<span data-ttu-id="f2808-406">Decimal</span><span class="sxs-lookup"><span data-stu-id="f2808-406">Decimal</span></span> |
| <span data-ttu-id="f2808-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="f2808-407">sql_variant</span></span> |<span data-ttu-id="f2808-408">Object *</span><span class="sxs-lookup"><span data-stu-id="f2808-408">Object *</span></span> |
| <span data-ttu-id="f2808-409">text</span><span class="sxs-lookup"><span data-stu-id="f2808-409">text</span></span> |<span data-ttu-id="f2808-410">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f2808-410">String, Char[]</span></span> |
| <span data-ttu-id="f2808-411">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="f2808-411">time</span></span> |<span data-ttu-id="f2808-412">timespan</span><span class="sxs-lookup"><span data-stu-id="f2808-412">TimeSpan</span></span> |
| <span data-ttu-id="f2808-413">timestamp</span><span class="sxs-lookup"><span data-stu-id="f2808-413">timestamp</span></span> |<span data-ttu-id="f2808-414">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f2808-414">Byte[]</span></span> |
| <span data-ttu-id="f2808-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="f2808-415">tinyint</span></span> |<span data-ttu-id="f2808-416">Byte</span><span class="sxs-lookup"><span data-stu-id="f2808-416">Byte</span></span> |
| <span data-ttu-id="f2808-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="f2808-417">uniqueidentifier</span></span> |<span data-ttu-id="f2808-418">Guid</span><span class="sxs-lookup"><span data-stu-id="f2808-418">Guid</span></span> |
| <span data-ttu-id="f2808-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="f2808-419">varbinary</span></span> |<span data-ttu-id="f2808-420">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f2808-420">Byte[]</span></span> |
| <span data-ttu-id="f2808-421">varchar</span><span class="sxs-lookup"><span data-stu-id="f2808-421">varchar</span></span> |<span data-ttu-id="f2808-422">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f2808-422">String, Char[]</span></span> |
| <span data-ttu-id="f2808-423">xml</span><span class="sxs-lookup"><span data-stu-id="f2808-423">xml</span></span> |<span data-ttu-id="f2808-424">xml</span><span class="sxs-lookup"><span data-stu-id="f2808-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="f2808-425">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="f2808-425">Mapping source to sink columns</span></span>
<span data-ttu-id="f2808-426">Para asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte el artículo sobre la [asignación de columnas de conjuntos de datos en Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f2808-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="f2808-427">Copia repetible</span><span class="sxs-lookup"><span data-stu-id="f2808-427">Repeatable copy</span></span>
<span data-ttu-id="f2808-428">Cuando se copian datos en SQL Server Database, la actividad de copia anexa datos a la tabla receptora de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f2808-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="f2808-429">Para ejecutar una semántica UPSERT en su lugar, consulte el artículo [Escritura repetible en SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="f2808-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="f2808-430">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="f2808-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="f2808-431">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="f2808-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f2808-432">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="f2808-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f2808-433">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="f2808-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f2808-434">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f2808-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f2808-435">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="f2808-435">Performance and Tuning</span></span>
<span data-ttu-id="f2808-436">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="f2808-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
