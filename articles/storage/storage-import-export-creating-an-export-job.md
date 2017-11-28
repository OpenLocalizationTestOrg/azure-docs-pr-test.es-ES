---
title: "Creación de un trabajo de exportación para Azure Import/Export | Microsoft Docs"
description: "Obtenga información sobre cómo crear un trabajo de exportación para el servicio Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="c7bfe-103">Creación de un trabajo de exportación para el servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="c7bfe-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="c7bfe-104">Para crear un trabajo de exportación para el servicio Microsoft Azure Import/Export con la API de REST, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c7bfe-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="c7bfe-105">Seleccionar los blobs que va a exportar.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="c7bfe-106">Obtener una ubicación de envío.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="c7bfe-107">Crear el trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-107">Creating the export job.</span></span>

-   <span data-ttu-id="c7bfe-108">Enviar sus unidades de disco vacías a Microsoft a través de un servicio de transporte admitido.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="c7bfe-109">Actualizar el trabajo de exportación con la información del paquete.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="c7bfe-110">Recibir las unidades de disco de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="c7bfe-111">Vea [Uso del servicio Microsoft Azure Import/Export para transferir datos a Blob Storage](storage-import-export-service.md) para leer una introducción al servicio Import/Export y ver un tutorial en el que se demuestra cómo usar [Azure Portal](https://portal.azure.com/) para crear y administrar trabajos de importación y exportación.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="c7bfe-112">Selección de los blobs que va a exportar</span><span class="sxs-lookup"><span data-stu-id="c7bfe-112">Selecting blobs to export</span></span>
 <span data-ttu-id="c7bfe-113">Para crear un trabajo de exportación, debe proporcionar una lista de blobs que desea exportar de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="c7bfe-114">Hay varias maneras de seleccionar los blobs que se van a exportar:</span><span class="sxs-lookup"><span data-stu-id="c7bfe-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="c7bfe-115">Puede usar una ruta de acceso relativa del blob para seleccionar un único blob y todas sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="c7bfe-116">Puede usar una ruta de acceso relativa del blob para seleccionar un único blob excluyendo sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="c7bfe-117">Puede usar una ruta de acceso relativa del blob y un tiempo de instantánea para seleccionar una sola instantánea.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="c7bfe-118">Puede utilizar un prefijo de blob para seleccionar todos los blobs e instantáneas con el prefijo especificado.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="c7bfe-119">Puede exportar todos los blobs e instantáneas en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="c7bfe-120">Para obtener más información sobre cómo especificar los blobs que va a exportar, vea la operación [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="c7bfe-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="c7bfe-121">Obtención de la ubicación de envío</span><span class="sxs-lookup"><span data-stu-id="c7bfe-121">Obtaining your shipping location</span></span>
<span data-ttu-id="c7bfe-122">Antes de crear un trabajo de exportación, necesita obtener un nombre de la ubicación de envío y una dirección mediante una llamada a la operación [Get Location](https://portal.azure.com) o [List Locations](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="c7bfe-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="c7bfe-123">`List Locations` devolverá una lista de ubicaciones y sus direcciones de correo.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="c7bfe-124">Puede seleccionar una ubicación de la lista devuelta y enviar las unidades de disco duro a esa dirección.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="c7bfe-125">También puede usar la operación `Get Location` para obtener directamente la dirección de envío para una ubicación específica.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="c7bfe-126">Siga los pasos siguientes para obtener la ubicación de envío:</span><span class="sxs-lookup"><span data-stu-id="c7bfe-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="c7bfe-127">Identifique el nombre de la ubicación de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="c7bfe-128">Este valor puede encontrarse en el campo **Ubicación** del **Panel** de la cuenta de almacenamiento del portal clásico o consultarse mediante el uso de la operación [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties) de Service Management API.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="c7bfe-129">Recupere la ubicación que está disponible para procesar esta cuenta de almacenamiento mediante una llamada a la operación `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="c7bfe-130">Si la propiedad `AlternateLocations` de la ubicación contiene la propia ubicación, entonces es apropiado usar esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="c7bfe-131">De lo contrario, vuelva a llamar a la operación `Get Location` con una de las ubicaciones alternativas.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="c7bfe-132">La ubicación original podría estar cerrada temporalmente para el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="c7bfe-133">Creación del trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="c7bfe-133">Creating the export job</span></span>
 <span data-ttu-id="c7bfe-134">Para crear el trabajo de exportación, llame a la operación [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="c7bfe-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="c7bfe-135">Tiene que proporcionar la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c7bfe-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="c7bfe-136">Un nombre para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-136">A name for the job.</span></span>

-   <span data-ttu-id="c7bfe-137">El nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-137">The storage account name.</span></span>

-   <span data-ttu-id="c7bfe-138">El nombre de la ubicación envío, obtenido en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="c7bfe-139">Un tipo de trabajo (exportar).</span><span class="sxs-lookup"><span data-stu-id="c7bfe-139">A job type (Export).</span></span>

-   <span data-ttu-id="c7bfe-140">El remite al que deben enviarse las unidades de disco después de que se ha completado el trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="c7bfe-141">La lista de blobs (o prefijos de blob) que se exportarán.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="c7bfe-142">Envío de las unidades de disco</span><span class="sxs-lookup"><span data-stu-id="c7bfe-142">Shipping your drives</span></span>
 <span data-ttu-id="c7bfe-143">A continuación, use la herramienta Azure Import/Export para determinar el número de unidades que necesita enviar, en función de los blobs seleccionados para la exportación y del tamaño de la unidad de disco.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="c7bfe-144">Vea [Referencia de la herramienta Azure Import-Export](storage-import-export-tool-how-to-v1.md) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="c7bfe-145">Introduzca todas las unidades de disco en un único paquete y envíelo a la dirección obtenida en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="c7bfe-146">Anote el número de seguimiento del paquete para el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="c7bfe-147">Debe enviar las unidades de disco a través de un servicio de transporte admitido, que proporcionará un número de seguimiento del paquete.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="c7bfe-148">Actualización del trabajo de exportación con la información del paquete</span><span class="sxs-lookup"><span data-stu-id="c7bfe-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="c7bfe-149">Cuando tenga el número de seguimiento, llame a la operación [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) para actualizar el nombre del transportista y el número de seguimiento del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="c7bfe-150">También puede especificar el número de unidades, el remite y la fecha de envío.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="c7bfe-151">Recepción del paquete</span><span class="sxs-lookup"><span data-stu-id="c7bfe-151">Receiving the package</span></span>
 <span data-ttu-id="c7bfe-152">Una vez procesado el trabajo de exportación, las unidades de disco se le devolverán con los datos cifrados.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="c7bfe-153">Puede recuperar la clave de BitLocker de cada una de las unidades de disco mediante una llamada a la operación [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="c7bfe-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="c7bfe-154">A continuación, puede desbloquear la unidad con la clave.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="c7bfe-155">El archivo de manifiesto de cada unidad contiene la lista de archivos de la unidad, así como la dirección del blob original de cada archivo.</span><span class="sxs-lookup"><span data-stu-id="c7bfe-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7bfe-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7bfe-156">Next steps</span></span>

* [<span data-ttu-id="c7bfe-157">Uso de la API de REST del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="c7bfe-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
