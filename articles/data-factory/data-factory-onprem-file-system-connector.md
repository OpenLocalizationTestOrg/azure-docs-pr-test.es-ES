---
title: "Copia de datos hacia un sistema de archivos y desde él con Azure Data Factory | Microsoft Docs"
description: "Aprenda a copiar datos hacia el sistema de archivos local y desde él con Azure Data Factory."
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
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="260f5-103">Copia de datos hacia y desde el sistema de archivos local mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="260f5-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="260f5-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para copiar datos hacia y desde un sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="260f5-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="260f5-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="260f5-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="260f5-106">Supported scenarios</span></span>
<span data-ttu-id="260f5-107">Puede copiar datos **de un sistema de archivos local** a los siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="260f5-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="260f5-108">Puede copiar datos de los siguientes almacenes de datos **a un sistema de archivos local**:</span><span class="sxs-lookup"><span data-stu-id="260f5-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="260f5-109">La actividad de copia no elimina el archivo de origen una vez copiado correctamente en el destino.</span><span class="sxs-lookup"><span data-stu-id="260f5-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="260f5-110">Si necesita eliminar el archivo de origen tras una copia correcta, cree una actividad personalizada para tal fin y úsela en la canalización.</span><span class="sxs-lookup"><span data-stu-id="260f5-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="260f5-111">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="260f5-111">Enabling connectivity</span></span>
<span data-ttu-id="260f5-112">Data Factory admite la conexión hacia y desde el sistema de archivos local mediante **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="260f5-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="260f5-113">Debe instalar Data Management Gateway en el entorno local para que el servicio de Data Factory se conecte a cualquier almacén de datos local compatible, incluido el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="260f5-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="260f5-114">Para más información al respecto y para obtener instrucciones paso a paso sobre la configuración de una puerta de enlace, consulte [Movimiento de datos entre orígenes locales y la nube con la puerta de enlace de administración de datos](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="260f5-115">Aparte de la puerta de enlace de administración de datos, no es necesario instalar otros archivos binarios para la comunicación hacia y desde un sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="260f5-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="260f5-116">Debe instalar y usar Data Management Gateway incluso si el sistema de archivos está en la máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="260f5-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="260f5-117">Para información más detallada sobre la puerta de enlace, consulte el artículo sobre [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="260f5-118">Para usar un recurso compartido de archivos de Linux, instale [Samba](https://www.samba.org/) en el servidor Linux e instale Data Management Gateway en un servidor Windows.</span><span class="sxs-lookup"><span data-stu-id="260f5-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="260f5-119">No se admite la instalación de la puerta de enlace de administración de datos en un servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="260f5-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="260f5-120">Introducción</span><span class="sxs-lookup"><span data-stu-id="260f5-120">Getting started</span></span>
<span data-ttu-id="260f5-121">Puede crear una canalización con actividad de copia que mueva los datos desde un sistema de archivos o hacia él mediante el uso de distintas herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="260f5-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="260f5-122">La manera más fácil de crear una canalización es usar el **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="260f5-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="260f5-123">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="260f5-124">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="260f5-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="260f5-125">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="260f5-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="260f5-126">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="260f5-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="260f5-127">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="260f5-127">Create a **data factory**.</span></span> <span data-ttu-id="260f5-128">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="260f5-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="260f5-129">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="260f5-130">Por ejemplo, si va a copiar datos de una instancia de Azure Blob Storage a un sistema de archivos local, creará dos servicios vinculados para vincular su sistema de archivos local y la cuenta de Azure Storage a su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="260f5-131">Para información sobre las propiedades de los servicios vinculados que son específicas de un sistema de archivos local, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="260f5-132">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="260f5-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="260f5-133">En el ejemplo mencionado en el último paso, se crea un conjunto de datos para especificar el contenedor de blobs y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="260f5-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="260f5-134">Y se crea otro conjunto de datos para especificar la carpeta y el nombre de archivo (opcional) en el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="260f5-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="260f5-135">Para información sobre las propiedades de los conjuntos de datos que son específicas del sistema de archivos local, consulte [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="260f5-136">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="260f5-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="260f5-137">En el ejemplo que se ha mencionado anteriormente, se usa BlobSource como origen y FileSystemSink como receptor en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="260f5-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="260f5-138">De igual forma, si va a copiar desde un sistema de archivos local hacia Azure Blob Storage, usará FileSystemSource y BlobSink en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="260f5-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="260f5-139">Para información sobre las propiedades de la actividad de copia que son específicas del sistema de archivos local, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="260f5-140">Para más información sobre cómo usar un almacén de datos como origen o como receptor, haga clic en el vínculo de la sección anterior para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="260f5-141">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="260f5-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="260f5-142">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="260f5-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="260f5-143">Para ver ejemplos con definiciones de JSON para entidades de Data Factory que se usan para copiar datos hacia un sistema de archivos y desde este, consulte la sección [Ejemplos de JSON](#json-examples-for-copying-data-to-and-from-file-system) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="260f5-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="260f5-144">En las secciones siguientes, se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un sistema de archivos:</span><span class="sxs-lookup"><span data-stu-id="260f5-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="260f5-145">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="260f5-145">Linked service properties</span></span>
<span data-ttu-id="260f5-146">Un sistema de archivos local se puede vincular a una factoría de datos de Azure con el servicio vinculado del **servidor de archivos local**.</span><span class="sxs-lookup"><span data-stu-id="260f5-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="260f5-147">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos al servicio vinculado del servidor de archivos local.</span><span class="sxs-lookup"><span data-stu-id="260f5-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="260f5-148">Propiedad</span><span class="sxs-lookup"><span data-stu-id="260f5-148">Property</span></span> | <span data-ttu-id="260f5-149">Descripción</span><span class="sxs-lookup"><span data-stu-id="260f5-149">Description</span></span> | <span data-ttu-id="260f5-150">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="260f5-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="260f5-151">type</span><span class="sxs-lookup"><span data-stu-id="260f5-151">type</span></span> |<span data-ttu-id="260f5-152">Asegúrese de que la propiedad type esté establecida en **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="260f5-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="260f5-153">Sí</span><span class="sxs-lookup"><span data-stu-id="260f5-153">Yes</span></span> |
| <span data-ttu-id="260f5-154">host</span><span class="sxs-lookup"><span data-stu-id="260f5-154">host</span></span> |<span data-ttu-id="260f5-155">Especifica la ruta de acceso raíz de la carpeta que quiere copiar.</span><span class="sxs-lookup"><span data-stu-id="260f5-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="260f5-156">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="260f5-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="260f5-157">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="260f5-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="260f5-158">Sí</span><span class="sxs-lookup"><span data-stu-id="260f5-158">Yes</span></span> |
| <span data-ttu-id="260f5-159">userid</span><span class="sxs-lookup"><span data-stu-id="260f5-159">userid</span></span> |<span data-ttu-id="260f5-160">Especifique el identificador del usuario que tiene acceso al servidor.</span><span class="sxs-lookup"><span data-stu-id="260f5-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="260f5-161">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="260f5-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="260f5-162">contraseña</span><span class="sxs-lookup"><span data-stu-id="260f5-162">password</span></span> |<span data-ttu-id="260f5-163">Especifique la contraseña del usuario (identificador de usuario).</span><span class="sxs-lookup"><span data-stu-id="260f5-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="260f5-164">No (si elige encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="260f5-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="260f5-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="260f5-165">encryptedCredential</span></span> |<span data-ttu-id="260f5-166">Especifique las credenciales cifradas que puede obtener ejecutando el cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="260f5-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="260f5-167">No (si opta por especificar el identificador de usuario y la contraseña en texto sin formato)</span><span class="sxs-lookup"><span data-stu-id="260f5-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="260f5-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="260f5-168">gatewayName</span></span> |<span data-ttu-id="260f5-169">Especifica el nombre de la puerta de enlace que debe usar Data Factory para conectarse al servidor de archivos local.</span><span class="sxs-lookup"><span data-stu-id="260f5-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="260f5-170">Sí</span><span class="sxs-lookup"><span data-stu-id="260f5-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="260f5-171">Ejemplos de definiciones de servicio vinculado y conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="260f5-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="260f5-172">Escenario</span><span class="sxs-lookup"><span data-stu-id="260f5-172">Scenario</span></span> | <span data-ttu-id="260f5-173">Host en definición de servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="260f5-173">Host in linked service definition</span></span> | <span data-ttu-id="260f5-174">folderPath en definición de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="260f5-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="260f5-175">Carpeta local en la máquina de Data Management Gateway:: </span><span class="sxs-lookup"><span data-stu-id="260f5-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="260f5-176">Ejemplos: D:\\\* o D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="260f5-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="260f5-177">D:\\\\ (para Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="260f5-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="260f5-178">localhost (para versiones anteriores a Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="260f5-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="260f5-179">\\\\ o la carpeta\\\\subcarpeta (Data Management Gateway 2.0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="260f5-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="260f5-180">D:\\\\ o D:\\\\carpeta\\\\subcarpeta (para versiones de la puerta de enlace interiores a 2.0)</span><span class="sxs-lookup"><span data-stu-id="260f5-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="260f5-181">Carpeta compartida remota: </span><span class="sxs-lookup"><span data-stu-id="260f5-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="260f5-182">Ejemplos: \\\\myserver\\share\\\* o \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="260f5-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="260f5-183">\\\\\\\\myserver\\\\</span><span class="sxs-lookup"><span data-stu-id="260f5-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="260f5-184">.\\\\ o carpeta\\\\subcarpeta</span><span class="sxs-lookup"><span data-stu-id="260f5-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="260f5-185">Ejemplo: uso de nombre de usuario y contraseña en texto sin formato</span><span class="sxs-lookup"><span data-stu-id="260f5-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="260f5-186">Ejemplo: uso de encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="260f5-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="260f5-187">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="260f5-187">Dataset properties</span></span>
<span data-ttu-id="260f5-188">Para ver una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="260f5-189">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="260f5-190">La sección typeProperties es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="260f5-191">Proporciona información como la ubicación y el formato de los datos del almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="260f5-192">La sección typeProperties del conjunto de datos de tipo **FileShare** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="260f5-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="260f5-193">Propiedad</span><span class="sxs-lookup"><span data-stu-id="260f5-193">Property</span></span> | <span data-ttu-id="260f5-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="260f5-194">Description</span></span> | <span data-ttu-id="260f5-195">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="260f5-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="260f5-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="260f5-196">folderPath</span></span> |<span data-ttu-id="260f5-197">Especifica la subruta de acceso a la carpeta.</span><span class="sxs-lookup"><span data-stu-id="260f5-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="260f5-198">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="260f5-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="260f5-199">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="260f5-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="260f5-200">Puede combinar esta propiedad con **partitionBy** para que las rutas de acceso de carpeta se basen en las fechas y horas de inicio y finalización del segmento.</span><span class="sxs-lookup"><span data-stu-id="260f5-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="260f5-201">Sí</span><span class="sxs-lookup"><span data-stu-id="260f5-201">Yes</span></span> |
| <span data-ttu-id="260f5-202">fileName</span><span class="sxs-lookup"><span data-stu-id="260f5-202">fileName</span></span> |<span data-ttu-id="260f5-203">Especifique el nombre del archivo en **folderPath** si quiere que la tabla haga referencia a un archivo específico de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="260f5-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="260f5-204">Si no especifica ningún valor para esta propiedad, la tabla apunta a todos los archivos de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="260f5-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="260f5-205">Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de la actividad, el nombre del archivo generado está en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="260f5-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="260f5-206">`Data.<Guid>.txt` (Ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="260f5-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="260f5-207">No</span><span class="sxs-lookup"><span data-stu-id="260f5-207">No</span></span> |
| <span data-ttu-id="260f5-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="260f5-208">fileFilter</span></span> |<span data-ttu-id="260f5-209">Especifique el filtro que se va a usar para seleccionar un subconjunto de archivos de folderPath, en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="260f5-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="260f5-210">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="260f5-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="260f5-211">Ejemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="260f5-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="260f5-212">Ejemplo 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="260f5-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="260f5-213">Tenga en cuenta que fileFilter es aplicable a un conjunto de datos de FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="260f5-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="260f5-214">No</span><span class="sxs-lookup"><span data-stu-id="260f5-214">No</span></span> |
| <span data-ttu-id="260f5-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="260f5-215">partitionedBy</span></span> |<span data-ttu-id="260f5-216">Puede usar partitionedBy para especificar un valor dinámico de folderPath/fileName para los datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="260f5-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="260f5-217">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="260f5-218">No</span><span class="sxs-lookup"><span data-stu-id="260f5-218">No</span></span> |
| <span data-ttu-id="260f5-219">formato</span><span class="sxs-lookup"><span data-stu-id="260f5-219">format</span></span> | <span data-ttu-id="260f5-220">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="260f5-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="260f5-221">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="260f5-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="260f5-222">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="260f5-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="260f5-223">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="260f5-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="260f5-224">No</span><span class="sxs-lookup"><span data-stu-id="260f5-224">No</span></span> |
| <span data-ttu-id="260f5-225">compresión</span><span class="sxs-lookup"><span data-stu-id="260f5-225">compression</span></span> | <span data-ttu-id="260f5-226">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="260f5-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="260f5-227">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="260f5-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="260f5-228">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="260f5-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="260f5-229">consulte [Formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="260f5-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="260f5-230">No</span><span class="sxs-lookup"><span data-stu-id="260f5-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="260f5-231">No se puede usar fileName y fileFilter a la vez.</span><span class="sxs-lookup"><span data-stu-id="260f5-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="260f5-232">Uso de la propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="260f5-232">Using partitionedBy property</span></span>
<span data-ttu-id="260f5-233">Como ya se ha indicado en la sección anterior, se puede especificar un valor dinámico de folderPath y filename para datos de series temporales con la propiedad **partitionedBy**, [funciones de Data Factory y las variables del sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="260f5-234">Para más información sobre los conjuntos de datos de series temporales, la programación y los segmentos, consulte los artículos [Creación de conjuntos de datos](data-factory-create-datasets.md), [Programación y ejecución](data-factory-scheduling-and-execution.md) y [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="260f5-235">Muestra 1:</span><span class="sxs-lookup"><span data-stu-id="260f5-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="260f5-236">En este ejemplo, {Slice} se reemplaza por el valor de la variable del sistema SliceStart de Data Factory en el formato (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="260f5-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="260f5-237">SliceStart hace referencia a la hora de inicio del segmento.</span><span class="sxs-lookup"><span data-stu-id="260f5-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="260f5-238">folderPath es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="260f5-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="260f5-239">Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="260f5-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="260f5-240">Ejemplo 2:</span><span class="sxs-lookup"><span data-stu-id="260f5-240">Sample 2:</span></span>

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

<span data-ttu-id="260f5-241">En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.</span><span class="sxs-lookup"><span data-stu-id="260f5-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="260f5-242">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="260f5-242">Copy activity properties</span></span>
<span data-ttu-id="260f5-243">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="260f5-244">Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="260f5-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="260f5-245">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="260f5-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="260f5-246">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="260f5-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="260f5-247">Si va a mover datos desde un sistema de archivos local, establezca el tipo de origen en la actividad de copia en **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="260f5-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="260f5-248">Del mismo modo, si va a mover datos hacia un sistema de archivos local, establezca el tipo de receptor de la actividad de copia en **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="260f5-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="260f5-249">Esta sección proporciona una lista de las propiedades compatibles con FileSystemSource y FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="260f5-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="260f5-250">**FileSystemSource** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="260f5-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="260f5-251">Propiedad</span><span class="sxs-lookup"><span data-stu-id="260f5-251">Property</span></span> | <span data-ttu-id="260f5-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="260f5-252">Description</span></span> | <span data-ttu-id="260f5-253">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="260f5-253">Allowed values</span></span> | <span data-ttu-id="260f5-254">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="260f5-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="260f5-255">recursive</span><span class="sxs-lookup"><span data-stu-id="260f5-255">recursive</span></span> |<span data-ttu-id="260f5-256">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="260f5-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="260f5-257">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="260f5-257">True, False (default)</span></span> |<span data-ttu-id="260f5-258">No</span><span class="sxs-lookup"><span data-stu-id="260f5-258">No</span></span> |

<span data-ttu-id="260f5-259">**FileSystemSink** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="260f5-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="260f5-260">Propiedad</span><span class="sxs-lookup"><span data-stu-id="260f5-260">Property</span></span> | <span data-ttu-id="260f5-261">Descripción</span><span class="sxs-lookup"><span data-stu-id="260f5-261">Description</span></span> | <span data-ttu-id="260f5-262">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="260f5-262">Allowed values</span></span> | <span data-ttu-id="260f5-263">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="260f5-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="260f5-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="260f5-264">copyBehavior</span></span> |<span data-ttu-id="260f5-265">Define el comportamiento de copia cuando el origen es BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="260f5-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="260f5-266">**PreserveHierarchy:**: conserva la jerarquía de archivos en la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="260f5-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="260f5-267">Es decir, la ruta de acceso relativa del archivo de origen a la carpeta de origen es la misma que la ruta de acceso relativa del archivo de destino a la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="260f5-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="260f5-268">**FlattenHierarchy:** todos los archivos de la carpeta de origen se crean en el primer nivel de la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="260f5-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="260f5-269">Los archivos de destino se crean con un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="260f5-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="260f5-270">**MergeFiles**: combina todos los archivos de la carpeta de origen en un archivo.</span><span class="sxs-lookup"><span data-stu-id="260f5-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="260f5-271">Si se especifica el nombre o el nombre del blob, el nombre de archivo combinado es el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="260f5-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="260f5-272">De lo contrario, es un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="260f5-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="260f5-273">No</span><span class="sxs-lookup"><span data-stu-id="260f5-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="260f5-274">Ejemplos de recursive y copyBehavior</span><span class="sxs-lookup"><span data-stu-id="260f5-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="260f5-275">En esta sección se describe el comportamiento resultante de la operación de copia para diferentes combinaciones de valores recursive y copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="260f5-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="260f5-276">valor recursive</span><span class="sxs-lookup"><span data-stu-id="260f5-276">recursive value</span></span> | <span data-ttu-id="260f5-277">valor copyBehavior</span><span class="sxs-lookup"><span data-stu-id="260f5-277">copyBehavior value</span></span> | <span data-ttu-id="260f5-278">Comportamiento resultante</span><span class="sxs-lookup"><span data-stu-id="260f5-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="260f5-279">true</span><span class="sxs-lookup"><span data-stu-id="260f5-279">true</span></span> |<span data-ttu-id="260f5-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="260f5-280">preserveHierarchy</span></span> |<span data-ttu-id="260f5-281">Para una carpeta de origen Folder1 con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="260f5-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="260f5-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-282">Folder1</span></span><br/><span data-ttu-id="260f5-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="260f5-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="260f5-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="260f5-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="260f5-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="260f5-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="260f5-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="260f5-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="260f5-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="260f5-289">la carpeta de destino Folder1 se crea con la misma estructura que el origen:</span><span class="sxs-lookup"><span data-stu-id="260f5-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="260f5-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-290">Folder1</span></span><br/><span data-ttu-id="260f5-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="260f5-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="260f5-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="260f5-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="260f5-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="260f5-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="260f5-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="260f5-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="260f5-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="260f5-297">true</span><span class="sxs-lookup"><span data-stu-id="260f5-297">true</span></span> |<span data-ttu-id="260f5-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="260f5-298">flattenHierarchy</span></span> |<span data-ttu-id="260f5-299">Para una carpeta de origen Folder1 con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="260f5-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="260f5-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-300">Folder1</span></span><br/><span data-ttu-id="260f5-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="260f5-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="260f5-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="260f5-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="260f5-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="260f5-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="260f5-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="260f5-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="260f5-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="260f5-307">la carpeta de destino Folder1 se crea con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="260f5-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="260f5-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-308">Folder1</span></span><br/><span data-ttu-id="260f5-309">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="260f5-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="260f5-310">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="260f5-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="260f5-311">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3</span><span class="sxs-lookup"><span data-stu-id="260f5-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="260f5-312">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4</span><span class="sxs-lookup"><span data-stu-id="260f5-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="260f5-313">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5</span><span class="sxs-lookup"><span data-stu-id="260f5-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="260f5-314">true</span><span class="sxs-lookup"><span data-stu-id="260f5-314">true</span></span> |<span data-ttu-id="260f5-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="260f5-315">mergeFiles</span></span> |<span data-ttu-id="260f5-316">Para una carpeta de origen Folder1 con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="260f5-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="260f5-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-317">Folder1</span></span><br/><span data-ttu-id="260f5-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="260f5-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="260f5-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="260f5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="260f5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="260f5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="260f5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="260f5-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="260f5-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="260f5-324">la carpeta de destino Folder1 se crea con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="260f5-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="260f5-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-325">Folder1</span></span><br/><span data-ttu-id="260f5-326">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="260f5-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="260f5-327">false</span><span class="sxs-lookup"><span data-stu-id="260f5-327">false</span></span> |<span data-ttu-id="260f5-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="260f5-328">preserveHierarchy</span></span> |<span data-ttu-id="260f5-329">Para una carpeta de origen Folder1 con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="260f5-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="260f5-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-330">Folder1</span></span><br/><span data-ttu-id="260f5-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="260f5-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="260f5-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="260f5-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="260f5-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="260f5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="260f5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="260f5-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="260f5-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="260f5-337">se crea la carpeta de destino Folder1 con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="260f5-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="260f5-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-338">Folder1</span></span><br/><span data-ttu-id="260f5-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="260f5-341">No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="260f5-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="260f5-342">false</span><span class="sxs-lookup"><span data-stu-id="260f5-342">false</span></span> |<span data-ttu-id="260f5-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="260f5-343">flattenHierarchy</span></span> |<span data-ttu-id="260f5-344">Para una carpeta de origen Folder1 con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="260f5-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="260f5-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-345">Folder1</span></span><br/><span data-ttu-id="260f5-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="260f5-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="260f5-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="260f5-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="260f5-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="260f5-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="260f5-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="260f5-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="260f5-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="260f5-352">se crea la carpeta de destino Folder1 con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="260f5-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="260f5-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-353">Folder1</span></span><br/><span data-ttu-id="260f5-354">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="260f5-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="260f5-355">&nbsp;&nbsp;&nbsp;&nbsp;nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="260f5-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="260f5-356">No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="260f5-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="260f5-357">false</span><span class="sxs-lookup"><span data-stu-id="260f5-357">false</span></span> |<span data-ttu-id="260f5-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="260f5-358">mergeFiles</span></span> |<span data-ttu-id="260f5-359">Para una carpeta de origen Folder1 con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="260f5-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="260f5-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-360">Folder1</span></span><br/><span data-ttu-id="260f5-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="260f5-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="260f5-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="260f5-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="260f5-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="260f5-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="260f5-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="260f5-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="260f5-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="260f5-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="260f5-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="260f5-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="260f5-367">se crea la carpeta de destino Folder1 con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="260f5-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="260f5-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="260f5-368">Folder1</span></span><br/><span data-ttu-id="260f5-369">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="260f5-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="260f5-370">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="260f5-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="260f5-371">No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="260f5-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="260f5-372">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="260f5-372">Supported file and compression formats</span></span>
<span data-ttu-id="260f5-373">Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="260f5-374">Ejemplos de JSON para copiar datos hacia un sistema de archivos y desde este</span><span class="sxs-lookup"><span data-stu-id="260f5-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="260f5-375">En los siguientes ejemplos se proporcionan definiciones JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="260f5-376">Muestran cómo copiar datos entre el sistema de archivos local y Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="260f5-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="260f5-377">Sin embargo, puede copiar datos *directamente* desde cualquiera de los orígenes y hasta cualquiera de los receptores enumerados en [orígenes y receptores compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="260f5-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="260f5-378">Ejemplo: Copia de datos de un sistema de archivos local a Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="260f5-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="260f5-379">En este ejemplo se muestra cómo copiar datos desde un sistema de archivos local hasta Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="260f5-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="260f5-380">El ejemplo consta de las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="260f5-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="260f5-381">Un servicio vinculado de tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="260f5-382">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="260f5-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="260f5-383">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="260f5-384">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="260f5-385">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="260f5-386">En el siguiente ejemplo se copian datos de series temporales de un sistema de archivos local hasta Azure Blob Storage cada hora.</span><span class="sxs-lookup"><span data-stu-id="260f5-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="260f5-387">Las propiedades JSON que se usan en estos ejemplos se describen en las secciones después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="260f5-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="260f5-388">Como primer paso, configure la puerta de enlace de administración de datos según las instrucciones que se describen en [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="260f5-389">**Servicio vinculado del servidor de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="260f5-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="260f5-390">Además, se recomienda usar la propiedad **encryptedCredential** en lugar de usar las propiedades **userid** y **password**.</span><span class="sxs-lookup"><span data-stu-id="260f5-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="260f5-391">Consulte [Servicio vinculado del sistema de archivos](#linked-service-properties) para más información sobre este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="260f5-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="260f5-392">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="260f5-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="260f5-393">**Conjunto de datos de entrada del sistema de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="260f5-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="260f5-394">Los datos se seleccionan de un archivo nuevo cada hora.</span><span class="sxs-lookup"><span data-stu-id="260f5-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="260f5-395">Las propiedades folderPath y fileName se determinan en función de la hora de inicio del segmento.</span><span class="sxs-lookup"><span data-stu-id="260f5-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="260f5-396">El valor `"external": "true"` informa a Data Factory de que el conjunto de datos es externo a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="260f5-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="260f5-397">**Conjunto de datos de salida de Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="260f5-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="260f5-398">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="260f5-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="260f5-399">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="260f5-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="260f5-400">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="260f5-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="260f5-401">**Actividad de copia en una canalización con el origen del sistema de archivos y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="260f5-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="260f5-402">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="260f5-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="260f5-403">En la definición de JSON de canalización, el tipo **source** se establece en **FileSystemSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="260f5-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="260f5-404">Ejemplo: Copia de datos desde Azure SQL Database a un sistema de archivos local</span><span class="sxs-lookup"><span data-stu-id="260f5-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="260f5-405">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="260f5-405">The following sample shows:</span></span>

* <span data-ttu-id="260f5-406">Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="260f5-407">Un servicio vinculado de tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="260f5-408">Un conjunto de datos de entrada de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="260f5-409">Un conjunto de datos de salida de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="260f5-410">Una canalización con una actividad de copia que usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) y [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="260f5-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="260f5-411">En el ejemplo se copian datos de series temporales de una tabla de Azure SQL a un sistema de archivos local cada hora.</span><span class="sxs-lookup"><span data-stu-id="260f5-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="260f5-412">Las propiedades JSON que se usan en estos ejemplos se describen en las secciones después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="260f5-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="260f5-413">**Servicio vinculado a Azure SQL Database:**</span><span class="sxs-lookup"><span data-stu-id="260f5-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="260f5-414">**Servicio vinculado del servidor de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="260f5-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="260f5-415">Además, se recomienda usar la propiedad **encryptedCredential** en lugar de usar las propiedades **userid** y **password**.</span><span class="sxs-lookup"><span data-stu-id="260f5-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="260f5-416">Consulte [Servicio vinculado del sistema de archivos](#linked-service-properties) para más información sobre este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="260f5-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="260f5-417">**Conjunto de datos de entrada SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="260f5-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="260f5-418">En el ejemplo se supone que ha creado una tabla "MyTable" en Azure SQL y que contiene una columna denominada "timestampcolumn" para los datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="260f5-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="260f5-419">El valor ``“external”: ”true”`` informa a Data Factory de que el conjunto de datos es externo a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="260f5-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="260f5-420">**Conjunto de datos de salida del sistema de archivos local:**</span><span class="sxs-lookup"><span data-stu-id="260f5-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="260f5-421">Los datos se copian en un archivo nuevo cada hora.</span><span class="sxs-lookup"><span data-stu-id="260f5-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="260f5-422">Los valores de folderPath y fileName del blob se determinan en función de la hora de inicio del segmento.</span><span class="sxs-lookup"><span data-stu-id="260f5-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

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

<span data-ttu-id="260f5-423">**Actividad de copia en una canalización con el origen de SQL y el receptor de sistema de archivos:**</span><span class="sxs-lookup"><span data-stu-id="260f5-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="260f5-424">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="260f5-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="260f5-425">En la definición de JSON de canalización, el tipo **source** se establece en **SqlSource** y el tipo **sink** en **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="260f5-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="260f5-426">La consulta SQL especificada para la propiedad **SqlReaderQuery** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="260f5-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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


<span data-ttu-id="260f5-427">También puede asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor en la definición de actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="260f5-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="260f5-428">Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="260f5-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="260f5-429">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="260f5-429">Performance and tuning</span></span>
 <span data-ttu-id="260f5-430">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Data Factory de Azure y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="260f5-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
