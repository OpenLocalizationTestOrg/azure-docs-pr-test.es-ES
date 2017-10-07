---
title: aaaMove datos de Teradata con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información sobre el conector de Teradata para hello servicio de factoría de datos que le permite mover los datos de la base de datos de Teradata"
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
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="18fa6-103">Movimiento de datos de Teradata mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="18fa6-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="18fa6-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de Teradata local.</span><span class="sxs-lookup"><span data-stu-id="18fa6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="18fa6-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="18fa6-106">Puede copiar datos desde un almacén de datos local Teradata datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="18fa6-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="18fa6-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="18fa6-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="18fa6-108">Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos de datos de Teradata, pero no para mover los datos de otro almacén de datos de datos almacenes tooa Teradata.</span><span class="sxs-lookup"><span data-stu-id="18fa6-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="18fa6-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18fa6-109">Prerequisites</span></span>
<span data-ttu-id="18fa6-110">Factoría de datos admite conectando orígenes de Teradata tooon local a través de hello Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="18fa6-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="18fa6-111">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="18fa6-112">Puerta de enlace es necesaria incluso aunque hello Teradata hospedado en una VM de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="18fa6-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="18fa6-113">Puede instalar la puerta de enlace de hello en Hola mismo IaaS VM como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="18fa6-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="18fa6-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="18fa6-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="18fa6-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="18fa6-115">Supported versions and installation</span></span>
<span data-ttu-id="18fa6-116">Para Data Management Gateway tooconnect toohello base de datos de Teradata, debe hello tooinstall [proveedor de datos .NET para Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versión 14 o por encima de Hola mismo sistema como Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="18fa6-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="18fa6-117">Se admite la versión 12 de Teradata o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="18fa6-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="18fa6-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="18fa6-118">Getting started</span></span>
<span data-ttu-id="18fa6-119">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="18fa6-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="18fa6-120">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="18fa6-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="18fa6-121">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="18fa6-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="18fa6-122">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="18fa6-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="18fa6-123">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="18fa6-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="18fa6-124">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="18fa6-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="18fa6-125">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="18fa6-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="18fa6-126">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="18fa6-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="18fa6-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="18fa6-128">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="18fa6-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="18fa6-129">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="18fa6-130">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de Teradata local, vea [ejemplo de JSON: copiar los datos de Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="18fa6-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="18fa6-131">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son el almacén de datos de uso toodefine factoría de datos entidades tooa específico Teradata:</span><span class="sxs-lookup"><span data-stu-id="18fa6-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="18fa6-132">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="18fa6-132">Linked service properties</span></span>
<span data-ttu-id="18fa6-133">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooTeradata vinculado.</span><span class="sxs-lookup"><span data-stu-id="18fa6-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="18fa6-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="18fa6-134">Property</span></span> | <span data-ttu-id="18fa6-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="18fa6-135">Description</span></span> | <span data-ttu-id="18fa6-136">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="18fa6-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="18fa6-137">type</span><span class="sxs-lookup"><span data-stu-id="18fa6-137">type</span></span> |<span data-ttu-id="18fa6-138">propiedad de tipo Hello debe establecerse en: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="18fa6-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="18fa6-139">Sí</span><span class="sxs-lookup"><span data-stu-id="18fa6-139">Yes</span></span> |
| <span data-ttu-id="18fa6-140">Servidor</span><span class="sxs-lookup"><span data-stu-id="18fa6-140">server</span></span> |<span data-ttu-id="18fa6-141">Nombre del servidor de Teradata Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="18fa6-142">Sí</span><span class="sxs-lookup"><span data-stu-id="18fa6-142">Yes</span></span> |
| <span data-ttu-id="18fa6-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="18fa6-143">authenticationType</span></span> |<span data-ttu-id="18fa6-144">Tipo de autenticación que utiliza la base de datos de Teradata tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="18fa6-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="18fa6-145">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="18fa6-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="18fa6-146">Sí</span><span class="sxs-lookup"><span data-stu-id="18fa6-146">Yes</span></span> |
| <span data-ttu-id="18fa6-147">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="18fa6-147">username</span></span> |<span data-ttu-id="18fa6-148">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="18fa6-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="18fa6-149">No</span><span class="sxs-lookup"><span data-stu-id="18fa6-149">No</span></span> |
| <span data-ttu-id="18fa6-150">Contraseña</span><span class="sxs-lookup"><span data-stu-id="18fa6-150">password</span></span> |<span data-ttu-id="18fa6-151">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="18fa6-152">No</span><span class="sxs-lookup"><span data-stu-id="18fa6-152">No</span></span> |
| <span data-ttu-id="18fa6-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="18fa6-153">gatewayName</span></span> |<span data-ttu-id="18fa6-154">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de Teradata local de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="18fa6-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="18fa6-155">Sí</span><span class="sxs-lookup"><span data-stu-id="18fa6-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="18fa6-156">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="18fa6-156">Dataset properties</span></span>
<span data-ttu-id="18fa6-157">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="18fa6-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="18fa6-158">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="18fa6-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="18fa6-159">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="18fa6-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="18fa6-160">Actualmente, no hay ninguna propiedad de tipo compatible con el conjunto de datos de hello Teradata.</span><span class="sxs-lookup"><span data-stu-id="18fa6-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="18fa6-161">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="18fa6-161">Copy activity properties</span></span>
<span data-ttu-id="18fa6-162">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="18fa6-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="18fa6-163">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="18fa6-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="18fa6-164">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="18fa6-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="18fa6-165">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="18fa6-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="18fa6-166">Cuando el origen de hello es del tipo **RelationalSource** (que incluye Teradata), Hola propiedades siguientes está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="18fa6-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="18fa6-167">Propiedad</span><span class="sxs-lookup"><span data-stu-id="18fa6-167">Property</span></span> | <span data-ttu-id="18fa6-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="18fa6-168">Description</span></span> | <span data-ttu-id="18fa6-169">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="18fa6-169">Allowed values</span></span> | <span data-ttu-id="18fa6-170">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="18fa6-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="18fa6-171">query</span><span class="sxs-lookup"><span data-stu-id="18fa6-171">query</span></span> |<span data-ttu-id="18fa6-172">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="18fa6-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="18fa6-173">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="18fa6-173">SQL query string.</span></span> <span data-ttu-id="18fa6-174">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="18fa6-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="18fa6-175">Sí</span><span class="sxs-lookup"><span data-stu-id="18fa6-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="18fa6-176">Ejemplo de JSON: copiar los datos de Teradata tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="18fa6-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="18fa6-177">Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="18fa6-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="18fa6-178">Muestran cómo toocopy datos de Teradata tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="18fa6-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="18fa6-179">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="18fa6-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="18fa6-180">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="18fa6-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="18fa6-181">Un servicio vinculado de tipo [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="18fa6-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="18fa6-182">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="18fa6-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="18fa6-183">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="18fa6-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="18fa6-184">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="18fa6-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="18fa6-185">Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="18fa6-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="18fa6-186">ejemplo de Hola copia datos de un resultado de consulta en el blob de tooa de base de datos de Teradata cada hora.</span><span class="sxs-lookup"><span data-stu-id="18fa6-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="18fa6-187">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="18fa6-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="18fa6-188">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="18fa6-189">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="18fa6-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="18fa6-190">**Servicio vinculado de Teradata:**</span><span class="sxs-lookup"><span data-stu-id="18fa6-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="18fa6-191">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="18fa6-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="18fa6-192">**Conjunto de datos de entrada de Teradata:**</span><span class="sxs-lookup"><span data-stu-id="18fa6-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="18fa6-193">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en Teradata y contiene una columna denominada "timestamp" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="18fa6-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="18fa6-194">Establecer "externo": true informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="18fa6-195">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="18fa6-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="18fa6-196">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="18fa6-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="18fa6-197">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="18fa6-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="18fa6-198">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="18fa6-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="18fa6-199">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="18fa6-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="18fa6-200">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="18fa6-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="18fa6-201">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="18fa6-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="18fa6-202">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="18fa6-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="18fa6-203">Asignación de tipos para Teradata</span><span class="sxs-lookup"><span data-stu-id="18fa6-203">Type mapping for Teradata</span></span>
<span data-ttu-id="18fa6-204">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, Hola actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="18fa6-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="18fa6-205">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="18fa6-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="18fa6-206">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="18fa6-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="18fa6-207">Al mover datos tooTeradata, hello asignaciones siguientes sirven de too.NET de tipo Teradata.</span><span class="sxs-lookup"><span data-stu-id="18fa6-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="18fa6-208">Tipo de base de datos Teradata</span><span class="sxs-lookup"><span data-stu-id="18fa6-208">Teradata Database type</span></span> | <span data-ttu-id="18fa6-209">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="18fa6-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="18fa6-210">Char</span><span class="sxs-lookup"><span data-stu-id="18fa6-210">Char</span></span> |<span data-ttu-id="18fa6-211">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-211">String</span></span> |
| <span data-ttu-id="18fa6-212">Clob</span><span class="sxs-lookup"><span data-stu-id="18fa6-212">Clob</span></span> |<span data-ttu-id="18fa6-213">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-213">String</span></span> |
| <span data-ttu-id="18fa6-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="18fa6-214">Graphic</span></span> |<span data-ttu-id="18fa6-215">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-215">String</span></span> |
| <span data-ttu-id="18fa6-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="18fa6-216">VarChar</span></span> |<span data-ttu-id="18fa6-217">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-217">String</span></span> |
| <span data-ttu-id="18fa6-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="18fa6-218">VarGraphic</span></span> |<span data-ttu-id="18fa6-219">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-219">String</span></span> |
| <span data-ttu-id="18fa6-220">Blob</span><span class="sxs-lookup"><span data-stu-id="18fa6-220">Blob</span></span> |<span data-ttu-id="18fa6-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="18fa6-221">Byte[]</span></span> |
| <span data-ttu-id="18fa6-222">Byte</span><span class="sxs-lookup"><span data-stu-id="18fa6-222">Byte</span></span> |<span data-ttu-id="18fa6-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="18fa6-223">Byte[]</span></span> |
| <span data-ttu-id="18fa6-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="18fa6-224">VarByte</span></span> |<span data-ttu-id="18fa6-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="18fa6-225">Byte[]</span></span> |
| <span data-ttu-id="18fa6-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="18fa6-226">BigInt</span></span> |<span data-ttu-id="18fa6-227">Int64</span><span class="sxs-lookup"><span data-stu-id="18fa6-227">Int64</span></span> |
| <span data-ttu-id="18fa6-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="18fa6-228">ByteInt</span></span> |<span data-ttu-id="18fa6-229">Int16</span><span class="sxs-lookup"><span data-stu-id="18fa6-229">Int16</span></span> |
| <span data-ttu-id="18fa6-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="18fa6-230">Decimal</span></span> |<span data-ttu-id="18fa6-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="18fa6-231">Decimal</span></span> |
| <span data-ttu-id="18fa6-232">Doble</span><span class="sxs-lookup"><span data-stu-id="18fa6-232">Double</span></span> |<span data-ttu-id="18fa6-233">Doble</span><span class="sxs-lookup"><span data-stu-id="18fa6-233">Double</span></span> |
| <span data-ttu-id="18fa6-234">Entero</span><span class="sxs-lookup"><span data-stu-id="18fa6-234">Integer</span></span> |<span data-ttu-id="18fa6-235">Int32</span><span class="sxs-lookup"><span data-stu-id="18fa6-235">Int32</span></span> |
| <span data-ttu-id="18fa6-236">Number</span><span class="sxs-lookup"><span data-stu-id="18fa6-236">Number</span></span> |<span data-ttu-id="18fa6-237">Doble</span><span class="sxs-lookup"><span data-stu-id="18fa6-237">Double</span></span> |
| <span data-ttu-id="18fa6-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="18fa6-238">SmallInt</span></span> |<span data-ttu-id="18fa6-239">Int16</span><span class="sxs-lookup"><span data-stu-id="18fa6-239">Int16</span></span> |
| <span data-ttu-id="18fa6-240">Date</span><span class="sxs-lookup"><span data-stu-id="18fa6-240">Date</span></span> |<span data-ttu-id="18fa6-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="18fa6-241">DateTime</span></span> |
| <span data-ttu-id="18fa6-242">Hora</span><span class="sxs-lookup"><span data-stu-id="18fa6-242">Time</span></span> |<span data-ttu-id="18fa6-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-243">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="18fa6-244">Time With Time Zone</span></span> |<span data-ttu-id="18fa6-245">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-245">String</span></span> |
| <span data-ttu-id="18fa6-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="18fa6-246">Timestamp</span></span> |<span data-ttu-id="18fa6-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="18fa6-247">DateTime</span></span> |
| <span data-ttu-id="18fa6-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="18fa6-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="18fa6-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="18fa6-249">DateTimeOffset</span></span> |
| <span data-ttu-id="18fa6-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="18fa6-250">Interval Day</span></span> |<span data-ttu-id="18fa6-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-251">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-252">Intervalo día tooHour</span><span class="sxs-lookup"><span data-stu-id="18fa6-252">Interval Day tooHour</span></span> |<span data-ttu-id="18fa6-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-253">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-254">Intervalo día tooMinute</span><span class="sxs-lookup"><span data-stu-id="18fa6-254">Interval Day tooMinute</span></span> |<span data-ttu-id="18fa6-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-255">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-256">Intervalo día tooSecond</span><span class="sxs-lookup"><span data-stu-id="18fa6-256">Interval Day tooSecond</span></span> |<span data-ttu-id="18fa6-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-257">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="18fa6-258">Interval Hour</span></span> |<span data-ttu-id="18fa6-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-259">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-260">Intervalo hora tooMinute</span><span class="sxs-lookup"><span data-stu-id="18fa6-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="18fa6-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-261">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-262">Intervalo hora tooSecond</span><span class="sxs-lookup"><span data-stu-id="18fa6-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="18fa6-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-263">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="18fa6-264">Interval Minute</span></span> |<span data-ttu-id="18fa6-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-265">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-266">TooSecond minutos del intervalo</span><span class="sxs-lookup"><span data-stu-id="18fa6-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="18fa6-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-267">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="18fa6-268">Interval Second</span></span> |<span data-ttu-id="18fa6-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18fa6-269">TimeSpan</span></span> |
| <span data-ttu-id="18fa6-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="18fa6-270">Interval Year</span></span> |<span data-ttu-id="18fa6-271">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-271">String</span></span> |
| <span data-ttu-id="18fa6-272">Intervalo año tooMonth</span><span class="sxs-lookup"><span data-stu-id="18fa6-272">Interval Year tooMonth</span></span> |<span data-ttu-id="18fa6-273">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-273">String</span></span> |
| <span data-ttu-id="18fa6-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="18fa6-274">Interval Month</span></span> |<span data-ttu-id="18fa6-275">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-275">String</span></span> |
| <span data-ttu-id="18fa6-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="18fa6-276">Period(Date)</span></span> |<span data-ttu-id="18fa6-277">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-277">String</span></span> |
| <span data-ttu-id="18fa6-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="18fa6-278">Period(Time)</span></span> |<span data-ttu-id="18fa6-279">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-279">String</span></span> |
| <span data-ttu-id="18fa6-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="18fa6-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="18fa6-281">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-281">String</span></span> |
| <span data-ttu-id="18fa6-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="18fa6-282">Period(Timestamp)</span></span> |<span data-ttu-id="18fa6-283">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-283">String</span></span> |
| <span data-ttu-id="18fa6-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="18fa6-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="18fa6-285">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-285">String</span></span> |
| <span data-ttu-id="18fa6-286">Xml</span><span class="sxs-lookup"><span data-stu-id="18fa6-286">Xml</span></span> |<span data-ttu-id="18fa6-287">String</span><span class="sxs-lookup"><span data-stu-id="18fa6-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="18fa6-288">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="18fa6-288">Map source toosink columns</span></span>
<span data-ttu-id="18fa6-289">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="18fa6-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="18fa6-290">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="18fa6-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="18fa6-291">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="18fa6-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="18fa6-292">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="18fa6-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="18fa6-293">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="18fa6-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="18fa6-294">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="18fa6-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="18fa6-295">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="18fa6-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="18fa6-296">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="18fa6-296">Performance and Tuning</span></span>
<span data-ttu-id="18fa6-297">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="18fa6-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
