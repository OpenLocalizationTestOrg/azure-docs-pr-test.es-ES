---
title: Movimiento de datos de MongoDB mediante Data Factory | Microsoft Docs
description: "Obtenga información acerca de cómo mover los datos de la base de datos de MongoDB mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: ac4ff55c765a5b874b81714c3d0063a5b4765a05
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="af13b-103">Movimiento de datos de MongoDB mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="af13b-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="af13b-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos de una base de datos MongoDB local.</span><span class="sxs-lookup"><span data-stu-id="af13b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="af13b-105">Se basa en la información general que ofrece el artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="af13b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="af13b-106">Puede copiar datos desde un almacén de datos de MongoDB local a cualquier almacén de datos del receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="af13b-106">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="af13b-107">Para ver una lista de almacenes de datos admitidos como receptores por la actividad de copia, consulte la tabla [Almacenes de datos y formatos que se admiten](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="af13b-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="af13b-108">Data Factory solo admite actualmente el movimiento de datos de un almacén de datos de MongoDB a otros almacenes de datos, pero no el movimiento de datos de otros almacenes de datos a una base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="af13b-108">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="af13b-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="af13b-109">Prerequisites</span></span>
<span data-ttu-id="af13b-110">Para que el servicio Data Factory de Azure pueda conectarse a la base de datos de MongoDB local, debe instalar los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="af13b-110">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="af13b-111">Versiones admitidas de MongoDB: 2.4, 2.6, 3.0 y 3.2.</span><span class="sxs-lookup"><span data-stu-id="af13b-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="af13b-112">Data Management Gateway en el mismo equipo que hospede la base de datos o en un equipo independiente para evitar la competencia por los recursos con la base de datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-112">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="af13b-113">Data Management Gateway es un software que conecta orígenes de datos locales a servicios en la nube de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="af13b-113">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="af13b-114">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="af13b-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="af13b-115">Consulte el artículo [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para instrucciones paso a paso sobre cómo configurar la puerta de enlace como canalización de datos para mover datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="af13b-116">Cuando instale la puerta de enlace, se instalará automáticamente el controlador ODBC de Microsoft MongoDB que se utiliza para establecer la conexión con MongoDB.</span><span class="sxs-lookup"><span data-stu-id="af13b-116">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af13b-117">Tiene que usar la puerta de enlace para conectar con MongoDB, incluso si está hospedado en máquinas virtuales de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="af13b-117">You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="af13b-118">Si está intentando conectarse a una instancia de MongoDB hospedada en la nube, también puede instalar la instancia de puerta de enlace en la máquina virtual de IaaS.</span><span class="sxs-lookup"><span data-stu-id="af13b-118">If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="af13b-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="af13b-119">Getting started</span></span>
<span data-ttu-id="af13b-120">Puede crear una canalización con actividad de copia que mueva los datos desde un almacén de datos MongoDB local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="af13b-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="af13b-121">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="af13b-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="af13b-122">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="af13b-123">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="af13b-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="af13b-124">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="af13b-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="af13b-125">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="af13b-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="af13b-126">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="af13b-127">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="af13b-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="af13b-128">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="af13b-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="af13b-129">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="af13b-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="af13b-130">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="af13b-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="af13b-131">Para obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan para copiar los datos de un almacén de datos de MongoDB local, consulte la sección [Ejemplo de JSON: Copiar datos de MongoDB a un blob de Azure](#json-example-copy-data-from-mongodb-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="af13b-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="af13b-132">En las secciones siguientes se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="af13b-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="af13b-133">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="af13b-133">Linked service properties</span></span>
<span data-ttu-id="af13b-134">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de **OnPremisesMongoDB** .</span><span class="sxs-lookup"><span data-stu-id="af13b-134">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="af13b-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="af13b-135">Property</span></span> | <span data-ttu-id="af13b-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="af13b-136">Description</span></span> | <span data-ttu-id="af13b-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="af13b-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af13b-138">type</span><span class="sxs-lookup"><span data-stu-id="af13b-138">type</span></span> |<span data-ttu-id="af13b-139">La propiedad type debe establecerse en: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="af13b-139">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="af13b-140">Sí</span><span class="sxs-lookup"><span data-stu-id="af13b-140">Yes</span></span> |
| <span data-ttu-id="af13b-141">server</span><span class="sxs-lookup"><span data-stu-id="af13b-141">server</span></span> |<span data-ttu-id="af13b-142">Dirección IP o nombre de host del servidor de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="af13b-142">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="af13b-143">Sí</span><span class="sxs-lookup"><span data-stu-id="af13b-143">Yes</span></span> |
| <span data-ttu-id="af13b-144">puerto</span><span class="sxs-lookup"><span data-stu-id="af13b-144">port</span></span> |<span data-ttu-id="af13b-145">Puerto TCP que el servidor de MongoDB utiliza para escuchar las conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="af13b-145">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="af13b-146">Valor predeterminado opcional: 27017</span><span class="sxs-lookup"><span data-stu-id="af13b-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="af13b-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="af13b-147">authenticationType</span></span> |<span data-ttu-id="af13b-148">Básica o anónima.</span><span class="sxs-lookup"><span data-stu-id="af13b-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="af13b-149">Sí</span><span class="sxs-lookup"><span data-stu-id="af13b-149">Yes</span></span> |
| <span data-ttu-id="af13b-150">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="af13b-150">username</span></span> |<span data-ttu-id="af13b-151">Cuenta de usuario para tener acceso a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="af13b-151">User account to access MongoDB.</span></span> |<span data-ttu-id="af13b-152">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="af13b-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="af13b-153">contraseña</span><span class="sxs-lookup"><span data-stu-id="af13b-153">password</span></span> |<span data-ttu-id="af13b-154">Contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="af13b-154">Password for the user.</span></span> |<span data-ttu-id="af13b-155">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="af13b-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="af13b-156">authSource</span><span class="sxs-lookup"><span data-stu-id="af13b-156">authSource</span></span> |<span data-ttu-id="af13b-157">Nombre de la base de datos de MongoDB que desea usar para comprobar las credenciales de autenticación.</span><span class="sxs-lookup"><span data-stu-id="af13b-157">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="af13b-158">Opcional (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="af13b-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="af13b-159">Valor predeterminado: se utiliza la cuenta de administrador y la base de datos especificada mediante la propiedad databaseName.</span><span class="sxs-lookup"><span data-stu-id="af13b-159">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="af13b-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="af13b-160">databaseName</span></span> |<span data-ttu-id="af13b-161">Nombre de la base de datos de MongoDB a la que desea acceder.</span><span class="sxs-lookup"><span data-stu-id="af13b-161">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="af13b-162">Sí</span><span class="sxs-lookup"><span data-stu-id="af13b-162">Yes</span></span> |
| <span data-ttu-id="af13b-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="af13b-163">gatewayName</span></span> |<span data-ttu-id="af13b-164">Nombre de la puerta de enlace que accede al almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-164">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="af13b-165">Sí</span><span class="sxs-lookup"><span data-stu-id="af13b-165">Yes</span></span> |
| <span data-ttu-id="af13b-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="af13b-166">encryptedCredential</span></span> |<span data-ttu-id="af13b-167">Credencial cifrada por la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="af13b-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="af13b-168">Opcional</span><span class="sxs-lookup"><span data-stu-id="af13b-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="af13b-169">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="af13b-169">Dataset properties</span></span>
<span data-ttu-id="af13b-170">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="af13b-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="af13b-171">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="af13b-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="af13b-172">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-172">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="af13b-173">La sección typeProperties del conjunto de datos de tipo **MongoDbCollection** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="af13b-173">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="af13b-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="af13b-174">Property</span></span> | <span data-ttu-id="af13b-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="af13b-175">Description</span></span> | <span data-ttu-id="af13b-176">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="af13b-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af13b-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="af13b-177">collectionName</span></span> |<span data-ttu-id="af13b-178">Nombre de la colección en la base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="af13b-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="af13b-179">Sí</span><span class="sxs-lookup"><span data-stu-id="af13b-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="af13b-180">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="af13b-180">Copy activity properties</span></span>
<span data-ttu-id="af13b-181">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="af13b-181">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="af13b-182">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="af13b-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="af13b-183">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="af13b-183">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="af13b-184">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="af13b-184">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="af13b-185">Si el origen es de tipo **MongoDbSource** , estarán disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="af13b-185">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="af13b-186">Propiedad</span><span class="sxs-lookup"><span data-stu-id="af13b-186">Property</span></span> | <span data-ttu-id="af13b-187">Descripción</span><span class="sxs-lookup"><span data-stu-id="af13b-187">Description</span></span> | <span data-ttu-id="af13b-188">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="af13b-188">Allowed values</span></span> | <span data-ttu-id="af13b-189">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="af13b-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="af13b-190">query</span><span class="sxs-lookup"><span data-stu-id="af13b-190">query</span></span> |<span data-ttu-id="af13b-191">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-191">Use the custom query to read data.</span></span> |<span data-ttu-id="af13b-192">Cadena de consulta SQL-92.</span><span class="sxs-lookup"><span data-stu-id="af13b-192">SQL-92 query string.</span></span> <span data-ttu-id="af13b-193">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="af13b-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="af13b-194">No (si se especifica **collectionName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="af13b-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="af13b-195">Ejemplo de JSON: Copiar datos de MongoDB a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="af13b-195">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="af13b-196">En este ejemplo se proporcionan definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="af13b-196">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="af13b-197">Muestra cómo copiar datos de una base de datos MongoDB local a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="af13b-197">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="af13b-198">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="af13b-198">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="af13b-199">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="af13b-199">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="af13b-200">Un servicio vinculado de tipo [OnPremisesMongoDB](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af13b-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="af13b-201">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="af13b-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="af13b-202">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="af13b-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="af13b-203">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="af13b-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="af13b-204">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [MongoDBSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="af13b-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="af13b-205">El ejemplo copia cada hora los datos de un resultado de consulta de la base de datos de MongoDB en un blob.</span><span class="sxs-lookup"><span data-stu-id="af13b-205">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="af13b-206">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="af13b-206">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="af13b-207">Como primer paso, configure la puerta de enlace de administración de datos según las instrucciones del artículo [Puerta de enlace de administración de datos](data-factory-data-management-gateway.md) .</span><span class="sxs-lookup"><span data-stu-id="af13b-207">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="af13b-208">**Servicio vinculado de MongoDB:**</span><span class="sxs-lookup"><span data-stu-id="af13b-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="af13b-209">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="af13b-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="af13b-210">**Conjunto de datos de entrada de MongoDB**: si “external” se establece en “true”, se informa al servicio Data Factory de que la tabla es externa a la factoría de datos y que no la genera ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="af13b-210">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="af13b-211">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="af13b-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="af13b-212">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="af13b-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="af13b-213">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="af13b-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="af13b-214">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="af13b-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="af13b-215">**Actividad de copia en una canalización con el origen MongoDB y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="af13b-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="af13b-216">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="af13b-216">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="af13b-217">En la definición de la canalización JSON, el tipo **source** se establece en **MongoDbSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="af13b-217">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="af13b-218">La consulta SQL especificada para la propiedad **query** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="af13b-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="af13b-219">Esquema de Data Factory</span><span class="sxs-lookup"><span data-stu-id="af13b-219">Schema by Data Factory</span></span>
<span data-ttu-id="af13b-220">El servicio de Data Factory de Azure deduce el esquema de una colección de MongoDB mediante el uso de los últimos 100 documentos de la colección.</span><span class="sxs-lookup"><span data-stu-id="af13b-220">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="af13b-221">Si estos 100 documentos no contienen el esquema completo, se pueden omitir algunas columnas durante la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="af13b-221">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="af13b-222">Asignación de tipos para MongoDB</span><span class="sxs-lookup"><span data-stu-id="af13b-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="af13b-223">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="af13b-223">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="af13b-224">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="af13b-224">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="af13b-225">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="af13b-225">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="af13b-226">Al mover datos a MongoDB, se usarán las asignaciones siguientes de tipos MongoDB a tipos .NET.</span><span class="sxs-lookup"><span data-stu-id="af13b-226">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="af13b-227">Tipo de MongoDB</span><span class="sxs-lookup"><span data-stu-id="af13b-227">MongoDB type</span></span> | <span data-ttu-id="af13b-228">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="af13b-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="af13b-229">Binary</span><span class="sxs-lookup"><span data-stu-id="af13b-229">Binary</span></span> |<span data-ttu-id="af13b-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="af13b-230">Byte[]</span></span> |
| <span data-ttu-id="af13b-231">Booleano</span><span class="sxs-lookup"><span data-stu-id="af13b-231">Boolean</span></span> |<span data-ttu-id="af13b-232">Booleano</span><span class="sxs-lookup"><span data-stu-id="af13b-232">Boolean</span></span> |
| <span data-ttu-id="af13b-233">Date</span><span class="sxs-lookup"><span data-stu-id="af13b-233">Date</span></span> |<span data-ttu-id="af13b-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="af13b-234">DateTime</span></span> |
| <span data-ttu-id="af13b-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="af13b-235">NumberDouble</span></span> |<span data-ttu-id="af13b-236">Doble</span><span class="sxs-lookup"><span data-stu-id="af13b-236">Double</span></span> |
| <span data-ttu-id="af13b-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="af13b-237">NumberInt</span></span> |<span data-ttu-id="af13b-238">Int32</span><span class="sxs-lookup"><span data-stu-id="af13b-238">Int32</span></span> |
| <span data-ttu-id="af13b-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="af13b-239">NumberLong</span></span> |<span data-ttu-id="af13b-240">Int64</span><span class="sxs-lookup"><span data-stu-id="af13b-240">Int64</span></span> |
| <span data-ttu-id="af13b-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="af13b-241">ObjectID</span></span> |<span data-ttu-id="af13b-242">String</span><span class="sxs-lookup"><span data-stu-id="af13b-242">String</span></span> |
| <span data-ttu-id="af13b-243">String</span><span class="sxs-lookup"><span data-stu-id="af13b-243">String</span></span> |<span data-ttu-id="af13b-244">String</span><span class="sxs-lookup"><span data-stu-id="af13b-244">String</span></span> |
| <span data-ttu-id="af13b-245">UUID</span><span class="sxs-lookup"><span data-stu-id="af13b-245">UUID</span></span> |<span data-ttu-id="af13b-246">Guid</span><span class="sxs-lookup"><span data-stu-id="af13b-246">Guid</span></span> |
| <span data-ttu-id="af13b-247">Objeto</span><span class="sxs-lookup"><span data-stu-id="af13b-247">Object</span></span> |<span data-ttu-id="af13b-248">Renormalizado en columnas acopladas con “_” como separador anidado</span><span class="sxs-lookup"><span data-stu-id="af13b-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="af13b-249">Para más información sobre la compatibilidad para matrices con tablas virtuales, consulte la sección [Compatibilidad para tipos complejos que usan tablas virtuales](#support-for-complex-types-using-virtual-tables) que aparece más adelante.</span><span class="sxs-lookup"><span data-stu-id="af13b-249">To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="af13b-250">Actualmente, no se admiten los siguientes tipos de datos de MongoDB: DBPointer, JavaScript, Clave Max y Min, Expresión regular, Símbolo, Marca de tiempo, Sin definir</span><span class="sxs-lookup"><span data-stu-id="af13b-250">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="af13b-251">Compatibilidad para tipos complejos que usan tablas virtuales</span><span class="sxs-lookup"><span data-stu-id="af13b-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="af13b-252">Data Factory de Azure utiliza un controlador ODBC integrado para conectarse a una base de datos de MongoDB y copiar datos de dicha base de datos.</span><span class="sxs-lookup"><span data-stu-id="af13b-252">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="af13b-253">Para los tipos complejos como matrices u objetos con diferentes tipos en los documentos, el controlador volverá a normalizar los datos en las tablas virtuales correspondientes.</span><span class="sxs-lookup"><span data-stu-id="af13b-253">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="af13b-254">En concreto, si una tabla contiene estas columnas, el controlador generará las siguientes tablas virtuales:</span><span class="sxs-lookup"><span data-stu-id="af13b-254">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="af13b-255">Una **tabla base**, que contiene los mismos datos que la tabla real, salvo las columnas de tipo complejo.</span><span class="sxs-lookup"><span data-stu-id="af13b-255">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="af13b-256">La tabla base utiliza el mismo nombre que la tabla real a la que representa.</span><span class="sxs-lookup"><span data-stu-id="af13b-256">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="af13b-257">Una **tabla virtual** para cada columna de tipo complejo, que ampliará los datos anidados.</span><span class="sxs-lookup"><span data-stu-id="af13b-257">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="af13b-258">Para asignar un nombre a las tablas virtuales, se utiliza el nombre de la tabla real, un separador “_” y el nombre de la matriz u objeto.</span><span class="sxs-lookup"><span data-stu-id="af13b-258">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="af13b-259">Las tablas virtuales hacen referencia a los datos de la tabla real, lo que permite al controlador obtener acceso a los datos no normalizados.</span><span class="sxs-lookup"><span data-stu-id="af13b-259">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="af13b-260">Consulte el ejemplo de la siguiente sección para más información.</span><span class="sxs-lookup"><span data-stu-id="af13b-260">See Example section below details.</span></span> <span data-ttu-id="af13b-261">Para acceder al contenido de las matrices de MongoDB, puede crear consultas y combinar las tablas virtuales.</span><span class="sxs-lookup"><span data-stu-id="af13b-261">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="af13b-262">Puede utilizar el [Asistente para copia](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) para consultar una vista intuitiva de la lista de tablas de la base de datos de MongoDB (incluidas las tablas virtuales) y una vista previa de los datos incluidos.</span><span class="sxs-lookup"><span data-stu-id="af13b-262">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="af13b-263">También puede crear una consulta en el Asistente para copia y validarla para ver el resultado.</span><span class="sxs-lookup"><span data-stu-id="af13b-263">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="af13b-264">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="af13b-264">Example</span></span>
<span data-ttu-id="af13b-265">Por ejemplo, la tabla “ExampleTable” que aparece a continuación es una tabla de MongoDB que tiene una columna con una matriz de objetos en cada celda: Facturas y una columna con una matriz de tipos escalares: Clasificaciones.</span><span class="sxs-lookup"><span data-stu-id="af13b-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="af13b-266">_id</span><span class="sxs-lookup"><span data-stu-id="af13b-266">_id</span></span> | <span data-ttu-id="af13b-267">Nombre del cliente</span><span class="sxs-lookup"><span data-stu-id="af13b-267">Customer Name</span></span> | <span data-ttu-id="af13b-268">Facturas</span><span class="sxs-lookup"><span data-stu-id="af13b-268">Invoices</span></span> | <span data-ttu-id="af13b-269">Nivel de servicios</span><span class="sxs-lookup"><span data-stu-id="af13b-269">Service Level</span></span> | <span data-ttu-id="af13b-270">Clasificaciones</span><span class="sxs-lookup"><span data-stu-id="af13b-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="af13b-271">1111</span><span class="sxs-lookup"><span data-stu-id="af13b-271">1111</span></span> |<span data-ttu-id="af13b-272">ABC</span><span class="sxs-lookup"><span data-stu-id="af13b-272">ABC</span></span> |<span data-ttu-id="af13b-273">[{invoice_id:”123”, artículo:”tostadora”, precio:”456”, descuento:”0.2”}, {invoice_id:”124”, artículo:”horno”, precio: ”1235”, descuento: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="af13b-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="af13b-274">Silver</span><span class="sxs-lookup"><span data-stu-id="af13b-274">Silver</span></span> |<span data-ttu-id="af13b-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="af13b-275">[5,6]</span></span> |
| <span data-ttu-id="af13b-276">2222</span><span class="sxs-lookup"><span data-stu-id="af13b-276">2222</span></span> |<span data-ttu-id="af13b-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="af13b-277">XYZ</span></span> |<span data-ttu-id="af13b-278">[{invoice_id:”135”, artículo:”frigorífico”, precio: ”12543”, descuento: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="af13b-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="af13b-279">Gold</span><span class="sxs-lookup"><span data-stu-id="af13b-279">Gold</span></span> |<span data-ttu-id="af13b-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="af13b-280">[1,2]</span></span> |

<span data-ttu-id="af13b-281">El controlador generará varias tablas virtuales que representan a esta tabla.</span><span class="sxs-lookup"><span data-stu-id="af13b-281">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="af13b-282">La primera tabla virtual es la tabla base y se denomina “ExampleTable”, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="af13b-282">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="af13b-283">La tabla base contiene todos los datos de la tabla original, pero los datos de las matrices se han omitido y se ampliarán en las tablas virtuales.</span><span class="sxs-lookup"><span data-stu-id="af13b-283">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="af13b-284">_id</span><span class="sxs-lookup"><span data-stu-id="af13b-284">_id</span></span> | <span data-ttu-id="af13b-285">Nombre del cliente</span><span class="sxs-lookup"><span data-stu-id="af13b-285">Customer Name</span></span> | <span data-ttu-id="af13b-286">Nivel de servicios</span><span class="sxs-lookup"><span data-stu-id="af13b-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af13b-287">1111</span><span class="sxs-lookup"><span data-stu-id="af13b-287">1111</span></span> |<span data-ttu-id="af13b-288">ABC</span><span class="sxs-lookup"><span data-stu-id="af13b-288">ABC</span></span> |<span data-ttu-id="af13b-289">Silver</span><span class="sxs-lookup"><span data-stu-id="af13b-289">Silver</span></span> |
| <span data-ttu-id="af13b-290">2222</span><span class="sxs-lookup"><span data-stu-id="af13b-290">2222</span></span> |<span data-ttu-id="af13b-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="af13b-291">XYZ</span></span> |<span data-ttu-id="af13b-292">Gold</span><span class="sxs-lookup"><span data-stu-id="af13b-292">Gold</span></span> |

<span data-ttu-id="af13b-293">Las siguientes tablas muestran las tablas virtuales que representan las matrices originales en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="af13b-293">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="af13b-294">Estas tablas contienen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="af13b-294">These tables contain the following:</span></span>

* <span data-ttu-id="af13b-295">Una referencia a la columna de clave principal original correspondiente a la fila de la matriz original (a través del identificador de la columna)</span><span class="sxs-lookup"><span data-stu-id="af13b-295">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="af13b-296">Una indicación de la posición de los datos dentro de la matriz original</span><span class="sxs-lookup"><span data-stu-id="af13b-296">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="af13b-297">Los datos ampliados para cada elemento de la matriz</span><span class="sxs-lookup"><span data-stu-id="af13b-297">The expanded data for each element within the array</span></span>

<span data-ttu-id="af13b-298">Tabla “ExampleTable_Invoices”:</span><span class="sxs-lookup"><span data-stu-id="af13b-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="af13b-299">_id</span><span class="sxs-lookup"><span data-stu-id="af13b-299">_id</span></span> | <span data-ttu-id="af13b-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="af13b-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="af13b-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="af13b-301">invoice_id</span></span> | <span data-ttu-id="af13b-302">item</span><span class="sxs-lookup"><span data-stu-id="af13b-302">item</span></span> | <span data-ttu-id="af13b-303">price</span><span class="sxs-lookup"><span data-stu-id="af13b-303">price</span></span> | <span data-ttu-id="af13b-304">Descuento</span><span class="sxs-lookup"><span data-stu-id="af13b-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="af13b-305">1111</span><span class="sxs-lookup"><span data-stu-id="af13b-305">1111</span></span> |<span data-ttu-id="af13b-306">0</span><span class="sxs-lookup"><span data-stu-id="af13b-306">0</span></span> |<span data-ttu-id="af13b-307">123</span><span class="sxs-lookup"><span data-stu-id="af13b-307">123</span></span> |<span data-ttu-id="af13b-308">tostadora</span><span class="sxs-lookup"><span data-stu-id="af13b-308">toaster</span></span> |<span data-ttu-id="af13b-309">456</span><span class="sxs-lookup"><span data-stu-id="af13b-309">456</span></span> |<span data-ttu-id="af13b-310">0,2</span><span class="sxs-lookup"><span data-stu-id="af13b-310">0.2</span></span> |
| <span data-ttu-id="af13b-311">1111</span><span class="sxs-lookup"><span data-stu-id="af13b-311">1111</span></span> |<span data-ttu-id="af13b-312">1</span><span class="sxs-lookup"><span data-stu-id="af13b-312">1</span></span> |<span data-ttu-id="af13b-313">124</span><span class="sxs-lookup"><span data-stu-id="af13b-313">124</span></span> |<span data-ttu-id="af13b-314">horno</span><span class="sxs-lookup"><span data-stu-id="af13b-314">oven</span></span> |<span data-ttu-id="af13b-315">1235</span><span class="sxs-lookup"><span data-stu-id="af13b-315">1235</span></span> |<span data-ttu-id="af13b-316">0,2</span><span class="sxs-lookup"><span data-stu-id="af13b-316">0.2</span></span> |
| <span data-ttu-id="af13b-317">2222</span><span class="sxs-lookup"><span data-stu-id="af13b-317">2222</span></span> |<span data-ttu-id="af13b-318">0</span><span class="sxs-lookup"><span data-stu-id="af13b-318">0</span></span> |<span data-ttu-id="af13b-319">135</span><span class="sxs-lookup"><span data-stu-id="af13b-319">135</span></span> |<span data-ttu-id="af13b-320">frigorífico</span><span class="sxs-lookup"><span data-stu-id="af13b-320">fridge</span></span> |<span data-ttu-id="af13b-321">12543</span><span class="sxs-lookup"><span data-stu-id="af13b-321">12543</span></span> |<span data-ttu-id="af13b-322">0.0</span><span class="sxs-lookup"><span data-stu-id="af13b-322">0.0</span></span> |

<span data-ttu-id="af13b-323">Tabla “ExampleTable_Ratings”:</span><span class="sxs-lookup"><span data-stu-id="af13b-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="af13b-324">_id</span><span class="sxs-lookup"><span data-stu-id="af13b-324">_id</span></span> | <span data-ttu-id="af13b-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="af13b-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="af13b-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="af13b-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af13b-327">1111</span><span class="sxs-lookup"><span data-stu-id="af13b-327">1111</span></span> |<span data-ttu-id="af13b-328">0</span><span class="sxs-lookup"><span data-stu-id="af13b-328">0</span></span> |<span data-ttu-id="af13b-329">5</span><span class="sxs-lookup"><span data-stu-id="af13b-329">5</span></span> |
| <span data-ttu-id="af13b-330">1111</span><span class="sxs-lookup"><span data-stu-id="af13b-330">1111</span></span> |<span data-ttu-id="af13b-331">1</span><span class="sxs-lookup"><span data-stu-id="af13b-331">1</span></span> |<span data-ttu-id="af13b-332">6</span><span class="sxs-lookup"><span data-stu-id="af13b-332">6</span></span> |
| <span data-ttu-id="af13b-333">2222</span><span class="sxs-lookup"><span data-stu-id="af13b-333">2222</span></span> |<span data-ttu-id="af13b-334">0</span><span class="sxs-lookup"><span data-stu-id="af13b-334">0</span></span> |<span data-ttu-id="af13b-335">1</span><span class="sxs-lookup"><span data-stu-id="af13b-335">1</span></span> |
| <span data-ttu-id="af13b-336">2222</span><span class="sxs-lookup"><span data-stu-id="af13b-336">2222</span></span> |<span data-ttu-id="af13b-337">1</span><span class="sxs-lookup"><span data-stu-id="af13b-337">1</span></span> |<span data-ttu-id="af13b-338">2</span><span class="sxs-lookup"><span data-stu-id="af13b-338">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="af13b-339">Asignación de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="af13b-339">Map source to sink columns</span></span>
<span data-ttu-id="af13b-340">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="af13b-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="af13b-341">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="af13b-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="af13b-342">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="af13b-342">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="af13b-343">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="af13b-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="af13b-344">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="af13b-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="af13b-345">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="af13b-345">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="af13b-346">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="af13b-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="af13b-347">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="af13b-347">Performance and Tuning</span></span>
<span data-ttu-id="af13b-348">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="af13b-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af13b-349">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af13b-349">Next Steps</span></span>
<span data-ttu-id="af13b-350">Consulte el artículo [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener instrucciones paso a paso para crear una canalización de datos que mueva los datos de un almacén de datos local a un almacén de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="af13b-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
