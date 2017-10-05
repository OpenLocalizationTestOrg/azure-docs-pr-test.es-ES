---
title: "Creación de un trabajo de importación para Azure Import/Export | Microsoft Docs"
description: "Obtenga información sobre cómo crear un trabajo de importación para el servicio Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="90144-103">Creación de un trabajo de importación para el servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="90144-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="90144-104">Para crear un trabajo de importación para el servicio Microsoft Azure Import/Export con la API de REST, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="90144-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="90144-105">Preparar las unidades con la herramienta Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="90144-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="90144-106">Obtener la ubicación a la que se va a enviar la unidad.</span><span class="sxs-lookup"><span data-stu-id="90144-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="90144-107">Crear el trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="90144-107">Creating the import job.</span></span>

-   <span data-ttu-id="90144-108">Enviar sus unidades de disco a Microsoft a través de un servicio de transporte admitido.</span><span class="sxs-lookup"><span data-stu-id="90144-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="90144-109">Actualizar el trabajo de importación con la información de envío.</span><span class="sxs-lookup"><span data-stu-id="90144-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="90144-110">Vea [Uso del servicio Microsoft Azure Import/Export para transferir datos a Blob Storage](storage-import-export-service.md) para leer una introducción al servicio Import/Export y ver un tutorial en el que se demuestra cómo usar [Azure Portal](https://portal.azure.com/) para crear y administrar trabajos de importación y exportación.</span><span class="sxs-lookup"><span data-stu-id="90144-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="90144-111">Preparación de las unidades con la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="90144-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="90144-112">Los pasos para preparar las unidades para un trabajo de importación son los mismos si crea el trabajo a través del portal o a través de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="90144-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="90144-113">A continuación se muestra una breve descripción general de cómo preparar la unidad.</span><span class="sxs-lookup"><span data-stu-id="90144-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="90144-114">Vea [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) (Referencia de la herramienta Azure Import/Export) para obtener las instrucciones completas.</span><span class="sxs-lookup"><span data-stu-id="90144-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="90144-115">Puede descargar la herramienta Azure Import/Export [aquí](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="90144-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="90144-116">La preparación de la unidad conlleva:</span><span class="sxs-lookup"><span data-stu-id="90144-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="90144-117">Identificar los datos que se van a importar.</span><span class="sxs-lookup"><span data-stu-id="90144-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="90144-118">Identificar los blobs de destino en Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="90144-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="90144-119">Usar la herramienta Azure Import/Export para copiar los datos en una o varias unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="90144-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="90144-120">La herramienta Azure Import/Export también genera un archivo de manifiesto para cada una de las unidades de disco mientras se prepara.</span><span class="sxs-lookup"><span data-stu-id="90144-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="90144-121">Un archivo de manifiesto contiene:</span><span class="sxs-lookup"><span data-stu-id="90144-121">A manifest file contains:</span></span>

-   <span data-ttu-id="90144-122">Una enumeración de todos los archivos pensados para la carga y las asignaciones de estos archivos en los blobs.</span><span class="sxs-lookup"><span data-stu-id="90144-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="90144-123">Sumas de comprobación de los segmentos de cada archivo.</span><span class="sxs-lookup"><span data-stu-id="90144-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="90144-124">Información sobre los metadatos y las propiedades para asociar a cada blob.</span><span class="sxs-lookup"><span data-stu-id="90144-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="90144-125">Una lista de la acción que se realizará si un blob que se va a cargar tiene el mismo nombre que un blob existente en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="90144-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="90144-126">Las opciones posibles son: a) sobrescribir el blob con el archivo, b) conservar el blob existente y omitir la carga del archivo, c) anexar un sufijo al nombre para que no entre en conflicto con otros archivos.</span><span class="sxs-lookup"><span data-stu-id="90144-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="90144-127">Obtención de la ubicación de envío</span><span class="sxs-lookup"><span data-stu-id="90144-127">Obtaining your shipping location</span></span>

