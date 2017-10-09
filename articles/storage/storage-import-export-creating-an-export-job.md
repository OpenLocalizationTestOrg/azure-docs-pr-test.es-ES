---
title: "aaaCreate una exportación de trabajo para la importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una exportación de trabajo para hello servicio de importación y exportación de Microsoft Azure."
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
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="aef6e-103">Crear un trabajo de exportación para hello servicio de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="aef6e-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="aef6e-104">La creación de un trabajo de exportación para servicio de importación y exportación de Microsoft Azure de hello mediante API de REST de hello implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="aef6e-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="aef6e-105">Seleccionar Hola blobs tooexport.</span><span class="sxs-lookup"><span data-stu-id="aef6e-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="aef6e-106">Obtener una ubicación de envío.</span><span class="sxs-lookup"><span data-stu-id="aef6e-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="aef6e-107">Crear trabajo de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-107">Creating hello export job.</span></span>

-   <span data-ttu-id="aef6e-108">Enviar su tooMicrosoft de unidades de disco vacías a través de un servicio de transporte admitido.</span><span class="sxs-lookup"><span data-stu-id="aef6e-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="aef6e-109">Actualizar el trabajo de exportación de hello con información del paquete Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="aef6e-110">Recibir hello las unidades de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aef6e-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="aef6e-111">Vea [con hello importación y exportación de Windows Azure service tooTransfer datos tooBlob almacenamiento](storage-import-export-service.md) para obtener información general del servicio de importación y exportación de Hola y un tutorial que demuestra cómo hello toouse [portal de Azure](https://portal.azure.com/) toocreate y administrar la importación y exportación de trabajos.</span><span class="sxs-lookup"><span data-stu-id="aef6e-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="aef6e-112">Seleccionar tooexport de blobs</span><span class="sxs-lookup"><span data-stu-id="aef6e-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="aef6e-113">toocreate un trabajo de exportación, deberá tooprovide una lista de blobs que desee tooexport desde su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="aef6e-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="aef6e-114">Hay varias maneras de tooselect toobe exportan los blobs:</span><span class="sxs-lookup"><span data-stu-id="aef6e-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="aef6e-115">Puede usar un tooselect de ruta de acceso relativa del blob un único blob y todas sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="aef6e-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="aef6e-116">Puede usar un tooselect de ruta de acceso relativa del blob en un solo blob, excepto sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="aef6e-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="aef6e-117">Puede usar una ruta de acceso relativa del blob y un tooselect de tiempo de la instantánea una sola instantánea.</span><span class="sxs-lookup"><span data-stu-id="aef6e-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="aef6e-118">Puede usar un tooselect de prefijo de blob todos los blobs e instantáneas con hello tiene prefijo.</span><span class="sxs-lookup"><span data-stu-id="aef6e-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="aef6e-119">Puede exportar todos los blobs e instantáneas en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="aef6e-120">Para obtener más información acerca de cómo especificar los blobs tooexport, vea hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación.</span><span class="sxs-lookup"><span data-stu-id="aef6e-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="aef6e-121">Obtención de la ubicación de envío</span><span class="sxs-lookup"><span data-stu-id="aef6e-121">Obtaining your shipping location</span></span>
<span data-ttu-id="aef6e-122">Antes de crear un trabajo de exportación, deberá tooobtain un nombre de la ubicación de envío y la dirección por llamada hello [obtener ubicación](https://portal.azure.com) o [ubicaciones de la lista](/rest/api/storageimportexport/listlocations) operación.</span><span class="sxs-lookup"><span data-stu-id="aef6e-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="aef6e-123">`List Locations` devolverá una lista de ubicaciones y sus direcciones de correo.</span><span class="sxs-lookup"><span data-stu-id="aef6e-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="aef6e-124">Puede seleccionar una ubicación de hello devuelve la lista y enviar su dirección de toothat de unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="aef6e-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="aef6e-125">También puede usar hello `Get Location` Hola de tooobtain operación directamente de la dirección de una ubicación específica de envío.</span><span class="sxs-lookup"><span data-stu-id="aef6e-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="aef6e-126">Siga los pasos de Hola por debajo de la ubicación de envío de Hola tooobtain:</span><span class="sxs-lookup"><span data-stu-id="aef6e-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="aef6e-127">Identificar el nombre de Hola de ubicación de saludo de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="aef6e-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="aef6e-128">Este valor puede encontrarse en hello **ubicación** campo de la cuenta de almacenamiento de hello **panel** en clásico de hello portal o puede consultarse mediante el uso de la operación de API de administración de servicio de hello [obtener Propiedades de la cuenta de almacenamiento](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="aef6e-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="aef6e-129">Recuperar esta cuenta de almacenamiento de ubicación de Hola que están disponibles tooprocess por llamada hello `Get Location` operación.</span><span class="sxs-lookup"><span data-stu-id="aef6e-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="aef6e-130">Si hello `AlternateLocations` propiedad de ubicación de hello contiene la ubicación de hello propio, entonces es correcto toouse esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="aef6e-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="aef6e-131">De lo contrario, llame a hello `Get Location` operación de nuevo con una de las ubicaciones alternativas de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="aef6e-132">ubicación original de Hello podría estar cerrado temporalmente para el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="aef6e-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="aef6e-133">Crear trabajo de exportación de Hola</span><span class="sxs-lookup"><span data-stu-id="aef6e-133">Creating hello export job</span></span>
 <span data-ttu-id="aef6e-134">trabajo de exportación de hello toocreate, llamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación.</span><span class="sxs-lookup"><span data-stu-id="aef6e-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="aef6e-135">Necesitará hello tooprovide siguiente información:</span><span class="sxs-lookup"><span data-stu-id="aef6e-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="aef6e-136">Un nombre para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-136">A name for hello job.</span></span>

-   <span data-ttu-id="aef6e-137">nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-137">hello storage account name.</span></span>

-   <span data-ttu-id="aef6e-138">Hola nombre de ubicación, obtenido en el paso anterior de Hola de envío.</span><span class="sxs-lookup"><span data-stu-id="aef6e-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="aef6e-139">Un tipo de trabajo (exportar).</span><span class="sxs-lookup"><span data-stu-id="aef6e-139">A job type (Export).</span></span>

-   <span data-ttu-id="aef6e-140">dirección de devolución de Hola que deben enviarse las unidades de hello después de que ha completado el trabajo de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="aef6e-141">Hola toobe de lista de blobs (o prefijos de blob) exportado.</span><span class="sxs-lookup"><span data-stu-id="aef6e-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="aef6e-142">Envío de las unidades de disco</span><span class="sxs-lookup"><span data-stu-id="aef6e-142">Shipping your drives</span></span>
 <span data-ttu-id="aef6e-143">A continuación, utilizar Hola herramienta de importación y exportación de Azure toodetermine Hola número de unidades que necesita toosend, en función de blobs de Hola que ha seleccionado toobe exportado y Hola tamaño de la unidad.</span><span class="sxs-lookup"><span data-stu-id="aef6e-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="aef6e-144">Vea hello [referencia de herramienta de importación y exportación de Azure](storage-import-export-tool-how-to-v1.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="aef6e-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="aef6e-145">Paquete Hola unidades en un único paquete y envíelas toohello dirección obtenida en hello el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="aef6e-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="aef6e-146">Tenga en cuenta Hola número del paquete para el paso siguiente Hola de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="aef6e-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="aef6e-147">Debe enviar las unidades de disco a través de un servicio de transporte admitido, que proporcionará un número de seguimiento del paquete.</span><span class="sxs-lookup"><span data-stu-id="aef6e-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="aef6e-148">Actualizar el trabajo de exportación de hello con la información del paquete</span><span class="sxs-lookup"><span data-stu-id="aef6e-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="aef6e-149">Una vez que el número de seguimiento, llame a hello [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) nombre de transportista de operación tooupdated Hola y el número de trabajo de Hola de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="aef6e-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="aef6e-150">También puede especificar número Hola de unidades, dirección de devolución de Hola y fecha de envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="aef6e-151">Recibir paquetes de saludo</span><span class="sxs-lookup"><span data-stu-id="aef6e-151">Receiving hello package</span></span>
 <span data-ttu-id="aef6e-152">Una vez procesado el trabajo de exportación, se devolverán las unidades de disco tooyou con los datos cifrados.</span><span class="sxs-lookup"><span data-stu-id="aef6e-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="aef6e-153">Puede recuperar la clave de BitLocker de Hola para cada una de las unidades de hello al Hola que realiza la llamada [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operación.</span><span class="sxs-lookup"><span data-stu-id="aef6e-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="aef6e-154">A continuación, puede desbloquear unidad Hola con clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef6e-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="aef6e-155">archivo de manifiesto de unidad de Hello en cada unidad de disco contiene la lista de Hola de archivos en la unidad de hello, así como la dirección del blob original Hola para cada archivo.</span><span class="sxs-lookup"><span data-stu-id="aef6e-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aef6e-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aef6e-156">Next steps</span></span>

* [<span data-ttu-id="aef6e-157">Usar servicio de importación y exportación de hello API de REST</span><span class="sxs-lookup"><span data-stu-id="aef6e-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
