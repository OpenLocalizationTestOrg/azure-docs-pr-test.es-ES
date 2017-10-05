---
title: Ejemplos de Azure Storage con .NET | Microsoft Docs
description: "Consulte, descargue y ejecute código de ejemplo y aplicaciones para Almacenamiento de Azure. Descubra ejemplos introductorios de blobs, colas, tablas y archivos, usando las bibliotecas de cliente de almacenamiento .NET."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 74777ed14ebb41ad31657f814e86724ff1e5e62e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="bfb22-104">Ejemplos de Azure Storage con .NET</span><span class="sxs-lookup"><span data-stu-id="bfb22-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="bfb22-105">Índice de ejemplos .NET</span><span class="sxs-lookup"><span data-stu-id="bfb22-105">.NET sample index</span></span>

<span data-ttu-id="bfb22-106">En la tabla siguiente se proporciona información general sobre el repositorio de ejemplos y los escenarios que abarca cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bfb22-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="bfb22-107">Haga clic en los vínculos para ver el código de ejemplo correspondiente en GitHub.</span><span class="sxs-lookup"><span data-stu-id="bfb22-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="bfb22-108">Extremo</span><span class="sxs-lookup"><span data-stu-id="bfb22-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="bfb22-109">Escenario</span><span class="sxs-lookup"><span data-stu-id="bfb22-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="bfb22-110">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bfb22-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="bfb22-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="bfb22-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="bfb22-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="bfb22-112">Append Blob</span></span></td> 
<td><span data-ttu-id="bfb22-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Ejemplo del método CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-114">Blob en bloques</span><span class="sxs-lookup"><span data-stu-id="bfb22-114">Block Blob</span></span></td>
<td><span data-ttu-id="bfb22-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-116">Cifrado de cliente</span><span class="sxs-lookup"><span data-stu-id="bfb22-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="bfb22-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Ejemplos de cifrado de blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-118">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="bfb22-118">Copy Blob</span></span></td>
<td><span data-ttu-id="bfb22-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="bfb22-120">Create Container</span></span></td>
<td><span data-ttu-id="bfb22-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="bfb22-122">Delete Blob</span></span></td>
<td><span data-ttu-id="bfb22-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="bfb22-124">Delete Container</span></span></td>
<td><span data-ttu-id="bfb22-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-126">Metadatos/propiedades/estadísticas de blobs</span><span class="sxs-lookup"><span data-stu-id="bfb22-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="bfb22-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-128">ACL/metadatos/propiedades de contenedor</span><span class="sxs-lookup"><span data-stu-id="bfb22-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="bfb22-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="bfb22-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="bfb22-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-132">Contenedor/blob de concesión</span><span class="sxs-lookup"><span data-stu-id="bfb22-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="bfb22-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-134">Contenedor/blob de lista</span><span class="sxs-lookup"><span data-stu-id="bfb22-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="bfb22-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-136">Blob en páginas</span><span class="sxs-lookup"><span data-stu-id="bfb22-136">Page Blob</span></span></td>
<td><span data-ttu-id="bfb22-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="bfb22-138">SAS</span><span class="sxs-lookup"><span data-stu-id="bfb22-138">SAS</span></span></td>
<td><span data-ttu-id="bfb22-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="bfb22-140">Propiedades de servicio</span><span class="sxs-lookup"><span data-stu-id="bfb22-140">Service Properties</span></span></td>
<td><span data-ttu-id="bfb22-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="bfb22-142">Instantánea de blob</span><span class="sxs-lookup"><span data-stu-id="bfb22-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="bfb22-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a> (Copias de seguridad de discos de máquinas virtuales de Azure con instantáneas incrementales)</span><span class="sxs-lookup"><span data-stu-id="bfb22-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="bfb22-144"><b>Archivo</b></span><span class="sxs-lookup"><span data-stu-id="bfb22-144"><b>File</b></span></span></td>
<td><span data-ttu-id="bfb22-145">Crear recursos compartidos/directorios/archivos</span><span class="sxs-lookup"><span data-stu-id="bfb22-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="bfb22-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="bfb22-147">Eliminar recursos compartidos/directorios/archivos</span><span class="sxs-lookup"><span data-stu-id="bfb22-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="bfb22-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET (Introducción al servicio Archivo de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-149">Metadatos/propiedades de directorio</span><span class="sxs-lookup"><span data-stu-id="bfb22-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="bfb22-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-151">Descargar archivos</span><span class="sxs-lookup"><span data-stu-id="bfb22-151">Download Files</span></span></td> 
<td><span data-ttu-id="bfb22-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-153">Propiedades/metadatos/métricas de archivo</span><span class="sxs-lookup"><span data-stu-id="bfb22-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="bfb22-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-155">Propiedades de servicio de archivo</span><span class="sxs-lookup"><span data-stu-id="bfb22-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="bfb22-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-157">Directorios y archivos de lista</span><span class="sxs-lookup"><span data-stu-id="bfb22-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="bfb22-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="bfb22-159">Recursos compartidos de lista</span><span class="sxs-lookup"><span data-stu-id="bfb22-159">List Shares</span></span></td> 
<td><span data-ttu-id="bfb22-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="bfb22-161">Propiedades/metadatos/estadísticas de recurso compartido</span><span class="sxs-lookup"><span data-stu-id="bfb22-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="bfb22-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="bfb22-163"><b>Cola</b></span><span class="sxs-lookup"><span data-stu-id="bfb22-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="bfb22-164">Agregar mensaje</span><span class="sxs-lookup"><span data-stu-id="bfb22-164">Add Message</span></span></td> 
<td><span data-ttu-id="bfb22-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-166">Cifrado de cliente</span><span class="sxs-lookup"><span data-stu-id="bfb22-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="bfb22-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Cifrado de cliente de Cola de Azure Storage en .NET</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-168">Crear colas</span><span class="sxs-lookup"><span data-stu-id="bfb22-168">Create Queues</span></span></td> 
<td><span data-ttu-id="bfb22-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-170">Eliminar mensaje/cola</span><span class="sxs-lookup"><span data-stu-id="bfb22-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="bfb22-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-172">Inspección de mensajes</span><span class="sxs-lookup"><span data-stu-id="bfb22-172">Peek Message</span></span></td> 
<td><span data-ttu-id="bfb22-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-174">ACL/metadatos/estadísticas de cola</span><span class="sxs-lookup"><span data-stu-id="bfb22-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="bfb22-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-176">Propiedades de Queue Service</span><span class="sxs-lookup"><span data-stu-id="bfb22-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="bfb22-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-178">Actualizar mensaje</span><span class="sxs-lookup"><span data-stu-id="bfb22-178">Update Message</span></span></td> 
<td><span data-ttu-id="bfb22-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="bfb22-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="bfb22-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="bfb22-181">Crear tabla</span><span class="sxs-lookup"><span data-stu-id="bfb22-181">Create Table</span></span></td> 
<td><span data-ttu-id="bfb22-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Administración de simultaneidad con Almacenamiento de Azure: aplicación de ejemplo</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-183">Eliminar entidad/tabla</span><span class="sxs-lookup"><span data-stu-id="bfb22-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="bfb22-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-185">Insertar/combinar/reemplazar entidad</span><span class="sxs-lookup"><span data-stu-id="bfb22-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="bfb22-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Administración de simultaneidad con Almacenamiento de Azure: aplicación de ejemplo</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="bfb22-187">Query Entities</span></span></td> 
<td><span data-ttu-id="bfb22-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-189">Consultar tablas</span><span class="sxs-lookup"><span data-stu-id="bfb22-189">Query Tables</span></span></td> 
<td><span data-ttu-id="bfb22-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-191">ACL/propiedades de tabla</span><span class="sxs-lookup"><span data-stu-id="bfb22-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="bfb22-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bfb22-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="bfb22-193">Update Entity</span></span></td> 
<td><span data-ttu-id="bfb22-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Administración de simultaneidad con Almacenamiento de Azure: aplicación de ejemplo</a></span><span class="sxs-lookup"><span data-stu-id="bfb22-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="bfb22-195">Biblioteca de ejemplos de código de Azure</span><span class="sxs-lookup"><span data-stu-id="bfb22-195">Azure Code Samples library</span></span>

<span data-ttu-id="bfb22-196">Para ver la biblioteca de completa de ejemplos, vaya a la biblioteca [Ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=storage), que incluye ejemplos para Azure Storage que puede descargar y ejecutar localmente.</span><span class="sxs-lookup"><span data-stu-id="bfb22-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="bfb22-197">En la biblioteca de código de ejemplo se proporciona código de ejemplo en formato zip.</span><span class="sxs-lookup"><span data-stu-id="bfb22-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="bfb22-198">Como alternativa, puede explorar y clonar el repositorio de GitHub para cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bfb22-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="bfb22-199">Guías de introducción</span><span class="sxs-lookup"><span data-stu-id="bfb22-199">Getting started guides</span></span>

<span data-ttu-id="bfb22-200">Consulte las guías siguientes si busca instrucciones sobre cómo instalar las bibliotecas de cliente de Azure Storage y cómo empezar a usarlas.</span><span class="sxs-lookup"><span data-stu-id="bfb22-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="bfb22-201">Getting Started with Azure Blob Service in .NET (Introducción al servicio BLOB de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="bfb22-201">Getting Started with Azure Blob Service in .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="bfb22-202">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="bfb22-202">Getting Started with Azure Queue Service in .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="bfb22-203">Getting Started with Azure Table Service in .NET (Introducción al servicio Tabla de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="bfb22-203">Getting Started with Azure Table Service in .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="bfb22-204">Getting Started with Azure File Service in .NET (Introducción al servicio Archivo de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="bfb22-204">Getting Started with Azure File Service in .NET</span></span>](../storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="bfb22-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfb22-205">Next steps</span></span>

<span data-ttu-id="bfb22-206">Para información sobre ejemplos para otros lenguajes:</span><span class="sxs-lookup"><span data-stu-id="bfb22-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="bfb22-207">Java: [ejemplos de Azure Storage con Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="bfb22-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="bfb22-208">Todos los otros lenguajes: [ejemplos de Azure Storage](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="bfb22-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
