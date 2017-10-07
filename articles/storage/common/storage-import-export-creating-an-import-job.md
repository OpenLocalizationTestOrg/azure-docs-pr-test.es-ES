---
title: "aaaCreate un trabajo de importación para la importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una importación para hello servicio de importación y exportación de Microsoft Azure."
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
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="b8ab4-103">Crear un trabajo de importación para hello servicio de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="b8ab4-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="b8ab4-104">La creación de un trabajo de importación para servicio de importación y exportación de Microsoft Azure de hello mediante API de REST de hello implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="b8ab4-105">Preparar las unidades con hello herramienta de importación y exportación de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="b8ab4-106">Obtención Hola ubicación toowhich tooship Hola unidad.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="b8ab4-107">Creando un trabajo de importación Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-107">Creating hello import job.</span></span>

-   <span data-ttu-id="b8ab4-108">Envío Hola unidades tooMicrosoft a través de un servicio de transporte admitido.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="b8ab4-109">Actualizar el trabajo de importación de hello con hello detalles de envío.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="b8ab4-110">Vea [con hello importación y exportación de Microsoft Azure service tooTransfer datos tooBlob almacenamiento](storage-import-export-service.md) para obtener información general del servicio de importación y exportación de Hola y un tutorial que demuestra cómo hello toouse [portal de Azure](https://portal.azure.com/) toocreate y administrar la importación y exportación de trabajos.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="b8ab4-111">Preparar las unidades con hello herramienta de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="b8ab4-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="b8ab4-112">Hola pasos tooprepare unidades para un trabajo de importación se Hola mismo si crea Hola jobvia portal de Hola o a través de Hola API de REST.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="b8ab4-113">A continuación se muestra una breve descripción general de cómo preparar la unidad.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="b8ab4-114">Consulte toohello [referencia ExportTool de importación de Azure](storage-import-export-tool-how-to-v1.md) para obtener instrucciones completas.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="b8ab4-115">Puede descargar la herramienta de importación y exportación de Azure de hello [aquí](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="b8ab4-116">La preparación de la unidad conlleva:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="b8ab4-117">Identificación toobe Hola de datos importado.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="b8ab4-118">Identificar blobs de destino de hello en almacenamiento de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="b8ab4-119">Uso de hello toocopy de herramienta de importación y exportación de Azure su tooone de datos o más unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="b8ab4-120">Hola, herramienta de importación y exportación de Azure también generará un archivo de manifiesto para cada una de las unidades de hello mientras las prepara.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="b8ab4-121">Un archivo de manifiesto contiene:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-121">A manifest file contains:</span></span>

-   <span data-ttu-id="b8ab4-122">Una enumeración de todos los archivos de hello diseñada para la carga y las asignaciones de Hola de estos tooblobs de archivos.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="b8ab4-123">Sumas de comprobación de los segmentos de Hola de cada archivo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="b8ab4-124">Información sobre tooassociate de metadatos y propiedades de Hola a cada blob.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="b8ab4-125">Un listado de hello acción tootake si un blob que se está cargando tiene Hola mismo nombre como un blob existente en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="b8ab4-126">Las opciones posibles son: a) Hola blob se sobrescribe con el archivo hello, b) tenga blob existente de Hola y omite la carga de archivo hello, c) se anexa un nombre de sufijo toohello para que no esté en conflicto con otros archivos.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="b8ab4-127">Obtención de la ubicación de envío</span><span class="sxs-lookup"><span data-stu-id="b8ab4-127">Obtaining your shipping location</span></span>

