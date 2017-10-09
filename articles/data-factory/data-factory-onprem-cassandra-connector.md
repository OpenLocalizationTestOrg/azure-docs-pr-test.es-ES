---
title: datos de aaaMove de Casandra con el generador de datos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de un Casandra local de base de datos con el generador de datos de Azure."
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
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="2387e-103">Movimiento de datos desde una base de datos de Cassandra local con Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="2387e-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="2387e-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de Casandra local.</span><span class="sxs-lookup"><span data-stu-id="2387e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="2387e-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="2387e-106">Puede copiar datos desde un almacén de datos local Casandra datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="2387e-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="2387e-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="2387e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2387e-108">Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos desde una datos Casandra, pero no para mover los datos de otro almacén de datos de datos almacenes tooa Casandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="2387e-109">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="2387e-109">Supported versions</span></span>
<span data-ttu-id="2387e-110">Conector de Hello Casandra admite Hola después de las versiones de Casandra: 2.X.</span><span class="sxs-lookup"><span data-stu-id="2387e-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2387e-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2387e-111">Prerequisites</span></span>
<span data-ttu-id="2387e-112">Para hello Data Factory de Azure servicio toobe tooconnect pueda tooyour local Casandra base de datos, debe instalar una puerta de enlace de administración de datos en hello mismo esa base de datos de Hola de hosts de máquina o en un tooavoid máquina independiente que compiten por los recursos con hello base de datos.</span><span class="sxs-lookup"><span data-stu-id="2387e-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="2387e-113">Data Management Gateway es un componente que se conecta a servicios de toocloud de orígenes de datos locales de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="2387e-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="2387e-114">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="2387e-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="2387e-115">Vea [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello una canalización de datos toomove datos.</span><span class="sxs-lookup"><span data-stu-id="2387e-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="2387e-116">Debe usar hello tooconnect tooa Casandra la base de datos, incluso si la base de datos de Hola se hospeda en la nube de hello, por ejemplo, en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="2387e-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="2387e-117">Y puede tener puerta de enlace de hello en Hola misma VM esa base de datos de Hola de hosts o en una máquina virtual independiente siempre y cuando la puerta de enlace de Hola se pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="2387e-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="2387e-118">Cuando se instala la puerta de enlace de hello, instala automáticamente una base de datos de Microsoft Casandra ODBC driver utiliza tooconnect tooCassandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="2387e-119">Por lo tanto, no es necesario toomanually instalar ningún controlador en la máquina de puerta de enlace de hello cuando se copian datos de base de datos de hello Casandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="2387e-120">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2387e-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2387e-121">Introducción</span><span class="sxs-lookup"><span data-stu-id="2387e-121">Getting started</span></span>
<span data-ttu-id="2387e-122">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="2387e-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2387e-123">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="2387e-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2387e-124">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="2387e-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="2387e-125">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="2387e-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2387e-126">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="2387e-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2387e-127">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="2387e-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2387e-128">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="2387e-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2387e-129">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2387e-130">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="2387e-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2387e-131">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="2387e-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2387e-132">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2387e-133">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos local Casandra, consulte [ejemplo de JSON: copiar los datos de Blob del Casandra tooAzure](#json-example-copy-data-from-cassandra-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2387e-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2387e-134">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son el almacén de datos de uso toodefine factoría de datos entidades tooa específico Casandra:</span><span class="sxs-lookup"><span data-stu-id="2387e-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2387e-135">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="2387e-135">Linked service properties</span></span>
<span data-ttu-id="2387e-136">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooCassandra vinculado.</span><span class="sxs-lookup"><span data-stu-id="2387e-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="2387e-137">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2387e-137">Property</span></span> | <span data-ttu-id="2387e-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="2387e-138">Description</span></span> | <span data-ttu-id="2387e-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2387e-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2387e-140">type</span><span class="sxs-lookup"><span data-stu-id="2387e-140">type</span></span> |<span data-ttu-id="2387e-141">propiedad de tipo Hello debe establecerse en: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="2387e-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="2387e-142">Sí</span><span class="sxs-lookup"><span data-stu-id="2387e-142">Yes</span></span> |
| <span data-ttu-id="2387e-143">host</span><span class="sxs-lookup"><span data-stu-id="2387e-143">host</span></span> |<span data-ttu-id="2387e-144">Una o varias direcciones IP o nombres de host de los servidores de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="2387e-145">Especifique una lista separada por comas de direcciones IP o servidores de tooall de tooconnect de nombres de host al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="2387e-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="2387e-146">Sí</span><span class="sxs-lookup"><span data-stu-id="2387e-146">Yes</span></span> |
| <span data-ttu-id="2387e-147">puerto</span><span class="sxs-lookup"><span data-stu-id="2387e-147">port</span></span> |<span data-ttu-id="2387e-148">Hola el puerto TCP que Hola server Casandra utiliza toolisten para las conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="2387e-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="2387e-149">No. El valor predeterminado es 9042.</span><span class="sxs-lookup"><span data-stu-id="2387e-149">No, default value: 9042</span></span> |
| <span data-ttu-id="2387e-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2387e-150">authenticationType</span></span> |<span data-ttu-id="2387e-151">Básica o anónima</span><span class="sxs-lookup"><span data-stu-id="2387e-151">Basic, or Anonymous</span></span> |<span data-ttu-id="2387e-152">Sí</span><span class="sxs-lookup"><span data-stu-id="2387e-152">Yes</span></span> |
| <span data-ttu-id="2387e-153">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="2387e-153">username</span></span> |<span data-ttu-id="2387e-154">Especifique el nombre de usuario para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="2387e-155">Sí, si authenticationType se establece tooBasic.</span><span class="sxs-lookup"><span data-stu-id="2387e-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="2387e-156">Contraseña</span><span class="sxs-lookup"><span data-stu-id="2387e-156">password</span></span> |<span data-ttu-id="2387e-157">Especifique la contraseña de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-157">Specify password for hello user account.</span></span> |<span data-ttu-id="2387e-158">Sí, si authenticationType se establece tooBasic.</span><span class="sxs-lookup"><span data-stu-id="2387e-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="2387e-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2387e-159">gatewayName</span></span> |<span data-ttu-id="2387e-160">nombre de Hola de puerta de enlace de Hola que es la base de datos de uso tooconnect toohello local Casandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="2387e-161">Sí</span><span class="sxs-lookup"><span data-stu-id="2387e-161">Yes</span></span> |
| <span data-ttu-id="2387e-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="2387e-162">encryptedCredential</span></span> |<span data-ttu-id="2387e-163">Credencial cifrada por la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="2387e-164">No</span><span class="sxs-lookup"><span data-stu-id="2387e-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2387e-165">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="2387e-165">Dataset properties</span></span>
<span data-ttu-id="2387e-166">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="2387e-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2387e-167">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="2387e-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2387e-168">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="2387e-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2387e-169">sección typeProperties Hello para el conjunto de datos de tipo **CassandraTable** tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="2387e-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="2387e-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2387e-170">Property</span></span> | <span data-ttu-id="2387e-171">Descripción</span><span class="sxs-lookup"><span data-stu-id="2387e-171">Description</span></span> | <span data-ttu-id="2387e-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2387e-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2387e-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="2387e-173">keyspace</span></span> |<span data-ttu-id="2387e-174">Nombre de keyspace de Hola o esquema de base de datos de Casandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="2387e-175">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="2387e-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="2387e-176">tableName</span><span class="sxs-lookup"><span data-stu-id="2387e-176">tableName</span></span> |<span data-ttu-id="2387e-177">Nombre de tabla de hello en la base de datos de Casandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="2387e-178">Sí (si no hay definida ninguna **consulta** para **CassandraSource**).</span><span class="sxs-lookup"><span data-stu-id="2387e-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2387e-179">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="2387e-179">Copy activity properties</span></span>
<span data-ttu-id="2387e-180">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="2387e-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2387e-181">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="2387e-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2387e-182">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="2387e-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2387e-183">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="2387e-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2387e-184">Cuando el origen es del tipo **CassandraSource**, Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="2387e-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2387e-185">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2387e-185">Property</span></span> | <span data-ttu-id="2387e-186">Descripción</span><span class="sxs-lookup"><span data-stu-id="2387e-186">Description</span></span> | <span data-ttu-id="2387e-187">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2387e-187">Allowed values</span></span> | <span data-ttu-id="2387e-188">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2387e-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2387e-189">query</span><span class="sxs-lookup"><span data-stu-id="2387e-189">query</span></span> |<span data-ttu-id="2387e-190">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="2387e-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="2387e-191">Consulta SQL-92 o consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="2387e-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="2387e-192">Vea la [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)(referencia de CQL).</span><span class="sxs-lookup"><span data-stu-id="2387e-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="2387e-193">Al usar una consulta SQL, especifique **keyspace name.table nombre** tabla de hello toorepresent desea tooquery.</span><span class="sxs-lookup"><span data-stu-id="2387e-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="2387e-194">No (si tableName y el espacio de claves del conjunto de datos están definidos).</span><span class="sxs-lookup"><span data-stu-id="2387e-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="2387e-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="2387e-195">consistencyLevel</span></span> |<span data-ttu-id="2387e-196">el nivel de coherencia de Hello especifica cuántas réplicas debe responder tooa solicitud de lectura antes de devolver la aplicación de cliente de toohello de datos.</span><span class="sxs-lookup"><span data-stu-id="2387e-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="2387e-197">Comprobaciones de Casandra Hola número de réplicas especificado para la solicitud de lectura de hello toosatisfy de datos.</span><span class="sxs-lookup"><span data-stu-id="2387e-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="2387e-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="2387e-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="2387e-199">Para más información, consulte [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configuración de la coherencia de datos).</span><span class="sxs-lookup"><span data-stu-id="2387e-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="2387e-200">No.</span><span class="sxs-lookup"><span data-stu-id="2387e-200">No.</span></span> <span data-ttu-id="2387e-201">El valor predeterminado es ONE.</span><span class="sxs-lookup"><span data-stu-id="2387e-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="2387e-202">Ejemplo de JSON: copiar los datos de Casandra tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="2387e-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="2387e-203">Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2387e-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2387e-204">Muestra cómo la base de datos toocopy de un Casandra local datos tooan almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="2387e-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="2387e-205">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2387e-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2387e-206">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="2387e-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="2387e-207">No incluye instrucciones paso a paso para la creación de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="2387e-208">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2387e-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="2387e-209">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="2387e-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="2387e-210">Un servicio vinculado de tipo [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2387e-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="2387e-211">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="2387e-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="2387e-212">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2387e-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="2387e-213">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2387e-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="2387e-214">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que use [CassandraSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2387e-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2387e-215">**Servicio vinculado de Cassandra**</span><span class="sxs-lookup"><span data-stu-id="2387e-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="2387e-216">Este ejemplo utiliza hello **Casandra** servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="2387e-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="2387e-217">Vea [Casandra servicio vinculado](#linked-service-properties) sección de propiedades de hello admitidos por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="2387e-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

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

<span data-ttu-id="2387e-218">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="2387e-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="2387e-219">**Conjunto de datos de entrada de Cassandra**</span><span class="sxs-lookup"><span data-stu-id="2387e-219">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="2387e-220">Establecer **externo** demasiado**true** informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="2387e-221">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="2387e-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2387e-222">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="2387e-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="2387e-223">**Actividad de copia en una canalización con el origen de Cassandra y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="2387e-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="2387e-224">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="2387e-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2387e-225">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**CassandraSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2387e-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="2387e-226">Vea [propiedades de tipo RelationalSource](#copy-activity-properties) para lista de Hola de propiedades admitidas por hello RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="2387e-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Cassandra tooan Azure blob",
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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="2387e-227">Asignación de tipos de Cassandra</span><span class="sxs-lookup"><span data-stu-id="2387e-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="2387e-228">Tipo de Cassandra</span><span class="sxs-lookup"><span data-stu-id="2387e-228">Cassandra Type</span></span> | <span data-ttu-id="2387e-229">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="2387e-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="2387e-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="2387e-230">ASCII</span></span> |<span data-ttu-id="2387e-231">String</span><span class="sxs-lookup"><span data-stu-id="2387e-231">String</span></span> |
| <span data-ttu-id="2387e-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="2387e-232">BIGINT</span></span> |<span data-ttu-id="2387e-233">Int64</span><span class="sxs-lookup"><span data-stu-id="2387e-233">Int64</span></span> |
| <span data-ttu-id="2387e-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="2387e-234">BLOB</span></span> |<span data-ttu-id="2387e-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2387e-235">Byte[]</span></span> |
| <span data-ttu-id="2387e-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="2387e-236">BOOLEAN</span></span> |<span data-ttu-id="2387e-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="2387e-237">Boolean</span></span> |
| <span data-ttu-id="2387e-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="2387e-238">DECIMAL</span></span> |<span data-ttu-id="2387e-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="2387e-239">Decimal</span></span> |
| <span data-ttu-id="2387e-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="2387e-240">DOUBLE</span></span> |<span data-ttu-id="2387e-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="2387e-241">Double</span></span> |
| <span data-ttu-id="2387e-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="2387e-242">FLOAT</span></span> |<span data-ttu-id="2387e-243">Single</span><span class="sxs-lookup"><span data-stu-id="2387e-243">Single</span></span> |
| <span data-ttu-id="2387e-244">INET</span><span class="sxs-lookup"><span data-stu-id="2387e-244">INET</span></span> |<span data-ttu-id="2387e-245">String</span><span class="sxs-lookup"><span data-stu-id="2387e-245">String</span></span> |
| <span data-ttu-id="2387e-246">INT</span><span class="sxs-lookup"><span data-stu-id="2387e-246">INT</span></span> |<span data-ttu-id="2387e-247">Int32</span><span class="sxs-lookup"><span data-stu-id="2387e-247">Int32</span></span> |
| <span data-ttu-id="2387e-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="2387e-248">TEXT</span></span> |<span data-ttu-id="2387e-249">String</span><span class="sxs-lookup"><span data-stu-id="2387e-249">String</span></span> |
| <span data-ttu-id="2387e-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="2387e-250">TIMESTAMP</span></span> |<span data-ttu-id="2387e-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="2387e-251">DateTime</span></span> |
| <span data-ttu-id="2387e-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="2387e-252">TIMEUUID</span></span> |<span data-ttu-id="2387e-253">Guid</span><span class="sxs-lookup"><span data-stu-id="2387e-253">Guid</span></span> |
| <span data-ttu-id="2387e-254">UUID</span><span class="sxs-lookup"><span data-stu-id="2387e-254">UUID</span></span> |<span data-ttu-id="2387e-255">Guid</span><span class="sxs-lookup"><span data-stu-id="2387e-255">Guid</span></span> |
| <span data-ttu-id="2387e-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="2387e-256">VARCHAR</span></span> |<span data-ttu-id="2387e-257">String</span><span class="sxs-lookup"><span data-stu-id="2387e-257">String</span></span> |
| <span data-ttu-id="2387e-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="2387e-258">VARINT</span></span> |<span data-ttu-id="2387e-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="2387e-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="2387e-260">Para la colección de tipos (mapa, conjunto, lista, etc.), consulte demasiado[trabajar con tipos de colección Casandra usando tabla virtual](#work-with-collections-using-virtual-table) sección.</span><span class="sxs-lookup"><span data-stu-id="2387e-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="2387e-261">No se admiten tipos definidos por el usuario.</span><span class="sxs-lookup"><span data-stu-id="2387e-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="2387e-262">longitud de Hola de longitudes de columna binaria y la columna de cadena no puede ser mayor que 4000.</span><span class="sxs-lookup"><span data-stu-id="2387e-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="2387e-263">Uso de colecciones con tablas virtuales</span><span class="sxs-lookup"><span data-stu-id="2387e-263">Work with collections using virtual table</span></span>
<span data-ttu-id="2387e-264">Factoría de datos de Azure usa un integrados tooconnect tooand copia datos del controlador ODBC de la base de datos de Casandra.</span><span class="sxs-lookup"><span data-stu-id="2387e-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="2387e-265">Para los tipos de colección incluida mapa, conjunto y una lista, controlador de hello Normalizar datos hello en tablas virtuales correspondientes.</span><span class="sxs-lookup"><span data-stu-id="2387e-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="2387e-266">En concreto, si una tabla contiene las columnas de la colección, el controlador de hello genera hello las tablas virtuales siguientes:</span><span class="sxs-lookup"><span data-stu-id="2387e-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="2387e-267">A **tabla base**, que contiene Hola los mismos datos como tabla real de hello excepto para las columnas del conjunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="2387e-268">tabla de base de Hello usa Hola mismo nombre como tabla real de Hola que representa.</span><span class="sxs-lookup"><span data-stu-id="2387e-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="2387e-269">A **tabla virtual** para cada columna de la colección, que expande datos Hola anidado.</span><span class="sxs-lookup"><span data-stu-id="2387e-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="2387e-270">tablas virtuales Hola que representan las colecciones se le asignó hello nombre de tabla real de hello, un separador de "*vt*" y el nombre de Hola de columna Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="2387e-271">Tablas virtuales hacen referencia datos toohello en la tabla real Hola, habilitación Hola controlador tooaccess Hola datos sin normalizar.</span><span class="sxs-lookup"><span data-stu-id="2387e-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="2387e-272">Consulte la sección de ejemplo para más información.</span><span class="sxs-lookup"><span data-stu-id="2387e-272">See Example section for details.</span></span> <span data-ttu-id="2387e-273">Puede tener acceso a contenido de Hola de colecciones de Casandra por consultar y combinar tablas virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="2387e-274">Puede usar hello [Asistente para copiar](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vista Hola lista de tablas de base de datos de Casandra incluye tablas virtuales hello y obtener una vista previa de los datos de saludo dentro.</span><span class="sxs-lookup"><span data-stu-id="2387e-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="2387e-275">También puede crear una consulta en el Asistente para copiar Hola y validar el resultado de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="2387e-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="2387e-276">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2387e-276">Example</span></span>
<span data-ttu-id="2387e-277">Por ejemplo, hello siguiente "ExampleTable" es una tabla de base de datos de Casandra que contiene una columna de clave de entero principal denominada "pk_int", una columna de texto con el nombre de valor, una columna de la lista, una columna de asignación y una columna del conjunto (denominado "StringSet").</span><span class="sxs-lookup"><span data-stu-id="2387e-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="2387e-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="2387e-278">pk_int</span></span> | <span data-ttu-id="2387e-279">Valor</span><span class="sxs-lookup"><span data-stu-id="2387e-279">Value</span></span> | <span data-ttu-id="2387e-280">Enumerar</span><span class="sxs-lookup"><span data-stu-id="2387e-280">List</span></span> | <span data-ttu-id="2387e-281">Map</span><span class="sxs-lookup"><span data-stu-id="2387e-281">Map</span></span> | <span data-ttu-id="2387e-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="2387e-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2387e-283">1</span><span class="sxs-lookup"><span data-stu-id="2387e-283">1</span></span> |<span data-ttu-id="2387e-284">"valor de ejemplo 1"</span><span class="sxs-lookup"><span data-stu-id="2387e-284">"sample value 1"</span></span> |<span data-ttu-id="2387e-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="2387e-285">["1", "2", "3"]</span></span> |<span data-ttu-id="2387e-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="2387e-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="2387e-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="2387e-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="2387e-288">3</span><span class="sxs-lookup"><span data-stu-id="2387e-288">3</span></span> |<span data-ttu-id="2387e-289">"valor de ejemplo 3"</span><span class="sxs-lookup"><span data-stu-id="2387e-289">"sample value 3"</span></span> |<span data-ttu-id="2387e-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="2387e-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="2387e-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="2387e-291">{"S1": "t"}</span></span> |<span data-ttu-id="2387e-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="2387e-292">{"A", "E"}</span></span> |

<span data-ttu-id="2387e-293">controlador de Hello generaría varios toorepresent tablas virtuales esta misma tabla.</span><span class="sxs-lookup"><span data-stu-id="2387e-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="2387e-294">Hello las columnas de clave externa en las tablas virtuales Hola hacen referencia a columnas de clave principal de hello en la tabla real de hello e indican qué real tabla fila Hola tabla virtual fila corresponde a.</span><span class="sxs-lookup"><span data-stu-id="2387e-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="2387e-295">la primera tabla virtual de Hello es la tabla de base de hello denominada "ExampleTable" se muestra en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="2387e-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="2387e-296">tabla de base de Hello contiene Hola mismos datos como tabla de base de datos original de hello excepto para las colecciones de hello, que se omite en esta tabla y se expanden en otras tablas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2387e-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="2387e-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="2387e-297">pk_int</span></span> | <span data-ttu-id="2387e-298">Valor</span><span class="sxs-lookup"><span data-stu-id="2387e-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2387e-299">1</span><span class="sxs-lookup"><span data-stu-id="2387e-299">1</span></span> |<span data-ttu-id="2387e-300">"valor de ejemplo 1"</span><span class="sxs-lookup"><span data-stu-id="2387e-300">"sample value 1"</span></span> |
| <span data-ttu-id="2387e-301">3</span><span class="sxs-lookup"><span data-stu-id="2387e-301">3</span></span> |<span data-ttu-id="2387e-302">"valor de ejemplo 3"</span><span class="sxs-lookup"><span data-stu-id="2387e-302">"sample value 3"</span></span> |

<span data-ttu-id="2387e-303">Hello en las tablas siguientes muestran tablas virtuales Hola que renormalize datos Hola de las columnas de lista y mapa, StringSet Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="2387e-304">columnas de Hello con nombres que terminan con "_index" o "_clave" indican la posición de Hola de datos de hello dentro de la lista original de Hola o mapa.</span><span class="sxs-lookup"><span data-stu-id="2387e-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="2387e-305">columnas de Hello con nombres que terminan con "_value" contienen datos de hello expandido de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="2387e-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="2387e-306">Tabla “ExampleTable_vt_List”:</span><span class="sxs-lookup"><span data-stu-id="2387e-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="2387e-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="2387e-307">pk_int</span></span> | <span data-ttu-id="2387e-308">List_index</span><span class="sxs-lookup"><span data-stu-id="2387e-308">List_index</span></span> | <span data-ttu-id="2387e-309">List_value</span><span class="sxs-lookup"><span data-stu-id="2387e-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2387e-310">1</span><span class="sxs-lookup"><span data-stu-id="2387e-310">1</span></span> |<span data-ttu-id="2387e-311">0</span><span class="sxs-lookup"><span data-stu-id="2387e-311">0</span></span> |<span data-ttu-id="2387e-312">1</span><span class="sxs-lookup"><span data-stu-id="2387e-312">1</span></span> |
| <span data-ttu-id="2387e-313">1</span><span class="sxs-lookup"><span data-stu-id="2387e-313">1</span></span> |<span data-ttu-id="2387e-314">1</span><span class="sxs-lookup"><span data-stu-id="2387e-314">1</span></span> |<span data-ttu-id="2387e-315">2</span><span class="sxs-lookup"><span data-stu-id="2387e-315">2</span></span> |
| <span data-ttu-id="2387e-316">1</span><span class="sxs-lookup"><span data-stu-id="2387e-316">1</span></span> |<span data-ttu-id="2387e-317">2</span><span class="sxs-lookup"><span data-stu-id="2387e-317">2</span></span> |<span data-ttu-id="2387e-318">3</span><span class="sxs-lookup"><span data-stu-id="2387e-318">3</span></span> |
| <span data-ttu-id="2387e-319">3</span><span class="sxs-lookup"><span data-stu-id="2387e-319">3</span></span> |<span data-ttu-id="2387e-320">0</span><span class="sxs-lookup"><span data-stu-id="2387e-320">0</span></span> |<span data-ttu-id="2387e-321">100</span><span class="sxs-lookup"><span data-stu-id="2387e-321">100</span></span> |
| <span data-ttu-id="2387e-322">3</span><span class="sxs-lookup"><span data-stu-id="2387e-322">3</span></span> |<span data-ttu-id="2387e-323">1</span><span class="sxs-lookup"><span data-stu-id="2387e-323">1</span></span> |<span data-ttu-id="2387e-324">101</span><span class="sxs-lookup"><span data-stu-id="2387e-324">101</span></span> |
| <span data-ttu-id="2387e-325">3</span><span class="sxs-lookup"><span data-stu-id="2387e-325">3</span></span> |<span data-ttu-id="2387e-326">2</span><span class="sxs-lookup"><span data-stu-id="2387e-326">2</span></span> |<span data-ttu-id="2387e-327">102</span><span class="sxs-lookup"><span data-stu-id="2387e-327">102</span></span> |
| <span data-ttu-id="2387e-328">3</span><span class="sxs-lookup"><span data-stu-id="2387e-328">3</span></span> |<span data-ttu-id="2387e-329">3</span><span class="sxs-lookup"><span data-stu-id="2387e-329">3</span></span> |<span data-ttu-id="2387e-330">103</span><span class="sxs-lookup"><span data-stu-id="2387e-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="2387e-331">Tabla “ExampleTable_vt_Map”:</span><span class="sxs-lookup"><span data-stu-id="2387e-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="2387e-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="2387e-332">pk_int</span></span> | <span data-ttu-id="2387e-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="2387e-333">Map_key</span></span> | <span data-ttu-id="2387e-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="2387e-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2387e-335">1</span><span class="sxs-lookup"><span data-stu-id="2387e-335">1</span></span> |<span data-ttu-id="2387e-336">S1</span><span class="sxs-lookup"><span data-stu-id="2387e-336">S1</span></span> |<span data-ttu-id="2387e-337">Una </span><span class="sxs-lookup"><span data-stu-id="2387e-337">A</span></span> |
| <span data-ttu-id="2387e-338">1</span><span class="sxs-lookup"><span data-stu-id="2387e-338">1</span></span> |<span data-ttu-id="2387e-339">S2</span><span class="sxs-lookup"><span data-stu-id="2387e-339">S2</span></span> |<span data-ttu-id="2387e-340">b</span><span class="sxs-lookup"><span data-stu-id="2387e-340">b</span></span> |
| <span data-ttu-id="2387e-341">3</span><span class="sxs-lookup"><span data-stu-id="2387e-341">3</span></span> |<span data-ttu-id="2387e-342">S1</span><span class="sxs-lookup"><span data-stu-id="2387e-342">S1</span></span> |<span data-ttu-id="2387e-343">t</span><span class="sxs-lookup"><span data-stu-id="2387e-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="2387e-344">Tabla “ExampleTable_vt_StringSet”:</span><span class="sxs-lookup"><span data-stu-id="2387e-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="2387e-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="2387e-345">pk_int</span></span> | <span data-ttu-id="2387e-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="2387e-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="2387e-347">1</span><span class="sxs-lookup"><span data-stu-id="2387e-347">1</span></span> |<span data-ttu-id="2387e-348">Una </span><span class="sxs-lookup"><span data-stu-id="2387e-348">A</span></span> |
| <span data-ttu-id="2387e-349">1</span><span class="sxs-lookup"><span data-stu-id="2387e-349">1</span></span> |<span data-ttu-id="2387e-350">b</span><span class="sxs-lookup"><span data-stu-id="2387e-350">B</span></span> |
| <span data-ttu-id="2387e-351">1</span><span class="sxs-lookup"><span data-stu-id="2387e-351">1</span></span> |<span data-ttu-id="2387e-352">C</span><span class="sxs-lookup"><span data-stu-id="2387e-352">C</span></span> |
| <span data-ttu-id="2387e-353">3</span><span class="sxs-lookup"><span data-stu-id="2387e-353">3</span></span> |<span data-ttu-id="2387e-354">Una </span><span class="sxs-lookup"><span data-stu-id="2387e-354">A</span></span> |
| <span data-ttu-id="2387e-355">3</span><span class="sxs-lookup"><span data-stu-id="2387e-355">3</span></span> |<span data-ttu-id="2387e-356">E</span><span class="sxs-lookup"><span data-stu-id="2387e-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="2387e-357">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="2387e-357">Map source toosink columns</span></span>
<span data-ttu-id="2387e-358">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2387e-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2387e-359">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="2387e-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="2387e-360">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="2387e-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2387e-361">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="2387e-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2387e-362">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="2387e-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2387e-363">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="2387e-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2387e-364">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2387e-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2387e-365">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="2387e-365">Performance and Tuning</span></span>
<span data-ttu-id="2387e-366">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="2387e-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
