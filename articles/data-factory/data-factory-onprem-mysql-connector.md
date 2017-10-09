---
title: aaaMove datos de MySQL con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de MySQL base de datos con el generador de datos de Azure."
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
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="96279-103">Movimiento de datos de MySQL mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="96279-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="96279-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de MySQL local.</span><span class="sxs-lookup"><span data-stu-id="96279-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="96279-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="96279-106">Puede copiar datos desde un almacén de datos local MySQL datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="96279-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="96279-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="96279-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="96279-108">Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos de datos MySQL, pero no para mover los datos de otro almacén de datos de MySQL tooan de datos almacenes.</span><span class="sxs-lookup"><span data-stu-id="96279-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="96279-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96279-109">Prerequisites</span></span>
<span data-ttu-id="96279-110">Servicio de factoría de datos admite conexión orígenes de MySQL de tooon locales mediante Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="96279-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="96279-111">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="96279-112">Puerta de enlace es necesario incluso si la base de datos de MySQL Hola se hospeda en una máquina virtual de IaaS de Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="96279-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="96279-113">Puede instalar la puerta de enlace de hello en hello misma máquina virtual como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola se pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="96279-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="96279-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="96279-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="96279-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="96279-115">Supported versions and installation</span></span>
<span data-ttu-id="96279-116">Para Data Management Gateway tooconnect toohello base de datos MySQL, necesita hello tooinstall [conector MySQL/Net para Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versión 6.6.5 o superior) en Hola mismo sistema como Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="96279-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="96279-117">Se admite la versión 5.1 de MySQL o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="96279-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="96279-118">Si se produce error "Error de autenticación porque ha cerrado la parte remota Hola hello secuencia de transporte.", considere hello tooupgrade versión toohigher de conector MySQL/Net.</span><span class="sxs-lookup"><span data-stu-id="96279-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="96279-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="96279-119">Getting started</span></span>
<span data-ttu-id="96279-120">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="96279-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="96279-121">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="96279-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="96279-122">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="96279-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="96279-123">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="96279-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="96279-124">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="96279-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="96279-125">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="96279-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="96279-126">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="96279-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="96279-127">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="96279-128">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="96279-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="96279-129">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="96279-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="96279-130">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="96279-131">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de MySQL local, vea [ejemplo de JSON: copiar los datos de MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="96279-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="96279-132">Hola las secciones siguientes proporciona detalles acerca de propiedades JSON que forman el almacén de datos de MySQL de toodefine usado factoría de datos entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="96279-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="96279-133">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="96279-133">Linked service properties</span></span>
<span data-ttu-id="96279-134">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooMySQL vinculado.</span><span class="sxs-lookup"><span data-stu-id="96279-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="96279-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="96279-135">Property</span></span> | <span data-ttu-id="96279-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="96279-136">Description</span></span> | <span data-ttu-id="96279-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="96279-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96279-138">type</span><span class="sxs-lookup"><span data-stu-id="96279-138">type</span></span> |<span data-ttu-id="96279-139">propiedad de tipo Hello debe establecerse en: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="96279-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="96279-140">Sí</span><span class="sxs-lookup"><span data-stu-id="96279-140">Yes</span></span> |
| <span data-ttu-id="96279-141">Servidor</span><span class="sxs-lookup"><span data-stu-id="96279-141">server</span></span> |<span data-ttu-id="96279-142">Nombre del servidor de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="96279-143">Sí</span><span class="sxs-lookup"><span data-stu-id="96279-143">Yes</span></span> |
| <span data-ttu-id="96279-144">database</span><span class="sxs-lookup"><span data-stu-id="96279-144">database</span></span> |<span data-ttu-id="96279-145">Nombre de base de datos de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="96279-146">Sí</span><span class="sxs-lookup"><span data-stu-id="96279-146">Yes</span></span> |
| <span data-ttu-id="96279-147">schema</span><span class="sxs-lookup"><span data-stu-id="96279-147">schema</span></span> |<span data-ttu-id="96279-148">Nombre del esquema de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="96279-149">No</span><span class="sxs-lookup"><span data-stu-id="96279-149">No</span></span> |
| <span data-ttu-id="96279-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="96279-150">authenticationType</span></span> |<span data-ttu-id="96279-151">Tipo de autenticación que utiliza la base de datos de MySQL tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="96279-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="96279-152">Los valores posibles son: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="96279-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="96279-153">Sí</span><span class="sxs-lookup"><span data-stu-id="96279-153">Yes</span></span> |
| <span data-ttu-id="96279-154">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="96279-154">username</span></span> |<span data-ttu-id="96279-155">Especifique la base de datos MySQL toohello de tooconnect de nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="96279-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="96279-156">Sí</span><span class="sxs-lookup"><span data-stu-id="96279-156">Yes</span></span> |
| <span data-ttu-id="96279-157">Contraseña</span><span class="sxs-lookup"><span data-stu-id="96279-157">password</span></span> |<span data-ttu-id="96279-158">Especifique la contraseña de cuenta de usuario de hello especificada.</span><span class="sxs-lookup"><span data-stu-id="96279-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="96279-159">Sí</span><span class="sxs-lookup"><span data-stu-id="96279-159">Yes</span></span> |
| <span data-ttu-id="96279-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="96279-160">gatewayName</span></span> |<span data-ttu-id="96279-161">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de MySQL de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="96279-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="96279-162">Sí</span><span class="sxs-lookup"><span data-stu-id="96279-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="96279-163">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="96279-163">Dataset properties</span></span>
<span data-ttu-id="96279-164">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="96279-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="96279-165">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="96279-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="96279-166">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="96279-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="96279-167">sección typeProperties Hello para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de MySQL) tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="96279-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="96279-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="96279-168">Property</span></span> | <span data-ttu-id="96279-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="96279-169">Description</span></span> | <span data-ttu-id="96279-170">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="96279-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96279-171">tableName</span><span class="sxs-lookup"><span data-stu-id="96279-171">tableName</span></span> |<span data-ttu-id="96279-172">Nombre de tabla de Hola Hola instancia de base de datos MySQL que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="96279-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="96279-173">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="96279-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="96279-174">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="96279-174">Copy activity properties</span></span>
<span data-ttu-id="96279-175">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="96279-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="96279-176">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="96279-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="96279-177">Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="96279-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="96279-178">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="96279-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="96279-179">Cuando el origen de la actividad de copia es del tipo **RelationalSource** (que incluye MySQL), Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="96279-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="96279-180">Propiedad</span><span class="sxs-lookup"><span data-stu-id="96279-180">Property</span></span> | <span data-ttu-id="96279-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="96279-181">Description</span></span> | <span data-ttu-id="96279-182">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="96279-182">Allowed values</span></span> | <span data-ttu-id="96279-183">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="96279-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="96279-184">query</span><span class="sxs-lookup"><span data-stu-id="96279-184">query</span></span> |<span data-ttu-id="96279-185">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="96279-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="96279-186">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="96279-186">SQL query string.</span></span> <span data-ttu-id="96279-187">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="96279-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="96279-188">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="96279-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="96279-189">Ejemplo de JSON: copiar los datos de MySQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="96279-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="96279-190">Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="96279-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="96279-191">Muestra cómo la base de datos toocopy desde un MySQL local datos tooan almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="96279-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="96279-192">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="96279-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96279-193">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="96279-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="96279-194">No incluye instrucciones paso a paso para la creación de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="96279-195">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="96279-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="96279-196">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="96279-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="96279-197">Un servicio vinculado de tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="96279-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="96279-198">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="96279-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="96279-199">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96279-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="96279-200">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96279-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="96279-201">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="96279-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="96279-202">ejemplo Hello copia datos de un resultado de consulta en el blob de tooa de base de datos de MySQL cada hora.</span><span class="sxs-lookup"><span data-stu-id="96279-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="96279-203">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="96279-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="96279-204">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="96279-205">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="96279-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="96279-206">**Servicio vinculado de MySQL:**</span><span class="sxs-lookup"><span data-stu-id="96279-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="96279-207">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="96279-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="96279-208">**Conjunto de datos de entrada de MySQL:**</span><span class="sxs-lookup"><span data-stu-id="96279-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="96279-209">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en MySQL y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="96279-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="96279-210">Establecer "externo": "true" informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="96279-211">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="96279-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="96279-212">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="96279-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="96279-213">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="96279-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="96279-214">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="96279-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="96279-215">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="96279-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="96279-216">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="96279-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="96279-217">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="96279-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="96279-218">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="96279-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="96279-219">Asignación de tipos para MySQL</span><span class="sxs-lookup"><span data-stu-id="96279-219">Type mapping for MySQL</span></span>
<span data-ttu-id="96279-220">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="96279-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="96279-221">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="96279-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="96279-222">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="96279-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="96279-223">Al mover datos tooMySQL, hello siguientes usan las asignaciones son de tipos de too.NET de tipos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="96279-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="96279-224">Tipo de Base de datos MySQL</span><span class="sxs-lookup"><span data-stu-id="96279-224">MySQL Database type</span></span> | <span data-ttu-id="96279-225">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="96279-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="96279-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="96279-226">bigint unsigned</span></span> |<span data-ttu-id="96279-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="96279-227">Decimal</span></span> |
| <span data-ttu-id="96279-228">bigint</span><span class="sxs-lookup"><span data-stu-id="96279-228">bigint</span></span> |<span data-ttu-id="96279-229">Int64</span><span class="sxs-lookup"><span data-stu-id="96279-229">Int64</span></span> |
| <span data-ttu-id="96279-230">bit</span><span class="sxs-lookup"><span data-stu-id="96279-230">bit</span></span> |<span data-ttu-id="96279-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="96279-231">Decimal</span></span> |
| <span data-ttu-id="96279-232">blob</span><span class="sxs-lookup"><span data-stu-id="96279-232">blob</span></span> |<span data-ttu-id="96279-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="96279-233">Byte[]</span></span> |
| <span data-ttu-id="96279-234">booleano</span><span class="sxs-lookup"><span data-stu-id="96279-234">bool</span></span> |<span data-ttu-id="96279-235">Booleano</span><span class="sxs-lookup"><span data-stu-id="96279-235">Boolean</span></span> |
| <span data-ttu-id="96279-236">char</span><span class="sxs-lookup"><span data-stu-id="96279-236">char</span></span> |<span data-ttu-id="96279-237">String</span><span class="sxs-lookup"><span data-stu-id="96279-237">String</span></span> |
| <span data-ttu-id="96279-238">fecha</span><span class="sxs-lookup"><span data-stu-id="96279-238">date</span></span> |<span data-ttu-id="96279-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="96279-239">Datetime</span></span> |
| <span data-ttu-id="96279-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="96279-240">datetime</span></span> |<span data-ttu-id="96279-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="96279-241">Datetime</span></span> |
| <span data-ttu-id="96279-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="96279-242">decimal</span></span> |<span data-ttu-id="96279-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="96279-243">Decimal</span></span> |
| <span data-ttu-id="96279-244">double precision</span><span class="sxs-lookup"><span data-stu-id="96279-244">double precision</span></span> |<span data-ttu-id="96279-245">Doble</span><span class="sxs-lookup"><span data-stu-id="96279-245">Double</span></span> |
| <span data-ttu-id="96279-246">Doble</span><span class="sxs-lookup"><span data-stu-id="96279-246">double</span></span> |<span data-ttu-id="96279-247">Doble</span><span class="sxs-lookup"><span data-stu-id="96279-247">Double</span></span> |
| <span data-ttu-id="96279-248">enum</span><span class="sxs-lookup"><span data-stu-id="96279-248">enum</span></span> |<span data-ttu-id="96279-249">String</span><span class="sxs-lookup"><span data-stu-id="96279-249">String</span></span> |
| <span data-ttu-id="96279-250">float</span><span class="sxs-lookup"><span data-stu-id="96279-250">float</span></span> |<span data-ttu-id="96279-251">Single</span><span class="sxs-lookup"><span data-stu-id="96279-251">Single</span></span> |
| <span data-ttu-id="96279-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="96279-252">int unsigned</span></span> |<span data-ttu-id="96279-253">Int64</span><span class="sxs-lookup"><span data-stu-id="96279-253">Int64</span></span> |
| <span data-ttu-id="96279-254">int</span><span class="sxs-lookup"><span data-stu-id="96279-254">int</span></span> |<span data-ttu-id="96279-255">Int32</span><span class="sxs-lookup"><span data-stu-id="96279-255">Int32</span></span> |
| <span data-ttu-id="96279-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="96279-256">integer unsigned</span></span> |<span data-ttu-id="96279-257">Int64</span><span class="sxs-lookup"><span data-stu-id="96279-257">Int64</span></span> |
| <span data-ttu-id="96279-258">integer</span><span class="sxs-lookup"><span data-stu-id="96279-258">integer</span></span> |<span data-ttu-id="96279-259">Int32</span><span class="sxs-lookup"><span data-stu-id="96279-259">Int32</span></span> |
| <span data-ttu-id="96279-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="96279-260">long varbinary</span></span> |<span data-ttu-id="96279-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="96279-261">Byte[]</span></span> |
| <span data-ttu-id="96279-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="96279-262">long varchar</span></span> |<span data-ttu-id="96279-263">String</span><span class="sxs-lookup"><span data-stu-id="96279-263">String</span></span> |
| <span data-ttu-id="96279-264">longblob</span><span class="sxs-lookup"><span data-stu-id="96279-264">longblob</span></span> |<span data-ttu-id="96279-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="96279-265">Byte[]</span></span> |
| <span data-ttu-id="96279-266">longtext</span><span class="sxs-lookup"><span data-stu-id="96279-266">longtext</span></span> |<span data-ttu-id="96279-267">String</span><span class="sxs-lookup"><span data-stu-id="96279-267">String</span></span> |
| <span data-ttu-id="96279-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="96279-268">mediumblob</span></span> |<span data-ttu-id="96279-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="96279-269">Byte[]</span></span> |
| <span data-ttu-id="96279-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="96279-270">mediumint unsigned</span></span> |<span data-ttu-id="96279-271">Int64</span><span class="sxs-lookup"><span data-stu-id="96279-271">Int64</span></span> |
| <span data-ttu-id="96279-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="96279-272">mediumint</span></span> |<span data-ttu-id="96279-273">Int32</span><span class="sxs-lookup"><span data-stu-id="96279-273">Int32</span></span> |
| <span data-ttu-id="96279-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="96279-274">mediumtext</span></span> |<span data-ttu-id="96279-275">String</span><span class="sxs-lookup"><span data-stu-id="96279-275">String</span></span> |
| <span data-ttu-id="96279-276">numeric</span><span class="sxs-lookup"><span data-stu-id="96279-276">numeric</span></span> |<span data-ttu-id="96279-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="96279-277">Decimal</span></span> |
| <span data-ttu-id="96279-278">real</span><span class="sxs-lookup"><span data-stu-id="96279-278">real</span></span> |<span data-ttu-id="96279-279">Doble</span><span class="sxs-lookup"><span data-stu-id="96279-279">Double</span></span> |
| <span data-ttu-id="96279-280">set</span><span class="sxs-lookup"><span data-stu-id="96279-280">set</span></span> |<span data-ttu-id="96279-281">String</span><span class="sxs-lookup"><span data-stu-id="96279-281">String</span></span> |
| <span data-ttu-id="96279-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="96279-282">smallint unsigned</span></span> |<span data-ttu-id="96279-283">Int32</span><span class="sxs-lookup"><span data-stu-id="96279-283">Int32</span></span> |
| <span data-ttu-id="96279-284">smallint</span><span class="sxs-lookup"><span data-stu-id="96279-284">smallint</span></span> |<span data-ttu-id="96279-285">Int16</span><span class="sxs-lookup"><span data-stu-id="96279-285">Int16</span></span> |
| <span data-ttu-id="96279-286">text</span><span class="sxs-lookup"><span data-stu-id="96279-286">text</span></span> |<span data-ttu-id="96279-287">String</span><span class="sxs-lookup"><span data-stu-id="96279-287">String</span></span> |
| <span data-ttu-id="96279-288">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="96279-288">time</span></span> |<span data-ttu-id="96279-289">timespan</span><span class="sxs-lookup"><span data-stu-id="96279-289">TimeSpan</span></span> |
| <span data-ttu-id="96279-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="96279-290">timestamp</span></span> |<span data-ttu-id="96279-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="96279-291">Datetime</span></span> |
| <span data-ttu-id="96279-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="96279-292">tinyblob</span></span> |<span data-ttu-id="96279-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="96279-293">Byte[]</span></span> |
| <span data-ttu-id="96279-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="96279-294">tinyint unsigned</span></span> |<span data-ttu-id="96279-295">Int16</span><span class="sxs-lookup"><span data-stu-id="96279-295">Int16</span></span> |
| <span data-ttu-id="96279-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="96279-296">tinyint</span></span> |<span data-ttu-id="96279-297">Int16</span><span class="sxs-lookup"><span data-stu-id="96279-297">Int16</span></span> |
| <span data-ttu-id="96279-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="96279-298">tinytext</span></span> |<span data-ttu-id="96279-299">String</span><span class="sxs-lookup"><span data-stu-id="96279-299">String</span></span> |
| <span data-ttu-id="96279-300">varchar</span><span class="sxs-lookup"><span data-stu-id="96279-300">varchar</span></span> |<span data-ttu-id="96279-301">String</span><span class="sxs-lookup"><span data-stu-id="96279-301">String</span></span> |
| <span data-ttu-id="96279-302">year</span><span class="sxs-lookup"><span data-stu-id="96279-302">year</span></span> |<span data-ttu-id="96279-303">int</span><span class="sxs-lookup"><span data-stu-id="96279-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="96279-304">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="96279-304">Map source toosink columns</span></span>
<span data-ttu-id="96279-305">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="96279-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="96279-306">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="96279-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="96279-307">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="96279-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="96279-308">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="96279-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="96279-309">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="96279-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="96279-310">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="96279-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="96279-311">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="96279-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="96279-312">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="96279-312">Performance and Tuning</span></span>
<span data-ttu-id="96279-313">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="96279-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
