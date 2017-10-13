---
title: 'Azure Stack Storage: Diferencias y consideraciones'
description: "Comprender las diferencias entre Azure Stack Storage y Azure Storage, junto con las consideraciones de implementación de Azure Stack."
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 381950321ac3a5ea8a43b76f3fba868da4be4682
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a><span data-ttu-id="651cd-103">Azure Stack Storage: Diferencias y consideraciones</span><span class="sxs-lookup"><span data-stu-id="651cd-103">Azure Stack Storage: Differences and considerations</span></span>

<span data-ttu-id="651cd-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="651cd-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="651cd-105">Azure Stack Storage es el conjunto de servicios de almacenamiento en la nube de Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="651cd-105">Azure Stack Storage is the set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="651cd-106">Azure Stack Storage proporciona blob, tabla, cola y funcionalidad de administración de cuenta con una semántica coherente de Azure.</span><span class="sxs-lookup"><span data-stu-id="651cd-106">Azure Stack Storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span>

<span data-ttu-id="651cd-107">En este artículo se resumen las diferencias entre Azure Stack Storage y Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="651cd-107">This article summarizes the known Azure Stack Storage differences from Azure Storage.</span></span> <span data-ttu-id="651cd-108">También se resumen otras consideraciones a tener en cuenta al implementar la Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="651cd-108">It also summarizes other considerations to keep in mind when you deploy Azure Stack.</span></span> <span data-ttu-id="651cd-109">Para obtener información acerca de las diferencias de alto nivel entre Azure y Azure Stack, consulte el tema [Consideraciones clave](azure-stack-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="651cd-109">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) topic.</span></span>

## <a name="cheat-sheet-storage-differences"></a><span data-ttu-id="651cd-110">Hoja de referencia rápida: Diferencias de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="651cd-110">Cheat sheet: Storage differences</span></span>

| <span data-ttu-id="651cd-111">Característica</span><span class="sxs-lookup"><span data-stu-id="651cd-111">Feature</span></span> | <span data-ttu-id="651cd-112">Azure (global)</span><span class="sxs-lookup"><span data-stu-id="651cd-112">Azure (global)</span></span> | <span data-ttu-id="651cd-113">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="651cd-113">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="651cd-114">File Storage</span><span class="sxs-lookup"><span data-stu-id="651cd-114">File storage</span></span>|<span data-ttu-id="651cd-115">Recursos compartidos de archivos SMB basado en la nube admitidos</span><span class="sxs-lookup"><span data-stu-id="651cd-115">Cloud-based SMB file shares supported</span></span>|<span data-ttu-id="651cd-116">Todavía no se admite</span><span class="sxs-lookup"><span data-stu-id="651cd-116">Not yet supported</span></span>
|<span data-ttu-id="651cd-117">Cifrado de datos en reposo</span><span class="sxs-lookup"><span data-stu-id="651cd-117">Data at rest encryption</span></span>|<span data-ttu-id="651cd-118">Cifrado de AES de 256 bits</span><span class="sxs-lookup"><span data-stu-id="651cd-118">256-bit AES encryption</span></span>|<span data-ttu-id="651cd-119">Todavía no se admite</span><span class="sxs-lookup"><span data-stu-id="651cd-119">Not yet supported</span></span>
|<span data-ttu-id="651cd-120">Tipo de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="651cd-120">Storage account type</span></span>|<span data-ttu-id="651cd-121">Cuentas de Azure Blob Storage y de uso general</span><span class="sxs-lookup"><span data-stu-id="651cd-121">General-purpose and Azure Blob storage accounts</span></span>|<span data-ttu-id="651cd-122">Solo para uso general</span><span class="sxs-lookup"><span data-stu-id="651cd-122">General-purpose only</span></span>
|<span data-ttu-id="651cd-123">Opciones de replicación</span><span class="sxs-lookup"><span data-stu-id="651cd-123">Replication options</span></span>|<span data-ttu-id="651cd-124">Almacenamiento con redundancia local, almacenamiento con redundancia geográfica, almacenamiento con redundancia geográfica con acceso de lectura y almacenamiento con redundancia de zona</span><span class="sxs-lookup"><span data-stu-id="651cd-124">Locally redundant storage, geo-redundant storage, read-access geo-redundant storage, and zone-redundant storage</span></span>|<span data-ttu-id="651cd-125">Almacenamiento con redundancia local</span><span class="sxs-lookup"><span data-stu-id="651cd-125">Locally redundant storage</span></span>
|<span data-ttu-id="651cd-126">Premium Storage</span><span class="sxs-lookup"><span data-stu-id="651cd-126">Premium storage</span></span>|<span data-ttu-id="651cd-127">Totalmente compatible</span><span class="sxs-lookup"><span data-stu-id="651cd-127">Fully supported</span></span>|<span data-ttu-id="651cd-128">Se pueden aprovisionar, pero no hay límite de rendimiento o garantía</span><span class="sxs-lookup"><span data-stu-id="651cd-128">Can be provisioned, but no performance limit or guarantee</span></span>
|<span data-ttu-id="651cd-129">Discos administrados</span><span class="sxs-lookup"><span data-stu-id="651cd-129">Managed disks</span></span>|<span data-ttu-id="651cd-130">Premium y estándar admitidos</span><span class="sxs-lookup"><span data-stu-id="651cd-130">Premium and standard supported</span></span>|<span data-ttu-id="651cd-131">Todavía no se admite</span><span class="sxs-lookup"><span data-stu-id="651cd-131">Not yet supported</span></span>
|<span data-ttu-id="651cd-132">Nombre de blob</span><span class="sxs-lookup"><span data-stu-id="651cd-132">Blob name</span></span>|<span data-ttu-id="651cd-133">1 024 caracteres (2 048 bytes)</span><span class="sxs-lookup"><span data-stu-id="651cd-133">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="651cd-134">880 caracteres (1 760 bytes)</span><span class="sxs-lookup"><span data-stu-id="651cd-134">880 characters (1,760 bytes)</span></span>
|<span data-ttu-id="651cd-135">Tamaño máximo de blob en bloque</span><span class="sxs-lookup"><span data-stu-id="651cd-135">Block blob max size</span></span>|<span data-ttu-id="651cd-136">4,75 TB (100 MB x 50 000 bloques)</span><span class="sxs-lookup"><span data-stu-id="651cd-136">4.75 TB (100 MB X 50,000 blocks)</span></span>|<span data-ttu-id="651cd-137">50 000 x 4 MB (195 GB aproximadamente)</span><span class="sxs-lookup"><span data-stu-id="651cd-137">50,000 X 4 MB (approx. 195 GB)</span></span>
|<span data-ttu-id="651cd-138">Copia de instantáneas incrementales del blob de página</span><span class="sxs-lookup"><span data-stu-id="651cd-138">Page blob incremental snapshot copy</span></span>|<span data-ttu-id="651cd-139">Blobs en páginas de Azure estándar y premium admitidos</span><span class="sxs-lookup"><span data-stu-id="651cd-139">Premium and standard Azure page blobs supported</span></span>|<span data-ttu-id="651cd-140">Todavía no se admite</span><span class="sxs-lookup"><span data-stu-id="651cd-140">Not yet supported</span></span>
|<span data-ttu-id="651cd-141">Tamaño máximo de blob en página</span><span class="sxs-lookup"><span data-stu-id="651cd-141">Page blob max size</span></span>|<span data-ttu-id="651cd-142">8 TB</span><span class="sxs-lookup"><span data-stu-id="651cd-142">8 TB</span></span>|<span data-ttu-id="651cd-143">1 TB</span><span class="sxs-lookup"><span data-stu-id="651cd-143">1 TB</span></span>
|<span data-ttu-id="651cd-144">Tamaño de página de blob en página</span><span class="sxs-lookup"><span data-stu-id="651cd-144">Page blob page size</span></span>|<span data-ttu-id="651cd-145">512 bytes</span><span class="sxs-lookup"><span data-stu-id="651cd-145">512 bytes</span></span>|<span data-ttu-id="651cd-146">4 KB</span><span class="sxs-lookup"><span data-stu-id="651cd-146">4 KB</span></span>
|<span data-ttu-id="651cd-147">Clave de partición de tabla y tamaño de clave de fila</span><span class="sxs-lookup"><span data-stu-id="651cd-147">Table partition key and row key size</span></span>|<span data-ttu-id="651cd-148">1 024 caracteres (2 048 bytes)</span><span class="sxs-lookup"><span data-stu-id="651cd-148">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="651cd-149">400 caracteres (800 bytes)</span><span class="sxs-lookup"><span data-stu-id="651cd-149">400 characters (800 bytes)</span></span>

