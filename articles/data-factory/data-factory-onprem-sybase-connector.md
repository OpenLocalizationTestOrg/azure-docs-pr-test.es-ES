---
title: Movimiento de datos de Sybase mediante Azure Data Factory | Microsoft Docs
description: "Obtenga información acerca de cómo mover los datos de la base de datos de Sybase mediante Factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="fc335-103">Movimiento de datos de Sybase mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="fc335-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="fc335-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos desde una base de datos Sybase local.</span><span class="sxs-lookup"><span data-stu-id="fc335-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="fc335-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="fc335-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="fc335-106">Puede copiar datos de un almacén de datos de Sybase local a cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="fc335-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="fc335-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como receptores.</span><span class="sxs-lookup"><span data-stu-id="fc335-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="fc335-108">Data Factory solo admite actualmente el movimiento de datos de un almacén de datos de Sybase a otros almacenes de datos, pero no viceversa.</span><span class="sxs-lookup"><span data-stu-id="fc335-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fc335-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fc335-109">Prerequisites</span></span>
<span data-ttu-id="fc335-110">El servicio Factoría de datos admite la conexión a orígenes de Sybase locales mediante Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="fc335-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="fc335-111">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="fc335-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="fc335-112">La puerta de enlace es necesaria incluso si la base de datos Sybase está hospedada en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc335-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="fc335-113">Puede instalar la puerta de enlace en la misma máquina virtual de IaaS como almacén de datos o en una máquina virtual diferente, siempre y cuando la puerta de enlace se pueda conectar a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="fc335-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="fc335-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="fc335-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="fc335-115">Supported versions and installation</span></span>
<span data-ttu-id="fc335-116">Para que Data Management Gateway se conecte a la Base de datos Sybase, es preciso instalar el [proveedor de datos para Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 o posterior en el mismo sistema que Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="fc335-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="fc335-117">Se admite la versión 16 de Sybase o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="fc335-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fc335-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="fc335-118">Getting started</span></span>
<span data-ttu-id="fc335-119">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="fc335-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="fc335-120">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="fc335-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="fc335-121">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="fc335-122">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="fc335-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fc335-123">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="fc335-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fc335-124">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="fc335-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="fc335-125">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="fc335-126">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="fc335-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="fc335-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="fc335-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fc335-128">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="fc335-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="fc335-129">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="fc335-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="fc335-130">Si desea obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan con el fin de copiar los datos desde un almacén de datos de Sybase local, consulte la sección [Ejemplo de JSON: Copia de datos de Sybase a un blob de Azure](#json-example-copy-data-from-sybase-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="fc335-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="fc335-131">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos de Sybase:</span><span class="sxs-lookup"><span data-stu-id="fc335-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fc335-132">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="fc335-132">Linked service properties</span></span>
<span data-ttu-id="fc335-133">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos al servicio vinculado de Sybase.</span><span class="sxs-lookup"><span data-stu-id="fc335-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="fc335-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fc335-134">Property</span></span> | <span data-ttu-id="fc335-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="fc335-135">Description</span></span> | <span data-ttu-id="fc335-136">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fc335-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc335-137">type</span><span class="sxs-lookup"><span data-stu-id="fc335-137">type</span></span> |<span data-ttu-id="fc335-138">La propiedad type debe establecerse en: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="fc335-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="fc335-139">Sí</span><span class="sxs-lookup"><span data-stu-id="fc335-139">Yes</span></span> |
| <span data-ttu-id="fc335-140">server</span><span class="sxs-lookup"><span data-stu-id="fc335-140">server</span></span> |<span data-ttu-id="fc335-141">Nombre del servidor de Sybase.</span><span class="sxs-lookup"><span data-stu-id="fc335-141">Name of the Sybase server.</span></span> |<span data-ttu-id="fc335-142">Sí</span><span class="sxs-lookup"><span data-stu-id="fc335-142">Yes</span></span> |
| <span data-ttu-id="fc335-143">database</span><span class="sxs-lookup"><span data-stu-id="fc335-143">database</span></span> |<span data-ttu-id="fc335-144">Nombre de la base de datos Sybase.</span><span class="sxs-lookup"><span data-stu-id="fc335-144">Name of the Sybase database.</span></span> |<span data-ttu-id="fc335-145">Sí</span><span class="sxs-lookup"><span data-stu-id="fc335-145">Yes</span></span> |
| <span data-ttu-id="fc335-146">schema</span><span class="sxs-lookup"><span data-stu-id="fc335-146">schema</span></span> |<span data-ttu-id="fc335-147">Nombre del esquema de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-147">Name of the schema in the database.</span></span> |<span data-ttu-id="fc335-148">No</span><span class="sxs-lookup"><span data-stu-id="fc335-148">No</span></span> |
| <span data-ttu-id="fc335-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fc335-149">authenticationType</span></span> |<span data-ttu-id="fc335-150">Tipo de autenticación usado para conectarse a la base de datos Sybase.</span><span class="sxs-lookup"><span data-stu-id="fc335-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="fc335-151">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="fc335-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="fc335-152">Sí</span><span class="sxs-lookup"><span data-stu-id="fc335-152">Yes</span></span> |
| <span data-ttu-id="fc335-153">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="fc335-153">username</span></span> |<span data-ttu-id="fc335-154">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="fc335-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="fc335-155">No</span><span class="sxs-lookup"><span data-stu-id="fc335-155">No</span></span> |
| <span data-ttu-id="fc335-156">contraseña</span><span class="sxs-lookup"><span data-stu-id="fc335-156">password</span></span> |<span data-ttu-id="fc335-157">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="fc335-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="fc335-158">No</span><span class="sxs-lookup"><span data-stu-id="fc335-158">No</span></span> |
| <span data-ttu-id="fc335-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fc335-159">gatewayName</span></span> |<span data-ttu-id="fc335-160">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos de Sybase local.</span><span class="sxs-lookup"><span data-stu-id="fc335-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="fc335-161">Sí</span><span class="sxs-lookup"><span data-stu-id="fc335-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="fc335-162">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="fc335-162">Dataset properties</span></span>
<span data-ttu-id="fc335-163">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="fc335-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fc335-164">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="fc335-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fc335-165">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="fc335-166">La sección **typeProperties** del conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de Sybase) tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="fc335-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="fc335-167">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fc335-167">Property</span></span> | <span data-ttu-id="fc335-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="fc335-168">Description</span></span> | <span data-ttu-id="fc335-169">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fc335-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc335-170">tableName</span><span class="sxs-lookup"><span data-stu-id="fc335-170">tableName</span></span> |<span data-ttu-id="fc335-171">Nombre de la tabla en la instancia de Base de datos Sybase a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="fc335-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="fc335-172">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="fc335-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fc335-173">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="fc335-173">Copy activity properties</span></span>
<span data-ttu-id="fc335-174">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="fc335-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fc335-175">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="fc335-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="fc335-176">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="fc335-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="fc335-177">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="fc335-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="fc335-178">Cuando el origen es de tipo **RelationalSource** (lo que incluye Sybase), están disponibles las propiedades siguientes en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="fc335-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="fc335-179">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fc335-179">Property</span></span> | <span data-ttu-id="fc335-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="fc335-180">Description</span></span> | <span data-ttu-id="fc335-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="fc335-181">Allowed values</span></span> | <span data-ttu-id="fc335-182">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="fc335-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc335-183">query</span><span class="sxs-lookup"><span data-stu-id="fc335-183">query</span></span> |<span data-ttu-id="fc335-184">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-184">Use the custom query to read data.</span></span> |<span data-ttu-id="fc335-185">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="fc335-185">SQL query string.</span></span> <span data-ttu-id="fc335-186">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="fc335-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="fc335-187">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="fc335-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="fc335-188">Ejemplo de JSON: Copia de datos de Sybase a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="fc335-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="fc335-189">En el siguiente ejemplo, se proporcionan definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fc335-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fc335-190">Se muestra cómo copiar datos desde la base de datos Sybase al almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc335-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="fc335-191">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc335-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="fc335-192">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="fc335-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="fc335-193">Un servicio vinculado de tipo [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fc335-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="fc335-194">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fc335-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fc335-195">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fc335-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="fc335-196">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fc335-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fc335-197">La [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fc335-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fc335-198">El ejemplo copia cada hora los datos de un resultado de consulta de la base de datos Sybase en un blob.</span><span class="sxs-lookup"><span data-stu-id="fc335-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="fc335-199">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="fc335-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="fc335-200">En primer lugar, configure Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="fc335-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="fc335-201">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="fc335-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fc335-202">**Servicio vinculado de Sybase:**</span><span class="sxs-lookup"><span data-stu-id="fc335-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="fc335-203">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="fc335-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="fc335-204">**Conjunto de datos de entrada de Sybase:**</span><span class="sxs-lookup"><span data-stu-id="fc335-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="fc335-205">El ejemplo supone que ha creado una tabla "MyTable" en Sybase y que contiene una columna denominada "timestamp" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="fc335-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="fc335-206">Si se establece "external": true, se informa al servicio Data Factory de que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="fc335-207">Tenga en cuenta que el **tipo** del servicio vinculado se establece en: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="fc335-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="fc335-208">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="fc335-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fc335-209">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="fc335-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fc335-210">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="fc335-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fc335-211">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="fc335-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="fc335-212">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="fc335-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="fc335-213">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="fc335-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="fc335-214">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fc335-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="fc335-215">La consulta SQL especificada para la propiedad **query** selecciona los datos de la tabla DBA.Orders de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="fc335-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="fc335-216">Asignación de tipos para Sybase</span><span class="sxs-lookup"><span data-stu-id="fc335-216">Type mapping for Sybase</span></span>
<span data-ttu-id="fc335-217">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="fc335-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="fc335-218">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="fc335-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="fc335-219">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="fc335-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="fc335-220">Sybase admite T-SQL y tipos de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="fc335-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="fc335-221">Para ver una tabla de asignación de tipos sql al tipo .NET, consulte el artículo [Conector SQL Azure](data-factory-azure-sql-connector.md) .</span><span class="sxs-lookup"><span data-stu-id="fc335-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="fc335-222">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="fc335-222">Map source to sink columns</span></span>
<span data-ttu-id="fc335-223">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fc335-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="fc335-224">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="fc335-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="fc335-225">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="fc335-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="fc335-226">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="fc335-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fc335-227">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="fc335-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fc335-228">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="fc335-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fc335-229">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fc335-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fc335-230">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="fc335-230">Performance and Tuning</span></span>
<span data-ttu-id="fc335-231">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="fc335-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
