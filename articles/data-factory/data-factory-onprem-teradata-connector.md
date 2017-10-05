---
title: Movimiento de datos de Teradata mediante Azure Data Factory | Microsoft Docs
description: "Obtenga información acerca del conector Teradata para el servicio Factoría de datos que le permite mover datos desde Base de datos Teradata."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="9ce54-103">Movimiento de datos de Teradata mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="9ce54-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="9ce54-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos de una base de datos de Teradata local.</span><span class="sxs-lookup"><span data-stu-id="9ce54-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="9ce54-105">Se basa en la información general ofrecida por el artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9ce54-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="9ce54-106">Puede copiar datos desde un almacén de datos de Teradata local a cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="9ce54-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="9ce54-107">Para ver una lista de almacenes de datos admitidos como receptores por la actividad de copia, consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9ce54-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="9ce54-108">Data Factory solo admite actualmente el movimiento de datos desde un almacén de datos de Teradata hasta otros almacenes de datos, pero no al contrario.</span><span class="sxs-lookup"><span data-stu-id="9ce54-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9ce54-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9ce54-109">Prerequisites</span></span>
<span data-ttu-id="9ce54-110">La Factoría de datos admite la conexión a orígenes de Teradata local a través de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="9ce54-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="9ce54-111">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="9ce54-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="9ce54-112">La puerta de enlace es necesaria incluso si Teradata está hospedado en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce54-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="9ce54-113">Puede instalar la puerta de enlace en la misma máquina virtual de IaaS como almacén de datos o en una máquina virtual diferente, siempre y cuando la puerta de enlace se pueda conectar a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="9ce54-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="9ce54-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="9ce54-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="9ce54-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="9ce54-115">Supported versions and installation</span></span>
<span data-ttu-id="9ce54-116">Para que Data Management Gateway se conecte a la Base de datos Teradata, es preciso instalar el [proveedor de datos .NET para Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versión 14 o posterior en el mismo sistema que Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="9ce54-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="9ce54-117">Se admite la versión 12 de Teradata o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9ce54-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9ce54-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="9ce54-118">Getting started</span></span>
<span data-ttu-id="9ce54-119">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="9ce54-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="9ce54-120">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="9ce54-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="9ce54-121">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="9ce54-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="9ce54-122">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="9ce54-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9ce54-123">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="9ce54-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9ce54-124">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="9ce54-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="9ce54-125">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="9ce54-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="9ce54-126">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="9ce54-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="9ce54-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="9ce54-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9ce54-128">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="9ce54-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="9ce54-129">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9ce54-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="9ce54-130">Para ver un ejemplo con definiciones JSON para entidades de Data Factory que se usan para copiar datos de un almacén de datos de Teradata local, consulte la sección [Ejemplo: Copia de datos de Teradata en Blob de Azure](#json-example-copy-data-from-teradata-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9ce54-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="9ce54-131">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos de Teradata:</span><span class="sxs-lookup"><span data-stu-id="9ce54-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9ce54-132">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="9ce54-132">Linked service properties</span></span>
<span data-ttu-id="9ce54-133">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos al servicio vinculado de Teradata.</span><span class="sxs-lookup"><span data-stu-id="9ce54-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="9ce54-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9ce54-134">Property</span></span> | <span data-ttu-id="9ce54-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="9ce54-135">Description</span></span> | <span data-ttu-id="9ce54-136">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9ce54-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9ce54-137">type</span><span class="sxs-lookup"><span data-stu-id="9ce54-137">type</span></span> |<span data-ttu-id="9ce54-138">La propiedad type debe establecerse en **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="9ce54-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="9ce54-139">Sí</span><span class="sxs-lookup"><span data-stu-id="9ce54-139">Yes</span></span> |
| <span data-ttu-id="9ce54-140">server</span><span class="sxs-lookup"><span data-stu-id="9ce54-140">server</span></span> |<span data-ttu-id="9ce54-141">Nombre del servidor de Teradata.</span><span class="sxs-lookup"><span data-stu-id="9ce54-141">Name of the Teradata server.</span></span> |<span data-ttu-id="9ce54-142">Sí</span><span class="sxs-lookup"><span data-stu-id="9ce54-142">Yes</span></span> |
| <span data-ttu-id="9ce54-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="9ce54-143">authenticationType</span></span> |<span data-ttu-id="9ce54-144">Tipo de autenticación usado para conectarse a la base de datos Teradata.</span><span class="sxs-lookup"><span data-stu-id="9ce54-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="9ce54-145">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="9ce54-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="9ce54-146">Sí</span><span class="sxs-lookup"><span data-stu-id="9ce54-146">Yes</span></span> |
| <span data-ttu-id="9ce54-147">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="9ce54-147">username</span></span> |<span data-ttu-id="9ce54-148">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="9ce54-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="9ce54-149">No</span><span class="sxs-lookup"><span data-stu-id="9ce54-149">No</span></span> |
| <span data-ttu-id="9ce54-150">contraseña</span><span class="sxs-lookup"><span data-stu-id="9ce54-150">password</span></span> |<span data-ttu-id="9ce54-151">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="9ce54-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="9ce54-152">No</span><span class="sxs-lookup"><span data-stu-id="9ce54-152">No</span></span> |
| <span data-ttu-id="9ce54-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9ce54-153">gatewayName</span></span> |<span data-ttu-id="9ce54-154">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos Teradata local.</span><span class="sxs-lookup"><span data-stu-id="9ce54-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="9ce54-155">Sí</span><span class="sxs-lookup"><span data-stu-id="9ce54-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="9ce54-156">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="9ce54-156">Dataset properties</span></span>
<span data-ttu-id="9ce54-157">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="9ce54-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9ce54-158">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="9ce54-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9ce54-159">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="9ce54-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="9ce54-160">Actualmente, no hay ninguna propiedad de tipo compatible con el conjunto de datos de Teradata.</span><span class="sxs-lookup"><span data-stu-id="9ce54-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="9ce54-161">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="9ce54-161">Copy activity properties</span></span>
<span data-ttu-id="9ce54-162">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="9ce54-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9ce54-163">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="9ce54-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="9ce54-164">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="9ce54-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="9ce54-165">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="9ce54-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="9ce54-166">Cuando la actividad de copia es de tipo **RelationalSource** (lo que incluye Teradata), están disponibles las propiedades siguientes en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="9ce54-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="9ce54-167">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9ce54-167">Property</span></span> | <span data-ttu-id="9ce54-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="9ce54-168">Description</span></span> | <span data-ttu-id="9ce54-169">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="9ce54-169">Allowed values</span></span> | <span data-ttu-id="9ce54-170">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9ce54-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9ce54-171">query</span><span class="sxs-lookup"><span data-stu-id="9ce54-171">query</span></span> |<span data-ttu-id="9ce54-172">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="9ce54-172">Use the custom query to read data.</span></span> |<span data-ttu-id="9ce54-173">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="9ce54-173">SQL query string.</span></span> <span data-ttu-id="9ce54-174">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="9ce54-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="9ce54-175">Sí</span><span class="sxs-lookup"><span data-stu-id="9ce54-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="9ce54-176">Ejemplo: Copia de datos de Teradata en Blob de Azure</span><span class="sxs-lookup"><span data-stu-id="9ce54-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="9ce54-177">En el siguiente ejemplo, se proporcionan definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9ce54-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9ce54-178">Se muestra cómo copiar datos desde la base de datos Teradata al almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce54-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="9ce54-179">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce54-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="9ce54-180">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="9ce54-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="9ce54-181">Un servicio vinculado de tipo [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9ce54-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="9ce54-182">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="9ce54-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9ce54-183">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9ce54-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="9ce54-184">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9ce54-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="9ce54-185">La [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9ce54-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9ce54-186">El ejemplo copia cada hora los datos de un resultado de consulta de la base de datos Teradata en un blob.</span><span class="sxs-lookup"><span data-stu-id="9ce54-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="9ce54-187">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="9ce54-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="9ce54-188">En primer lugar, configure Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="9ce54-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="9ce54-189">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="9ce54-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="9ce54-190">**Servicio vinculado de Teradata:**</span><span class="sxs-lookup"><span data-stu-id="9ce54-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="9ce54-191">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="9ce54-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="9ce54-192">**Conjunto de datos de entrada de Teradata:**</span><span class="sxs-lookup"><span data-stu-id="9ce54-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="9ce54-193">El ejemplo supone que ha creado una tabla "MyTable" en Teradata y que contiene una columna denominada "timestamp" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="9ce54-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="9ce54-194">Si se establece "external": true, se informa al servicio Data Factory de que la tabla es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="9ce54-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
        },
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

<span data-ttu-id="9ce54-195">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="9ce54-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="9ce54-196">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="9ce54-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9ce54-197">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="9ce54-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9ce54-198">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="9ce54-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="9ce54-199">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="9ce54-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="9ce54-200">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="9ce54-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="9ce54-201">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9ce54-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="9ce54-202">La consulta SQL especificada para la propiedad **query** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="9ce54-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="9ce54-203">Asignación de tipos para Teradata</span><span class="sxs-lookup"><span data-stu-id="9ce54-203">Type mapping for Teradata</span></span>
<span data-ttu-id="9ce54-204">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="9ce54-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="9ce54-205">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="9ce54-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="9ce54-206">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="9ce54-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="9ce54-207">Al mover datos a Teradata, se usan las asignaciones siguientes de tipo Teradata a tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="9ce54-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="9ce54-208">Tipo de base de datos Teradata</span><span class="sxs-lookup"><span data-stu-id="9ce54-208">Teradata Database type</span></span> | <span data-ttu-id="9ce54-209">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="9ce54-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="9ce54-210">Char</span><span class="sxs-lookup"><span data-stu-id="9ce54-210">Char</span></span> |<span data-ttu-id="9ce54-211">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-211">String</span></span> |
| <span data-ttu-id="9ce54-212">Clob</span><span class="sxs-lookup"><span data-stu-id="9ce54-212">Clob</span></span> |<span data-ttu-id="9ce54-213">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-213">String</span></span> |
| <span data-ttu-id="9ce54-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="9ce54-214">Graphic</span></span> |<span data-ttu-id="9ce54-215">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-215">String</span></span> |
| <span data-ttu-id="9ce54-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="9ce54-216">VarChar</span></span> |<span data-ttu-id="9ce54-217">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-217">String</span></span> |
| <span data-ttu-id="9ce54-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="9ce54-218">VarGraphic</span></span> |<span data-ttu-id="9ce54-219">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-219">String</span></span> |
| <span data-ttu-id="9ce54-220">Blob</span><span class="sxs-lookup"><span data-stu-id="9ce54-220">Blob</span></span> |<span data-ttu-id="9ce54-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9ce54-221">Byte[]</span></span> |
| <span data-ttu-id="9ce54-222">Byte</span><span class="sxs-lookup"><span data-stu-id="9ce54-222">Byte</span></span> |<span data-ttu-id="9ce54-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9ce54-223">Byte[]</span></span> |
| <span data-ttu-id="9ce54-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="9ce54-224">VarByte</span></span> |<span data-ttu-id="9ce54-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="9ce54-225">Byte[]</span></span> |
| <span data-ttu-id="9ce54-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="9ce54-226">BigInt</span></span> |<span data-ttu-id="9ce54-227">Int64</span><span class="sxs-lookup"><span data-stu-id="9ce54-227">Int64</span></span> |
| <span data-ttu-id="9ce54-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="9ce54-228">ByteInt</span></span> |<span data-ttu-id="9ce54-229">Int16</span><span class="sxs-lookup"><span data-stu-id="9ce54-229">Int16</span></span> |
| <span data-ttu-id="9ce54-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="9ce54-230">Decimal</span></span> |<span data-ttu-id="9ce54-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="9ce54-231">Decimal</span></span> |
| <span data-ttu-id="9ce54-232">Doble</span><span class="sxs-lookup"><span data-stu-id="9ce54-232">Double</span></span> |<span data-ttu-id="9ce54-233">Doble</span><span class="sxs-lookup"><span data-stu-id="9ce54-233">Double</span></span> |
| <span data-ttu-id="9ce54-234">Entero</span><span class="sxs-lookup"><span data-stu-id="9ce54-234">Integer</span></span> |<span data-ttu-id="9ce54-235">Int32</span><span class="sxs-lookup"><span data-stu-id="9ce54-235">Int32</span></span> |
| <span data-ttu-id="9ce54-236">Number</span><span class="sxs-lookup"><span data-stu-id="9ce54-236">Number</span></span> |<span data-ttu-id="9ce54-237">Doble</span><span class="sxs-lookup"><span data-stu-id="9ce54-237">Double</span></span> |
| <span data-ttu-id="9ce54-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="9ce54-238">SmallInt</span></span> |<span data-ttu-id="9ce54-239">Int16</span><span class="sxs-lookup"><span data-stu-id="9ce54-239">Int16</span></span> |
| <span data-ttu-id="9ce54-240">Date</span><span class="sxs-lookup"><span data-stu-id="9ce54-240">Date</span></span> |<span data-ttu-id="9ce54-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="9ce54-241">DateTime</span></span> |
| <span data-ttu-id="9ce54-242">Hora</span><span class="sxs-lookup"><span data-stu-id="9ce54-242">Time</span></span> |<span data-ttu-id="9ce54-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-243">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="9ce54-244">Time With Time Zone</span></span> |<span data-ttu-id="9ce54-245">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-245">String</span></span> |
| <span data-ttu-id="9ce54-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="9ce54-246">Timestamp</span></span> |<span data-ttu-id="9ce54-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="9ce54-247">DateTime</span></span> |
| <span data-ttu-id="9ce54-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="9ce54-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="9ce54-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="9ce54-249">DateTimeOffset</span></span> |
| <span data-ttu-id="9ce54-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="9ce54-250">Interval Day</span></span> |<span data-ttu-id="9ce54-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-251">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-252">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="9ce54-252">Interval Day To Hour</span></span> |<span data-ttu-id="9ce54-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-253">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-254">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="9ce54-254">Interval Day To Minute</span></span> |<span data-ttu-id="9ce54-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-255">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-256">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="9ce54-256">Interval Day To Second</span></span> |<span data-ttu-id="9ce54-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-257">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="9ce54-258">Interval Hour</span></span> |<span data-ttu-id="9ce54-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-259">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-260">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="9ce54-260">Interval Hour To Minute</span></span> |<span data-ttu-id="9ce54-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-261">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-262">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="9ce54-262">Interval Hour To Second</span></span> |<span data-ttu-id="9ce54-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-263">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="9ce54-264">Interval Minute</span></span> |<span data-ttu-id="9ce54-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-265">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-266">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="9ce54-266">Interval Minute To Second</span></span> |<span data-ttu-id="9ce54-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-267">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="9ce54-268">Interval Second</span></span> |<span data-ttu-id="9ce54-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9ce54-269">TimeSpan</span></span> |
| <span data-ttu-id="9ce54-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="9ce54-270">Interval Year</span></span> |<span data-ttu-id="9ce54-271">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-271">String</span></span> |
| <span data-ttu-id="9ce54-272">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="9ce54-272">Interval Year To Month</span></span> |<span data-ttu-id="9ce54-273">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-273">String</span></span> |
| <span data-ttu-id="9ce54-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="9ce54-274">Interval Month</span></span> |<span data-ttu-id="9ce54-275">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-275">String</span></span> |
| <span data-ttu-id="9ce54-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="9ce54-276">Period(Date)</span></span> |<span data-ttu-id="9ce54-277">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-277">String</span></span> |
| <span data-ttu-id="9ce54-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="9ce54-278">Period(Time)</span></span> |<span data-ttu-id="9ce54-279">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-279">String</span></span> |
| <span data-ttu-id="9ce54-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="9ce54-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="9ce54-281">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-281">String</span></span> |
| <span data-ttu-id="9ce54-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="9ce54-282">Period(Timestamp)</span></span> |<span data-ttu-id="9ce54-283">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-283">String</span></span> |
| <span data-ttu-id="9ce54-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="9ce54-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="9ce54-285">String</span><span class="sxs-lookup"><span data-stu-id="9ce54-285">String</span></span> |
| <span data-ttu-id="9ce54-286">Xml</span><span class="sxs-lookup"><span data-stu-id="9ce54-286">Xml</span></span> |<span data-ttu-id="9ce54-287">string</span><span class="sxs-lookup"><span data-stu-id="9ce54-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="9ce54-288">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="9ce54-288">Map source to sink columns</span></span>
<span data-ttu-id="9ce54-289">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9ce54-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="9ce54-290">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="9ce54-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="9ce54-291">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="9ce54-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="9ce54-292">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="9ce54-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="9ce54-293">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="9ce54-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="9ce54-294">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="9ce54-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="9ce54-295">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="9ce54-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9ce54-296">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="9ce54-296">Performance and Tuning</span></span>
<span data-ttu-id="9ce54-297">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="9ce54-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
