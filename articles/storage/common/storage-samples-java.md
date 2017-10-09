---
title: ejemplos de almacenamiento de aaaAzure mediante Java | Documentos de Microsoft
description: "Consulte, descargue y ejecute código de ejemplo y aplicaciones para Almacenamiento de Azure. Detectar Introducción ejemplos para blobs, colas, tablas y archivos, utilizando las bibliotecas cliente de almacenamiento de Java de Hola."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="9cc95-104">Ejemplos de Azure Storage con Java</span><span class="sxs-lookup"><span data-stu-id="9cc95-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="9cc95-105">Índice de ejemplos Java</span><span class="sxs-lookup"><span data-stu-id="9cc95-105">Java sample index</span></span>

<span data-ttu-id="9cc95-106">Hello tabla siguiente proporciona una visión general de nuestros ejemplos hello y repositorio escenarios incluidas en cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cc95-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="9cc95-107">Haga clic en hello vínculos tooview Hola correspondiente código de ejemplo en GitHub.</span><span class="sxs-lookup"><span data-stu-id="9cc95-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="9cc95-108">Extremo</span><span class="sxs-lookup"><span data-stu-id="9cc95-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="9cc95-109">Escenario</span><span class="sxs-lookup"><span data-stu-id="9cc95-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="9cc95-110">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9cc95-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="9cc95-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="9cc95-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="9cc95-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="9cc95-112">Append Blob</span></span></td> 
<td><span data-ttu-id="9cc95-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-114">Blob en bloques</span><span class="sxs-lookup"><span data-stu-id="9cc95-114">Block Blob</span></span></td>
<td><span data-ttu-id="9cc95-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-116">Cifrado de cliente</span><span class="sxs-lookup"><span data-stu-id="9cc95-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="9cc95-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Introducción a Cifrado de cliente de Azure en Java</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-118">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="9cc95-118">Copy Blob</span></span></td>
<td><span data-ttu-id="9cc95-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="9cc95-120">Create Container</span></span></td>
<td><span data-ttu-id="9cc95-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="9cc95-122">Delete Blob</span></span></td>
<td><span data-ttu-id="9cc95-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="9cc95-124">Delete Container</span></span></td>
<td><span data-ttu-id="9cc95-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-126">Metadatos/propiedades/estadísticas de blobs</span><span class="sxs-lookup"><span data-stu-id="9cc95-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="9cc95-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-128">ACL/metadatos/propiedades de contenedor</span><span class="sxs-lookup"><span data-stu-id="9cc95-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="9cc95-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="9cc95-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="9cc95-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Ejemplo de pruebas de blob en páginas</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-132">Contenedor/blob de concesión</span><span class="sxs-lookup"><span data-stu-id="9cc95-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="9cc95-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-134">Contenedor/blob de lista</span><span class="sxs-lookup"><span data-stu-id="9cc95-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="9cc95-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-136">Blob en páginas</span><span class="sxs-lookup"><span data-stu-id="9cc95-136">Page Blob</span></span></td>
<td><span data-ttu-id="9cc95-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="9cc95-138">SAS</span><span class="sxs-lookup"><span data-stu-id="9cc95-138">SAS</span></span></td>
<td><span data-ttu-id="9cc95-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Ejemplo de pruebas de SAS</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="9cc95-140">Propiedades de servicio</span><span class="sxs-lookup"><span data-stu-id="9cc95-140">Service Properties</span></span></td>
<td><span data-ttu-id="9cc95-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="9cc95-142">Instantánea de blob</span><span class="sxs-lookup"><span data-stu-id="9cc95-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="9cc95-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="9cc95-144"><b>Archivo</b></span><span class="sxs-lookup"><span data-stu-id="9cc95-144"><b>File</b></span></span></td>
<td><span data-ttu-id="9cc95-145">Crear recursos compartidos/directorios/archivos</span><span class="sxs-lookup"><span data-stu-id="9cc95-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="9cc95-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9cc95-147">Eliminar recursos compartidos/directorios/archivos</span><span class="sxs-lookup"><span data-stu-id="9cc95-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="9cc95-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-149">Metadatos/propiedades de directorio</span><span class="sxs-lookup"><span data-stu-id="9cc95-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="9cc95-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-151">Descargar archivos</span><span class="sxs-lookup"><span data-stu-id="9cc95-151">Download Files</span></span></td> 
<td><span data-ttu-id="9cc95-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-153">Propiedades/metadatos/métricas de archivo</span><span class="sxs-lookup"><span data-stu-id="9cc95-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="9cc95-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-155">Propiedades de servicio de archivo</span><span class="sxs-lookup"><span data-stu-id="9cc95-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="9cc95-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-157">Directorios y archivos de lista</span><span class="sxs-lookup"><span data-stu-id="9cc95-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="9cc95-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9cc95-159">Recursos compartidos de lista</span><span class="sxs-lookup"><span data-stu-id="9cc95-159">List Shares</span></span></td> 
<td><span data-ttu-id="9cc95-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9cc95-161">Propiedades/metadatos/estadísticas de recurso compartido</span><span class="sxs-lookup"><span data-stu-id="9cc95-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="9cc95-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="9cc95-163"><b>Cola</b></span><span class="sxs-lookup"><span data-stu-id="9cc95-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="9cc95-164">Agregar mensaje</span><span class="sxs-lookup"><span data-stu-id="9cc95-164">Add Message</span></span></td> 
<td><span data-ttu-id="9cc95-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-166">Cifrado de cliente</span><span class="sxs-lookup"><span data-stu-id="9cc95-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="9cc95-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-168">Crear colas</span><span class="sxs-lookup"><span data-stu-id="9cc95-168">Create Queues</span></span></td> 
<td><span data-ttu-id="9cc95-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-170">Eliminar mensaje/cola</span><span class="sxs-lookup"><span data-stu-id="9cc95-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="9cc95-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-172">Inspección de mensajes</span><span class="sxs-lookup"><span data-stu-id="9cc95-172">Peek Message</span></span></td> 
<td><span data-ttu-id="9cc95-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-174">ACL/metadatos/estadísticas de cola</span><span class="sxs-lookup"><span data-stu-id="9cc95-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="9cc95-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introducción al servicio Cola de Azure en .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-176">Propiedades de Queue Service</span><span class="sxs-lookup"><span data-stu-id="9cc95-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="9cc95-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introducción al servicio Cola de Azure en .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-178">Actualizar mensaje</span><span class="sxs-lookup"><span data-stu-id="9cc95-178">Update Message</span></span></td> 
<td><span data-ttu-id="9cc95-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="9cc95-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="9cc95-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="9cc95-181">Crear tabla</span><span class="sxs-lookup"><span data-stu-id="9cc95-181">Create Table</span></span></td> 
<td><span data-ttu-id="9cc95-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-183">Eliminar entidad/tabla</span><span class="sxs-lookup"><span data-stu-id="9cc95-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="9cc95-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-185">Insertar/combinar/reemplazar entidad</span><span class="sxs-lookup"><span data-stu-id="9cc95-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="9cc95-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="9cc95-187">Query Entities</span></span></td> 
<td><span data-ttu-id="9cc95-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-189">Consultar tablas</span><span class="sxs-lookup"><span data-stu-id="9cc95-189">Query Tables</span></span></td> 
<td><span data-ttu-id="9cc95-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-191">ACL/propiedades de tabla</span><span class="sxs-lookup"><span data-stu-id="9cc95-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="9cc95-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cc95-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="9cc95-193">Update Entity</span></span></td> 
<td><span data-ttu-id="9cc95-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></span><span class="sxs-lookup"><span data-stu-id="9cc95-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="9cc95-195">Biblioteca de ejemplos de código de Azure</span><span class="sxs-lookup"><span data-stu-id="9cc95-195">Azure Code Samples library</span></span>

