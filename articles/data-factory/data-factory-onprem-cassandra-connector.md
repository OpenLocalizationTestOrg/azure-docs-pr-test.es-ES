---
title: Movimiento de datos de Cassandra mediante Data Factory | Microsoft Docs
description: Aprenda a mover los datos de una base de datos de Cassandra local con Data Factory de Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: f2b225bdbdf2880d26a6ab5f992301bf0a804b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="2f441-103">Movimiento de datos desde una base de datos de Cassandra local con Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="2f441-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="2f441-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos de una base de datos de Cassandra local.</span><span class="sxs-lookup"><span data-stu-id="2f441-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="2f441-105">Se basa en la información general ofrecida por el artículo sobre [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2f441-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="2f441-106">Puede copiar datos de un almacén de datos de Cassandra local a cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="2f441-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="2f441-107">Para ver una lista de almacenes de datos admitidos como receptores por la actividad de copia, consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2f441-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2f441-108">Data Factory solo admite actualmente el movimiento de datos desde un almacén de datos de Cassandra hasta otros almacenes de datos, pero no al contrario.</span><span class="sxs-lookup"><span data-stu-id="2f441-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="2f441-109">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="2f441-109">Supported versions</span></span>
<span data-ttu-id="2f441-110">El conector de Cassandra admite la versión 2.X de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2f441-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f441-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2f441-111">Prerequisites</span></span>
<span data-ttu-id="2f441-112">Para que el servicio de Azure Data Factory pueda conectarse a la base de datos de Cassandra local, se debe instalar Data Management Gateway en la misma máquina que hospeda la base de datos o en una máquina independiente, con el fin de evitar la competencia por los recursos con la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="2f441-113">Data Management Gateway es un componente que conecta orígenes de datos locales a servicios en la nube de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="2f441-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="2f441-114">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="2f441-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="2f441-115">Consulte el artículo [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para instrucciones paso a paso sobre cómo configurar la puerta de enlace como canalización de datos para mover datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="2f441-116">Debe usar la puerta de enlace para conectarse a una base de datos de Cassandra incluso si la base de datos está hospedada en la nube, por ejemplo, en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f441-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="2f441-117">Puede tener la puerta de enlace en la misma máquina virtual que hospeda la base de datos o en una máquina virtual independiente, siempre que la puerta de enlace se pueda conectar a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="2f441-118">Cuando instale la puerta de enlace, se instalará automáticamente el controlador ODBC de Microsoft Cassandra que se utiliza para establecer la conexión con la base de datos de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2f441-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="2f441-119">Por lo tanto, no es necesario instalar manualmente ningún controlador en la máquina de puerta de enlace cuando se copian datos desde la base de datos de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2f441-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="2f441-120">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f441-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2f441-121">Introducción</span><span class="sxs-lookup"><span data-stu-id="2f441-121">Getting started</span></span>
<span data-ttu-id="2f441-122">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="2f441-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2f441-123">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="2f441-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2f441-124">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="2f441-125">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="2f441-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2f441-126">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="2f441-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2f441-127">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="2f441-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="2f441-128">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="2f441-129">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="2f441-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="2f441-130">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="2f441-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2f441-131">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="2f441-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2f441-132">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2f441-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="2f441-133">Para ver un ejemplo con definiciones JSON para entidades de Data Factory que se usan para copiar datos de un almacén de datos de Cassandra local, consulte la sección [Ejemplo: Copia de datos de Cassandra en un blob de Azure](#json-example-copy-data-from-cassandra-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2f441-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2f441-134">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos de Cassandra:</span><span class="sxs-lookup"><span data-stu-id="2f441-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2f441-135">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="2f441-135">Linked service properties</span></span>
<span data-ttu-id="2f441-136">La tabla siguiente incluye una descripción de los elementos JSON específicos para el servicio vinculado de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2f441-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="2f441-137">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2f441-137">Property</span></span> | <span data-ttu-id="2f441-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f441-138">Description</span></span> | <span data-ttu-id="2f441-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f441-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f441-140">type</span><span class="sxs-lookup"><span data-stu-id="2f441-140">type</span></span> |<span data-ttu-id="2f441-141">La propiedad type debe estar establecida en: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="2f441-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="2f441-142">Sí</span><span class="sxs-lookup"><span data-stu-id="2f441-142">Yes</span></span> |
| <span data-ttu-id="2f441-143">host</span><span class="sxs-lookup"><span data-stu-id="2f441-143">host</span></span> |<span data-ttu-id="2f441-144">Una o varias direcciones IP o nombres de host de los servidores de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2f441-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="2f441-145">Especifica una lista de direcciones IP o nombres de host separada por comas para conectar con todos los servidores a la vez.</span><span class="sxs-lookup"><span data-stu-id="2f441-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="2f441-146">Sí</span><span class="sxs-lookup"><span data-stu-id="2f441-146">Yes</span></span> |
| <span data-ttu-id="2f441-147">puerto</span><span class="sxs-lookup"><span data-stu-id="2f441-147">port</span></span> |<span data-ttu-id="2f441-148">Puerto TCP que el servidor de Cassandra utiliza para escuchar las conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="2f441-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="2f441-149">No. El valor predeterminado es 9042.</span><span class="sxs-lookup"><span data-stu-id="2f441-149">No, default value: 9042</span></span> |
| <span data-ttu-id="2f441-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2f441-150">authenticationType</span></span> |<span data-ttu-id="2f441-151">Básica o anónima</span><span class="sxs-lookup"><span data-stu-id="2f441-151">Basic, or Anonymous</span></span> |<span data-ttu-id="2f441-152">Sí</span><span class="sxs-lookup"><span data-stu-id="2f441-152">Yes</span></span> |
| <span data-ttu-id="2f441-153">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="2f441-153">username</span></span> |<span data-ttu-id="2f441-154">Especifique el nombre de usuario de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="2f441-154">Specify user name for the user account.</span></span> |<span data-ttu-id="2f441-155">Sí, si el valor de authenticationType es Basic.</span><span class="sxs-lookup"><span data-stu-id="2f441-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="2f441-156">contraseña</span><span class="sxs-lookup"><span data-stu-id="2f441-156">password</span></span> |<span data-ttu-id="2f441-157">Especifique la contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="2f441-157">Specify password for the user account.</span></span> |<span data-ttu-id="2f441-158">Sí, si el valor de authenticationType es Basic.</span><span class="sxs-lookup"><span data-stu-id="2f441-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="2f441-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2f441-159">gatewayName</span></span> |<span data-ttu-id="2f441-160">Nombre de la puerta de enlace que se va a utilizar en la conexión con la base de datos de Cassandra local.</span><span class="sxs-lookup"><span data-stu-id="2f441-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="2f441-161">Sí</span><span class="sxs-lookup"><span data-stu-id="2f441-161">Yes</span></span> |
| <span data-ttu-id="2f441-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="2f441-162">encryptedCredential</span></span> |<span data-ttu-id="2f441-163">Credencial cifrada por la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f441-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="2f441-164">No</span><span class="sxs-lookup"><span data-stu-id="2f441-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2f441-165">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="2f441-165">Dataset properties</span></span>
<span data-ttu-id="2f441-166">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="2f441-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2f441-167">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="2f441-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2f441-168">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2f441-169">La sección typeProperties de los conjuntos de datos de tipo **CassandraTable** tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="2f441-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="2f441-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2f441-170">Property</span></span> | <span data-ttu-id="2f441-171">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f441-171">Description</span></span> | <span data-ttu-id="2f441-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f441-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f441-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="2f441-173">keyspace</span></span> |<span data-ttu-id="2f441-174">Nombre del espacio de claves o esquema de la base de datos de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2f441-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="2f441-175">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="2f441-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="2f441-176">tableName</span><span class="sxs-lookup"><span data-stu-id="2f441-176">tableName</span></span> |<span data-ttu-id="2f441-177">Nombre de la tabla de la base de datos de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2f441-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="2f441-178">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="2f441-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2f441-179">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="2f441-179">Copy activity properties</span></span>
<span data-ttu-id="2f441-180">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2f441-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2f441-181">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="2f441-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2f441-182">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="2f441-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="2f441-183">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="2f441-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="2f441-184">Si el origen es de tipo **CassandraSource**, estarán disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="2f441-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2f441-185">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2f441-185">Property</span></span> | <span data-ttu-id="2f441-186">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f441-186">Description</span></span> | <span data-ttu-id="2f441-187">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2f441-187">Allowed values</span></span> | <span data-ttu-id="2f441-188">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f441-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f441-189">query</span><span class="sxs-lookup"><span data-stu-id="2f441-189">query</span></span> |<span data-ttu-id="2f441-190">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-190">Use the custom query to read data.</span></span> |<span data-ttu-id="2f441-191">Consulta SQL-92 o consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="2f441-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="2f441-192">Vea la [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)(referencia de CQL).</span><span class="sxs-lookup"><span data-stu-id="2f441-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="2f441-193">Cuando utilice una consulta SQL, especifique **nombre de espacio de claves.nombre de tabla** para representar la tabla que quiere consultar.</span><span class="sxs-lookup"><span data-stu-id="2f441-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="2f441-194">No (si tableName y el espacio de claves del conjunto de datos están definidos).</span><span class="sxs-lookup"><span data-stu-id="2f441-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="2f441-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="2f441-195">consistencyLevel</span></span> |<span data-ttu-id="2f441-196">El nivel de coherencia establece el número de réplicas que deben responder a una solicitud de lectura antes de que se devuelvan datos a la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="2f441-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="2f441-197">Cassandra comprueba el número de réplicas especificado para que los datos satisfagan la solicitud de lectura.</span><span class="sxs-lookup"><span data-stu-id="2f441-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="2f441-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="2f441-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="2f441-199">Para más información, consulte [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configuración de la coherencia de datos).</span><span class="sxs-lookup"><span data-stu-id="2f441-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="2f441-200">No.</span><span class="sxs-lookup"><span data-stu-id="2f441-200">No.</span></span> <span data-ttu-id="2f441-201">El valor predeterminado es ONE.</span><span class="sxs-lookup"><span data-stu-id="2f441-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="2f441-202">Ejemplo con definiciones de JSON: copia de datos de Cassandra a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="2f441-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="2f441-203">Este ejemplo proporciona definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2f441-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2f441-204">Muestra cómo copiar datos de una base de datos de Cassandra local a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2f441-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="2f441-205">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f441-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f441-206">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="2f441-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="2f441-207">No incluye instrucciones paso a paso para crear la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="2f441-208">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2f441-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="2f441-209">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="2f441-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="2f441-210">Un servicio vinculado de tipo [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2f441-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="2f441-211">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="2f441-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="2f441-212">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2f441-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="2f441-213">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2f441-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="2f441-214">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que use [CassandraSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2f441-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2f441-215">**Servicio vinculado de Cassandra**</span><span class="sxs-lookup"><span data-stu-id="2f441-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="2f441-216">En este ejemplo, se utiliza el servicio vinculado de **Cassandra** .</span><span class="sxs-lookup"><span data-stu-id="2f441-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="2f441-217">Consulte la sección [Propiedades del servicio vinculado OnPremisesCassandra](#linked-service-properties) para ver las propiedades admitidas por el mismo.</span><span class="sxs-lookup"><span data-stu-id="2f441-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="2f441-218">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="2f441-218">**Azure Storage linked service:**</span></span>

```json
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

<span data-ttu-id="2f441-219">**Conjunto de datos de entrada de Cassandra**</span><span class="sxs-lookup"><span data-stu-id="2f441-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

<span data-ttu-id="2f441-220">Si se establece **external** en **true**, se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="2f441-221">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="2f441-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2f441-222">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="2f441-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="2f441-223">**Actividad de copia en una canalización con el origen de Cassandra y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="2f441-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="2f441-224">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="2f441-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2f441-225">En la definición de JSON de la canalización, el tipo de **origen** está establecido en **CassandraSource**, mientras que el tipo de **receptor** está establecido en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2f441-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="2f441-226">Consulte las [propiedades de tipo RelationalSource](#copy-activity-properties) para obtener la lista de propiedades admitidas por RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="2f441-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="2f441-227">Asignación de tipos de Cassandra</span><span class="sxs-lookup"><span data-stu-id="2f441-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="2f441-228">Tipo de Cassandra</span><span class="sxs-lookup"><span data-stu-id="2f441-228">Cassandra Type</span></span> | <span data-ttu-id="2f441-229">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="2f441-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="2f441-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="2f441-230">ASCII</span></span> |<span data-ttu-id="2f441-231">String</span><span class="sxs-lookup"><span data-stu-id="2f441-231">String</span></span> |
| <span data-ttu-id="2f441-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="2f441-232">BIGINT</span></span> |<span data-ttu-id="2f441-233">Int64</span><span class="sxs-lookup"><span data-stu-id="2f441-233">Int64</span></span> |
| <span data-ttu-id="2f441-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="2f441-234">BLOB</span></span> |<span data-ttu-id="2f441-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2f441-235">Byte[]</span></span> |
| <span data-ttu-id="2f441-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="2f441-236">BOOLEAN</span></span> |<span data-ttu-id="2f441-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="2f441-237">Boolean</span></span> |
| <span data-ttu-id="2f441-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="2f441-238">DECIMAL</span></span> |<span data-ttu-id="2f441-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="2f441-239">Decimal</span></span> |
| <span data-ttu-id="2f441-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="2f441-240">DOUBLE</span></span> |<span data-ttu-id="2f441-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="2f441-241">Double</span></span> |
| <span data-ttu-id="2f441-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="2f441-242">FLOAT</span></span> |<span data-ttu-id="2f441-243">Single</span><span class="sxs-lookup"><span data-stu-id="2f441-243">Single</span></span> |
| <span data-ttu-id="2f441-244">INET</span><span class="sxs-lookup"><span data-stu-id="2f441-244">INET</span></span> |<span data-ttu-id="2f441-245">String</span><span class="sxs-lookup"><span data-stu-id="2f441-245">String</span></span> |
| <span data-ttu-id="2f441-246">INT</span><span class="sxs-lookup"><span data-stu-id="2f441-246">INT</span></span> |<span data-ttu-id="2f441-247">Int32</span><span class="sxs-lookup"><span data-stu-id="2f441-247">Int32</span></span> |
| <span data-ttu-id="2f441-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="2f441-248">TEXT</span></span> |<span data-ttu-id="2f441-249">String</span><span class="sxs-lookup"><span data-stu-id="2f441-249">String</span></span> |
| <span data-ttu-id="2f441-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="2f441-250">TIMESTAMP</span></span> |<span data-ttu-id="2f441-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="2f441-251">DateTime</span></span> |
| <span data-ttu-id="2f441-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="2f441-252">TIMEUUID</span></span> |<span data-ttu-id="2f441-253">Guid</span><span class="sxs-lookup"><span data-stu-id="2f441-253">Guid</span></span> |
| <span data-ttu-id="2f441-254">UUID</span><span class="sxs-lookup"><span data-stu-id="2f441-254">UUID</span></span> |<span data-ttu-id="2f441-255">Guid</span><span class="sxs-lookup"><span data-stu-id="2f441-255">Guid</span></span> |
| <span data-ttu-id="2f441-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="2f441-256">VARCHAR</span></span> |<span data-ttu-id="2f441-257">String</span><span class="sxs-lookup"><span data-stu-id="2f441-257">String</span></span> |
| <span data-ttu-id="2f441-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="2f441-258">VARINT</span></span> |<span data-ttu-id="2f441-259">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="2f441-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="2f441-260">Par más información sobre tipos de colecciones (map, set, list, etc.), consulte la sección [Uso de colecciones con tablas virtuales](#work-with-collections-using-virtual-table) .</span><span class="sxs-lookup"><span data-stu-id="2f441-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="2f441-261">No se admiten tipos definidos por el usuario.</span><span class="sxs-lookup"><span data-stu-id="2f441-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="2f441-262">La longitud de la columna binaria y la columna de cadena no puede ser superior a 4000.</span><span class="sxs-lookup"><span data-stu-id="2f441-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="2f441-263">Uso de colecciones con tablas virtuales</span><span class="sxs-lookup"><span data-stu-id="2f441-263">Work with collections using virtual table</span></span>
<span data-ttu-id="2f441-264">Data Factory de Azure utiliza un controlador ODBC integrado para conectarse a una base de datos de Cassandra y copiar datos de dicha base de datos.</span><span class="sxs-lookup"><span data-stu-id="2f441-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="2f441-265">En el caso de los tipos de colección (como map, set y list), el controlador volverá a normalizar los datos en las tablas virtuales correspondientes.</span><span class="sxs-lookup"><span data-stu-id="2f441-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="2f441-266">En concreto, si una tabla contiene columnas de colecciones, el controlador generará las siguientes tablas virtuales:</span><span class="sxs-lookup"><span data-stu-id="2f441-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="2f441-267">Una **tabla base**, que contiene los mismos datos que la tabla real, salvo las columnas de colecciones.</span><span class="sxs-lookup"><span data-stu-id="2f441-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="2f441-268">La tabla base utiliza el mismo nombre que la tabla real a la que representa.</span><span class="sxs-lookup"><span data-stu-id="2f441-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="2f441-269">Una **tabla virtual** para cada columna de la colección, que ampliará los datos anidados.</span><span class="sxs-lookup"><span data-stu-id="2f441-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="2f441-270">Para asignar un nombre a las tablas virtuales que representan colecciones, se utiliza el nombre de la tabla real, un separador “*vt*” y el nombre de la columna.</span><span class="sxs-lookup"><span data-stu-id="2f441-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="2f441-271">Las tablas virtuales hacen referencia a los datos de la tabla real, lo que permite al controlador obtener acceso a los datos no normalizados.</span><span class="sxs-lookup"><span data-stu-id="2f441-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="2f441-272">Consulte la sección de ejemplo para más información.</span><span class="sxs-lookup"><span data-stu-id="2f441-272">See Example section for details.</span></span> <span data-ttu-id="2f441-273">Para acceder al contenido de las colecciones de Cassandra, puede crear consultas y combinar las tablas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2f441-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="2f441-274">Si usa el [Asistente para copia](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity), podrá consultar una vista intuitiva de la lista de tablas de la base de datos de Cassandra (incluidas las tablas virtuales) y una vista previa de los datos incluidos.</span><span class="sxs-lookup"><span data-stu-id="2f441-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="2f441-275">También puede crear una consulta en el Asistente para copia y validarla para ver el resultado.</span><span class="sxs-lookup"><span data-stu-id="2f441-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="2f441-276">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2f441-276">Example</span></span>
<span data-ttu-id="2f441-277">Por ejemplo, el siguiente “ExampleTable” es una tabla de una base de datos de Cassandra que contiene una columna de clave principal de enteros denominada “pk_int”, una columna de texto denominada “value”, una columna List, una columna Map y una columna Set (denominada “StringSet”).</span><span class="sxs-lookup"><span data-stu-id="2f441-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="2f441-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="2f441-278">pk_int</span></span> | <span data-ttu-id="2f441-279">Valor</span><span class="sxs-lookup"><span data-stu-id="2f441-279">Value</span></span> | <span data-ttu-id="2f441-280">Enumerar</span><span class="sxs-lookup"><span data-stu-id="2f441-280">List</span></span> | <span data-ttu-id="2f441-281">Map</span><span class="sxs-lookup"><span data-stu-id="2f441-281">Map</span></span> | <span data-ttu-id="2f441-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="2f441-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2f441-283">1</span><span class="sxs-lookup"><span data-stu-id="2f441-283">1</span></span> |<span data-ttu-id="2f441-284">"valor de ejemplo 1"</span><span class="sxs-lookup"><span data-stu-id="2f441-284">"sample value 1"</span></span> |<span data-ttu-id="2f441-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="2f441-285">["1", "2", "3"]</span></span> |<span data-ttu-id="2f441-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="2f441-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="2f441-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="2f441-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="2f441-288">3</span><span class="sxs-lookup"><span data-stu-id="2f441-288">3</span></span> |<span data-ttu-id="2f441-289">"valor de ejemplo 3"</span><span class="sxs-lookup"><span data-stu-id="2f441-289">"sample value 3"</span></span> |<span data-ttu-id="2f441-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="2f441-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="2f441-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="2f441-291">{"S1": "t"}</span></span> |<span data-ttu-id="2f441-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="2f441-292">{"A", "E"}</span></span> |

<span data-ttu-id="2f441-293">El controlador generará varias tablas virtuales que representan a esta tabla.</span><span class="sxs-lookup"><span data-stu-id="2f441-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="2f441-294">Las columnas de clave externa de las tablas virtuales hacen referencia a las columnas de clave principal de la tabla real e indican qué fila de la tabla real se corresponde con la fila de la tabla virtual.</span><span class="sxs-lookup"><span data-stu-id="2f441-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="2f441-295">La primera tabla virtual es la tabla base y se denomina “ExampleTable”, tal y como se muestra en la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="2f441-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="2f441-296">La tabla base contiene los mismos datos que la tabla de base de datos original a excepción de las colecciones, que no aparecen en esta tabla, sino que se amplían en otras tablas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2f441-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="2f441-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="2f441-297">pk_int</span></span> | <span data-ttu-id="2f441-298">Valor</span><span class="sxs-lookup"><span data-stu-id="2f441-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2f441-299">1</span><span class="sxs-lookup"><span data-stu-id="2f441-299">1</span></span> |<span data-ttu-id="2f441-300">"valor de ejemplo 1"</span><span class="sxs-lookup"><span data-stu-id="2f441-300">"sample value 1"</span></span> |
| <span data-ttu-id="2f441-301">3</span><span class="sxs-lookup"><span data-stu-id="2f441-301">3</span></span> |<span data-ttu-id="2f441-302">"valor de ejemplo 3"</span><span class="sxs-lookup"><span data-stu-id="2f441-302">"sample value 3"</span></span> |

<span data-ttu-id="2f441-303">Las tablas siguientes representan las tablas virtuales que normalizan de nuevo los datos de las columnas List, Map y StringSet.</span><span class="sxs-lookup"><span data-stu-id="2f441-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="2f441-304">Las columnas cuyos nombres terminan en “_index” o “_key” indican la posición de los datos en la columna List o Map original.</span><span class="sxs-lookup"><span data-stu-id="2f441-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="2f441-305">Las columnas cuyos nombres terminan en “_value” contienen los datos ampliados de la colección.</span><span class="sxs-lookup"><span data-stu-id="2f441-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="2f441-306">Tabla “ExampleTable_vt_List”:</span><span class="sxs-lookup"><span data-stu-id="2f441-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="2f441-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="2f441-307">pk_int</span></span> | <span data-ttu-id="2f441-308">List_index</span><span class="sxs-lookup"><span data-stu-id="2f441-308">List_index</span></span> | <span data-ttu-id="2f441-309">List_value</span><span class="sxs-lookup"><span data-stu-id="2f441-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f441-310">1</span><span class="sxs-lookup"><span data-stu-id="2f441-310">1</span></span> |<span data-ttu-id="2f441-311">0</span><span class="sxs-lookup"><span data-stu-id="2f441-311">0</span></span> |<span data-ttu-id="2f441-312">1</span><span class="sxs-lookup"><span data-stu-id="2f441-312">1</span></span> |
| <span data-ttu-id="2f441-313">1</span><span class="sxs-lookup"><span data-stu-id="2f441-313">1</span></span> |<span data-ttu-id="2f441-314">1</span><span class="sxs-lookup"><span data-stu-id="2f441-314">1</span></span> |<span data-ttu-id="2f441-315">2</span><span class="sxs-lookup"><span data-stu-id="2f441-315">2</span></span> |
| <span data-ttu-id="2f441-316">1</span><span class="sxs-lookup"><span data-stu-id="2f441-316">1</span></span> |<span data-ttu-id="2f441-317">2</span><span class="sxs-lookup"><span data-stu-id="2f441-317">2</span></span> |<span data-ttu-id="2f441-318">3</span><span class="sxs-lookup"><span data-stu-id="2f441-318">3</span></span> |
| <span data-ttu-id="2f441-319">3</span><span class="sxs-lookup"><span data-stu-id="2f441-319">3</span></span> |<span data-ttu-id="2f441-320">0</span><span class="sxs-lookup"><span data-stu-id="2f441-320">0</span></span> |<span data-ttu-id="2f441-321">100</span><span class="sxs-lookup"><span data-stu-id="2f441-321">100</span></span> |
| <span data-ttu-id="2f441-322">3</span><span class="sxs-lookup"><span data-stu-id="2f441-322">3</span></span> |<span data-ttu-id="2f441-323">1</span><span class="sxs-lookup"><span data-stu-id="2f441-323">1</span></span> |<span data-ttu-id="2f441-324">101</span><span class="sxs-lookup"><span data-stu-id="2f441-324">101</span></span> |
| <span data-ttu-id="2f441-325">3</span><span class="sxs-lookup"><span data-stu-id="2f441-325">3</span></span> |<span data-ttu-id="2f441-326">2</span><span class="sxs-lookup"><span data-stu-id="2f441-326">2</span></span> |<span data-ttu-id="2f441-327">102</span><span class="sxs-lookup"><span data-stu-id="2f441-327">102</span></span> |
| <span data-ttu-id="2f441-328">3</span><span class="sxs-lookup"><span data-stu-id="2f441-328">3</span></span> |<span data-ttu-id="2f441-329">3</span><span class="sxs-lookup"><span data-stu-id="2f441-329">3</span></span> |<span data-ttu-id="2f441-330">103</span><span class="sxs-lookup"><span data-stu-id="2f441-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="2f441-331">Tabla “ExampleTable_vt_Map”:</span><span class="sxs-lookup"><span data-stu-id="2f441-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="2f441-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="2f441-332">pk_int</span></span> | <span data-ttu-id="2f441-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="2f441-333">Map_key</span></span> | <span data-ttu-id="2f441-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="2f441-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f441-335">1</span><span class="sxs-lookup"><span data-stu-id="2f441-335">1</span></span> |<span data-ttu-id="2f441-336">S1</span><span class="sxs-lookup"><span data-stu-id="2f441-336">S1</span></span> |<span data-ttu-id="2f441-337">Una </span><span class="sxs-lookup"><span data-stu-id="2f441-337">A</span></span> |
| <span data-ttu-id="2f441-338">1</span><span class="sxs-lookup"><span data-stu-id="2f441-338">1</span></span> |<span data-ttu-id="2f441-339">S2</span><span class="sxs-lookup"><span data-stu-id="2f441-339">S2</span></span> |<span data-ttu-id="2f441-340">b</span><span class="sxs-lookup"><span data-stu-id="2f441-340">b</span></span> |
| <span data-ttu-id="2f441-341">3</span><span class="sxs-lookup"><span data-stu-id="2f441-341">3</span></span> |<span data-ttu-id="2f441-342">S1</span><span class="sxs-lookup"><span data-stu-id="2f441-342">S1</span></span> |<span data-ttu-id="2f441-343">t</span><span class="sxs-lookup"><span data-stu-id="2f441-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="2f441-344">Tabla “ExampleTable_vt_StringSet”:</span><span class="sxs-lookup"><span data-stu-id="2f441-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="2f441-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="2f441-345">pk_int</span></span> | <span data-ttu-id="2f441-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="2f441-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="2f441-347">1</span><span class="sxs-lookup"><span data-stu-id="2f441-347">1</span></span> |<span data-ttu-id="2f441-348">Una </span><span class="sxs-lookup"><span data-stu-id="2f441-348">A</span></span> |
| <span data-ttu-id="2f441-349">1</span><span class="sxs-lookup"><span data-stu-id="2f441-349">1</span></span> |<span data-ttu-id="2f441-350">b</span><span class="sxs-lookup"><span data-stu-id="2f441-350">B</span></span> |
| <span data-ttu-id="2f441-351">1</span><span class="sxs-lookup"><span data-stu-id="2f441-351">1</span></span> |<span data-ttu-id="2f441-352">C</span><span class="sxs-lookup"><span data-stu-id="2f441-352">C</span></span> |
| <span data-ttu-id="2f441-353">3</span><span class="sxs-lookup"><span data-stu-id="2f441-353">3</span></span> |<span data-ttu-id="2f441-354">Una </span><span class="sxs-lookup"><span data-stu-id="2f441-354">A</span></span> |
| <span data-ttu-id="2f441-355">3</span><span class="sxs-lookup"><span data-stu-id="2f441-355">3</span></span> |<span data-ttu-id="2f441-356">E</span><span class="sxs-lookup"><span data-stu-id="2f441-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="2f441-357">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="2f441-357">Map source to sink columns</span></span>
<span data-ttu-id="2f441-358">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2f441-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2f441-359">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="2f441-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="2f441-360">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="2f441-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="2f441-361">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="2f441-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2f441-362">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="2f441-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2f441-363">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="2f441-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2f441-364">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2f441-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2f441-365">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="2f441-365">Performance and Tuning</span></span>
<span data-ttu-id="2f441-366">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="2f441-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