<span data-ttu-id="b8ab4-128">Antes de crear un trabajo de importación, deberá tooobtain un nombre de la ubicación de envío y la dirección por llamada hello [ubicaciones de la lista](/rest/api/storageimportexport/listlocations) operación.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="b8ab4-129">`List Locations` devolverá una lista de ubicaciones y sus direcciones de correo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="b8ab4-130">Puede seleccionar una ubicación de hello devuelve la lista y enviar su dirección de toothat de unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="b8ab4-131">También puede usar hello `Get Location` Hola de tooobtain operación directamente de la dirección de una ubicación específica de envío.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="b8ab4-132">Siga los pasos de Hola por debajo de la ubicación de envío de Hola tooobtain:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="b8ab4-133">Identificar el nombre de Hola de ubicación de saludo de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="b8ab4-134">Este valor puede encontrarse en hello **ubicación** campo de la cuenta de almacenamiento de hello **panel** en hello Azure portal o puede consultarse mediante el uso de la operación de API de administración de servicio de hello [obtener almacenamiento Propiedades de la cuenta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="b8ab4-135">Recuperar ubicación hello tooprocess disponible esta cuenta de almacenamiento que realiza la llamada hello `Get Location` operación.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="b8ab4-136">Si hello `AlternateLocations` propiedad de ubicación de hello contiene la ubicación de hello propio, entonces es correcto toouse esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="b8ab4-137">De lo contrario, llame a hello `Get Location` operación de nuevo con una de las ubicaciones alternativas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="b8ab4-138">ubicación original de Hello podría estar cerrado temporalmente para el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="b8ab4-139">Crear trabajo de importación de Hola</span><span class="sxs-lookup"><span data-stu-id="b8ab4-139">Creating hello import job</span></span>
<span data-ttu-id="b8ab4-140">trabajo de importación de hello toocreate, llamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="b8ab4-141">Necesitará hello tooprovide siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="b8ab4-142">Un nombre para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-142">A name for hello job.</span></span>

-   <span data-ttu-id="b8ab4-143">nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-143">hello storage account name.</span></span>

-   <span data-ttu-id="b8ab4-144">Hola nombre de ubicación, obtenida en el paso anterior de Hola de envío.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="b8ab4-145">Un tipo de trabajo (importar).</span><span class="sxs-lookup"><span data-stu-id="b8ab4-145">A job type (Import).</span></span>

-   <span data-ttu-id="b8ab4-146">dirección de devolución de Hola que deben enviarse las unidades de hello después de que ha completado el trabajo de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="b8ab4-147">lista de Hola de unidades de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-147">hello list of drives in hello job.</span></span> <span data-ttu-id="b8ab4-148">Para cada unidad, debe incluir Hola siguiendo la información que se obtuvo durante el paso de preparación de unidad de hello:</span><span class="sxs-lookup"><span data-stu-id="b8ab4-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="b8ab4-149">Id. de unidad de Hola</span><span class="sxs-lookup"><span data-stu-id="b8ab4-149">hello drive Id</span></span>

    -   <span data-ttu-id="b8ab4-150">clave de BitLocker de Hola</span><span class="sxs-lookup"><span data-stu-id="b8ab4-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="b8ab4-151">Hola archivo de manifiesto ruta de acceso relativa en la unidad de disco duro de Hola</span><span class="sxs-lookup"><span data-stu-id="b8ab4-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="b8ab4-152">archivo de manifiesto algoritmo hash MD5 codificado en Hello Base16</span><span class="sxs-lookup"><span data-stu-id="b8ab4-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="b8ab4-153">Envío de las unidades de disco</span><span class="sxs-lookup"><span data-stu-id="b8ab4-153">Shipping your drives</span></span>
<span data-ttu-id="b8ab4-154">Debes enviar su dirección de toohello de unidades que obtuvo en el paso anterior de Hola y debe proporcionar Hola servicio de importación y exportación con hello seguimiento número de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="b8ab4-155">Debe enviar las unidades de disco a través de un servicio de transporte admitido, que proporcionará un número de seguimiento del paquete.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="b8ab4-156">Actualizar el trabajo de importación de hello con la información de envío</span><span class="sxs-lookup"><span data-stu-id="b8ab4-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="b8ab4-157">Una vez que el número de seguimiento, llame a hello [actualizar propiedades del trabajo](/api/storageimportexport/jobs#Jobs_Update) hello tooupdate de operación de envío nombre del operador, número de seguimiento de hello para el trabajo de Hola y número de cuenta del transportista hello para el trasvase de valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="b8ab4-158">Opcionalmente, puede especificar número de Hola de hello también la fecha de envío y las unidades.</span><span class="sxs-lookup"><span data-stu-id="b8ab4-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8ab4-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8ab4-159">Next steps</span></span>

* [<span data-ttu-id="b8ab4-160">Usar servicio de importación y exportación de hello API de REST</span><span class="sxs-lookup"><span data-stu-id="b8ab4-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