<span data-ttu-id="9cc95-196">biblioteca de ejemplo completo de hello tooview, vaya toohello [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=storage) library, que incluye ejemplos para el almacenamiento de Azure que puede descargar y ejecutar localmente.</span><span class="sxs-lookup"><span data-stu-id="9cc95-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="9cc95-197">Biblioteca de código de ejemplo de Hola proporciona código de ejemplo en formato zip.</span><span class="sxs-lookup"><span data-stu-id="9cc95-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="9cc95-198">Como alternativa, puede examinar y clonar el repositorio de GitHub de Hola para cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cc95-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="9cc95-199">Guías de introducción</span><span class="sxs-lookup"><span data-stu-id="9cc95-199">Getting started guides</span></span>

<span data-ttu-id="9cc95-200">Extraer del repositorio Hola siguiendo guías si desea obtener instrucciones sobre cómo tooinstall y empezar a trabajar con hello bibliotecas de cliente de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc95-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* <span data-ttu-id="9cc95-201">[Getting Started with Azure Blob Service in Java](../blobs/storage-java-how-to-use-blob-storage.md) (Introducción a Blob service de Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-201">[Getting Started with Azure Blob Service in Java](../blobs/storage-java-how-to-use-blob-storage.md)</span></span>
* [<span data-ttu-id="9cc95-202">Introducción al servicio Cola de Azure en .NET</span><span class="sxs-lookup"><span data-stu-id="9cc95-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* <span data-ttu-id="9cc95-203">[Getting Started with Azure Table service in Java](../../cosmos-db/table-storage-how-to-use-java.md) (Introducción a Azure Table service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-203">[Getting Started with Azure Table Service in Java](../../cosmos-db/table-storage-how-to-use-java.md)</span></span>
* <span data-ttu-id="9cc95-204">[Getting Started with Azure File Service in Java](../storage-java-how-to-use-file-storage.md) (Introducción a Azure File service en Java)</span><span class="sxs-lookup"><span data-stu-id="9cc95-204">[Getting Started with Azure File Service in Java](../storage-java-how-to-use-file-storage.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc95-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9cc95-205">Next steps</span></span>

<span data-ttu-id="9cc95-206">Para información sobre ejemplos para otros lenguajes:</span><span class="sxs-lookup"><span data-stu-id="9cc95-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="9cc95-207">.NET: [ejemplos de Azure Storage con .NET](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="9cc95-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="9cc95-208">Todos los otros lenguajes: [ejemplos de Azure Storage](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="9cc95-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