### <a name="metrics"></a><span data-ttu-id="651cd-150">Métricas</span><span class="sxs-lookup"><span data-stu-id="651cd-150">Metrics</span></span>
<span data-ttu-id="651cd-151">También hay algunas diferencias con las métricas de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="651cd-151">There are also some differences with storage metrics:</span></span>
* <span data-ttu-id="651cd-152">Los datos de transacción de las métricas de almacenamiento no distinguirán el ancho de banda de red interna o externa.</span><span class="sxs-lookup"><span data-stu-id="651cd-152">The transaction data in storage metrics does not differentiate internal or external network bandwidth.</span></span>
* <span data-ttu-id="651cd-153">Los datos de transacción de las métricas de almacenamiento no incluyen el acceso de la máquina virtual a los discos montados.</span><span class="sxs-lookup"><span data-stu-id="651cd-153">The transaction data in storage metrics does not include virtual machine access to the mounted disks.</span></span>

## <a name="api-version"></a><span data-ttu-id="651cd-154">Versión de API</span><span class="sxs-lookup"><span data-stu-id="651cd-154">API version</span></span>
<span data-ttu-id="651cd-155">Solo las siguientes versiones son compatibles con Azure Stack Storage:</span><span class="sxs-lookup"><span data-stu-id="651cd-155">The following versions are supported with Azure Stack Storage:</span></span>

* <span data-ttu-id="651cd-156">Servicios de datos de Azure Storage: [Versión de API de REST de 05-04-2015](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="651cd-156">Azure Storage data services: [2015-04-05 REST API version](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span></span>
* <span data-ttu-id="651cd-157">Servicios de administración de Azure Storage: [ Versión preliminar de 01-05-2015, 15-06-2015 y 01-01-2016](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="651cd-157">Azure Storage management services: [2015-05-01-preview, 2015-06-15, and 2016-01-01](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span></span> 

## <a name="next-steps"></a><span data-ttu-id="651cd-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="651cd-158">Next steps</span></span>

* [<span data-ttu-id="651cd-159">Empezar a trabajar con herramientas de desarrollo de Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="651cd-159">Get started with Azure Stack Storage development tools</span></span>](azure-stack-storage-dev.md)
* [<span data-ttu-id="651cd-160">Introducción a Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="651cd-160">Introduction to Azure Stack Storage</span></span>](azure-stack-storage-overview.md)

