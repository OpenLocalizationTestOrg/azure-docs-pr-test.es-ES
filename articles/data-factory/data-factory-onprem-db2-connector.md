---
title: Movimiento de datos de DB2 mediante Azure Data Factory | Microsoft Docs
description: "Obtenga información sobre cómo mover los datos desde una base de datos DB2 local mediante la actividad de copia de Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="2322e-103">Movimiento de datos de DB2 mediante la actividad de copia de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2322e-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="2322e-104">En este artículo se describe cómo se puede usar la actividad de copia en Azure Data Factory para copiar datos desde una base de datos DB2 local a un almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="2322e-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="2322e-105">Puede copiar los datos a cualquier almacén que aparezca como un receptor compatible en el artículo sobre [actividades de movimiento de datos de Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2322e-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="2322e-106">Este tema se basa en el artículo sobre Data Factory, que presenta información general sobre el movimiento de datos mediante la actividad de copia y enumera las combinaciones de almacenes de datos compatibles.</span><span class="sxs-lookup"><span data-stu-id="2322e-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="2322e-107">Data Factory actualmente solo admite mover datos desde una base de datos DB2 a un [almacén de datos de receptor compatible](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2322e-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2322e-108">No se admite el movimiento de datos desde otros almacenes de datos a una base de datos DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2322e-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2322e-109">Prerequisites</span></span>
<span data-ttu-id="2322e-110">Data Factory admite la conexión a una base de datos DB2 local mediante la [puerta de enlace de administración de datos](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="2322e-111">Para instrucciones paso a paso sobre cómo configurar la canalización de datos de la puerta de enlace para mover los datos, consulte el artículo [Movimiento de datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2322e-112">Se requiere una puerta de enlace incluso si DB2 está hospedada en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="2322e-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="2322e-113">Puede instalarla en la misma máquina virtual de IaaS en la que está el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="2322e-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="2322e-114">Si la puerta de enlace se puede conectar a la base de datos, es posible instalar la puerta de enlace en otra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2322e-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="2322e-115">La puerta de enlace de administración de datos proporciona un controlador de DB2 integrado, por lo que no es necesario instalar manualmente un controlador para copiar datos desde DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="2322e-116">Para sugerencias sobre cómo solucionar problemas con la conexión y la puerta de enlace, consulte el artículo [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="2322e-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="2322e-117">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="2322e-117">Supported versions</span></span>
<span data-ttu-id="2322e-118">Este conector de DB2 de Data Factory admite las plataformas y versiones de IBM DB2 siguientes con las versiones 9, 10 y 11 de SQL Access Manager (SQLAM) de la arquitectura distribuida de bases de datos relacionales (DRDA):</span><span class="sxs-lookup"><span data-stu-id="2322e-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="2322e-119">IBM DB2 para z/OS versión 11.1</span><span class="sxs-lookup"><span data-stu-id="2322e-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="2322e-120">IBM DB2 para z/OS versión 10.1</span><span class="sxs-lookup"><span data-stu-id="2322e-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="2322e-121">IBM DB2 para i (AS400) versión 7.2</span><span class="sxs-lookup"><span data-stu-id="2322e-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="2322e-122">IBM DB2 para i (AS400) versión 7.1</span><span class="sxs-lookup"><span data-stu-id="2322e-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="2322e-123">IBM DB2 para Linux, UNIX y (LUW) versión 11</span><span class="sxs-lookup"><span data-stu-id="2322e-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="2322e-124">IBM DB2 para LUW versión 10.5</span><span class="sxs-lookup"><span data-stu-id="2322e-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="2322e-125">IBM DB2 para LUW versión 10.1</span><span class="sxs-lookup"><span data-stu-id="2322e-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="2322e-126">Si recibe el mensaje de error "No se encontró el paquete correspondiente a una solicitud de ejecución de la instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="2322e-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="2322e-127">SQLSTATE=51002 SQLCODE=-805", es porque no se creó un paquete necesario para el usuario normal en el SO.</span><span class="sxs-lookup"><span data-stu-id="2322e-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="2322e-128">Para resolver el problema, siga estas instrucciones según el tipo de servidor de DB2:</span><span class="sxs-lookup"><span data-stu-id="2322e-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="2322e-129">DB2 para i (AS400): permita que un usuario avanzado cree la colección del usuario normal antes de ejecutar la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="2322e-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="2322e-130">Para crear la colección, use el comando: `create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="2322e-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="2322e-131">DB2 para z/OS o LUW: use una cuenta con privilegios elevados (usuario avanzado o administrador con entidades de paquete y permisos BIND, BINDADD, GRANT EXECUTE TO PUBLIC) para ejecutar una vez la copia.</span><span class="sxs-lookup"><span data-stu-id="2322e-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="2322e-132">El paquete necesario se creará de forma automáticamente durante la copia.</span><span class="sxs-lookup"><span data-stu-id="2322e-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="2322e-133">A continuación, puede cambiar al usuario normal para las ejecuciones de copia posteriores.</span><span class="sxs-lookup"><span data-stu-id="2322e-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2322e-134">Introducción</span><span class="sxs-lookup"><span data-stu-id="2322e-134">Getting started</span></span>
<span data-ttu-id="2322e-135">Puede crear una canalización con actividad de copia para mover datos desde un almacén de datos DB2 local mediante el uso de distintas herramientas o API:</span><span class="sxs-lookup"><span data-stu-id="2322e-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="2322e-136">La manera más fácil de crear una canalización es usar el Asistente para copia de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2322e-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="2322e-137">Para un tutorial rápido sobre cómo crear una canalización con el Asistente para copia, consulte [Tutorial: Creación de una canalización mediante el Asistente para copia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="2322e-138">También puede usar herramientas para crear una canalización, como Azure Portal, Visual Studio, Azure PowerShell, una plantilla de Azure Resource Manager, la API de .NET y la API de REST.</span><span class="sxs-lookup"><span data-stu-id="2322e-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="2322e-139">Para instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia, consulte el [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="2322e-140">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="2322e-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="2322e-141">Cree servicios vinculados para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2322e-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="2322e-142">Cree conjuntos de datos con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="2322e-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="2322e-143">Cree una canalización con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="2322e-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2322e-144">Cuando se usa el Asistente para copia, se crean automáticamente definiciones de JSON para las entidades de canalizaciones, los conjuntos de datos y los servicios vinculados de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2322e-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="2322e-145">Al usar herramientas o API (excepto la API de .NET), se definen las entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2322e-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="2322e-146">El [ejemplo de JSON: Copiar datos de DB2 a Azure Blob Storage](#json-example-copy-data-from-db2-to-azure-blob) muestra las definiciones de JSON para las entidades de Data Factory que se usan para copiar datos de un almacén de datos DB2 local.</span><span class="sxs-lookup"><span data-stu-id="2322e-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="2322e-147">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos de DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="2322e-148">Propiedades del servicio vinculado de DB2</span><span class="sxs-lookup"><span data-stu-id="2322e-148">DB2 linked service properties</span></span>
<span data-ttu-id="2322e-149">En la tabla siguiente se enumeran las propiedades JSON que son específicas de un servicio vinculado de DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="2322e-150">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2322e-150">Property</span></span> | <span data-ttu-id="2322e-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="2322e-151">Description</span></span> | <span data-ttu-id="2322e-152">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2322e-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2322e-153">**type**</span><span class="sxs-lookup"><span data-stu-id="2322e-153">**type**</span></span> |<span data-ttu-id="2322e-154">Esta propiedad se debe establecer en **OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="2322e-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="2322e-155">Sí</span><span class="sxs-lookup"><span data-stu-id="2322e-155">Yes</span></span> |
| <span data-ttu-id="2322e-156">**server**</span><span class="sxs-lookup"><span data-stu-id="2322e-156">**server**</span></span> |<span data-ttu-id="2322e-157">Nombre del servidor DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-157">The name of the DB2 server.</span></span> |<span data-ttu-id="2322e-158">Sí</span><span class="sxs-lookup"><span data-stu-id="2322e-158">Yes</span></span> |
| <span data-ttu-id="2322e-159">**database**</span><span class="sxs-lookup"><span data-stu-id="2322e-159">**database**</span></span> |<span data-ttu-id="2322e-160">Nombre de la base de datos DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-160">The name of the DB2 database.</span></span> |<span data-ttu-id="2322e-161">Sí</span><span class="sxs-lookup"><span data-stu-id="2322e-161">Yes</span></span> |
| <span data-ttu-id="2322e-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="2322e-162">**schema**</span></span> |<span data-ttu-id="2322e-163">Nombre del esquema de la base de datos DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="2322e-164">Esta propiedad distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2322e-164">This property is case-sensitive.</span></span> |<span data-ttu-id="2322e-165">No</span><span class="sxs-lookup"><span data-stu-id="2322e-165">No</span></span> |
| <span data-ttu-id="2322e-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="2322e-166">**authenticationType**</span></span> |<span data-ttu-id="2322e-167">Tipo de autenticación que se usa para conectarse a la base de datos DB2.</span><span class="sxs-lookup"><span data-stu-id="2322e-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="2322e-168">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="2322e-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="2322e-169">Sí</span><span class="sxs-lookup"><span data-stu-id="2322e-169">Yes</span></span> |
| <span data-ttu-id="2322e-170">**username**</span><span class="sxs-lookup"><span data-stu-id="2322e-170">**username**</span></span> |<span data-ttu-id="2322e-171">Nombre de la cuenta de usuario si se usa autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="2322e-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="2322e-172">No</span><span class="sxs-lookup"><span data-stu-id="2322e-172">No</span></span> |
| <span data-ttu-id="2322e-173">**password**</span><span class="sxs-lookup"><span data-stu-id="2322e-173">**password**</span></span> |<span data-ttu-id="2322e-174">Contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="2322e-174">The password for the user account.</span></span> |<span data-ttu-id="2322e-175">No</span><span class="sxs-lookup"><span data-stu-id="2322e-175">No</span></span> |
| <span data-ttu-id="2322e-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="2322e-176">**gatewayName**</span></span> |<span data-ttu-id="2322e-177">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos DB2 local.</span><span class="sxs-lookup"><span data-stu-id="2322e-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="2322e-178">Sí</span><span class="sxs-lookup"><span data-stu-id="2322e-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2322e-179">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="2322e-179">Dataset properties</span></span>
<span data-ttu-id="2322e-180">Para una lista de las secciones y propiedades disponibles para definir conjuntos de datos, consulte el artículo sobre [creación de conjuntos de datos](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="2322e-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2322e-181">Las secciones como **structure**, **availability** y **policy** del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (Azure SQL, Azure Blob Storage, Azure Table Storage, etc.).</span><span class="sxs-lookup"><span data-stu-id="2322e-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="2322e-182">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="2322e-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2322e-183">La sección **typeProperties** del conjunto de datos de tipo **RelationalTable**, que incluye el conjunto de datos de DB2, tiene la propiedad siguiente:</span><span class="sxs-lookup"><span data-stu-id="2322e-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="2322e-184">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2322e-184">Property</span></span> | <span data-ttu-id="2322e-185">Descripción</span><span class="sxs-lookup"><span data-stu-id="2322e-185">Description</span></span> | <span data-ttu-id="2322e-186">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2322e-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2322e-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="2322e-187">**tableName**</span></span> |<span data-ttu-id="2322e-188">Nombre de la tabla en la instancia de base de datos DB2 a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="2322e-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="2322e-189">Esta propiedad distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2322e-189">This property is case-sensitive.</span></span> |<span data-ttu-id="2322e-190">No (si se especifica la propiedad **query** de una actividad de copia de tipo **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="2322e-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2322e-191">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="2322e-191">Copy Activity properties</span></span>
<span data-ttu-id="2322e-192">Para una lista de las secciones y propiedades disponibles para definir actividades de copia, consulte el artículo sobre [creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2322e-193">Las propiedades de la actividad de copia, como **nombre**, **descripción**, tabla de **entradas**, tabla de **salidas** y **directiva**, están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="2322e-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="2322e-194">Las propiedades que están disponibles en la sección **typeProperties** de la actividad de cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="2322e-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="2322e-195">Para la actividad de copia, las propiedades varían en función de los tipos de orígenes y receptores de datos.</span><span class="sxs-lookup"><span data-stu-id="2322e-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="2322e-196">En el caso de la actividad de copia, si el origen es de tipo **RelationalSource** (que incluye DB2), las propiedades siguientes están disponibles en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="2322e-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="2322e-197">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2322e-197">Property</span></span> | <span data-ttu-id="2322e-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="2322e-198">Description</span></span> | <span data-ttu-id="2322e-199">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2322e-199">Allowed values</span></span> | <span data-ttu-id="2322e-200">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2322e-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2322e-201">**consulta**</span><span class="sxs-lookup"><span data-stu-id="2322e-201">**query**</span></span> |<span data-ttu-id="2322e-202">Use la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="2322e-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="2322e-203">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="2322e-203">SQL query string.</span></span> <span data-ttu-id="2322e-204">Por ejemplo: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="2322e-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="2322e-205">No (si se especifica la propiedad **tableName** de un conjunto de datos)</span><span class="sxs-lookup"><span data-stu-id="2322e-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="2322e-206">Los nombres de esquema y tabla distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2322e-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="2322e-207">En la instrucción de consulta, escriba los nombres de propiedades entre "" (comillas dobles).</span><span class="sxs-lookup"><span data-stu-id="2322e-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="2322e-208">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2322e-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="2322e-209">Ejemplo de JSON: Copiar datos de DB2 a Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="2322e-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="2322e-210">Este ejemplo proporciona definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2322e-211">En el ejemplo se muestra cómo copiar datos desde una base de datos DB2 a Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2322e-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="2322e-212">Sin embargo, es posible copiar los datos a [cualquier tipo de receptor de almacén de datos compatible](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2322e-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="2322e-213">El ejemplo consta de las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="2322e-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="2322e-214">Un servicio vinculado DB2 de tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2322e-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="2322e-215">Un servicio vinculado de Azure Blob Storage de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2322e-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="2322e-216">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2322e-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="2322e-217">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2322e-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="2322e-218">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa las propiedades [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2322e-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="2322e-219">En el ejemplo se copian datos cada hora de un resultado de consulta de una base de datos DB2 en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="2322e-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="2322e-220">Las propiedades JSON que se usan en el ejemplo se describen en las secciones que aparecen después de las definiciones de entidad.</span><span class="sxs-lookup"><span data-stu-id="2322e-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="2322e-221">Como primer paso, instale y configure una puerta de enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="2322e-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="2322e-222">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2322e-223">**Servicio vinculado DB2**</span><span class="sxs-lookup"><span data-stu-id="2322e-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

<span data-ttu-id="2322e-224">**Servicio vinculado de almacenamiento de blobs de Azure**</span><span class="sxs-lookup"><span data-stu-id="2322e-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="2322e-225">**Conjunto de datos de entrada de DB2**</span><span class="sxs-lookup"><span data-stu-id="2322e-225">**DB2 input dataset**</span></span>

<span data-ttu-id="2322e-226">En el ejemplo se supone que creó una tabla en DB2 llamada "MyTable" que tiene una columna etiquetada "timestamp" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="2322e-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="2322e-227">La propiedad **external** está establecida en "true."</span><span class="sxs-lookup"><span data-stu-id="2322e-227">The **external** property is set to "true."</span></span> <span data-ttu-id="2322e-228">Este valor informa al servicio Data Factory de que el conjunto de datos es externo a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="2322e-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="2322e-229">Tenga en cuenta que la propiedad **type** se establece en **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2322e-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

<span data-ttu-id="2322e-230">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="2322e-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="2322e-231">Para escribir los datos en un blob nuevo cada hora, la propiedad **frequency** se establece en "Hora" y la propiedad **interval**, en 1.</span><span class="sxs-lookup"><span data-stu-id="2322e-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="2322e-232">La propiedad **folderPath** del blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="2322e-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2322e-233">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="2322e-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="2322e-234">**Canalización de la actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="2322e-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="2322e-235">La canalización contiene una actividad de copia que está configurada para usar conjuntos de datos de entrada y de salida especificados y que está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="2322e-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="2322e-236">En la definición JSON de la canalización, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2322e-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="2322e-237">La consulta SQL especificada para la propiedad **query** selecciona los datos de la tabla "Orders".</span><span class="sxs-lookup"><span data-stu-id="2322e-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="2322e-238">Asignación de tipos para DB2</span><span class="sxs-lookup"><span data-stu-id="2322e-238">Type mapping for DB2</span></span>
<span data-ttu-id="2322e-239">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md), la actividad de copia realiza conversiones automáticas del tipo de origen al tipo de receptor con el enfoque de dos pasos siguiente:</span><span class="sxs-lookup"><span data-stu-id="2322e-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="2322e-240">Conversión de un tipo de origen nativo a un tipo .NET</span><span class="sxs-lookup"><span data-stu-id="2322e-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="2322e-241">Conversión de un tipo .NET a un tipo de receptor nativo</span><span class="sxs-lookup"><span data-stu-id="2322e-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="2322e-242">Las asignaciones siguientes se usan cuando la actividad de copia convierte los datos de un tipo DB2 a un tipo .NET:</span><span class="sxs-lookup"><span data-stu-id="2322e-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="2322e-243">Tipo de base de datos DB2</span><span class="sxs-lookup"><span data-stu-id="2322e-243">DB2 database type</span></span> | <span data-ttu-id="2322e-244">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2322e-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="2322e-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="2322e-245">SmallInt</span></span> |<span data-ttu-id="2322e-246">Int16</span><span class="sxs-lookup"><span data-stu-id="2322e-246">Int16</span></span> |
| <span data-ttu-id="2322e-247">Entero</span><span class="sxs-lookup"><span data-stu-id="2322e-247">Integer</span></span> |<span data-ttu-id="2322e-248">Int32</span><span class="sxs-lookup"><span data-stu-id="2322e-248">Int32</span></span> |
| <span data-ttu-id="2322e-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="2322e-249">BigInt</span></span> |<span data-ttu-id="2322e-250">Int64</span><span class="sxs-lookup"><span data-stu-id="2322e-250">Int64</span></span> |
| <span data-ttu-id="2322e-251">Real</span><span class="sxs-lookup"><span data-stu-id="2322e-251">Real</span></span> |<span data-ttu-id="2322e-252">Single</span><span class="sxs-lookup"><span data-stu-id="2322e-252">Single</span></span> |
| <span data-ttu-id="2322e-253">Doble</span><span class="sxs-lookup"><span data-stu-id="2322e-253">Double</span></span> |<span data-ttu-id="2322e-254">Doble</span><span class="sxs-lookup"><span data-stu-id="2322e-254">Double</span></span> |
| <span data-ttu-id="2322e-255">Float</span><span class="sxs-lookup"><span data-stu-id="2322e-255">Float</span></span> |<span data-ttu-id="2322e-256">Doble</span><span class="sxs-lookup"><span data-stu-id="2322e-256">Double</span></span> |
| <span data-ttu-id="2322e-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-257">Decimal</span></span> |<span data-ttu-id="2322e-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-258">Decimal</span></span> |
| <span data-ttu-id="2322e-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="2322e-259">DecimalFloat</span></span> |<span data-ttu-id="2322e-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-260">Decimal</span></span> |
| <span data-ttu-id="2322e-261">Numeric</span><span class="sxs-lookup"><span data-stu-id="2322e-261">Numeric</span></span> |<span data-ttu-id="2322e-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-262">Decimal</span></span> |
| <span data-ttu-id="2322e-263">Date</span><span class="sxs-lookup"><span data-stu-id="2322e-263">Date</span></span> |<span data-ttu-id="2322e-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="2322e-264">DateTime</span></span> |
| <span data-ttu-id="2322e-265">Hora</span><span class="sxs-lookup"><span data-stu-id="2322e-265">Time</span></span> |<span data-ttu-id="2322e-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2322e-266">TimeSpan</span></span> |
| <span data-ttu-id="2322e-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2322e-267">Timestamp</span></span> |<span data-ttu-id="2322e-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="2322e-268">DateTime</span></span> |
| <span data-ttu-id="2322e-269">xml</span><span class="sxs-lookup"><span data-stu-id="2322e-269">Xml</span></span> |<span data-ttu-id="2322e-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2322e-270">Byte[]</span></span> |
| <span data-ttu-id="2322e-271">Char</span><span class="sxs-lookup"><span data-stu-id="2322e-271">Char</span></span> |<span data-ttu-id="2322e-272">String</span><span class="sxs-lookup"><span data-stu-id="2322e-272">String</span></span> |
| <span data-ttu-id="2322e-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="2322e-273">VarChar</span></span> |<span data-ttu-id="2322e-274">String</span><span class="sxs-lookup"><span data-stu-id="2322e-274">String</span></span> |
| <span data-ttu-id="2322e-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="2322e-275">LongVarChar</span></span> |<span data-ttu-id="2322e-276">String</span><span class="sxs-lookup"><span data-stu-id="2322e-276">String</span></span> |
| <span data-ttu-id="2322e-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="2322e-277">DB2DynArray</span></span> |<span data-ttu-id="2322e-278">String</span><span class="sxs-lookup"><span data-stu-id="2322e-278">String</span></span> |
| <span data-ttu-id="2322e-279">Binary</span><span class="sxs-lookup"><span data-stu-id="2322e-279">Binary</span></span> |<span data-ttu-id="2322e-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2322e-280">Byte[]</span></span> |
| <span data-ttu-id="2322e-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="2322e-281">VarBinary</span></span> |<span data-ttu-id="2322e-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2322e-282">Byte[]</span></span> |
| <span data-ttu-id="2322e-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="2322e-283">LongVarBinary</span></span> |<span data-ttu-id="2322e-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2322e-284">Byte[]</span></span> |
| <span data-ttu-id="2322e-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="2322e-285">Graphic</span></span> |<span data-ttu-id="2322e-286">String</span><span class="sxs-lookup"><span data-stu-id="2322e-286">String</span></span> |
| <span data-ttu-id="2322e-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="2322e-287">VarGraphic</span></span> |<span data-ttu-id="2322e-288">String</span><span class="sxs-lookup"><span data-stu-id="2322e-288">String</span></span> |
| <span data-ttu-id="2322e-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="2322e-289">LongVarGraphic</span></span> |<span data-ttu-id="2322e-290">String</span><span class="sxs-lookup"><span data-stu-id="2322e-290">String</span></span> |
| <span data-ttu-id="2322e-291">Clob</span><span class="sxs-lookup"><span data-stu-id="2322e-291">Clob</span></span> |<span data-ttu-id="2322e-292">String</span><span class="sxs-lookup"><span data-stu-id="2322e-292">String</span></span> |
| <span data-ttu-id="2322e-293">Blob</span><span class="sxs-lookup"><span data-stu-id="2322e-293">Blob</span></span> |<span data-ttu-id="2322e-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2322e-294">Byte[]</span></span> |
| <span data-ttu-id="2322e-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="2322e-295">DbClob</span></span> |<span data-ttu-id="2322e-296">String</span><span class="sxs-lookup"><span data-stu-id="2322e-296">String</span></span> |
| <span data-ttu-id="2322e-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="2322e-297">SmallInt</span></span> |<span data-ttu-id="2322e-298">Int16</span><span class="sxs-lookup"><span data-stu-id="2322e-298">Int16</span></span> |
| <span data-ttu-id="2322e-299">Entero</span><span class="sxs-lookup"><span data-stu-id="2322e-299">Integer</span></span> |<span data-ttu-id="2322e-300">Int32</span><span class="sxs-lookup"><span data-stu-id="2322e-300">Int32</span></span> |
| <span data-ttu-id="2322e-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="2322e-301">BigInt</span></span> |<span data-ttu-id="2322e-302">Int64</span><span class="sxs-lookup"><span data-stu-id="2322e-302">Int64</span></span> |
| <span data-ttu-id="2322e-303">Real</span><span class="sxs-lookup"><span data-stu-id="2322e-303">Real</span></span> |<span data-ttu-id="2322e-304">Single</span><span class="sxs-lookup"><span data-stu-id="2322e-304">Single</span></span> |
| <span data-ttu-id="2322e-305">Doble</span><span class="sxs-lookup"><span data-stu-id="2322e-305">Double</span></span> |<span data-ttu-id="2322e-306">Doble</span><span class="sxs-lookup"><span data-stu-id="2322e-306">Double</span></span> |
| <span data-ttu-id="2322e-307">Float</span><span class="sxs-lookup"><span data-stu-id="2322e-307">Float</span></span> |<span data-ttu-id="2322e-308">Doble</span><span class="sxs-lookup"><span data-stu-id="2322e-308">Double</span></span> |
| <span data-ttu-id="2322e-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-309">Decimal</span></span> |<span data-ttu-id="2322e-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-310">Decimal</span></span> |
| <span data-ttu-id="2322e-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="2322e-311">DecimalFloat</span></span> |<span data-ttu-id="2322e-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-312">Decimal</span></span> |
| <span data-ttu-id="2322e-313">Numeric</span><span class="sxs-lookup"><span data-stu-id="2322e-313">Numeric</span></span> |<span data-ttu-id="2322e-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="2322e-314">Decimal</span></span> |
| <span data-ttu-id="2322e-315">Date</span><span class="sxs-lookup"><span data-stu-id="2322e-315">Date</span></span> |<span data-ttu-id="2322e-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="2322e-316">DateTime</span></span> |
| <span data-ttu-id="2322e-317">Hora</span><span class="sxs-lookup"><span data-stu-id="2322e-317">Time</span></span> |<span data-ttu-id="2322e-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2322e-318">TimeSpan</span></span> |
| <span data-ttu-id="2322e-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2322e-319">Timestamp</span></span> |<span data-ttu-id="2322e-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="2322e-320">DateTime</span></span> |
| <span data-ttu-id="2322e-321">xml</span><span class="sxs-lookup"><span data-stu-id="2322e-321">Xml</span></span> |<span data-ttu-id="2322e-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2322e-322">Byte[]</span></span> |
| <span data-ttu-id="2322e-323">Char</span><span class="sxs-lookup"><span data-stu-id="2322e-323">Char</span></span> |<span data-ttu-id="2322e-324">string</span><span class="sxs-lookup"><span data-stu-id="2322e-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="2322e-325">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="2322e-325">Map source to sink columns</span></span>
<span data-ttu-id="2322e-326">Para información sobre cómo asignar columnas en el conjunto de datos de origen a columnas en el conjunto de datos de receptor, consulte [Asignación de columnas de conjunto de datos en Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="2322e-327">Lecturas repetibles desde orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="2322e-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="2322e-328">Cuando se copian datos desde un almacén de datos relacionales, se debe tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="2322e-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="2322e-329">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="2322e-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2322e-330">También puede configurar la propiedad **policy** de reintentos para un conjunto de datos a fin de que se vuelva a ejecutar un segmento cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="2322e-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="2322e-331">Asegúrese de que se lean los mismos datos, sin importar cuántas veces se vuelve a ejecutar el segmento e independientemente de cómo se haga.</span><span class="sxs-lookup"><span data-stu-id="2322e-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="2322e-332">Para más información, consulte [Lecturas repetibles desde orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2322e-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2322e-333">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="2322e-333">Performance and tuning</span></span>
<span data-ttu-id="2322e-334">Obtenga información sobre los factores clave que afectan el rendimiento de la actividad de copia y las formas de optimizar el rendimiento en la [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="2322e-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>