<span data-ttu-id="90144-128">Antes de crear un trabajo de importación, necesita obtener un nombre de la ubicación de envío y una dirección mediante una llamada a la operación [List Locations](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="90144-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="90144-129">`List Locations` devolverá una lista de ubicaciones y sus direcciones de correo.</span><span class="sxs-lookup"><span data-stu-id="90144-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="90144-130">Puede seleccionar una ubicación de la lista devuelta y enviar las unidades de disco duro a esa dirección.</span><span class="sxs-lookup"><span data-stu-id="90144-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="90144-131">También puede usar la operación `Get Location` para obtener directamente la dirección de envío para una ubicación específica.</span><span class="sxs-lookup"><span data-stu-id="90144-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="90144-132">Siga los pasos siguientes para obtener la ubicación de envío:</span><span class="sxs-lookup"><span data-stu-id="90144-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="90144-133">Identifique el nombre de la ubicación de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="90144-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="90144-134">Este valor puede encontrarse en el campo **Ubicación** del **Panel** de la cuenta de almacenamiento de Azure Portal o puede consultarse mediante el uso de la operación [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties) de Service Management API.</span><span class="sxs-lookup"><span data-stu-id="90144-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="90144-135">Recupere la ubicación que está disponible para procesar esta cuenta de almacenamiento mediante una llamada a la operación `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="90144-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="90144-136">Si la propiedad `AlternateLocations` de la ubicación contiene la propia ubicación, entonces es apropiado usar esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="90144-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="90144-137">De lo contrario, vuelva a llamar a la operación `Get Location` con una de las ubicaciones alternativas.</span><span class="sxs-lookup"><span data-stu-id="90144-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="90144-138">La ubicación original podría estar cerrada temporalmente para el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="90144-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="90144-139">Creación del trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="90144-139">Creating the import job</span></span>
<span data-ttu-id="90144-140">Para crear el trabajo de importación, llame a la operación [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="90144-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="90144-141">Tiene que proporcionar la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="90144-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="90144-142">Un nombre para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="90144-142">A name for the job.</span></span>

-   <span data-ttu-id="90144-143">El nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="90144-143">The storage account name.</span></span>

-   <span data-ttu-id="90144-144">El nombre de la ubicación envío, obtenido en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="90144-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="90144-145">Un tipo de trabajo (importar).</span><span class="sxs-lookup"><span data-stu-id="90144-145">A job type (Import).</span></span>

-   <span data-ttu-id="90144-146">El remite al que deben enviarse las unidades de disco después de que se ha completado el trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="90144-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="90144-147">La lista de unidades del trabajo.</span><span class="sxs-lookup"><span data-stu-id="90144-147">The list of drives in the job.</span></span> <span data-ttu-id="90144-148">Para cada unidad, debe incluir la siguiente información que se obtuvo durante el paso de preparación de la unidad:</span><span class="sxs-lookup"><span data-stu-id="90144-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="90144-149">El Id. de unidad</span><span class="sxs-lookup"><span data-stu-id="90144-149">The drive Id</span></span>

    -   <span data-ttu-id="90144-150">La clave de BitLocker</span><span class="sxs-lookup"><span data-stu-id="90144-150">The BitLocker key</span></span>

    -   <span data-ttu-id="90144-151">La ruta de acceso relativa del archivo de manifiesto de la unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="90144-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="90144-152">Hash MD5 del archivo de manifiesto codificado en Base16</span><span class="sxs-lookup"><span data-stu-id="90144-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="90144-153">Envío de las unidades de disco</span><span class="sxs-lookup"><span data-stu-id="90144-153">Shipping your drives</span></span>
<span data-ttu-id="90144-154">Debe enviar las unidades de disco a la dirección que ha obtenido en el paso anterior, y debe proporcionar al servicio Import/Export el número de seguimiento del paquete.</span><span class="sxs-lookup"><span data-stu-id="90144-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="90144-155">Debe enviar las unidades de disco a través de un servicio de transporte admitido, que proporcionará un número de seguimiento del paquete.</span><span class="sxs-lookup"><span data-stu-id="90144-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="90144-156">Actualización del trabajo de importación con la información de envío</span><span class="sxs-lookup"><span data-stu-id="90144-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="90144-157">Cuando tenga el número de seguimiento, llame a la operación [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) para actualizar el nombre del transportista, el número de seguimiento del trabajo y el número de cuenta del transportista para el envío de devolución.</span><span class="sxs-lookup"><span data-stu-id="90144-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="90144-158">También puede especificar el número de unidades y la fecha de envío.</span><span class="sxs-lookup"><span data-stu-id="90144-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90144-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90144-159">Next steps</span></span>

* [<span data-ttu-id="90144-160">Uso de la API de REST del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="90144-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
