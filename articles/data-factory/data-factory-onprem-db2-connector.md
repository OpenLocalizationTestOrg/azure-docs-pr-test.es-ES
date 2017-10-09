---
title: aaaMove datos de DB2 mediante el uso de Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde un DB2 local de base de datos mediante el uso de la actividad de copia de factoría de datos de Azure"
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
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="f9198-103">Movimiento de datos de DB2 mediante la actividad de copia de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f9198-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="f9198-104">Este artículo describe cómo puede usar actividad de copia de datos de Data Factory de Azure toocopy desde un almacén de datos local tooa de base de datos de DB2.</span><span class="sxs-lookup"><span data-stu-id="f9198-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="f9198-105">Puede copiar el almacén de datos de tooany que aparece como un receptor admitido en hello [las actividades de movimiento de datos de Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artículo.</span><span class="sxs-lookup"><span data-stu-id="f9198-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="f9198-106">En este tema se basa en el artículo de factoría de datos de hello, que presenta una visión general de movimiento de datos mediante la actividad de copia y se incluyen combinaciones de almacén de datos de Hola admitida.</span><span class="sxs-lookup"><span data-stu-id="f9198-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="f9198-107">Factoría de datos admite actualmente solo mover datos desde un tooa de base de datos de DB2 [almacén de datos del receptor compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f9198-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f9198-108">Mover los datos de otros datos almacena tooa DB2 no se admite la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f9198-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9198-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f9198-109">Prerequisites</span></span>
<span data-ttu-id="f9198-110">Factoría de datos admite la base de datos DB2 de conexión tooan local mediante hello [puerta de enlace de administración de datos](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f9198-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="f9198-111">Para instrucciones paso a paso tooset los datos de la puerta de enlace de hello canalización toomove los datos, consulte hello [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f9198-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f9198-112">Una puerta de enlace es necesaria incluso aunque hello DB2 alojada en VM de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9198-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="f9198-113">Puede instalar la puerta de enlace de hello en hello mismo IaaS VM como almacén de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="f9198-114">Si la puerta de enlace de hello puede conectarse toohello base de datos, puede instalar puerta de enlace de hello en una máquina virtual diferente.</span><span class="sxs-lookup"><span data-stu-id="f9198-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="f9198-115">puerta de enlace de administración de datos de Hello proporciona un controlador DB2 integrado, por lo que no necesita toomanually instalar una datos toocopy del controlador de DB2.</span><span class="sxs-lookup"><span data-stu-id="f9198-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="f9198-116">Para obtener sugerencias sobre cómo solucionar problemas de la puerta de enlace y de conexión, vea hello [solucionar problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artículo.</span><span class="sxs-lookup"><span data-stu-id="f9198-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="f9198-117">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="f9198-117">Supported versions</span></span>
<span data-ttu-id="f9198-118">Conector de Hello DB2 de factoría de datos admite Hola siguientes plataformas IBM DB2 y las versiones con el Administrador de acceso de SQL de arquitectura de base de datos relacionales (DRDA) distribuidas versiones 9, 10 y 11:</span><span class="sxs-lookup"><span data-stu-id="f9198-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="f9198-119">IBM DB2 para z/OS versión 11.1</span><span class="sxs-lookup"><span data-stu-id="f9198-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="f9198-120">IBM DB2 para z/OS versión 10.1</span><span class="sxs-lookup"><span data-stu-id="f9198-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="f9198-121">IBM DB2 para i (AS400) versión 7.2</span><span class="sxs-lookup"><span data-stu-id="f9198-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="f9198-122">IBM DB2 para i (AS400) versión 7.1</span><span class="sxs-lookup"><span data-stu-id="f9198-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="f9198-123">IBM DB2 para Linux, UNIX y (LUW) versión 11</span><span class="sxs-lookup"><span data-stu-id="f9198-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="f9198-124">IBM DB2 para LUW versión 10.5</span><span class="sxs-lookup"><span data-stu-id="f9198-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="f9198-125">IBM DB2 para LUW versión 10.1</span><span class="sxs-lookup"><span data-stu-id="f9198-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="f9198-126">Si recibe el mensaje de error de saludo "hello paquete correspondiente tooan SQL instrucción solicitud de ejecución no se encontró.</span><span class="sxs-lookup"><span data-stu-id="f9198-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="f9198-127">SQLSTATE = 51002 SQLCODE =-805, "motivo de hello no es se crea un paquete es necesario para el usuario normal de hello en hello SO.</span><span class="sxs-lookup"><span data-stu-id="f9198-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="f9198-128">tooresolve este problema, siga estas instrucciones para el tipo de servidor DB2:</span><span class="sxs-lookup"><span data-stu-id="f9198-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="f9198-129">DB2 para i (AS400): permiten a un usuario avanzado Crear colección de hello para el usuario normal de hello antes de ejecutar la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="f9198-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="f9198-130">colección de hello toocreate, use Hola comando:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="f9198-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="f9198-131">DB2 para z/OS o LUW: utilice una cuenta con privilegios elevados: un usuario avanzado o administrador que tenga entidades de paquete y se ENLAZA, BINDADD, conceda permisos de tooPUBLIC EXECUTE: copia de hello toorun una vez.</span><span class="sxs-lookup"><span data-stu-id="f9198-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="f9198-132">paquete necesario Hola se crea automáticamente durante la copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="f9198-133">A continuación, puede cambiar usuario normal toohello atrás para las ejecuciones de copia posteriores.</span><span class="sxs-lookup"><span data-stu-id="f9198-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f9198-134">Introducción</span><span class="sxs-lookup"><span data-stu-id="f9198-134">Getting started</span></span>
<span data-ttu-id="f9198-135">Puede crear una canalización con datos de toomove de actividad de copia de un almacén de datos de DB2 local mediante distintas herramientas y API:</span><span class="sxs-lookup"><span data-stu-id="f9198-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="f9198-136">toocreate de manera más fácil de Hello una canalización es toouse Hola Asistente para copiar de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9198-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="f9198-137">Para ver un tutorial rápido sobre cómo crear una canalización mediante Hola Asistente para copiar, vea hello [Tutorial: crear una canalización mediante Hola Asistente para copiar](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f9198-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="f9198-138">También puede usar herramientas toocreate una canalización, incluidos Hola portal de Azure, Visual Studio, Azure PowerShell, una plantilla de Azure Resource Manager, Hola API de .NET y Hola API de REST.</span><span class="sxs-lookup"><span data-stu-id="f9198-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="f9198-139">Para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia, consulte hello [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f9198-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="f9198-140">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="f9198-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="f9198-141">Crear la factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink de servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="f9198-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="f9198-142">Creación de conjuntos de datos toorepresent entrada y salida de datos para la operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="f9198-143">Cree una canalización con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="f9198-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f9198-144">Cuando usas Hola Asistente para copiar, definiciones de JSON para los servicios de la factoría de datos vinculado de Hola, conjuntos de datos y entidades de canalización se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="f9198-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="f9198-145">Cuando usa herramientas o las API (excepto Hola API. NET), defina las entidades de hello factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="f9198-146">Hola [ejemplo de JSON: copiar los datos de DB2 tooAzure almacenamiento de blobs](#json-example-copy-data-from-db2-to-azure-blob) muestra las definiciones de JSON de Hola para hello las entidades de la factoría de datos que son toocopy usa datos de un almacén de datos de DB2 local.</span><span class="sxs-lookup"><span data-stu-id="f9198-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="f9198-147">Hola las secciones siguientes proporciona detalles sobre Hola propiedades JSON que son utilizados toodefine Hola factoría de datos entidades que son el almacén de datos específico tooa DB2.</span><span class="sxs-lookup"><span data-stu-id="f9198-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="f9198-148">Propiedades del servicio vinculado de DB2</span><span class="sxs-lookup"><span data-stu-id="f9198-148">DB2 linked service properties</span></span>
<span data-ttu-id="f9198-149">Hello en la tabla siguiente enumera propiedades JSON de Hola que son tooa específico del servicio vinculado DB2.</span><span class="sxs-lookup"><span data-stu-id="f9198-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="f9198-150">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f9198-150">Property</span></span> | <span data-ttu-id="f9198-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="f9198-151">Description</span></span> | <span data-ttu-id="f9198-152">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f9198-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9198-153">**type**</span><span class="sxs-lookup"><span data-stu-id="f9198-153">**type**</span></span> |<span data-ttu-id="f9198-154">Esta propiedad debe establecerse demasiado**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="f9198-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="f9198-155">Sí</span><span class="sxs-lookup"><span data-stu-id="f9198-155">Yes</span></span> |
| <span data-ttu-id="f9198-156">**server**</span><span class="sxs-lookup"><span data-stu-id="f9198-156">**server**</span></span> |<span data-ttu-id="f9198-157">nombre de saludo del servidor de hello DB2.</span><span class="sxs-lookup"><span data-stu-id="f9198-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="f9198-158">Sí</span><span class="sxs-lookup"><span data-stu-id="f9198-158">Yes</span></span> |
| <span data-ttu-id="f9198-159">**database**</span><span class="sxs-lookup"><span data-stu-id="f9198-159">**database**</span></span> |<span data-ttu-id="f9198-160">nombre de Hola de base de datos de DB2 Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="f9198-161">Sí</span><span class="sxs-lookup"><span data-stu-id="f9198-161">Yes</span></span> |
| <span data-ttu-id="f9198-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="f9198-162">**schema**</span></span> |<span data-ttu-id="f9198-163">nombre de Hello del esquema de hello en la base de datos de DB2 Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="f9198-164">Esta propiedad distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f9198-164">This property is case-sensitive.</span></span> |<span data-ttu-id="f9198-165">No</span><span class="sxs-lookup"><span data-stu-id="f9198-165">No</span></span> |
| <span data-ttu-id="f9198-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="f9198-166">**authenticationType**</span></span> |<span data-ttu-id="f9198-167">tipo de Hola de autenticación que es la base de datos de uso tooconnect toohello DB2.</span><span class="sxs-lookup"><span data-stu-id="f9198-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="f9198-168">Hola los valores posibles son: anónima, básica y Windows.</span><span class="sxs-lookup"><span data-stu-id="f9198-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="f9198-169">Sí</span><span class="sxs-lookup"><span data-stu-id="f9198-169">Yes</span></span> |
| <span data-ttu-id="f9198-170">**username**</span><span class="sxs-lookup"><span data-stu-id="f9198-170">**username**</span></span> |<span data-ttu-id="f9198-171">nombre de Hello para la cuenta de usuario de hello si utiliza la autenticación básica o de Windows.</span><span class="sxs-lookup"><span data-stu-id="f9198-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="f9198-172">No</span><span class="sxs-lookup"><span data-stu-id="f9198-172">No</span></span> |
| <span data-ttu-id="f9198-173">**password**</span><span class="sxs-lookup"><span data-stu-id="f9198-173">**password**</span></span> |<span data-ttu-id="f9198-174">contraseña de Hello para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-174">hello password for hello user account.</span></span> |<span data-ttu-id="f9198-175">No</span><span class="sxs-lookup"><span data-stu-id="f9198-175">No</span></span> |
| <span data-ttu-id="f9198-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="f9198-176">**gatewayName**</span></span> |<span data-ttu-id="f9198-177">nombre de Hola de puerta de enlace de Hola Hola servicio Data Factory debe usar base de datos de DB2 de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="f9198-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="f9198-178">Sí</span><span class="sxs-lookup"><span data-stu-id="f9198-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f9198-179">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="f9198-179">Dataset properties</span></span>
<span data-ttu-id="f9198-180">Para obtener una lista de secciones de Hola y propiedades que están disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f9198-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f9198-181">Las secciones, como **estructura**, **disponibilidad**, hello y **directiva** para un conjunto de datos JSON son similares para todos los tipos de conjunto de datos (SQL Azure, almacenamiento de blobs de Azure, tabla de Azure almacenamiento y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="f9198-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="f9198-182">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="f9198-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="f9198-183">Hola **typeProperties** sección para un conjunto de datos de tipo **RelationalTable**, que incluye el conjunto de datos de DB2 hello, tiene Hola después de propiedad:</span><span class="sxs-lookup"><span data-stu-id="f9198-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="f9198-184">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f9198-184">Property</span></span> | <span data-ttu-id="f9198-185">Descripción</span><span class="sxs-lookup"><span data-stu-id="f9198-185">Description</span></span> | <span data-ttu-id="f9198-186">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f9198-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9198-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="f9198-187">**tableName**</span></span> |<span data-ttu-id="f9198-188">Hola nombre de tabla de hello en la instancia de base de datos de DB2 de Hola que Hola servicio vinculado hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="f9198-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="f9198-189">Esta propiedad distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f9198-189">This property is case-sensitive.</span></span> |<span data-ttu-id="f9198-190">No (si hello **consulta** propiedad de una actividad de copia de tipo **RelationalSource** se especifica)</span><span class="sxs-lookup"><span data-stu-id="f9198-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f9198-191">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="f9198-191">Copy Activity properties</span></span>
<span data-ttu-id="f9198-192">Para obtener una lista de secciones de Hola y propiedades que están disponibles para la definición de actividades de copia, consulte hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f9198-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f9198-193">Las propiedades de la actividad de copia, como **nombre**, **descripción**, tabla de **entradas**, tabla de **salidas** y **directiva**, están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="f9198-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="f9198-194">Hola propiedades que están disponibles en hello **typeProperties** sección de la actividad de Hola para cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="f9198-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="f9198-195">Para la actividad de copia, propiedades de hello varían en función de tipos de hello receptores y orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="f9198-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="f9198-196">Para la actividad de copia, cuando el origen de hello es de tipo **RelationalSource** (que incluye DB2), Hola propiedades siguientes está disponible en hello **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="f9198-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="f9198-197">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f9198-197">Property</span></span> | <span data-ttu-id="f9198-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="f9198-198">Description</span></span> | <span data-ttu-id="f9198-199">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f9198-199">Allowed values</span></span> | <span data-ttu-id="f9198-200">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f9198-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9198-201">**consulta**</span><span class="sxs-lookup"><span data-stu-id="f9198-201">**query**</span></span> |<span data-ttu-id="f9198-202">Usar datos de hello consulta personalizada tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="f9198-203">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="f9198-203">SQL query string.</span></span> <span data-ttu-id="f9198-204">Por ejemplo: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="f9198-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="f9198-205">No (si hello **tableName** se especifica la propiedad de un conjunto de datos)</span><span class="sxs-lookup"><span data-stu-id="f9198-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="f9198-206">Los nombres de esquema y tabla distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f9198-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="f9198-207">En la instrucción de consulta de hello, incluya los nombres de propiedad mediante el uso de "" (comillas dobles).</span><span class="sxs-lookup"><span data-stu-id="f9198-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="f9198-208">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f9198-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="f9198-209">Ejemplo de JSON: copiar los datos de DB2 tooAzure almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="f9198-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="f9198-210">Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f9198-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f9198-211">ejemplo de Hola muestra cómo la base de datos de toocopy de DB2 datos tooBlob almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f9198-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="f9198-212">Sin embargo, se pueden copiar datos demasiado[todos los datos admitidos almacenan el tipo de receptor](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante el uso de la actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9198-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="f9198-213">ejemplo de Hola tiene Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="f9198-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="f9198-214">Un servicio vinculado DB2 de tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f9198-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="f9198-215">Un servicio vinculado de Azure Blob Storage de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f9198-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="f9198-216">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f9198-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="f9198-217">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f9198-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="f9198-218">A [canalización](data-factory-create-pipelines.md) con una actividad de copia que utiliza hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) propiedades</span><span class="sxs-lookup"><span data-stu-id="f9198-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="f9198-219">ejemplo Hello copia datos de un resultado de consulta en un tooan de base de datos DB2 blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="f9198-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="f9198-220">propiedades JSON de Hola que se usan en el ejemplo de Hola se describen en las secciones de Hola que siguen a las definiciones de entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="f9198-221">Como primer paso, instale y configure una puerta de enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="f9198-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="f9198-222">Las instrucciones están en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f9198-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f9198-223">**Servicio vinculado DB2**</span><span class="sxs-lookup"><span data-stu-id="f9198-223">**DB2 linked service**</span></span>

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

<span data-ttu-id="f9198-224">**Servicio vinculado de almacenamiento de blobs de Azure**</span><span class="sxs-lookup"><span data-stu-id="f9198-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="f9198-225">**Conjunto de datos de entrada de DB2**</span><span class="sxs-lookup"><span data-stu-id="f9198-225">**DB2 input dataset**</span></span>

<span data-ttu-id="f9198-226">ejemplo de Hola se da por supuesto que ha creado una tabla de DB2 con el nombre "MyTable" que tiene una columna denominada "timestamp" para los datos de serie temporal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="f9198-227">Hola **externo** propiedad se establece demasiado "true".</span><span class="sxs-lookup"><span data-stu-id="f9198-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="f9198-228">Esta configuración indica el servicio de factoría de datos de Hola que este conjunto de datos es externo toohello factoría de datos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="f9198-229">Tenga en cuenta que hello **tipo** propiedad se establece demasiado**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="f9198-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


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

<span data-ttu-id="f9198-230">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="f9198-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="f9198-231">Los datos se escriben cada hora de tooa nuevo blob mediante configuración hello **frecuencia** propiedad demasiado hello y "Hora" **intervalo** too1 de propiedad.</span><span class="sxs-lookup"><span data-stu-id="f9198-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="f9198-232">Hola **folderPath** propiedad de blob de Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="f9198-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f9198-233">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y hora de Hola Hola hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="f9198-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

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

<span data-ttu-id="f9198-234">**Canalización para la actividad de copia de hello**</span><span class="sxs-lookup"><span data-stu-id="f9198-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="f9198-235">canalización de Hello contiene una actividad de copia que se configura toouse especifica los conjuntos de datos de entrada y salida y que es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="f9198-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="f9198-236">Hola definición JSON de la canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** hello y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f9198-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="f9198-237">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos de Hola de tabla de Hola "Orders".</span><span class="sxs-lookup"><span data-stu-id="f9198-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
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

## <a name="type-mapping-for-db2"></a><span data-ttu-id="f9198-238">Asignación de tipos para DB2</span><span class="sxs-lookup"><span data-stu-id="f9198-238">Type mapping for DB2</span></span>
<span data-ttu-id="f9198-239">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática del tipo de toosink de tipo de origen mediante Hola enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="f9198-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="f9198-240">Convertir de un tipo de origen nativo tipo tooa .NET</span><span class="sxs-lookup"><span data-stu-id="f9198-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="f9198-241">Convertir de un tipo de receptor nativo de tooa de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="f9198-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="f9198-242">Hello asignaciones siguientes se utilizan cuando copia actividad convierte datos de Hola de un tipo de .NET de DB2 tipo tooa:</span><span class="sxs-lookup"><span data-stu-id="f9198-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="f9198-243">Tipo de base de datos DB2</span><span class="sxs-lookup"><span data-stu-id="f9198-243">DB2 database type</span></span> | <span data-ttu-id="f9198-244">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f9198-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="f9198-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f9198-245">SmallInt</span></span> |<span data-ttu-id="f9198-246">Int16</span><span class="sxs-lookup"><span data-stu-id="f9198-246">Int16</span></span> |
| <span data-ttu-id="f9198-247">Entero</span><span class="sxs-lookup"><span data-stu-id="f9198-247">Integer</span></span> |<span data-ttu-id="f9198-248">Int32</span><span class="sxs-lookup"><span data-stu-id="f9198-248">Int32</span></span> |
| <span data-ttu-id="f9198-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="f9198-249">BigInt</span></span> |<span data-ttu-id="f9198-250">Int64</span><span class="sxs-lookup"><span data-stu-id="f9198-250">Int64</span></span> |
| <span data-ttu-id="f9198-251">Real</span><span class="sxs-lookup"><span data-stu-id="f9198-251">Real</span></span> |<span data-ttu-id="f9198-252">Single</span><span class="sxs-lookup"><span data-stu-id="f9198-252">Single</span></span> |
| <span data-ttu-id="f9198-253">Doble</span><span class="sxs-lookup"><span data-stu-id="f9198-253">Double</span></span> |<span data-ttu-id="f9198-254">Doble</span><span class="sxs-lookup"><span data-stu-id="f9198-254">Double</span></span> |
| <span data-ttu-id="f9198-255">Float</span><span class="sxs-lookup"><span data-stu-id="f9198-255">Float</span></span> |<span data-ttu-id="f9198-256">Doble</span><span class="sxs-lookup"><span data-stu-id="f9198-256">Double</span></span> |
| <span data-ttu-id="f9198-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-257">Decimal</span></span> |<span data-ttu-id="f9198-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-258">Decimal</span></span> |
| <span data-ttu-id="f9198-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="f9198-259">DecimalFloat</span></span> |<span data-ttu-id="f9198-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-260">Decimal</span></span> |
| <span data-ttu-id="f9198-261">Numeric</span><span class="sxs-lookup"><span data-stu-id="f9198-261">Numeric</span></span> |<span data-ttu-id="f9198-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-262">Decimal</span></span> |
| <span data-ttu-id="f9198-263">Date</span><span class="sxs-lookup"><span data-stu-id="f9198-263">Date</span></span> |<span data-ttu-id="f9198-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="f9198-264">DateTime</span></span> |
| <span data-ttu-id="f9198-265">Hora</span><span class="sxs-lookup"><span data-stu-id="f9198-265">Time</span></span> |<span data-ttu-id="f9198-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f9198-266">TimeSpan</span></span> |
| <span data-ttu-id="f9198-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="f9198-267">Timestamp</span></span> |<span data-ttu-id="f9198-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="f9198-268">DateTime</span></span> |
| <span data-ttu-id="f9198-269">xml</span><span class="sxs-lookup"><span data-stu-id="f9198-269">Xml</span></span> |<span data-ttu-id="f9198-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f9198-270">Byte[]</span></span> |
| <span data-ttu-id="f9198-271">Char</span><span class="sxs-lookup"><span data-stu-id="f9198-271">Char</span></span> |<span data-ttu-id="f9198-272">String</span><span class="sxs-lookup"><span data-stu-id="f9198-272">String</span></span> |
| <span data-ttu-id="f9198-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="f9198-273">VarChar</span></span> |<span data-ttu-id="f9198-274">String</span><span class="sxs-lookup"><span data-stu-id="f9198-274">String</span></span> |
| <span data-ttu-id="f9198-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="f9198-275">LongVarChar</span></span> |<span data-ttu-id="f9198-276">String</span><span class="sxs-lookup"><span data-stu-id="f9198-276">String</span></span> |
| <span data-ttu-id="f9198-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="f9198-277">DB2DynArray</span></span> |<span data-ttu-id="f9198-278">String</span><span class="sxs-lookup"><span data-stu-id="f9198-278">String</span></span> |
| <span data-ttu-id="f9198-279">Binary</span><span class="sxs-lookup"><span data-stu-id="f9198-279">Binary</span></span> |<span data-ttu-id="f9198-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f9198-280">Byte[]</span></span> |
| <span data-ttu-id="f9198-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="f9198-281">VarBinary</span></span> |<span data-ttu-id="f9198-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f9198-282">Byte[]</span></span> |
| <span data-ttu-id="f9198-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="f9198-283">LongVarBinary</span></span> |<span data-ttu-id="f9198-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f9198-284">Byte[]</span></span> |
| <span data-ttu-id="f9198-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="f9198-285">Graphic</span></span> |<span data-ttu-id="f9198-286">String</span><span class="sxs-lookup"><span data-stu-id="f9198-286">String</span></span> |
| <span data-ttu-id="f9198-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="f9198-287">VarGraphic</span></span> |<span data-ttu-id="f9198-288">String</span><span class="sxs-lookup"><span data-stu-id="f9198-288">String</span></span> |
| <span data-ttu-id="f9198-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="f9198-289">LongVarGraphic</span></span> |<span data-ttu-id="f9198-290">String</span><span class="sxs-lookup"><span data-stu-id="f9198-290">String</span></span> |
| <span data-ttu-id="f9198-291">Clob</span><span class="sxs-lookup"><span data-stu-id="f9198-291">Clob</span></span> |<span data-ttu-id="f9198-292">String</span><span class="sxs-lookup"><span data-stu-id="f9198-292">String</span></span> |
| <span data-ttu-id="f9198-293">Blob</span><span class="sxs-lookup"><span data-stu-id="f9198-293">Blob</span></span> |<span data-ttu-id="f9198-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f9198-294">Byte[]</span></span> |
| <span data-ttu-id="f9198-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="f9198-295">DbClob</span></span> |<span data-ttu-id="f9198-296">String</span><span class="sxs-lookup"><span data-stu-id="f9198-296">String</span></span> |
| <span data-ttu-id="f9198-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f9198-297">SmallInt</span></span> |<span data-ttu-id="f9198-298">Int16</span><span class="sxs-lookup"><span data-stu-id="f9198-298">Int16</span></span> |
| <span data-ttu-id="f9198-299">Entero</span><span class="sxs-lookup"><span data-stu-id="f9198-299">Integer</span></span> |<span data-ttu-id="f9198-300">Int32</span><span class="sxs-lookup"><span data-stu-id="f9198-300">Int32</span></span> |
| <span data-ttu-id="f9198-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="f9198-301">BigInt</span></span> |<span data-ttu-id="f9198-302">Int64</span><span class="sxs-lookup"><span data-stu-id="f9198-302">Int64</span></span> |
| <span data-ttu-id="f9198-303">Real</span><span class="sxs-lookup"><span data-stu-id="f9198-303">Real</span></span> |<span data-ttu-id="f9198-304">Single</span><span class="sxs-lookup"><span data-stu-id="f9198-304">Single</span></span> |
| <span data-ttu-id="f9198-305">Doble</span><span class="sxs-lookup"><span data-stu-id="f9198-305">Double</span></span> |<span data-ttu-id="f9198-306">Doble</span><span class="sxs-lookup"><span data-stu-id="f9198-306">Double</span></span> |
| <span data-ttu-id="f9198-307">Float</span><span class="sxs-lookup"><span data-stu-id="f9198-307">Float</span></span> |<span data-ttu-id="f9198-308">Doble</span><span class="sxs-lookup"><span data-stu-id="f9198-308">Double</span></span> |
| <span data-ttu-id="f9198-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-309">Decimal</span></span> |<span data-ttu-id="f9198-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-310">Decimal</span></span> |
| <span data-ttu-id="f9198-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="f9198-311">DecimalFloat</span></span> |<span data-ttu-id="f9198-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-312">Decimal</span></span> |
| <span data-ttu-id="f9198-313">Numeric</span><span class="sxs-lookup"><span data-stu-id="f9198-313">Numeric</span></span> |<span data-ttu-id="f9198-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="f9198-314">Decimal</span></span> |
| <span data-ttu-id="f9198-315">Date</span><span class="sxs-lookup"><span data-stu-id="f9198-315">Date</span></span> |<span data-ttu-id="f9198-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="f9198-316">DateTime</span></span> |
| <span data-ttu-id="f9198-317">Hora</span><span class="sxs-lookup"><span data-stu-id="f9198-317">Time</span></span> |<span data-ttu-id="f9198-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f9198-318">TimeSpan</span></span> |
| <span data-ttu-id="f9198-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="f9198-319">Timestamp</span></span> |<span data-ttu-id="f9198-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="f9198-320">DateTime</span></span> |
| <span data-ttu-id="f9198-321">xml</span><span class="sxs-lookup"><span data-stu-id="f9198-321">Xml</span></span> |<span data-ttu-id="f9198-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f9198-322">Byte[]</span></span> |
| <span data-ttu-id="f9198-323">Char</span><span class="sxs-lookup"><span data-stu-id="f9198-323">Char</span></span> |<span data-ttu-id="f9198-324">String</span><span class="sxs-lookup"><span data-stu-id="f9198-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="f9198-325">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="f9198-325">Map source toosink columns</span></span>
<span data-ttu-id="f9198-326">toolearn toomap columnas en hello toocolumns de conjunto de datos de origen en el conjunto de datos de receptor de hello, vea [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f9198-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="f9198-327">Lecturas repetibles desde orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="f9198-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="f9198-328">Al copiar datos desde un almacén de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="f9198-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="f9198-329">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="f9198-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f9198-330">También puede configurar reintento hello **directiva** propiedad para un toorerun un segmento cuando se produce un error de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f9198-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="f9198-331">Asegúrese de que Hola mismo no se leen los datos importar cómo segmento de hello muchas veces se vuelva a ejecutar y, a continuación, independientemente de cómo volver a ejecutar el segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9198-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="f9198-332">Para más información, consulte [Lecturas repetibles desde orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f9198-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f9198-333">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="f9198-333">Performance and tuning</span></span>
<span data-ttu-id="f9198-334">Obtenga información acerca de los factores claves que afectan al rendimiento de Hola de actividad de copia y maneras de rendimiento toooptimize en hello [copia actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="f9198-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
