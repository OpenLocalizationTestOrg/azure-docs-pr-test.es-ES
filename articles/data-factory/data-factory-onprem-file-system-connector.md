---
title: datos de aaaCopy hacia/desde un sistema de archivos con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy tooand de datos desde un sistema de archivos local mediante el uso de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="e1537-103">Copiar datos tooand desde un sistema de archivos local mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="e1537-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="e1537-104">Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toocopy a/desde un sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="e1537-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="e1537-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="e1537-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="e1537-106">Supported scenarios</span></span>
<span data-ttu-id="e1537-107">Puede copiar datos **desde un sistema de archivos local** toohello siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="e1537-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="e1537-108">Puede copiar los datos de hello siguientes almacenes de datos **tooan sistema de archivos local**:</span><span class="sxs-lookup"><span data-stu-id="e1537-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="e1537-109">Actividad de copia no elimina archivos de origen de Hola cuando este destino toohello copió correctamente.</span><span class="sxs-lookup"><span data-stu-id="e1537-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="e1537-110">Si necesita toodelete archivo de código fuente de hello después de una copia correcta, cree un archivo de actividad personalizada toodelete hello y usar actividad hello en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="e1537-111">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="e1537-111">Enabling connectivity</span></span>
<span data-ttu-id="e1537-112">Factoría de datos admite la conexión tooand desde un sistema de archivos local a través de **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="e1537-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="e1537-113">Debe instalar Hola Data Management Gateway en su entorno local para hello factoría de datos servicio tooconnect tooany local compatible almacén de datos incluyendo el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="e1537-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="e1537-114">toolearn acerca de Data Management Gateway y para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello, consulte [mover datos entre orígenes locales y en la nube con Data Management Gateway hello](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="e1537-115">Aparte de Data Management Gateway, no hay otros archivos binarios deben toobe instalado toocommunicate tooand desde un sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="e1537-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="e1537-116">Debe instalar y usar Hola Data Management Gateway incluso si es de sistema de archivos de hello en VM de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1537-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="e1537-117">Para obtener información detallada acerca de la puerta de enlace de hello, consulte [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="e1537-118">instalar un recurso compartido de archivos de Linux, toouse [Samba](https://www.samba.org/) en el servidor Linux e instalar Data Management Gateway en un servidor de Windows.</span><span class="sxs-lookup"><span data-stu-id="e1537-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="e1537-119">No se admite la instalación de la puerta de enlace de administración de datos en un servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="e1537-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e1537-120">Introducción</span><span class="sxs-lookup"><span data-stu-id="e1537-120">Getting started</span></span>
<span data-ttu-id="e1537-121">Puede crear una canalización con actividad de copia que mueva los datos desde un sistema de archivos o hacia él mediante el uso de distintas herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="e1537-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="e1537-122">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="e1537-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e1537-123">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="e1537-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="e1537-124">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="e1537-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e1537-125">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="e1537-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="e1537-126">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="e1537-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="e1537-127">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="e1537-127">Create a **data factory**.</span></span> <span data-ttu-id="e1537-128">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="e1537-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="e1537-129">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="e1537-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="e1537-130">Por ejemplo, si va a copiar datos desde un sistema de archivos de blob de Azure almacenamiento tooan local, cree dos toolink servicios vinculados su sistema de archivos local y la factoría de datos de almacenamiento de Azure cuenta tooyour.</span><span class="sxs-lookup"><span data-stu-id="e1537-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="e1537-131">Para las propiedades de servicio vinculado que el sistema de archivos local tooan específicos, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="e1537-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="e1537-132">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="e1537-133">En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="e1537-134">Y crear otro conjunto de datos toospecify Hola carpeta y nombre de archivo (opcional) en el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="e1537-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="e1537-135">Para el sistema de archivos de propiedades de conjunto de datos que son locales tooon específicos, consulte [propiedades de conjunto de datos](#dataset-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="e1537-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="e1537-136">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="e1537-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="e1537-137">En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y FileSystemSink como un receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="e1537-138">De forma similar, si va a copiar de tooAzure de sistema de archivos local almacenamiento de blobs, utilice FileSystemSource y BlobSink en la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="e1537-139">Para las propiedades de la actividad de copia local tooon específico de sistema de archivos, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="e1537-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="e1537-140">Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="e1537-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="e1537-141">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="e1537-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e1537-142">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e1537-143">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde un sistema de archivos, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-file-system) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="e1537-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="e1537-144">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que están toodefine usado factoría de datos entidades específicas toofile sistema:</span><span class="sxs-lookup"><span data-stu-id="e1537-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e1537-145">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="e1537-145">Linked service properties</span></span>
<span data-ttu-id="e1537-146">Puede vincular un generador de datos de Azure local tooan de sistema de archivo con hello **servidor de archivos local** servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="e1537-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="e1537-147">Hello en la tabla siguiente proporciona descripciones para los elementos JSON que sean específico toohello servicio servidor de archivos local vinculado.</span><span class="sxs-lookup"><span data-stu-id="e1537-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="e1537-148">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1537-148">Property</span></span> | <span data-ttu-id="e1537-149">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1537-149">Description</span></span> | <span data-ttu-id="e1537-150">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e1537-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1537-151">type</span><span class="sxs-lookup"><span data-stu-id="e1537-151">type</span></span> |<span data-ttu-id="e1537-152">Asegúrese de que la propiedad de tipo hello está establecido demasiado**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="e1537-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="e1537-153">Sí</span><span class="sxs-lookup"><span data-stu-id="e1537-153">Yes</span></span> |
| <span data-ttu-id="e1537-154">host</span><span class="sxs-lookup"><span data-stu-id="e1537-154">host</span></span> |<span data-ttu-id="e1537-155">Especifica la ruta de acceso de raíz de Hola de carpeta de Hola que desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="e1537-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="e1537-156">Utilice el carácter de escape de hello ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="e1537-157">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="e1537-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="e1537-158">Sí</span><span class="sxs-lookup"><span data-stu-id="e1537-158">Yes</span></span> |
| <span data-ttu-id="e1537-159">userid</span><span class="sxs-lookup"><span data-stu-id="e1537-159">userid</span></span> |<span data-ttu-id="e1537-160">Especifique el identificador de Hola Hola del usuario de que tiene acceso toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="e1537-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="e1537-161">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="e1537-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="e1537-162">Contraseña</span><span class="sxs-lookup"><span data-stu-id="e1537-162">password</span></span> |<span data-ttu-id="e1537-163">Especifique la contraseña de hello para el usuario de hello (userid).</span><span class="sxs-lookup"><span data-stu-id="e1537-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="e1537-164">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="e1537-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="e1537-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e1537-165">encryptedCredential</span></span> |<span data-ttu-id="e1537-166">Especifique las credenciales de hello cifrada que pueden obtener ejecutando el cmdlet New-AzureRmDataFactoryEncryptValue Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="e1537-167">No (si elige toospecify identificador de usuario y una contraseña en texto sin formato)</span><span class="sxs-lookup"><span data-stu-id="e1537-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="e1537-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e1537-168">gatewayName</span></span> |<span data-ttu-id="e1537-169">Especifica el nombre de Hola de puerta de enlace de Hola que factoría de datos debe usar el servidor de archivos de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="e1537-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="e1537-170">Sí</span><span class="sxs-lookup"><span data-stu-id="e1537-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="e1537-171">Ejemplos de definiciones de servicio vinculado y conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="e1537-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="e1537-172">Escenario</span><span class="sxs-lookup"><span data-stu-id="e1537-172">Scenario</span></span> | <span data-ttu-id="e1537-173">Host en definición de servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="e1537-173">Host in linked service definition</span></span> | <span data-ttu-id="e1537-174">folderPath en definición de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="e1537-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1537-175">Carpeta local en la máquina de Data Management Gateway:: </span><span class="sxs-lookup"><span data-stu-id="e1537-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="e1537-176">Ejemplos: D:\\\* o D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="e1537-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="e1537-177">D:\\\\ (para Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="e1537-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="e1537-178">localhost (para versiones anteriores a Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="e1537-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="e1537-179">\\\\ o la carpeta\\\\subcarpeta (Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="e1537-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="e1537-180">D:\\\\ o D:\\\\carpeta\\\\subcarpeta (para versiones de la puerta de enlace interiores a 2.0)</span><span class="sxs-lookup"><span data-stu-id="e1537-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="e1537-181">Carpeta compartida remota: </span><span class="sxs-lookup"><span data-stu-id="e1537-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="e1537-182">Ejemplos: \\\\myserver\\share\\\* o \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="e1537-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="e1537-183">\\\\\\\\myserver\\\\</span><span class="sxs-lookup"><span data-stu-id="e1537-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="e1537-184">.\\\\ o carpeta\\\\subcarpeta</span><span class="sxs-lookup"><span data-stu-id="e1537-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="e1537-185">Ejemplo: uso de nombre de usuario y contraseña en texto sin formato</span><span class="sxs-lookup"><span data-stu-id="e1537-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="e1537-186">Ejemplo: uso de encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="e1537-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="e1537-187">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="e1537-187">Dataset properties</span></span>
<span data-ttu-id="e1537-188">Para ver una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="e1537-189">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="e1537-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="e1537-190">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="e1537-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="e1537-191">Proporciona información como ubicación de Hola y el formato de datos de hello en el almacén de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="e1537-192">Hola typeProperties sección Hola conjunto de datos de tipo **FileShare** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1537-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="e1537-193">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1537-193">Property</span></span> | <span data-ttu-id="e1537-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1537-194">Description</span></span> | <span data-ttu-id="e1537-195">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e1537-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1537-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="e1537-196">folderPath</span></span> |<span data-ttu-id="e1537-197">Especifica la carpeta de hello subruta toohello.</span><span class="sxs-lookup"><span data-stu-id="e1537-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="e1537-198">Utilice el carácter de escape de hello ' \' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="e1537-199">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="e1537-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="e1537-200">Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin.</span><span class="sxs-lookup"><span data-stu-id="e1537-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="e1537-201">Sí</span><span class="sxs-lookup"><span data-stu-id="e1537-201">Yes</span></span> |
| <span data-ttu-id="e1537-202">fileName</span><span class="sxs-lookup"><span data-stu-id="e1537-202">fileName</span></span> |<span data-ttu-id="e1537-203">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="e1537-204">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="e1537-205">Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de actividad, nombre de hello del archivo hello generado está en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="e1537-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="e1537-206">`Data.<Guid>.txt` (Ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="e1537-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="e1537-207">No</span><span class="sxs-lookup"><span data-stu-id="e1537-207">No</span></span> |
| <span data-ttu-id="e1537-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="e1537-208">fileFilter</span></span> |<span data-ttu-id="e1537-209">Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="e1537-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="e1537-210">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="e1537-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="e1537-211">Ejemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="e1537-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="e1537-212">Ejemplo 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="e1537-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="e1537-213">Tenga en cuenta que fileFilter es aplicable a un conjunto de datos de FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="e1537-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="e1537-214">No</span><span class="sxs-lookup"><span data-stu-id="e1537-214">No</span></span> |
| <span data-ttu-id="e1537-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e1537-215">partitionedBy</span></span> |<span data-ttu-id="e1537-216">Puede usar partitionedBy toospecify dinámica folderPath/nombre de archivo para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="e1537-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="e1537-217">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="e1537-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="e1537-218">No</span><span class="sxs-lookup"><span data-stu-id="e1537-218">No</span></span> |
| <span data-ttu-id="e1537-219">formato</span><span class="sxs-lookup"><span data-stu-id="e1537-219">format</span></span> | <span data-ttu-id="e1537-220">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="e1537-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e1537-221">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="e1537-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e1537-222">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="e1537-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e1537-223">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="e1537-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e1537-224">No</span><span class="sxs-lookup"><span data-stu-id="e1537-224">No</span></span> |
| <span data-ttu-id="e1537-225">compresión</span><span class="sxs-lookup"><span data-stu-id="e1537-225">compression</span></span> | <span data-ttu-id="e1537-226">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e1537-227">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="e1537-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e1537-228">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="e1537-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e1537-229">consulte [Formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="e1537-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e1537-230">No</span><span class="sxs-lookup"><span data-stu-id="e1537-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="e1537-231">No se puede usar fileName y fileFilter a la vez.</span><span class="sxs-lookup"><span data-stu-id="e1537-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="e1537-232">Uso de la propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e1537-232">Using partitionedBy property</span></span>
<span data-ttu-id="e1537-233">Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámica y el nombre de archivo de datos de serie temporal con hello **partitionedBy** propiedad, [funciones de factoría de datos y las variables del sistema hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="e1537-234">toounderstand más detalles sobre los conjuntos de datos de series temporales, programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="e1537-235">Muestra 1:</span><span class="sxs-lookup"><span data-stu-id="e1537-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="e1537-236">En este ejemplo, {Slice} se reemplaza con el valor de Hola de variable del sistema Hola factoría de datos SliceStart en formato de hello (AAAAMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="e1537-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="e1537-237">SliceStart refiere a tiempo toostart de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="e1537-238">Hola folderPath es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="e1537-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="e1537-239">Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="e1537-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="e1537-240">Ejemplo 2:</span><span class="sxs-lookup"><span data-stu-id="e1537-240">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="e1537-241">En este ejemplo, año, mes, día y hora de SliceStart se extraen en variables independientes que usan propiedades folderPath y fileName de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e1537-242">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="e1537-242">Copy activity properties</span></span>
<span data-ttu-id="e1537-243">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="e1537-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e1537-244">Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="e1537-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="e1537-245">Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="e1537-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="e1537-246">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="e1537-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="e1537-247">Si va a mover datos desde un sistema de archivos local, establecer tipo de origen de hello en la actividad de copia de hello demasiado**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="e1537-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="e1537-248">De forma similar, si va a mover datos tooan sistema de archivos local, establezca el tipo de receptor de hello en la actividad de copia de hello demasiado**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="e1537-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="e1537-249">Esta sección proporciona una lista de las propiedades compatibles con FileSystemSource y FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="e1537-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="e1537-250">**FileSystemSource** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1537-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="e1537-251">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1537-251">Property</span></span> | <span data-ttu-id="e1537-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1537-252">Description</span></span> | <span data-ttu-id="e1537-253">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="e1537-253">Allowed values</span></span> | <span data-ttu-id="e1537-254">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e1537-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e1537-255">recursive</span><span class="sxs-lookup"><span data-stu-id="e1537-255">recursive</span></span> |<span data-ttu-id="e1537-256">Indica si los datos de Hola es de lectura de forma recursiva de las subcarpetas de Hola o solo de la carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="e1537-257">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="e1537-257">True, False (default)</span></span> |<span data-ttu-id="e1537-258">No</span><span class="sxs-lookup"><span data-stu-id="e1537-258">No</span></span> |

<span data-ttu-id="e1537-259">**FileSystemSink** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1537-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="e1537-260">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e1537-260">Property</span></span> | <span data-ttu-id="e1537-261">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1537-261">Description</span></span> | <span data-ttu-id="e1537-262">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="e1537-262">Allowed values</span></span> | <span data-ttu-id="e1537-263">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e1537-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e1537-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="e1537-264">copyBehavior</span></span> |<span data-ttu-id="e1537-265">Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="e1537-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="e1537-266">**PreserveHierarchy:** conserva la jerarquía de archivos de hello en la carpeta de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="e1537-267">Es decir, ruta de acceso relativa de Hola de carpeta de origen de toohello de archivo de origen de hello es Hola igual a la ruta de acceso relativa de Hola de carpeta de destino de toohello de archivo de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="e1537-268">**FlattenHierarchy:** todos los archivos de la carpeta de origen Hola se crean en el primer nivel de Hola de carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="e1537-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="e1537-269">archivos de destino de Hola se crean con un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e1537-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="e1537-270">**MergeFiles:** combina todos los archivos del archivo de tooone de carpeta de origen de hello.</span><span class="sxs-lookup"><span data-stu-id="e1537-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="e1537-271">Si se especifica el nombre de blob/nombre de archivo de hello, nombre de archivo combinado de hello es nombre especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="e1537-272">De lo contrario, es un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e1537-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="e1537-273">No</span><span class="sxs-lookup"><span data-stu-id="e1537-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="e1537-274">Ejemplos de recursive y copyBehavior</span><span class="sxs-lookup"><span data-stu-id="e1537-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="e1537-275">Esta sección describe el comportamiento resultante de Hola de operación de copia de Hola para diferentes combinaciones de valores para propiedades de recursiva y copyBehavior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="e1537-276">valor recursive</span><span class="sxs-lookup"><span data-stu-id="e1537-276">recursive value</span></span> | <span data-ttu-id="e1537-277">valor copyBehavior</span><span class="sxs-lookup"><span data-stu-id="e1537-277">copyBehavior value</span></span> | <span data-ttu-id="e1537-278">Comportamiento resultante</span><span class="sxs-lookup"><span data-stu-id="e1537-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1537-279">true</span><span class="sxs-lookup"><span data-stu-id="e1537-279">true</span></span> |<span data-ttu-id="e1537-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="e1537-280">preserveHierarchy</span></span> |<span data-ttu-id="e1537-281">Para una carpeta de origen carpeta1 con hello siguiendo estructura,</span><span class="sxs-lookup"><span data-stu-id="e1537-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="e1537-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-282">Folder1</span></span><br/><span data-ttu-id="e1537-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="e1537-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="e1537-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="e1537-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="e1537-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="e1537-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="e1537-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="e1537-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="e1537-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="e1537-289">se crea la carpeta de destino de Hola carpeta1 con hello misma estructura como origen de Hola:</span><span class="sxs-lookup"><span data-stu-id="e1537-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="e1537-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-290">Folder1</span></span><br/><span data-ttu-id="e1537-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="e1537-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="e1537-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="e1537-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="e1537-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="e1537-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="e1537-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="e1537-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="e1537-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="e1537-297">true</span><span class="sxs-lookup"><span data-stu-id="e1537-297">true</span></span> |<span data-ttu-id="e1537-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="e1537-298">flattenHierarchy</span></span> |<span data-ttu-id="e1537-299">Para una carpeta de origen carpeta1 con hello siguiendo estructura,</span><span class="sxs-lookup"><span data-stu-id="e1537-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="e1537-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-300">Folder1</span></span><br/><span data-ttu-id="e1537-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="e1537-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="e1537-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="e1537-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="e1537-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="e1537-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="e1537-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="e1537-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="e1537-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="e1537-307">se crea el destino de Hola carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="e1537-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="e1537-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-308">Folder1</span></span><br/><span data-ttu-id="e1537-309">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="e1537-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="e1537-310">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="e1537-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="e1537-311">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3</span><span class="sxs-lookup"><span data-stu-id="e1537-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="e1537-312">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4</span><span class="sxs-lookup"><span data-stu-id="e1537-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="e1537-313">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5</span><span class="sxs-lookup"><span data-stu-id="e1537-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="e1537-314">true</span><span class="sxs-lookup"><span data-stu-id="e1537-314">true</span></span> |<span data-ttu-id="e1537-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="e1537-315">mergeFiles</span></span> |<span data-ttu-id="e1537-316">Para una carpeta de origen carpeta1 con hello siguiendo estructura,</span><span class="sxs-lookup"><span data-stu-id="e1537-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="e1537-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-317">Folder1</span></span><br/><span data-ttu-id="e1537-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="e1537-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="e1537-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="e1537-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="e1537-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="e1537-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="e1537-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="e1537-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="e1537-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="e1537-324">se crea el destino de Hola carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="e1537-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="e1537-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-325">Folder1</span></span><br/><span data-ttu-id="e1537-326">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e1537-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="e1537-327">false</span><span class="sxs-lookup"><span data-stu-id="e1537-327">false</span></span> |<span data-ttu-id="e1537-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="e1537-328">preserveHierarchy</span></span> |<span data-ttu-id="e1537-329">Para una carpeta de origen carpeta1 con hello siguiendo estructura,</span><span class="sxs-lookup"><span data-stu-id="e1537-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="e1537-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-330">Folder1</span></span><br/><span data-ttu-id="e1537-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="e1537-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="e1537-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="e1537-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="e1537-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="e1537-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="e1537-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="e1537-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="e1537-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="e1537-337">carpeta de destino de Hello carpeta1 se crea con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="e1537-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="e1537-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-338">Folder1</span></span><br/><span data-ttu-id="e1537-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="e1537-341">No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="e1537-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="e1537-342">false</span><span class="sxs-lookup"><span data-stu-id="e1537-342">false</span></span> |<span data-ttu-id="e1537-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="e1537-343">flattenHierarchy</span></span> |<span data-ttu-id="e1537-344">Para una carpeta de origen carpeta1 con hello siguiendo estructura,</span><span class="sxs-lookup"><span data-stu-id="e1537-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="e1537-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-345">Folder1</span></span><br/><span data-ttu-id="e1537-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="e1537-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="e1537-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="e1537-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="e1537-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="e1537-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="e1537-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="e1537-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="e1537-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="e1537-352">carpeta de destino de Hello carpeta1 se crea con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="e1537-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="e1537-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-353">Folder1</span></span><br/><span data-ttu-id="e1537-354">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="e1537-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="e1537-355">&nbsp;&nbsp;&nbsp;&nbsp;nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="e1537-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="e1537-356">No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="e1537-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="e1537-357">false</span><span class="sxs-lookup"><span data-stu-id="e1537-357">false</span></span> |<span data-ttu-id="e1537-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="e1537-358">mergeFiles</span></span> |<span data-ttu-id="e1537-359">Para una carpeta de origen carpeta1 con hello siguiendo estructura,</span><span class="sxs-lookup"><span data-stu-id="e1537-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="e1537-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-360">Folder1</span></span><br/><span data-ttu-id="e1537-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="e1537-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="e1537-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="e1537-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="e1537-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="e1537-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="e1537-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="e1537-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="e1537-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="e1537-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="e1537-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="e1537-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="e1537-367">carpeta de destino de Hello carpeta1 se crea con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="e1537-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="e1537-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="e1537-368">Folder1</span></span><br/><span data-ttu-id="e1537-369">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e1537-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="e1537-370">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="e1537-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="e1537-371">No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="e1537-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="e1537-372">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="e1537-372">Supported file and compression formats</span></span>
<span data-ttu-id="e1537-373">Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="e1537-374">Ejemplos JSON para copiar datos tooand de sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="e1537-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="e1537-375">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e1537-376">Muestran cómo toocopy tooand de datos desde un sistema de archivos local y el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1537-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="e1537-377">Sin embargo, puede copiar datos *directamente* desde cualquiera de hello orígenes tooany de receptores de hello enumerados en [admite orígenes y receptores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando la actividad de copia de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1537-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="e1537-378">Ejemplo: Copiar datos desde un sistema de archivos local tooAzure almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="e1537-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="e1537-379">Este ejemplo se muestra cómo toocopy datos desde un sistema de archivos local tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="e1537-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="e1537-380">ejemplo de Hola tiene Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="e1537-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="e1537-381">Un servicio vinculado de tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="e1537-382">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="e1537-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="e1537-383">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="e1537-384">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="e1537-385">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e1537-386">Hola según muestra copia datos de serie temporal de un sistema de archivos local tooAzure almacenamiento de blobs cada hora.</span><span class="sxs-lookup"><span data-stu-id="e1537-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="e1537-387">propiedades JSON de Hola que se usan en estos ejemplos se describen en secciones de hello después de los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="e1537-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="e1537-388">Como primer paso, configurar la puerta de enlace de datos de administración según las instrucciones de hello en [mover datos entre orígenes locales y en la nube con Data Management Gateway hello](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="e1537-389">**Servicio vinculado del servidor de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="e1537-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="e1537-390">Se recomienda usar hello **encryptedCredential** propiedad en su lugar Hola **userid** y **contraseña** propiedades.</span><span class="sxs-lookup"><span data-stu-id="e1537-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="e1537-391">Consulte [Servicio vinculado del sistema de archivos](#linked-service-properties) para más información sobre este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="e1537-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="e1537-392">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="e1537-392">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="e1537-393">**Conjunto de datos de entrada del sistema de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="e1537-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="e1537-394">Los datos se seleccionan de un archivo nuevo cada hora.</span><span class="sxs-lookup"><span data-stu-id="e1537-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="e1537-395">Hola folderPath y propiedades de nombre de archivo se determinan en función del tiempo de inicio de Hola de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="e1537-396">Establecer `"external": "true"` informa factoría de datos de ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="e1537-397">**Conjunto de datos de salida de Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="e1537-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="e1537-398">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="e1537-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e1537-399">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="e1537-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e1537-400">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y hora de Hola Hola hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="e1537-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="e1537-401">**Actividad de copia en una canalización con origen del sistema de archivos y receptor blob:**</span><span class="sxs-lookup"><span data-stu-id="e1537-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="e1537-402">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="e1537-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="e1537-403">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource**, y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e1537-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="e1537-404">Ejemplo: Copiar los datos de sistema de archivos de base de datos de SQL Azure tooan local</span><span class="sxs-lookup"><span data-stu-id="e1537-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="e1537-405">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="e1537-405">hello following sample shows:</span></span>

* <span data-ttu-id="e1537-406">Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="e1537-407">Un servicio vinculado de tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="e1537-408">Un conjunto de datos de entrada de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="e1537-409">Un conjunto de datos de salida de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="e1537-410">Una canalización con una actividad de copia que usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) y [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e1537-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="e1537-411">ejemplo Hello copia datos de serie temporal de un sistema de archivos local de SQL Azure tabla tooan cada hora.</span><span class="sxs-lookup"><span data-stu-id="e1537-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="e1537-412">propiedades JSON de Hola que se usan en estos ejemplos se describen en secciones después de los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="e1537-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="e1537-413">**Servicio vinculado a Azure SQL Database:**</span><span class="sxs-lookup"><span data-stu-id="e1537-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="e1537-414">**Servicio vinculado del servidor de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="e1537-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="e1537-415">Se recomienda usar hello **encryptedCredential** propiedad en lugar de usar hello **userid** y **contraseña** propiedades.</span><span class="sxs-lookup"><span data-stu-id="e1537-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="e1537-416">Consulte [Servicio vinculado del sistema de archivos](#linked-service-properties) para más información sobre este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="e1537-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="e1537-417">**Conjunto de datos de entrada SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="e1537-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="e1537-418">ejemplo de Hola se supone que ha creado una tabla "MyTable" en SQL Azure, y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="e1537-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="e1537-419">Establecer ``“external”: ”true”`` informa factoría de datos de ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="e1537-420">**Conjunto de datos de salida del sistema de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="e1537-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="e1537-421">Datos son tooa copiado nuevo archivo cada hora.</span><span class="sxs-lookup"><span data-stu-id="e1537-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="e1537-422">folderPath Hola y el nombre de blob de Hola se determinan en función del tiempo de inicio de Hola de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="e1537-423">**Actividad de copia en una canalización con el origen de SQL y el receptor de sistema de archivos:**</span><span class="sxs-lookup"><span data-stu-id="e1537-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="e1537-424">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="e1537-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="e1537-425">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource**, hello y **receptor** tipo está establecido demasiado**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="e1537-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="e1537-426">consulta SQL de Hola que se especifica para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="e1537-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="e1537-427">También puede asignar columnas de toocolumns de conjunto de datos de origen del conjunto de datos de receptor en la definición de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1537-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="e1537-428">Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e1537-429">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="e1537-429">Performance and tuning</span></span>
 <span data-ttu-id="e1537-430">toolearn acerca de la clave de factores que afectan al rendimiento Hola de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas formas, vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="e1537-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
