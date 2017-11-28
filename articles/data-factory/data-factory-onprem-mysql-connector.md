---
title: Movimiento de datos de MySQL mediante Azure Data Factory | Microsoft Docs
description: "Obtenga información acerca de cómo mover los datos de la base de datos de MySQL mediante Factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="490a8-103">Movimiento de datos de MySQL mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="490a8-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="490a8-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos de una base de datos MySQL local.</span><span class="sxs-lookup"><span data-stu-id="490a8-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="490a8-105">Se basa en la información general ofrecida por el artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="490a8-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="490a8-106">Puede copiar datos desde un almacén de datos de MySQL local a cualquier almacén de datos del receptor admitidos.</span><span class="sxs-lookup"><span data-stu-id="490a8-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="490a8-107">Para ver una lista de almacenes de datos admitidos como receptores por la actividad de copia, consulte la tabla [Almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="490a8-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="490a8-108">Data Factory solo admite actualmente el movimiento de datos de un almacén de datos de MySQL a otros almacenes de datos, pero no viceversa.</span><span class="sxs-lookup"><span data-stu-id="490a8-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="490a8-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="490a8-109">Prerequisites</span></span>
<span data-ttu-id="490a8-110">El servicio Factoría de datos admite la conexión a orígenes de MySQL locales mediante Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="490a8-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="490a8-111">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="490a8-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="490a8-112">La puerta de enlace es necesaria incluso si la base de datos MySQL está hospedada en una máquina virtual (VM) de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="490a8-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="490a8-113">Puede instalar la puerta de enlace en la misma máquina virtual como almacén de datos o en una máquina virtual diferente, siempre y cuando la puerta de enlace se pueda conectar a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="490a8-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="490a8-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="490a8-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="490a8-115">Supported versions and installation</span></span>
<span data-ttu-id="490a8-116">Para que la puerta de enlace de administración de datos se conecte a la Base de datos MySQL, deberá instalar el [conector MySQL/Net para Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versión 6.6.5 o superior) en el mismo sistema que la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="490a8-117">Se admite la versión 5.1 de MySQL o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="490a8-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="490a8-118">Si se produce error en "Error de autenticación porque la parte remota cerró la secuencia de transporte.", considere la posibilidad de actualizar el conector MySQL/Net a una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="490a8-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="490a8-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="490a8-119">Getting started</span></span>
<span data-ttu-id="490a8-120">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="490a8-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="490a8-121">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="490a8-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="490a8-122">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="490a8-123">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="490a8-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="490a8-124">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="490a8-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="490a8-125">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="490a8-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="490a8-126">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="490a8-127">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="490a8-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="490a8-128">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="490a8-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="490a8-129">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="490a8-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="490a8-130">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="490a8-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="490a8-131">Para obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan para copiar los datos de un almacén de datos de MySQL local, consulte la sección [Ejemplo de JSON: Copiar datos de MySQL a un blob de Azure](#json-example-copy-data-from-mysql-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="490a8-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="490a8-132">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos de MySQL:</span><span class="sxs-lookup"><span data-stu-id="490a8-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="490a8-133">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="490a8-133">Linked service properties</span></span>
<span data-ttu-id="490a8-134">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos al servicio vinculado de MySQL.</span><span class="sxs-lookup"><span data-stu-id="490a8-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="490a8-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="490a8-135">Property</span></span> | <span data-ttu-id="490a8-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="490a8-136">Description</span></span> | <span data-ttu-id="490a8-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="490a8-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="490a8-138">type</span><span class="sxs-lookup"><span data-stu-id="490a8-138">type</span></span> |<span data-ttu-id="490a8-139">La propiedad type debe establecerse en: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="490a8-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="490a8-140">Sí</span><span class="sxs-lookup"><span data-stu-id="490a8-140">Yes</span></span> |
| <span data-ttu-id="490a8-141">server</span><span class="sxs-lookup"><span data-stu-id="490a8-141">server</span></span> |<span data-ttu-id="490a8-142">Nombre del servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="490a8-142">Name of the MySQL server.</span></span> |<span data-ttu-id="490a8-143">Sí</span><span class="sxs-lookup"><span data-stu-id="490a8-143">Yes</span></span> |
| <span data-ttu-id="490a8-144">database</span><span class="sxs-lookup"><span data-stu-id="490a8-144">database</span></span> |<span data-ttu-id="490a8-145">Nombre de la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="490a8-145">Name of the MySQL database.</span></span> |<span data-ttu-id="490a8-146">Sí</span><span class="sxs-lookup"><span data-stu-id="490a8-146">Yes</span></span> |
| <span data-ttu-id="490a8-147">schema</span><span class="sxs-lookup"><span data-stu-id="490a8-147">schema</span></span> |<span data-ttu-id="490a8-148">Nombre del esquema de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-148">Name of the schema in the database.</span></span> |<span data-ttu-id="490a8-149">No</span><span class="sxs-lookup"><span data-stu-id="490a8-149">No</span></span> |
| <span data-ttu-id="490a8-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="490a8-150">authenticationType</span></span> |<span data-ttu-id="490a8-151">Tipo de autenticación usado para conectarse a la Base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="490a8-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="490a8-152">Los valores posibles son: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="490a8-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="490a8-153">Sí</span><span class="sxs-lookup"><span data-stu-id="490a8-153">Yes</span></span> |
| <span data-ttu-id="490a8-154">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="490a8-154">username</span></span> |<span data-ttu-id="490a8-155">Especifique el nombre de usuario para conectarse a la base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="490a8-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="490a8-156">Sí</span><span class="sxs-lookup"><span data-stu-id="490a8-156">Yes</span></span> |
| <span data-ttu-id="490a8-157">contraseña</span><span class="sxs-lookup"><span data-stu-id="490a8-157">password</span></span> |<span data-ttu-id="490a8-158">Especifique la contraseña de la cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="490a8-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="490a8-159">Sí</span><span class="sxs-lookup"><span data-stu-id="490a8-159">Yes</span></span> |
| <span data-ttu-id="490a8-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="490a8-160">gatewayName</span></span> |<span data-ttu-id="490a8-161">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la Base de datos MySQL local.</span><span class="sxs-lookup"><span data-stu-id="490a8-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="490a8-162">Sí</span><span class="sxs-lookup"><span data-stu-id="490a8-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="490a8-163">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="490a8-163">Dataset properties</span></span>
<span data-ttu-id="490a8-164">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="490a8-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="490a8-165">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="490a8-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="490a8-166">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="490a8-167">La sección typeProperties del conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de MySQL) tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="490a8-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="490a8-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="490a8-168">Property</span></span> | <span data-ttu-id="490a8-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="490a8-169">Description</span></span> | <span data-ttu-id="490a8-170">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="490a8-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="490a8-171">tableName</span><span class="sxs-lookup"><span data-stu-id="490a8-171">tableName</span></span> |<span data-ttu-id="490a8-172">Nombre de la tabla en la instancia de la Base de datos MySQL a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="490a8-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="490a8-173">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="490a8-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="490a8-174">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="490a8-174">Copy activity properties</span></span>
<span data-ttu-id="490a8-175">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="490a8-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="490a8-176">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="490a8-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="490a8-177">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="490a8-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="490a8-178">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="490a8-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="490a8-179">Si el origen es de tipo **RelationalSource** (que incluye MySQL), están disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="490a8-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="490a8-180">Propiedad</span><span class="sxs-lookup"><span data-stu-id="490a8-180">Property</span></span> | <span data-ttu-id="490a8-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="490a8-181">Description</span></span> | <span data-ttu-id="490a8-182">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="490a8-182">Allowed values</span></span> | <span data-ttu-id="490a8-183">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="490a8-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="490a8-184">query</span><span class="sxs-lookup"><span data-stu-id="490a8-184">query</span></span> |<span data-ttu-id="490a8-185">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-185">Use the custom query to read data.</span></span> |<span data-ttu-id="490a8-186">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="490a8-186">SQL query string.</span></span> <span data-ttu-id="490a8-187">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="490a8-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="490a8-188">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="490a8-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="490a8-189">Ejemplo de JSON: Copiar datos de MySQL a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="490a8-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="490a8-190">Este ejemplo proporciona definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="490a8-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="490a8-191">Muestra cómo copiar datos de una base de datos MySQL local a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="490a8-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="490a8-192">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="490a8-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="490a8-193">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="490a8-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="490a8-194">No incluye instrucciones paso a paso para crear la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="490a8-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="490a8-195">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="490a8-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="490a8-196">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="490a8-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="490a8-197">Un servicio vinculado de tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="490a8-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="490a8-198">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="490a8-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="490a8-199">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="490a8-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="490a8-200">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="490a8-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="490a8-201">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="490a8-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="490a8-202">En el ejemplo se copian datos de un resultado de consulta de una base de datos MySQL en un blob cada hora.</span><span class="sxs-lookup"><span data-stu-id="490a8-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="490a8-203">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="490a8-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="490a8-204">En primer lugar, configure Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="490a8-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="490a8-205">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="490a8-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="490a8-206">**Servicio vinculado de MySQL:**</span><span class="sxs-lookup"><span data-stu-id="490a8-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="490a8-207">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="490a8-207">**Azure Storage linked service:**</span></span>

