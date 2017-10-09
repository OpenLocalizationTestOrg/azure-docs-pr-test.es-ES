---
title: datos de aaaMove de SAP HANA con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de SAP HANA con Data Factory de Azure."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="82f81-103">Movimiento de datos de SAP HANA mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="82f81-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="82f81-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un local SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="82f81-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="82f81-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="82f81-106">Puede copiar datos desde un almacén de datos local SAP HANA datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="82f81-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="82f81-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="82f81-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="82f81-108">Factoría de datos admite actualmente solo mover almacenes de datos de un dato de tooother de SAP HANA, pero no para mover los datos de otros datos de los almacenes tooan SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="82f81-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="82f81-109">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="82f81-109">Supported versions and installation</span></span>
<span data-ttu-id="82f81-110">Este conector es compatible con cualquier versión de base de datos de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="82f81-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="82f81-111">Admite la copia de datos de modelos de información de HANA (como las vistas de análisis y cálculo) y las tablas de fila o columna mediante consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="82f81-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="82f81-112">tooenable Hola conectividad toohello instancia SAP HANA, instale Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="82f81-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="82f81-113">**Data Management Gateway**: conectar tooon local de datos de servicio de factoría de datos admite almacenes (incluidos SAP HANA) mediante un componente denominado Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="82f81-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="82f81-114">toolearn acerca de Data Management Gateway e instrucciones paso a paso para configurar la puerta de enlace de hello, consulte [toocloud almacén de datos del almacén de datos de movimiento entre los datos locales](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="82f81-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="82f81-115">Puerta de enlace es necesaria incluso aunque Hola SAP HANA se hospeda en una máquina virtual de IaaS de Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="82f81-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="82f81-116">Puede instalar la puerta de enlace de hello en hello misma máquina virtual como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola se pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="82f81-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="82f81-117">**Controlador ODBC de SAP HANA** en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="82f81-118">Puede descargar el controlador de ODBC de SAP HANA Hola de hello [centro de descarga de Software de SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="82f81-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="82f81-119">Búsqueda con la palabra clave de hello **SAP HANA cliente para Windows**.</span><span class="sxs-lookup"><span data-stu-id="82f81-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="82f81-120">Introducción</span><span class="sxs-lookup"><span data-stu-id="82f81-120">Getting started</span></span>
<span data-ttu-id="82f81-121">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="82f81-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="82f81-122">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="82f81-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="82f81-123">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="82f81-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="82f81-124">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="82f81-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="82f81-125">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="82f81-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="82f81-126">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="82f81-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="82f81-127">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="82f81-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="82f81-128">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="82f81-129">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="82f81-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="82f81-130">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="82f81-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="82f81-131">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="82f81-132">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy de datos de un local SAP HANA, consulte [ejemplo de JSON: copiar los datos de SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="82f81-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="82f81-133">Hola las secciones siguientes proporciona detalles acerca de propiedades JSON que forman el almacén de datos de SAP HANA de toodefine usado factoría de datos entidades tooan específico:</span><span class="sxs-lookup"><span data-stu-id="82f81-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="82f81-134">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="82f81-134">Linked service properties</span></span>
<span data-ttu-id="82f81-135">Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSAP HANA servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="82f81-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="82f81-136">Propiedad</span><span class="sxs-lookup"><span data-stu-id="82f81-136">Property</span></span> | <span data-ttu-id="82f81-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="82f81-137">Description</span></span> | <span data-ttu-id="82f81-138">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="82f81-138">Allowed values</span></span> | <span data-ttu-id="82f81-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="82f81-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="82f81-140">Servidor</span><span class="sxs-lookup"><span data-stu-id="82f81-140">server</span></span> | <span data-ttu-id="82f81-141">Nombre del servidor de hello en qué Hola SAP HANA reside la instancia.</span><span class="sxs-lookup"><span data-stu-id="82f81-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="82f81-142">Si el servidor usa un puerto personalizado, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="82f81-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="82f81-143">string</span><span class="sxs-lookup"><span data-stu-id="82f81-143">string</span></span> | <span data-ttu-id="82f81-144">Sí</span><span class="sxs-lookup"><span data-stu-id="82f81-144">Yes</span></span>
<span data-ttu-id="82f81-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="82f81-145">authenticationType</span></span> | <span data-ttu-id="82f81-146">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="82f81-146">Type of authentication.</span></span> | <span data-ttu-id="82f81-147">cadena.</span><span class="sxs-lookup"><span data-stu-id="82f81-147">string.</span></span> <span data-ttu-id="82f81-148">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="82f81-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="82f81-149">Sí</span><span class="sxs-lookup"><span data-stu-id="82f81-149">Yes</span></span> 
<span data-ttu-id="82f81-150">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="82f81-150">username</span></span> | <span data-ttu-id="82f81-151">Nombre de usuario de Hola que tiene el servidor de acceso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="82f81-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="82f81-152">cadena</span><span class="sxs-lookup"><span data-stu-id="82f81-152">string</span></span> | <span data-ttu-id="82f81-153">Sí</span><span class="sxs-lookup"><span data-stu-id="82f81-153">Yes</span></span>
<span data-ttu-id="82f81-154">Contraseña</span><span class="sxs-lookup"><span data-stu-id="82f81-154">password</span></span> | <span data-ttu-id="82f81-155">Contraseña de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-155">Password for hello user.</span></span> | <span data-ttu-id="82f81-156">cadena</span><span class="sxs-lookup"><span data-stu-id="82f81-156">string</span></span> | <span data-ttu-id="82f81-157">Sí</span><span class="sxs-lookup"><span data-stu-id="82f81-157">Yes</span></span>
<span data-ttu-id="82f81-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="82f81-158">gatewayName</span></span> | <span data-ttu-id="82f81-159">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la instancia de SAP HANA de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="82f81-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="82f81-160">cadena</span><span class="sxs-lookup"><span data-stu-id="82f81-160">string</span></span> | <span data-ttu-id="82f81-161">Sí</span><span class="sxs-lookup"><span data-stu-id="82f81-161">Yes</span></span>
<span data-ttu-id="82f81-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="82f81-162">encryptedCredential</span></span> | <span data-ttu-id="82f81-163">Hola cifra la cadena de credenciales.</span><span class="sxs-lookup"><span data-stu-id="82f81-163">hello encrypted credential string.</span></span> | <span data-ttu-id="82f81-164">cadena</span><span class="sxs-lookup"><span data-stu-id="82f81-164">string</span></span> | <span data-ttu-id="82f81-165">No</span><span class="sxs-lookup"><span data-stu-id="82f81-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="82f81-166">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="82f81-166">Dataset properties</span></span>
<span data-ttu-id="82f81-167">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="82f81-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="82f81-168">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="82f81-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="82f81-169">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="82f81-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="82f81-170">No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP HANA de Hola de tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="82f81-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="82f81-171">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="82f81-171">Copy activity properties</span></span>
<span data-ttu-id="82f81-172">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="82f81-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="82f81-173">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="82f81-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="82f81-174">Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="82f81-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="82f81-175">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="82f81-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="82f81-176">Cuando el origen de la actividad de copia es del tipo **RelationalSource** (que incluye SAP HANA), Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="82f81-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="82f81-177">Propiedad</span><span class="sxs-lookup"><span data-stu-id="82f81-177">Property</span></span> | <span data-ttu-id="82f81-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="82f81-178">Description</span></span> | <span data-ttu-id="82f81-179">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="82f81-179">Allowed values</span></span> | <span data-ttu-id="82f81-180">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="82f81-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82f81-181">query</span><span class="sxs-lookup"><span data-stu-id="82f81-181">query</span></span> | <span data-ttu-id="82f81-182">Especifica Hola SQL permite consultar tooread datos de instancia de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="82f81-183">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="82f81-183">SQL query.</span></span> | <span data-ttu-id="82f81-184">Sí</span><span class="sxs-lookup"><span data-stu-id="82f81-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="82f81-185">Ejemplo de JSON: copiar los datos de SAP HANA tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="82f81-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="82f81-186">en el ejemplo siguiente Hello proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="82f81-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="82f81-187">Este ejemplo se muestra cómo toocopy datos desde un tooan de SAP HANA local almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="82f81-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="82f81-188">Sin embargo, se pueden copiar datos **directamente** tooany de receptores de hello aparecen [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="82f81-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="82f81-189">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="82f81-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="82f81-190">No incluye instrucciones paso a paso para la creación de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="82f81-191">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="82f81-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="82f81-192">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="82f81-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="82f81-193">Un servicio vinculado de tipo [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="82f81-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="82f81-194">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="82f81-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="82f81-195">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="82f81-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="82f81-196">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="82f81-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="82f81-197">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="82f81-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="82f81-198">ejemplo Hello copia datos de un tooan de la instancia de SAP HANA blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="82f81-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="82f81-199">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="82f81-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="82f81-200">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="82f81-201">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="82f81-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="82f81-202">Servicio vinculado de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="82f81-202">SAP HANA linked service</span></span>
<span data-ttu-id="82f81-203">Esto vincula los vínculos de servicio su factoría de datos de SAP HANA instancia toohello.</span><span class="sxs-lookup"><span data-stu-id="82f81-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="82f81-204">propiedad de tipo Hello se establece demasiado**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="82f81-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="82f81-205">sección de Hello typeProperties proporciona información de conexión para la instancia de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="82f81-206">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="82f81-206">Azure Storage linked service</span></span>
<span data-ttu-id="82f81-207">Esto vincula los vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello.</span><span class="sxs-lookup"><span data-stu-id="82f81-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="82f81-208">propiedad de tipo Hello se establece demasiado**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="82f81-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="82f81-209">sección de Hello typeProperties proporciona información de conexión para hello cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="82f81-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="82f81-210">Conjunto de datos de entrada de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="82f81-210">SAP HANA input dataset</span></span>

<span data-ttu-id="82f81-211">Este conjunto de datos define el conjunto de datos de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="82f81-212">Se establece el tipo de saludo del conjunto de datos de hello factoría de datos demasiado**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="82f81-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="82f81-213">Actualmente, no establece ninguna propiedad específica de tipo para un conjunto de datos de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="82f81-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="82f81-214">consulta de Hola Hola definición de actividad de copia especifica qué tooread de datos de instancia de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="82f81-215">Establecer la propiedad external tootrue informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="82f81-216">Propiedades de frecuencia y el intervalo define la programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="82f81-217">En este caso, los datos de Hola se leen desde la instancia de SAP HANA Hola cada hora.</span><span class="sxs-lookup"><span data-stu-id="82f81-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="82f81-218">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="82f81-218">Azure Blob output dataset</span></span>
<span data-ttu-id="82f81-219">Este conjunto de datos define el conjunto de datos de hello salida blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="82f81-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="82f81-220">propiedad de tipo Hello se establece tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="82f81-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="82f81-221">sección de Hello typeProperties proporciona donde se almacenan los datos de hello copiados de la instancia de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="82f81-222">Hola se escriben los datos blob nuevo tooa cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="82f81-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="82f81-223">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="82f81-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="82f81-224">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="82f81-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="82f81-225">Canalización con actividad de copia</span><span class="sxs-lookup"><span data-stu-id="82f81-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="82f81-226">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="82f81-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="82f81-227">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** (para el origen de SAP HANA) y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="82f81-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="82f81-228">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="82f81-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="82f81-229">Asignación de tipos para SAP HANA</span><span class="sxs-lookup"><span data-stu-id="82f81-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="82f81-230">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="82f81-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="82f81-231">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="82f81-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="82f81-232">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="82f81-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="82f81-233">Al mover los datos de SAP HANA, se usa Hola siguiendo las asignaciones de tipos de too.NET de tipos de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="82f81-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="82f81-234">Tipo de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="82f81-234">SAP HANA Type</span></span> | <span data-ttu-id="82f81-235">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="82f81-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="82f81-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="82f81-236">TINYINT</span></span> | <span data-ttu-id="82f81-237">Byte</span><span class="sxs-lookup"><span data-stu-id="82f81-237">Byte</span></span>
<span data-ttu-id="82f81-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="82f81-238">SMALLINT</span></span> | <span data-ttu-id="82f81-239">Int16</span><span class="sxs-lookup"><span data-stu-id="82f81-239">Int16</span></span>
<span data-ttu-id="82f81-240">INT</span><span class="sxs-lookup"><span data-stu-id="82f81-240">INT</span></span> | <span data-ttu-id="82f81-241">Int32</span><span class="sxs-lookup"><span data-stu-id="82f81-241">Int32</span></span>
<span data-ttu-id="82f81-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="82f81-242">BIGINT</span></span> | <span data-ttu-id="82f81-243">Int64</span><span class="sxs-lookup"><span data-stu-id="82f81-243">Int64</span></span>
<span data-ttu-id="82f81-244">REAL</span><span class="sxs-lookup"><span data-stu-id="82f81-244">REAL</span></span> | <span data-ttu-id="82f81-245">Single</span><span class="sxs-lookup"><span data-stu-id="82f81-245">Single</span></span>
<span data-ttu-id="82f81-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="82f81-246">DOUBLE</span></span> | <span data-ttu-id="82f81-247">Single</span><span class="sxs-lookup"><span data-stu-id="82f81-247">Single</span></span>
<span data-ttu-id="82f81-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="82f81-248">DECIMAL</span></span> | <span data-ttu-id="82f81-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="82f81-249">Decimal</span></span>
<span data-ttu-id="82f81-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="82f81-250">BOOLEAN</span></span> | <span data-ttu-id="82f81-251">Byte</span><span class="sxs-lookup"><span data-stu-id="82f81-251">Byte</span></span>
<span data-ttu-id="82f81-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="82f81-252">VARCHAR</span></span> | <span data-ttu-id="82f81-253">String</span><span class="sxs-lookup"><span data-stu-id="82f81-253">String</span></span>
<span data-ttu-id="82f81-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="82f81-254">NVARCHAR</span></span> | <span data-ttu-id="82f81-255">String</span><span class="sxs-lookup"><span data-stu-id="82f81-255">String</span></span>
<span data-ttu-id="82f81-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="82f81-256">CLOB</span></span> | <span data-ttu-id="82f81-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="82f81-257">Byte[]</span></span>
<span data-ttu-id="82f81-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="82f81-258">ALPHANUM</span></span> | <span data-ttu-id="82f81-259">String</span><span class="sxs-lookup"><span data-stu-id="82f81-259">String</span></span>
<span data-ttu-id="82f81-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="82f81-260">BLOB</span></span> | <span data-ttu-id="82f81-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="82f81-261">Byte[]</span></span>
<span data-ttu-id="82f81-262">DATE</span><span class="sxs-lookup"><span data-stu-id="82f81-262">DATE</span></span> | <span data-ttu-id="82f81-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="82f81-263">DateTime</span></span>
<span data-ttu-id="82f81-264">TIME</span><span class="sxs-lookup"><span data-stu-id="82f81-264">TIME</span></span> | <span data-ttu-id="82f81-265">timespan</span><span class="sxs-lookup"><span data-stu-id="82f81-265">TimeSpan</span></span>
<span data-ttu-id="82f81-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="82f81-266">TIMESTAMP</span></span> | <span data-ttu-id="82f81-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="82f81-267">DateTime</span></span>
<span data-ttu-id="82f81-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="82f81-268">SECONDDATE</span></span> | <span data-ttu-id="82f81-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="82f81-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="82f81-270">Limitaciones conocidas</span><span class="sxs-lookup"><span data-stu-id="82f81-270">Known limitations</span></span>
<span data-ttu-id="82f81-271">Cuando se copian datos de SAP HANA, hay algunas limitaciones conocidas:</span><span class="sxs-lookup"><span data-stu-id="82f81-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="82f81-272">Las cadenas NVARCHAR son longitud truncada toomaximum de 4.000 caracteres Unicode</span><span class="sxs-lookup"><span data-stu-id="82f81-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="82f81-273">SMALLDECIMAL no se admite</span><span class="sxs-lookup"><span data-stu-id="82f81-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="82f81-274">VARBINARY no se admite</span><span class="sxs-lookup"><span data-stu-id="82f81-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="82f81-275">Las fechas válidas son las del intervalo entre 30/12/1899 y 31/12/9999</span><span class="sxs-lookup"><span data-stu-id="82f81-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="82f81-276">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="82f81-276">Map source toosink columns</span></span>
<span data-ttu-id="82f81-277">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="82f81-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="82f81-278">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="82f81-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="82f81-279">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="82f81-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="82f81-280">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="82f81-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="82f81-281">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="82f81-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="82f81-282">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="82f81-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="82f81-283">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="82f81-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="82f81-284">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="82f81-284">Performance and Tuning</span></span>
<span data-ttu-id="82f81-285">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="82f81-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
