---
title: datos de aaaMove de SAP Business Warehouse mediante Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de SAP Business Warehouse mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="89881-103">Movimiento de datos de SAP Business Warehouse mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="89881-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="89881-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un almacenamiento de negocios de SAP (BW) local.</span><span class="sxs-lookup"><span data-stu-id="89881-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="89881-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="89881-106">Puede copiar datos desde un almacén de datos local SAP Business Warehouse datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="89881-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="89881-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="89881-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="89881-108">Factoría de datos admite actualmente solo mover datos de un tooother de datos de SAP Business Warehouse almacena, pero no para mover los datos de otros datos de los almacenes tooan SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="89881-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="89881-109">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="89881-109">Supported versions and installation</span></span>
<span data-ttu-id="89881-110">Este conector es compatible con la versión 7.x de SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="89881-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="89881-111">Admite la copia de datos de InfoCubes y QueryCubes (incluidas las consultas BEx) mediante consultas MDX.</span><span class="sxs-lookup"><span data-stu-id="89881-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="89881-112">tooenable Hola conectividad toohello instancia de SAP BW, instale Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="89881-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="89881-113">**Data Management Gateway**: conectar tooon local de datos de servicio de factoría de datos admite almacenes (incluidos SAP Business Warehouse) mediante un componente denominado Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="89881-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="89881-114">toolearn acerca de Data Management Gateway e instrucciones paso a paso para configurar la puerta de enlace de hello, consulte [toocloud almacén de datos del almacén de datos de movimiento entre los datos locales](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="89881-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="89881-115">Puerta de enlace es necesaria incluso aunque Hola SAP Business Warehouse se hospeda en una máquina virtual de IaaS de Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="89881-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="89881-116">Puede instalar la puerta de enlace de hello en hello misma máquina virtual como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola se pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="89881-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="89881-117">**Biblioteca SAP NetWeaver** en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="89881-118">Puede obtener la biblioteca de SAP Netweaver Hola desde el Administrador de SAP o directamente desde hello [centro de descarga de Software de SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="89881-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="89881-119">Busque hello **1025361 de SAP nota #** tooget ubicación de descarga de hello para la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="89881-120">Asegúrese de que la arquitectura de hello para la biblioteca de SAP NetWeaver hello (32 bits o 64 bits) coincida con la instalación de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="89881-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="89881-121">A continuación, instale todos los archivos incluidos en hello SAP NetWeaver RFC SDK correspondiente toohello nota de SAP.</span><span class="sxs-lookup"><span data-stu-id="89881-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="89881-122">biblioteca de SAP NetWeaver Hello también se incluye en hello instalación de las herramientas de cliente de SAP.</span><span class="sxs-lookup"><span data-stu-id="89881-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="89881-123">Incluir las DLL de hello extraídas de hello SDK de RFC de NetWeaver en la carpeta system32.</span><span class="sxs-lookup"><span data-stu-id="89881-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="89881-124">Introducción</span><span class="sxs-lookup"><span data-stu-id="89881-124">Getting started</span></span>
<span data-ttu-id="89881-125">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="89881-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="89881-126">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="89881-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="89881-127">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="89881-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="89881-128">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="89881-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="89881-129">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="89881-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="89881-130">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="89881-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="89881-131">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="89881-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="89881-132">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="89881-133">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="89881-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="89881-134">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="89881-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="89881-135">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="89881-136">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy de datos de un local SAP Business Warehouse, consulte [ejemplo de JSON: copiar los datos de SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="89881-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="89881-137">Hola las secciones siguientes proporciona detalles acerca de propiedades JSON que forman el almacén de datos de SAP BW de toodefine usado factoría de datos entidades tooan específico:</span><span class="sxs-lookup"><span data-stu-id="89881-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="89881-138">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="89881-138">Linked service properties</span></span>
<span data-ttu-id="89881-139">Hello en la tabla siguiente proporciona la descripción de JSON elementos específico tooSAP servicio Business Warehouse (BW) vinculados.</span><span class="sxs-lookup"><span data-stu-id="89881-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="89881-140">Propiedad</span><span class="sxs-lookup"><span data-stu-id="89881-140">Property</span></span> | <span data-ttu-id="89881-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="89881-141">Description</span></span> | <span data-ttu-id="89881-142">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="89881-142">Allowed values</span></span> | <span data-ttu-id="89881-143">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="89881-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="89881-144">Servidor</span><span class="sxs-lookup"><span data-stu-id="89881-144">server</span></span> | <span data-ttu-id="89881-145">Nombre del servidor de hello en qué Hola SAP BW reside la instancia.</span><span class="sxs-lookup"><span data-stu-id="89881-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="89881-146">cadena</span><span class="sxs-lookup"><span data-stu-id="89881-146">string</span></span> | <span data-ttu-id="89881-147">Sí</span><span class="sxs-lookup"><span data-stu-id="89881-147">Yes</span></span>
<span data-ttu-id="89881-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="89881-148">systemNumber</span></span> | <span data-ttu-id="89881-149">Número de sistema de hello sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="89881-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="89881-150">Número decimal de dos dígitos que se representa en forma de cadena.</span><span class="sxs-lookup"><span data-stu-id="89881-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="89881-151">Sí</span><span class="sxs-lookup"><span data-stu-id="89881-151">Yes</span></span>
<span data-ttu-id="89881-152">clientId</span><span class="sxs-lookup"><span data-stu-id="89881-152">clientId</span></span> | <span data-ttu-id="89881-153">Identificador de cliente del cliente de Hola Hola sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="89881-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="89881-154">Número decimal de tres dígitos que se representa en forma de cadena.</span><span class="sxs-lookup"><span data-stu-id="89881-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="89881-155">Sí</span><span class="sxs-lookup"><span data-stu-id="89881-155">Yes</span></span>
<span data-ttu-id="89881-156">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="89881-156">username</span></span> | <span data-ttu-id="89881-157">Nombre de usuario de Hola que tiene el servidor de acceso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="89881-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="89881-158">cadena</span><span class="sxs-lookup"><span data-stu-id="89881-158">string</span></span> | <span data-ttu-id="89881-159">Sí</span><span class="sxs-lookup"><span data-stu-id="89881-159">Yes</span></span>
<span data-ttu-id="89881-160">Contraseña</span><span class="sxs-lookup"><span data-stu-id="89881-160">password</span></span> | <span data-ttu-id="89881-161">Contraseña de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-161">Password for hello user.</span></span> | <span data-ttu-id="89881-162">cadena</span><span class="sxs-lookup"><span data-stu-id="89881-162">string</span></span> | <span data-ttu-id="89881-163">Sí</span><span class="sxs-lookup"><span data-stu-id="89881-163">Yes</span></span>
<span data-ttu-id="89881-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="89881-164">gatewayName</span></span> | <span data-ttu-id="89881-165">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la instancia de SAP BW de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="89881-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="89881-166">cadena</span><span class="sxs-lookup"><span data-stu-id="89881-166">string</span></span> | <span data-ttu-id="89881-167">Sí</span><span class="sxs-lookup"><span data-stu-id="89881-167">Yes</span></span>
<span data-ttu-id="89881-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="89881-168">encryptedCredential</span></span> | <span data-ttu-id="89881-169">Hola cifra la cadena de credenciales.</span><span class="sxs-lookup"><span data-stu-id="89881-169">hello encrypted credential string.</span></span> | <span data-ttu-id="89881-170">cadena</span><span class="sxs-lookup"><span data-stu-id="89881-170">string</span></span> | <span data-ttu-id="89881-171">No</span><span class="sxs-lookup"><span data-stu-id="89881-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="89881-172">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="89881-172">Dataset properties</span></span>
<span data-ttu-id="89881-173">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="89881-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="89881-174">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="89881-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="89881-175">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="89881-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="89881-176">No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP BW de Hola de tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="89881-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="89881-177">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="89881-177">Copy activity properties</span></span>
<span data-ttu-id="89881-178">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="89881-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="89881-179">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="89881-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="89881-180">Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="89881-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="89881-181">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="89881-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="89881-182">Cuando el origen de la actividad de copia es del tipo **RelationalSource** (que incluye SAP BW), Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="89881-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="89881-183">Propiedad</span><span class="sxs-lookup"><span data-stu-id="89881-183">Property</span></span> | <span data-ttu-id="89881-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="89881-184">Description</span></span> | <span data-ttu-id="89881-185">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="89881-185">Allowed values</span></span> | <span data-ttu-id="89881-186">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="89881-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89881-187">query</span><span class="sxs-lookup"><span data-stu-id="89881-187">query</span></span> | <span data-ttu-id="89881-188">Especifica Hola MDX consultar tooread datos de instancia de SAP BW Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="89881-189">Consulta MDX.</span><span class="sxs-lookup"><span data-stu-id="89881-189">MDX query.</span></span> | <span data-ttu-id="89881-190">Sí</span><span class="sxs-lookup"><span data-stu-id="89881-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="89881-191">Ejemplo de JSON: copiar los datos de SAP Business Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="89881-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="89881-192">Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="89881-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="89881-193">Este ejemplo se muestra cómo toocopy datos desde un tooan de SAP Business Warehouse local almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="89881-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="89881-194">Sin embargo, se pueden copiar datos **directamente** tooany de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="89881-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="89881-195">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="89881-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="89881-196">No incluye instrucciones paso a paso para la creación de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="89881-197">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="89881-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="89881-198">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="89881-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="89881-199">Un servicio vinculado del tipo [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89881-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="89881-200">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="89881-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="89881-201">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89881-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="89881-202">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89881-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="89881-203">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="89881-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="89881-204">ejemplo Hello copia datos de un tooan de la instancia de SAP Business Warehouse blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="89881-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="89881-205">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="89881-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="89881-206">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="89881-207">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="89881-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="89881-208">Servicio vinculado de SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="89881-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="89881-209">Esto vincula los vínculos de servicio su factoría de datos de SAP BW instancia toohello.</span><span class="sxs-lookup"><span data-stu-id="89881-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="89881-210">propiedad de tipo Hello se establece demasiado**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="89881-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="89881-211">sección de Hello typeProperties proporciona información de conexión para la instancia de SAP BW Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="89881-212">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="89881-212">Azure Storage linked service</span></span>
<span data-ttu-id="89881-213">Esto vincula los vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello.</span><span class="sxs-lookup"><span data-stu-id="89881-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="89881-214">propiedad de tipo Hello se establece demasiado**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="89881-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="89881-215">sección de Hello typeProperties proporciona información de conexión para hello cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="89881-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="89881-216">Conjunto de datos de entrada de SAP BW</span><span class="sxs-lookup"><span data-stu-id="89881-216">SAP BW input dataset</span></span>
<span data-ttu-id="89881-217">Este conjunto de datos define el conjunto de datos de SAP Business Warehouse Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="89881-218">Se establece el tipo de saludo del conjunto de datos de hello factoría de datos demasiado**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="89881-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="89881-219">Actualmente, no se especifica ninguna propiedad concreta de tipo para un conjunto de datos de SAP BW.</span><span class="sxs-lookup"><span data-stu-id="89881-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="89881-220">consulta de Hola Hola definición de actividad de copia especifica qué tooread de datos de instancia de SAP BW Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="89881-221">Establecer la propiedad external tootrue informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="89881-222">Propiedades de frecuencia y el intervalo define la programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="89881-223">En este caso, los datos de Hola se leen desde la instancia de SAP BW Hola cada hora.</span><span class="sxs-lookup"><span data-stu-id="89881-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="89881-224">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="89881-224">Azure Blob output dataset</span></span>
<span data-ttu-id="89881-225">Este conjunto de datos define el conjunto de datos de hello salida blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="89881-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="89881-226">propiedad de tipo Hello se establece tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="89881-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="89881-227">sección de Hello typeProperties proporciona donde se almacenan los datos de hello copiados de la instancia de SAP BW Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="89881-228">Hola se escriben los datos blob nuevo tooa cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="89881-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="89881-229">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="89881-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="89881-230">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="89881-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="89881-231">Canalización con actividad de copia</span><span class="sxs-lookup"><span data-stu-id="89881-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="89881-232">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="89881-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="89881-233">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** (para el origen de SAP BW) y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="89881-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="89881-234">consulta de Hello especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="89881-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="89881-235">Asignación de tipos para SAP BW</span><span class="sxs-lookup"><span data-stu-id="89881-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="89881-236">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="89881-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="89881-237">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="89881-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="89881-238">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="89881-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="89881-239">Al mover los datos de SAP BW, se usa Hola siguiendo las asignaciones de tipos de too.NET de tipos de SAP BW.</span><span class="sxs-lookup"><span data-stu-id="89881-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="89881-240">Tipo de datos de hello ABAP diccionario</span><span class="sxs-lookup"><span data-stu-id="89881-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="89881-241">Tipo de datos de .Net</span><span class="sxs-lookup"><span data-stu-id="89881-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="89881-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="89881-242">ACCP</span></span> |  <span data-ttu-id="89881-243">int</span><span class="sxs-lookup"><span data-stu-id="89881-243">Int</span></span>
<span data-ttu-id="89881-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="89881-244">CHAR</span></span> | <span data-ttu-id="89881-245">String</span><span class="sxs-lookup"><span data-stu-id="89881-245">String</span></span>
<span data-ttu-id="89881-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="89881-246">CLNT</span></span> | <span data-ttu-id="89881-247">String</span><span class="sxs-lookup"><span data-stu-id="89881-247">String</span></span>
<span data-ttu-id="89881-248">CURR</span><span class="sxs-lookup"><span data-stu-id="89881-248">CURR</span></span> | <span data-ttu-id="89881-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="89881-249">Decimal</span></span>
<span data-ttu-id="89881-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="89881-250">CUKY</span></span> | <span data-ttu-id="89881-251">string</span><span class="sxs-lookup"><span data-stu-id="89881-251">String</span></span>
<span data-ttu-id="89881-252">DEC</span><span class="sxs-lookup"><span data-stu-id="89881-252">DEC</span></span> | <span data-ttu-id="89881-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="89881-253">Decimal</span></span>
<span data-ttu-id="89881-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="89881-254">FLTP</span></span> | <span data-ttu-id="89881-255">Doble</span><span class="sxs-lookup"><span data-stu-id="89881-255">Double</span></span>
<span data-ttu-id="89881-256">INT1</span><span class="sxs-lookup"><span data-stu-id="89881-256">INT1</span></span> | <span data-ttu-id="89881-257">Byte</span><span class="sxs-lookup"><span data-stu-id="89881-257">Byte</span></span>
<span data-ttu-id="89881-258">INT2</span><span class="sxs-lookup"><span data-stu-id="89881-258">INT2</span></span> | <span data-ttu-id="89881-259">Int16</span><span class="sxs-lookup"><span data-stu-id="89881-259">Int16</span></span>
<span data-ttu-id="89881-260">INT4</span><span class="sxs-lookup"><span data-stu-id="89881-260">INT4</span></span> | <span data-ttu-id="89881-261">int</span><span class="sxs-lookup"><span data-stu-id="89881-261">Int</span></span>
<span data-ttu-id="89881-262">LANG</span><span class="sxs-lookup"><span data-stu-id="89881-262">LANG</span></span> | <span data-ttu-id="89881-263">String</span><span class="sxs-lookup"><span data-stu-id="89881-263">String</span></span>
<span data-ttu-id="89881-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="89881-264">LCHR</span></span> | <span data-ttu-id="89881-265">string</span><span class="sxs-lookup"><span data-stu-id="89881-265">String</span></span>
<span data-ttu-id="89881-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="89881-266">LRAW</span></span> | <span data-ttu-id="89881-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89881-267">Byte[]</span></span>
<span data-ttu-id="89881-268">PREC</span><span class="sxs-lookup"><span data-stu-id="89881-268">PREC</span></span> | <span data-ttu-id="89881-269">Int16</span><span class="sxs-lookup"><span data-stu-id="89881-269">Int16</span></span>
<span data-ttu-id="89881-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="89881-270">QUAN</span></span> | <span data-ttu-id="89881-271">Decimal</span><span class="sxs-lookup"><span data-stu-id="89881-271">Decimal</span></span>
<span data-ttu-id="89881-272">RAW</span><span class="sxs-lookup"><span data-stu-id="89881-272">RAW</span></span> | <span data-ttu-id="89881-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89881-273">Byte[]</span></span>
<span data-ttu-id="89881-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="89881-274">RAWSTRING</span></span> | <span data-ttu-id="89881-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89881-275">Byte[]</span></span>
<span data-ttu-id="89881-276">STRING</span><span class="sxs-lookup"><span data-stu-id="89881-276">STRING</span></span> | <span data-ttu-id="89881-277">string</span><span class="sxs-lookup"><span data-stu-id="89881-277">String</span></span>
<span data-ttu-id="89881-278">UNIDAD</span><span class="sxs-lookup"><span data-stu-id="89881-278">UNIT</span></span> | <span data-ttu-id="89881-279">string</span><span class="sxs-lookup"><span data-stu-id="89881-279">String</span></span>
<span data-ttu-id="89881-280">DATS</span><span class="sxs-lookup"><span data-stu-id="89881-280">DATS</span></span> | <span data-ttu-id="89881-281">String</span><span class="sxs-lookup"><span data-stu-id="89881-281">String</span></span>
<span data-ttu-id="89881-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="89881-282">NUMC</span></span> | <span data-ttu-id="89881-283">String</span><span class="sxs-lookup"><span data-stu-id="89881-283">String</span></span>
<span data-ttu-id="89881-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="89881-284">TIMS</span></span> | <span data-ttu-id="89881-285">String</span><span class="sxs-lookup"><span data-stu-id="89881-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="89881-286">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="89881-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="89881-287">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="89881-287">Map source toosink columns</span></span>
<span data-ttu-id="89881-288">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="89881-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="89881-289">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="89881-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="89881-290">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="89881-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="89881-291">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="89881-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="89881-292">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="89881-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="89881-293">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="89881-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="89881-294">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="89881-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="89881-295">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="89881-295">Performance and Tuning</span></span>
<span data-ttu-id="89881-296">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="89881-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
