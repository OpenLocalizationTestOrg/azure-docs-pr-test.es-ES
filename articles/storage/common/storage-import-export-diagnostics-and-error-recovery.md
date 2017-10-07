---
title: "aaaDiagnostics y recuperación de errores para los trabajos de importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable el registro detallado para la importación/exportación de Microsoft Azure service trabajos."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="29d18-103">Diagnóstico y recuperación de errores de los trabajos de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="29d18-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="29d18-104">Para cada unidad de disco procesada, Hola servicio de importación y exportación de Azure crea un registro de errores en la cuenta de almacenamiento de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="29d18-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="29d18-105">También puede habilitar el registro detallado por establecer hello `LogLevel` propiedad demasiado`Verbose` al llamar a hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) operaciones.</span><span class="sxs-lookup"><span data-stu-id="29d18-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="29d18-106">De forma predeterminada, se escriben los registros con el nombre de contenedor de tooa `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="29d18-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="29d18-107">Puede especificar un nombre diferente configuración hello `DiagnosticsPath` propiedad al llamar a hello `Put Job` o `Update Job Properties` las operaciones.</span><span class="sxs-lookup"><span data-stu-id="29d18-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="29d18-108">Hello registros se almacenan como blobs en bloques con hello sigue la convención de nomenclatura: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="29d18-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="29d18-109">Puede recuperar Hola URI de registros de Hola para un trabajo por llamada hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operación.</span><span class="sxs-lookup"><span data-stu-id="29d18-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="29d18-110">Hola URI para el registro detallado de Hola se devuelve en hello `VerboseLogUri` propiedad para cada unidad, mientras hello URI para el registro de errores de Hola se devuelve en hello `ErrorLogUri` propiedad.</span><span class="sxs-lookup"><span data-stu-id="29d18-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="29d18-111">Puede usar Hola Hola tooidentify de datos después de problemas de registro.</span><span class="sxs-lookup"><span data-stu-id="29d18-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="29d18-112">Errores en la unidad</span><span class="sxs-lookup"><span data-stu-id="29d18-112">Drive errors</span></span>

<span data-ttu-id="29d18-113">Hola siguientes elementos se clasifica como errores en la unidad:</span><span class="sxs-lookup"><span data-stu-id="29d18-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="29d18-114">Archivo de manifiesto de errores de acceso o lectura Hola</span><span class="sxs-lookup"><span data-stu-id="29d18-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="29d18-115">Claves de BitLocker incorrectas</span><span class="sxs-lookup"><span data-stu-id="29d18-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="29d18-116">Errores de escritura/lectura en la unidad</span><span class="sxs-lookup"><span data-stu-id="29d18-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="29d18-117">Errores de blobs</span><span class="sxs-lookup"><span data-stu-id="29d18-117">Blob errors</span></span>

<span data-ttu-id="29d18-118">Hola siguientes elementos se clasifica como errores de blobs:</span><span class="sxs-lookup"><span data-stu-id="29d18-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="29d18-119">Nombres o blobs incorrectos o conflictivos</span><span class="sxs-lookup"><span data-stu-id="29d18-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="29d18-120">Archivos que faltan</span><span class="sxs-lookup"><span data-stu-id="29d18-120">Missing files</span></span>

-   <span data-ttu-id="29d18-121">Blob no encontrado</span><span class="sxs-lookup"><span data-stu-id="29d18-121">Blob not found</span></span>

-   <span data-ttu-id="29d18-122">Archivos truncados (archivos de hello en el disco de hello son más pequeños que lo especificado en el manifiesto de hello)</span><span class="sxs-lookup"><span data-stu-id="29d18-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="29d18-123">Contenido de archivo dañado (para los trabajos de importación, se ha detectado una incoherencia de suma de comprobación MD5)</span><span class="sxs-lookup"><span data-stu-id="29d18-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="29d18-124">Archivos de metadatos y propiedades de blobs dañados (detectados con una incoherencia de suma de comprobación MD5)</span><span class="sxs-lookup"><span data-stu-id="29d18-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="29d18-125">Esquema incorrecto para propiedades del blob de Hola o archivos de metadatos</span><span class="sxs-lookup"><span data-stu-id="29d18-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="29d18-126">Puede haber casos donde algunas partes de un trabajo de importación o exportación no finaliza correctamente, mientras hello general trabajo finaliza.</span><span class="sxs-lookup"><span data-stu-id="29d18-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="29d18-127">En este caso, puede cargar o descargar Hola falta partes de los datos de Hola a través de red, o puede crear una nueva trabajo tootransfer Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="29d18-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="29d18-128">Vea hello [referencia de herramienta de importación y exportación de Azure](storage-import-export-tool-how-to-v1.md) toolearn cómo toorepair Hola datos a través de la red.</span><span class="sxs-lookup"><span data-stu-id="29d18-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29d18-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29d18-129">Next steps</span></span>

* [<span data-ttu-id="29d18-130">Usar servicio de importación y exportación de hello API de REST</span><span class="sxs-lookup"><span data-stu-id="29d18-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
