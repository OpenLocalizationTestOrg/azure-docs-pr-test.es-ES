---
title: "formato de archivo de registro de importación y exportación de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca del formato de Hola Hola de archivos de registro creado cuando se ejecutan los pasos de un trabajo de servicio de importación y exportación."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="e7d2f-103">Formato del archivo de registro del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="e7d2f-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="e7d2f-104">Cuando Hola servicio de importación y exportación de Microsoft Azure realiza una acción en una unidad como parte de un trabajo de importación o un trabajo de exportación, los registros se escriben tooblock blobs en la cuenta de almacenamiento de hello asociada con ese trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="e7d2f-105">Hay dos registros que se pueden escribir Hola servicio de importación y exportación:</span><span class="sxs-lookup"><span data-stu-id="e7d2f-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="e7d2f-106">siempre se genera el registro de errores de Hello en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="e7d2f-107">Hello registro detallado no está habilitado de forma predeterminada, pero puede habilitarla mediante configuración hello `EnableVerboseLog` propiedad en un [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) operación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="e7d2f-108">Ubicación del archivo de registro</span><span class="sxs-lookup"><span data-stu-id="e7d2f-108">Log file location</span></span>  
<span data-ttu-id="e7d2f-109">Hola se escriben los registros tooblock blobs en el contenedor de Hola o el directorio virtual especificado por hello `ImportExportStatesPath` configuración, que puede establecer en un `Put Job` operación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="e7d2f-110">Hola ubicación toowhich Hola registros se escriben depende de cómo se especifica la autenticación para el trabajo de hello, junto con el valor de hello especificado para `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="e7d2f-111">Se puede especificar la autenticación para el trabajo de Hola a través de una clave de cuenta de almacenamiento o un contenedor SAS (firma de acceso compartido).</span><span class="sxs-lookup"><span data-stu-id="e7d2f-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="e7d2f-112">nombre Hola de hello contenedor o directorio virtual puede ser el nombre predeterminado de Hola de `waimportexport`, o en otro contenedor o nombre del directorio virtual que especifique.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="e7d2f-113">Hola tabla siguiente muestran opciones posibles de hello:</span><span class="sxs-lookup"><span data-stu-id="e7d2f-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="e7d2f-114">Método de autenticación</span><span class="sxs-lookup"><span data-stu-id="e7d2f-114">Authentication Method</span></span>|<span data-ttu-id="e7d2f-115">Valor de `ImportExportStatesPath`Element</span><span class="sxs-lookup"><span data-stu-id="e7d2f-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="e7d2f-116">Ubicación de blobs del registro</span><span class="sxs-lookup"><span data-stu-id="e7d2f-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="e7d2f-117">Clave de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e7d2f-117">Storage account key</span></span>|<span data-ttu-id="e7d2f-118">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-118">Default value</span></span>|<span data-ttu-id="e7d2f-119">Un contenedor denominado `waimportexport`, que es el contenedor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="e7d2f-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7d2f-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="e7d2f-121">Clave de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e7d2f-121">Storage account key</span></span>|<span data-ttu-id="e7d2f-122">Valor especificado por el usuario</span><span class="sxs-lookup"><span data-stu-id="e7d2f-122">User-specified value</span></span>|<span data-ttu-id="e7d2f-123">Un contenedor denominado por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-123">A container named by hello user.</span></span> <span data-ttu-id="e7d2f-124">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7d2f-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="e7d2f-125">SAS de contenedor</span><span class="sxs-lookup"><span data-stu-id="e7d2f-125">Container SAS</span></span>|<span data-ttu-id="e7d2f-126">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-126">Default value</span></span>|<span data-ttu-id="e7d2f-127">Un directorio virtual denominado `waimportexport`, que es nombre predeterminado de hello, debajo de contenedor de hello especificado en hello SAS.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="e7d2f-128">Por ejemplo, si especifica Hola SAS para trabajo de hello es `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, ubicación de registro de hello sería`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="e7d2f-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="e7d2f-129">SAS de contenedor</span><span class="sxs-lookup"><span data-stu-id="e7d2f-129">Container SAS</span></span>|<span data-ttu-id="e7d2f-130">Valor especificado por el usuario</span><span class="sxs-lookup"><span data-stu-id="e7d2f-130">User-specified value</span></span>|<span data-ttu-id="e7d2f-131">Un directorio virtual denominado por el usuario de hello, debajo de contenedor de hello especificado en hello SAS.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="e7d2f-132">Por ejemplo, si especifica Hola SAS para trabajo de hello es `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, y Hola especifica el directorio virtual se denomina `mylogblobs`, ubicación de registro de hello sería `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="e7d2f-133">Puede recuperar la dirección URL de Hola para error de Hola y el registro detallado por llamada hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="e7d2f-134">registros de Hello están disponibles una vez completado el procesamiento de unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="e7d2f-135">Formato de archivo de registro</span><span class="sxs-lookup"><span data-stu-id="e7d2f-135">Log file format</span></span>  
<span data-ttu-id="e7d2f-136">Hello formato para los registros se Hola mismo: un blob que contiene las descripciones XML de eventos de Hola que se produjeron mientras se copiaban blobs entre la unidad de disco duro de Hola y la cuenta del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="e7d2f-137">registro detallado de Hello contiene información completa sobre el estado de Hola de operación de copia de Hola para cada blob (para un trabajo de importación) o el archivo (para un trabajo de exportación), mientras que el registro de errores de hello contiene únicamente la información de Hola de blobs o archivos que encontraron errores durante Hola importar o exportar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="e7d2f-138">a continuación se muestra el formato de registro detallado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="e7d2f-139">registro de errores de Hello tiene Hola equivalente a la estructura, pero filtra las operaciones correctas.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="e7d2f-140">Hello tabla siguiente describe los elementos de Hola Hola del archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="e7d2f-141">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="e7d2f-141">XML Element</span></span>|<span data-ttu-id="e7d2f-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="e7d2f-142">Type</span></span>|<span data-ttu-id="e7d2f-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7d2f-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="e7d2f-144">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="e7d2f-144">XML Element</span></span>|<span data-ttu-id="e7d2f-145">Representa un registro de la unidad.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="e7d2f-146">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-146">Attribute, String</span></span>|<span data-ttu-id="e7d2f-147">versión de Hola del formato de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="e7d2f-148">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-148">String</span></span>|<span data-ttu-id="e7d2f-149">Hola número de serie del hardware de la unidad de disco.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="e7d2f-150">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-150">String</span></span>|<span data-ttu-id="e7d2f-151">Estado de procesamiento de la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-151">Status of hello drive processing.</span></span> <span data-ttu-id="e7d2f-152">Vea hello `Drive Status Codes` tabla de abajo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="e7d2f-153">Elemento XML anidado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-153">Nested XML element</span></span>|<span data-ttu-id="e7d2f-154">Representa un blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="e7d2f-155">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-155">String</span></span>|<span data-ttu-id="e7d2f-156">URI de blob de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="e7d2f-157">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-157">String</span></span>|<span data-ttu-id="e7d2f-158">archivo de toohello de la ruta de acceso relativa de Hello en unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="e7d2f-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="e7d2f-159">DateTime</span></span>|<span data-ttu-id="e7d2f-160">versión de instantánea de Hola de blob de hello, para un trabajo de exportación únicamente.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="e7d2f-161">Entero</span><span class="sxs-lookup"><span data-stu-id="e7d2f-161">Integer</span></span>|<span data-ttu-id="e7d2f-162">longitud total de Hola de blob de hello en bytes.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="e7d2f-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="e7d2f-163">DateTime</span></span>|<span data-ttu-id="e7d2f-164">fecha y hora de Hello blob Hola se modificó por última vez, para un trabajo de exportación únicamente.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="e7d2f-165">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-165">String</span></span>|<span data-ttu-id="e7d2f-166">Hola importar disposition del blob de hello, para un trabajo de importación únicamente.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="e7d2f-167">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-167">Attribute, String</span></span>|<span data-ttu-id="e7d2f-168">estado de saludo del programa Hola a disposición de importación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="e7d2f-169">Elemento XML anidado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-169">Nested XML element</span></span>|<span data-ttu-id="e7d2f-170">Representa una lista de los intervalos de páginas de un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="e7d2f-171">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="e7d2f-171">XML element</span></span>|<span data-ttu-id="e7d2f-172">Representa un intervalo de páginas.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="e7d2f-173">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="e7d2f-173">Attribute, Integer</span></span>|<span data-ttu-id="e7d2f-174">Desplazamiento inicial del intervalo de páginas de hello en blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="e7d2f-175">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="e7d2f-175">Attribute, Integer</span></span>|<span data-ttu-id="e7d2f-176">Longitud en bytes del intervalo de páginas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="e7d2f-177">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-177">Attribute, String</span></span>|<span data-ttu-id="e7d2f-178">Hash de MD5 codificado en Base16 del intervalo de páginas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="e7d2f-179">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-179">Attribute, String</span></span>|<span data-ttu-id="e7d2f-180">Estado de procesamiento de intervalo de páginas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="e7d2f-181">Elemento XML anidado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-181">Nested XML element</span></span>|<span data-ttu-id="e7d2f-182">Representa una lista de bloques de un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="e7d2f-183">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="e7d2f-183">XML element</span></span>|<span data-ttu-id="e7d2f-184">Representa un bloque.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="e7d2f-185">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="e7d2f-185">Attribute, Integer</span></span>|<span data-ttu-id="e7d2f-186">Desplazamiento inicial del bloque de hello en blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="e7d2f-187">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="e7d2f-187">Attribute, Integer</span></span>|<span data-ttu-id="e7d2f-188">Longitud en bytes del bloque de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="e7d2f-189">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-189">Attribute, String</span></span>|<span data-ttu-id="e7d2f-190">identificador de bloque de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="e7d2f-191">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-191">Attribute, String</span></span>|<span data-ttu-id="e7d2f-192">Hash de MD5 codificado en Base16 del bloque de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="e7d2f-193">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-193">Attribute, String</span></span>|<span data-ttu-id="e7d2f-194">Estado de procesamiento bloque Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="e7d2f-195">Elemento XML anidado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-195">Nested XML element</span></span>|<span data-ttu-id="e7d2f-196">Representa los metadatos del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="e7d2f-197">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-197">Attribute, String</span></span>|<span data-ttu-id="e7d2f-198">Estado de procesamiento de metadatos del blob Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="e7d2f-199">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-199">String</span></span>|<span data-ttu-id="e7d2f-200">Archivo de metadatos globales toohello de ruta de acceso relativa.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="e7d2f-201">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-201">Attribute, String</span></span>|<span data-ttu-id="e7d2f-202">Hash de MD5 codificado en Base16 del archivo de metadatos globales Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="e7d2f-203">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-203">String</span></span>|<span data-ttu-id="e7d2f-204">Archivo de metadatos de toohello de ruta de acceso relativa.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="e7d2f-205">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-205">Attribute, String</span></span>|<span data-ttu-id="e7d2f-206">Hash de MD5 codificado en Base16 del archivo de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="e7d2f-207">Elemento XML anidado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-207">Nested XML element</span></span>|<span data-ttu-id="e7d2f-208">Representa las propiedades de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="e7d2f-209">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-209">Attribute, String</span></span>|<span data-ttu-id="e7d2f-210">Estado de procesamiento de propiedades del blob hello, por ejemplo, archivo no encontrado, finalizado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="e7d2f-211">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-211">String</span></span>|<span data-ttu-id="e7d2f-212">Archivo de propiedades globales de toohello de ruta de acceso relativa.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="e7d2f-213">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-213">Attribute, String</span></span>|<span data-ttu-id="e7d2f-214">Hash de MD5 codificado en Base16 del archivo de propiedades globales de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="e7d2f-215">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-215">String</span></span>|<span data-ttu-id="e7d2f-216">Archivo de propiedades de toohello de ruta de acceso relativa.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="e7d2f-217">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-217">Attribute, String</span></span>|<span data-ttu-id="e7d2f-218">Hash de MD5 codificado en Base16 del archivo de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="e7d2f-219">String</span><span class="sxs-lookup"><span data-stu-id="e7d2f-219">String</span></span>|<span data-ttu-id="e7d2f-220">Estado de procesamiento Hola blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="e7d2f-221">Códigos de estado de unidad</span><span class="sxs-lookup"><span data-stu-id="e7d2f-221">Drive status codes</span></span>  
<span data-ttu-id="e7d2f-222">Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de una unidad.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="e7d2f-223">Código de estado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-223">Status code</span></span>|<span data-ttu-id="e7d2f-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7d2f-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e7d2f-225">unidad de Hello ha finalizado el procesamiento sin errores.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="e7d2f-226">unidad de Hello ha finalizado el procesamiento con advertencias en uno o más blobs según las disposiciones de importación de hello especificadas para los blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="e7d2f-227">Hola unidad ha finalizado con errores en uno o más blobs o fragmentos.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="e7d2f-228">Se encontró ningún disco en la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="e7d2f-229">primer volumen de datos Hello en el disco de hello no está en formato NTFS.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="e7d2f-230">Se produjo un error desconocido al realizar operaciones en la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="e7d2f-231">No se encuentra ningún volumen cifrable de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="e7d2f-232">BitLocker no está habilitado en el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="e7d2f-233">protector de clave de contraseña numérica de Hello no existe en el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="e7d2f-234">contraseña numérica de Hello especificada no puede desbloquear el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="e7d2f-235">Ha ocurrido error desconocido al tratar de volumen de hello toounlock.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="e7d2f-236">Se produjo un error desconocido al realizar operaciones de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="e7d2f-237">nombre de archivo de manifiesto de Hello no es válido.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="e7d2f-238">nombre de archivo de manifiesto de Hello es demasiado largo.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="e7d2f-239">no se encuentra el archivo de manifiesto de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="e7d2f-240">Archivo de manifiesto de toohello de acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="e7d2f-241">Hello archivo de manifiesto está dañado (contenido de hello no coincide con su hash).</span><span class="sxs-lookup"><span data-stu-id="e7d2f-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="e7d2f-242">contenido del manifiesto Hello no cumple el formato requerido de toohello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="e7d2f-243">unidad de Hello no coincide con el Id. de archivo de manifiesto de Hola Hola se lee en la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="e7d2f-244">Se ha producido un error de E/S de disco al leer desde el manifiesto de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="e7d2f-245">lista de blobs exportación de Hello no cumple el formato requerido de toohello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="e7d2f-246">Se prohíbe blobs de toohello de acceso de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="e7d2f-247">Esto podría ser debido a la clave de cuenta de almacenamiento de tooinvalid o un contenedor SAS.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="e7d2f-248">Y se produjo un error interno al procesar la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="e7d2f-249">Códigos de estado de blob</span><span class="sxs-lookup"><span data-stu-id="e7d2f-249">Blob status codes</span></span>  
<span data-ttu-id="e7d2f-250">Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de un blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="e7d2f-251">Código de estado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-251">Status code</span></span>|<span data-ttu-id="e7d2f-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7d2f-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e7d2f-253">blob de Hello ha finalizado el procesamiento sin errores.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="e7d2f-254">blob de Hello ha finalizado el procesamiento con errores en uno o más intervalos de páginas o bloques, metadatos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="e7d2f-255">nombre de archivo de Hello no es válido.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="e7d2f-256">nombre de archivo de Hello es demasiado largo.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="e7d2f-257">no se encuentra el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="e7d2f-258">Archivo de toohello de acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e7d2f-259">Error de solicitud de servicio de Blob de Hello tooaccess Hola blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="e7d2f-260">se prohíbe la solicitud del servicio Blob Hello tooaccess Hola blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="e7d2f-261">Esto podría ser debido a la clave de cuenta de almacenamiento de tooinvalid o un contenedor SAS.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="e7d2f-262">No se pudo blob de hello toorename (para un trabajo de importación) o archivo de hello (para un trabajo de exportación).</span><span class="sxs-lookup"><span data-stu-id="e7d2f-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="e7d2f-263">Se ha producido un cambio inesperado con blob hello (para un trabajo de exportación).</span><span class="sxs-lookup"><span data-stu-id="e7d2f-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="e7d2f-264">Hay una concesión en el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="e7d2f-265">Un disco o un error de E/S de red se ha producido durante el procesamiento de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="e7d2f-266">Se ha producido un error desconocido al procesar Hola blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="e7d2f-267">Códigos de estado de disposición de importación</span><span class="sxs-lookup"><span data-stu-id="e7d2f-267">Import disposition status codes</span></span>  
<span data-ttu-id="e7d2f-268">Hello tabla siguiente enumeran los códigos de estado de Hola para resolver una disposición de importación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="e7d2f-269">Código de estado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-269">Status code</span></span>|<span data-ttu-id="e7d2f-270">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7d2f-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="e7d2f-271">se ha creado el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="e7d2f-272">se ha cambiado el blob de Hola por disposición de importación de cambio de nombre.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="e7d2f-273">Hola `Blob/BlobPath` elemento contiene Hola URI de blob de hello cambia el nombre.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="e7d2f-274">se ha omitido el blob de Hola por `no-overwrite` disposición de importación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="e7d2f-275">blob de Hello ha sobrescrito un blob existente según `overwrite` disposición de importación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="e7d2f-276">Un error anterior ha detenido el procesamiento posterior de disposición de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="e7d2f-277">Códigos de estado de intervalo de páginas o bloque</span><span class="sxs-lookup"><span data-stu-id="e7d2f-277">Page range/block status codes</span></span>  
<span data-ttu-id="e7d2f-278">Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de un intervalo de páginas o un bloque.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="e7d2f-279">Código de estado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-279">Status code</span></span>|<span data-ttu-id="e7d2f-280">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7d2f-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e7d2f-281">intervalo de páginas de Hola o bloque ha finalizado el procesamiento sin errores.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="e7d2f-282">Hola bloque se ha confirmado, pero no en hello lista de bloques completa porque otros bloques dispone de error o colocar la propia lista de bloques completa ha.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="e7d2f-283">bloque de Hello es cargado pero no confirmado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="e7d2f-284">intervalo de páginas de Hola o bloque está dañado (contenido de hello no coincide con su hash).</span><span class="sxs-lookup"><span data-stu-id="e7d2f-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="e7d2f-285">Se ha encontrado un final de archivo inesperado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="e7d2f-286">Se ha encontrado un final de blob inesperado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e7d2f-287">Hola solicitud del servicio Blob tooaccess Hola intervalo de páginas o bloque ha fallado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="e7d2f-288">Un disco o un error de E/S de red se produjo al procesar el intervalo de páginas de Hola o bloque.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="e7d2f-289">Se ha producido un error desconocido al procesar el intervalo de páginas de Hola o bloque.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="e7d2f-290">Un error anterior ha detenido el procesamiento posterior de intervalo de páginas de Hola o un bloque.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="e7d2f-291">Códigos de estado de metadatos</span><span class="sxs-lookup"><span data-stu-id="e7d2f-291">Metadata status codes</span></span>  
<span data-ttu-id="e7d2f-292">Hello tabla siguiente enumeran los códigos de estado de Hola para procesar los metadatos de blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="e7d2f-293">Código de estado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-293">Status code</span></span>|<span data-ttu-id="e7d2f-294">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7d2f-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e7d2f-295">metadatos de Hello han finalizado el procesamiento sin errores.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="e7d2f-296">nombre de archivo de metadatos de Hello no es válido.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="e7d2f-297">nombre de archivo de metadatos de Hello es demasiado largo.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="e7d2f-298">no se encuentra el archivo de metadatos de Hello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="e7d2f-299">Archivo de metadatos de toohello de acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="e7d2f-300">archivo de metadatos de Hello está dañado (contenido de hello no coincide con su hash).</span><span class="sxs-lookup"><span data-stu-id="e7d2f-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="e7d2f-301">contenido de metadatos de Hello no cumple el formato requerido de toohello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="e7d2f-302">Escribir metadatos Hola que XML ha fallado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e7d2f-303">Error de solicitud de servicio de Blob de Hello tooaccess Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="e7d2f-304">Se ha producido un error de E/S de disco o de red al procesar metadatos Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="e7d2f-305">Se ha producido un error desconocido al procesar metadatos Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="e7d2f-306">Un error anterior ha detenido el procesamiento posterior de los metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="e7d2f-307">Códigos de estado de las propiedades</span><span class="sxs-lookup"><span data-stu-id="e7d2f-307">Properties status codes</span></span>  
<span data-ttu-id="e7d2f-308">Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de propiedades del blob.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="e7d2f-309">Código de estado</span><span class="sxs-lookup"><span data-stu-id="e7d2f-309">Status code</span></span>|<span data-ttu-id="e7d2f-310">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7d2f-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e7d2f-311">propiedades de Hello han finalizado el procesamiento sin errores.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="e7d2f-312">nombre de archivo de propiedades de Hello no es válido.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="e7d2f-313">nombre de archivo de propiedades de Hello es demasiado largo.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="e7d2f-314">no se encuentra el archivo de propiedades de Hello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="e7d2f-315">Archivo de propiedades de toohello de acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="e7d2f-316">archivo de propiedades de Hello está dañado (contenido de hello no coincide con su hash).</span><span class="sxs-lookup"><span data-stu-id="e7d2f-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="e7d2f-317">contenido de las propiedades Hello no cumplen el formato requerido de toohello.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="e7d2f-318">Escribir propiedades de hello que XML ha fallado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e7d2f-319">Error de solicitud de servicio de Blob de Hello tooaccess Hola propiedades.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="e7d2f-320">Se ha producido un error de E/S de disco o de red durante el procesamiento de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="e7d2f-321">Se produjo un error desconocido durante el procesamiento de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="e7d2f-322">Un error anterior ha detenido el procesamiento posterior de las propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="e7d2f-323">Registros de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e7d2f-323">Sample logs</span></span>  
<span data-ttu-id="e7d2f-324">Hola aquí te mostramos un ejemplo de registro detallado.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-324">hello following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="e7d2f-325">registro de errores de Hello correspondiente se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-325">hello corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="e7d2f-326">registro de errores de seguimiento de Hola para un trabajo de importación contiene un error sobre un archivo que no se encuentra en la unidad de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="e7d2f-327">Tenga en cuenta que el estado de saludo de los componentes siguientes es `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="e7d2f-328">Hello siguiente registro de errores para un trabajo de exportación indica que el contenido de blob Hola se ha escrito correctamente toohello unidad, pero que se produjo un error al exportar las propiedades del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7d2f-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="e7d2f-329">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7d2f-329">Next steps</span></span>
 
* [<span data-ttu-id="e7d2f-330">API de REST de Storage Import/Export</span><span class="sxs-lookup"><span data-stu-id="e7d2f-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
