---
title: Movimiento de datos de SAP HANA mediante Azure Data Factory | Microsoft Docs
description: Aprenda a mover datos de SAP HANA mediante Azure Data Factory.
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
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="94f9e-103">Movimiento de datos de SAP HANA mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="94f9e-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="94f9e-104">En este artículo, se explica el uso de la actividad de copia en Azure Data Factory para mover datos desde un almacén de datos de SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="94f9e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="94f9e-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="94f9e-106">Puede copiar datos de un almacén de datos de SAP HANA local a cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="94f9e-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="94f9e-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como receptores.</span><span class="sxs-lookup"><span data-stu-id="94f9e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="94f9e-108">Por el momento, Data Factory solo admite el movimiento de datos de un almacén de datos de SAP HANA a otros almacenes de datos, pero no viceversa.</span><span class="sxs-lookup"><span data-stu-id="94f9e-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="94f9e-109">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="94f9e-109">Supported versions and installation</span></span>
<span data-ttu-id="94f9e-110">Este conector es compatible con cualquier versión de base de datos de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="94f9e-111">Admite la copia de datos de modelos de información de HANA (como las vistas de análisis y cálculo) y las tablas de fila o columna mediante consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="94f9e-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="94f9e-112">Para habilitar la conectividad a la instancia de SAP HANA, instale los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="94f9e-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="94f9e-113">**Data Management Gateway**: el servicio Data Factory admite la conexión a almacenes de datos locales (incluido SAP HANA) mediante un componente denominado Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="94f9e-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="94f9e-114">Para obtener información acerca de Data Management Gateway e instrucciones paso a paso sobre cómo configurar la puerta de enlace, consulte el artículo [Movimiento de datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="94f9e-115">La puerta de enlace es necesaria incluso si SAP HANA se hospeda en una máquina virtual (VM) de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="94f9e-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="94f9e-116">Puede instalar la puerta de enlace en la misma máquina virtual como almacén de datos o en una máquina virtual diferente, siempre y cuando la puerta de enlace se pueda conectar a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="94f9e-117">**Controlador ODBC de SAP HANA** en la máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="94f9e-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="94f9e-118">Puede descargar el controlador ODBC de SAP HANA desde el [centro de descarga de software de SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="94f9e-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="94f9e-119">Busque con la palabra clave **SAP HANA CLIENT for Windows** (Cliente SAP HANA para Windows).</span><span class="sxs-lookup"><span data-stu-id="94f9e-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="94f9e-120">Introducción</span><span class="sxs-lookup"><span data-stu-id="94f9e-120">Getting started</span></span>
<span data-ttu-id="94f9e-121">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="94f9e-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="94f9e-122">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="94f9e-123">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="94f9e-124">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="94f9e-125">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="94f9e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="94f9e-126">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="94f9e-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="94f9e-127">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="94f9e-128">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="94f9e-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="94f9e-129">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="94f9e-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="94f9e-130">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="94f9e-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="94f9e-131">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="94f9e-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="94f9e-132">Para ver un ejemplo con definiciones de JSON para entidades de Data Factory que se emplean para copiar datos de un almacén de datos de SAP HANA local, consulte la sección [Ejemplo con definiciones de JSON: copia de datos de SAP HANA a un blob de Azure](#json-example-copy-data-from-sap-hana-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="94f9e-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="94f9e-133">En las secciones siguientes, se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos de SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="94f9e-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="94f9e-134">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="94f9e-134">Linked service properties</span></span>
<span data-ttu-id="94f9e-135">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="94f9e-136">Propiedad</span><span class="sxs-lookup"><span data-stu-id="94f9e-136">Property</span></span> | <span data-ttu-id="94f9e-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="94f9e-137">Description</span></span> | <span data-ttu-id="94f9e-138">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="94f9e-138">Allowed values</span></span> | <span data-ttu-id="94f9e-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="94f9e-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="94f9e-140">server</span><span class="sxs-lookup"><span data-stu-id="94f9e-140">server</span></span> | <span data-ttu-id="94f9e-141">Nombre del servidor en el que reside la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="94f9e-142">Si el servidor usa un puerto personalizado, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="94f9e-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="94f9e-143">string</span><span class="sxs-lookup"><span data-stu-id="94f9e-143">string</span></span> | <span data-ttu-id="94f9e-144">Sí</span><span class="sxs-lookup"><span data-stu-id="94f9e-144">Yes</span></span>
<span data-ttu-id="94f9e-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="94f9e-145">authenticationType</span></span> | <span data-ttu-id="94f9e-146">Tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="94f9e-146">Type of authentication.</span></span> | <span data-ttu-id="94f9e-147">cadena.</span><span class="sxs-lookup"><span data-stu-id="94f9e-147">string.</span></span> <span data-ttu-id="94f9e-148">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="94f9e-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="94f9e-149">Sí</span><span class="sxs-lookup"><span data-stu-id="94f9e-149">Yes</span></span> 
<span data-ttu-id="94f9e-150">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="94f9e-150">username</span></span> | <span data-ttu-id="94f9e-151">Nombre del usuario que tiene acceso al servidor SAP</span><span class="sxs-lookup"><span data-stu-id="94f9e-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="94f9e-152">cadena</span><span class="sxs-lookup"><span data-stu-id="94f9e-152">string</span></span> | <span data-ttu-id="94f9e-153">Sí</span><span class="sxs-lookup"><span data-stu-id="94f9e-153">Yes</span></span>
<span data-ttu-id="94f9e-154">contraseña</span><span class="sxs-lookup"><span data-stu-id="94f9e-154">password</span></span> | <span data-ttu-id="94f9e-155">Contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="94f9e-155">Password for the user.</span></span> | <span data-ttu-id="94f9e-156">string</span><span class="sxs-lookup"><span data-stu-id="94f9e-156">string</span></span> | <span data-ttu-id="94f9e-157">Sí</span><span class="sxs-lookup"><span data-stu-id="94f9e-157">Yes</span></span>
<span data-ttu-id="94f9e-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="94f9e-158">gatewayName</span></span> | <span data-ttu-id="94f9e-159">Nombre de la puerta de enlace que debe usar el servicio Data Factory para conectarse a la instancia de SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="94f9e-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="94f9e-160">string</span><span class="sxs-lookup"><span data-stu-id="94f9e-160">string</span></span> | <span data-ttu-id="94f9e-161">Sí</span><span class="sxs-lookup"><span data-stu-id="94f9e-161">Yes</span></span>
<span data-ttu-id="94f9e-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="94f9e-162">encryptedCredential</span></span> | <span data-ttu-id="94f9e-163">La cadena de credenciales cifrada.</span><span class="sxs-lookup"><span data-stu-id="94f9e-163">The encrypted credential string.</span></span> | <span data-ttu-id="94f9e-164">string</span><span class="sxs-lookup"><span data-stu-id="94f9e-164">string</span></span> | <span data-ttu-id="94f9e-165">No</span><span class="sxs-lookup"><span data-stu-id="94f9e-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="94f9e-166">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="94f9e-166">Dataset properties</span></span>
<span data-ttu-id="94f9e-167">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="94f9e-168">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="94f9e-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="94f9e-169">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="94f9e-170">No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP HANA de tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="94f9e-171">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="94f9e-171">Copy activity properties</span></span>
<span data-ttu-id="94f9e-172">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="94f9e-173">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="94f9e-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="94f9e-174">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="94f9e-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="94f9e-175">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="94f9e-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="94f9e-176">Si el origen es de tipo **RelationalSource** (que incluye SAP HANA), están disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="94f9e-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="94f9e-177">Propiedad</span><span class="sxs-lookup"><span data-stu-id="94f9e-177">Property</span></span> | <span data-ttu-id="94f9e-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="94f9e-178">Description</span></span> | <span data-ttu-id="94f9e-179">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="94f9e-179">Allowed values</span></span> | <span data-ttu-id="94f9e-180">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="94f9e-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="94f9e-181">query</span><span class="sxs-lookup"><span data-stu-id="94f9e-181">query</span></span> | <span data-ttu-id="94f9e-182">Especifica la consulta SQL para leer datos de la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="94f9e-183">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="94f9e-183">SQL query.</span></span> | <span data-ttu-id="94f9e-184">Sí</span><span class="sxs-lookup"><span data-stu-id="94f9e-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="94f9e-185">Ejemplo con definiciones de JSON: copia de datos de SAP HANA a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="94f9e-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="94f9e-186">En el siguiente ejemplo se proporcionan definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="94f9e-187">En este ejemplo, se muestra cómo copiar datos de una instancia de SAP HANA local a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="94f9e-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="94f9e-188">Sin embargo, se pueden copiar datos **directamente** a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94f9e-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="94f9e-189">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="94f9e-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="94f9e-190">No incluye instrucciones paso a paso para crear la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="94f9e-191">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="94f9e-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="94f9e-192">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="94f9e-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="94f9e-193">Un servicio vinculado de tipo [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="94f9e-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="94f9e-194">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="94f9e-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="94f9e-195">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="94f9e-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="94f9e-196">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="94f9e-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="94f9e-197">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="94f9e-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="94f9e-198">En el ejemplo se copian los datos de una instancia de SAP HANA a un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="94f9e-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="94f9e-199">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="94f9e-200">En primer lugar, configure Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="94f9e-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="94f9e-201">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="94f9e-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="94f9e-202">Servicio vinculado de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94f9e-202">SAP HANA linked service</span></span>
<span data-ttu-id="94f9e-203">Este servicio vinculado vincula su instancia de SAP HANA a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="94f9e-204">La propiedad type se establece en **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="94f9e-205">La sección typeProperties proporciona información de conexión para la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="94f9e-206">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="94f9e-206">Azure Storage linked service</span></span>
<span data-ttu-id="94f9e-207">Este servicio vinculado vincula una cuenta de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="94f9e-208">La propiedad type se establece en **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="94f9e-209">La sección typeProperties proporciona información de conexión para la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="94f9e-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="94f9e-210">Conjunto de datos de entrada de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94f9e-210">SAP HANA input dataset</span></span>

<span data-ttu-id="94f9e-211">Este conjunto de datos define el conjunto de datos de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="94f9e-212">Establezca el tipo del conjunto de datos de Data Factory en **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="94f9e-213">Actualmente, no establece ninguna propiedad específica de tipo para un conjunto de datos de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="94f9e-214">La consulta en la definición de actividad de copia especifica qué datos leer de la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="94f9e-215">Si se establece la propiedad "external" en "true", se informa al servicio Data Factory de que la tabla es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="94f9e-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="94f9e-216">Las propiedades de frecuencia e intervalo definen la programación.</span><span class="sxs-lookup"><span data-stu-id="94f9e-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="94f9e-217">En este caso, los datos se leen de la instancia de SAP HANA cada hora.</span><span class="sxs-lookup"><span data-stu-id="94f9e-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="94f9e-218">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="94f9e-218">Azure Blob output dataset</span></span>
<span data-ttu-id="94f9e-219">Este conjunto de datos define el conjunto de datos de salida del blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="94f9e-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="94f9e-220">La propiedad type se establece en AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="94f9e-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="94f9e-221">La sección typeProperties proporciona el lugar donde se almacenan los datos copiados desde la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94f9e-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="94f9e-222">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="94f9e-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="94f9e-223">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="94f9e-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="94f9e-224">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="94f9e-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="94f9e-225">Canalización con actividad de copia</span><span class="sxs-lookup"><span data-stu-id="94f9e-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="94f9e-226">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="94f9e-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="94f9e-227">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** (para el origen de SAP HANA) y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="94f9e-228">La consulta SQL especificada para la propiedad **query** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="94f9e-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="94f9e-229">Asignación de tipos para SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94f9e-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="94f9e-230">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="94f9e-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="94f9e-231">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="94f9e-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="94f9e-232">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="94f9e-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="94f9e-233">Al mover datos desde SAP HANA, se usarán las asignaciones siguientes desde tipos de SAP HANA a tipos de .NET.</span><span class="sxs-lookup"><span data-stu-id="94f9e-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="94f9e-234">Tipo de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94f9e-234">SAP HANA Type</span></span> | <span data-ttu-id="94f9e-235">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="94f9e-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="94f9e-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="94f9e-236">TINYINT</span></span> | <span data-ttu-id="94f9e-237">Byte</span><span class="sxs-lookup"><span data-stu-id="94f9e-237">Byte</span></span>
<span data-ttu-id="94f9e-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="94f9e-238">SMALLINT</span></span> | <span data-ttu-id="94f9e-239">Int16</span><span class="sxs-lookup"><span data-stu-id="94f9e-239">Int16</span></span>
<span data-ttu-id="94f9e-240">INT</span><span class="sxs-lookup"><span data-stu-id="94f9e-240">INT</span></span> | <span data-ttu-id="94f9e-241">Int32</span><span class="sxs-lookup"><span data-stu-id="94f9e-241">Int32</span></span>
<span data-ttu-id="94f9e-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="94f9e-242">BIGINT</span></span> | <span data-ttu-id="94f9e-243">Int64</span><span class="sxs-lookup"><span data-stu-id="94f9e-243">Int64</span></span>
<span data-ttu-id="94f9e-244">REAL</span><span class="sxs-lookup"><span data-stu-id="94f9e-244">REAL</span></span> | <span data-ttu-id="94f9e-245">Single</span><span class="sxs-lookup"><span data-stu-id="94f9e-245">Single</span></span>
<span data-ttu-id="94f9e-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="94f9e-246">DOUBLE</span></span> | <span data-ttu-id="94f9e-247">Single</span><span class="sxs-lookup"><span data-stu-id="94f9e-247">Single</span></span>
<span data-ttu-id="94f9e-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="94f9e-248">DECIMAL</span></span> | <span data-ttu-id="94f9e-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="94f9e-249">Decimal</span></span>
<span data-ttu-id="94f9e-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="94f9e-250">BOOLEAN</span></span> | <span data-ttu-id="94f9e-251">Byte</span><span class="sxs-lookup"><span data-stu-id="94f9e-251">Byte</span></span>
<span data-ttu-id="94f9e-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="94f9e-252">VARCHAR</span></span> | <span data-ttu-id="94f9e-253">String</span><span class="sxs-lookup"><span data-stu-id="94f9e-253">String</span></span>
<span data-ttu-id="94f9e-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="94f9e-254">NVARCHAR</span></span> | <span data-ttu-id="94f9e-255">String</span><span class="sxs-lookup"><span data-stu-id="94f9e-255">String</span></span>
<span data-ttu-id="94f9e-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="94f9e-256">CLOB</span></span> | <span data-ttu-id="94f9e-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="94f9e-257">Byte[]</span></span>
<span data-ttu-id="94f9e-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="94f9e-258">ALPHANUM</span></span> | <span data-ttu-id="94f9e-259">String</span><span class="sxs-lookup"><span data-stu-id="94f9e-259">String</span></span>
<span data-ttu-id="94f9e-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="94f9e-260">BLOB</span></span> | <span data-ttu-id="94f9e-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="94f9e-261">Byte[]</span></span>
<span data-ttu-id="94f9e-262">DATE</span><span class="sxs-lookup"><span data-stu-id="94f9e-262">DATE</span></span> | <span data-ttu-id="94f9e-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="94f9e-263">DateTime</span></span>
<span data-ttu-id="94f9e-264">TIME</span><span class="sxs-lookup"><span data-stu-id="94f9e-264">TIME</span></span> | <span data-ttu-id="94f9e-265">timespan</span><span class="sxs-lookup"><span data-stu-id="94f9e-265">TimeSpan</span></span>
<span data-ttu-id="94f9e-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="94f9e-266">TIMESTAMP</span></span> | <span data-ttu-id="94f9e-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="94f9e-267">DateTime</span></span>
<span data-ttu-id="94f9e-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="94f9e-268">SECONDDATE</span></span> | <span data-ttu-id="94f9e-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="94f9e-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="94f9e-270">Limitaciones conocidas</span><span class="sxs-lookup"><span data-stu-id="94f9e-270">Known limitations</span></span>
<span data-ttu-id="94f9e-271">Cuando se copian datos de SAP HANA, hay algunas limitaciones conocidas:</span><span class="sxs-lookup"><span data-stu-id="94f9e-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="94f9e-272">Las cadenas NVARCHAR se truncan al llegar a la longitud máxima de 4000 caracteres Unicode</span><span class="sxs-lookup"><span data-stu-id="94f9e-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="94f9e-273">SMALLDECIMAL no se admite</span><span class="sxs-lookup"><span data-stu-id="94f9e-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="94f9e-274">VARBINARY no se admite</span><span class="sxs-lookup"><span data-stu-id="94f9e-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="94f9e-275">Las fechas válidas son las del intervalo entre 30/12/1899 y 31/12/9999</span><span class="sxs-lookup"><span data-stu-id="94f9e-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="94f9e-276">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="94f9e-276">Map source to sink columns</span></span>
<span data-ttu-id="94f9e-277">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="94f9e-278">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="94f9e-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="94f9e-279">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="94f9e-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="94f9e-280">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="94f9e-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="94f9e-281">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="94f9e-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="94f9e-282">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="94f9e-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="94f9e-283">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="94f9e-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="94f9e-284">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="94f9e-284">Performance and Tuning</span></span>
<span data-ttu-id="94f9e-285">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="94f9e-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
