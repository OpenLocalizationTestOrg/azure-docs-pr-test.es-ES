---
title: "datos de aaaMove de MongoDB utilizando factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de MongoDB base de datos con el generador de datos de Azure."
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
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="dc3b7-103">Movimiento de datos de MongoDB mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="dc3b7-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="dc3b7-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de MongoDB local.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="dc3b7-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="dc3b7-106">Puede copiar datos desde un almacén de datos local MongoDB datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="dc3b7-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="dc3b7-108">Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos de datos MongoDB, pero no para mover los datos de otro almacén de datos de MongoDB del tooan de almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dc3b7-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dc3b7-109">Prerequisites</span></span>
<span data-ttu-id="dc3b7-110">Para hello Data Factory de Azure servicio toobe tooconnect pueda tooyour local MongoDB base de datos, debe instalar Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="dc3b7-111">Versiones admitidas de MongoDB: 2.4, 2.6, 3.0 y 3.2.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="dc3b7-112">Data Management Gateway en Hola misma máquina esa base de datos de Hola de hosts o en un tooavoid máquina independiente que compiten por los recursos con la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="dc3b7-113">Data Management Gateway es un software que se conecta a servicios de toocloud de orígenes de datos locales de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="dc3b7-114">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="dc3b7-115">Vea [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello una canalización de datos toomove datos.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="dc3b7-116">Cuando se instala la puerta de enlace de hello, instala automáticamente un tooMongoDB de tooconnect del controlador que se usa Microsoft MongoDB ODBC.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc3b7-117">Debe toouse Hola puerta de enlace tooconnect tooMongoDB incluso si está hospedado en máquinas virtuales de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="dc3b7-118">Si está tratando de instancia de tooan tooconnect de MongoDB hospedada en la nube, también puede instalar instancia de puerta de enlace de Hola Hola IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="dc3b7-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="dc3b7-119">Getting started</span></span>
<span data-ttu-id="dc3b7-120">Puede crear una canalización con actividad de copia que mueva los datos desde un almacén de datos MongoDB local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="dc3b7-121">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="dc3b7-122">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="dc3b7-123">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="dc3b7-124">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="dc3b7-125">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="dc3b7-126">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="dc3b7-127">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="dc3b7-128">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="dc3b7-129">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="dc3b7-130">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="dc3b7-131">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de MongoDB local, vea [ejemplo de JSON: copiar los datos de MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="dc3b7-132">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son origen de tooMongoDB específicos de entidades de toodefine usado factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="dc3b7-133">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="dc3b7-133">Linked service properties</span></span>
<span data-ttu-id="dc3b7-134">Hello tabla siguiente proporciona descripción para los elementos JSON específicos demasiado**OnPremisesMongoDB** servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="dc3b7-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="dc3b7-135">Property</span></span> | <span data-ttu-id="dc3b7-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="dc3b7-136">Description</span></span> | <span data-ttu-id="dc3b7-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="dc3b7-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc3b7-138">type</span><span class="sxs-lookup"><span data-stu-id="dc3b7-138">type</span></span> |<span data-ttu-id="dc3b7-139">propiedad de tipo Hello debe establecerse en: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="dc3b7-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="dc3b7-140">Sí</span><span class="sxs-lookup"><span data-stu-id="dc3b7-140">Yes</span></span> |
| <span data-ttu-id="dc3b7-141">Servidor</span><span class="sxs-lookup"><span data-stu-id="dc3b7-141">server</span></span> |<span data-ttu-id="dc3b7-142">IP dirección o nombre de host del servidor de MongoDB Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="dc3b7-143">Sí</span><span class="sxs-lookup"><span data-stu-id="dc3b7-143">Yes</span></span> |
| <span data-ttu-id="dc3b7-144">puerto</span><span class="sxs-lookup"><span data-stu-id="dc3b7-144">port</span></span> |<span data-ttu-id="dc3b7-145">El puerto TCP que Hola MongoDB server usa toolisten para las conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="dc3b7-146">Valor predeterminado opcional: 27017</span><span class="sxs-lookup"><span data-stu-id="dc3b7-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="dc3b7-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="dc3b7-147">authenticationType</span></span> |<span data-ttu-id="dc3b7-148">Básica o anónima.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="dc3b7-149">Sí</span><span class="sxs-lookup"><span data-stu-id="dc3b7-149">Yes</span></span> |
| <span data-ttu-id="dc3b7-150">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="dc3b7-150">username</span></span> |<span data-ttu-id="dc3b7-151">Tooaccess de cuenta de usuario MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="dc3b7-152">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="dc3b7-153">Contraseña</span><span class="sxs-lookup"><span data-stu-id="dc3b7-153">password</span></span> |<span data-ttu-id="dc3b7-154">Contraseña de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-154">Password for hello user.</span></span> |<span data-ttu-id="dc3b7-155">Sí (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="dc3b7-156">authSource</span><span class="sxs-lookup"><span data-stu-id="dc3b7-156">authSource</span></span> |<span data-ttu-id="dc3b7-157">Nombre de base de datos de MongoDB de Hola que quiere toouse toocheck sus credenciales de autenticación.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="dc3b7-158">Opcional (si se usa la autenticación básica).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="dc3b7-159">valor predeterminado: utiliza la cuenta de administrador de Hola y base de datos de hello especificada mediante la propiedad databaseName.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="dc3b7-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="dc3b7-160">databaseName</span></span> |<span data-ttu-id="dc3b7-161">Nombre de base de datos de MongoDB de Hola que desea tooaccess.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="dc3b7-162">Sí</span><span class="sxs-lookup"><span data-stu-id="dc3b7-162">Yes</span></span> |
| <span data-ttu-id="dc3b7-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="dc3b7-163">gatewayName</span></span> |<span data-ttu-id="dc3b7-164">Nombre de puerta de enlace de Hola que tiene acceso a almacén de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="dc3b7-165">Sí</span><span class="sxs-lookup"><span data-stu-id="dc3b7-165">Yes</span></span> |
| <span data-ttu-id="dc3b7-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="dc3b7-166">encryptedCredential</span></span> |<span data-ttu-id="dc3b7-167">Credencial cifrada por la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="dc3b7-168">Opcional</span><span class="sxs-lookup"><span data-stu-id="dc3b7-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="dc3b7-169">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="dc3b7-169">Dataset properties</span></span>
<span data-ttu-id="dc3b7-170">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="dc3b7-171">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="dc3b7-172">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="dc3b7-173">sección typeProperties Hello para el conjunto de datos de tipo **MongoDbCollection** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="dc3b7-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="dc3b7-174">Property</span></span> | <span data-ttu-id="dc3b7-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="dc3b7-175">Description</span></span> | <span data-ttu-id="dc3b7-176">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="dc3b7-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc3b7-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="dc3b7-177">collectionName</span></span> |<span data-ttu-id="dc3b7-178">Nombre de colección de hello en la base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="dc3b7-179">Sí</span><span class="sxs-lookup"><span data-stu-id="dc3b7-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="dc3b7-180">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="dc3b7-180">Copy activity properties</span></span>
<span data-ttu-id="dc3b7-181">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="dc3b7-182">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="dc3b7-183">Propiedades disponibles en hello **typeProperties** sección de actividad de hello en hello varían con cada tipo de actividad en otra parte.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="dc3b7-184">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="dc3b7-185">Cuando el origen de hello es del tipo **MongoDbSource** Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="dc3b7-186">Propiedad</span><span class="sxs-lookup"><span data-stu-id="dc3b7-186">Property</span></span> | <span data-ttu-id="dc3b7-187">Descripción</span><span class="sxs-lookup"><span data-stu-id="dc3b7-187">Description</span></span> | <span data-ttu-id="dc3b7-188">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="dc3b7-188">Allowed values</span></span> | <span data-ttu-id="dc3b7-189">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="dc3b7-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dc3b7-190">query</span><span class="sxs-lookup"><span data-stu-id="dc3b7-190">query</span></span> |<span data-ttu-id="dc3b7-191">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="dc3b7-192">Cadena de consulta SQL-92.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-192">SQL-92 query string.</span></span> <span data-ttu-id="dc3b7-193">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="dc3b7-194">No (si se especifica **collectionName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="dc3b7-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="dc3b7-195">Ejemplo de JSON: copiar los datos de MongoDB tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="dc3b7-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="dc3b7-196">Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="dc3b7-197">Muestra cómo toocopy datos desde un tooan de MongoDB local almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="dc3b7-198">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="dc3b7-199">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="dc3b7-200">Un servicio vinculado de tipo [OnPremisesMongoDB](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="dc3b7-201">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="dc3b7-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="dc3b7-202">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="dc3b7-203">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="dc3b7-204">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [MongoDBSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="dc3b7-205">ejemplo de Hola copia datos de un resultado de consulta en el blob de tooa de base de datos de MongoDB cada hora.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="dc3b7-206">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="dc3b7-207">Como primer paso, el programa de instalación puerta de enlace de hello datos administración según las instrucciones de Hola Hola [Data Management Gateway](data-factory-data-management-gateway.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="dc3b7-208">**Servicio vinculado de MongoDB:**</span><span class="sxs-lookup"><span data-stu-id="dc3b7-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="dc3b7-209">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="dc3b7-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="dc3b7-210">**Conjunto de datos de entrada de MongoDB:** establecer "externo": "true" informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="dc3b7-211">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="dc3b7-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="dc3b7-212">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="dc3b7-213">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="dc3b7-214">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="dc3b7-215">**Actividad de copia en una canalización con el origen MongoDB y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="dc3b7-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="dc3b7-216">canalización de Hello contiene una actividad de copia que es hello toouse configurado por encima de los conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="dc3b7-217">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**MongoDbSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="dc3b7-218">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


## <a name="schema-by-data-factory"></a><span data-ttu-id="dc3b7-219">Esquema de Data Factory</span><span class="sxs-lookup"><span data-stu-id="dc3b7-219">Schema by Data Factory</span></span>
<span data-ttu-id="dc3b7-220">Servicio de factoría de datos de Azure deduce el esquema de una colección de MongoDB mediante el uso de documentos de hello 100 más reciente en la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="dc3b7-221">Si estos 100 documentos no incluyan esquema completo, algunas columnas pueden omitirse durante la operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="dc3b7-222">Asignación de tipos para MongoDB</span><span class="sxs-lookup"><span data-stu-id="dc3b7-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="dc3b7-223">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="dc3b7-224">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="dc3b7-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="dc3b7-225">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="dc3b7-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="dc3b7-226">Al mover hello tooMongoDB de datos siguientes se usan asignaciones de tipos de too.NET de tipos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="dc3b7-227">Tipo de MongoDB</span><span class="sxs-lookup"><span data-stu-id="dc3b7-227">MongoDB type</span></span> | <span data-ttu-id="dc3b7-228">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dc3b7-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="dc3b7-229">Binary</span><span class="sxs-lookup"><span data-stu-id="dc3b7-229">Binary</span></span> |<span data-ttu-id="dc3b7-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="dc3b7-230">Byte[]</span></span> |
| <span data-ttu-id="dc3b7-231">Booleano</span><span class="sxs-lookup"><span data-stu-id="dc3b7-231">Boolean</span></span> |<span data-ttu-id="dc3b7-232">Booleano</span><span class="sxs-lookup"><span data-stu-id="dc3b7-232">Boolean</span></span> |
| <span data-ttu-id="dc3b7-233">Date</span><span class="sxs-lookup"><span data-stu-id="dc3b7-233">Date</span></span> |<span data-ttu-id="dc3b7-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="dc3b7-234">DateTime</span></span> |
| <span data-ttu-id="dc3b7-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="dc3b7-235">NumberDouble</span></span> |<span data-ttu-id="dc3b7-236">Doble</span><span class="sxs-lookup"><span data-stu-id="dc3b7-236">Double</span></span> |
| <span data-ttu-id="dc3b7-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="dc3b7-237">NumberInt</span></span> |<span data-ttu-id="dc3b7-238">Int32</span><span class="sxs-lookup"><span data-stu-id="dc3b7-238">Int32</span></span> |
| <span data-ttu-id="dc3b7-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="dc3b7-239">NumberLong</span></span> |<span data-ttu-id="dc3b7-240">Int64</span><span class="sxs-lookup"><span data-stu-id="dc3b7-240">Int64</span></span> |
| <span data-ttu-id="dc3b7-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="dc3b7-241">ObjectID</span></span> |<span data-ttu-id="dc3b7-242">String</span><span class="sxs-lookup"><span data-stu-id="dc3b7-242">String</span></span> |
| <span data-ttu-id="dc3b7-243">String</span><span class="sxs-lookup"><span data-stu-id="dc3b7-243">String</span></span> |<span data-ttu-id="dc3b7-244">String</span><span class="sxs-lookup"><span data-stu-id="dc3b7-244">String</span></span> |
| <span data-ttu-id="dc3b7-245">UUID</span><span class="sxs-lookup"><span data-stu-id="dc3b7-245">UUID</span></span> |<span data-ttu-id="dc3b7-246">Guid</span><span class="sxs-lookup"><span data-stu-id="dc3b7-246">Guid</span></span> |
| <span data-ttu-id="dc3b7-247">Objeto</span><span class="sxs-lookup"><span data-stu-id="dc3b7-247">Object</span></span> |<span data-ttu-id="dc3b7-248">Renormalizado en columnas acopladas con “_” como separador anidado</span><span class="sxs-lookup"><span data-stu-id="dc3b7-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="dc3b7-249">toolearn sobre la compatibilidad con matrices mediante tablas virtuales, consulte demasiado[admite para los tipos complejos con tablas virtuales](#support-for-complex-types-using-virtual-tables) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="dc3b7-250">Actualmente, no se admite los siguientes tipos de datos de MongoDB de hello: DBPointer, JavaScript, Max y Min clave, expresiones regulares, símbolo, marca de tiempo, sin definir</span><span class="sxs-lookup"><span data-stu-id="dc3b7-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="dc3b7-251">Compatibilidad para tipos complejos que usan tablas virtuales</span><span class="sxs-lookup"><span data-stu-id="dc3b7-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="dc3b7-252">Factoría de datos de Azure usa un integrados ODBC driver tooconnect tooand copiar datos desde la base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="dc3b7-253">Para los tipos complejos, como matrices u objetos con diferentes tipos en documentos de hello, controlador de hello normaliza volver a datos en las tablas virtuales correspondientes.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="dc3b7-254">En concreto, si una tabla contiene estas columnas, controlador de hello genera hello las tablas virtuales siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="dc3b7-255">A **tabla base**, que contiene Hola los mismos datos que la tabla real de hello excepto para las columnas de tipo complejo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="dc3b7-256">tabla de base de Hello usa Hola mismo nombre como tabla real de Hola que representa.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="dc3b7-257">A **tabla virtual** para cada columna de tipo complejo, que expande datos Hola anidado.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="dc3b7-258">tablas virtuales Hola se denominan utilizando nombre Hola de tabla real de hello, un separador "_" y el nombre de Hola de objeto o matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="dc3b7-259">Tablas virtuales hacen referencia datos toohello en la tabla real Hola, habilitación Hola controlador tooaccess Hola datos sin normalizar.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="dc3b7-260">Consulte el ejemplo de la siguiente sección para más información.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-260">See Example section below details.</span></span> <span data-ttu-id="dc3b7-261">Puede tener acceso a contenido de Hola de matrices de MongoDB por consultar y combinar tablas virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="dc3b7-262">Puede usar hello [Asistente para copiar](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vista Hola lista de tablas de base de datos de MongoDB incluye tablas virtuales hello y obtener una vista previa de los datos de saludo dentro.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="dc3b7-263">También puede crear una consulta en el Asistente para copiar Hola y validar el resultado de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="dc3b7-264">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="dc3b7-264">Example</span></span>
<span data-ttu-id="dc3b7-265">Por ejemplo, la tabla “ExampleTable” que aparece a continuación es una tabla de MongoDB que tiene una columna con una matriz de objetos en cada celda: Facturas y una columna con una matriz de tipos escalares: Clasificaciones.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="dc3b7-266">_id</span><span class="sxs-lookup"><span data-stu-id="dc3b7-266">_id</span></span> | <span data-ttu-id="dc3b7-267">Nombre del cliente</span><span class="sxs-lookup"><span data-stu-id="dc3b7-267">Customer Name</span></span> | <span data-ttu-id="dc3b7-268">Facturas</span><span class="sxs-lookup"><span data-stu-id="dc3b7-268">Invoices</span></span> | <span data-ttu-id="dc3b7-269">Nivel de servicios</span><span class="sxs-lookup"><span data-stu-id="dc3b7-269">Service Level</span></span> | <span data-ttu-id="dc3b7-270">Clasificaciones</span><span class="sxs-lookup"><span data-stu-id="dc3b7-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="dc3b7-271">1111</span><span class="sxs-lookup"><span data-stu-id="dc3b7-271">1111</span></span> |<span data-ttu-id="dc3b7-272">ABC</span><span class="sxs-lookup"><span data-stu-id="dc3b7-272">ABC</span></span> |<span data-ttu-id="dc3b7-273">[{invoice_id:”123”, artículo:”tostadora”, precio:”456”, descuento:”0.2”}, {invoice_id:”124”, artículo:”horno”, precio: ”1235”, descuento: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="dc3b7-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="dc3b7-274">Silver</span><span class="sxs-lookup"><span data-stu-id="dc3b7-274">Silver</span></span> |<span data-ttu-id="dc3b7-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="dc3b7-275">[5,6]</span></span> |
| <span data-ttu-id="dc3b7-276">2222</span><span class="sxs-lookup"><span data-stu-id="dc3b7-276">2222</span></span> |<span data-ttu-id="dc3b7-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="dc3b7-277">XYZ</span></span> |<span data-ttu-id="dc3b7-278">[{invoice_id:”135”, artículo:”frigorífico”, precio: ”12543”, descuento: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="dc3b7-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="dc3b7-279">Gold</span><span class="sxs-lookup"><span data-stu-id="dc3b7-279">Gold</span></span> |<span data-ttu-id="dc3b7-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="dc3b7-280">[1,2]</span></span> |

<span data-ttu-id="dc3b7-281">controlador de Hello generaría varios toorepresent tablas virtuales esta misma tabla.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="dc3b7-282">Hola primera virtual tabla es Hola base denominada "ExampleTable", se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="dc3b7-283">tabla de base de Hello contiene todos los datos de Hola de tabla original hello, pero los datos de Hola de matrices de Hola se ha omitido y se expanden en las tablas virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="dc3b7-284">_id</span><span class="sxs-lookup"><span data-stu-id="dc3b7-284">_id</span></span> | <span data-ttu-id="dc3b7-285">Nombre del cliente</span><span class="sxs-lookup"><span data-stu-id="dc3b7-285">Customer Name</span></span> | <span data-ttu-id="dc3b7-286">Nivel de servicios</span><span class="sxs-lookup"><span data-stu-id="dc3b7-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc3b7-287">1111</span><span class="sxs-lookup"><span data-stu-id="dc3b7-287">1111</span></span> |<span data-ttu-id="dc3b7-288">ABC</span><span class="sxs-lookup"><span data-stu-id="dc3b7-288">ABC</span></span> |<span data-ttu-id="dc3b7-289">Silver</span><span class="sxs-lookup"><span data-stu-id="dc3b7-289">Silver</span></span> |
| <span data-ttu-id="dc3b7-290">2222</span><span class="sxs-lookup"><span data-stu-id="dc3b7-290">2222</span></span> |<span data-ttu-id="dc3b7-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="dc3b7-291">XYZ</span></span> |<span data-ttu-id="dc3b7-292">Gold</span><span class="sxs-lookup"><span data-stu-id="dc3b7-292">Gold</span></span> |

<span data-ttu-id="dc3b7-293">Hello en las tablas siguientes muestran Hola tablas virtuales que representan matrices original de hello en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="dc3b7-294">Estas tablas contienen siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-294">These tables contain hello following:</span></span>

* <span data-ttu-id="dc3b7-295">Toohello columna de clave principal correspondiente toohello fila original de la matriz original Hola hacer copia de una referencia (a través de la columna de hello _id)</span><span class="sxs-lookup"><span data-stu-id="dc3b7-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="dc3b7-296">Una indicación de posición de Hola de datos de hello dentro de la matriz original Hola</span><span class="sxs-lookup"><span data-stu-id="dc3b7-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="dc3b7-297">Hola expande datos para cada elemento de matriz de Hola</span><span class="sxs-lookup"><span data-stu-id="dc3b7-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="dc3b7-298">Tabla “ExampleTable_Invoices”:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="dc3b7-299">_id</span><span class="sxs-lookup"><span data-stu-id="dc3b7-299">_id</span></span> | <span data-ttu-id="dc3b7-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="dc3b7-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="dc3b7-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="dc3b7-301">invoice_id</span></span> | <span data-ttu-id="dc3b7-302">item</span><span class="sxs-lookup"><span data-stu-id="dc3b7-302">item</span></span> | <span data-ttu-id="dc3b7-303">price</span><span class="sxs-lookup"><span data-stu-id="dc3b7-303">price</span></span> | <span data-ttu-id="dc3b7-304">Descuento</span><span class="sxs-lookup"><span data-stu-id="dc3b7-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="dc3b7-305">1111</span><span class="sxs-lookup"><span data-stu-id="dc3b7-305">1111</span></span> |<span data-ttu-id="dc3b7-306">0</span><span class="sxs-lookup"><span data-stu-id="dc3b7-306">0</span></span> |<span data-ttu-id="dc3b7-307">123</span><span class="sxs-lookup"><span data-stu-id="dc3b7-307">123</span></span> |<span data-ttu-id="dc3b7-308">tostadora</span><span class="sxs-lookup"><span data-stu-id="dc3b7-308">toaster</span></span> |<span data-ttu-id="dc3b7-309">456</span><span class="sxs-lookup"><span data-stu-id="dc3b7-309">456</span></span> |<span data-ttu-id="dc3b7-310">0,2</span><span class="sxs-lookup"><span data-stu-id="dc3b7-310">0.2</span></span> |
| <span data-ttu-id="dc3b7-311">1111</span><span class="sxs-lookup"><span data-stu-id="dc3b7-311">1111</span></span> |<span data-ttu-id="dc3b7-312">1</span><span class="sxs-lookup"><span data-stu-id="dc3b7-312">1</span></span> |<span data-ttu-id="dc3b7-313">124</span><span class="sxs-lookup"><span data-stu-id="dc3b7-313">124</span></span> |<span data-ttu-id="dc3b7-314">horno</span><span class="sxs-lookup"><span data-stu-id="dc3b7-314">oven</span></span> |<span data-ttu-id="dc3b7-315">1235</span><span class="sxs-lookup"><span data-stu-id="dc3b7-315">1235</span></span> |<span data-ttu-id="dc3b7-316">0,2</span><span class="sxs-lookup"><span data-stu-id="dc3b7-316">0.2</span></span> |
| <span data-ttu-id="dc3b7-317">2222</span><span class="sxs-lookup"><span data-stu-id="dc3b7-317">2222</span></span> |<span data-ttu-id="dc3b7-318">0</span><span class="sxs-lookup"><span data-stu-id="dc3b7-318">0</span></span> |<span data-ttu-id="dc3b7-319">135</span><span class="sxs-lookup"><span data-stu-id="dc3b7-319">135</span></span> |<span data-ttu-id="dc3b7-320">frigorífico</span><span class="sxs-lookup"><span data-stu-id="dc3b7-320">fridge</span></span> |<span data-ttu-id="dc3b7-321">12543</span><span class="sxs-lookup"><span data-stu-id="dc3b7-321">12543</span></span> |<span data-ttu-id="dc3b7-322">0.0</span><span class="sxs-lookup"><span data-stu-id="dc3b7-322">0.0</span></span> |

<span data-ttu-id="dc3b7-323">Tabla “ExampleTable_Ratings”:</span><span class="sxs-lookup"><span data-stu-id="dc3b7-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="dc3b7-324">_id</span><span class="sxs-lookup"><span data-stu-id="dc3b7-324">_id</span></span> | <span data-ttu-id="dc3b7-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="dc3b7-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="dc3b7-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="dc3b7-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc3b7-327">1111</span><span class="sxs-lookup"><span data-stu-id="dc3b7-327">1111</span></span> |<span data-ttu-id="dc3b7-328">0</span><span class="sxs-lookup"><span data-stu-id="dc3b7-328">0</span></span> |<span data-ttu-id="dc3b7-329">5</span><span class="sxs-lookup"><span data-stu-id="dc3b7-329">5</span></span> |
| <span data-ttu-id="dc3b7-330">1111</span><span class="sxs-lookup"><span data-stu-id="dc3b7-330">1111</span></span> |<span data-ttu-id="dc3b7-331">1</span><span class="sxs-lookup"><span data-stu-id="dc3b7-331">1</span></span> |<span data-ttu-id="dc3b7-332">6</span><span class="sxs-lookup"><span data-stu-id="dc3b7-332">6</span></span> |
| <span data-ttu-id="dc3b7-333">2222</span><span class="sxs-lookup"><span data-stu-id="dc3b7-333">2222</span></span> |<span data-ttu-id="dc3b7-334">0</span><span class="sxs-lookup"><span data-stu-id="dc3b7-334">0</span></span> |<span data-ttu-id="dc3b7-335">1</span><span class="sxs-lookup"><span data-stu-id="dc3b7-335">1</span></span> |
| <span data-ttu-id="dc3b7-336">2222</span><span class="sxs-lookup"><span data-stu-id="dc3b7-336">2222</span></span> |<span data-ttu-id="dc3b7-337">1</span><span class="sxs-lookup"><span data-stu-id="dc3b7-337">1</span></span> |<span data-ttu-id="dc3b7-338">2</span><span class="sxs-lookup"><span data-stu-id="dc3b7-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="dc3b7-339">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="dc3b7-339">Map source toosink columns</span></span>
<span data-ttu-id="dc3b7-340">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="dc3b7-341">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="dc3b7-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="dc3b7-342">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="dc3b7-343">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="dc3b7-344">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="dc3b7-345">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="dc3b7-346">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="dc3b7-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="dc3b7-347">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="dc3b7-347">Performance and Tuning</span></span>
<span data-ttu-id="dc3b7-348">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc3b7-349">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc3b7-349">Next Steps</span></span>
<span data-ttu-id="dc3b7-350">Vea [mover datos entre local y nube](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso para crear una canalización de datos que mueve el almacén de datos de Azure tooan del almacén de datos desde un datos locales.</span><span class="sxs-lookup"><span data-stu-id="dc3b7-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
