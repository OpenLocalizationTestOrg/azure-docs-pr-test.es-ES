---
title: ejemplos de almacenamiento de aaaAzure mediante .NET | Documentos de Microsoft
description: "Consulte, descargue y ejecute código de ejemplo y aplicaciones para Almacenamiento de Azure. Detectar Introducción ejemplos para blobs, colas, tablas y archivos, utilizando las bibliotecas cliente de almacenamiento de .NET de Hola."
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
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="79aa9-104">Ejemplos de Azure Storage con .NET</span><span class="sxs-lookup"><span data-stu-id="79aa9-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="79aa9-105">Índice de ejemplos .NET</span><span class="sxs-lookup"><span data-stu-id="79aa9-105">.NET sample index</span></span>

<span data-ttu-id="79aa9-106">Hello tabla siguiente proporciona una visión general de nuestros ejemplos hello y repositorio escenarios incluidas en cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="79aa9-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="79aa9-107">Haga clic en hello vínculos tooview Hola correspondiente código de ejemplo en GitHub.</span><span class="sxs-lookup"><span data-stu-id="79aa9-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="79aa9-108">Extremo</span><span class="sxs-lookup"><span data-stu-id="79aa9-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="79aa9-109">Escenario</span><span class="sxs-lookup"><span data-stu-id="79aa9-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="79aa9-110">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="79aa9-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="79aa9-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="79aa9-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="79aa9-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="79aa9-112">Append Blob</span></span></td> 
<td><span data-ttu-id="79aa9-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Ejemplo del método CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-114">Blob en bloques</span><span class="sxs-lookup"><span data-stu-id="79aa9-114">Block Blob</span></span></td>
<td><span data-ttu-id="79aa9-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-116">Cifrado de cliente</span><span class="sxs-lookup"><span data-stu-id="79aa9-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="79aa9-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Ejemplos de cifrado de blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-118">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="79aa9-118">Copy Blob</span></span></td>
<td><span data-ttu-id="79aa9-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="79aa9-120">Create Container</span></span></td>
<td><span data-ttu-id="79aa9-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="79aa9-122">Delete Blob</span></span></td>
<td><span data-ttu-id="79aa9-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="79aa9-124">Delete Container</span></span></td>
<td><span data-ttu-id="79aa9-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-126">Metadatos/propiedades/estadísticas de blobs</span><span class="sxs-lookup"><span data-stu-id="79aa9-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="79aa9-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-128">ACL/metadatos/propiedades de contenedor</span><span class="sxs-lookup"><span data-stu-id="79aa9-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="79aa9-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Aplicación web de la galería de fotos de Almacenamiento de blobs de Azure)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="79aa9-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="79aa9-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-132">Contenedor/blob de concesión</span><span class="sxs-lookup"><span data-stu-id="79aa9-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="79aa9-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-134">Contenedor/blob de lista</span><span class="sxs-lookup"><span data-stu-id="79aa9-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="79aa9-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-136">Blob en páginas</span><span class="sxs-lookup"><span data-stu-id="79aa9-136">Page Blob</span></span></td>
<td><span data-ttu-id="79aa9-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="79aa9-138">SAS</span><span class="sxs-lookup"><span data-stu-id="79aa9-138">SAS</span></span></td>
<td><span data-ttu-id="79aa9-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="79aa9-140">Propiedades de servicio</span><span class="sxs-lookup"><span data-stu-id="79aa9-140">Service Properties</span></span></td>
<td><span data-ttu-id="79aa9-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introducción a blobs</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="79aa9-142">Instantánea de blob</span><span class="sxs-lookup"><span data-stu-id="79aa9-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="79aa9-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a> (Copias de seguridad de discos de máquinas virtuales de Azure con instantáneas incrementales)</span><span class="sxs-lookup"><span data-stu-id="79aa9-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="79aa9-144"><b>Archivo</b></span><span class="sxs-lookup"><span data-stu-id="79aa9-144"><b>File</b></span></span></td>
<td><span data-ttu-id="79aa9-145">Crear recursos compartidos/directorios/archivos</span><span class="sxs-lookup"><span data-stu-id="79aa9-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="79aa9-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="79aa9-147">Eliminar recursos compartidos/directorios/archivos</span><span class="sxs-lookup"><span data-stu-id="79aa9-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="79aa9-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET (Introducción al servicio Archivo de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-149">Metadatos/propiedades de directorio</span><span class="sxs-lookup"><span data-stu-id="79aa9-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="79aa9-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-151">Descargar archivos</span><span class="sxs-lookup"><span data-stu-id="79aa9-151">Download Files</span></span></td> 
<td><span data-ttu-id="79aa9-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-153">Propiedades/metadatos/métricas de archivo</span><span class="sxs-lookup"><span data-stu-id="79aa9-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="79aa9-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-155">Propiedades de servicio de archivo</span><span class="sxs-lookup"><span data-stu-id="79aa9-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="79aa9-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-157">Directorios y archivos de lista</span><span class="sxs-lookup"><span data-stu-id="79aa9-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="79aa9-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="79aa9-159">Recursos compartidos de lista</span><span class="sxs-lookup"><span data-stu-id="79aa9-159">List Shares</span></span></td> 
<td><span data-ttu-id="79aa9-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="79aa9-161">Propiedades/metadatos/estadísticas de recurso compartido</span><span class="sxs-lookup"><span data-stu-id="79aa9-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="79aa9-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Ejemplo de File Storage .NET de Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="79aa9-163"><b>Cola</b></span><span class="sxs-lookup"><span data-stu-id="79aa9-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="79aa9-164">Agregar mensaje</span><span class="sxs-lookup"><span data-stu-id="79aa9-164">Add Message</span></span></td> 
<td><span data-ttu-id="79aa9-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-166">Cifrado de cliente</span><span class="sxs-lookup"><span data-stu-id="79aa9-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="79aa9-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Cifrado de cliente de Cola de Azure Storage en .NET</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-168">Crear colas</span><span class="sxs-lookup"><span data-stu-id="79aa9-168">Create Queues</span></span></td> 
<td><span data-ttu-id="79aa9-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-170">Eliminar mensaje/cola</span><span class="sxs-lookup"><span data-stu-id="79aa9-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="79aa9-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-172">Inspección de mensajes</span><span class="sxs-lookup"><span data-stu-id="79aa9-172">Peek Message</span></span></td> 
<td><span data-ttu-id="79aa9-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-174">ACL/metadatos/estadísticas de cola</span><span class="sxs-lookup"><span data-stu-id="79aa9-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="79aa9-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-176">Propiedades de Queue Service</span><span class="sxs-lookup"><span data-stu-id="79aa9-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="79aa9-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-178">Actualizar mensaje</span><span class="sxs-lookup"><span data-stu-id="79aa9-178">Update Message</span></span></td> 
<td><span data-ttu-id="79aa9-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="79aa9-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="79aa9-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="79aa9-181">Crear tabla</span><span class="sxs-lookup"><span data-stu-id="79aa9-181">Create Table</span></span></td> 
<td><span data-ttu-id="79aa9-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Administración de simultaneidad con Almacenamiento de Azure: aplicación de ejemplo</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-183">Eliminar entidad/tabla</span><span class="sxs-lookup"><span data-stu-id="79aa9-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="79aa9-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-185">Insertar/combinar/reemplazar entidad</span><span class="sxs-lookup"><span data-stu-id="79aa9-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="79aa9-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Administración de simultaneidad con Almacenamiento de Azure: aplicación de ejemplo</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="79aa9-187">Query Entities</span></span></td> 
<td><span data-ttu-id="79aa9-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-189">Consultar tablas</span><span class="sxs-lookup"><span data-stu-id="79aa9-189">Query Tables</span></span></td> 
<td><span data-ttu-id="79aa9-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-191">ACL/propiedades de tabla</span><span class="sxs-lookup"><span data-stu-id="79aa9-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="79aa9-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introducción a Azure Table Storage mediante .NET</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="79aa9-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="79aa9-193">Update Entity</span></span></td> 
<td><span data-ttu-id="79aa9-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Administración de simultaneidad con Almacenamiento de Azure: aplicación de ejemplo</a></span><span class="sxs-lookup"><span data-stu-id="79aa9-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="79aa9-195">Biblioteca de ejemplos de código de Azure</span><span class="sxs-lookup"><span data-stu-id="79aa9-195">Azure Code Samples library</span></span>

<span data-ttu-id="79aa9-196">biblioteca de ejemplo completo de hello tooview, vaya toohello [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=storage) library, que incluye ejemplos para el almacenamiento de Azure que puede descargar y ejecutar localmente.</span><span class="sxs-lookup"><span data-stu-id="79aa9-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="79aa9-197">Biblioteca de código de ejemplo de Hola proporciona código de ejemplo en formato zip.</span><span class="sxs-lookup"><span data-stu-id="79aa9-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="79aa9-198">Como alternativa, puede examinar y clonar el repositorio de GitHub de Hola para cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="79aa9-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="79aa9-199">Guías de introducción</span><span class="sxs-lookup"><span data-stu-id="79aa9-199">Getting started guides</span></span>

<span data-ttu-id="79aa9-200">Extraer del repositorio Hola siguiendo guías si desea obtener instrucciones sobre cómo tooinstall y empezar a trabajar con hello bibliotecas de cliente de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="79aa9-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="79aa9-201">Getting Started with Azure Blob Service in .NET (Introducción al servicio BLOB de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="79aa9-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="79aa9-202">Getting Started with Azure Queue Service in .NET (Introducción al servicio Cola de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="79aa9-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="79aa9-203">Getting Started with Azure Table Service in .NET (Introducción al servicio Tabla de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="79aa9-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="79aa9-204">Getting Started with Azure File Service in .NET (Introducción al servicio Archivo de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="79aa9-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="79aa9-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79aa9-205">Next steps</span></span>

<span data-ttu-id="79aa9-206">Para información sobre ejemplos para otros lenguajes:</span><span class="sxs-lookup"><span data-stu-id="79aa9-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="79aa9-207">Java: [ejemplos de Azure Storage con Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="79aa9-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="79aa9-208">Todos los otros lenguajes: [ejemplos de Azure Storage](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="79aa9-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