```JSON
    {
      "name": "AzureStorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
      }
    }
```

<span data-ttu-id="490a8-208">**Conjunto de datos de entrada de MySQL:**</span><span class="sxs-lookup"><span data-stu-id="490a8-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="490a8-209">El ejemplo supone que ha creado una tabla "MyTable" en MySQL y que contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="490a8-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="490a8-210">Si se establece "external": true, se informa al servicio Data Factory de que la tabla es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="490a8-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="490a8-211">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="490a8-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="490a8-212">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="490a8-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="490a8-213">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="490a8-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="490a8-214">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="490a8-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="490a8-215">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="490a8-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="490a8-216">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="490a8-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="490a8-217">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="490a8-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="490a8-218">La consulta SQL especificada para la propiedad **query** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="490a8-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="490a8-219">Asignación de tipos para MySQL</span><span class="sxs-lookup"><span data-stu-id="490a8-219">Type mapping for MySQL</span></span>
<span data-ttu-id="490a8-220">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="490a8-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="490a8-221">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="490a8-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="490a8-222">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="490a8-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="490a8-223">Al mover datos a MySQL, se usarán las asignaciones siguientes de tipos MySQL a tipos .NET.</span><span class="sxs-lookup"><span data-stu-id="490a8-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="490a8-224">Tipo de Base de datos MySQL</span><span class="sxs-lookup"><span data-stu-id="490a8-224">MySQL Database type</span></span> | <span data-ttu-id="490a8-225">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="490a8-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="490a8-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="490a8-226">bigint unsigned</span></span> |<span data-ttu-id="490a8-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="490a8-227">Decimal</span></span> |
| <span data-ttu-id="490a8-228">bigint</span><span class="sxs-lookup"><span data-stu-id="490a8-228">bigint</span></span> |<span data-ttu-id="490a8-229">Int64</span><span class="sxs-lookup"><span data-stu-id="490a8-229">Int64</span></span> |
| <span data-ttu-id="490a8-230">bit</span><span class="sxs-lookup"><span data-stu-id="490a8-230">bit</span></span> |<span data-ttu-id="490a8-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="490a8-231">Decimal</span></span> |
| <span data-ttu-id="490a8-232">blob</span><span class="sxs-lookup"><span data-stu-id="490a8-232">blob</span></span> |<span data-ttu-id="490a8-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="490a8-233">Byte[]</span></span> |
| <span data-ttu-id="490a8-234">booleano</span><span class="sxs-lookup"><span data-stu-id="490a8-234">bool</span></span> |<span data-ttu-id="490a8-235">Booleano</span><span class="sxs-lookup"><span data-stu-id="490a8-235">Boolean</span></span> |
| <span data-ttu-id="490a8-236">char</span><span class="sxs-lookup"><span data-stu-id="490a8-236">char</span></span> |<span data-ttu-id="490a8-237">String</span><span class="sxs-lookup"><span data-stu-id="490a8-237">String</span></span> |
| <span data-ttu-id="490a8-238">fecha</span><span class="sxs-lookup"><span data-stu-id="490a8-238">date</span></span> |<span data-ttu-id="490a8-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="490a8-239">Datetime</span></span> |
| <span data-ttu-id="490a8-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="490a8-240">datetime</span></span> |<span data-ttu-id="490a8-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="490a8-241">Datetime</span></span> |
| <span data-ttu-id="490a8-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="490a8-242">decimal</span></span> |<span data-ttu-id="490a8-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="490a8-243">Decimal</span></span> |
| <span data-ttu-id="490a8-244">double precision</span><span class="sxs-lookup"><span data-stu-id="490a8-244">double precision</span></span> |<span data-ttu-id="490a8-245">Doble</span><span class="sxs-lookup"><span data-stu-id="490a8-245">Double</span></span> |
| <span data-ttu-id="490a8-246">Doble</span><span class="sxs-lookup"><span data-stu-id="490a8-246">double</span></span> |<span data-ttu-id="490a8-247">Doble</span><span class="sxs-lookup"><span data-stu-id="490a8-247">Double</span></span> |
| <span data-ttu-id="490a8-248">enum</span><span class="sxs-lookup"><span data-stu-id="490a8-248">enum</span></span> |<span data-ttu-id="490a8-249">String</span><span class="sxs-lookup"><span data-stu-id="490a8-249">String</span></span> |
| <span data-ttu-id="490a8-250">float</span><span class="sxs-lookup"><span data-stu-id="490a8-250">float</span></span> |<span data-ttu-id="490a8-251">Single</span><span class="sxs-lookup"><span data-stu-id="490a8-251">Single</span></span> |
| <span data-ttu-id="490a8-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="490a8-252">int unsigned</span></span> |<span data-ttu-id="490a8-253">Int64</span><span class="sxs-lookup"><span data-stu-id="490a8-253">Int64</span></span> |
| <span data-ttu-id="490a8-254">int</span><span class="sxs-lookup"><span data-stu-id="490a8-254">int</span></span> |<span data-ttu-id="490a8-255">Int32</span><span class="sxs-lookup"><span data-stu-id="490a8-255">Int32</span></span> |
| <span data-ttu-id="490a8-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="490a8-256">integer unsigned</span></span> |<span data-ttu-id="490a8-257">Int64</span><span class="sxs-lookup"><span data-stu-id="490a8-257">Int64</span></span> |
| <span data-ttu-id="490a8-258">integer</span><span class="sxs-lookup"><span data-stu-id="490a8-258">integer</span></span> |<span data-ttu-id="490a8-259">Int32</span><span class="sxs-lookup"><span data-stu-id="490a8-259">Int32</span></span> |
| <span data-ttu-id="490a8-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="490a8-260">long varbinary</span></span> |<span data-ttu-id="490a8-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="490a8-261">Byte[]</span></span> |
| <span data-ttu-id="490a8-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="490a8-262">long varchar</span></span> |<span data-ttu-id="490a8-263">String</span><span class="sxs-lookup"><span data-stu-id="490a8-263">String</span></span> |
| <span data-ttu-id="490a8-264">longblob</span><span class="sxs-lookup"><span data-stu-id="490a8-264">longblob</span></span> |<span data-ttu-id="490a8-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="490a8-265">Byte[]</span></span> |
| <span data-ttu-id="490a8-266">longtext</span><span class="sxs-lookup"><span data-stu-id="490a8-266">longtext</span></span> |<span data-ttu-id="490a8-267">String</span><span class="sxs-lookup"><span data-stu-id="490a8-267">String</span></span> |
| <span data-ttu-id="490a8-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="490a8-268">mediumblob</span></span> |<span data-ttu-id="490a8-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="490a8-269">Byte[]</span></span> |
| <span data-ttu-id="490a8-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="490a8-270">mediumint unsigned</span></span> |<span data-ttu-id="490a8-271">Int64</span><span class="sxs-lookup"><span data-stu-id="490a8-271">Int64</span></span> |
| <span data-ttu-id="490a8-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="490a8-272">mediumint</span></span> |<span data-ttu-id="490a8-273">Int32</span><span class="sxs-lookup"><span data-stu-id="490a8-273">Int32</span></span> |
| <span data-ttu-id="490a8-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="490a8-274">mediumtext</span></span> |<span data-ttu-id="490a8-275">String</span><span class="sxs-lookup"><span data-stu-id="490a8-275">String</span></span> |
| <span data-ttu-id="490a8-276">numeric</span><span class="sxs-lookup"><span data-stu-id="490a8-276">numeric</span></span> |<span data-ttu-id="490a8-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="490a8-277">Decimal</span></span> |
| <span data-ttu-id="490a8-278">real</span><span class="sxs-lookup"><span data-stu-id="490a8-278">real</span></span> |<span data-ttu-id="490a8-279">Doble</span><span class="sxs-lookup"><span data-stu-id="490a8-279">Double</span></span> |
| <span data-ttu-id="490a8-280">set</span><span class="sxs-lookup"><span data-stu-id="490a8-280">set</span></span> |<span data-ttu-id="490a8-281">String</span><span class="sxs-lookup"><span data-stu-id="490a8-281">String</span></span> |
| <span data-ttu-id="490a8-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="490a8-282">smallint unsigned</span></span> |<span data-ttu-id="490a8-283">Int32</span><span class="sxs-lookup"><span data-stu-id="490a8-283">Int32</span></span> |
| <span data-ttu-id="490a8-284">smallint</span><span class="sxs-lookup"><span data-stu-id="490a8-284">smallint</span></span> |<span data-ttu-id="490a8-285">Int16</span><span class="sxs-lookup"><span data-stu-id="490a8-285">Int16</span></span> |
| <span data-ttu-id="490a8-286">text</span><span class="sxs-lookup"><span data-stu-id="490a8-286">text</span></span> |<span data-ttu-id="490a8-287">String</span><span class="sxs-lookup"><span data-stu-id="490a8-287">String</span></span> |
| <span data-ttu-id="490a8-288">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="490a8-288">time</span></span> |<span data-ttu-id="490a8-289">timespan</span><span class="sxs-lookup"><span data-stu-id="490a8-289">TimeSpan</span></span> |
| <span data-ttu-id="490a8-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="490a8-290">timestamp</span></span> |<span data-ttu-id="490a8-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="490a8-291">Datetime</span></span> |
| <span data-ttu-id="490a8-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="490a8-292">tinyblob</span></span> |<span data-ttu-id="490a8-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="490a8-293">Byte[]</span></span> |
| <span data-ttu-id="490a8-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="490a8-294">tinyint unsigned</span></span> |<span data-ttu-id="490a8-295">Int16</span><span class="sxs-lookup"><span data-stu-id="490a8-295">Int16</span></span> |
| <span data-ttu-id="490a8-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="490a8-296">tinyint</span></span> |<span data-ttu-id="490a8-297">Int16</span><span class="sxs-lookup"><span data-stu-id="490a8-297">Int16</span></span> |
| <span data-ttu-id="490a8-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="490a8-298">tinytext</span></span> |<span data-ttu-id="490a8-299">String</span><span class="sxs-lookup"><span data-stu-id="490a8-299">String</span></span> |
| <span data-ttu-id="490a8-300">varchar</span><span class="sxs-lookup"><span data-stu-id="490a8-300">varchar</span></span> |<span data-ttu-id="490a8-301">String</span><span class="sxs-lookup"><span data-stu-id="490a8-301">String</span></span> |
| <span data-ttu-id="490a8-302">year</span><span class="sxs-lookup"><span data-stu-id="490a8-302">year</span></span> |<span data-ttu-id="490a8-303">int</span><span class="sxs-lookup"><span data-stu-id="490a8-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="490a8-304">Asignación de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="490a8-304">Map source to sink columns</span></span>
<span data-ttu-id="490a8-305">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="490a8-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="490a8-306">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="490a8-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="490a8-307">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="490a8-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="490a8-308">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="490a8-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="490a8-309">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="490a8-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="490a8-310">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="490a8-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="490a8-311">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="490a8-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="490a8-312">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="490a8-312">Performance and Tuning</span></span>
<span data-ttu-id="490a8-313">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="490a8-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
